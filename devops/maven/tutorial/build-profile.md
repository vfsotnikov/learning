#Руководство по Maven. Профиль сборки.

Профиль сборки – это множество настроек, которые могут быть использованы для установки или перезаписи стандартных значений сборки Maven. Используя профиль сборки Maven, мы можем настраивать сборку для различных окружений, таких как Разработка или Продакшн.

Профили настраиваются в файле pom.xml с помощью элементов activeProfiles / profiles и запускаются различными методами. Профили изменяют файл pom.xml во время сборки и используются для передачи параметров различным целевым окружениям, например, в директорию сервера базы данных в продакшн, разработку и тестирования.

Типы профилей сборки

В Maven существует три основных типа профилей сборки:

Тип	Описание
Per Project	Определяется в POM файле, pom.xml
Per User	Определяется в настройках Maven – xml файл (%USER_HOME%/.m2/settings.xml)
Global	Определяется в глобальных настройках – xml файл (%M2_HOME%/conf/settings.xml)
Активация профиля

Профиль сборки Maven может быть активирован различными способами:

Использованием команды в консоли
С помощью настроек Maven
С помощью переменных окружения
Настройках ОС
Существующими, отсутствующими файлами.
 

Для понимания того, как это работает на практике, рассмотрим следующий пример:

Структура проекта:

MavenTutorialStructure

 

В папке scr/main/resources находятся файлы для настройки трёх различных окружений:

Имя файла	Описание
environment.production.properties	Конфигурация продакшн. Когда используется профиль production.
environment.properties	Стандартная конфигурация. Используется по умолчанию.
environment.test.properties	Тестовая конфигурация. Когда используется профиль test.
Явная активация профиля (команда в консоли)

