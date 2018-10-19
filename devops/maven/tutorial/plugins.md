# Руководство по Maven. Плагины.
Если говорить в целом, то Maven – это фреймворк, который выполняет плагины. В этом фреймворке каждая задача, по сути своей, выполняется с помощью плагинов.

Единого списка всех плагинов естественно не существует, на [официальном сайте](http://maven.apache.org/plugins/) только есть поддерживаемые плагины непосредственно разработчиками Maven. Однако хотелось бы отметить, что названия плагинов довольно прямолинейны и сделав поиск по ключевым словам **«maven tomcat plugin»** вы скорее всего обнаружите первой ссылкой плагин для деплоймента проекта в Tomcat.

Плагины Maven использутся для:
- создания jar – файла
- создания war – файла
- компиляции кода файлов
- юнит-тестирования кода
- создание отчётов проекта
- создание документации проекта

В общей форме, плагин обеспечивает набор целей, которые могут быть выполнены с помощью такого синтаксиса:

```sh
mvn [имя-плагина]:[имя-цели]
```

Например, для того, чтобы выполнить компиляцию проекта нам необходимо использовать следующую команду:

```sh
mvn compiler:compile
```

## Типы плагинов

Существует два типа плагинов в Maven:

- **Плагины сборки**. Выполняются в процессе сборки и должны быть конфигурированны внутри блока <build></build> файла pom.xml
- **Плагины отчётов**. Выполняются в процесса генерирования сайта и должны быть конфигурированны внутри блока <reporting></reporting> файла pom.xml.

Вот список, наиболее используемых плагинов:
- **clean**. Очищает цель после сборки. Удаляет директорию target.
- **compiler**. Компилирует исходные Java файлы.
- **surefire**. Запускает тесты JUnit. Создаёт отчёты о тестировании.
- **jar**. Собирает JAR файл текущего проекта.
- **war**. Собирает WAR файл текущего проекта.
- **javadoc**. Генерирует Javadoc проекта.
- **antrun**. Запускает набор задач ant из любой указанной фазы.

Для понимания того, как это работает на практике, рассмотрим следующий пример.

Пример:

```xml
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
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>1.1</version>
                <executions>
                    <execution>
                        <id>id.clean</id>
                        <phase>compile</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>compile phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

После этого выполним в терминале следующую команду:

```sh
mvn compile
```

В результате выполнения команды, мы получим, примерно, следующий результат:

```log
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
[INFO] --- maven-antrun-plugin:1.1:run (id.clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] compile phase
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.620s
[INFO] Finished at: Wed Apr 27 16:21:41 EEST 2016
[INFO] Final Memory: 6M/150M
[INFO] ------------------------------------------------------------------------
```

Пример, приведённый выше, демонстрирует следующие ключевые концепции:

- Плагины указываются в файле pom.xml внутри блока <plugins></plugins>
- Каждый плагин может иметь несколько целей.
- Мы можем определять фазу, из которой мы можем начать выполнение плагина. В примере выше мы использовали фазу compile.

На этом мы заканчиваем изучение плагинов.

В следующем уроке мы рассмотрим создание проекта Maven.

[Дальше](project-creation.md)

[README.md](../../README.md)