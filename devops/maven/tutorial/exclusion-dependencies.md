# Руководство по Maven. Исключение транзитивных зависимостей

**Задача**
Исключить нежелательную зависимость библиотеки Struts 1.2.9 при добавлении библиотеки spring-struts

**Решение**
Для интеграции фреймворков Spring и Struts в Maven проект необходимо добавить зависимость библиотеки spring-struts.jar
```xml
  <dependency>
     <groupId>org.springframework</groupId>
     <artifactId>spring-struts</artifactId>
     <version>3.1.0.RELEASE</version>
 </dependency>
```

Данная зависимость тянет за собой транзитивно зависимость на библиотеку Struts версии 1.2.9, в то время как в проекте предполагается использование более поздней вресии Struts 1.3.10
 
Для исключение нежелательных транзитивных зависимостей в Maven начиная с версии 2.x добавлен тег **< exclusions >**.  Для указания библиотек которые не следует добавлять в Classpath, при объявлении тега exclusions необходимо так же указать groupId и artifactId исключаемой библиотеки, указание версии не требуется
```xml
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-struts</artifactId>
    <version>3.1.0.RELEASEversion>
    <exclusions>
       <exclusion>
            <groupId>struts</groupId>
            <artifactId>struts</artifactId>
         </exclusion>
       </exclusions>
  </dependency>
```
Далее можно объявить использование нужной в проекте версии Struts 1.3.10
```xml
  <dependency>
    <groupId>org.apache.struts</groupId>
    <artifactId>struts-core</artifactId>
    <version>1.3.10</version>
  </dependency>
``` 