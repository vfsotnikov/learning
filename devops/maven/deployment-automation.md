# Руководство по Maven. Автоматизация развёртывания (deployment).

При разработке проекта процесс развёртывания состоит из следующих шагов:
- Проверка всего кода проекта в системе контроля версий.
- Скачивание всего исходного кода из системы контроля версий.
- Сборка приложения.
- Получение WAR или EAR файла проекта.
- Развёртывание файла на сервере.
- Обновление документации и обновление номера версии приложения.

## Проблема

Обычно в процессе развёртывания участвуют много человек. Одна команда проверяет код вторая выполняет сборку и т.д. Если всё выполнять вручную, какой-то из моментов может быть упущен и т.д.

## Решение

Здесь приходит на помощь автоматизация развёртывания с помощью комбинирования:
- Сборки и релиза проекта с помощью Maven;
- Использование системы контроля версий (например, Git) для работы с кодом;
- Использования систем управления удалёнными репозиториями (например, Nexus).

## Обновление pom.xml проекта

Для автоматизирования релиза продукта мы будем использовать плагин Maven Release.

Файл **pom.xml** будет выглядеть следующим образом:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
   http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <groupId>bus-core-api</groupId>
   <artifactId>mavenTutorial</artifactId>
   <version>1.0-SNAPSHOT</version>
   <packaging>jar</packaging> 
   <scm>
      <url>http://www.svn.com</url>
      <connection>scm:github:http://localhost:8080/svn/proselyte/tutorial/maven</connection>
      <developerConnection>scm:svn:${username}/${password}@localhost:8080:
      core_features:1102:code</developerConnection>
   </scm>
   <distributionManagement>
      <repository>
         <id>MavenTutorial</id>
         <name>Release repository</name>
         <url>http://localhost:8088/nexus/content/repositories/
         MavenTutorial</url>
      </repository>
   </distributionManagement>
   <build>
      <plugins>
         <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-release-plugin</artifactId>
            <version>2.0-beta-8</version>
            <configuration>
               <useReleaseProfile>false</useReleaseProfile>
               <goals>deploy</goals>
               <scmCommentPrefix>[maven-tutorial-release-checkin]-<
               /scmCommentPrefix>
            </configuration>
         </plugin>
      </plugins>
   </build>
</project>
```

В этом **pom.xml** файле мы использовали следующие важные элементы:
- **Repositories**. Место, где выполняется сборка JAR, WAR, или EAR или другие артифакты, которые будут получены в случае успешной сборки.
- **Plugin**. Элемент maven-release-plugin сконфигурирован для автоматизации процесса развёртывания.
- **SCM**. Определяет расположение системы контроля версий, в которой Maven выполнит проверку исходного кода.

С помощью maven-release-plugin Maven выполняет следующие задачи:

```sh
mvn release:clean
```
Выполняет “очистку” в случае, если релиз не был успешным.

```sh
mvn release:rollback
```
“Откатывает изменения”, которые были сделаны в коде и конфигурациях, если крайний релиз не был успешным.

```sh
mvn release:prepare
```

Выполняет множество операций:
- Проверяет наличие изменений, которые не были внесены в системы контроля версий;
- Проверяет, что нет snapshot зависимостей;
- Обновляет **pom.xml** файл в системе контроля версий;
- Проверяет версию приложения и удаляет snapshot-ы из версии перед релизом;
- Выполняет тесты;
- Выполняет коммит изменённого файла pom.xml;
- Отмечает код в системе контроля версий;
- Изменяет (увеличивает) номер версии и “подтягивает” snapshot-ы для будущих релизов;
- Выполняет коммит изменённых файлов pom.xml в системы контроля версий.

```sh
mvn release:perform
```

Проверяет код, используя предыдущую метку и запускает цель Maven – **deploy** – для развертывания артефакта, полученного в результате сборки на репозитории. 

После того, как проект был успешно запущен выполняется загрузка артефакта в репозиторий.

На этом мы заканчиваем изучение автоматизации развёртывания (deployment).

В следующей статье мы рассмотрим пример веб-приложения, созданного с использованием Maven.

[Дальше](web-project.md)

[README.md](../../README.md)