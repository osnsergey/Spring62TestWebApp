# Issue description
Spring Component Scan doesn't work in the Web application after the migration from Spring 6.1 to Spring 6.2.

The exception during startup:
```
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'beanFromXML' defined in ServletContext resource [/WEB-INF/applicationContext.xml]: Cannot resolve reference to bean 'beanFromScan' while setting bean property 'beanFromScan'
        at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:377)
        at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveValueIfNecessary(BeanDefinitionValueResolver.java:135)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyPropertyValues(AbstractAutowireCapableBeanFactory.java:1711)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1460)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:600)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:523)
        at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:336)
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:307)
        at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:334)

        at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:199)
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.instantiateSingleton(DefaultListableBeanFactory.java:1122)
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingleton(DefaultListableBeanFactory.java:1093)
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:1030)
        at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:987)
        at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:627)
        at org.springframework.web.context.ContextLoader.configureAndRefreshWebApplicationContext(ContextLoader.java:394)
        at org.springframework.web.context.ContextLoader.initWebApplicationContext(ContextLoader.java:274)
        at org.springframework.web.context.ContextLoaderListener.contextInitialized(ContextLoaderListener.java:126)
        at org.apache.catalina.core.StandardContext.listenerStart(StandardContext.java:4008)
        at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:4436)
        at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:164)
        at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1203)
        at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1193)
        at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
        at org.apache.tomcat.util.threads.InlineExecutorService.execute(InlineExecutorService.java:75)
        at java.base/java.util.concurrent.AbstractExecutorService.submit(AbstractExecutorService.java:145)
        at org.apache.catalina.core.ContainerBase.startInternal(ContainerBase.java:749)
        at org.apache.catalina.core.StandardHost.startInternal(StandardHost.java:772)
        at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:164)
        at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1203)
        at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1193)
        at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
        at org.apache.tomcat.util.threads.InlineExecutorService.execute(InlineExecutorService.java:75)
        at java.base/java.util.concurrent.AbstractExecutorService.submit(AbstractExecutorService.java:145)
        at org.apache.catalina.core.ContainerBase.startInternal(ContainerBase.java:749)
        at org.apache.catalina.core.StandardEngine.startInternal(StandardEngine.java:203)
        at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:164)
        at org.apache.catalina.core.StandardService.startInternal(StandardService.java:415)
        at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:164)
        at org.apache.catalina.core.StandardServer.startInternal(StandardServer.java:870)
        at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:164)
        at org.apache.catalina.startup.Tomcat.start(Tomcat.java:437)
        at com.test.app.runner.AppRunner.run(AppRunner.java:42)
        at com.test.app.runner.AppRunner.main(AppRunner.java:131)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:568)
        at org.springframework.boot.loader.MainMethodRunner.run(MainMethodRunner.java:49)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:95)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:58)
        at com.test.app.runner.JarLauncher.main(JarLauncher.java:38)
Caused by: org.springframework.beans.factory.NoSuchBeanDefinitionException: No bean named 'beanFromScan' available
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.getBeanDefinition(DefaultListableBeanFactory.java:925)
        at org.springframework.beans.factory.support.AbstractBeanFactory.getMergedLocalBeanDefinition(AbstractBeanFactory.java:1361)
        at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:299)

        at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:199)
        at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:365)
        ... 51 common frames omitted
```

**beanFromScan** can't be found by the Component Scan.

# Build sample application
Use JDK 17.
```
./gradlew spring62webapp:release
```
# Run sample application
Enter the release directory:
```
cd ./spring62webapp/result/release 
```
Run the jar:
```
java -jar spring62webapp.jar
```
