---
description: DIGIT Platform v 2.9.2
---

# DIGIT 2.9.2

This release addresses major gaps in **monitoring and tracing** that previously limited end-to-end visibility and operational insights.

### Limitations in older Monitoring and Tracing

#### 1. Only partial tracing is available

* Description: While some traces may exist for incoming requests, they stop once the request finishes writing a message to Kafka. Any subsequent handling on the consumer side remains untraced.
* Why it’s a problem:
  * Missing End-to-End Visibility: Without tracing beyond the Kafka boundary, it’s impossible to see how a request flows through the entire system—from one microservice into Kafka, and from there to any consuming service. This gap in the trace makes root cause analysis difficult when issues arise.
  * Incomplete Latency Analysis: You can’t accurately measure the time spent in different stages (producer vs. consumer) if traces end before consumer processing begins.
  * Harder Debugging: When investigating performance bottlenecks or errors, you won’t have a full picture of where a request failed or got delayed.

#### 2. Service-related metrics like DB connections, Tomcat threads, Kafka producers, and consumers are not available

* Description: The current setup does not provide standard service metrics, such as database connection pool usage, thread pool usage for Tomcat, or Kafka producer/consumer metrics (e.g., queue size, lag, or processing rates).
* Why it’s a problem:
  * Limited Operational Insights: Without these metrics, you cannot easily detect resource saturation (e.g., running out of database connections or Tomcat threads).
  * Performance Tuning Difficulty: Metrics on DB connections, threading, and Kafka help in understanding where bottlenecks occur—tuning thread pools, adjusting Kafka consumer concurrency, or scaling databases.
  * Proactive Issue Detection: Having no insight into Kafka producer/consumer metrics means you can’t see if the consumers are falling behind (consumer lag) or if producers are experiencing frequent retries.

### How Adopting OpenTelemetry and Micrometre Helps

* End-to-End Tracing: By instrumenting Kafka producers and consumers, you can maintain the trace context across message boundaries, ensuring full visibility from the first service to any downstream services.
* Detailed Metrics: Micrometre provides out-of-the-box instrumentation for common components (Tomcat threads, DB connection pools, Kafka, etc.), giving you critical performance insights.
* Unified Observability: OpenTelemetry’s approach—along with backends like Jaeger, Grafana, or Prometheus—allows you to bring traces, metrics, and even logs into a single pane of glass. This unified view accelerates troubleshooting and root cause analysis.

## Release Highlights

| Area                      | What changed                                                                                                                                                                              | Why it matters                                                                                                                                                           |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Distributed tracing**   | Re-instrumented every core service with **OpenTelemetry 1.35** (replacing the deprecated Jaeger client) and enabled automatic context propagation across Kafka producers _and_ consumers. | Complete end-to-end traces: a request is now visible from the first HTTP call all the way through asynchronous processing, eliminating the “black hole after Kafka” gap. |
| **Metrics**               | Added **Micrometer** with default binders for Tomcat, HikariCP, Kafka, JVM, and system metrics.                                                                                           | Gives operators real-time insight into thread pools, DB-connection utilisation, consumer lag, etc., enabling proactive alerting and capacity planning.                   |
| **Unified observability** | Traces, logs (optional), and metrics can now be shipped together via OTLP to Grafana / Prometheus / Jaeger for a single-pane-of-glass view.                                               | Faster root-cause analysis; no more jumping between siloed tools.                                                                                                        |

### Breaking / Behaviour-Changing Updates

| Change                                        | Impact                                                                      | Action required                                                                                          |
| --------------------------------------------- | --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Jaeger client removed**                     | The old Jaeger libraries are now _deprecated_ and incompatible with JDK 17. | Drop any explicit `io.jaegertracing` dependencies; follow the migration guide below.                     |
| **Tracer BOM bump**                           | Internal tracer module updated to **`2.9.2`** (was `2.9.1-SNAPSHOT`).       | Ensure all modules inherit this version to avoid shaded-JAR conflicts.                                   |
| **Datasource URL change for DB span capture** | JDBC URLs must be prefixed with `jdbc:otel:`.                               | Point `SPRING_DATASOURCE_URL` (or chart values) to the new `db-otel-url` as shown below.                 |
| **New config surface**                        | OpenTelemetry & Micrometer properties added.                                | Add the new keys to each service’s `application.properties` or Helm `values.yaml` (see migration guide). |

## Migration Guide

Refer to the [migration guide here ](migration-guide.md)to update services other than core to use OpenTelemetry for tracing.
