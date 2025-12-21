Quickstart
==========

* goal
  * how MicroProfile Reactive Messaging works /
    * Reactive messaging | in memory
      * == ❌NO external broker❌ 

## Anatomy

* `Main`
  * == main entry point + (incoming and outgoing) messaging handlers

## how to start the application?

* set JDK v17
  * Reason: 🧠root project requires it🧠
* | [root path](../../)
  * `mvn clean install -DskipTests`
* | this path, 
  * `mvn compile exec:java`
    * Problems:
      * Problem1: "An exception occurred while executing the Java class. null: DeploymentException: ObserverException: 'java.lang.Object org.jboss.logging.Logger.getMessageLogger(java.lang.invoke.MethodHandles$Lookup, java.lang.Class, java.lang.String)' -> [Help 1]"
        * Solution: TODO:
    * check the output == incoming outgoing messages
    
        ```bash
        >> HELLO
        >> SMALLRYE
        >> REACTIVE
        >> MESSAGE
        ```

## Logging

* [documentation](../../documentation/src/main/docs/concepts/logging.md)

* [logging output configuration](src/main/resources/logging.properties)

* `mvn package exec:java -Dexec.mainClass=quickstart.Main -Djava.util.logging.config.file=./src/main/resources/logging.properties`
  * test logging output
