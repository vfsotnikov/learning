#Руководство по Maven. Жизненный цикл сборки.
Жизненный цикл сборки в Maven – это чётко определённая последовательность фаз во время выполнения которых должны быть достигнуты определённые цели.

Типичный жизненный цикл сборки Maven выглядит следующим образом:

Фаза|Действия|Описание
---|---|---
prepare-resources|Копирование ресурсов|В этой фазе происходит копирование ресурсов, которое, также, может быть настроено.
compile|Компиляция|В этой фазе происходит компиляция исходного кода.
package|Создание пакета|В этой фазе, в зависимости от настроек создаётся архив JAR/WAR. Тип архива указывается в pom.xml файле.
install|Установка|В этой фазе происходит установка пакета в локальный/удалённый репозиторий maven.

Каждая из этих фаз имеет фазы **pre** и **post**. Они могут быть использованы для регистрации задач, которые должны быть запущены перед и после указанной фазы.

Когда Maven начинает сборку проекта, он проходит через определённую последовательность фаз и выполняет определённые задачи, которые указаны в каждой из фаз. Maven имеет следующие 3 стандартных жизненных цикла:
- clean
- default
- site

**Задача (goal)** – это специальная задача, которая относится к сборке проекта и его управлению. Она может привязываться как к нескольким фазам, так и ни к одной. Задача, которая не привязана ни к одной фазе, может быть запущена вне фаз сборки с помощью прямого вызова.

Порядок выполнения зависит от порядка вызова целей и фаз.

Например, рассмотрим команду ниже. Аргументы clean и package являются фазами сборки до тех пор, пока dependency: copy-dependencies является задачей.
```sh
mvn clean dependency:copy-dependencies package
```
В этом случае, сначала будет выполнена фаза clean, после этого будет выполнена задача dependency: copy-dependencies. После чего будет выполнена фаза package.

## Жизенный цикл Clean

Когда вы выполняете команду
```sh
mvn post-clean
```
Задача clean Maven  (clean:clean) привязывается к фазе clean в жизненном цикле сборки. Эта задача удаляет ввод сборки путём удаления директории сборки. Таким образом, когда выполняется команда **mvn clean**, Maven удаляет директорию сборки.

Мы можем настроить это поведение указав эти задачи в любой из фаз сборки.

