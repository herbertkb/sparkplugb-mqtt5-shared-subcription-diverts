# Sparkplug-B MQTT5 Shared Subscription with ActiveMQ Artemis Diverts

## Configuration

Add this to your ActiveMQ Artemis `broker.xml`:

```xml

<diverts>
    <divert name="shared">
        <address>spBv1.0/group01/NDATA/+</address>
        <forwarding-address>$share/share01/group01</forwarding-address>
        <routing-type>PASS</routing-type>
        <exclusive>false</exclusive>
    </divert>
</diverts>

<!-- see https://activemq.apache.org/components/artemis/documentation/latest/mqtt.html#wildcard-subscriptions -->
<wildcard-addresses>
    <delimiter>/</delimiter>
    <any-words>#</any-words>
    <single-word>+</single-word>
</wildcard-addresses>
```
---

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: <https://quarkus.io/>.

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:

```shell script
./mvnw quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at <http://localhost:8080/q/dev/>.

## Packaging and running the application

The application can be packaged using:

```shell script
./mvnw package
```

It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:

```shell script
./mvnw package -Dquarkus.package.jar.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using:

```shell script
./mvnw package -Dnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using:

```shell script
./mvnw package -Dnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/simple-tahu-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult <https://quarkus.io/guides/maven-tooling>.

## Related Guides

- Camel Timer ([guide](https://camel.apache.org/camel-quarkus/latest/reference/extensions/timer.html)): Generate messages in specified intervals using java.util.Timer
