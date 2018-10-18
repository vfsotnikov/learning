# Руководство по Maven. Создание проекта.

Для создания проекта, Maven использует **архитипы**. Для создания простого Java приложения, мы будем использовать плагин **mvn-archetype-quickstart**. В примере, приведённом ниже, мы создадим Java приложение с использованием  Maven в директории **/home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject**.

Для этого нам необходимо открыть терминал и после перехода в необходимую нам директорию выполнить следующую команду:

```sh
/home/proselyte/Programming/Projects/MavenSimpleProject>
mvn archetype:generate
-DgroupId=net.proselyte.mavensimple 
-DartifactId=javaStudent 
-DarchetypeArtifactId=maven-archetype-quickstart 
-DinteractiveMode=false
```

В результате мы получим, примерно, следующий результат:

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
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Old (1.x) Archetype: maven-archetype-quickstart:1.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: basedir, Value: /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject
[INFO] Parameter: package, Value: net.proselyte.mavensimple
[INFO] Parameter: groupId, Value: net.proselyte.mavensimple
[INFO] Parameter: artifactId, Value: javaStudent
[INFO] Parameter: packageName, Value: net.proselyte.mavensimple
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] project created from Old (1.x) Archetype in dir: /home/proselyte/Programming/Projects/Proselyte/MavenSimpleProject/javaStudent
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.927s
[INFO] Finished at: Wed Apr 27 16:40:50 EEST 2016
[INFO] Final Memory: 14M/222M
[INFO] ------------------------------------------------------------------------
```

В указынной директории мы увидим папку **javaStudent**, внутри которой находится папка **src** и файл **pom.xml**

Перейдя в папку **src/main/java** мы найдём исходыне файлы нашего приложения, а в папке **src/main/test** – тесты.

Класс App.java

```java
package net.proselyte.mavensimple;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args )
    {
        System.out.println( "Hello World!" );
    }
}
```
Класс AppTest.java

```java
package net.proselyte.mavensimple;

import junit.framework.Test;
import junit.framework.TestCase;
import junit.framework.TestSuite;

/**
 * Unit test for simple App.
 */
public class AppTest 
    extends TestCase
{
    /**
     * Create the test case
     *
     * @param testName name of the test case
     */
    public AppTest( String testName )
    {
        super( testName );
    }

    /**
     * @return the suite of tests being tested
     */
    public static Test suite()
    {
        return new TestSuite( AppTest.class );
    }

    /**
     * Rigourous Test :-)
     */
    public void testApp()
    {
        assertTrue( true );
    }
}
```
На этом мы заканчиваем наш урок.
В следующей статье мы рассмотрим сборку и тестирование проекта Maven.

[Дальше](build-and-test-project.md)

[README.md](../../README.md)