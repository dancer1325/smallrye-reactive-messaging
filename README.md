[![Maven Central](https://img.shields.io/maven-central/v/io.smallrye.reactive/smallrye-reactive-messaging)](https://search.maven.org/search?q=a:smallrye-reactive-messaging)
[![Continuous Integration Build](https://github.com/smallrye/smallrye-reactive-messaging/workflows/Continuous%20Integration%20Build/badge.svg)](https://github.com/smallrye/smallrye-reactive-messaging/actions)
[![License](https://img.shields.io/github/license/smallrye/smallrye-reactive-messaging.svg)](http://www.apache.org/licenses/LICENSE-2.0)

# Implementation of the MicroProfile Reactive Messaging specification

* implementation of the [Eclipse MicroProfile Reactive Messaging specification](https://github.com/eclipse/microprofile-reactive-messaging)
  * == CDI extension
  * uses
    * build
      * event-driven microservices
      * data streaming applications
  * provides
    * support for
      * [Apache Kafka](https://kafka.apache.org/)
      * [MQTT](http://mqtt.org/)
      * [AMQP](https://www.amqp.org/) 1.0
      * [Apache Camel](https://camel.apache.org/)
      * ...
    * way to inject _streams_ | CDI beans
      * -> link your [Reactive Messaging streams](https://github.com/eclipse/microprofile-reactive-streams-operators) |
        * [CDI](http://www.cdi-spec.org/) beans
        * [JAX-RS](https://github.com/eclipse-ee4j/jaxrs-api) resources

## [documentation](documentation/README.md)

## Branches

* main - 4.x development stream. Uses Vert.x 4.x, Microprofile 5.x, Mutiny 2.x and Jakarta 9
* 3.x - Previous development stream. Uses Vert.x 4.x and Microprofile 4.x
* 2.x - Not under development anymore. Uses Vert.x 3.x and Microprofile 3.x

## Getting started

### Prerequisites

* [PREREQUISITES.md](PREREQUISITES.md)

### how to build

```bash
mvn clean install
```

### How to start

* [examples/quickstart](examples/quickstart) project

## -- Based on -- 

* [Eclipse Vert.x](https://vertx.io/)
* [SmallRye Mutiny](https://github.com/smallrye/smallrye-mutiny)
* [SmallRye Reactive Stream Operators](https://github.com/smallrye/smallrye-reactive-streams-operators)
  * valid ALSO any Microprofile reactive streams operators implementation
* [Weld](https://weld.cdi-spec.org/)
  * valid ALSO any CDI

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
