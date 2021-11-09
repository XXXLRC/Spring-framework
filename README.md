# Spring-framework
Overview of the Spring Framework

设计理念
- 提供各个层面的选择。Spring允许您尽可能晚地推迟设计决策。例如，您可以通过配置切换持久性提供程序，而无需更改代码。许多其他基础架构问题以及与第三方API的集成也是如此。
- 适应不同的观点。Spring拥抱灵活性，并不认为应该如何做。它以不同的视角支持广泛的应用需求。
- 保持强大的向后兼容性。Spring的演变经过精心设计，可以在版本之间进行一些重大改变。Spring支持精心挑选的JDK版本和第三方库，以便于维护依赖于Spring的应用程序和库。
- 关心API设计。Spring团队投入了大量的思考和时间来制作直观的API，并且可以支持多个版本和多年。
- 为代码质量设定高标准。Spring框架强调有意义的，当前的和准确的javadoc。它是极少数项目之一，可以声称干净的代码结构，包之间没有循环依赖。

Spring框架由大约20个模块组成的特性组成。这些模块分为核心容器、数据访问/集成、Web、AOP（面向方面编程）、工具、消息传递和测试，如下图所示。
![]()

**核心容器**

核心容器由SpringCore、SpringBean、SpringContext、SpringContext支持和SpringExpression（SpringExpressionLanguage）模块组成。

SpringCore和SpringBeans模块提供了框架的基本部分，包括IoC和依赖注入特性。BeanFactory是factory模式的复杂实现。它消除了对编程单例的需求，并允许将依赖项的配置和规范与实际的程序逻辑解耦。

Context（spring context）模块构建在Core和bean模块提供的坚实基础上：它是一种以类似于JNDI注册表的框架风格方式访问对象的方法。Context模块继承了Beans模块的特性，并添加了对国际化（例如使用资源束）、事件传播、资源加载以及通过Servlet容器等透明创建上下文的支持。Context模块还支持JavaEE特性，如EJB、JMX和基本远程处理。ApplicationContext接口是上下文模块的焦点。spring Context支持支持将公共第三方库集成到spring应用程序context中，用于缓存（EhCache、Guava、JCache）、邮件（JavaMail）、调度（CommonJ、Quartz）和模板引擎（FreeMarker、JasperReports、Velocity）。

spring-expression模块提供了一种强大的表达式语言，用于在运行时查询和操作对象图。它是JSP2.1规范中指定的统一表达式语言（unified EL）的扩展。该语言支持设置和获取属性值、属性分配、方法调用、访问数组内容、集合和索引器、逻辑和算术运算符、命名变量以及从Spring的IoC容器中按名称检索对象。它还支持列表投影和选择以及常见的列表聚合。

Bean在Spring中就是一个个业务组件，我们通过使用各种Bean来完成最终的业务逻辑功能。Bean的创建和装配交个Spring容器来完成，这叫做控制翻转。

JNDI是Java Naming and Directory Interface（JAVA命名和目录接口）的英文简写，它是为JAVA应用程序提供命名和目录访问服务的API（Application Programing Interface，应用程序编程接口）。JNDI 是一个sun提出的一个规范(相似于jdbc)，详细的实现是各个j2ee容器提供商。JNDI是J2EE组件在执行时间接地查找其它组件、资源或服务的通用机制，可实现组件之间的解耦。JNDI 是通过资源的名字来查找的，资源的名字在整个j2ee应用中(j2ee容器中)是唯一的。 
