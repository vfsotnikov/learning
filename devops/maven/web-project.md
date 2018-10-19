# Руководство по Maven. Веб-проект с использованием Maven.

В этой статье мы рассмотрим процесс создания веб-приложения с использованием Maven. После чего мы выполним сборку, деплой и запуск нашего проекта.

## Создание проекта

Для того, чтобы созать простой веб-проект мы будем использовать плагин **maven-archetype-webapp**.

Перейдём в нужную нам директорию и выполним в терминале следующиую команду:

```sh
mvn archetype:generate 
-DgroupId=net.proselyte.tutorial 
-DartifactId=maven 
-DarchetypeArtifactId=maven-archetype-webapp 
-DinteractiveMode=false
```

В итоге мы получим следующий результат:

```log
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] >>> maven-archetype-plugin:2.4:generate (default-cli) @ standalone-pom >>>
[INFO] 
[INFO] <<< maven-archetype-plugin:2.4:generate (default-cli) @ standalone-pom <<<
[INFO] 
[INFO] --- maven-archetype-plugin:2.4:generate (default-cli) @ standalone-pom ---
[INFO] Generating project in Batch mode
[WARNING] Error reading archetype catalog http://repo.maven.apache.org/maven2
org.apache.maven.wagon.TransferFailedException: repo.maven.apache.org
	at org.apache.maven.wagon.providers.http.AbstractHttpClientWagon.fillInputData(AbstractHttpClientWagon.java:892)
	at org.apache.maven.wagon.StreamWagon.getInputStream(StreamWagon.java:116)
	at org.apache.maven.wagon.StreamWagon.getIfNewer(StreamWagon.java:88)
	at org.apache.maven.wagon.StreamWagon.get(StreamWagon.java:61)
	at org.apache.maven.archetype.source.RemoteCatalogArchetypeDataSource.downloadCatalog(RemoteCatalogArchetypeDataSource.java:119)
	at org.apache.maven.archetype.source.RemoteCatalogArchetypeDataSource.getArchetypeCatalog(RemoteCatalogArchetypeDataSource.java:87)
	at org.apache.maven.archetype.DefaultArchetypeManager.getRemoteCatalog(DefaultArchetypeManager.java:216)
	at org.apache.maven.archetype.DefaultArchetypeManager.getRemoteCatalog(DefaultArchetypeManager.java:205)
	at org.apache.maven.archetype.ui.generation.DefaultArchetypeSelector.getArchetypesByCatalog(DefaultArchetypeSelector.java:200)
	at org.apache.maven.archetype.ui.generation.DefaultArchetypeSelector.selectArchetype(DefaultArchetypeSelector.java:71)
	at org.apache.maven.archetype.mojos.CreateProjectFromArchetypeMojo.execute(CreateProjectFromArchetypeMojo.java:181)
	at org.apache.maven.plugin.DefaultBuildPluginManager.executeMojo(DefaultBuildPluginManager.java:101)
	at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:209)
	at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:153)
	at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:145)
	at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject(LifecycleModuleBuilder.java:84)
	at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject(LifecycleModuleBuilder.java:59)
	at org.apache.maven.lifecycle.internal.LifecycleStarter.singleThreadedBuild(LifecycleStarter.java:183)
	at org.apache.maven.lifecycle.internal.LifecycleStarter.execute(LifecycleStarter.java:161)
	at org.apache.maven.DefaultMaven.doExecute(DefaultMaven.java:320)
	at org.apache.maven.DefaultMaven.execute(DefaultMaven.java:156)
	at org.apache.maven.cli.MavenCli.execute(MavenCli.java:537)
	at org.apache.maven.cli.MavenCli.doMain(MavenCli.java:196)
	at org.apache.maven.cli.MavenCli.main(MavenCli.java:141)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.codehaus.plexus.classworlds.launcher.Launcher.launchEnhanced(Launcher.java:289)
	at org.codehaus.plexus.classworlds.launcher.Launcher.launch(Launcher.java:229)
	at org.codehaus.plexus.classworlds.launcher.Launcher.mainWithExitCode(Launcher.java:415)
	at org.codehaus.plexus.classworlds.launcher.Launcher.main(Launcher.java:356)
Caused by: java.net.UnknownHostException: repo.maven.apache.org
	at java.net.InetAddress.getAllByName0(InetAddress.java:1280)
	at java.net.InetAddress.getAllByName(InetAddress.java:1192)
	at java.net.InetAddress.getAllByName(InetAddress.java:1126)
	at org.apache.maven.wagon.providers.http.httpclient.impl.conn.SystemDefaultDnsResolver.resolve(SystemDefaultDnsResolver.java:45)
	at org.apache.maven.wagon.providers.http.httpclient.impl.conn.DefaultClientConnectionOperator.resolveHostname(DefaultClientConnectionOperator.java:278)
	at org.apache.maven.wagon.providers.http.httpclient.impl.conn.DefaultClientConnectionOperator.openConnection(DefaultClientConnectionOperator.java:162)
	at org.apache.maven.wagon.providers.http.httpclient.impl.conn.ManagedClientConnectionImpl.open(ManagedClientConnectionImpl.java:294)
	at org.apache.maven.wagon.providers.http.httpclient.impl.client.DefaultRequestDirector.tryConnect(DefaultRequestDirector.java:643)
	at org.apache.maven.wagon.providers.http.httpclient.impl.client.DefaultRequestDirector.execute(DefaultRequestDirector.java:479)
	at org.apache.maven.wagon.providers.http.httpclient.impl.client.AbstractHttpClient.execute(AbstractHttpClient.java:906)
	at org.apache.maven.wagon.providers.http.httpclient.impl.client.AbstractHttpClient.execute(AbstractHttpClient.java:805)
	at org.apache.maven.wagon.providers.http.AbstractHttpClientWagon.execute(AbstractHttpClientWagon.java:746)
	at org.apache.maven.wagon.providers.http.AbstractHttpClientWagon.fillInputData(AbstractHttpClientWagon.java:886)
	... 31 more
[WARNING] No archetype found in remote catalog. Defaulting to internal catalog
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Old (1.x) Archetype: maven-archetype-webapp:1.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: basedir, Value: /home/proselyte/Programming/Projects/Proselyte/MavenWebProject
[INFO] Parameter: package, Value: net.proselyte.tutorial
[INFO] Parameter: groupId, Value: net.proselyte.tutorial
[INFO] Parameter: artifactId, Value: maven
[INFO] Parameter: packageName, Value: net.proselyte.tutorial
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] project created from Old (1.x) Archetype in dir: /home/proselyte/Programming/Projects/Proselyte/MavenWebProject/maven
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.494s
[INFO] Finished at: Fri Apr 29 12:41:33 EEST 2016
[INFO] Final Memory: 17M/212M
[INFO] ------------------------------------------------------------------------
```

