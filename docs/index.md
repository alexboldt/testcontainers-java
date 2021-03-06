# TestContainers

> TestContainers is a Java library that supports JUnit tests, providing lightweight, throwaway instances of common databases, Selenium web browsers, or anything else that can run in a Docker container.

[![Circle CI](https://circleci.com/gh/testcontainers/testcontainers-java/tree/master.svg?style=svg)](https://circleci.com/gh/testcontainers/testcontainers-java/tree/master) [View on Github](https://github.com/testcontainers/testcontainers-java)

![Testcontainers logo](logo.png)

## Use Cases

TestContainers makes it easy to launch useful Docker containers for the duration of JUnit tests.

 * **Data access layer integration tests**: use a containerized instance of a MySQL, PostgreSQL or Oracle database to test your data access layer code for complete compatibility, but without requiring complex setup on developers' machines and safe in the knowledge that your tests will always start with a known DB state. Any other database type that can be containerized can also be used.
 * **Application integration tests**: for running your application in a short-lived test mode with dependencies, such as databases, message queues or web servers.
 * **UI/Acceptance tests**: use containerized web browsers, compatible with Selenium, for conducting automated UI tests. Each test can get a fresh instance of the browser, with no browser state, plugin variations or automated browser upgrades to worry about. And you get a video recording of each test session, or just each session where tests failed.

## Usage

### Prerequisites

Docker or docker-machine (for OS X) must be installed on the machine you are running tests on. TestContainers currently requires JDK 1.8 and is compatible with JUnit.

### Usage modes

* [Temporary database containers](usage/database_containers.md) - specialized MySQL, PostgreSQL and Oracle XE container support
* [Webdriver containers](usage/webdriver_containers.md) - run a Dockerized Chrome or Firefox browser ready for Selenium/Webdriver operations - complete with automatic video recording
* [Generic containers](usage/generic_containers.md) - run any Docker container as a test dependency
* [Docker compose](usage/docker_compose.md) - reuse services defined in a Docker Compose YAML file

## Maven dependencies

TestContainers is distributed in a handful of Maven modules:

* **testcontainers** for just core functionality and generic containers support
* **mysql**, **postgresql** or **oracle-xe** for database container support
* **selenium** for selenium/webdriver support
* **docker-compose** for Docker Compose support
* **nginx** for nginx container support

In the dependency description below, replace `--artifact name--` as appropriate:

    <dependency>
        <groupId>org.testcontainers</groupId>
        <artifactId>--artifact name--</artifactId>
        <version>0.9.8</version>
    </dependency>

> **Note**: Testcontainers uses the docker-java client library, which in turn depends on JAX-RS and various Jersey
libraries. If your project also uses these, you may need to set appropriate maven dependency exclusions or use
`dependencyManagement` to avoid conflicts, on a case-by-case basis.

## Logging

Testcontainers, and many of the libraries it uses, utilize slf4j for logging. In order to see logs from Testcontainers,
your project should include an SLF4J implementation (Logback is recommended). The following example `logback-test.xml`
should be included in your classpath to show a reasonable level of log output:

```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="info">
        <appender-ref ref="STDOUT"/>
    </root>

    <logger name="org.apache.http" level="WARN"/>
    <logger name="com.github.dockerjava" level="WARN"/>
    <logger name="org.zeroturnaround.exec" level="WARN"/>
</configuration>
```

## License

See [LICENSE](https://raw.githubusercontent.com/testcontainers/testcontainers-java/master/LICENSE).

## Attributions

This project includes a modified class (ScriptUtils) taken from the Spring JDBC project, adapted under the terms of the Apache license. Copyright for that class remains with the original authors.

This project was initially inspired by a [gist](https://gist.github.com/mosheeshel/c427b43c36b256731a0b) by Mosche Eschel.

## Contributing

* Star the project on [Github](https://github.com/testcontainers/testcontainers-java) and help spread the word :)
* See [ROADMAP](ROADMAP.md) to understand the approach behind the project and what may/may not be in store for the future.
* [Post an issue](https://github.com/testcontainers/testcontainers-java/issues) if you find any bugs
* Contribute improvements or fixes using a [Pull Request](https://github.com/testcontainers/testcontainers-java/pulls). If you're going to contribute, thank you! Please just be sure to:
	* discuss with the authors on an issue ticket prior to doing anything big
	* follow the style, naming and structure conventions of the rest of the project
	* make commits atomic and easy to merge
	* verify all tests are passing. Build the project with `mvn clean install -Pproprietary-deps` to do this.

## Copyright

Copyright (c) 2015 Richard North and other authors.

See [AUTHORS](https://raw.githubusercontent.com/testcontainers/testcontainers-java/master/AUTHORS) for contributors.
