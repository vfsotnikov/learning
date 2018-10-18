# Руководство по Maven. Внешние зависимости.

Ранее мы уже изучали управление зависимостями с помощью репозиториев. Но что, если необходимые файлы не найдены ни в центральном, ни на удалённом репозитории? Для решения этой проблемы используются внешние зависимости.

Рассмотрим такой пример.

Добавим в нам проект в папку **src** директорию **lib**.

Добавьте в эту директорию любой jar файл. Например, someJar.jar.

![ExternalDependencies](https://i1.wp.com/proselyte.net/wp-content/uploads/2016/04/ExternalDependencies.png)

Теперь у нас есть наш собственный jar-файл в проекте.

Для того, чтобы Maven обрабатывал этот пакет, нам необходимо внести следующие изменения в файл **pom.xml**.

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
        
        <!-- External dependency -->
        <dependency>
            <groupId>someJar</groupId>
            <artifactId>someJar</artifactId>
            <scope>system</scope>
            <version>1.0</version>
            <systemPath>/home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/lib/someJar.jar</systemPath>
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

Изучив данный **pom.xml** файл можно сделать несколько выводов по поводу ключевых аспектов внешних зависимостей:
- внешние зависимости могут быть конфигурированы в файле **pom.xml** таким же образом, как и другие зависимости.
- определите groupId таким же именем, как и имя файла.
- определите artifactId таким же именем, как и имя файла.
- определите область видимости зависимости, как system.
- укажите абсолютный путь к файлу.

На этом мы заканчиваем изучение внешних зависимостей.

В следующем уроке мы рассмотрим документирование проекта в Maven.

[Дальше](project-documents.md)

[README.md](../../README.md)