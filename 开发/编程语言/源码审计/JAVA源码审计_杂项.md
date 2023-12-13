## WEB-INF

- WEB-INF是用来存储服务端配置文件信息和在服务端运行的类文件的，它下面的东西不允许客户端直接访问的。
- 一般会有web.xml文件(WEB项目配置文件)
- 通过文件读取该文件我们可以获取到这个项目的架构和配置信息(编码、过滤器、监听器…)

## SpringMVC工作流程

1. 用户发起请求->SPring MVC 前端控制器(DispathcerServlet)->处理器映射器(HandlerMapping)进行处理->根据URL选择对应的Controller
2. 控制器(Controller)执行相应处理逻辑,执行完毕,Return 返回值。
3. ViewResolver解析控制器返回值->前端控制器(DispathcerSevlet)去解析->View对象
4. 前端控制器(DispathcerSevlet)对View进行渲染,返回至客户端浏览器,完成请求交互

## 常见JAVA WEB 项目分层
- 视图层（View 视图)
- 控制层（Controller、Action 控制层）
- 服务层（Service）
- 业务逻辑层BO(business object)  
- 实体层（entity 实体对象、VO(value object) 值对象 、模型层（bean）。
- 持久层（dao- Data Access Object 数据访问层、PO(persistant object) 持久对象）

## JSP 与 Servlet
JSP、JSPX文件是可以直接被Java容器直接解析的动态脚本，jsp和其他脚本语言无异，不但可以用于页面数据展示，也可以用来处理后端业务逻辑。

从本质上说JSP就是一个Servlet，因为jsp文件最终会被编译成class文件，而这个Class文件实际上就是一个特殊的Servlet。

JSP文件会被编译成一个java类文件，如index.jsp在Tomcat中Jasper编译后会生成index_jsp.java和index_jsp.class两个文件。而index_jsp.java 继承于HttpJspBase类，HttpJspBase是一个实现了HttpJspPage接口并继承了HttpServlet的标准的Servlet，__jspService方法其实是HttpJspPage接口方法，类似于Servlet中的service方法，这里的__jspService方法其实就是HttpJspBase的service方法调用。

## Filter
Filter是JavaWeb中的过滤器,用于过滤URL请求。通过Filter我们可以实现URL请求资源权限验证、用户登陆检测等功能。Filter是一个接口，实现一个Filter只需要重写init、doFilter、destroy方法即可，其中过滤逻辑都在doFilter方法中实现。

Filter和Servlet一样是Java Web中最为核心的部分，使用Servlet和Filter可以实现后端接口开发和权限控制，当然使用Filter机制也可以实现MVC框架，Struts2实现机制就是使用的Filter。

Filter的配置类似于Servlet，由`<filter>`和`<filter-mapping>`两组标签组成，如果Servlet版本大于3.0同样可以使用注解的方式配置Filter。

## Filter 与 Servlet
- Filter和Servlet都需要在web.xml或注解(@WebFilter、@WebServlet)中配置，而且配置方式是非常的相似的。

- Filter和Servlet都可以处理来自Http请求的请求，两者都有request、response对象。

- Filter和Servlet基础概念不一样，Servlet定义是容器端小程序，用于直接处理后端业务逻辑，而Filter的思想则是实现对Java Web请求资源的拦截过滤。

- Filter和Servlet虽然概念上不太一样，但都可以处理Http请求，都可以用来实现MVC控制器(Struts2和Spring框架分别基于Filter和Servlet技术实现的)。

- 一般来说Filter通常配置在MVC、Servlet和JSP请求前面，常用于后端权限控制、统一的Http请求参数过滤(统一的XSS、SQL注入、Struts2命令执行等攻击检测处理)处理，其核心主要体现在请求过滤上，而Servlet更多的是用来处理后端业务请求上。

## MVC
传统的开发存在结构混乱易用性差耦合度高可维护性差等多种问题，为了解决这些毛病分层思想和MVC框架就出现了。MVC即模型(Model)、视图(View)、控制器(Controller)， MVC模式的目的就是实现Web系统的职能分工。

### Spring MVC 控制器
#### 注解配置
在Spring进入了3.0时代,使用Java注解的方式也逐渐的流行了起来，曾经写一个Spring的控制器我们通常要在xml中声明Spring bean并配置处理的URL，而在新时代的Spring项目中我们通常用Spring MVC注解就可以轻松完成Spring MVC的配置了。

Spring Controller注解:

- @Controller
- @RestController
- @RepositoryRestController

Spring MVC请求配置注解:

- @RequestMapping
- @GetMapping
- @PostMapping
- @PutMapping
- @DeleteMapping
- @PatchMapping

>Spring MVC除了上述6种Http请求处理注解以外还有Spring Data JPA Rest提供的特殊的@RepositoryRestResource注解，@RepositoryRestResource是基于Spring Data JPA REST库实现的，Spring Data JPA REST提供的API可支持通过JPA查询数据并处理Http请求服务。

#### XML配置
对于一些老旧的项目可能还保留了一些基于xml配置的方式Spring MVC项目，这里只简单的介绍下如何配置不做过多的描述。基于配置方式的控制器一般是在Controller类中实现了Spring的org.springframework.web.servlet.mvc.Controller接口的handleRequest方法(当然还有其他途径，如:AbstractCommandController和SimpleFormController但都已经过时了)。

```java
package org.javaweb.codereview.controller;

import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * @author yz
 */
public class TestController implements Controller {

	@Override
	public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
		ModelAndView mv = new ModelAndView();
		mv.setViewName("index");

		return mv;
	}

}
```

```xml
<bean name="/test.do" class="org.javaweb.codereview.controller.TestController"/>
```

### Strus2控制器
Struts2主要的开发模式是基于xml配置，在struts.xml中配置Action地址和对应的处理类。

