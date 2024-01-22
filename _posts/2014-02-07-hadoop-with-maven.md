---
layout: post
title: "Hadoop with Maven"
---

The last couple of days, I have been playing with Hadoop. Because of that, I couldn't blog much often.

I wanted to automated packaging with Maven. Below gist shows a sample Maven pom.xml for Hadoop.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>groupId</groupId>
	<artifactId>artifactId</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>Name</name>
	<url>http://maven.apache.org</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-jar-plugin</artifactId>
				<configuration>
					<archive>
						<manifest>
							<addClasspath>true</addClasspath>
							<mainClass>package.MainClass</mainClass>
						</manifest>
					</archive>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
                                <configuration>
                                       <source>1.6</source>
                                       <target>1.6</target>
                                </configuration>
			</plugin>
		</plugins>
	</build>

	<dependencies>
		<dependency>
			<groupId>org.apache.hadoop</groupId>
			<artifactId>hadoop-core</artifactId>
			<version>1.2.1</version>
		</dependency>
	</dependencies>
</project>
```

This will resolve Hadoop dependency and package it as a jar file. Hope this will help you!

### Gists

- <https://gist.github.com/dedunumax/8416120>

### Tags

- hadoop
- maven