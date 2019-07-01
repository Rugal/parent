# parent

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/ga.rugal/parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/ga.rugal/parent)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FRugal%2Fparent.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FRugal%2Fparent?ref=badge_shield)


## release instruction

```bash
mvn -P sonatype release:prepare release:perform
```

## release version

To include in your `pom.xml`
```xml
<parent>
  <groupId>ga.rugal</groupId>
  <artifactId>parent</artifactId>
  <version>VERSION</version>
</parent>
```


## snapshot version
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


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FRugal%2Fparent.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FRugal%2Fparent?ref=badge_large)