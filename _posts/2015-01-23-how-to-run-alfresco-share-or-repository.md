---
layout: post
title: How to run Alfresco Share or Repository AMP projects
---

From [the previous post, I explained how to generate an Alfresco AMP project using Maven](http://www.dedunu.info/2015/01/how-to-generate-alfresco-5-amp-project.html). When you have an AMP project you can run it by deploying it to an existing Alfresco Repository or Share. But if you are a developer you will not find it as an effective way to run Alfresco modules. The other way is that you can run the AMP project using Maven plug-in. 

In this post, I'm not going to talk about the first method. As I said earlier we can run an Alfresco instance using Maven. To do that from your terminal move to Alfresco AMP project folder and run below command.

```console
$ mvn clean package -Pamp-to-war
```

Perhaps it may take a while. If you are running this command for the first time it will download Alfresco binary for local Maven repository. If you are running an instance again, your changes would be still available on that Alfresco instance. 

If you want to discard all the previous data, use below command.

```console
$ mvn clean package -Ppurge -Pamp-to-war
```

Above command will discard all the changes and data. It will start a fresh instance.

Enjoy Alfresco Development!!!

### Tags

- maven
- alfresco
