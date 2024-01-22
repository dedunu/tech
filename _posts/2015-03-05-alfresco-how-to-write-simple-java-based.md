---
layout: post
title: 'Alfresco: How to write a simple Java based Alfresco web script?'
---

If you want to develop a new feature for Alfresco best way is WebScript! Let's start with a simple Alfresco web script. First, you need to create an Alfresco AMP maven project using archetype. In this example, I'll use the latest alfresco version 5.0.

First I generated Alfresco All-in-One AMP. ([Please refer my blog post on generating AMP projects](http://www.dedunu.info/2015/01/how-to-generate-alfresco-5-amp-project.html).)

If you go through the files structure which is generated, you will find out a sample web script. It is a JavaScript-based WebScript. By this example, I'm going to explain how to write a simple Java-based Hello World web script.  

HelloWorldWebScript.java
```java
package org.dedunu.alfresco;

import java.util.HashMap;
import java.util.Map;

import org.springframework.extensions.webscripts.Cache;
import org.springframework.extensions.webscripts.DeclarativeWebScript;
import org.springframework.extensions.webscripts.Status;
import org.springframework.extensions.webscripts.WebScriptRequest;

public class HelloWorldWebScript extends DeclarativeWebScript {

    @Override
    protected Map<String, Object> executeImpl(WebScriptRequest req,
             Status status, Cache cache) {
        Map<String, Object> model = new HashMap<String, Object>();

        model.put("helloMessage", "Hello World! - Welcome to Alfresco Development!");

        return model;
    }
}
```

service-context.xml
```xml
<?xml version='1.0' encoding='UTF-8'?>
<!DOCTYPE beans PUBLIC '-//SPRING//DTD BEAN//EN' 'http://www.springframework.org/dtd/spring-beans.dtd'>
<!--
	Licensed to the Apache Software Foundation (ASF) under one or more
	contributor license agreements.  See the NOTICE file distributed with
	this work for additional information regarding copyright ownership.
	The ASF licenses this file to You under the Apache License, Version 2.0
	(the "License"); you may not use this file except in compliance with
	the License.  You may obtain a copy of the License at
	http://www.apache.org/licenses/LICENSE-2.0
	Unless required by applicable law or agreed to in writing, software
	distributed under the License is distributed on an "AS IS" BASIS,
	WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	See the License for the specific language governing permissions and
	limitations under the License.
-->
<beans>

	<bean id="webscript.org.dedunu.alfresco.helloworld.get" class="org.dedunu.alfresco.HelloWorldWebScript" parent="webscript">
	</bean>

</beans>
```

helloworld.get.desc.xml
```xml
<webscript>
    <shortname>Java based Sample Webscript</shortname>
    <description>This simple WebScript prints Hello World</description>
    <url>/dedunu/helloworld</url>
    <authentication>user</authentication>
    <format default="html"></format>
</webscript>
```

helloworld.get.html.ftl  
```console
${helloMessage}
```

Create the above files in below locations of your maven project.

*   HelloWorldWebScript.java - `repo-amp/src/main/java/org/dedunu/alfresco/HelloWorldWebScript.java`
*   helloworld.get.desc.xml - `repo-amp/src/main/amp/config/alfresco/extension/templates/webscripts/org/dedunu/alfresco/helloworld.get.desc.xml`
*   helloworld.get.html.ftl - `repo-amp/src/main/amp/config/alfresco/extension/templates/webscripts/org/dedunu/alfresco/helloworld.get.html.ftl`
*   service-context.xml - `repo-amp/src/main/amp/config/alfresco/module/repo-amp/context/service-context.xml`

Use below command to run the maven project.

```console
$ mvn clean install -Prun 
```

It may take a while to run the project after that open a browser window. Then visit below URL  

[http://localhost:8080/alfresco/service/dedunu/helloworld](http://localhost:8080/alfresco/service/dedunu/helloworld).

![](http://3.bp.blogspot.com/-tQToG3yhLVI/VPilF8wi8bI/AAAAAAAABOw/ERDwjCoD36c/s1600/Screen%2BShot%2B2015-03-05%2Bat%2B11.32.32%2BPM.png)

The source [code of this project is available on GitHub](https://github.com/dedunumax/hello-webscript).

#### Gistss

- <https://gist.github.com/dedunumax/411620c73e80e81755d0>
- <https://gist.github.com/dedunumax/ef370e4d00cfd4d6b05f>
- <https://gist.github.com/dedunumax/534139d220554e6a3e0f>
- <https://gist.github.com/dedunumax/480335164d5aa5f698fd>

### Tags

- webscript
- Java
- alfresco