В примере, приведённом ниже мы прикрепим задачу maven-antrun-[lugin:run к фазе test. Это позволит нам получать текстовые сообщения для различных профилей. Мы используем файл pom.xml для определения различных профилей и будем активировать различные профили с помощью команд в консоли.

Пример:


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>net.proselyte.maventutorial</groupId>
    <artifactId>MavenTutorial</artifactId>
    <version>1.0-SNAPSHOT</version>
    <profiles>
        <profile>
            <id>test</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.1</version>
                        <executions>
                            <execution>
                                <phase>test</phase>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                                <configuration>
                                    <tasks>
                                        <echo>Using environment.test.properties</echo>
                                        <copy file="src/main/resources/environment.test.properties" tofile
                                                ="${project.build.outputDirectory}/environment.properties"/>
                                    </tasks>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

Файлы:

environment.properties


environment=debug

environment.test.properties


environment=test

environment.production.properties


environment=production

Теперь откроем консоль и выполним следующую команду:


mvn test -Ptest

В результате мы получим, примерно, следующий результат:


[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 3 resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:testCompile (default-testCompile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ MavenTutorial ---
[INFO] No tests to run.
[INFO] Surefire report directory: /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------

Results :

Tests run: 0, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (default) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] Using environment.test.properties
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.163s
[INFO] Finished at: Sun Mar 27 23:55:31 EEST 2016
[INFO] Final Memory: 9M/212M
[INFO] ------------------------------------------------------------------------

В качестве тренировки мы можем изменить путь к файлу и использовать такие команды:


mvn test -Pnormal


mvn test -Pprod

Активация профиля с помощью настроек Maven

Для начала нам необходимо открыть файл settings.xml, который находится в директории %USER_HOME%/.m2.

Если файла там нет – создадим его.

Активируем тестовый профиль с помощью элемента activeProfile, как показано в примере ниже:


<settings xmlns="http://maven.apache.org/POM/4.0.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
   http://maven.apache.org/xsd/settings-1.0.0.xsd">
   <mirrors>
      <mirror>
         <id>maven.dev.snaponglobal.com</id>
         <name>Internal Artifactory Maven repository</name>
         <url>http://repo1.maven.org/maven2/</url>
         <mirrorOf>*</mirrorOf>
      </mirror>
   </mirrors>
   <activeProfiles>
      <activeProfile>test</activeProfile>
   </activeProfiles>
</settings>

Теперь выполним команду:


mvn test


[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 3 resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:testCompile (default-testCompile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ MavenTutorial ---
[INFO] No tests to run.
[INFO] Surefire report directory: /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------

Results :

Tests run: 0, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.089s
[INFO] Finished at: Mon Mar 28 00:07:04 EEST 2016
[INFO] Final Memory: 7M/150M
[INFO] ------------------------------------------------------------------------

Активация профиля с помощью переменных окружения

Удалим файл settings.xml и изменим профиль test в файле pom.xml. Добавим элемент activation.

Профиль test запустит системное свойство “environment”, которое опредлено, как значение “test”.

Пример:


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>ProselyteTutorials</groupId>
    <artifactId>MavenTutorial</artifactId>
    <version>1.0-SNAPSHOT</version>
    <profiles>
        <profile>
            <id>test</id>
            <activation>
                <property>
                    <name>environment</name>
                    <value>test</value>
                </property>
            </activation>
        </profile>
    </profiles>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

Теперь выполним команду:


mvn test

В результате получим, примерно, следующий результат:


[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 3 resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:testCompile (default-testCompile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ MavenTutorial ---
[INFO] No tests to run.
[INFO] Surefire report directory: /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------

Results :

Tests run: 0, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.234s
[INFO] Finished at: Mon Mar 28 00:14:57 EEST 2016
[INFO] Final Memory: 8M/212M
[INFO] ------------------------------------------------------------------------

Активация профиля с помощью ОС

Для активации профиля с помощью ОС мы должны изменить тип активации в файла pom.xml на следующий:


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>ProselyteTutorials</groupId>
    <artifactId>MavenTutorial</artifactId>
    <version>1.0-SNAPSHOT</version>
    <profiles>
        <profile>
            <id>test</id>
            <activation>
                <os>
                    <name>Ubuntu</name>
                    <family>Linux</family>
                    <arch>x64</arch>
                    <version>14.044 LTS</version>
                </os>
            </activation>
        </profile>
    </profiles>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

Выполняем команду:


mvn test

В результате мы получим, примерно, следующий результат:


[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 3 resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:testCompile (default-testCompile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ MavenTutorial ---
[INFO] No tests to run.
[INFO] Surefire report directory: /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------

Results :

Tests run: 0, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.097s
[INFO] Finished at: Mon Mar 28 00:21:13 EEST 2016
[INFO] Final Memory: 7M/150M
[INFO] ------------------------------------------------------------------------

Активация с помощью присутствующих или отсутствующих файлов

В примере, приведённом ниже, активация профиля произойдёт в случае отсутствия

target/generated-sources/some/dir/net/proselyte/maven

Пример:


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>ProselyteTutorials</groupId>
    <artifactId>MavenTutorial</artifactId>
    <version>1.0-SNAPSHOT</version>
    <profiles>
        <profile>
            <id>test</id>
            <activation>
                <file>
                    <missing>target/generated-sources/some/dir/net/proselyte/maven</missing>
                </file>
            </activation>
        </profile>
    </profiles>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

Выполняем команду:


mvn test

В результате мы получим, примерно, следующий результат:


[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 3 resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.3:testResources (default-testResources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:testCompile (default-testCompile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ MavenTutorial ---
[INFO] No tests to run.
[INFO] Surefire report directory: /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------

Results :

Tests run: 0, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.090s
[INFO] Finished at: Mon Mar 28 00:23:45 EEST 2016
[INFO] Final Memory: 8M/212M
[INFO] ------------------------------------------------------------------------

В этом уроке мы изучили основы профилей сборки приложений и рассмотрели примеры их активации.
В следующем уроке мы изучим репозитории и работу с ними в Maven.