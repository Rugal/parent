# parent

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/ga.rugal/parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/ga.rugal/parent)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FRugal%2Fparent.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FRugal%2Fparent?ref=badge_shield)
[![Known Vulnerabilities](https://snyk.io/test/github/Rugal/parent/badge.svg?targetFile=pom.xml)](https://snyk.io/test/github/Rugal/parent?targetFile=pom.xml)  

## download

### release version

To include in your `pom.xml`
```xml
<parent>
  <groupId>ga.rugal</groupId>
  <artifactId>parent</artifactId>
  <version>VERSION</version>
</parent>
```

### snapshot version

for snapshot version, please add sonatype:
```xml
<repositories>
  <repository>
    <id>ossrh</id>
    <name>Sonatype snapshot repository</name>
    <url>https://oss.sonatype.org/content/repositories/snapshots</url>
    <layout>default</layout>
    <releases>
      <enabled>false</enabled>
      <updatePolicy>always</updatePolicy>
      <checksumPolicy>warn</checksumPolicy>
    </releases>
    <snapshots>
      <enabled>true</enabled>
      <updatePolicy>never</updatePolicy>
      <checksumPolicy>fail</checksumPolicy>
    </snapshots>
  </repository>
</repositories>
```

## Configurable Property

name | default | note
---|---|---
java.version | 11 | Java Development Kit version
skip.surefire.tests | true | Skip unit test & coverage report
skip.failsafe.tests | true | Skip integration test & coverage report
branch.threshold | 0.9 | Minimum branch coverage threshold
line.threshold | 0.9 | Minimum line coverage threshold
jacoco.skip.coverage.check | true | Skip test coverage check, this will fail build if threshold not reached
openapi.codegen.package.root | ${project.groupId}.${project.artifactId}.openapi |
openapi.codegen.skipIfSpecIsUnchanged | true | Skip codegen if no change in `contract.yml`
checkstyle.exclusion|target/**/*,**/dto/**/*, **/ExceptionController.java|
flyway.schema | test | the target database schema for flyway
azure.function.name | ${project.artifactId} | name of function app in Azure
azure.resourceGroup | eastus2-206136 | resource group name
azure.servicePlanName | ASP-eastus2206136-837f |  service plan name
azure.region | eastus2 | function app region
azure.stagingDirectory | ${project.build.directory}/azure-functions/${azure.function.name} | staging directory
azure.runtime.os | linux | operating system function app
graphql.package.name | ${project.groupId}.${project.artifactId}.graphql | package for graphql codegen
graphql.schema.path|src/main/resources/graphql|the schema file of graphql for codegen

## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FRugal%2Fparent.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FRugal%2Fparent?ref=badge_large)  

# development instruction

## release command

```bash
mvn -P sonatype release:prepare release:perform
```
