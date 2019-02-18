# 说明
为了让单个微服务专注于业务代码的开发。由架构组统一研发标准，涉及到`代码规范`、`打包规范`、`部署规范`等方面，下面分别描述

## 配置参数
有些参数在所有模块中都不会变化， 例如端口、日志等。将这些参数统一放到bootstrap.properties，打包时与jar放到同一目录

```properties
logging.file=/opt/logs/${"APP_NAME"}.log
logging.file.max-history=10
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
spring.application.name=${"APP_NAME"}
spring.application.version=${"APP_VERSION"}
```

## 监控与指标
统一外部资源的监控与指标，包括如下一些资源
- kafka
- elasticsearch

## 版本
为了让单个微服务专注于代码的
