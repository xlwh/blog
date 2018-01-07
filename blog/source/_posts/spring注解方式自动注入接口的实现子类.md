---
title: spring注解方式自动注入接口的实现子类
date: 2018-01-07 20:20:21
tags: 随笔
---

applicationContext.xml配置文件加入：

 

```
<context:annotation-config/>
```

作用是隐式地向 Spring 容器注册

> AutowiredAnnotationBeanPostProcessor、CommonAnnotationBeanPostProcessor、
> 
> PersistenceAnnotationBeanPostProcessor 以及
> RequiredAnnotationBeanPostProcessor 这 4 个BeanPostProcessor。

注册这4个 BeanPostProcessor的作用，就是为了你的系统能够识别相应的注解。

 

 

 

```
   <!--
设置需要进行Spring注解扫描的类包 -->

<context:component-scan
base-package="xx.xx"
/> 可以用*代表所有

@Service()

publicclass ServiceImpl
implements Service
```

调用时：

```
    @Resource()

private Service
Service;
```

 

这样的话就能实现自动注入了

@Service一般用来定义Service层 dao，action都有对应的注解网上可查
