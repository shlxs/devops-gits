# 说明
为了让单个微服务专注于业务代码的开发。由架构组统一研发标准，涉及到`代码规范`、`打包规范`、`部署规范`等方面，下面分别描述

## Gitlab Template
新建工程时选择相应的Template，分别创建`Service`、`Job`等工程

## Gradle插件
打开工程下的build.gradle文件可看到默认引入了`cloud-native`插件
``` gradle
plugins {
    id "com.dobest.cloud-native" version "0.0.1"
}
```
插件里包含了[java](https://docs.gradle.org/current/dsl/org.gradle.api.tasks.JavaExec.html#org.gradle.api.tasks.JavaExec)、[spring-boot](https://plugins.gradle.org/plugin/org.springframework.boot)、[docker](https://plugins.gradle.org/plugin/com.palantir.docker)

## Maven仓库
``` gradle 
repositories {
    maven { url 'http://artifactory:8081/artifactory/gradle-dev/' }
}
```

## JVM参数
``` gradle
compileJava {
    sourceCompatibility = 1.8
    targetCompatibility = 1.8
    options.encoding = 'UTF-8'
}
```

## 配置参数
有些参数在所有模块中都不会变化， 例如端口、日志等。将这些参数统一放到bootstrap.properties，docker打包时与jar放到同一目录
```properties
logging.file=/opt/logs/${"APP_NAME"}.log
logging.file.max-history=10
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
spring.application.name=${"APP_NAME"}
spring.application.version=${"APP_VERSION"}
```

## Spring Boot Starter
提供web、kafka、elasticsearch、jdbc等starter

| Starter | 地址 | 描述 |
| ------ | ------ | ------ |
| web | com.dobest:dobest-cloud-native-web | |
| kafka | com.dobest:dobest-cloud-native-kafka | kafka监控、指标 |
| elasticsearch | com.dobest:dobest-cloud-native-elasticsearch | elasticsearch监控、指标 |

## 依赖版本
每个`cloud-native`插件内置了一组`dobest-cloud-native-dependencies`依赖，指明项目中用到的Spring Boot、Spring Kafka版本，继承自spring-boot-dependencies

| 组ID | 工件ID | 版本 |
| ------ | ------ | ------ |
| org.apache.kafka | kafka_2.11 | 2.1.0 |
| org.apache.kafka | kafka_2.12 | 2.1.0 |
| org.apache.kafka | kafka-clients | 2.1.0 |
| org.apache.kafka | kafka-log4j-appender | 2.1.0 |
| org.apache.kafka | kafka-streams | 2.1.0 |
| org.apache.kafka | kafka-tools | 2.1.0 |
