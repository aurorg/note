# ==javaweb:== springboot+mybatis

## 实现功能：

售票系统：用户浏览电影信息，电影分类查看，搜索查看，购票操作（未实现支付沙箱），超时取消订单等

管理系统：管理员管理影院信息，电影信息，用户角色，角色权限，查看订单信息等功能

安全校验：使用shiro安全框架进行用户请求过滤，密码加密

## 数据库：druid

1. 高性能：Druid使用列存储和索引技术，可以快速响应查询请求，同时支持水平扩展，可以处理海量数据。
2. 高可靠性：Druid提供了多种数据备份和容错机制，可以保证数据的可靠性和一致性。
3. 监控和诊断：Druid提供了丰富的监控指标和诊断工具，可以帮助开发人员快速定位问题。
4. 安全性：Druid提供了多种安全性措施，例如IP白名单、访问密码、SSL加密等，可以保证数据的安全性。

在Spring Boot项目中，使用Druid的步骤：

1. 在Maven或Gradle中添加Druid的依赖：

xml

```java
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>${druid.version}</version>
</dependency>
```

1. 在application.properties或application.yml中配置Druid的数据源：

properties

```java
# 数据源配置
spring.datasource.url=jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf-8&useSSL=false
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.jdbc.Driver

# Druid配置
spring.datasource.druid.initial-size=5
spring.datasource.druid.min-idle=5
spring.datasource.druid.max-active=20
spring.datasource.druid.max-wait=60000
```

1. 在配置类中添加Druid的监控配置：

```java
@Configuration
public class DruidConfig {

    @Bean
    public ServletRegistrationBean statViewServlet() {
        ServletRegistrationBean servletRegistrationBean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");
        Map<String, String> initParams = new HashMap<>();
        initParams.put("loginUsername", "admin");// 用户名
        initParams.put("loginPassword", "123456");// 密码
        servletRegistrationBean.setInitParameters(initParams);
        return servletRegistrationBean;
    }

    @Bean
    public FilterRegistrationBean webStatFilter() {
        FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean(new WebStatFilter());
        filterRegistrationBean.addUrlPatterns("/*");
        Map<String, String> initParams = new HashMap<>();
        initParams.put("exclusions", "*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*");// 过滤掉静态资源
        filterRegistrationBean.setInitParameters(initParams);
        return filterRegistrationBean;
    }
}
```

这样就可以在Spring Boot项目中使用Druid了。Druid提供了丰富的监控指标和诊断工具，可以通过访问Druid的监控页面来查看数据源的使用情况和性能指标。同时，也可以通过Druid的API来获取监控数据和进行诊断分析。

## 分页插件：pageHelper

使用分页插件PageHelper的好处是可以简化分页查询的代码，提高查询效率，并且支持多种数据库的分页查询。

PageHelper是一个开源的MyBatis分页插件，可以通过拦截器的方式在MyBatis执行SQL语句之前自动进行分页处理。它支持多种分页方式，例如基本分页、带有总数统计的分页、滑动窗口分页等，并且支持多种数据库类型，例如MySQL、Oracle、PostgreSQL等。



使用PageHelper的步骤：

1. 在Maven或Gradle中添加PageHelper的依赖：

xml

```java
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>${pagehelper.version}</version>
</dependency>
```

1. 在application.properties或application.yml中配置PageHelper：

properties

```java
# PageHelper配置
pagehelper.helperDialect=mysql
pagehelper.reasonable=true
pagehelper.supportMethodsArguments=true
pagehelper.params=count=countSql
```

1. 在Mapper接口中添加分页方法：

java

```java
public interface UserMapper {
    List<User> findAll();

    List<User> findByPage(@Param("pageNum") int pageNum, @Param("pageSize") int pageSize);
}
```

1. 在Service中调用分页方法：

java

```java
@Service
public class UserServiceImpl implements UserService {

    @Autowired
    private UserMapper userMapper;

    @Override
    public PageInfo<User> findByPage(int pageNum, int pageSize) {
        PageHelper.startPage(pageNum, pageSize);
        List<User> userList = userMapper.findByPage(pageNum, pageSize);
        return new PageInfo<>(userList);
    }
}
```

1. 在Controller中接收分页参数并返回分页结果：

java

```java
@RestController
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/users")
    public PageInfo<User> getUsers(@RequestParam(defaultValue = "1") int pageNum,
                                   @RequestParam(defaultValue = "10") int pageSize) {
        return userService.findByPage(pageNum, pageSize);
    }
}
```

这样就可以在Spring Boot项目中使用PageHelper进行分页查询了。PageHelper会自动拦截MyBatis的SQL语句并进行分页处理，返回分页结果的类型为PageInfo，包含了分页信息和查询结果列表。可以通过PageInfo中的方法来获取分页信息和查询结果。

## 购票操作（未实现支付沙箱），超时取消订单







## 安全校验：使用shiro安全框架进行用户请求过滤，密码加密







## oreo_admin

administrator，系统管理员或网站管理员

主要放登录的功能，以及一些后端和前端交互的Controller

接口

## oreo_common

通用的功能

文件上传

分页的设置

response ：返json数据的格式

springBoot工厂工具类

选座超时处理



## oreo_framework

超时处理+安全加密框架

## oreo_system

后端完成数据的crud

# ==java_front==:vue



