# Swagger2

## 一、简介

Swagger 是一个规范和完整的框架，用于生成、描述、调用和可视化 RESTful 风格的 Web 服务。总体目标是使客户端和文件系统作为服务器以同样的速度来更新。文件的方法，参数和模型紧密集成到服务器端的代码，允许API来始终保持同步。

总结：跟Knife4J一样，是个自动生成API文档，可以进行在线调试的框架

## 二、快速开始

**1、导入依赖**

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.8.0</version>
</dependency>
```

**2、编写配置类**

```java

package com.swaggerTest;
 
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
 
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;
 
/**
 * Swagger2配置类
 * 在与spring boot集成时，放在与Application.java同级的目录下。
 * 通过@Configuration注解，让Spring来加载该类配置。
 * 再通过@EnableSwagger2注解来启用Swagger2。
 */
@Configuration
@EnableSwagger2
public class Swagger2 {
    
    @Value("${swagger.enable}")
    private boolean swaggerEnable;
    
    /**
     * 创建API应用
     * apiInfo() 增加API相关信息
     * 通过select()函数返回一个ApiSelectorBuilder实例,用来控制哪些接口暴露给Swagger来展现，
     * 本例采用指定扫描的包路径来定义指定要建立API的目录。
     * 
     * @return
     */
    @Bean
    public Docket createRestApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .enable(swaggerEnable)
                .apiInfo(apiInfo())
                .select()
                //.apis(RequestHandlerSelectors
                //      .basePackage("com.swaggerTest.controller")
                //     )
                .apis(RequestHandlerSelectors.withClassAnnotation(Api.class))
                .paths(PathSelectors.any())
                .build();
    }
    
    /**
     * 创建该API的基本信息（这些基本信息会展现在文档页面中）
     * 访问地址：http://项目实际地址/swagger-ui.html
     * @return
     */
    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("Spring Boot中使用Swagger2构建RESTful APIs")
                .description("xx相关接口的文档"")
                .termsOfServiceUrl("http://www.baidu.com")
                .contact("sunf")
                .version("1.0")
                .build();
    }
```

说明：

- apiInfo：api基本信息的配置，信息会在api文档上显示，可有选择的填充，比如配置文档名称、项目版本号等
- apis：使用什么样的方式来扫描接口，RequestHandlerSelectors下共有五种方法可选。我们当前使用通过在类前添加@Api注解的方式，其他方法我们后续介绍。
- path：扫描接口的路径，PathSelectors下有四种方法，我们这里是全扫，其他方法我们后续介绍。

**3、在接口文件中增加对应注解。**

代码如下，由于我们第二步选择扫描接口的方式是在**类**前添加@Api；

@ApiOperation用于注明接口，value是接口的解释；

@ApiParam注解函数里面的参数，name一般与参数名一致，value是解释，required是是否参数必须。

```java
package com.swaggerTest.controller;
 
import org.springframework.stereotype.Controller;
import org.springframework.util.StringUtils;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;
 
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiImplicitParam;
import io.swagger.annotations.ApiImplicitParams;
import io.swagger.annotations.ApiOperation;
 
/**
 * 一个用来测试swagger注解的控制器
 * 注意@ApiImplicitParam的使用会影响程序运行，如果使用不当可能造成控制器收不到消息
 */
@RestController
@RequestMapping("/say")
@Api(value = "SayController|一个用来测试swagger注解的控制器")
public class SayController {
    
    @RequestMapping(value ="/getUserName", method= RequestMethod.GET)
    @ApiOperation(value="根据用户编号获取用户姓名", notes="test: 仅1和2有正确返回")
    @ApiImplicitParam(paramType="query", name = "userNumber", value = "用户编号", required = true, dataType = "Integer")
    public String getUserName(@RequestParam Integer userNumber){
        if(userNumber == 1){
            return "张三丰";
        }
        else if(userNumber == 2){
            return "慕容复";
        }
        else{
            return "未知";
        }
    }
    
    @RequestMapping("/updatePassword")
    @ApiOperation(value="修改用户密码", notes="根据用户id修改密码")
    @ApiImplicitParams({
        @ApiImplicitParam(paramType="query", name = "userId", value = "用户ID", required = true, dataType = "Integer"),
        @ApiImplicitParam(paramType="query", name = "password", value = "旧密码", required = true, dataType = "String"),
        @ApiImplicitParam(paramType="query", name = "newPassword", value = "新密码", required = true, dataType = "String")
    })
    public String updatePassword(@RequestParam(value="userId") Integer userId, @RequestParam(value="password") String password, 
            @RequestParam(value="newPassword") String newPassword){
      if(userId <= 0 || userId > 2){
          return "未知的用户";
      }
      if(StringUtils.isEmpty(password) || StringUtils.isEmpty(newPassword)){
          return "密码不能为空";
      }
      if(password.equals(newPassword)){
          return "新旧密码不能相同";
      }
      return "密码修改成功!";
    }
}
```

**4、测试**

在浏览器中输入网址：http://localhost:8080/swagger-ui.html，如默认的8080，以自己项目的配置为准。

## 三、注解

@Api： 用于类，标识这个类是swagger的资源

@ApiIgnore： 用于类，忽略该 Controller，指不对当前类做扫描

@ApiOperation： 用于方法，描述 Controller类中的 method接口，来给API增加方法说明

@ApiParam： 用于参数，单个参数描述，与 @ApiImplicitParam不同的是，他是写在参数左侧的。如（ @ApiParam(name="username",value="用户名")Stringusername）

@ApiModel： 用于类，表示对类进行说明，用于参数用实体类接收

- @ApiProperty：用于方法，字段，表示对model属性的说明或者数据操作更改

@ApiImplicitParam： 用于方法，表示单独的请求参数。用注解来给方法入参增加说明

- **paramType**：指定参数放在哪个地方
- name：参数名
- dataType：参数类型
- required：参数是否必须传
- value：说明参数的意思
- defaultValue：参数的默认值

@ApiImplicitParams： 用于方法，包含多个 @ApiImplicitParam

@ApiResponse： 用于方法，描述单个出参信息

- **code**：数字，例如400
- **message**：信息，例如"请求参数没填好"
- **response**：抛出异常的类  

@ApiResponses： 用于方法，包含多个@ApiResponse

@ApiError： 用于方法，接口错误所返回的信息

## 四、注意

1. Conntroller中定义的方法必须在@RequestMapper中显示的指定RequestMethod类型，否则SawggerUi会默认为全类型皆可访问， API列表中会生成多条项目。
2. paramType会直接影响程序的运行期，如果paramType与方法参数获取使用的注解不一致，会直接影响到参数的接收。
