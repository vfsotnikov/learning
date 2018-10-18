# Руководство по Maven. Шаблоны проектов.

С помощью концепции Архитипов Maven обеспечивает большое количество различных шаблонов проектов (более 600). Это помогает пользователям быстро начинать новые проекты используя команду такого вида:

```sh
mvn archetype:generate
```

## Архитип

Архитип – это плагин Maven, задача которого состоит в создании структуры проекта по определённому шаблону. Рассмотри архитип quickstart и создадим с его помощью java-приложение.

## Создание приложения

Переходим в нужную нам директорию и выполняем в терминале следющую команду:

```sh
mvn archetype:generate
```

В результате мы получим следующее:

```log
1576: remote -> uk.ac.ebi.gxa:atlas-archetype (Archetype for generating a custom Atlas webapp)
1577: remote -> uk.ac.rdg.resc:edal-ncwms-based-webapp (-)
1578: remote -> uk.co.nemstix:basic-javaee7-archetype (A basic Java EE7 Maven archetype)
1579: remote -> uk.co.solong:angular-spring-archetype (So Long archetype for RESTful spring services with an AngularJS frontend. Includes debian deployment)
1580: remote -> us.fatehi:schemacrawler-archetype-maven-project (-)
1581: remote -> us.fatehi:schemacrawler-archetype-plugin-command (-)
1582: remote -> us.fatehi:schemacrawler-archetype-plugin-dbconnector (-)
1583: remote -> us.fatehi:schemacrawler-archetype-plugin-lint (-)
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 771: 7
```

Выбираем число 7 и нужную нам версию.
После этого указываем наши параметры.

```log
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 771: 7
Choose am.ik.archetype:spring-boot-jersey-blank-archetype version: 
1: 1.0.0
2: 1.0.1
3: 1.0.2
Choose a number: 3: 1
Define value for property 'groupId': : Tutorials
Define value for property 'artifactId': : MavenTutorial
Define value for property 'version':  1.0-SNAPSHOT: : 
Define value for property 'package':  Tutorials: : net.proselyte.mavenproject
```

И вводим Y, после чего нажимаем Enter.

В итоге мы получим следующий результат:

```log
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Archetype: spring-boot-jersey-blank-archetype:1.0.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: groupId, Value: Tutorials
[INFO] Parameter: artifactId, Value: MavenTutorial
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: net.proselyte.mavenproject
[INFO] Parameter: packageInPathFormat, Value: net/proselyte/mavenproject
[INFO] Parameter: package, Value: net.proselyte.mavenproject
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: groupId, Value: Tutorials
[INFO] Parameter: artifactId, Value: MavenTutorial
[INFO] project created from Archetype in dir: /home/proselyte/Programming/Projects/Proselyte/MavenProject/MavenTutorial
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1:20.860s
[INFO] Finished at: Thu Apr 28 10:29:18 EEST 2016
[INFO] Final Memory: 17M/222M
[INFO] ------------------------------------------------------------------------
```

В результате мы получим следующую структуру проекта:

 
![MavenProject](https://i1.wp.com/proselyte.net/wp-content/uploads/2016/04/MavenProject.png)

Наш **pom.xml** файл будет выглядеть следующим образом:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
   http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <groupId>Tutorials</groupId>
   <artifactId>MavenProject</artifactId>
   <version>1.0-SNAPSHOT</version>
   <packaging>jar</packaging>
   <name>MavenTutorial</name>
   <url>http://maven.apache.org</url>
   <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   <dependencies>
      <dependency>
      <groupId>junit</groupId>
         <artifactId>junit</artifactId>
         <version>3.8.1</version>
         <scope>test</scope>
      </dependency>
   </dependencies>
</project>
```

На этом мы заканчиваем изучение шаблонов проектов. С остальными шаблонами Вы можете ознакомиться на официальном сайте проекта.
В следующем уроке мы рассмотрим снепшоты (snapshots).

[Дальше](snapshots.md)

[README.md](../../README.md)