Рассмотрим пример, в котором мы привяжем задачу maven-antrun-plugin:run к фазам pre-clean, clean и post-clean.

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

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>1.1</version>
                <executions>
                    <execution>
                        <id>id.pre-clean</id>
                        <phase>pre-clean</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>pre-clean phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.clean</id>
                        <phase>clean</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>clean phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.post-clean</id>
                        <phase>post-clean</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>post-clean phase</echo>
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
mvn post-clean
```
В результате мы получим следующий результат:
```log
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.pre-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] pre-clean phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ MavenTutorial ---
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] clean phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.post-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] post-clean phase
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.417s
[INFO] Finished at: Sun Mar 27 21:38:15 EEST 2016
[INFO] Final Memory: 7M/150M
[INFO] ------------------------------------------------------------------------
```
Мы также можем выполнить такие же действия для фаз pre-clean и clean.

## Жизненный цикл Default (Build)

Это основной жизненный цикл Maven, который используется для сборки проектов. Он включает в себя 23 фазы:

Фаза жизненного цикла|Описание
---|---
validate | Подтверждает, является ли проект корректным и вся ли необходимая информация доступа для завершения процесса сборки.
initialize | Инициализирует состояние сборки, например, различные настройки.
generate-sources |Включает любой исходный код в фазу компиляции.
process-sources |Обрабатывает исходный код (подготавливает). Например, фильтрует определённые значения.
generate-resources | Генерирует ресурсы, которые должны быть включены в пакет.
process-resources | Копирует и отправляет ресурсы в указанную директорию. Это фаза перед упаковкой.
compile | Комплирует исходный код проекта.
process-classes | Обработка файлов, полученных в результате компиляции. Например, оптимизация байт-кода Java классов.
generate-test-sources | Генерирует любые тестовые ресурсы, которые должны быть включены в фазу компиляции.
process-test-sources | Обрабатывает исходный код тестов. Например, фильтрует значения.
test-compile | Компилирует исходный код тестов в указанную директорию тестов.
process-test-classes | Обрабатывает файлы, полученные в результате компиляции исходного кода тестов.
test | Запускает тесты, используя приемлемый фреймворк юнит-тестирования (например, Junit).
prepare-package | Выполняет все необходимые операции для подготовки пакет, непосредственно перед упаковкой.
package | Преобразует скомпилированный код и пакет в дистрибутивный формат. Такие как JAR, WAR или EAR.
pre-integration-test | Выполняет необходимые действия перед выполнением интеграционных тестов.
integration-test | Обрабатывает и распаковывает пакет, если необходимо, в среду, где будут выполняться интеграционные тесты.
post-integration-test | Выполняет действия, необходимые  после выполнения интеграционных тестов. Например, освобождение ресурсов.
verify | Выполняет любые проверки для подтверждения того, что пакет пригоден и отвечает критериям качества.
install | Устанавливает пакет в локальный репозиторий, который может быть использован как зависимость в других локальных проектах.
deploy | Копирует финальный пакет (архив) в удалённый репозиторий для, того, чтобы сделать его доступным другим разработчикам и проектам.

Необходимо уточнить два момента:
- Когда мы выполняем команду Maven, например install, то будут выполнены фазы до install и фаза install.
- Различные задачи Maven будут привязаны к различным фазам жизненного цикла Maven в зависимости от типа архива (JAR/WAR/EAR).

В следующем примере, мы привязываем задачу maven-antrun-plugin:run к нескольким фазам жизненного цикла сборки. Это также позволяет нам вызывать текстовые сообщения, отображая фазу жизненного цикла.

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
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>1.1</version>
                <executions>
                    <execution>
                        <id>id.validate</id>
                        <phase>validate</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>validate phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.compile</id>
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
                    <execution>
                        <id>id.test</id>
                        <phase>test</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>test phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.package</id>
                        <phase>package</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>package phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.deploy</id>
                        <phase>deploy</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>deploy phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

После этого выполним следующую команду:
```sh
mvn compile
```
В результате мы получим, примерно, следующий результат:
```log
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.pre-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] pre-clean phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ MavenTutorial ---
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] clean phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.post-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] post-clean phase
[INFO] Executed tasks
proselyte@proselyte:~/Programming/Projects/Proselyte/MavenTutorial$ mvn pre-clean 
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.pre-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] pre-clean phase
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.331s
[INFO] Finished at: Sun Mar 27 21:39:39 EEST 2016
[INFO] Final Memory: 7M/150M
[INFO] ------------------------------------------------------------------------
proselyte@proselyte:~/Programming/Projects/Proselyte/MavenTutorial$ mvn clean
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.pre-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] pre-clean phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ MavenTutorial ---
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] clean phase
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.405s
[INFO] Finished at: Sun Mar 27 21:39:45 EEST 2016
[INFO] Final Memory: 6M/119M
[INFO] ------------------------------------------------------------------------
proselyte@proselyte:~/Programming/Projects/Proselyte/MavenTutorial$ mvn post-clean 
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.pre-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] pre-clean phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ MavenTutorial ---
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] clean phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.post-clean) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] post-clean phase
[INFO] Executed tasks
proselyte@proselyte:~/Programming/Projects/Proselyte/MavenTutorial$ mvn compile
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.validate) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] validate phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-resources-plugin:2.3:resources (default-resources) @ MavenTutorial ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 0 resource
[INFO] 
[INFO] --- maven-compiler-plugin:2.0.2:compile (default-compile) @ MavenTutorial ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.compile) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] compile phase
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.824s
[INFO] Finished at: Sun Mar 27 22:07:37 EEST 2016
[INFO] Final Memory: 8M/150M
[INFO] ------------------------------------------------------------------------
```
## Жизненный цикл Site

Плагин Maven – Site – используется для создания докладов, документации, развёртывания и т.д.

Он включает в себя такие фазы:
- pre-site
- site
- post-site
- site-deploy

В примере ниже мы прикрепляем задачу maven-antrun-plugin:run ко всем фазам жизненного цикла Site. Это позволяет нам вызывать текстовые сообщения для отображения фаз жизненного цикла.

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
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>1.1</version>
                <executions>
                    <execution>
                        <id>id.pre-site</id>
                        <phase>pre-site</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>pre-site phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.site</id>
                        <phase>site</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>site phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.post-site</id>
                        <phase>post-site</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>post-site phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                    <execution>
                        <id>id.site-deploy</id>
                        <phase>site-deploy</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <tasks>
                                <echo>site-deploy phase</echo>
                            </tasks>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

Теперь выполним команду Maven:
```sh
mvn site
```
В результате мы получим, примерно, следующий результат:
```log
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.pre-site) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] pre-site phase
[INFO] Executed tasks
[INFO] 
[INFO] --- maven-site-plugin:3.0:site (default-site) @ MavenTutorial ---
[WARNING] Report plugin org.apache.maven.plugins:maven-project-info-reports-plugin has an empty version.
[WARNING] 
[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
[WARNING] 
[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
[INFO] configuring report plugin org.apache.maven.plugins:maven-project-info-reports-plugin:2.9
[WARNING] No project URL defined - decoration links will not be relativized!
[INFO] Rendering site with org.apache.maven.skins:maven-default-skin:jar:1.0 skin.
[INFO] Generating "Dependency Convergence" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Dependency Information" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "About" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Plugin Management" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Plugins" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Summary" report    --- maven-project-info-reports-plugin:2.9
[INFO] 
[INFO] --- maven-antrun-plugin:1.1:run (id.site) @ MavenTutorial ---
[INFO] Executing tasks
     [echo] site phase
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.717s
[INFO] Finished at: Sun Mar 27 23:02:41 EEST 2016
[INFO] Final Memory: 17M/268M
[INFO] ------------------------------------------------------------------------
```
В этом уроке мы изучили основы жизненного цикла сборки проектов в Maven.
В следующем уроке мы изучим профиль сборки.

[Дальше](build-profile.md)

[README.md](../../README.md)