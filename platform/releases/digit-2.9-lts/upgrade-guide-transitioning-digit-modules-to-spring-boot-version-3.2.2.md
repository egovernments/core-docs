# Upgrade Guide: Transitioning DIGIT Modules to Spring Boot Version 3.2.2

## Overview

This document contains information about the code changes that will be required in the registries for upgrading Spring boot and client libraries

## Steps

### POM Updates

1. Upgrade the Java version in the module to Java 17 before upgrading the Spring Boot version to 3.2.2. Following is a sample snippet of the Java version upgrade:

```
<properties>
    <java.version>17</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
</properties>
```

2. Upgrade spring-boot-starter-parent library to version 3.2.2. The code snippet of the dependency is shown below:

```
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.2</version>
    </parent>
```

3. Upgrade the Flyway library to version 9.22.3 for compatibility with Postgres 14. Below is the code snippet:

```
      <dependency>
         <groupId>org.flywaydb</groupId>
         <artifactId>flyway-core</artifactId>
         <version>9.22.3</version>
      </dependency>
```

4. Upgrade the _postgresql_ library to version 42.7.1:

```
       <dependency>
           <groupId>org.postgresql</groupId>
           <artifactId>postgresql</artifactId>
           <version>42.7.1</version>
        </dependency>
```

5. The tracer library is upgraded to springboot 3.2.2. The updates are available in the library version 2.9.0. If the module is using the tracer, upgrade the tracer version to 2.9.0 as shown below:

```
        <dependency>
            <groupId>org.egov.services</groupId>
            <artifactId>tracer</artifactId>
            <version>2.9.0</version>
        </dependency>
```

6. The _service-common_ library is upgraded and added in tracer. You don't have to explicitly upgrade the _services-common_ library and remove it from POM if you upgrade the tracer. In case your module is using only  _services-common,_ you can directly upgrade the version to 2.9.0
7. Use the below version of _JUnit_ which is compatible with Java 17:

```
          <dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>4.13.2</version>
               <scope>test</scope>
          </dependency>
```

8. If you are using the MDMS client library update the dependency version to 2.9.0 as shown below:

```
            <dependency>
               <groupId>org.egov</groupId>
               <artifactId>mdms-client</artifactId>
               <version>2.9.0</version>
            </dependency>
```

9. Update the Lombok version in the pom.xml to 1.8.22:

```
  <properties>
    <log4j2.version>2.17.1</log4j2.version>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <java.version>17</java.version>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <lombok.version>1.18.22</lombok.version>
  </properties>
```

10. If you are using net.minidev library, upgrade the version to `2.5.0`

```
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>2.5.0</version>
    </dependency>
```

11. To simplify dependency management and ensure version compatibility for Spring Kafka and Spring Redis dependencies use the spring-boot-starter-parent as your project's parent in the pom.xml. This ensures the _spring-kafka_ or _spring-redis_ dependency is included without specifying a version, Spring Boot will automatically provide a compatible version of the dependency. Following are code snippets of both the dependencies:

```
 <dependency>
      <groupId>org.springframework.kafka</groupId>
      <artifactId>spring-kafka</artifactId>
 </dependency>
```

```
 <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-redis</artifactId>
 </dependency>
```

_Note: If a tracer library is implemented there is no need to explicitly import spring-kafka._

### Registry Code Changes&#x20;

1.  Javax is deprecated and transitioning to Jakarta. Remove any Javax dependencies and update all Javax imports to Jakarta. For example, change imports like PostConstruct and valid to their Jakarta counterparts in all occurrences.\


    <figure><img src="../../../.gitbook/assets/Screenshot 2024-03-14 at 11.05.01 AM (1).png" alt=""><figcaption></figcaption></figure>
2. Remove the annotation _@javax.annotation.Generated_ which is now deprecated.
3. Update the Dockerfile for flyway migration with the below content:\
   \
   &#x20; `FROM egovio/flyway:10.7.1`

&#x20;         `COPY ./migration/main /flyway/sql`

&#x20;         `COPY migrate.sh /usr/bin/migrate.sh`

&#x20;         `RUN chmod +x /usr/bin/migrate.sh`

&#x20;         `ENTRYPOINT ["/usr/bin/migrate.sh"]`

3. Update the migrate.sh script:\
   &#x20;   `#!/bin/sh`

`flyway -url=$DB_URL -table=$SCHEMA_TABLE -user=$FLYWAY_USER -password=$FLYWAY_PASSWORD -locations=$FLYWAY_LOCATIONS -baselineOnMigrate=true   -outOfOrder=true migrate`

4. If you are using _spring-redis_, add the following configuration file:

```
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConfiguration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.connection.RedisStandaloneConfiguration;
import org.springframework.data.redis.connection.jedis.JedisConnectionFactory;
import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;
import org.springframework.data.redis.core.StringRedisTemplate;

@Configuration
public class RedisConfig {

    @Value("${spring.redis.host}")
    private String redisHost;

    @Value("${spring.redis.port}")
    private int redisPort;

    @Bean
    public RedisConnectionFactory redisConnectionFactory() {
        RedisConfiguration redisConfiguration = new RedisStandaloneConfiguration(redisHost, redisPort);
        return new LettuceConnectionFactory(redisConfiguration);
    }

    @Bean
    public StringRedisTemplate stringRedisTemplate(RedisConnectionFactory redisConnectionFactory) {
        return new StringRedisTemplate(redisConnectionFactory);
    }

}
```

5. Remove @SafeHtml annotation from the fields in POJO models as it is deprecated.
6. Update the Junit dependencies in the test cases as shown below:

<figure><img src="../../../.gitbook/assets/Screenshot 2024-03-04 at 7.03.06 PM.png" alt=""><figcaption><p> </p></figcaption></figure>
