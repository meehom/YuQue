[https://blog.csdn.net/weixin_44751434/article/details/119358203?spm=1001.2014.3001.5501](https://blog.csdn.net/weixin_44751434/article/details/119358203?spm=1001.2014.3001.5501)


## HelloworldDemo

---

1. 引入依赖
```cpp
<dependencies>
    <!-- SpringMVC -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.1</version>
    </dependency>

    <!-- 日志 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>

    <!-- ServletAPI -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>

    <!-- Spring5和Thymeleaf整合包 -->
    <dependency>
        <groupId>org.thymeleaf</groupId>
        <artifactId>thymeleaf-spring5</artifactId>
        <version>3.0.12.RELEASE</version>
    </dependency>
</dependencies>
```
2.配置springMVC-servlet.xml
```cpp
<!-- 配置SpringMVC的前端控制器，对浏览器发送的请求统一进行处理 -->
<servlet>
    <servlet-name>springMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!-- 通过初始化参数指定SpringMVC配置文件的位置和名称 -->
    <init-param>
        <!-- contextConfigLocation为固定值 -->
        <param-name>contextConfigLocation</param-name>
        <!-- 使用classpath:表示从类路径查找配置文件，例如maven工程中的src/main/resources -->
        <param-value>classpath:springMVC.xml</param-value>
    </init-param>
    <!-- 
 		作为框架的核心组件，在启动过程中有大量的初始化操作要做
		而这些操作放在第一次请求时才执行会严重影响访问速度
		因此需要通过此标签将启动控制DispatcherServlet的初始化时间提前到服务器启动时
	-->
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>springMVC</servlet-name>
    <!--
        设置springMVC的核心控制器所能处理的请求的请求路径
        /所匹配的请求可以是/login或.html或.js或.css方式的请求路径
        但是/不能匹配.jsp请求路径的请求
    -->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

3. 配置springMVC配置文件
```cpp
<!-- 自动扫描包 -->
<context:component-scan base-package="com.atguigu.mvc.controller"/>

<!-- 配置Thymeleaf视图解析器 -->
<bean id="viewResolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
    <property name="order" value="1"/>
    <property name="characterEncoding" value="UTF-8"/>
    <property name="templateEngine">
        <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
            <property name="templateResolver">
                <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
    
                    <!-- 视图前缀 -->
                    <property name="prefix" value="/WEB-INF/templates/"/>
    
                    <!-- 视图后缀 -->
                    <property name="suffix" value=".html"/>
                    <property name="templateMode" value="HTML5"/>
                    <property name="characterEncoding" value="UTF-8" />
                </bean>
            </property>
        </bean>
    </property>
</bean>

<!-- 
   处理静态资源，例如html、js、css、jpg
  若只设置该标签，则只能访问静态资源，其他请求则无法访问
  此时必须设置<mvc:annotation-driven/>解决问题
 -->
<mvc:default-servlet-handler/>

<!-- 开启mvc注解驱动 -->
<mvc:annotation-driven>
    <mvc:message-converters>
        <!-- 处理响应中文内容乱码 -->
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
            <property name="defaultCharset" value="UTF-8" />
            <property name="supportedMediaTypes">
                <list>
                    <value>text/html</value>
                    <value>application/json</value>
                </list>
            </property>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>

```
4.配置控制器
```cpp
// @RequestMapping注解：处理请求和控制器方法之间的映射关系
// @RequestMapping注解的value属性可以通过请求地址匹配请求，/表示的当前工程的上下文路径
// localhost:8080/springMVC/
@RequestMapping("/")
public String index() {
    //设置视图名称
    return "index";
}

@RequestMapping("/hello")
public String HelloWorld() {
    return "target";
}
```
5.配置index.html
```cpp
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>首页</title>
</head>
<body>
    <h1>首页</h1>
    <a th:href="@{/hello}">HelloWorld</a><br/>
</body>
</html>

```
流程：

- 前端控制器DispatcherServlet接收请求，读取springmvc配置文件，扫描组件，找到控制器
- 匹配请求地址和控制器中@RequestMapping注解的value属性值，匹配成功则处理
- 视图解析器渲染页面后返回页面

**补充：**
前端控制器（DispatcherServlet）：主要负责捕获来自客户端的请求和调度各个组件。

处理器映射器（HandlerMapping）：根据url查找后端控制器Handler。

处理器适配器（HandlerAdapter）：执行后端控制器（Handler），拿到后端控制器返回的结果ModelAndView后将结果返回给前端控制器DispatcherServlet。

后端控制器（处理器）（Handler）：主要负责处理前端请求，完成业务逻辑，生成ModelAndView对象返回给HandlerAdapter。

视图解析器（ViewResolver）：主要负责将从DispatcherServlet中拿到的ModelAndView对象进行解析，生成View对象返回给DispatcherServlet。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649386585561-f4eb6b26-9179-4eaa-9b3e-44f55f9736ba.png#clientId=uf56fe337-dcb3-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=656&id=u4fd0b53d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=656&originWidth=881&originalType=binary&ratio=1&rotation=0&showTitle=false&size=315604&status=done&style=none&taskId=u932a34a7-9378-40d2-89ef-cc2272f6360&title=&width=881)


## @RequestMapping注解

---

1.标识类与方法
```java
@Controller
@RequestMapping("/test")
public class RequestMappingController {

	//此时请求映射所映射的请求的请求路径为：/test/testRequestMapping
    @RequestMapping("/testRequestMapping")
    public String testRequestMapping(){
        return "success";
    }

}
```

2. value属性(是一个数组)
```java
@RequestMapping(
        value = {"/testRequestMapping", "/test"}
)
public String testRequestMapping(){
    return "success";
}
```
3.method方法(也是一个数组)
```java
@RequestMapping(
        value = {"/testRequestMapping", "/test"},
        method = {RequestMethod.GET, RequestMethod.POST}
)
public String testRequestMapping(){
    return "success";
}
```

4. param参数
```java
@RequestMapping(
        value = {"/testRequestMapping", "/test"}
        ,method = {RequestMethod.GET, RequestMethod.POST}
        ,params = {"username","password!=123456"}
)
public String testRequestMapping(){
    return "success";
}
```

5. 占位符和@PathVariable
```java
@RequestMapping("/testRest/{id}/{username}")
public String testRest(@PathVariable("id") String id, @PathVariable("username") String username){
    System.out.println("id:"+id+",username:"+username);
    return "success";
}
//最终输出的内容为-->id:1,username:admin
```


## springmvc获取请求参数

---

1. 通过httpservletrequest获取
```java
@RequestMapping("/testParam")
public String testParam(HttpServletRequest request){
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    System.out.println("username:"+username+",password:"+password);
    return "success";
}
```

2. 控制器形参获取
```java
@RequestMapping("/testParam")
public String testParam(String username, String password){
    System.out.println("username:"+username+",password:"+password);
    return "success";
}
```

3. @RequestParam
3. @RequestHeader
3. @CookieValue
3. POJO对象
```java
@RequestMapping("/testpojo")
public String testPOJO(User user){
    System.out.println(user);
    return "success";
}
//最终结果-->User{id=null, username='张三', password='123', age=23, sex='男', email='123@qq.com'}
```

7. 请求参数乱码处理(web.xml)
```java
<!--配置springMVC的编码过滤器-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceResponseEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```



## 域对象共享数据

1. servelet共享数据
```java
@RequestMapping("/testServletAPI")
public String testServletAPI(HttpServletRequest request){
    request.setAttribute("testScope", "hello,servletAPI");
    return "success";
}
```

2. ModelAndView
```java
@RequestMapping("/testModelAndView")
public ModelAndView testModelAndView(){
    /**
     * ModelAndView有Model和View的功能
     * Model主要用于向请求域共享数据
     * View主要用于设置视图，实现页面跳转
     */
    ModelAndView mav = new ModelAndView();
    //向请求域共享数据
    mav.addObject("testScope", "hello,ModelAndView");
    //设置视图，实现页面跳转
    mav.setViewName("success");
    return mav;
}
```
3.model对象
```java
@RequestMapping("/testModel")
public String testModel(Model model){
    model.addAttribute("testScope", "hello,Model");
    return "success";
}
```
4.map对象
```java
@RequestMapping("/testMap")
public String testMap(Map<String, Object> map){
    map.put("testScope", "hello,Map");
    return "success";
}
```
5.modelmap
```java
@RequestMapping("/testModelMap")
public String testModelMap(ModelMap modelMap){
    modelMap.addAttribute("testScope", "hello,ModelMap");
    return "success";
}
```
6.model、modelmap，map关系
Model、ModelMap、Map类型的参数其实本质上都是 BindingAwareModelMap 类型的
7.session域
```java
@RequestMapping("/testSession")
public String testSession(HttpSession session){
    session.setAttribute("testSessionScope", "hello,session");
    return "success";
}
```
8.application域
```java
@RequestMapping("/testApplication")
public String testApplication(HttpSession session){
	ServletContext application = session.getServletContext();
    application.setAttribute("testApplicationScope", "hello,application");
    return "success";
}
```


## 视图

---

1.ThymeleafView
```java
@RequestMapping("/testHello")
public String testHello(){
    return "hello";
}
```
2.转发视图
```java
@RequestMapping("/testForward")
public String testForward(){
    return "forward:/testHello";
}
```
3.重定向
```java
@RequestMapping("/testRedirect")
public String testRedirect(){
    return "redirect:/testHello";
}
```
4.视图控制器
```java
<!--
	path：设置处理的请求地址
	view-name：设置请求地址所对应的视图名称
-->
<mvc:view-controller path="/testView" view-name="success"></mvc:view-controller>
```
注：
当SpringMVC中设置任何一个view-controller时，其他控制器中的请求映射将全部失效，此时需要在SpringMVC的核心配置文件中设置开启mvc注解驱动的标签：
<mvc:annotation-driven />


## Restful

---

| **操作** | **传统方式** | **REST风格** |
| --- | --- | --- |
| 查询操作 | getUserById?id=1 | user/1–>get请求方式 |
| 保存操作 | saveUser | user–>post请求方式 |
| 删除操作 | deleteUser?id=1 | user/1–>delete请求方式 |
| 更新操作 | updateUser | user–>put请求方式 |


hiddenHttpMethodFilter:帮助我们**将 POST 请求转换为 DELETE 或 PUT 请求**
```java
<filter>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```
a>当前请求的请求方式必须为post
b>当前请求必须传输请求参数_method
满足以上条件，**HiddenHttpMethodFilter** 过滤器就会将当前请求的请求方式转换为请求参数_method的值，因此请求参数_method的值才是最终的请求方式


## HttpMessageConverter

---

HttpMessageConverter提供了两个注解和两个类型：@RequestBody，@ResponseBody，RequestEntity，
ResponseEntity

1.@RequestBody
```java
@RequestMapping("/testRequestBody")
public String testRequestBody(@RequestBody String requestBody){
    System.out.println("requestBody:"+requestBody);
    return "success";
}
// requestBody:username=admin&password=123456
```

2. requestEntity
```java
@RequestMapping("/testRequestEntity")
public String testRequestEntity(RequestEntity<String> requestEntity){
    System.out.println("requestHeader:"+requestEntity.getHeaders());
    System.out.println("requestBody:"+requestEntity.getBody());
    return "success";
}
// requestHeader:[host:“localhost:8080”, connection:“keep-alive”, content-length:“27”, cache-control:“max-age=0”, sec-ch-ua:"" Not A;Brand";v=“99”, “Chromium”;v=“90”, “Google Chrome”;v=“90"”, sec-ch-ua-mobile:"?0", upgrade-insecure-requests:“1”, origin:“http://localhost:8080”, user-agent:“Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36”]
// requestBody:username=admin&password=123
```

3. @ResponseBody
```java
@RequestMapping("/testResponseBody")
@ResponseBody
public String testResponseBody(){
    return "success";
}
```

4. 处理json
- 导入依赖
```cpp
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.1</version>
</dependency>
```

- springmvc注解驱动
```java
<mvc:annotation-driven />
```

- 处理器加RequestBody注解
```java
@RequestMapping("/testResponseUser")
@ResponseBody
public User testResponseUser(){
    return new User(1001,"admin","123456",23,"男");
}
```
5.@RestController
6.RespnseEntity


## 文件上传和下载

---

- 文件下载
```java
@RequestMapping("/testDown")
public ResponseEntity<byte[]> testResponseEntity(HttpSession session) throws IOException {
    //获取ServletContext对象
    ServletContext servletContext = session.getServletContext();
    //获取服务器中文件的真实路径
    String realPath = servletContext.getRealPath("/static/img/1.jpg");
    //创建输入流
    InputStream is = new FileInputStream(realPath);
    //创建字节数组
    byte[] bytes = new byte[is.available()];
    //将流读到字节数组中
    is.read(bytes);
    //创建HttpHeaders对象设置响应头信息
    MultiValueMap<String, String> headers = new HttpHeaders();
    //设置要下载方式以及下载文件的名字
    headers.add("Content-Disposition", "attachment;filename=1.jpg");
    //设置响应状态码
    HttpStatus statusCode = HttpStatus.OK;
    //创建ResponseEntity对象
    ResponseEntity<byte[]> responseEntity = new ResponseEntity<>(bytes, headers, statusCode);
    //关闭输入流
    is.close();
    return responseEntity;
}
```

- 文件上传

a.添加依赖
```cpp
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.1</version>
</dependency>
```
b.springmvc配置
```cpp
<!--必须通过文件解析器的解析才能将文件转换为MultipartFile对象-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"></bean>
```
c.控制器方法
```java
@RequestMapping("/testUp")
public String testUp(MultipartFile photo, HttpSession session) throws IOException {
    //获取上传的文件的文件名
    String fileName = photo.getOriginalFilename();
    //处理文件重名问题
    String hzName = fileName.substring(fileName.lastIndexOf("."));
    fileName = UUID.randomUUID().toString() + hzName;
    //获取服务器中photo目录的路径
    ServletContext servletContext = session.getServletContext();
    String photoPath = servletContext.getRealPath("photo");
    File file = new File(photoPath);
    if(!file.exists()){
        file.mkdir();
    }
    String finalPath = photoPath + File.separator + fileName;
    //实现上传功能
    photo.transferTo(new File(finalPath));
    return "success";
}
```

## 拦截器

---

- springmvc配置
```java
<bean class="com.atguigu.interceptor.FirstInterceptor"></bean>
<ref bean="firstInterceptor"></ref>
<!-- 以上两种配置方式都是对DispatcherServlet所处理的所有的请求进行拦截 -->
<mvc:interceptor>
    <mvc:mapping path="/**"/>
    <mvc:exclude-mapping path="/testRequestEntity"/>
    <ref bean="firstInterceptor"></ref>
</mvc:interceptor>
<!-- 
	以上配置方式可以通过ref或bean标签设置拦截器，通过mvc:mapping设置需要拦截的请求，通过mvc:exclude-mapping设置需要排除的请求，即不需要拦截的请求
-->
```



## 异常处理器

---

- springmvc配置
```java
<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
    <property name="exceptionMappings">
        <props>
        	<!--
        		properties的键表示处理器方法执行过程中出现的异常
        		properties的值表示若出现指定异常时，设置一个新的视图名称，跳转到指定页面
        	-->
            <prop key="java.lang.ArithmeticException">error</prop>
        </props>
    </property>
    <!--
    	exceptionAttribute属性设置一个属性名，将出现的异常信息在请求域中进行共享
    -->
    <property name="exceptionAttribute" value="ex"></property>
</bean>

```

- 基于注解@ControllerAdvice
```java
//@ControllerAdvice将当前类标识为异常处理的组件
@ControllerAdvice
public class ExceptionController {

    //@ExceptionHandler用于设置所标识方法处理的异常
    @ExceptionHandler(ArithmeticException.class)
    //ex表示当前请求处理中出现的异常对象
    public String handleArithmeticException(Exception ex, Model model){
        model.addAttribute("ex", ex);
        return "error";
    }

}
```

## 注解配置mvc

---

- 初始化类
```java
public class WebInit extends AbstractAnnotationConfigDispatcherServletInitializer {

    /**
     * 指定spring的配置类
     * @return
     */
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    /**
     * 指定SpringMVC的配置类
     * @return
     */
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{WebConfig.class};
    }

    /**
     * 指定DispatcherServlet的映射规则，即url-pattern
     * @return
     */
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    /**
     * 添加过滤器
     * @return
     */
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter encodingFilter = new CharacterEncodingFilter();
        encodingFilter.setEncoding("UTF-8");
        encodingFilter.setForceRequestEncoding(true);
        HiddenHttpMethodFilter hiddenHttpMethodFilter = new HiddenHttpMethodFilter();
        return new Filter[]{encodingFilter, hiddenHttpMethodFilter};
    }
}
```

- 创建springConfig配置类
```java
@Configuration
public class SpringConfig {
	//ssm整合之后，spring的配置信息写在此类中
}
```

- springmvc配置文件配置类
```java
@Configuration
//扫描组件
@ComponentScan("com.atguigu.mvc.controller")
//开启MVC注解驱动
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    //使用默认的servlet处理静态资源
    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
    }

    //配置文件上传解析器
    @Bean
    public CommonsMultipartResolver multipartResolver(){
        return new CommonsMultipartResolver();
    }

    //配置拦截器
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        FirstInterceptor firstInterceptor = new FirstInterceptor();
        registry.addInterceptor(firstInterceptor).addPathPatterns("/**");
    }
    
    //配置视图控制
    
    /*@Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/").setViewName("index");
    }*/
    
    //配置异常映射
    /*@Override
    public void configureHandlerExceptionResolvers(List<HandlerExceptionResolver> resolvers) {
        SimpleMappingExceptionResolver exceptionResolver = new SimpleMappingExceptionResolver();
        Properties prop = new Properties();
        prop.setProperty("java.lang.ArithmeticException", "error");
        //设置异常映射
        exceptionResolver.setExceptionMappings(prop);
        //设置共享异常信息的键
        exceptionResolver.setExceptionAttribute("ex");
        resolvers.add(exceptionResolver);
    }*/

    //配置生成模板解析器
    @Bean
    public ITemplateResolver templateResolver() {
        WebApplicationContext webApplicationContext = ContextLoader.getCurrentWebApplicationContext();
        // ServletContextTemplateResolver需要一个ServletContext作为构造参数，可通过WebApplicationContext 的方法获得
        ServletContextTemplateResolver templateResolver = new ServletContextTemplateResolver(
                webApplicationContext.getServletContext());
        templateResolver.setPrefix("/WEB-INF/templates/");
        templateResolver.setSuffix(".html");
        templateResolver.setCharacterEncoding("UTF-8");
        templateResolver.setTemplateMode(TemplateMode.HTML);
        return templateResolver;
    }

    //生成模板引擎并为模板引擎注入模板解析器
    @Bean
    public SpringTemplateEngine templateEngine(ITemplateResolver templateResolver) {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver);
        return templateEngine;
    }

    //生成视图解析器并未解析器注入模板引擎
    @Bean
    public ViewResolver viewResolver(SpringTemplateEngine templateEngine) {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
        viewResolver.setCharacterEncoding("UTF-8");
        viewResolver.setTemplateEngine(templateEngine);
        return viewResolver;
    }


}

