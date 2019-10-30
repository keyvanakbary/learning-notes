# [Everything You Wanted to Know About Distributed Tracing](https://www.youtube.com/watch?v=HSgb7gOO1Ig)

## Software evolution

From

* Monolith
* On premise
* Single language
* Single stack
* Virtual machines

To

* Microservices
* Containers
* Multi cloud/hybrid
* Polyglot
* Serverless/Cloud functions

Better scalability or team performance and autonomy.

## New microservice architecture, new challenges

* **Observability**. A single instance does not give enough context to dedbug or understand stuff.
* Deployment / packaging
* Configuration management
* Debugging
* Secrets management

## Distributed tracing

Method used to profile and monitor applications, especially those built using microservices. It helps pinpoint where failures occur and what causes poor performance.

**Trace**: A trace is a tree of spans that follows the course of a request or system from it source to its ultimate destination. Each trace is a narrative that tells the request story as it travels throught he system.

**Span**: Are logical units of work in a distributed system. They have a name, a start time, and a duration. Each span captures important data points specific to the current process handling request.

**Context propagation**: Metadata information passed form one service to another so it can be collected later. Usually passed by headers

       Incoming request   ┌───────────┐   Outbound request   ┌───────────┐
    ─────────────────────>│ Service 1 │─────────────────────>│ Service 2 │
       trace-id = 123     └───────────┘   trace-id = 123     └───────────┘
       parent-id = nil                    parent-id = 1
       span-id = 1                        spain-id = 2

**Tags & Logs**: Both annotate the span with some contextual information.
* Tags typically apply to the whole span, while logs represent some events that happened during the span execution.
* A log always has a timestamp that falls within the span's start-end time interval.
* The tracing system does not explicitly track causality between logged events the way it keeps track of causality relationship between spans, because it can be inferred from the timestamps.

### What questions help distributed tracing answer?

* What services did a **request pass through**?
* What ocurred in **each service** for a given request? Root-cause analysis
* Where did the **error** happen? We are able to pinpoint where the error originated
* Where are the **bottlenecks**?
* What is the **critical path** for a request?
* Who should I **page**?

### Why isn't everybody using it?

* Not much education or not many publicised case studies on the benefits.
* Vendor Lock in is unacceptable: Instrumentation must be decoupled from vendors.
* Inconsistent APIs: Tracing semantics must not be language dependent.
* Handoff woes: Tracing libs in Project X do not handoff to tracing libs in Project Y.

### Meet OpenTelemetry (opentelemetry.io)

[OpenTelemetry](https://opentelemetry.io/) is a match between [OpenTracing](https://opentracing.io/) and [OpenCensus](https://opencensus.io/) projects

* **Single set of APIs** for tracing and metrics collection.
* **Standarised Context Propagation**.
* **Exporters** for sending data to backend of choice.
* **Collector** for smart traces & metrics aggregation.
* **Integrations** with popular web, RPC and storage frameworks.


#### Options

With agent
* It does bytecode instrumentation and sends the data automatically

Manually instrumenting your application

* You have to manually instrument to collect information

### Tracers

Open source

* [Jaeger](https://www.jaegertracing.io/)
* [Zipkin](https://zipkin.io/)
* [Lightstep](https://lightstep.com/products/tracing/)
* [Apache Skywalking](https://skywalking.apache.org/)

Hosted

* Honeycomb
* New Relic
* Data Dog
