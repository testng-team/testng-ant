# TestNG Ant Integration

This repository houses the code related to TestNG Ant integration so as to help run TestNG tests via an Ant build file.

## Pre-requisites

* JDK11 (or) Higher
* TestNG `v.7.10.2` or higher on the CLASSPATH.

## Jar location

The TestNG Ant jar can be downloaded from [here](https://repo1.maven.org/maven2/org/testng/testng-ant/1.0.0/)

This jar contains ONLY the TestNG Ant integration code alone. It is NOT a fat/uber jar that includes TestNG within it.
TestNG jar needs to be explicitly provided in the CLASSPATH for the integration to work fine.