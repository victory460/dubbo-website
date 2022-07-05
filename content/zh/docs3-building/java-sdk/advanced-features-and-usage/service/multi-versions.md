---
type: docs
title: "服务分版本"
linkTitle: "服务分版本"
weight: 1
description: "在 Dubbo 中为同一个服务配置多个版本"
---
## 特性说明
按照以下的步骤进行版本迁移：

1. 在低压力时间段，先升级一半提供者为新版本
2. 再将所有消费者升级为新版本
3. 然后将剩下的一半提供者升级为新版本

配置
- 新旧版本服务提供者
- 新旧版本服务消费者

## 使用场景
当一个接口实现，出现不兼容升级时，可以用版本号过渡，版本号不同的服务相互间不引用。
## 使用方式
- 服务提供者
老版本服务提供者配置：
```xml
<dubbo:service interface="com.foo.BarService" version="1.0.0" />
```

新版本服务提供者配置：
```xml
<dubbo:service interface="com.foo.BarService" version="2.0.0" />
```
- 服务消费者
老版本服务消费者配置：
```xml
<dubbo:reference id="barService" interface="com.foo.BarService" version="1.0.0" />
```

新版本服务消费者配置：
```xml
<dubbo:reference id="barService" interface="com.foo.BarService" version="2.0.0" />
```

如果不需要区分版本，可以按照以下的方式配置：
```xml
<dubbo:reference id="barService" interface="com.foo.BarService" version="*" />
```
#### 提示：
`2.2.0` 以上版本支持