Перейдём в директорию, в папку Maven

![MavenWebProject](https://i2.wp.com/proselyte.net/wp-content/uploads/2016/04/MavenWebProject.png)

Рассмотрим файл **pom.xml**

```xml 
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>net.proselyte.tutorial</groupId>
  <artifactId>maven</artifactId>
  <packaging>war</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>maven Maven Webapp</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  <build>
    <finalName>maven</finalName>
  </build>
</project>
```

В папке **webapp** есть файл **index.jsp**

```log
Hello World!
```

Выполним команду:

```sh
mvn clean package
```

В итоге получим следующий результат:

```log
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building maven Maven Webapp 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ maven ---
[INFO] Deleting /home/proselyte/Programming/Projects/Proselyte/MavenWebProject/maven/target
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ maven ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 0 resource
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ maven ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ maven ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenWebProject/maven/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:testCompile (default-testCompile) @ maven ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ maven ---
[INFO] No tests to run.
[INFO] Surefire report directory: /home/proselyte/Programming/Projects/Proselyte/MavenWebProject/maven/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------

Results :

Tests run: 0, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-war-plugin:2.1.1:war (default-war) @ maven ---
[INFO] Packaging webapp
[INFO] Assembling webapp [maven] in [/home/proselyte/Programming/Projects/Proselyte/MavenWebProject/maven/target/maven]
[INFO] Processing war project
[INFO] Copying webapp resources [/home/proselyte/Programming/Projects/Proselyte/MavenWebProject/maven/src/main/webapp]
[INFO] Webapp assembled in [25 msecs]
[INFO] Building war: /home/proselyte/Programming/Projects/Proselyte/MavenWebProject/maven/target/maven.war
[INFO] WEB-INF/web.xml already added, skipping
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.464s
[INFO] Finished at: Fri Apr 29 12:48:48 EEST 2016
[INFO] Final Memory: 9M/150M
[INFO] ------------------------------------------------------------------------
```

Запустим наше приложение с помощью локального сервера (в примере – tomcat) и получим следующий результат:

![HelloWorldMaven](https://i0.wp.com/proselyte.net/wp-content/uploads/2016/04/HelloWorldMaven.png)

На этом мы заканчиваем этот урок.
На этом мы заканчиваем изучение фреймворка Maven.

[Назад на страницу о maven](index.md)

[README.md](../../README.md)