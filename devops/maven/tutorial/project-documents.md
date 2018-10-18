# Руководство по Maven. Документирование проекта.

В этом уроке мы изучим как создавать документацию проекта.

Для начала нам необходимо перейти в директорию нашего проекта.

После этого выполним в терминале команду:

```sh
mvn site
```
В результате мы получим, примерно, следующий результат:

```log
[INFO] Scanning for projects...
[WARNING] 
[WARNING] Some problems were encountered while building the effective model for ProselyteTutorials:MavenTutorial:jar:1.0-SNAPSHOT
[WARNING] 'dependencies.dependency.systemPath' for someJar:someJar:jar should use a variable instead of a hard-coded path /home/proselyte/Programming/Projects/Proselyte/MavenTutorial/src/lib/someJar.jar @ line 34, column 25
[WARNING] 
[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
[WARNING] 
[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
[WARNING] 
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building MavenTutorial 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
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
[INFO] Generating "Dependencies" report    --- maven-project-info-reports-plugin:2.9
[WARNING] Artifact someJar:someJar:jar:1.0 has no file and won't be listed in dependency files details.
[INFO] Generating "Dependency Convergence" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Dependency Information" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "About" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Plugin Management" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Plugins" report    --- maven-project-info-reports-plugin:2.9
[INFO] Generating "Summary" report    --- maven-project-info-reports-plugin:2.9
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 3.320s
[INFO] Finished at: Wed Apr 27 18:13:58 EEST 2016
[INFO] Final Memory: 17M/260M
[INFO] ------------------------------------------------------------------------
```

После этого перейдём в директорию **target/site** и откроем файл **index.html**.

ProjectSummaryMaven создаёт документацию с помощью механизма documentation-processing, который называется Doxia, который считывает различные форматы в один документ.
Вы можете более подробно ознакомиться с Doxia перейдя по этой ссылке:

http://maven.apache.org/doxia/index.html

На этом мы заканчиваем изучение документирования проектов в Maven.

В следующем уроке мы рассмотрим шаблоны проектов Maven.

[Дальше](project-templates.md)

[README.md](../../README.md)