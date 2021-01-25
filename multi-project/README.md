# Gradle Multi Project 예제

## 1. 'Gradle' 이란?
* 빌드 스크립트의 기초([Build Script Basics](https://docs.gradle.org/current/userguide/tutorial_using_tasks.html))
  - Gradle build 는 **하나 이상의 project 로 구성**되며, 이 project 는 *library JAR 혹은 web application* 이 될 수도 있고, *ZIP 형태의 JARs 등을 배포하는 다수의 프로젝트*가 될 수도 있습니다. 
  - Gradle 의 **project 는 하나 이상의 tasks 로 구성**됩니다. task 는 build 를 수행하는 데에 필요한 원자적인 작업의 단위이며, *class 를 compile 하거나, JAR*를 만들어내거나, *Javadoc 을 만들*거나 혹은 *repository 에 archives 들을 publishing* 하는 작업을 말합니다
  - Gradle tasks 들은 플러그인([applying a plugin](https://docs.gradle.org/current/userguide/plugins.html#sec:plugins_block])을 통해서 수행될 수 있습니다.
* Hello World
  - gradle 커맨드를 통해 수행되는 build 작업은 build.gradle 파일을 통해 수행되며 아래와 같이 groovy (혹은 kotlin) 언어를 통해 구성할 수 있습니다
```groovy
tasks.register('hello') {
  doLast {
    println 'Hello world!'
  }
}
```
  - 아래와 같이 등록된 task 이름 hello 를 명시하며, 여기서 '-q' 옵션은 로그 메시지를 출력하지 않도록 (suppresses Gradle’s log messages)하는 옵션입니다
```bash
bash> ./gradle -q hello
```

## 2. 그레이들 프로젝트 구성
* [Organizing Gradle Projects](https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#organizing_gradle_projects)
  - 

## 3. 커스텀 그레이들 타스크 개발
* [Developing Custom Gradle Task Types](https://docs.gradle.org/current/userguide/custom_tasks.html#custom_tasks)
  - 

## 4. 그레이들 플러그인
* [Using Gradle Plugins](https://docs.gradle.org/current/userguide/plugins.html)

## 5. 스프링 부트 그레이들 연동
* [Spring Boot Gradle Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/gradle-plugin/reference/html/)



## 9. 예제에 앞서
* 스프링 프로젝트의 경우 대부분, common, server, web 등으로 구분되기 마련이고, 항상 참조하는 common 같은 코드를 쉽게 참조하여 사용할 수 있도록 구성되어야 합니다
  - 최신 스프링 부트 버전은 2.4.2 버전입니다
* Gradle 설치를 통해 사용하기 보다는 gradlew 즉 그레이들 래퍼를 사용하여야 호환성이나 향후 여러 사람이 협업 시에도 버전에 따른 문제가 없습니다
  - gradle 은 로컬에 특정 버전을 설치하는 것이고, gradlew 는 gradle/wrapper/gradle-wrapper.properties 파일에 명시된 gradle 버전을 내려받아 사용합니다
  - 현재는 [Gradle 5.6.4](https://docs.gradle.org/5.6.4/userguide/userguide.html) 버전을 사용합니다
  - gradle java application 및 gradle wrapper 생성을 위해 아래와 같이 초기화를 합니다
```bash
bash> gradle init --type java-application --test-framework junit-jupiter
```
* settings.gradle 파일에서 서브 프로젝트를 정의합니다
```gradle
// settings.gradle
rootProject.name = 'multi-project'
include 'module-common', 'module-server'
```
* build.gradle 파일을 아래와 같이 생성합니다
  - ':' 는 디렉토리 경로를 말합니다. 즉 root 위치에서 하나 아래의 경로인 module-server 디렉토리를 지칭하는 :module-server 라고 사용합니다
```gradle
buldscript {
}

subprojects {
}

project(':module-server') {
}
```
* 아래와 같이 2가지 방법으로 플러그인을 연동할 수 있습니다
  - plugins  
```groovy
// Using plugins DSL
plugins {
  id "org.springframework.boot" version "2.4.2"
}

// Using legacy plugin application
buildscript {
  repositories {
    maven {
      url "https://plugins.gradle.org/m2/"
    }
  }
  dependencies {
    classpath "org.springframework.boot:spring-boot-gradle-plugin:2.4.2"
  }
}

apply plugin: "org.springframework.boot"

```
