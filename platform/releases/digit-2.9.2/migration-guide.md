# Migration Guide

## Steps

Below are the steps to migrate from Jaeger Client to OpenTelemetry and Micrometre.

**Deprecation Note**\
As announced in the official [Jaeger Client Deprecation Notice](https://www.jaegertracing.io/docs/1.17/client-libraries/#deprecating-jaeger-clients), the Jaeger client is deprecated and does not support JDK 17.

**New Approach**\
OpenTelemetry and Micrometre libraries, along with their configurations, have been integrated into the tracer and are available in v2.9.1-SNAPSHOT.

**Enabling Tracing and Metrics**\
To enable tracing and Micrometre metrics in any service, you must:

1. Update your pom.xml to include the required dependencies.
2. Add specific configuration properties to your application.properties file.

**Changes in pom.xml**

1. Update the tracer library version to 2.9.1-SNAPSHOT.\
   \
   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSCfYKjpwp_RiAgd-rvSwxsl1Ozt_Abl-PNYvx3omcMIPA5K-N9ViWhIKUQfmasDEYDe4bTyREmdQkp2t59v-Dwox2Ob_vln3B6bG6cBvyB-QBNEYNfJ59VRifD_5o1sR8al-88Q?key=w4UKqbNyjS7A3js8JsoA1VYm)
2. Add dependency management for Optel libraries to set the correct version of child libraries. Add the below :

```
<dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-bom</artifactId>
        <version>1.35.0</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <dependency>
        <groupId>io.opentelemetry.instrumentation</groupId>
        <artifactId>opentelemetry-instrumentation-bom-alpha</artifactId>
        <version>2.1.0-alpha</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>
```

#### Changes in application.properties

New parameters need to be added in application.properties to provide the required configuration for micrometer and open telemetry. The following are the parameters that need to be added:

```
otel.traces.exporter=otlp
otel.service.name=egov-idgen
otel.logs.exporter=none
otel.metrics.exporter=none
otel.exporter.otlp.endpoint=http://jaeger-collector.tracing:4318
otel.exporter.otlp.protocol=http/protobuf
otel.instrumentation.kafka.enabled=true
otel.instrumentation.kafka.experimental-span-attributes=true
otel.instrumentation.http.server.ignore-urls=/egov-idgen/health,/egov-idgen/promethus
```

{% hint style="info" %}
**Note:** Changes the otel.service.name and otel.instrumentation.http.server.ignore-urls based on your service name. Other parameters can be added in Helm charts.
{% endhint %}

Add the otel DB URL in the env file:

```
db-otel-url: "jdbc:otel:postgresql://postgresql-lts.egov:5432/postgres"
```

Point the SPRING\_DATASOURCE\_URL of the service which has tracing enabled to the above URL.

{% hint style="info" %}
**Note:** For DB queries, tracing the DB URL needs to be updated by adding otel after jdbc in the URL, as shown above.
{% endhint %}

The following is the definition of the parameters:

<table><thead><tr><th width="223.51953125">Property</th><th>Description</th></tr></thead><tbody><tr><td>otel.traces.exporter</td><td><p>What it does: Assigns a service name to the application for trace grouping.</p><p>Why it's used: Backends (e.g., Jaeger, Zipkin) use this service name to organize and display telemetry data.</p></td></tr><tr><td>otel.service.name</td><td><p>What it does: Assigns a service name to the application for trace grouping.</p><p>Why it's used: Backends (e.g., Jaeger, Zipkin) use this service name to organize and display telemetry data.</p></td></tr><tr><td>otel.logs.exporter</td><td><p>What it does: Disables the export of log data.</p><p>Why it's used: If you do not want to send logs via OpenTelemetry (or do not have a suitable collector/log management configuration), you can disable log exporting.</p></td></tr><tr><td>otel.metrics.exporter</td><td><p>What it does: Disables the export of metric data through OpenTelemetry.</p><p>Why it's used: In some setups, metrics may be handled by Micrometer or another system. This configuration ensures no metric data is sent via OTLP.</p></td></tr><tr><td>otel.exporter.otlp.endpoint</td><td><p>What it does: Sets the endpoint for sending OTLP data. In this case, it points to the Jaeger collector’s OTLP endpoint.</p><p>Why it's used: The traces (and any other OTLP data if enabled) will be sent to Jaeger for storage and visualization.</p></td></tr><tr><td>otel.exporter.otlp.protocol</td><td><p>What it does: Specifies the protocol and serialization format (protobuf) for OTLP exports.</p><p>Why it's used: Ensures that data sent to the collector is in the correct format (HTTP over Protobuf) expected by the Jaeger or OTLP-compatible endpoint.</p></td></tr><tr><td>otel.instrumentation.kafka.enabled=true</td><td><p>What it does: Enables instrumentation for Kafka producers and consumers.</p><p>Why it's used: Automatically creates traces for Kafka interactions (producing, consuming messages), which can help you understand messaging flow in distributed systems</p></td></tr><tr><td>otel.instrumentation.kafka.experimental-span-attributes</td><td><p>What it does: Includes additional, possibly more detailed or experimental, span attributes for Kafka instrumentation.</p><p>Why it's used: Provides more visibility into Kafka operations for debugging or performance analysis</p></td></tr><tr><td>otel.instrumentation.http.server.ignore-urls</td><td><p>What it does: Configures the HTTP server instrumentation to skip tracing for the specified endpoints (health check, Prometheus endpoint, etc.).</p><p>Why it's used: Health and metrics endpoints often create unneeded trace noise, so they’re excluded</p></td></tr></tbody></table>
