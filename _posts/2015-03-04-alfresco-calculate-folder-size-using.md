---
layout: post
title: 'Alfresco: Calculate folder size using Java based WebScript'
---

I was assigned to a training task to write a web script for calculating the size of a folder or a file. But you need to go through all the nodes recursively. If you don't calculate it recursively in folders you won't get accurate folder size.  

Requirements:  

*   Java Development Kit 1.7 or later
*   Text Editor or IDE (Eclipse/Sublime Text/Atom)
*   Apache Maven 3 or later
*   Web Browser (Chrome/Firefox/Safari)
  
For this project, I generated the [Alfresco 5 All-in-One maven project](http://www.dedunu.info/2015/01/how-to-generate-alfresco-5-amp-project.html). You really don't want Alfresco  Share module in this project. But I included it because you may need to find a NodeRefId. It would be easier with Share.  The source [code of this project is available at GitHub](https://github.com/dedunumax/filesize-webscript).

size.get.html.ftl
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
    	<meta http-equiv="X-UA-Compatible" content="IE=edge">
    	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Check file size</title>
</head>
<body>
    	<div>
 		<h1>Check file size</h1>
  		<p>File Name : ${fileName}</p>
		<p>File Size : ${size}</p>
	</div>
</body>
</html>
```

size.get.desc.xml
```xml
<webscript>
   <shortname>File Size</shortname>
   <description>Returns the file size of the given nodeRef</description>
   <url>/size?nodeRef={RefForNode}</url>
   <authentication>user</authentication>
   <format default="html">extension</format>
   <family>File Size Utilities</family>
</webscript>
```

FileSizeWebScript.java
```java
package org.dedunu.alfresco;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.alfresco.model.ContentModel;
import org.alfresco.service.cmr.repository.ChildAssociationRef;
import org.alfresco.service.cmr.repository.ContentData;
import org.alfresco.service.cmr.repository.NodeRef;
import org.alfresco.service.cmr.repository.NodeService;
import org.springframework.extensions.webscripts.Cache;
import org.springframework.extensions.webscripts.DeclarativeWebScript;
import org.springframework.extensions.webscripts.Status;
import org.springframework.extensions.webscripts.WebScriptRequest;

public class FileSizeWebScript extends DeclarativeWebScript {

    /**
     * Defining node service.
     */
    private NodeService nodeService;

    /**
     * @param nodeService
     */
    public final void setNodeService(final NodeService nodeService) {
        this.nodeService = nodeService;
    }

    @Override
    protected Map<String, Object> executeImpl(WebScriptRequest req,
             Status status, Cache cache) {
        Map<String, Object> model = new HashMap<String, Object>();
        String nodeRefId = req.getParameter("nodeRef");
        NodeRef nodeRef = new NodeRef(nodeRefId);

        String fileName = (String) nodeService.getProperty(nodeRef,
                ContentModel.PROP_NAME);

        long size = getNodeSize(nodeRef);

        model.put("fileName", fileName);
        model.put("size", Long.toString(size));

        return model;
    }

    private long getNodeSize(NodeRef nodeRef) {
        long size = 0;

        // Collecting current node size
        ContentData contentData = (ContentData) nodeService.getProperty(
                nodeRef, ContentModel.PROP_CONTENT);
        try {
            size = contentData.getSize();
        } catch (Exception e) {
            size = 0;
        }

        // Collecting child nodes' sizes
        List<ChildAssociationRef> chilAssocsList = nodeService
                .getChildAssocs(nodeRef);

        for (ChildAssociationRef childAssociationRef : chilAssocsList) {
            NodeRef childNodeRef = childAssociationRef.getChildRef();
            size = size + getNodeSize(childNodeRef);
        }

        return size;
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
    
	<bean id="webscript.org.dedunu.alfresco.size.get" class="org.dedunu.alfresco.FileSizeWebScript" parent="webscript">
		<property name="nodeService">
			<ref bean="NodeService" />
		</property>
	</bean>
    
</beans>
```

Create above files in below locations of your maven project. 

*   size.get.desc.xml - `repo-amp/src/main/amp/config/alfresco/extension/templates/webscripts/org/dedunu/alfresco/size.get.desc.xml`
*   size.get.html.ftl - `repo-amp/src/main/amp/config/alfresco/extension/templates/webscripts/org/dedunu/alfresco/size.get.html.ftl`
*   FileSizeWebScript.java - `repo-amp/src/main/java/org/dedunu/alfresco/FileSizeWebScript.java`
*   service-context.xml - `repo-amp/src/main/amp/config/alfresco/module/repo-amp/context/service-context.xml`

**How to test the web script?**  

Take a terminal. Navigate to project folder. And type below command.

```console
$ mvn clean install -Prun -Dmaven.test.skip
```

It may take a while to start the Alfresco Repository and Share server. Wait till it finishes completely. 

Then open a web browser and go to [http://localhost:8080/share](http://localhost:8080/share). Then login. Go to Document library.

![](http://1.bp.blogspot.com/-3XALkt-WA60/VPdII_SUDjI/AAAAAAAABOM/UJjeLuRVu80/s1600/Screen%2BShot%2B2015-03-04%2Bat%2B11.25.58%2BPM.png)

Find a folder and click on "View Details". Then copy NodeRef from browser as shown below.

![](http://1.bp.blogspot.com/-VmlsYQdXa8E/VPdIaq0IucI/AAAAAAAABOU/4pukMQMRmE8/s1600/Screen%2BShot%2B2015-03-04%2Bat%2B11.26.05%2BPM.png)

Open a new tab and type below URL. (Replace <NodeRef> with the NodeRef you copied from Alfresco Share interface.)

[http://localhost:8080/alfresco/s/size?nodeRef=<NodeRef>](http://localhost:8080/alfresco/s/size?nodeRef=%3CNodeRef%3E)

If you have followed the instruction properly, you will get a page like below.

![](http://4.bp.blogspot.com/-09zxIR-N5dg/VPdJHJXr5pI/AAAAAAAABOc/EsSsf7swrLc/s1600/Screen%2BShot%2B2015-03-04%2Bat%2B11.25.34%2BPM.png)

If you have any questions regarding these examples, please comment!!! Enjoy Alfresco!

#### Gistss

- <https://gist.github.com/dedunumax/20a17d08c6efe1f2314f>
- <https://gist.github.com/dedunumax/e131cbf9aaef1ffc4e60>
- <https://gist.github.com/dedunumax/be88aaf300dac7a19ed9>
- <https://gist.github.com/dedunumax/3bb550ce1c3250613519>

### Tags

- webscript
- Java
- recursive
- folder
- alfresco