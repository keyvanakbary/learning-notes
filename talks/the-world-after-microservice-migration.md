# [The World after Microservice Migration](https://www.youtube.com/watch?v=MxhcFPRkzlw)

## Motivation

Car-sharing application integration and aggregation into the system. Not caring about the technical debt, right to bite you in the ass at the end.

Providers as microservices. There is a gateway that either goes to providers or to an aggregator of internal services.

Providers can be extracted from the monolith. They needed some kind of dynamic routing for this.

## Service mesh

> A dedicated infrastructure layer for making service-to-service communication safe, fast and reliable.

* Dynamic routing
* Load-balancing
* Retryable failures
* Circuit-breaking
* Distributed tracing and metrics

We are already familiar with these concepts, the difference is that we want to extract all this behaviour from your application code.

* Linkerd v1

### Linkerd deployment models

* All services talk to a single linkerd instance
* Each service talk to a service linkerd sidecar. You can do as outgoing or incoming call.
    Then you can use Zipkin to analise and measure calls.

POST http://free2move.com/providers/drive2move/login

1) Identification. Where to route can be identified by header Host, the path, or by method like POST
2) Binding the services that will match with the identification, starting from top to bottom
3) Resolution, after we get a Consul namer por example, we resolve the IPs

Take into account that there is a little performance of having Linkerd intermediate between requests

#### Linkerd 2.0

Linkerd is not precisely light. You shouldn't be deploying it with your application. The idea is to have a proxy sidecar (data plane) and the whole Linkerd logic plus configuration in Kubernetes or in another place (control plane).

### Alernatives to Linkerd

* Istio, which looks like Linkerd 2.0
* Consul connect that now includes a service mesh with Istio

## Consumer-Driven Contract testing

[Pact](https://docs.pact.io/) framework for doing contract testing, the specification of the contract.

- How does a request/response format look
- Upstream/downstream
- The client defines the contract, and the provider the one that implements it

Pact generates contract files that you can upload to the Pact broker, you can see a graph of your services. On the build pipeline, we can run the tests with the contracts against real services. You can combine it with Swagger too.

For legacy applications you can use WireMock to check for recording incoming and outcoming requests.