```

- 测试功能
```java
@RequestMapping("/")
public String index(){
    return "index";
}
```


## springmvc执行流程

---

1. 用户向服务器发送请求，请求被SpringMVC 前端控制器 DispatcherServlet捕获。
1. DispatcherServlet对请求URL进行解析，得到请求资源标识符（URI），判断请求URI对应的映射：

a) 不存在
i. 再判断是否配置了mvc:default-servlet-handler
ii. 如果没配置，则控制台报映射查找不到，客户端展示404错误
iii. 如果有配置，则访问目标资源（一般为静态资源，如：JS,CSS,HTML），找不到客户端也会展示404错误
b) 存在则执行下面的流程

3. 根据该URI，调用HandlerMapping获得该Handler配置的所有相关的对象（包括Handler对象以及Handler对象对应的拦截器），最后以HandlerExecutionChain执行链对象的形式返回。
3. DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter。
3. 如果成功获得HandlerAdapter，此时将开始执行拦截器的preHandler(…)方法【正向】
3. 提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)方法，处理请求。在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作：

a) HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定 	   的响应信息
b) 数据转换：对请求消息进行数据转换。如String转换成Integer、Double等
c) 数据格式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等
d) 数据验证： 验证数据的有效性（长度、格式等），验证结果存储到BindingResult或Error中

7. Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象。
7. 此时将开始执行拦截器的postHandle(…)方法【逆向】
7. 根据返回的ModelAndView（此时会判断是否存在异常：如果存在异常，则执行HandlerExceptionResolver进行异常处理）选择一个适合的ViewResolver进行视图解析，根据Model和View，来渲染视图
7. 渲染视图完毕执行拦截器的afterCompletion(…)方法【逆向】
7. 将渲染结果返回给客户端




## javaweb

---


### servlet

- sevelet是一个接口
- sevlet是三大组件之一，selvet程序，filter过滤器，listener监听器
- sevlet是一个运行在服务端java小程序

入门servlet

- 继承接口
```java
public class HelloServlet implement Servelet{
    
