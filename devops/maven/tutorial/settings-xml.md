## Maven, где мои артефакты? Еще одна статья про управление зависимостями

Легко жить с maven, когда есть доступ к центральному репозиторию, или у компании есть один корпоративный репозиторий. Все меняется, если работаешь в закрытом контуре, а количество репозиториев ближе к сотне. Под катом история о том, где искать потерявшийся артефакт и как для этого приготовить maven.

**Что будет?**

В статье будут примеры настройки settings, pom, описание поиска в репозиториях. Не будет настройки nexus\artifactory, проблем связанных с ними.

## Начнем с простого

Добавим зависимость на spring в своем pom. 

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.0.0.RELEASE</version>
</dependency>

**pom.xml**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>test</groupId>
    <artifactId>dependency-testing</artifactId>
    <version>1.0.0</version>
    <name>Dependency test</name>

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.0.0.RELEASE</version>
        </dependency>
    </dependencies>
</project>
```
Предположим, что мы только установили maven и не меняли никаких настроек. После инициализации поиска зависимостей через сборку maven, или через ide, maven сначала проверит наличие артефакта в локальном репозитории в директории _${user.home}/.m2/repository/_.

Если в локальном репозитории артефакта нет, то запрос пойдет в репозиторий _central_. 

![local-central](https://habrastorage.org/webt/59/d7/66/59d766a76229b020059817.png)

Мы не указывали этот репозиторий, но он всегда добавляется мавеном при сборке.

**Зачем мне settings.xml?**

В нем можно настроить репозитории, зеркала, прокси, переменные среды и т.д. Прописать один раз и использовать во всех проектах (в идеальном мире)
[Подробнее про settings.xml](https://maven.apache.org/settings.html)

**Сконфигурируем settings.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd"
          xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <profiles>
        <profile>
            <repositories>
                <repository>
                    <id>nexus-corp</id>
                    <name>nexus-corp-repo</name>
                    <url>http://nexus.mycompany.com:8081/nexus/central/</url>
                </repository>
            </repositories>
            <id>nexus</id>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>nexus</activeProfile>
    </activeProfiles>
</settings>
```
<a name="nexus"></a>
С такой конфигурацией порядок поиска будет аналогичен варианту с конфигурацией по умолчанию, но появится дополнительный шаг. Перед тем как пойти в central, мавен попытается скачать артефакт из репозитория nexus-corp.

![local-nexus-central](https://habrastorage.org/webt/59/d7/66/59d766a75a32d249597273.png)

**Зеркало**

Добавим зеркало для репозитория nexus-corp.
```xml
<mirror>
    <id>nexus-corp-mirror</id>
    <name>nexus-corp-mirror</name>
    <url>http://nexus.mirror.mycompany.com:8081/nexus/central/</url>
    <mirrorOf>nexus-corp</mirrorOf>
</mirror>
```
**Когда нужно зеркало?**
- недоступен внешний репозиторий
- для экономии внешнего трафика
- чтобы переопределить репозиторий из settings\pom

[Подробнее про зеркала](https://maven.apache.org/guides/mini/guide-mirror-settings.html)

Когда maven дойдет до шага поиска в репозитории nexus-corp, то вместо него попытается найти артефакт в репозитории _nexus-corp-mirror_. 

При этом если он не найдет его в _nexus-corp-mirror_, то запроса в _nexus-corp_ не будет.

![nexus-mirror](https://habrastorage.org/webt/59/d7/66/59d766a77f365030516424.png)

А если добавить зеркало с wildcard, то все запросы будут направлены на него, если не указаны другие зеркала.
```xml
<mirror>
    <id>all</id>
    <name>nexus-corp-mirror</name>
    <url>http://nexus.mirror.mycompany.com:8081/nexus/central/</url>
    <mirrorOf>*</mirrorOf>
</mirror>
```

# Порядок поиска

В общем случае схема поиска будет такой:
1. Поиск в локальном репо
1. Поиск в репозиториях в порядке объявления с учетом приоритета (либо в их зеркалах)

В конце добавляется _central_. Он всегда последний, если не был перезаписан.

![nexus-mirror-central](https://habrastorage.org/webt/59/d7/61/59d761cc478af917197327.png)

## Merge конфигураций

Перед выполнением сборки maven «склеивает» конфиги: 
- глобальный — ${maven.home}/conf/settings.xml
- пользовательский — ${user.home}/.m2/settings.xml
- проектный — pom.xml

С приоритетом конфигурацией у меня случился небольшой конфуз. [В документации](https://maven.apache.org/settings.html) написано:
```log
The former settings.xml are also called global settings, the latter settings.xml are referred to as user settings. If both files exists, their contents gets merged, with the user-specific settings.xml being dominant.
```
По факту, если при склеивании не возникло конфликтов, то приоритет репозиториев следующий, в порядке уменьшения: 
- глобальный
- пользовательский
- pom.xml

Из примеров ниже порядок будет следующий:
- repo-global-setting1
- repo-user-setting1
- repo-user-setting2
- repo-pom1
- central

**global-settings.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd"
          xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <profiles>
        <profile>
            <repositories>
                <repository>
                    <id>repo-global-setting1</id>
                    <url>http://nexus.mycompany.com:8081/nexus/repo-global-setting1-url/</url>
                </repository>
            </repositories>
            <id>g-nexus</id>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>g-nexus</activeProfile>
    </activeProfiles>
</settings>
```

**user-settings.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd"
          xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <profiles>
        <profile>
            <repositories>
                <repository>
                    <id>repo-user-setting1</id>
                    <url>http://nexus.mycompany.com:8081/nexus/repo-user-setting1-url/</url>
                </repository>
                <repository>
                    <id>repo-user-setting2</id>
                    <url>http://nexus.mycompany.com:8081/nexus/repo-user-setting2-url/</url>
                </repository>
            </repositories>
            <id>nexus</id>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>nexus</activeProfile>
    </activeProfiles>
</settings>
```

pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>test</groupId>
    <artifactId>dependency-testing</artifactId>
    <version>1.0.0</version>
    <name>Dependency test</name>

    <repositories>
        <repository>
            <id>repo-pom1</id>
            <url>http://nexus.mycompany.com:8081/nexus/repo-pom1-url/</url>
        </repository>
    </repositories>
    
    <dependencies>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.25</version>
        </dependency>
    </dependencies>
</project>
```


С разрешением конфликтов появилось еще большее непонимание. Если объявить репозиторий с одним id в разных профилях, то приоритет имеет глобальный конфиг, но если объявить профили с одинаковым id, то приоритет имеет пользовательский. Дальше экспериментировать уже не стал. 

## Поиск пропавших

Так что делать с ошибкой _Could not resolve dependencies for project myproject:jar:1.0.0: Failed to collect dependencies at com.someproject:artifact-name:jar:1.0.0_?

1. Проверить правильность имени и версии артефакта. 
1. Посмотреть какие репозитории\зеркала указаны в ваших settings\pom.
1. Проверить наличие артефакта в этих репозиторииях

Обычно проблема решается на втором шаге, но кроме этих пунктов встречаются проблемы из-за прокси, также бывает, что скаченный jar поврежден(хотя сам я сталкивался с таким всего один раз). 

Для snapshot версий полезна команда -U — принудительное обновление snapshot зависимостей. По умолчанию maven обновляет их только после истечения таймаута раз в день (параметр updatePolicy)

[Дальше](plugins.md)

[README.md](../../README.md)
