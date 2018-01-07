---
title: Spring Bean的scope
date: 2018-01-07 20:16:50
tags: 学习
---

scope 描述的是spring容器如何新建Bean实例的。Spring的Scope有以下的几种Scope注解的实现：

 1. Singleton:一个Spring容器中只有一个Bean实例，此为Spring的默认配置
 2. Prototype:每次调用，创建一个新的实例
 3. Request: 在web项目中，给每一个http request 新建一个bean实例
 4. Session: 在web项目中，给每一个http session新建一个实例
 5. GlobalSession: 这个只是在portal应用中有用，给每一个global http session 新建一个实例

##示例演示
（1）编写Singleton的bean

```
package chapter2;

import org.springframework.stereotype.Service;

/**
 * Created by zhanghongbin01 on 2017/4/10.
 */
@Service
public class DemoSingleService {
}

```

(2)编写Prototype的Bean

```
package chapter2;

import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Service;

/**
 * Created by zhanghongbin01 on 2017/4/10.
 */
@Service
@Scope("prototype")
public class DemoProtypeService {
}

```

（3）编写配置类

```
package chapter2;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

/**
 * Created by zhanghongbin01 on 2017/4/10.
 */
@Configuration
@ComponentScan("chapter2")
public class DiConfig {
}

```

（4）在主函数中启动，进行测试

```
package chapter2;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;

/**
 * Created by zhanghongbin01 on 2017/4/10.
 */
public class TestBeanScopMain {

    public static void main(String[] args) {
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(DiConfig.class);
        DemoSingleService single1 = ctx.getBean(DemoSingleService.class);
        DemoSingleService single2 = ctx.getBean(DemoSingleService.class);

        DemoProtypeService p1 = ctx.getBean(DemoProtypeService.class);
        DemoProtypeService p2 = ctx.getBean(DemoProtypeService.class);

        //single1 和single2默认使用的是单例模式，在整个的系统中保持的是单例
        System.out.println("s1和s2是否相等:"+single1.equals(single2));
        //p1和p2使用的是非单例模式，每次都会创建一个新的实例
        System.out.println("p1和p2是否相等:"+p1.equals(p2));
    }
}

```

### 结果演示
![这里写图片描述](http://img.blog.csdn.net/20170410083254740?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2l0aHViXzIwMDY2MDA1/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
