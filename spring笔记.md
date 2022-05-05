[https://blog.csdn.net/oneby1314/article/details/114259893](https://blog.csdn.net/oneby1314/article/details/114259893)

## spring入门

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649392041556-4228be54-5f9a-4d63-805a-460fd954a771.png#clientId=u9f978591-dfc9-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=612&id=u13eb737a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=612&originWidth=1026&originalType=binary&ratio=1&rotation=0&showTitle=false&size=176477&status=done&style=none&taskId=u77317900-fece-4b59-95f1-3f323ef8598&title=&width=1026)
入门案例

- 引入依赖
```java
<dependencies>
    <!-- spring-beans -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>5.2.6.RELEASE</version>
    </dependency>

    <!-- spring-context -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.6.RELEASE</version>
    </dependency>

    <!-- spring-core -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.2.6.RELEASE</version>
    </dependency>

    <!-- spring-expression -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-expression</artifactId>
        <version>5.2.6.RELEASE</version>
    </dependency>

    <!-- commons-logging -->
    <dependency>
        <groupId>commons-logging</groupId>
        <artifactId>commons-logging</artifactId>
        <version>1.2</version>
    </dependency>

    <!-- jupiter -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>RELEASE</version>
        <scope>test</scope>
    </dependency>

    <!-- spring-test -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>5.2.6.RELEASE</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

- 创建实体类
```java
public class Student {

    private Integer stuId;
    private String stuName;

    ...

}

```

- 编写spring配置文件
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- 使用bean元素定义一个由IOC容器创建的对象 -->
    <!-- class属性指定用于创建bean的全类名 -->
    <!-- id属性指定用于引用bean实例的标识 -->
    <bean id="student" class="com.oneby.entity.Student">
        <!-- 使用property子元素为bean的属性赋值 -->
        <property name="stuId" value="007"/>
        <property name="stuName" value="Oneby"/>
    </bean>

</beans>
```

- 测试代码
```java
public class SpringTest {

    @Test
    public void gettingStart() {
        //1.创建IOC容器对象
        ApplicationContext iocContainer =
                new ClassPathXmlApplicationContext("getting-start.xml");

        //2.根据id值获取bean实例对象
        Student student = (Student) iocContainer.getbean("student");

        //3.打印bean
        System.out.println(student);
    }

}

```
另一种更强的方法
```java

@SpringJUnitConfig(locations = "classpath:getting-start.xml")
public class SpringTest {

    @Autowired
    private Student student;

    @Test
    public void gettingStart() {
        System.out.println(student);
    }

}

```

## IOC容器和Bean的管理

---

spring提供IOC的两种实现
beanFactory：IOC容器的基本实现，是Spring内部的基础设施，是面向Spring本身的，不是提供给开发人员使用的。
ApplicationContext：beanFactory的子接口，提供了更多高级特性。面向Spring的使用者，几乎所有场合都使用ApplicationContext而不是底层的beanFactory

**ApplicationContext的主要实现类**

1. ClassPathXmlApplicationContext：对应类路径下的XML格式的配置文件
1. FileSystemXmlApplicationContext：对应文件系统中的XML格式的配置文件

**ioc降低耦合度对比**

1. 原始方式
```java
Student stu = new Student();
stu.setStuId(7);
stu.setStuName("Oneby");
```

2. 工厂模式
```xml
<bean id="student" class="com.oneby.entity.Student">
    <property name="stuId" value="007"/>
    <property name="stuName" value="Oneby"/>
</bean>
```
```java
public class StudentFactory {
    public static Student getStudent(){
        String className = ...; // 通过 XML 解析获取全类名
        String[] fieldNames = ..; // 通过 XML 解析获取字段名
        String[] fieldValues = ...; // 通过 XML 解析获取字段值
        Class clazz = Class.forName(className); // 通过反射创建对象实例
        for (int i = 0; i < fieldNames.length; i++) {
            // 依次为字段赋值
        }
        return clazz; // 返回创建的实例对象
    }
}
```

3. ioc管理bean

在通过 iocContainer.getbean("beanId") 方法或者 @Autowire 方式获取 bean 岂不美滋滋，这样我们可以将 bean 的创建与它们之间的依赖关系完全交给 Spring IOC 容器去管理，代码耦合程度极大降低



**bean属性的赋值**

---

1. bean中的setter方式
```java
<!-- 使用property子元素为bean的属性赋值 -->
<bean id="student" class="com.oneby.entity.Student">
    <property name="stuId" value="007"/>
    <property name="stuName" value="Oneby"/>
</bean>
```

2. 构造器赋值
```java
<!-- 通过构造器（constructor-arg）为 bean 的属性赋值 -->
<bean id="student" class="com.oneby.entity.Student">
    <constructor-arg name="stuId" value="1" />
    <constructor-arg name="stuName" value="Oneby" />
</bean>
```

3. 级联属性赋值
```java
<!-- 演示级联属性赋值 -->
<bean id="student" class="com.oneby.entity.Student">
    <property name="computer" ref="computer"/>
    <!-- 设置级联属性(了解) -->
    <property name="computer.computerId" value="233"/>
    <property name="computer.computerName" value="HP"/>
</bean>

<bean id="computer" class="com.oneby.entity.Computer"/>
```

4. p名称空间注入
```java
<!-- 演示 p 名称空间注入属性值 -->
<bean id="student" class="com.oneby.entity.Student" p:stuId="1" p:stuName="Oneby"/>
```

属性赋值的类型

1. 字面量
```java
<!-- 演示字面量的使用 -->
<bean id="student" class="com.oneby.entity.Student">
    <property name="stuId" value="233"/>
    <property name="stuName" value="Oneby"/>
</bean>
```

2. null
```java
<!-- 演示 null 值的使用-->
<bean id="student" class="com.oneby.entity.Student">
    <property name="stuId" value="233"/>
    <!-- 将 stuName 字段的值设置为 null -->
    <property name="stuName">
        <null/>
    </property>
    <!-- 将 computer 字段的值设置为 null -->
    <property name="computer">
        <null/>
    </property>
</bean>

```
3.外部bean
```java
<!-- 引用外部声明的 bean -->
<bean id="student" class="com.oneby.entity.Student">
    <property name="stuId" value="233"/>
    <property name="stuName" value="Oneby"/>
    <!-- 通过 ref 属性引用外部的 bean -->
    <property name="computer" ref="computer"/>
</bean>
<!-- 外部 bean -->
<bean id="computer" class="com.oneby.entity.Computer">
    <property name="computerId" value="255"/>
    <property name="computerName" value="HP"/>
</bean>
```
4.内部bean
```java
<!-- 引用内部声明的 bean -->
<bean id="student" class="com.oneby.entity.Student">
    <property name="stuId" value="233"/>
    <property name="stuName" value="Oneby"/>
    <property name="computer">
        <!-- 通过 <bean> 标签定义内部 bean -->
        <bean class="com.oneby.entity.Computer">
            <property name="computerId" value="255"/>
            <property name="computerName" value="HP"/>
        </bean>
    </property>
</bean>
```

5. 数组
```java
<!-- 演示数组的赋值 -->
<bean id="collectionExample" class="com.oneby.entity.CollectionExample">
    <property name="array">
        <array>
            <value>Oneby</value>
            <value>Heygo</value>
        </array>
    </property>
</bean>
```

6. list
```java
<!-- 演示 List 的赋值 -->
<bean id="collectionExample" class="com.oneby.entity.CollectionExample">
    <property name="list">
        <list>
            <value>Oneby</value>
            <value>Heygo</value>
        </list>
    </property>
</bean>
```
7.set
```java
<!-- 演示 Set 的赋值-->
<bean id="collectionExample" class="com.oneby.entity.CollectionExample">
    <property name="set">
        <set>
            <value>Oneby</value>
            <value>Heygo</value>
        </set>
    </property>
</bean>
```
8.map
```java
<!-- 演示 Map 的赋值-->
<bean id="collectionExample" class="com.oneby.entity.CollectionExample">
    <property name="map">
        <map>
            <entry key="name" value="Oneby"></entry>
            <entry key="hobby" value="code"></entry>
        </map>
    </property>
</bean>
```
9.properties
```java
<!-- 演示 properties 的赋值-->
<bean id="collectionExample" class="com.oneby.entity.CollectionExample">
    <property name="properties">
        <props>
            <prop key="name">Oneby</prop>
            <prop key="hobby">code</prop>
        </props>
    </property>
</bean>
```

10. 集合类型bean
- 引入util名称空间
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation=
               "http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/util
                http://www.springframework.org/schema/util/spring-util.xsd">
```

- 使用
```java
<!-- 集合类型的 bean-->
<util:list id="list">
    <value>Oneby</value>
    <value>Heygo</value>
</util:list>
<bean id="collectionExample" class="com.oneby.entity.CollectionExample">
    <property name="list" ref="list"/>
</bean>
```

### bean的作用域

---

默认情况下，Spring只为每个在IOC容器里声明的bean创建唯一一个实例（单例对象），整个IOC容器范围内都能共享该实例：所有后续的getBean()调用和bean引用都将返回这个唯一的bean实例。该作用域被称为singleton，它是所有bean的默认作用域

设置为prototype
```java
<!-- 演示 bean 的作用域 -->
<bean id="student" class="com.oneby.entity.Student" scope="prototype">
    <property name="stuId" value="233" />
    <property name="stuName" value="Oneby" />
</bean>
```


### bean的生命周期

---

1. 通过构造器或工厂方法创建bean实例
1. 为bean的属性设置值和对其他bean的引用
1. 调用bean的初始化方法
1. bean可以使用了
1. 当容器关闭时，调用bean的销毁方法

- 创建实体类
```java
/**
 * @ClassName Order
 * @Description TODO
 * @Author Oneby
 * @Date 2021/2/21 21:50
 * @Version 1.0
 */
public class Order {

    private String name;

    public Order() {
        System.out.println("第一步：执行无参数构造创建 bean 实例");
    }

    public void setName(String name) {
        this.name = name;
        System.out.println("第二步：调用 setter 方法为属性赋值");
    }

    //  init-method 初始化方法
    public void initMethod(){
        System.out.println("第三步：执行 init-method 初始化方法");
    }

    //  destroy-method 销毁方法
    public void destroyMethod(){
        System.out.println("第五步：执行 destroy-method 初销毁方法");
    }

}

```

- bean
```java
<!-- 演示 bean 的生命周期 -->
<bean id="order" class="com.oneby.entity.Order"
      init-method="initMethod" destroy-method="destroyMethod">
    <property name="name" value="iPad" />
</bean>
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649393846694-273d949c-ff2b-4430-b985-7850f464e540.png#clientId=u9f978591-dfc9-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=248&id=uf28e3f83&margin=%5Bobject%20Object%5D&name=image.png&originHeight=248&originWidth=1023&originalType=binary&ratio=1&rotation=0&showTitle=false&size=103996&status=done&style=none&taskId=ueebfc7a4-81ee-4aaa-a06d-cf251c14615&title=&width=1023)


**添加后置处理器后：**bean后置处理器允许在调用初始化方法前后对bean进行额外的处理

通过构造器或工厂方法创建bean实例
为bean的属性设置值和对其他bean的引用
将bean实例传递给bean后置处理器的postProcessBeforeInitialization()方法
调用bean的初始化方法
将bean实例传递给bean后置处理器的postProcessAfterInitialization()方法
bean可以使用了
当容器关闭时调用bean的销毁方法
[

](https://blog.csdn.net/oneby1314/article/details/114259893)

- 创建后置处理器类
```java

public class MyBeanPost implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("第三步：执行 postProcessBeforeInitialization 方法");
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("第五步：执行 postProcessAfterInitialization 方法");
        return bean;
    }
}

```

- 配置文件
```java
<!-- 演示 bean 的生命周期 -->
<bean id="order" class="com.oneby.entity.Order"
      init-method="initMethod" destroy-method="destroyMethod">
    <property name="name" value="iPad" />
</bean>

<!-- 加上 BeanPostProcessor 后的生命周期 -->
<bean id="myBeanPost" class="com.oneby.config.MyBeanPost"/>
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649394051075-7818a250-43fb-4e30-9d42-d03ccef266c9.png#clientId=u9f978591-dfc9-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=334&id=uc5548ca6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=334&originWidth=1028&originalType=binary&ratio=1&rotation=0&showTitle=false&size=154859&status=done&style=none&taskId=uff704a62-a8e7-4444-9077-89c30f0fca0&title=&width=1028)


### 引入properties文件

---

- 添加context命名空间
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation=
               "http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/context
                http://www.springframework.org/schema/context/spring-context.xsd">
```

- 创建properties文件
```properties
prop.userName=root
prop.password=root
prop.url=jdbc:mysql:///test
prop.driverClass=com.mysql.jdbc.Driver
```

- 使用
```java
<!-- 引用外部属性文件来配置数据库连接池 -->
<!-- 指定 properties 属性文件的位置，classpath:xxx 表示属性文件位于类路径下 -->
<context:property-placeholder location="classpath:jdbc.properties"/>
<!-- 从properties属性文件中引入属性值 -->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="username" value="${prop.userName}"/>
    <property name="password" value="${prop.password}"/>
    <property name="url" value="${prop.url}"/>
    <property name="driverClassName" value="${prop.driverClass}"/>
</bean>
```



### 注解配置bean

---

- 引入依赖
```java
<!-- spring-aop -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
    <version>5.2.6.RELEASE</version>
</dependency>
```

- 引入context名称空间
- 开启组件扫描
```java
<!-- 开启组件扫描 -->
<context:component-scan base-package="com.oneby"/>
```
<context:include-filter>子节点表示要包含的目标类。注意：通常需要与use-default-filters属性配合使用才能够达到“仅包含某些组件”这样的效果。即：通过将use-default-filters属性设置为false，禁用默认过滤器，然后扫描的就只是include-filter中的规则指定的组件了。
<context:exclude-filter>子节点表示要排除在外的目标类
component-scan下可以拥有若干个include-filter和exclude-filter子节点
```java
<!--示例1：use-default-filters="false" 表示现在不使用默认filter，自己配置filter 
	context:include-filter用于设置扫描哪些内容（这里配置只扫描 Controller 注解） -->
<context:component-scan base-package="com.oneby" use-default-filters="false">
    <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan> 

<!--示例2：下面配置扫描包所有内容 context:exclude-filter： 设置哪些内容不进行扫描（这里排除 Controller 注解） -->
<context:component-scan base-package="com.oneby">
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

- 组件装配

@autowired 类型自动装配
@Qualifier    名称自动装配
@Resource 不指定名称按照类型，指定名称按照名称
@value       注入普通属性
```java
@Autowired //根据类型进行注入 
@Qualifier(value = "orderDao1") //根据bean名称进行注入 
private OrderDao orderDao;

//@Resource //根据类型进行注入 
@Resource(name = "orderDao1") //根据bean名称进行注入 
private OrderDao orderDao;

@Value(value = "Oneby") 
private String name;
```


### 全注解开发

---

配置类
```java

@Configuration
@ComponentScan(basePackages = "com.oneby")
public class SpringConfig {

    @Bean
    public OrderService getOrderService(){
        return new OrderService();
    }

}

```
测试
```java
@Test
public void testCompleteAnnotation() {
    //1.创建IOC容器对象
    ApplicationContext iocContainer =
            new AnnotationConfigApplicationContext(SpringConfig.class);

    //2.根据id值获取bean实例对象
    OrderService orderService = (OrderService) iocContainer.getBean("orderService");

    //3.调用bean中的方法
    orderService.sell();
}
```


## AOP

---

连接点：类里面哪些方法可以被增强，这些方法被称为连接点
切入点：实际被真正增强的方法，称为切入点
通知（增强）：实际增强的逻辑部分称为通知（增强）。通知的类型：前置通知、后置通知、环绕通知、异常通知、最终通知
切面：把通知应用到切入点过程（是动作）


ASPECTJ
[1]@Before：前置通知，在方法执行之前执行

[2]@After：后置通知，在方法执行之后执行

[3]@AfterRunning：返回通知，在方法返回结果之后执行

[4]@AfterThrowing：异常通知，在方法抛出异常之后执行

[5]@Around：环绕通知，围绕着方法执行
[

](https://blog.csdn.net/oneby1314/article/details/114259893)

使用

- 引入aop依赖
```java
<!-- spring-aop -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
    <version>5.2.6.RELEASE</version>
</dependency>

<!-- spring-aspects -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>5.2.6.RELEASE</version>
</dependency>

<!-- aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.6</version>
</dependency>

<!-- aopalliance -->
<dependency>
    <groupId>aopalliance</groupId>
    <artifactId>aopalliance</artifactId>
    <version>1.0</version>
</dependency>

<!-- cglib -->
<dependency>
    <groupId>net.sourceforge.cglib</groupId>
    <artifactId>com.springsource.net.sf.cglib</artifactId>
    <version>2.2.0</version>
</dependency>
```

- spring配置文件
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation=
               "http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/context
                http://www.springframework.org/schema/context/spring-context.xsd
                http://www.springframework.org/schema/aop
                http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- 组件扫描 -->
    <context:component-scan base-package="com.oneby"/>

    <!-- 开启 Aspect生成代理对象 -->
    <aop:aspectj-autoproxy/>

</beans>
```

- 普通类
```java
/**
 * @ClassName ArithmeticCalculatorImpl
 * @Description TODO
 * @Author Oneby
 * @Date 2021/2/22 22:02
 * @Version 1.0
 */
@Component
public class ArithmeticCalculatorImpl implements ArithmeticCalculator {
    @Override
    public void add(int i, int j) {
        int result = i + j;
        System.out.println("计算器计算得到的结果为： " + result);
    }

    @Override
    public void sub(int i, int j) {
        int result = i - j;
        System.out.println("计算器计算得到的结果为： " + result);
    }

    @Override
    public void mul(int i, int j) {
        int result = i * j;
        System.out.println("计算器计算得到的结果为： " + result);
    }

    @Override
    public void div(int i, int j) {
        int result = i / j;
        System.out.println("计算器计算得到的结果为： " + result);
    }
}
```

- 切面类

**切入点表达式的语法格式**：execution([权限修饰符] [返回值类型] [简单类名/全类名] [方法名]([参数列表]))
```java
/**
 * @ClassName CalcLoggingAspect
 * @Description TODO
 * @Author Oneby
 * @Date 2021/2/22 21:57
 * @Version 1.0
 */
@Component
@Aspect
public class CalculatorLoggingAspect {

    //解释说明：第一个“*”代表任意修饰符及任意返回值；第二个“*”代表任意方法；“..”匹配任意数量、任意类型的参数
    @Before(value = "execution(* com.oneby.calc.ArithmeticCalculator.*(..))")
    public void before(JoinPoint joinPoint) {
        System.out.println("@Before 前置通知");
    }

    @After(value = "execution(* com.oneby.calc.ArithmeticCalculator.*(..))")
    public void after(JoinPoint joinPoint) {
        System.out.println("@After 后置通知");
    }

    @AfterReturning(value = "execution(* com.oneby.calc.ArithmeticCalculator.*(..))")
    public void afterReturning(JoinPoint joinPoint) {
        System.out.println("@AfterReturning 返回后通知");
    }

    @AfterThrowing(value = "execution(* com.oneby.calc.ArithmeticCalculator.*(..))")
    public void afterThrowing(JoinPoint joinPoint) {
        System.out.println("@AfterThrowing 异常通知");
    }

    @Around(value = "execution(* com.oneby.calc.ArithmeticCalculator.*(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("@Around 环绕通知之前");
        proceedingJoinPoint.proceed(); // 执行目标方法
        System.out.println("@Around 环绕通知之后");
    }
    
}
```

- 测试
```java

public class SpringTest {

    @Test
    public void test() {
        //1.创建IOC容器对象
        ApplicationContext iocContainer =
                new ClassPathXmlApplicationContext("aop-test.xml");

        //2.根据id值获取bean实例对象
        ArithmeticCalculator arithmeticCalculator = iocContainer.getBean(ArithmeticCalculator.class);

        //3.调用bean中的方法
        System.out.println("spring版本：" + SpringVersion.getVersion() + "下的测试");
        arithmeticCalculator.add(1, 1);
    }

}
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649396299019-60055818-0f1a-4a50-82c2-7fe78e9c9dd3.png#clientId=u9f978591-dfc9-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=352&id=u3afb0a6b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=352&originWidth=659&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86014&status=done&style=none&taskId=u4b451fa2-2da7-429b-8e35-4172fd0e383&title=&width=659)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649396425512-fafaf0da-3ad3-4791-b3bb-89ab29ac1d6b.png#clientId=u9f978591-dfc9-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=357&id=u93fa8dde&margin=%5Bobject%20Object%5D&name=image.png&originHeight=357&originWidth=685&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89423&status=done&style=none&taskId=ue6d149ca-a89b-4c74-b0ad-bc6e0c6ce16&title=&width=685)
全注解spring
```java

@Configuration
@ComponentScan(basePackages = "com.oneby")
@EnableAspectJAutoProxy(proxyTargetClass = true)
public class SpringAopConfig {
    
}
```

aop其他操作

- @pointcut 提取表达式
- @Order  指定切入点优先级

xml配置切面
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation=
               "http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/context
                http://www.springframework.org/schema/context/spring-context.xsd
                http://www.springframework.org/schema/aop
                http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- 开启 Aspect 生成代理对象 -->
    <aop:aspectj-autoproxy/>

    <!-- 创建切面类（CalculatorLoggingAspect）和被增强类（ArithmeticCalculatorImpl）的对象 -->
    <bean id="arithmeticCalculatorImpl" class="com.oneby.calc.ArithmeticCalculatorImpl"/>
    <bean id="calculatorLoggingAspect" class="com.oneby.calc.CalculatorLoggingAspect"/>

    <!-- 配置 aop 切入点 -->
    <aop:config>
        <!-- 配置切入点表达式 -->
        <aop:pointcut id="calcPointcut" expression="execution(* com.oneby.calc.ArithmeticCalculator.*(..))"/>
        <!-- 配置切面 -->
        <aop:aspect ref="calculatorLoggingAspect">
            <!-- 配置通知的类型，以及具体切哪些方法 -->
            <aop:before method="before" pointcut-ref="calcPointcut"/>
            <aop:after method="after" pointcut-ref="calcPointcut"/>
            <aop:after-returning method="afterReturning" pointcut-ref="calcPointcut"/>
            <aop:after-throwing method="afterThrowing" pointcut-ref="calcPointcut"/>
            <aop:around method="around" pointcut-ref="calcPointcut"/>
        </aop:aspect>
    </aop:config>

</beans>
```



## JDBCtemplate

---

- 引入依赖
```java
<!-- spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.8.RELEASE</version>
</dependency>

<!-- spring-tx -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
    <version>5.2.8.RELEASE</version>
</dependency>

<!-- spring-orm -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-orm</artifactId>
    <version>5.2.8.RELEASE</version>
</dependency>

<!-- druid -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.9</version>
</dependency>

<!-- mysql -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.8</version>
</dependency>
```

- 数据库文件
```java
prop.userName=root
prop.password=root
prop.url=jdbc:mysql:///test
prop.driverClass=com.mysql.jdbc.Driver
```

- spring配置文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation=
               "http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/context
                http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 组件扫描 -->
    <context:component-scan base-package="com.oneby"/>

    <!-- 引用外部属性文件来配置数据库连接池 -->
    <!-- 指定 properties 属性文件的位置，classpath:xxx 表示属性文件位于类路径下 -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!-- 从properties属性文件中引入属性值 -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="username" value="${prop.userName}"/>
        <property name="password" value="${prop.password}"/>
        <property name="url" value="${prop.url}"/>
        <property name="driverClassName" value="${prop.driverClass}"/>
    </bean>

    <!-- 配置 JdbcTemplate 对象，并注入 dataSource 数据源 -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"/>
    </bean>

</beans>
```

- 实体类
- dao接口
- 持久化
```java
@Repository
public class BookDaoImpl implements BookDao {

    // 注入 JdbcTemplate 对象
    @Autowired
    private JdbcTemplate jdbcTemplate;


    @Override
    public int addBook(Book book) {
        // 创建 SQL 语句
        String sql = "insert into t_books (book_name, book_category) values (?, ?) ";

        // SQL 语句参数
        Object[] args = {book.getBookName(), book.getBookCategory()};

        // 执行 SQL 语句
        int insertRows = jdbcTemplate.update(sql, args);
        return insertRows;
    }

    @Override
    public int deleteBook(String bookId) {
        // 创建 SQL 语句
        String sql = "delete from t_books where book_id = ?";

        // 执行 SQL 语句
        int deleteRows = jdbcTemplate.update(sql, bookId);
        return deleteRows;
    }

    @Override
    public int updateBook(Book book) {
        // 创建 SQL 语句
        String sql = "update t_books set book_name = ?, book_category = ? where book_id = ?";

        // SQL 语句参数
        Object[] args = {book.getBookName(), book.getBookCategory(), book.getBookId()};

        // 执行 SQL 语句
        int insertRows = jdbcTemplate.update(sql, args);
        return insertRows;
    }

    @Override
    public Book findBookInfo(int bookId) {
        // 创建 SQL 语句
        String sql = "select * from t_books where book_id = ?";

        // 执行 SQL 语句
        Book book = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<>(Book.class), bookId);
        return book;
    }

    @Override
    public int findBookCount() {
        // 创建 SQL 语句
        String sql = "select count(*) from t_books";

        // 执行 SQL 语句
        Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
        return count;
    }

    @Override
    public List<Book> findAllBookInfo() {
        // 创建 SQL 语句
        String sql = "select * from t_books";

        // 执行 SQL 语句
        List<Book> books = jdbcTemplate.query(sql, new BeanPropertyRowMapper<Book>(Book.class));
        return books;
    }

    @Override
    public int[] batchAddBook(List<Book> books) {
        // 创建 SQL 语句
        String sql = "insert into t_book (book_name, book_category) values (?, ?)";

        // 构造参数
        List<Object[]> batchArgs = new ArrayList<>();
        for (Book book : books) {
            batchArgs.add(new Object[]{book.getBookName(), book.getBookCategory()});
        }

        // 批量执行
        int[] batchAffectedRows = jdbcTemplate.batchUpdate(sql, batchArgs);
        return batchAffectedRows;
    }

    @Override
    public int[] batchUpdateBook(List<Book> books) {
        // 创建 SQL 语句
        String sql = "update t_books set book_name = ?, book_category = ? where book_id = ?";

        // 构造参数
        List<Object[]> batchArgs = new ArrayList<>();
        for (Book book : books) {
            batchArgs.add(new Object[]{book.getBookName(), book.getBookCategory(), book.getBookId()});
        }

        // 批量执行
        int[] batchAffectedRows = jdbcTemplate.batchUpdate(sql, batchArgs);
        return batchAffectedRows;
    }

    @Override
    public int[] batchDeleteBook(List<Integer> bookIds) {
        // 创建 SQL 语句
        String sql = "delete from t_books where book_id = ?";

        // 构造参数
        List<Object[]> batchArgs = new ArrayList<>();
        for (Integer bookId : bookIds) {
            batchArgs.add(new Object[]{bookId});
        }

        // 批量执行
        int[] batchAffectedRows = jdbcTemplate.batchUpdate(sql, batchArgs);
        return batchAffectedRows;
    }

}

```

## 声明式事务管理

---

- spring配置文件
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation=
               "http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/context
                http://www.springframework.org/schema/context/spring-context.xsd
                http://www.springframework.org/schema/tx
                http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!-- 组件扫描 -->
    <context:component-scan base-package="com.oneby"/>

    <!-- 引用外部属性文件来配置数据库连接池 -->
    <!-- 指定 properties 属性文件的位置，classpath:xxx 表示属性文件位于类路径下 -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!-- 从properties属性文件中引入属性值 -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="username" value="${prop.userName}"/>
        <property name="password" value="${prop.password}"/>
        <property name="url" value="${prop.url}"/>
        <property name="driverClassName" value="${prop.driverClass}"/>
    </bean>

    <!-- 配置 JdbcTemplate 对象，并注入 dataSource 数据源 -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!-- 配置事务管理器（注意：bean 的 id 属性一定要是 transactionManager） -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager" >
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!-- 启用事务注解 -->
    <tx:annotation-driven transaction-manager="transactionManager"/>

</beans>
```

- 添加事务@Transactional

[1]rollbackFor属性：指定遇到时必须进行回滚的异常类型，可以为多个
[2]noRollbackFor属性：指定遇到时不回滚的异常类型，可以为多个
[3] timeout 属性：超时时间
[4] readOnly 只读
```java
/**
 * @ClassName AccountService
 * @Description TODO
 * @Author Oneby
 * @Date 2021/2/24 21:03
 * @Version 1.0
 */
@Service
@Transactional
public class AccountService {

    @Autowired
    private AccountDao accountDao;

    public void transfer(String srcAccountName, String destAccountName, int money) {
        accountDao.tranfer(srcAccountName, money);
        int i = 10 / 0; // 手动制造异常
        accountDao.tranfer(destAccountName, -money);
        System.out.println(srcAccountName + " 向 " + destAccountName + " 转账 " + money + " 元");
    }

}
```

- 事务传播级别
- 事务隔离级别

完全注解
```java
/**
 * @ClassName TransactionConfig
 * @Description TODO
 * @Author Oneby
 * @Date 2021/2/24 22:39
 * @Version 1.0
 */
@Configuration
@ComponentScan(basePackages = "com.oneby")
@EnableTransactionManagement
@PropertySource(value = "classpath:jdbc.properties")
public class TransactionConfig {

    @Value("${prop.userName}")
    private String userName;

    @Value("${prop.password}")
    private String password;

    @Value("${prop.url}")
    private String url;

    @Value("${prop.driverClass}")
    private String driverClass;

    // 数据库连接池
    @Bean
    public DruidDataSource getDruidDataSource() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setUsername(userName);
        dataSource.setPassword(password);
        dataSource.setUrl(url);
        dataSource.setDriverClassName(driverClass);
        return dataSource;
    }

    // 创建 JdbcTemplate 对象
    // DataSource：IOC 容器会自动为我们注入类型为 DataSource 的 bean
    @Bean
    public JdbcTemplate getJdbcTemplate(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }

    // 创建事务管理器
    // DataSource：IOC 容器会自动为我们注入类型为 DataSource 的 bean
    @Bean
    public DataSourceTransactionManager getDataSourceTransactionManager(DataSource dataSource) {
        DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
        transactionManager.setDataSource(dataSource);
        return transactionManager;
    }

}
```

