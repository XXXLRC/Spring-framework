# Spring-framework
Overview of the Spring Framework

设计理念
- 提供各个层面的选择。Spring允许您尽可能晚地推迟设计决策。例如，您可以通过配置切换持久性提供程序，而无需更改代码。许多其他基础架构问题以及与第三方API的集成也是如此。
- 适应不同的观点。Spring拥抱灵活性，并不认为应该如何做。它以不同的视角支持广泛的应用需求。
- 保持强大的向后兼容性。Spring的演变经过精心设计，可以在版本之间进行一些重大改变。Spring支持精心挑选的JDK版本和第三方库，以便于维护依赖于Spring的应用程序和库。
- 关心API设计。Spring团队投入了大量的思考和时间来制作直观的API，并且可以支持多个版本和多年。
- 为代码质量设定高标准。Spring框架强调有意义的，当前的和准确的javadoc。它是极少数项目之一，可以声称干净的代码结构，包之间没有循环依赖。

Spring框架由大约20个模块组成的特性组成。这些模块分为核心容器、数据访问/集成、Web、AOP（面向方面编程）、工具、消息传递和测试，如下图所示。

![](https://github.com/XXXLRC/Spring-framework/blob/bd08c2c4864830bb62712f901989471733434d01/images/spring-overview.png)

**核心容器**

核心容器由SpringCore、SpringBean、SpringContext、SpringContext支持和SpringExpression（SpringExpressionLanguage）模块组成。

SpringCore和SpringBeans模块提供了框架的基本部分，包括IoC和依赖注入特性。BeanFactory是factory模式的复杂实现。它消除了对编程单例的需求，并允许将依赖项的配置和规范与实际的程序逻辑解耦。

Context（spring context）模块构建在Core和bean模块提供的坚实基础上：它是一种以类似于JNDI注册表的框架风格方式访问对象的方法。Context模块继承了Beans模块的特性，并添加了对国际化（例如使用资源束）、事件传播、资源加载以及通过Servlet容器等透明创建上下文的支持。Context模块还支持JavaEE特性，如EJB、JMX和基本远程处理。ApplicationContext接口是上下文模块的焦点。spring Context支持支持将公共第三方库集成到spring应用程序context中，用于缓存（EhCache、Guava、JCache）、邮件（JavaMail）、调度（CommonJ、Quartz）和模板引擎（FreeMarker、JasperReports、Velocity）。

spring-expression模块提供了一种强大的表达式语言，用于在运行时查询和操作对象图。它是JSP2.1规范中指定的统一表达式语言（unified EL）的扩展。该语言支持设置和获取属性值、属性分配、方法调用、访问数组内容、集合和索引器、逻辑和算术运算符、命名变量以及从Spring的IoC容器中按名称检索对象。它还支持列表投影和选择以及常见的列表聚合。

Bean：在Spring中，构成应用程序主干并由SpringIOC容器管理的对象称为bean。bean是由SpringIOC容器实例化、组装和管理的对象。bean以及它们之间的依赖关系反映在容器使用的配置元数据中。

JNDI是Java Naming and Directory Interface（JAVA命名和目录接口）的英文简写，它是为JAVA应用程序提供命名和目录访问服务的API（Application Programing Interface，应用程序编程接口）。JNDI 是一个sun提出的一个规范(相似于jdbc)，详细的实现是各个j2ee容器提供商。JNDI是J2EE组件在执行时间接地查找其它组件、资源或服务的通用机制，可实现组件之间的解耦。JNDI 是通过资源的名字来查找的，资源的名字在整个j2ee应用中(j2ee容器中)是唯一的。 



## IoC容器

在Spring中，BeanFactory是IOC容器的核心接口，它的职责包括：实例化、定位、配置应用程序中的对象及建立这些对象间的依赖。是IoC容器最基本客户端视图。

一级容器
提供的方法定义有：
- getBean  根据名称或者类型获取容器中bean
- getBeanProvider 获取给定bean的提供者
- containsBean  检验容器中是否包含给定bean
- isSingleton   检验给定bean是否是Singleton类型
- isPrototype   检验给定bean是否是Prototype类型
- isTypeMatch   检验给定bean是否与指定类型匹配
- getType       获取给定bean的类型
- getAliases    获取给定bean的别名



BeanFactory的四级体系结构：
|-- BeanFactory 是Spring bean容器的根接口.提供获取bean,是否包含bean,是否单例与原型,获取bean类型,bean 别名的api.
|-- -- ListableBeanFactory 提供容器内bean实例的枚举功能.不考虑父容器内的实例.这是设计模式原则里的接口隔离原则。
|-- -- AutowireCapableBeanFactory 提供工厂的装配功能。
|-- -- HierarchicalBeanFactory 提供父容器的访问功能
|-- -- -- ConfigurableBeanFactory 如名可配置工厂,提供factory的可配置功能
|-- -- -- -- ConfigurableListableBeanFactory 集大成者，在ConfigurableBeanFactory基础上,提供解析,修改bean定义,并初始化单例的功能

二级容器

ListableBeanFactory接口定义了按条件批量获取bean的方法，扩展了BeanFactory的功能

ListableBeanFactory中定义的方法：
- containsBeanDefinition //检查容器中是否包含给定名称的bean definition
- getBeanDefinitionCount //获取容器中包含的bean definition数量
- getBeanDefinitionNames //获取容器中所有bean definition数组
- getBeanNamesForType    //根据指定类型获取所有bean名称数组，可选条件为是否是singleton，是否是可以早期初始化的
- getBeanNamesForAnnotation //根据指定注解获取所有bean名称，不创建相应的实例
- getBeansOfType         //根据指定类型获取bean实例map
- getBeansWithAnnotation //根据指定注解获取bean实例map
- findAnnotationOnBean //在指定bean上查找annotationType的注解

AutowireCapableBeanFactory接口定义了可以自动装配bean相关依赖的方法，提供bean创建(带有构造函数解析)、属性填充、连接(包括自动装配)和初始化。处理运行时bean引用、解析托管集合、调用初始化方法等。支持自动装配构造函数、按名称的属性和按类型的属性。通过实现类AbstractAutowireCapableBeanFactory 实现bean的创建.

AutowireCapableBeanFactory中定义的方法
- createBean              //(按条件)创建bean
- autowire                //装配bean，把给定bean填入构造函数参数或者属性中
- autowireBean            //(按条件)装配bean，把给定bean填入指定属性中
- autowireBeanProperties  //装配bean的属性，把给定的bean填入指定属性中
- configureBean           //配置bean，调用了initializeBean
- initializeBean          //初始化bean，一般用于autowireBeanProperties之后，初始化bean相关属性（包括加强，初始化前置处理器，实现了InitializingBean的bean处理，初始化后置处理器）
- applyBeanPropertyValues //该方法用于将指定类型bean通过setter方法装配到bean的属性中
- applyBeanPostProcessorsAfterInitialization    // bean初始化后置处理器
- applyBeanPostProcessorsBeforeInitialization   // bean初始化前置处理器
- destroyBean       //销毁bean
- resolveNamedBean  //解析命名的bean
- resolveBeanByName //根据指定名称解析bean
- resolveDependency //解析bean的依赖

HierarchicalBeanFactory接口定义了BeanFactory之间的分层结构，ConfigurableBeanFactory中的setParentBeanFactory方法能设置父级的BeanFactory

HierarchicalBeanFactory中定义的方法：
- BeanFactory getParentBeanFactory(); // 获取父级的BeanFactory
- boolean containsLocalBean(String name); // 判断本地的工厂是否包含指定的bean，忽略在祖先工厂中定义的bean。

上面三个 Factory 是 BeanFactory 接口的直系亲属，三种不同样式的BeanFactory ，分层容器，可列举(查询)容器，自动装配容器，职能单一。


三级容器
ConfigurableBeanFactory