    ...
    
    public void service(...){
        System.out.println("Hello world");
    }
}
```

- 实现方法service
- 编写xml

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649400122411-c223e669-e85b-4c6f-85d7-b1d590094dc5.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=563&id=u4af91d3f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=563&originWidth=1027&originalType=binary&ratio=1&rotation=0&showTitle=false&size=455526&status=done&style=none&taskId=u7eb70724-c4df-4715-ae67-8f5ce68f9ef&title=&width=1027)

子类实现
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649400670334-c7601606-7b38-4c73-8783-bc6048c991ee.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=394&id=u13806faf&margin=%5Bobject%20Object%5D&name=image.png&originHeight=394&originWidth=1398&originalType=binary&ratio=1&rotation=0&showTitle=false&size=227231&status=done&style=none&taskId=uf1ff004f-53bd-4407-98e6-829d6c1ea62&title=&width=1398)



### servletContext

- 是一个接口，表示上下文对象
- 一个web工程，只有一个servletContext对象实例
- 域对象

功能

- 获取web.xml中的上下文对象
- 获取工程路径
- 获取磁盘路径

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649400979018-392a8414-1acf-42d7-a399-1a75132909d8.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=343&id=u034dc7ec&margin=%5Bobject%20Object%5D&name=image.png&originHeight=343&originWidth=794&originalType=binary&ratio=1&rotation=0&showTitle=false&size=219590&status=done&style=none&taskId=u988747df-c5a0-429a-acd6-9cbd86523e8&title=&width=794)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649401151332-477adb51-c489-487d-86a1-f3b2d10a3d70.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=414&id=u211f8185&margin=%5Bobject%20Object%5D&name=image.png&originHeight=414&originWidth=1246&originalType=binary&ratio=1&rotation=0&showTitle=false&size=421456&status=done&style=none&taskId=ue782f12a-2b4b-4247-ae0f-5cfc329be3e&title=&width=1246)




### listener监听器

---

- 三大组件之一

#### ServletContextListener
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649402032145-2a42ac37-8da7-46d3-98e3-0f76a624078c.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=229&id=u3a8a1f94&margin=%5Bobject%20Object%5D&name=image.png&originHeight=229&originWidth=833&originalType=binary&ratio=1&rotation=0&showTitle=false&size=152892&status=done&style=none&taskId=u7db0e1f4-70d6-4d17-9644-f0a19e14ea1&title=&width=833)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649402050483-77549d08-d2d2-44f3-80a5-c2ec757bed81.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=580&id=u7c861880&margin=%5Bobject%20Object%5D&name=image.png&originHeight=580&originWidth=905&originalType=binary&ratio=1&rotation=0&showTitle=false&size=194214&status=done&style=none&taskId=u4186c9f1-f8c6-4f41-94ca-e7c2a8786b8&title=&width=905)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649402071389-2e323566-e006-4693-991c-7190dea332ff.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=216&id=u569953e8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=216&originWidth=742&originalType=binary&ratio=1&rotation=0&showTitle=false&size=85734&status=done&style=none&taskId=ufc5f1fe4-1dc2-44b3-8c97-be7598761fb&title=&width=742)




## Cookie

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649402252635-f8423cd1-36b4-42f3-aec5-228eb44b9913.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=170&id=uafbdb2d5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=170&originWidth=732&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78783&status=done&style=none&taskId=udab5e074-9b17-46e4-94fe-0e5b5b0d6ce&title=&width=732)
### cookie的创建
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649402340505-4d6c14d2-bdc2-4e10-a062-cfc89f7d02ca.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=462&id=u5890cd23&margin=%5Bobject%20Object%5D&name=image.png&originHeight=462&originWidth=1314&originalType=binary&ratio=1&rotation=0&showTitle=false&size=258656&status=done&style=none&taskId=ud3086eae-eaa1-4707-ac2c-cf3a7105667&title=&width=1314)![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649402379565-5dddb088-0464-4b7f-a0cd-9aa5cf276c49.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=465&id=ud98e3436&margin=%5Bobject%20Object%5D&name=image.png&originHeight=465&originWidth=1501&originalType=binary&ratio=1&rotation=0&showTitle=false&size=163793&status=done&style=none&taskId=u1b144490-110e-4c48-9ee3-a5d2254fa38&title=&width=1501)

### cookie对象的获取
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649402567863-6ac96faa-e7f6-440b-8a16-5a66cd47ef3b.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=388&id=ucac1c079&margin=%5Bobject%20Object%5D&name=image.png&originHeight=388&originWidth=1563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=304081&status=done&style=none&taskId=udebc8d2b-5de4-45e8-8da8-0730c27bd3a&title=&width=1563)


### cookie对象的修改
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649403693466-fb0be95d-0658-4992-86a9-7708f4438da3.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=331&id=u9c498df3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=331&originWidth=994&originalType=binary&ratio=1&rotation=0&showTitle=false&size=265805&status=done&style=none&taskId=u95722515-752d-4b21-8118-8c5bf74ea82&title=&width=994)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649403745568-9ce0661e-726f-4976-9dc0-3dd29ff4df7c.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=350&id=u82e86112&margin=%5Bobject%20Object%5D&name=image.png&originHeight=350&originWidth=1107&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274956&status=done&style=none&taskId=ub2b91f73-e060-4f79-a338-7072fbc24c8&title=&width=1107)

### cookie生命周期
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404001599-ee123258-fedf-49fb-8323-ead6fb19e7b6.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=268&id=uf97bfc9f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=268&originWidth=1173&originalType=binary&ratio=1&rotation=0&showTitle=false&size=201655&status=done&style=none&taskId=uff089096-9045-4abf-a77d-e8c8ea3c824&title=&width=1173)

### cookie中path
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404110559-ccccbf6a-1ed3-4da7-9f58-8a62cf4efed5.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=243&id=uf44673a6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=243&originWidth=1073&originalType=binary&ratio=1&rotation=0&showTitle=false&size=160686&status=done&style=none&taskId=u5da4d00d-8045-4626-af91-f336fae77c5&title=&width=1073)


### cookie免密登陆
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404233731-40b394b5-9ab1-4621-8bde-2aade7402fe2.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=373&id=uf6389ea9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=373&originWidth=1076&originalType=binary&ratio=1&rotation=0&showTitle=false&size=280866&status=done&style=none&taskId=u34c02d7b-4aa8-4986-9447-6b74f441da1&title=&width=1076)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404305426-df252534-c1b7-4b72-ad92-68ed1acd0161.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=269&id=ubc05f78d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=269&originWidth=1295&originalType=binary&ratio=1&rotation=0&showTitle=false&size=276577&status=done&style=none&taskId=u11334e38-a0d3-4447-9d31-3da9135ac7c&title=&width=1295)


## session

---

### 创建session
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404612666-89e38e45-24b3-4623-b16a-d968300fe189.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=513&id=uede6e3bb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=513&originWidth=1231&originalType=binary&ratio=1&rotation=0&showTitle=false&size=412492&status=done&style=none&taskId=ufe17bcb9-52d3-4c11-be3d-a782136403f&title=&width=1231)

### 保存session数据
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404742366-a299dbfe-f04d-4d47-98dd-16127ac07318.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=171&id=u27fb9d23&margin=%5Bobject%20Object%5D&name=image.png&originHeight=171&originWidth=1245&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155733&status=done&style=none&taskId=u36f5b6a7-fa03-4cce-91f2-a2d11212a88&title=&width=1245)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404953918-9f3d404c-fc88-4f9d-ae2b-ec6850065ca2.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=133&id=u6c75674e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=133&originWidth=1175&originalType=binary&ratio=1&rotation=0&showTitle=false&size=97843&status=done&style=none&taskId=u8c3fc3cb-7304-420c-a226-59e79694f33&title=&width=1175)
### session生命周期
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649404919365-8f06c348-1c68-4c7e-a9fa-6676cedd8925.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=421&id=u70b225ff&margin=%5Bobject%20Object%5D&name=image.png&originHeight=421&originWidth=1204&originalType=binary&ratio=1&rotation=0&showTitle=false&size=211712&status=done&style=none&taskId=ubed7adea-8455-4792-8dd8-c4e6c3c68b6&title=&width=1204)



### session和cookie的关系（重要）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649405292826-587b8388-9856-49c9-bc6d-8f41dd9e527c.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=824&id=uf1abed45&margin=%5Bobject%20Object%5D&name=image.png&originHeight=824&originWidth=1730&originalType=binary&ratio=1&rotation=0&showTitle=false&size=999911&status=done&style=none&taskId=u44d5e463-7fcb-4a8d-96c2-670cd5dbd2e&title=&width=1730)



## 验证码

---

谷歌验证码
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649405841447-0a2398e7-fd23-47f6-8111-129ba68098f8.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=335&id=ueca80dba&margin=%5Bobject%20Object%5D&name=image.png&originHeight=335&originWidth=1214&originalType=binary&ratio=1&rotation=0&showTitle=false&size=290012&status=done&style=none&taskId=uf3f0b6a1-aa94-48f4-a0d8-e4e2dc82725&title=&width=1214)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649406098586-ae638c82-36d3-4d08-a32f-8274a565fc16.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=470&id=u708288a3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=470&originWidth=1213&originalType=binary&ratio=1&rotation=0&showTitle=false&size=447017&status=done&style=none&taskId=ud06a90ce-f1f1-4c9a-9d79-a6889d9dfd6&title=&width=1213)
验证码切换
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649406525576-0b8a16f2-6000-4423-b4cf-01b8ed76ecdf.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=644&id=ub6f4dbd3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=644&originWidth=1439&originalType=binary&ratio=1&rotation=0&showTitle=false&size=425000&status=done&style=none&taskId=u0258976c-148b-4e4d-b673-3ec9f54bb6a&title=&width=1439)

## JSON

---

### json对象和json字符串之间的转换
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649408190069-18dd985d-12aa-4acc-9e96-712c527f587c.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=276&id=u543ac7e9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=276&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=219503&status=done&style=none&taskId=u998b0b64-e696-4555-942d-aa232ee628b&title=&width=1134)

json字符串和pojo对象之间的转换
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1649408304233-f43dfa22-ad29-4a06-bd2b-a78d3556ba1a.png#clientId=u86322573-10de-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=413&id=ua492d535&margin=%5Bobject%20Object%5D&name=image.png&originHeight=413&originWidth=931&originalType=binary&ratio=1&rotation=0&showTitle=false&size=313428&status=done&style=none&taskId=uaa6c095e-bac2-4636-a56c-e05c7a1b5fb&title=&width=931)
