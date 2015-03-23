# Introduction #

dex2jar host a maven repository at cloudbees


# Details #

add dex2jar reop to your pom.xml (release builds)
```
<repositories>
    <repository>
        <id>Dex2jar Repo</id>
        <url>http://repository-dex2jar.forge.cloudbees.com/release/</url>
    </repository>
    ...
</repositories>
```

also Snapshot builds
```
<repositories>
    <repository>
        <id>Dex2jar Snapshot Repo</id>
        <url>http://repository-dex2jar.forge.cloudbees.com/snapshot/</url>
    </repository>
    ...
</repositories>
```

here is an example
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>a.b</groupId>
    <artifactId>asdf</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <dependencies>
        <dependency>
            <groupId>com.googlecode.dex2jar</groupId>
            <artifactId>dex-reader</artifactId>
            <version>1.4</version>
        </dependency>
    </dependencies>
    <repositories>
        <repository>
            <id>Dex2jar Repo</id>
            <url>http://repository-dex2jar.forge.cloudbees.com/release/</url>
        </repository>
    </repositories>
</project>
```