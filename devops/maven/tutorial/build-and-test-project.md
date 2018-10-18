# Руководство по Maven. Сборка и тестирование проекта.

В предыдущем разделе мы рассмотрели создание Java приложения с помощью Maven. Теперь мы рассмотрим, как собрать и протестировать наше приложение.

Наш **pom.xml** файл выглядит следующим образом:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>net.proselyte.mavensimple</groupId>
  <artifactId>javaStudent</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>javaStudent</name>
  <url>http://maven.apache.org</url>
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
Мы видим, что Maven автоматически добавил зависимости Junit в наш проект.

В терминале перейдём в директорию нашего проекта в папку javaStudent и напишем следующее:

```sh
mvn clean package
```

В результате мы получим следующий результат:

```log
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building javaStudent 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ javaStudent ---
[INFO] Deleting /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent/target
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ javaStudent ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ javaStudent ---
[INFO] Compiling 1 source file to /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent/target/classes
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ javaStudent ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:testCompile (default-testCompile) @ javaStudent ---
[INFO] Compiling 1 source file to /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ javaStudent ---
[INFO] Surefire report directory: /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running net.proselyte.mavensimple.AppTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.018 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-jar-plugin:2.2:jar (default-jar) @ javaStudent ---
[INFO] Building jar: /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent/target/javaStudent-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.071s
[INFO] Finished at: Wed Apr 27 17:04:01 EEST 2016
[INFO] Final Memory: 19M/190M
[INFO] ------------------------------------------------------------------------
```

Теперь попробуем запустить наше приложение.
Выполним в терминале следующую команду:

```sh
 cd target/classes
```

А затем следующую:

```sh
java net.proselyte.mavensimple.App
```

В результате мы получим, следующий результат:

```log
/*Some system messages*/
Hello World!
```

На этом мы заканчиваем изучение данного урока.
В следующей статье мы рассмотрим внешние зависимости.

[Дальше](external-dependencies.md)

[README.md](../../README.md)