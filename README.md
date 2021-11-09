# Spring-framework
Overview of the Spring Framework
![]()

**核心容器**

核心容器由SpringCore、SpringBean、SpringContext、SpringContext支持和SpringExpression（SpringExpressionLanguage）模块组成。

SpringCore和SpringBeans模块提供了框架的基本部分，包括IoC和依赖注入特性。BeanFactory是factory模式的复杂实现。它消除了对编程单例的需求，并允许将依赖项的配置和规范与实际的程序逻辑解耦。

Context（spring context）模块构建在Core和bean模块提供的坚实基础上：它是一种以类似于JNDI注册表的框架风格方式访问对象的方法。Context模块继承了Beans模块的特性，并添加了对国际化（例如使用资源束）、事件传播、资源加载以及通过Servlet容器等透明创建上下文的支持。Context模块还支持JavaEE特性，如EJB、JMX和基本远程处理。ApplicationContext接口是上下文模块的焦点。spring Context支持支持将公共第三方库集成到spring应用程序context中，用于缓存（EhCache、Guava、JCache）、邮件（JavaMail）、调度（CommonJ、Quartz）和模板引擎（FreeMarker、JasperReports、Velocity）。

spring-expression模块提供了一种强大的表达式语言，用于在运行时查询和操作对象图。它是JSP2.1规范中指定的统一表达式语言（unified EL）的扩展。该语言支持设置和获取属性值、属性分配、方法调用、访问数组内容、集合和索引器、逻辑和算术运算符、命名变量以及从Spring的IoC容器中按名称检索对象。它还支持列表投影和选择以及常见的列表聚合。
