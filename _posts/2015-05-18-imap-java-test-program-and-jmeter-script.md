---
layout: post
title: IMAP Java Test program and JMeter Script
---

One of my colleagues wanted to write a JMeter script to test IMAP. But that code failed. So I also got involved in that. JMeter BeanShell uses Java in the backend. First I tried with a Maven project. Finally, I could write code to list the IMAP folders. Java implementation is shown below.

```java
package org.dedunu.imap;

import java.util.Properties;
import javax.mail.Folder;
import javax.mail.Session;
import javax.mail.Store;

public class IMAPTest {
    public static void main(String []args) {
        Properties props = System.getProperties();
        props.setProperty("mail.store.protocol","imap");
        Session session = Session.getDefaultInstance(props, null);

        try {
          
            /*
            	Hostname : imap.example.com
            	Port : 143
            	Username : john.doe@example.com
            	Password : Pa$$w0rd
            */
	          
            Store store = session.getStore("imap");
            store.connect("imap.example.com",143,"john.doe@example.com","Pa$$w0rd");
            Folder rootFolder = store.getDefaultFolder();
            Folder[] imapFolders = rootFolder.list("*");
            
            System.out.println(imapFolders.length);

            for (Folder folder : imapFolders) {
                System.out.println(folder.getFullName());
            }
            
            store.close();
            
        } catch (Exception ex) {
            System.out.println(ex.getMessage());
        }
    }
}
```

Then we wrote a code to print IMAP folder count for JMeter BeanShell. Code is shown below.

```java
import java.util.*;
import javax.mail.Folder;
import javax.mail.Session;
import javax.mail.Store;

Properties props = System.getProperties();
props.setProperty("mail.store.protocol","imap");
Session session = Session.getDefaultInstance(props, null);

try {

	Store store = session.getStore("imap");
	store.connect("localhost",143,"john.doe@example.com","Pa$$w0rd");
	Folder rootFolder = store.getDefaultFolder();
	Folder[] imapFolders = rootFolder.list("*");
	log.info("Folders found: " + imapFolders.length);
	store.close();

} catch (Exception ex) {

	log.error("IMAP operation failed", ex);

}
```

Complete Maven project is available on GitHub - [https://github.com/dedunu/imapTest](https://github.com/dedunu/imapTest)

#### Gistss

- <https://gist.github.com/dedunumax/a5c5498bfefe64b0bbe4>
- <https://gist.github.com/dedunumax/13cbacfbdf60c7692b64>

### Tags

- IMAP
- Java
- JMeter
