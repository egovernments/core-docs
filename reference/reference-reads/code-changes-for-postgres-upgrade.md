---
description: Code changes required once Postgres is upgraded
---

# Code Changes For Postgres Upgrade

## Overview

The page contains changes needed in code after Postgres is upgraded to version 14.

## Steps

1. Update the _postgresql_ library as given in the below snippet:

```
    <dependency>
       <groupId>org.postgresql</groupId>
       <artifactId>postgresql</artifactId>
       <version>42.7.1</version>
    </dependency>
```

2. Update the flyway client library as per details given below:

```
    <dependency>
       <groupId>org.flywaydb</groupId>
       <artifactId>flyway-core</artifactId>
       <version>9.22.3</version>      
    </dependency>
```

3. Update the flyway _Dockerfile_ and _migrate.sh_ file as given below:

{% code title="Dockerfile" %}
```
COPY ./migration/main /flyway/sql
COPY migrate.sh /usr/bin/migrate.sh
RUN chmod +x /usr/bin/migrate.sh
ENTRYPOINT ["/usr/bin/migrate.sh"]
```
{% endcode %}

{% code title="migrate.sh" %}
```
#!/bin/sh
flyway -url=$DB_URL -table=$SCHEMA_TABLE -user=$FLYWAY_USER -password=$FLYWAY_PASSWORD -locations=$FLYWAY_LOCATIONS -baselineOnMigrate=true -outOfOrder=true migrate
```
{% endcode %}

