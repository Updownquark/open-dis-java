# Open DIS for Java

[![Build Status](https://travis-ci.org/open-dis/open-dis-java.svg?branch=master)](https://travis-ci.org/open-dis/open-dis-java)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/edu.nps.moves/open-dis/badge.svg)](https://maven-badges.herokuapp.com/maven-central/edu.nps.moves/open-dis)
[![Javadocs](http://www.javadoc.io/badge/edu.nps.moves/open-dis.svg)](http://www.javadoc.io/doc/edu.nps.moves/open-dis)

## Introduction

This repository contains a Java implementation of the Distributed Interactive Simulation (DIS) IEEE-1278 standard, which is often used in military simulations.

The library consists of classes that represent Protocol Data Units (PDUs).
These classes have fields, getters, and setters, and are able to marshal and unmarshal themselves to and from the DIS binary format.
Many of the classes were initially generated with [XMLPG](http://github.com/open-dis/xmlpg).

The library also provides supporting classes that read and write PDUs from the network, log PDUs to a file, and more.

## Documentation

Javadocs for the current and previous artifact versions can be found on [javadoc.io](https://www.javadoc.io/doc/edu.nps.moves/open-dis/).
Or to generate javadocs yourself run `mvn javadoc:javadoc`.

Example code can be found in the [repository](src/main/java/edu/nps/moves/examples/).

## Using the Java Library

### Maven

There are two repositories where Open DIS can be found; JitPack and Maven Central. Read below before making a choice.

#### JitPack

[JitPack](https://jitpack.io/) is a terrific service that enables you to include any development snapshot of the Open DIS java library as a Maven dependency in your project. A common use case is someone who wants to try the latest code because it contains a fix that was recently merged in. To use this service do the following: 

1. Add the jitpack repository to your project `pom.xml`.

```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://www.jitpack.io</url>
    </repository>
</repositories>
```

2. And this to your `<dependencies>` section, replacing the `<version>` value with any SHA1 from this library you wish.

```xml
<dependency>
    <groupId>com.github.open-dis</groupId>
    <artifactId>open-dis-java</artifactId>
    <version>d3c2b19aed8e80c5e7ef938dc0982f5ad0282ae6</version> <!-- replace with any git SHA1 -->
</dependency>
```

Note: When you use the JitPack service for the first time it is common your project build will time out and then fail. This is because your request likely has triggered a new build that no one else has and the JitPack servers are busy doing that for you. If this happens, retry you project build 5-10 minutes later and it should succeed this time. Future builds of your project will be much faster because the library artifact will have been cached on jitpack servers and be stored locally on your disk.

#### Maven Central

Official releases published by the Open DIS maintainers can be found on Maven Central. These are less frequent, but can be more stable because they are conciously released.

Add the following to your `pom.xml`.

```xml
<dependency>
    <groupId>edu.nps.moves</groupId>
    <artifactId>open-dis</artifactId>
    <version>4.08</version>
</dependency>
```

### Ant

Include the `open-dis-<version-number>.jar` file in your project, found on the [releases](https://github.com/open-dis/open-dis-java/releases) page of this GitHub project.

## Release Notes

### 5.0 release highlights (not yet released)

* Dropped Hibernate and JAXB support (i.e. the annotations were removed from PDU classes), consequently the `dismobile` and `dis7mobile` packages became redundant and  were removed.
* `PDUFactory` has gained support for more PDU's; `EventPDU`, `SignalPDU`, `TransmitterPDU` and `ReceiverPDU`.
* Added more JUnit tests.
* Migrated to GitHub and extracted Java library into own repository.

### 4.x release highlights

* SQL support.
* Modified & rationalized repository layout.
* Added mobile support in addition to desktop support.

### 3.x release highlights

* Robert Harder has reworked the Java marshal and unmarshal code to use much more memory efficient NIO classes, which dramatically reduce the amount of temporary object memory generated.

* Sheldon Snyder has contributed dead reckoning algorithms in Java, available in the `edu.nps.moves.deadreckoning` package.

* Enumerations. The SISO EBV XML document was used to generate Java enumeration classes. This can be extended as the EBV XML document is completed. The enumerations are used in several places in the open-dis code, notably the PduFactory.

* Unit tests. The Java code has added some JUnit 4.4 unit tests, primarily to test that post-processing source code patches have been applied correctly. These can be extended to provide more complete test coverage.

## License

All code is BSD license. See `LICENSE.md`.

## For Contributors

This section is useful for developers who may be contributing to the library.
This contains info about "how the hotdog is made".

### Software release process

Once enough changes have been made we cut a new release and deploy it to Maven Central.

In a nutshell the person performing the release will need:
 * A Sonatype JIRA account
 * Your JIRA credentials placed in your `~/.m2/settings.xml`
 * Your GPG key published

For more info view this [guide](https://docs.sonatype.org/display/Repository/Sonatype+OSS+Maven+Repository+Usage+Guide).

Once that's done, for each release do the following commands:

    $ mvn release:clean
    $ mvn release:prepare
    $ mvn release:perform
