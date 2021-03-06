# Руководство по Maven. POM

POM (Project Object Model) является базовым модулем Maven. Это специальный XML-файл, который всегда хранится в базовой директории проекта и называется **pom.xml**.

Файл POM содержит информацию о проекте и различных деталях конфигурации, которые используются Maven для создания проекта.

Этот файл также содержит задачи и плагины. Во время выполнения задач, Maven ищет файл pom.xml в базовой директории проекта. Он читает его и получает необходимую информацию, после чего выполняет задачи.

Среди конфигураций Maven мы можем выделить следующие:
- зависимости проекта
- плагины
- задачи
- профиль создания
- версия проекта
- разработчики
- список рассылки

Перед тем, как создавать **pom.xml**  нам необходимо прежде всего определить группу проекта (groupId), его имя (artifactId) и его версию. Все это поможет нам унифицировать проект для простой его идентификации в репозитории.

Рассмотрим простейший пример **pom.xml** файла:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
   http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>

   <groupId>com.companyname.project-group</groupId>
   <artifactId>project</artifactId>
   <version>1.0</version>
 
</project>
```
Каждый проект должен иметь свой собственный POM файл.

Все POM файлы должны иметь три обязательных элемента: groupId, artifactId, version.
В репозитории проект выглядит следующим образом: groupId:artifactId:version.

Ключевой элемент в POM файле – это project, который делится на три главных подгруппы:
– **groupId**. Это ID группы проекта. Зачастую, это уникальная организация или проект. Например, если мы хотим создать   группу, которая отвечает за видео, то groupId будет выглядеть, примерно так:
com.github.code. 
- В этой группе будут все проекты, которые относятся к видео.– **artifactId** Это идентификатор самого проекта. Чаще всего – его имя. Например, maven-video. artifactId также помогает найти проект в репозитории.
– **version**. Версия проекта. Определяет конкретную версию продукта.

Например:
com.github.code:maven-video:1.0
com.github.code:maven-video:1.1

##Супер POM

Все POM-файлы являются наследниками родительского POM. Этот POM-файл называется Super POM и содержит значения, унаследованные по умолчанию.

Простой способ просмотреть настройки по умолчанию Super POM файла – это использование команды:

**mvn help:effective-pom**

Для понимания того, как это работает на практике, рассмотрим простой пример.

Пример:

Создадим простой Maven проект:
![step1](https://i1.wp.com/proselyte.net/wp-content/uploads/2016/03/1.png)

![step2](https://i2.wp.com/proselyte.net/wp-content/uploads/2016/03/2.png)

![step3](https://i1.wp.com/proselyte.net/wp-content/uploads/2016/03/3.png)

![step4](https://i0.wp.com/proselyte.net/wp-content/uploads/2016/03/4.png)

Открываем консоль и пишем следующее: 
```sh
mvn help:effective-pom
```
В результате мы получим, примерно, следующий результат:

```log
[INFO] Scanning for projects...
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.2/maven-jar-plugin-2.2.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.2/maven-jar-plugin-2.2.pom (9 KB at 15.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/10/maven-plugins-10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/10/maven-plugins-10.pom (8 KB at 57.8 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.2/maven-jar-plugin-2.2.jar
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.2/maven-jar-plugin-2.2.jar (27 KB at 184.5 KB/sec)
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- maven-help-plugin:2.2:effective-pom (default-cli) @ MavenTutorial ---
[INFO]
Effective POMs, after inheritance, interpolation, and profiles are applied:

<?xml version="1.0" encoding="UTF-8"?>
<!-- ====================================================================== -->
<!--                                                                        -->
<!-- Generated by Maven Help Plugin on 2016-03-27T08:48:48                  -->
<!-- See: http://maven.apache.org/plugins/maven-help-plugin/                -->
<!--                                                                        -->
<!-- ====================================================================== -->

<!-- ====================================================================== -->
<!--                                                                        -->
<!-- Effective POM for project                                              -->
<!-- 'ProselyteTutorials:MavenTutorial:jar:1.0-SNAPSHOT'                    -->
<!--                                                                        -->
<!-- ====================================================================== -->

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>ProselyteTutorials</groupId>
<artifactId>MavenTutorial</artifactId>
<version>1.0-SNAPSHOT</version>
<repositories>
<repository>
<snapshots>
<enabled>false</enabled>
</snapshots>
<id>central</id>
<name>Central Repository</name>
<url>http://repo.maven.apache.org/maven2</url>
</repository>
</repositories>
<pluginRepositories>
<pluginRepository>
<releases>
<updatePolicy>never</updatePolicy>
</releases>
<snapshots>
<enabled>false</enabled>
</snapshots>
<id>central</id>
<name>Central Repository</name>
<url>http://repo.maven.apache.org/maven2</url>
</pluginRepository>
</pluginRepositories>
<build>
<sourceDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/main/java</sourceDirectory>
<scriptSourceDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/main/scripts</scriptSourceDirectory>
<testSourceDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/test/java</testSourceDirectory>
<outputDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/classes</outputDirectory>
<testOutputDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/test-classes</testOutputDirectory>
<resources>
<resource>
<directory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/main/resources</directory>
</resource>
</resources>
<testResources>
<testResource>
<directory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/test/resources</directory>
</testResource>
</testResources>
<directory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target</directory>
<finalName>MavenTutorial-1.0-SNAPSHOT</finalName>
<pluginManagement>
<plugins>
<plugin>
<artifactId>maven-antrun-plugin</artifactId>
<version>1.3</version>
</plugin>
<plugin>
<artifactId>maven-assembly-plugin</artifactId>
<version>2.2-beta-5</version>
</plugin>
<plugin>
<artifactId>maven-dependency-plugin</artifactId>
<version>2.1</version>
</plugin>
<plugin>
<artifactId>maven-release-plugin</artifactId>
<version>2.0</version>
</plugin>
</plugins>
</pluginManagement>
<plugins>
<plugin>
<artifactId>maven-clean-plugin</artifactId>
<version>2.5</version>
<executions>
<execution>
<id>default-clean</id>
<phase>clean</phase>
<goals>
<goal>clean</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-resources-plugin</artifactId>
<version>2.3</version>
<executions>
<execution>
<id>default-testResources</id>
<phase>process-test-resources</phase>
<goals>
<goal>testResources</goal>
</goals>
</execution>
<execution>
<id>default-resources</id>
<phase>process-resources</phase>
<goals>
<goal>resources</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-jar-plugin</artifactId>
<version>2.2</version>
<executions>
<execution>
<id>default-jar</id>
<phase>package</phase>
<goals>
<goal>jar</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-compiler-plugin</artifactId>
<version>2.0.2</version>
<executions>
<execution>
<id>default-compile</id>
<phase>compile</phase>
<goals>
<goal>compile</goal>
</goals>
</execution>
<execution>
<id>default-testCompile</id>
<phase>test-compile</phase>
<goals>
<goal>testCompile</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-surefire-plugin</artifactId>
<version>2.10</version>
<executions>
<execution>
<id>default-test</id>
<phase>test</phase>
<goals>
<goal>test</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-install-plugin</artifactId>
<version>2.3</version>
<executions>
<execution>
<id>default-install</id>
<phase>install</phase>
<goals>
<goal>install</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-deploy-plugin</artifactId>
<version>2.7</version>
<executions>
<execution>
<id>default-deploy</id>
<phase>deploy</phase>
<goals>
<goal>deploy</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-site-plugin</artifactId>
<version>3.0</version>
<executions>
<execution>
<id>default-site</id>
<phase>site</phase>
<goals>
<goal>site</goal>
</goals>
<configuration>
<outputDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/site</outputDirectory>
<reportPlugins>
<reportPlugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-project-info-reports-plugin</artifactId>
</reportPlugin>
</reportPlugins>
</configuration>
</execution>
<execution>
<id>default-deploy</id>
<phase>site-deploy</phase>
<goals>
<goal>deploy</goal>
</goals>
<configuration>
<outputDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/site</outputDirectory>
<reportPlugins>
<reportPlugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-project-info-reports-plugin</artifactId>
</reportPlugin>
</reportPlugins>
</configuration>
</execution>
</executions>
<configuration>
<outputDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/site</outputDirectory>
<reportPlugins>
<reportPlugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-project-info-reports-plugin</artifactId>
</reportPlugin>
</reportPlugins>
</configuration>
</plugin>
</plugins>
</build>
<reporting>
<outputDirectory>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/site</outputDirectory>
</reporting>
</project>

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.158s
[INFO] Finished at: Sun Mar 27 20:48:48 EEST 2016
[INFO] Final Memory: 11M/150M
[INFO] ------------------------------------------------------------------------
```

В полученном файле мы можем видеть изначальную структуру проекта, директорию вывода, необходимые плагины, репозитории которые Maven будет использовать во время выполнения необходимых задач.

Maven также обеспечивает множество архитипов для создания проектов для создания определённой структуры и файла pom.xml

В этом уроке мы изучили основы файла pom.xml и рассмотрели пример файла effective-pom.

В следующем уроке мы изучим жизненный цикл сборки проекта.

[Дальше](build-life-cycle.md)

[README.md](../../README.md)