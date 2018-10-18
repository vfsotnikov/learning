# Руководство по Maven. Snapshots.

Любое большое приложение состоит из нескольких модулей и, чаще всего над каждым модулем программы работает отдельная команда. Например, одна команда работает над бизнес логикой приложения и они используют проект business-logic (business-logic.jar.1.0), а другая команда работает на внешним видом приложения и разрабатывает проект app-front-end (app-front-end.jar:1.0).

В этом случае может случиться такая ситуация, при которой команда, которая работает над бизнес-логикой и они выпускают обновления каждую неделю и выкладывают его на удалённый репозиторий.

Таким образом, если эта команда часто выкладывает обновления, то можем произойти следующее:
- комнада бизнес логики должна уведомлять команду фронт-ендщиков, когда именно они будут выкладывать обновления;
- команда front-end должна обновлять свой файл **pom.xml** для того, чтобы иметь текущую версию продукта.

Для того, что исправить эту ситуацию используется концепция **snapshot**.

## Snapshot

Snapshot – это специальная версия, которая показывает текущую рабочую копию. При каждой сборке Maven проверяет наличие новой snapshot версии на удалённом репозитории.

В этом случае, команда business-logic будет выпускать snapshot своего обновления на репозиторий в виде business-logic:1.0-SNAPSHOT замещая предыдущий jar файл.

## Snapshot и Версия

В случае с версией, если Maven однажды загрузил версию business-logic:1.0, то он больше не будет пытаться загрузить новую версию 1.0 из репозитория. Для того, чтобы скачать обновлённый продукт business-logic должен быть обновлён до версии 1.1.

В случае со snapshot, Maven автоматически будет подтягивать крайний snapshot (business-logic:1.0-SNAPSHOT) каждый раз, когда команда front-end будет выполнять сборку своего проекта.

Вот как это выглядит в **pom.xml** файле:

**front-end pom.xml**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
   http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <groupId>front-end</groupId>
   <artifactId>front-end</artifactId>
   <version>1.0</version>
   <packaging>jar</packaging>
   <name>maventutorial</name>
   <url>http://maven.apache.org</url>
   <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   <dependencies>
      <dependency>
      <groupId>data-service</groupId>
         <artifactId>business-logic</artifactId>
         <version>1.0-SNAPSHOT</version>
         <scope>test</scope>
      </dependency>
   </dependencies>
</project>
```

business-logic pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
   http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <groupId>business-logic</groupId>
   <artifactId>business-logic</artifactId>
   <version>1.0-SNAPSHOT</version>
   <packaging>jar</packaging>
   <name>maven-tutorial</name>
   <url>http://maven.apache.org</url>
   <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   </project>
```

Для того чтобы подтянуть крайний snapshot нам необходимо использовать -U в каждой команде.

```sh
mvn clean package -U
```
На этом мы заканчиваем изучение snapshot-ов.
В следующей статье мы рассмотрим управление зависимостями.

[Дальше](build-automation.md)

[README.md](../../README.md)