[https://www.yuque.com/atguigu/springboot](https://www.yuque.com/atguigu/springboot)


## 入门案例

---

- 引入依赖
```xml
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
    </parent>


    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

    </dependencies>
```

- 编写properties
```properties
server.port=8888
```

- 创建主程序
```java
/**
 * 主程序类
 * @SpringBootApplication：这是一个SpringBoot应用
 */
@SpringBootApplication
public class MainApplication {

    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
}
```

- 业务类
```java
@RestController
public class HelloController {


    @RequestMapping("/hello")
    public String handle01(){
        return "Hello, Spring Boot 2!";
    }


}
```

- 简化部署(打包成jar包)
```xml
 <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

## 自动装配原理

---

- 自动配好Tomcat
- 自动配好SpringMVC
- 自动配好Web常见功能，如：字符编码问题
- 默认的包结构
   - 主程序所在包及其下面的所有子包里面的组件都会被默认扫描进来
   - 无需以前的包扫描配置
   - 想要改变扫描路径，@SpringBootApplication(scanBasePackages=**"com.atguigu"**)
      - 或者@ComponentScan 指定扫描路径
```java
@SpringBootApplication
等同于
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("com.atguigu.boot")
```

总结：

- SpringBoot先加载所有的自动配置类  xxxxxAutoConfiguration
- 每个自动配置类按照条件进行生效，默认都会绑定配置文件指定的值。xxxxProperties里面拿。xxxProperties和配置文件进行了绑定
- 生效的配置类就会给容器中装配很多组件
- 只要容器中有这些组件，相当于这些功能就有了
- 定制化配置
   - 用户直接自己@Bean替换底层的组件
   - 用户去看这个组件是获取的配置文件什么值就去修改。

**xxxxxAutoConfiguration ---> 组件  ---> xxxxProperties里面拿值  ----> application.properties**

## Web相关

---

### 1 静态资源访问
只要静态资源放在类路径下： called `/static` (or `/public` or `/resources` or `/META-INF/resources`
访问 ： 当前项目根路径/ + 静态资源名 

原理： 静态映射/**。
请求进来，先去找Controller看能不能处理。不能处理的所有请求又都交给静态资源处理器。静态资源也找不到则响应404页面

修改默认静态资源路径
```yaml
spring:
  mvc:
    static-path-pattern: /res/**

  resources:
    static-locations: [classpath:/haha/]
```

### 2、静态资源访问前缀
默认无前缀
```yaml
spring:
  mvc:
    static-path-pattern: /res/**
```
当前项目 + static-path-pattern + 静态资源名 = 静态资源文件夹下找


### 3 数据响应
jackson.jar+@ResponseBody


## 指标监控

---

1. 引入依赖
```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```

2. 使用
- 引入场景
- 访问 [http://localhost:8080/actuator/](http://localhost:8080/actuator/)**
- 暴露所有监控信息为HTTP
```yaml
management:
  endpoints:
    enabled-by-default: true #暴露所有端点信息
    web:
      exposure:
        include: '*'  #以web方式暴露
```

## 配置文件

---

加载顺序

1. 当前jar包内部的application.properties和application.yml
1. 当前jar包内部的application-{profile}.properties 和 application-{profile}.yml
1. 引用的外部jar包的application.properties和application.yml
1. 引用的外部jar包的application-{profile}.properties 和 application-{profile}.yml
