# Logging

* goal
  * how to 
    * configure the loggers -- for -- various logging backends
    * write messages | log file

* -- based on -- [JBoss Logging](https://github.com/jboss-logging)
  * [logs management](https://jboss-logging.github.io/jboss-logging-tools/#introduction) 
  * uses
    * logging API

## Logging Backends

* JBoss Logging
  * == 👀logging *bridge*👀 /
    * integrates MULTIPLE log frameworks
      - JBoss LogManager (`jboss`)
      - Log4j 2 (`log4j2`)
      - Log4j 1 (`log4j`)
      - Slf4j (`slf4j`)
      - JDK logging (`jul`)

* steps
  * add the chosen framework | classpath
    * if there are >1 frameworks | classpath -> JBoss Logging picks
      * by default, the first found
      * the one / set by `org.jboss.logging.provider`

* / EACH logging library, specific
  * configuration file format 
  * *dependencies* 
  * log levels name

## Log Categories

* log categories
  * group messages -- from -- specific connectors, classes or components 
  * SAME / ALL frameworks 

| Main SmallRye Reactive Messaging Category                                     | Description                                                                       |
|----------------------------------------------|-----------------------------------------------------------------------------------|
| `io.smallrye.reactive.messaging`             | == ALL messages / written -- by -- SmallRye Reactive Messaging    |
| `io.smallrye.reactive.messaging.provider`    | ALL messages generated -- by the -- *core* (provider)       |
| `io.smallrye.reactive.messaging.kafka`       | ALL messages generated -- by the -- Kafka Connector.         |
| `io.smallrye.reactive.messaging.amqp`        | ALL messages generated -- by the -- AMQP Connector.          |
| `io.smallrye.reactive.messaging.jms`         | ALL messages generated -- by the -- JMS Connector.           |
| `io.smallrye.reactive.messaging.camel`       | ALL messages generated -- by the -- Camel Connector.         |
| `io.smallrye.reactive.messaging.mqtt`        | ALL messages generated -- by the -- MQTT (Client) Connector. |
| `io.smallrye.reactive.messaging.mqtt-server` | ALL messages generated -- by the -- MQTT (Server) Connector. |

* log level
  * name are defined -- by -- your logging framework
  * determine the amount and granularity of the log messages
  * assigned / EACH category
  * if you do NOT specify -> inherited -- from -- its parent category
    * -> set `io.smallrye.reactive.messaging` influences every SmallRye Reactive Messaging loggers 

## Message Code

* 's unique identifier code
* == `SRMSG` + numeric code

* _Example:_ `SRMSG00229`

    [2020-06-15 13:35:07] [INFO   ] SRMSG00229: Channel manager initializing...

## Recommended logging configurations

### Development

#### Log4J 1

```properties, title="log4j.properties"
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{HH:mm:ss,SSS} %-5p [%c] - %m%n

log4j.rootLogger=info, stdout
log4j.logger.io.smallrye.reactive.messaging=info
log4j.logger.org.jboss.weld=warn
```

#### Log4J 2

```xml, title="log4j2.xml"
<Configuration monitorInterval="60">
  <Properties>
    <Property name="log-path">PropertiesConfiguration</Property>
  </Properties>
  <Appenders>
    <Console name="Console-Appender" target="SYSTEM*OUT">
      <PatternLayout>
        <pattern>
          [%-5level] %d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %c{1} - %msg%n
        </pattern>>
      </PatternLayout>
    </Console>
  </Appenders>
  <Loggers>
    <Logger name="io.smallrye.reactive.messaging" level="info" additivity="false">
      <AppenderRef ref="Console-Appender"/>
    </Logger>
    <Logger name="org.jboss.weld" level="warn" additivity="false">
      <AppenderRef ref="Console-Appender"/>
    </Logger>
    <Root level="info">
      <AppenderRef ref="Console-Appender"/>
    </Root>
  </Loggers>
</Configuration>
```

#### JDK (JUL)

```properties,title="logging.properties"
handlers=java.util.logging.ConsoleHandler

java.util.logging.ConsoleHandler.level=FINEST
java.util.logging.ConsoleHandler.formatter=java.util.logging.SimpleFormatter
java.util.logging.SimpleFormatter.format=[%1$tF %1$tT] [%4$-7s] %5$s %n

.level=INFO
io.smallrye.reactive.messaging.level=INFO
org.jboss.weld.level=WARNING
```

#### LogBack via SLF4J*

```xml, title="logback.xml"
<configuration>
  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
      <Pattern>
        %d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
      </Pattern>
    </encoder>
  </appender>
  <logger name="io.smallrye.reactive.messaging" level="info" additivity="false">
    <appender-ref ref="STDOUT"/>
  </logger>
  <logger name="org.jboss.weld" level="warn" additivity="false">
    <appender-ref ref="STDOUT"/>
  </logger>
  <root level="info">
    <appender-ref ref="STDOUT"/>
  </root>
</configuration>
```

### Production

#### Log4J 1



*log4j.properties*



``` properties
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{HH:mm:ss,SSS} %-5p [%c] - %m%n

log4j.rootLogger=info, stdout
log4j.logger.io.smallrye.reactive.messaging=warn
log4j.logger.org.jboss.weld=error
```

#### Log4J 2



*log4j2.xml*



``` xml
<Configuration monitorInterval="60">
  <Properties>
    <Property name="log-path">PropertiesConfiguration</Property>
  </Properties>
  <Appenders>
    <Console name="Console-Appender" target="SYSTEM*OUT">
      <PatternLayout>
        <pattern>
          [%-5level] %d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %c{1} - %msg%n
        </pattern>>
      </PatternLayout>
    </Console>
  </Appenders>
  <Loggers>
    <Logger name="io.smallrye.reactive.messaging" level="warn" additivity="false">
      <AppenderRef ref="Console-Appender"/>
    </Logger>
    <Logger name="org.jboss.weld" level="error" additivity="false">
      <AppenderRef ref="Console-Appender"/>
    </Logger>
    <Root level="info">
      <AppenderRef ref="Console-Appender"/>
    </Root>
  </Loggers>
</Configuration>
```

#### JDK (JUL)



*logging.properties*



``` properties
handlers=java.util.logging.ConsoleHandler

java.util.logging.ConsoleHandler.level=INFO
java.util.logging.ConsoleHandler.formatter=java.util.logging.SimpleFormatter
java.util.logging.SimpleFormatter.format=[%1$tF %1$tT] [%4$-7s] %5$s %n

.level=INFO
io.smallrye.reactive.messaging.level=WARNING
org.jboss.weld.level=SEVERE
```



*logback.xml*



``` xml
<configuration>
  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
      <Pattern>
        %d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
      </Pattern>
    </encoder>
  </appender>
  <logger name="io.smallrye.reactive.messaging" level="warn" additivity="false">
    <appender-ref ref="STDOUT"/>
  </logger>
  <logger name="org.jboss.weld" level="error" additivity="false">
    <appender-ref ref="STDOUT"/>
  </logger>
  <root level="info">
    <appender-ref ref="STDOUT"/>
  </root>
</configuration>
```

