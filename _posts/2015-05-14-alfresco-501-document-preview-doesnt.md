---
layout: post
title: "Alfresco 5.0.1 Document Preview doesn't work on Ubuntu?"
---

I recently installed Alfresco for testing in the vagrant instance. I used the Ubuntu image for the vagrant instance. But I forgot to install all the libraries which are necessary to be installed on Ubuntu before you install alfresco. But fortunately alfresco worked without those dependencies.

[http://docs.alfresco.com/5.0/concepts/install-lolibfiles.html](http://docs.alfresco.com/5.0/concepts/install-lolibfiles.html)

Above link gives you what are the libraries you should install before you install Alfresco. You should run below command to install libraries.

```console
$ sudo apt-get install libice6 libsm6 libxt6 libxrender1 libfontconfig1 libcups2
```
But still, office document previews didn't work properly. Some documents worked properly but some of them didn't. Then I tried to debug it with one of my colleagues. We found below text in our logs.

```console
2015-05-14 10:04:16,607  ERROR [repo.content.JodConverterSharedInstance] [localhost-startStop-1] Unable to start JodConverter library. The following error is shown for informational purposes only.
 org.artofsolving.jodconverter.office.OfficeException: failed to start and connect
	at org.artofsolving.jodconverter.office.ManagedOfficeProcess.startAndWait(ManagedOfficeProcess.java:68)
	at org.artofsolving.jodconverter.office.PooledOfficeManager.start(PooledOfficeManager.java:101)
	at org.artofsolving.jodconverter.office.ProcessPoolOfficeManager.start(ProcessPoolOfficeManager.java:66)
	at org.alfresco.enterprise.repo.content.JodConverterSharedInstance.afterPropertiesSet(JodConverterSharedInstance.java:239)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1572)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1510)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:521)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:458)
	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:293)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:223)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:290)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:191)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:633)
	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:932)
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:479)
	at org.alfresco.repo.management.subsystems.ChildApplicationContextFactory$ApplicationContextState.start(ChildApplicationContextFactory.java:809)
	at org.alfresco.repo.management.subsystems.AbstractPropertyBackedBean.start(AbstractPropertyBackedBean.java:1018)
	at org.alfresco.repo.management.subsystems.AbstractPropertyBackedBean.onApplicationEvent(AbstractPropertyBackedBean.java:557)
	at org.alfresco.repo.management.SafeApplicationEventMulticaster.multicastEventInternal(SafeApplicationEventMulticaster.java:209)
	at org.alfresco.repo.management.SafeApplicationEventMulticaster.multicastEvent(SafeApplicationEventMulticaster.java:180)
	at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:334)
	at org.springframework.context.support.AbstractApplicationContext.finishRefresh(AbstractApplicationContext.java:948)
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:482)
	at org.springframework.web.context.ContextLoader.configureAndRefreshWebApplicationContext(ContextLoader.java:410)
	at org.springframework.web.context.ContextLoader.initWebApplicationContext(ContextLoader.java:306)
	at org.springframework.web.context.ContextLoaderListener.contextInitialized(ContextLoaderListener.java:112)
	at org.alfresco.web.app.ContextLoaderListener.contextInitialized(ContextLoaderListener.java:63)
	at org.apache.catalina.core.StandardContext.listenerStart(StandardContext.java:5016)
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5524)
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:150)
	at org.apache.catalina.core.ContainerBase.addChildInternal(ContainerBase.java:901)
	at org.apache.catalina.core.ContainerBase.addChild(ContainerBase.java:877)
	at org.apache.catalina.core.StandardHost.addChild(StandardHost.java:649)
	at org.apache.catalina.startup.HostConfig.deployWAR(HostConfig.java:1081)
	at org.apache.catalina.startup.HostConfig$DeployWar.run(HostConfig.java:1877)
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:745)
Caused by: java.util.concurrent.ExecutionException: org.artofsolving.jodconverter.office.OfficeException: could not establish connection
	at java.util.concurrent.FutureTask.report(FutureTask.java:122)
	at java.util.concurrent.FutureTask.get(FutureTask.java:206)
	at org.artofsolving.jodconverter.office.ManagedOfficeProcess.startAndWait(ManagedOfficeProcess.java:66)
	... 39 more
Caused by: org.artofsolving.jodconverter.office.OfficeException: could not establish connection
	at org.artofsolving.jodconverter.office.ManagedOfficeProcess.doStartProcessAndConnect(ManagedOfficeProcess.java:147)
	at org.artofsolving.jodconverter.office.ManagedOfficeProcess.access$0(ManagedOfficeProcess.java:122)
	at org.artofsolving.jodconverter.office.ManagedOfficeProcess$1.run(ManagedOfficeProcess.java:62)
	... 5 more
Caused by: java.lang.IllegalStateException: process with acceptString 'socket,host=127.0.0.1,port=8100' started but its pid could not be found
	at org.artofsolving.jodconverter.office.OfficeProcess.start(OfficeProcess.java:137)
	at org.artofsolving.jodconverter.office.OfficeProcess.start(OfficeProcess.java:67)
	at org.artofsolving.jodconverter.office.ManagedOfficeProcess.doStartProcessAndConnect(ManagedOfficeProcess.java:124)
	... 7 more
```

Then we tried to run the soffice application from the terminal. Look what we got!

```
/home/vagrant/alfresco-5.0.1/libreoffice/program/oosplash: error while loading shared libraries: libXinerama.so.1: cannot open shared object file: No such file or directory
```

Then we realised that we should install that library on Ubuntu. Run below command on the Ubuntu server to install the missing library.

```console
$ sudo apt-get install libxinerama1
```

Make sure you run both commands above!

## Gist

- <https://gist.github.com/dedunumax/3d748846bc7f6fc6b87e>

### Tags

- libreoffice
- openoffice
- Ubuntu
- alfresco