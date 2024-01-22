---
layout: post
title: How to generate Alfresco 5 AMP project
---

Recently I have been working as an Alfresco Developer. When you are developing Alfresco Modules, you need to have a proper project with the correct directory structure. Since Alfresco use Maven, you can generate an Alfresco 5 AMP project using archetype.

First, you need Java and Maven installed on your Linux/Mac/Windows computer. Then run below command to start the project.

```console
$ mvn archetype:generate -DarchetypeCatalog=http://repo1.maven.org/maven2/archetype-catalog.xml -Dfilter=org.alfresco:
```

Then you will get below text.

```console
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] >>> maven-archetype-plugin:2.2:generate (default-cli) > generate-sources @ standalone-pom >>>
[INFO] 
[INFO] <<< maven-archetype-plugin:2.2:generate (default-cli) < generate-sources @ standalone-pom <<<
[INFO] 
[INFO] --- maven-archetype-plugin:2.2:generate (default-cli) @ standalone-pom ---
[INFO] Generating project in Interactive mode
[INFO] No archetype defined. Using maven-archetype-quickstart (org.apache.maven.archetypes:maven-archetype-quickstart:1.0)
Choose archetype:
1: http://repo1.maven.org/maven2/archetype-catalog.xml -> org.alfresco.maven.archetype:alfresco-allinone-archetype (Sample multi-module project for All-in-One development on the Alfresco plaftorm. Includes modules for: Repository WAR overlay, Repository AMP, Share WAR overlay, Solr configuration, and embedded Tomcat runner)
2: http://repo1.maven.org/maven2/archetype-catalog.xml -> org.alfresco.maven.archetype:alfresco-amp-archetype (Sample project with full support for lifecycle and rapid development of Repository AMPs (Alfresco Module Packages))
3: http://repo1.maven.org/maven2/archetype-catalog.xml -> org.alfresco.maven.archetype:share-amp-archetype (Share project with full support for lifecycle and rapid development of AMPs (Alfresco Module Packages))

Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): :
```

Now you have 3 options to select.

1.  All-in-One (This includes Repository Module, Share Module, Solar configuration and Tomcat runner. One-stop solution for Alfresco development. I don't recommend it to beginners to start with. )
2.  Alfresco Repository Module (This will generate AMP for Alfresco Repository.)
3.  Alfresco Share Module (This will generate AMP for Alfresco Share.)

```console
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): : 2
Choose org.alfresco.maven.archetype:alfresco-amp-archetype version: 
1: 2.0.0-beta-1
2: 2.0.0-beta-2
3: 2.0.0-beta-3
4: 2.0.0-beta-4
5: 2.0.0
Choose a number: 5: Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): : 2
Choose org.alfresco.maven.archetype:alfresco-amp-archetype version: 
1: 2.0.0-beta-1
2: 2.0.0-beta-2
3: 2.0.0-beta-3
4: 2.0.0-beta-4
5: 2.0.0
Choose a number: 5: 
```

In this example, I used the Alfresco Repository Module. Then it prompts for SDK version. By pressing enter you can get the latest(default) SDK version. Then Maven prompts for groupId and artifactId. Please provide suitable Ids for them.

```console
Define value for property 'groupId': : org.dedunu
Define value for property 'artifactId': : training
[INFO] Using property: version = 1.0-SNAPSHOT
[INFO] Using property: package = (not used)
[INFO] Using property: alfresco_target_groupId = org.alfresco
[INFO] Using property: alfresco_target_version = 5.0.c
Confirm properties configuration:
groupId: org.dedunu
artifactId: training
version: 1.0-SNAPSHOT
package: (not used)
alfresco_target_groupId: org.alfresco

alfresco_target_version: 5.0.c
 Y: : 
```

Then again Maven prompts for your target Alfresco version. At the moment the latest Alfresco version is 5.0.c. If you hit enter it will continue with the latest version. Otherwise, you can customize the target Alfresco version. Then it will generate a Maven project for Alfresco.

```console
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Archetype: alfresco-amp-archetype:2.0.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: groupId, Value: org.dedunu
[INFO] Parameter: artifactId, Value: training
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: (not used)
[INFO] Parameter: packageInPathFormat, Value: (not used)
[INFO] Parameter: package, Value: (not used)
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: groupId, Value: org.dedunu
[INFO] Parameter: alfresco_target_version, Value: 5.0.c
[INFO] Parameter: artifactId, Value: training
[INFO] Parameter: alfresco_target_groupId, Value: org.alfresco
[INFO] project created from Archetype in dir: /Users/dedunu/Documents/workspace/training
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 08:33 min
[INFO] Finished at: 2015-01-19T23:58:38+05:30
[INFO] Final Memory: 14M/155M

[INFO] ------------------------------------------------------------------------
```

### Tags

- Java
- archetype
- maven
- alfresco
