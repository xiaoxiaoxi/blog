# Spring完整揭秘（一）：IoC

## Spring的起源

在早期的J2EE平台开发实践过程中，过分强调分布式环境的使用，比如EJB，开发和部署复杂、测试困难，且代价昂贵，在这种历史背景情况下，倡导轻量级应用解决方案的Spring应运而生。

## Spring框架

Spring倡导一切从实际出发，以敏捷、实用的态度来选择适合当前开发场景的解决方案。Spring框架的本质就是提供各种服务组件，以帮助我们简化基于POJO的Java企业级应用程序开发。

- Spring框架总体结构
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200729085429934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)
  组成整个Spring框架的各种服务实现被划分到了多个相互独立却又相互依赖的模块当中，它们组成了Spring框架的核心骨架。

### Spring的IOC容器

- 整个Spring框架构建在Core核心模块之上，它是整个框架的基础。在该模块中，Spring为我们提供了一个IoC容器（IoC Container）实现，用于帮助我们以依赖注入的方式管理对象之间的依赖关系。

### IoC的基本概念

> IoC的全称为Inversion of Control，中文通常翻译为“控制反转”。用大白话来讲的意思就是“你不用找我们，我们会找你的”。

- 我们进食午餐时需要依赖于食物（Food），传统方式的做法就是主动new一个Food对象，然后完成进餐过程。

```java
/**
 * IOC的理解--传统方式
 *
 * @author zhuhuix
 * @date 2020-07-29
 */
public class Person {
    // 食物
    private Food food;
    // 进食午餐
    public void haveLunch(){
        // 主动创建食物对象
        this.food= new Food("面食","馄饨面",1);
        // 进餐过程
        // ...
        System.out.println("进食午餐："+this.food.toString());
    }
	// 食物类
    class Food {
        // 类型
        private String foodType;
        // 名称
        private String foodName;
        // 数量
        private int foodNum;

        public Food(){}

        public Food(String foodType, String foodName, int foodNum) {
            this.foodType = foodType;
            this.foodName = foodName;
            this.foodNum = foodNum;
        }

        public String getFoodType() {
            return foodType;
        }

        public void setFoodType(String foodType) {
            this.foodType = foodType;
        }

        public String getFoodName() {
            return foodName;
        }

        public void setFoodName(String foodName) {
            this.foodName = foodName;
        }

        public int getFoodNum() {
            return foodNum;
        }

        public void setFoodNum(int foodNum) {
            this.foodNum = foodNum;
        }

        @Override
        public String toString() {
            return "Food{" +
                    "foodType='" + foodType + '\'' +
                    ", foodName='" + foodName + '\'' +
                    ", foodNum=" + foodNum +
                    '}';
        }
    }
}

```

- IoC的场景
  - 二者之间通过IoC ServiceProvider来打交道，所有的被注入对象和依赖对象现在由IoC Service Provider统一管理。被注入对象需要什么，通行IoC Service Provider，就会把相应的被依赖对象注入到被注入对象中，从而达到IoC Service Provider为被注入对象服务的目的。
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200729101133161.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

### IoC的注入方式

1. 构造方法注入

> 这种注入方式的优点就是，对象在构造完成之后，即已进入就绪状态，可以马上使用。缺点就是，当依赖对象比较多的时候，构造方法的参数列表会比较长。

```java
/**
 * IOC的注入方式--构造方法注入
 *
 * @author zhuhuix
 * @date 2020-07-29
 */
public class PersonIoC1 {
    private Food food;

    // 构造方法注入
    public PersonIoC1(Food food) {
        this.food = food;
    }

    // 进食午餐
    public void haveLunch(){
        // 进餐过程
        // ...
        System.out.println("进食午餐："+this.food.toString());
    }
}


```

1. setter 方法注入

> setter方法注入在描述性上要比构造方法注入好一些。另外，setter方法可以被继承，允许设置默认值，而且有良好的IDE支持。缺点当然就是对象无法在构造完成后马上进入就绪状态。

```java
/**
 * IOC的注入方式--setter方法注入
 *
 * @author zhuhuix
 * @date 2020-07-29
 */
public class PersonIoC2 {
    private Food food;
    
    public PersonIoC2() { }

    // setter方法注入
    public void setFood(Food food) {
        this.food = food;
    }

    // 进食午餐
    public void haveLunch(){
        // 进餐过程
        // ...
        System.out.println("进食午餐："+this.food.toString());
    }
}
```

1. 接口注入

> 需要被依赖的对象实现不必要的接口，带有侵入性。一般都不推荐这种方式

```java
/**
 * IOC的注入方式--接口注入
 *
 * @author zhuhuix
 * @date 2020-07-29
 */
public class PersonIoC3 implements injectFood{
    private Food food;

    public PersonIoC3() { }
    
    // 实现接口进行注入
    @Override
    public void injectFood(Food food) {
        this.food = food;
    }

    // 进食午餐
    public void haveLunch(){
        // 进餐过程
        // ...
        System.out.println("进食午餐："+this.food.toString());
    }


}

//注入接口
interface injectFood{
     void injectFood(Food food);
}

```

## 我对IOC的理解

- 我们要完成某个业务逻辑时需要用到其他的对象来协作完成，在没有使用Spring的时候，均要使用像new object() 这样的语法来将合作对象创建出来，这个合作对象是由自己主动创建出来的，**在本例中，由Person对象主动创建了Food对象。** 这样两个对象就紧密地耦合在了一起。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200729105433352.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)
- 而使用了Spring之后，创建协作对象的工作是由Spring来完成，Spring创建好对象，存储到一个容器里面，当需要使用协作对象时，可以从Spring存放对象的容器里面取出并直接使用，至于Spring是如何创建那个对象，以及什么时候创建好对象的，完全不需要关心这些细节问题。**在本例中，Person对象向Spring容器请求Food对象。** 这样两个对象通过Spirng Ioc容器完成了解耦。
- 从图上也可以看出来，IoC实际描述的是创建对象的控制权进行了转移，以前创建对象的主动权和创建时机是由自己把控的，而现在这种权力转移到第三方。
- 用一句话来总结：IoC是一种可以帮助我们解耦各业务对象间依赖关系的对象绑定方式



# Spring完整揭秘（二）：Spring的IoC容器之BeanFactory

## 背景

- 在[《Spring完整揭秘（一）：IoC》](https://blog.csdn.net/jpgzhu/article/details/107653513)文章中描述了IoC Service Provider 的基本职责:

1. 对象的构建管理;
2. 对象间的依赖绑定;
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200730152900608.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

本文将针对Spring的 IoC容器中的IoC Service Provider功能进行深入剖析。

## Spring 的 IoC容器

> Spring的IoC容器除了基本的IoC支持，还提供了相应的AOP框架支持、企业级服务集成等功能。
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200730153919222.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

## Spring的IoC容器之BeanFactory

- BeanFactory是基础类型IoC容器，Spring BeanFactory相关UML结构图如下：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200730160244555.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)
- BeanFactory 的定义
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200730160501876.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

##### 用 BeanFactory 的XML配置方式实现业务对象间的依赖管理

### 格式

- XML格式的容器信息管理方式是Spring提供的最为强大、支持最为全面的方式。

```
<!-- 基于XSD的Spring配置文件文档声明 -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	<bean id="" class="">
	...
	</bean>
</beans>
```

#### beans

- “beans” 是XML配置文件中最顶层的元素 包括如下属性：

> - default-lazy-init 。其值可以指定为 true 或者 false ，默认值为 false 。用来标志是否对所有的 bean 进行延迟初始化。
> - default-autowire 。可以取值为 no 、 byName 、 byType 、 constructor 以及autodetect 。默认值为 no ，如果使用自动绑定的话，用来标志全体bean使用哪一种默认绑定方式。
> - default-dependency-check 。可以取值 none 、 objects 、 simple 以及 all ，默认值为 none ，即不做依赖检查。
> - default-init-method 。如果所管辖的 bean 按照某种规则，都有同样名称的初始化方法的话，可以在这里统一指定这个初始化方法名，而不用在每一个 bean 上都重复单独指定。
> - default-destroy-method 。与 default-init-method 相对应，如果所管辖的bean有按照某种规则使用了相同名称的对象销毁方法，可以通过这个属性统一指定。

#### bean

- Bean是指每个业务对象个体

	<!--食物对象-->
	<bean id="food1" class="Food">
	    <property name="foodType" value="面食"></property>
	    <property name="foodName" value="馄饨面"></property>
	    <property name="foodNum" value="1"></property>
	</bean>
	
	<bean id="food2" class="Food">
	    <property name="foodType" value="面食"></property>
	    <property name="foodName" value="重庆小面"></property>
	    <property name="foodNum" value="1"></property>
	</bean>
	<!--人物对象-->
	<bean id="person1" class="Person" scope="prototype">
	    <constructor-arg name="name" value="张三"></constructor-arg>
	    <constructor-arg name="food" ref="food1"></constructor-arg>
	</bean>
	
	<bean id="person2" class="Person" scope="prototype">
	    <constructor-arg name="name" value="李四"></constructor-arg>
	    <constructor-arg name="food" ref="food2"></constructor-arg>
	</bean>

> - id 属性：指定 bean 在容器中的标志
> - class 属性： 每个注册到容器的对象都需要通过 bean>元素的 class 属性指定其类型
> - constructor-arg：通过构造方法注入方式，为当前业务对象注入其所依赖的对象
> - name 构造方法传入的参数名称
> - value 构造方法传入的参数值
> - ref：引用的Bean实例

- 使用 list 进行依赖注入的对象定义以及相关配置内容



    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
           <description>SpringIoc</description>
    
            <bean id="food1" class="Food">
                <property name="foodType" value="面食"/>
                <property name="foodName" value="馄饨面"/>
                <property name="foodNum" value="1"/>
            </bean>
    
            <bean id="food2" class="Food">
                <property name="foodType" value="面食"/>
                <property name="foodName" value="重庆小面"/>
                <property name="foodNum" value="1"/>
            </bean>
            <!-- 通过setter注入list 对象-->
            <bean id="person1" class="Person" scope="prototype">
                <property name="name" value="张三"/>
                <property name="foods" >
                <list>
                    <ref bean="food1"/>
                    <ref bean="food2"/>
                </list>
                </property>
            </bean>
    </beans>
#### bean 的 scope

- scope用来声明容器中的对象所应该处的限定场景或者说该对象的存活时间，目前存在singleton和prototype，request、session和global session类型
  - singleton ：在Spring的IoC容器中只存在一个对象实例
  - prototype：容器在接到该类型对象的请求的时候，会每次都重新生成一个新的对象实例给请求方
  - request：XmlWebApplicationContext 会为每个HTTP请求创建一个全新的 Request-Processor 对象供当前请求使用，当请求结束后，该对象实例的生命周期即告结束
  - session：Spring容器会为每个独立的session创建属于它们自己的全新的对象实例

## BeanFactory的完整例子

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020073016531190.png)

- Food.Class





```
/**
    食物类
    @author zhuhuix
    @date 2020-0730
*/
public class Food {
    // 类型
    private String foodType;
    // 名称
    private String foodName;
    // 数量
    private int foodNum;

    public Food(){}

    public Food(String foodType, String foodName, int foodNum) {
        this.foodType = foodType;
        this.foodName = foodName;
        this.foodNum = foodNum;
    }

    public String getFoodType() {
        return foodType;
    }

    public void setFoodType(String foodType) {
        this.foodType = foodType;
    }

    public String getFoodName() {
        return foodName;
    }

    public void setFoodName(String foodName) {
        this.foodName = foodName;
    }

    public int getFoodNum() {
        return foodNum;
    }

    public void setFoodNum(int foodNum) {
        this.foodNum = foodNum;
    }

    @Override
    public String toString() {
        return "Food{" +
                "foodType='" + foodType + '\'' +
                ", foodName='" + foodName + '\'' +
                ", foodNum=" + foodNum +
                '}';
    }
}
```

- Person.Class

```
/**
 * 人物类
 *
 * @author zhuhuix
 * @date 2020-0730
 * /
 */
public class Person {
    // 姓名
    private String name;
    // 食物
    private Food food;

    public Person(String name, Food food) {
        this.name = name;
        this.food = food;
    }

    public void havaLunch() {
        System.out.println(getName() + "进食午餐：" + this.food.toString());
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Food getFood() {
        return food;
    }

    public void setFood(Food food) {
        this.food = food;
    }

}

```

- bean.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="food1" class="Food">
        <property name="foodType" value="面食"></property>
        <property name="foodName" value="馄饨面"></property>
        <property name="foodNum" value="1"></property>
    </bean>

    <bean id="food2" class="Food">
        <property name="foodType" value="面食"></property>
        <property name="foodName" value="重庆小面"></property>
        <property name="foodNum" value="1"></property>
    </bean>

    <bean id="person1" class="Person" scope="prototype">
        <constructor-arg name="name" value="张三"></constructor-arg>
        <constructor-arg name="food" ref="food1"></constructor-arg>
    </bean>

    <bean id="person2" class="Person" scope="prototype">
        <constructor-arg name="name" value="李四"></constructor-arg>
        <constructor-arg name="food" ref="food2"></constructor-arg>
    </bean>

</beans>

```

- Application.java

```
/**
 * beanFactory加载
 *
 * @author zhuhuix
 * @date 2020-07-30
 */
public class Application {
    public static void main(String[] args) {

        DefaultListableBeanFactory beanRegistry = new DefaultListableBeanFactory();
        // XmlBeanDefinitionReader 负责读取Spring指定格式的XML配置文件并解析\
        XmlBeanDefinitionReader xmlBeanDefinitionReader = new XmlBeanDefinitionReader(beanRegistry);
        xmlBeanDefinitionReader.loadBeanDefinitions(new ClassPathResource("bean.xml"));
        BeanFactory beanFactory = beanRegistry;
        
        Food food1 = (Food) beanFactory.getBean("food1");
        System.out.println(food1.toString());

        Food food2 = (Food) beanFactory.getBean("food2");
        System.out.println(food2.toString());

        Person person1 = (Person) beanFactory.getBean("person1");
        person1.havaLunch();

        Person person2 = (Person) beanFactory.getBean("person2");
        person2.havaLunch();
    }
}

```

- 运行结果
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200730165419342.png)

## Bean的加载过程

可见本文[《Spring源码解析：加载Bean过程》](https://blog.csdn.net/jpgzhu/article/details/107411711)



# Spring完整揭秘（三）：Spring的IoC容器之ApplicationContext

## ApplicationContext与BeanFactory的区别

- Spring提供了基本的IoC容器： [BeanFactory](https://blog.csdn.net/jpgzhu/article/details/107680906)， 在此基础上又提供了更为先进的IoC容器：ApplicationContext，该容器除了拥有BeanFactory所支持的所有功能之外，还进一步扩展了基本容器的功能：

  - 包括 BeanFactoryPostProcessor 、 BeanPostProcessor 以及其他特殊类型bean的自动识别、容器启动后bean实例的自动初始化、国际化的信息支持、容器内事件发布等

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803093559153.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

## Spring统一资源加载策略

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803094110343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

- Spring框架内部使用 **org.springframework.core.io.Resource** 接口作为所有资源的抽象和访问接口：详见[《Spring源码解析（一）：认识统一资源Resource》](https://blog.csdn.net/jpgzhu/article/details/107386421)。
- 在此基础上，Spring框架通过 **org.springframework.core.io.ResourceLoader**接口作为资源查找定位策略的统一抽象：

```
public interface ResourceLoader {
	/** Pseudo URL prefix for loading from the class path: "classpath:". */
	String CLASSPATH_URL_PREFIX = ResourceUtils.CLASSPATH_URL_PREFIX;
	Resource getResource(String location);	
	@Nullable
	ClassLoader getClassLoader();
}

```

## ApplicationContext 与 统一资源Resource的关系

- 从下图可以看出：ApplicationContext 继承了 ResourcePatternResolver ，间接实现了 ResourceLoader 接口， 即ApplicationContext 支持Spring统一资源加载策略。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803100328776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

关系验证代码：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803105528851.png)



```
/**
 * ApplicationContext与Resource的关系
 *
 * @author zhuhuix
 */
public class ApplicationContext {
    public static void main(String[] args) throws IOException {

        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("bean.xml");
        // 通过applicationContext获取资源文件，并测试资源文件是否存在
        Resource resource1 = applicationContext.getResource("bean.xml");
        System.out.println("资源bean.xml是否存在：" + resource1.exists());
        // 通过applicationContext获取资源文件，并测试资源文件是否存在
        Resource resource2 = applicationContext.getResource("bean2.xml");
        System.out.println("资源bean2.xml是否存在：" + resource2.exists());

    }
}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803105243517.png)

## ApplicationContext多配置模块加载的简化

相对于 BeanFactory ，ApplicationContext 可以使用通配符进行模块加载：

- 配置文件
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803110647365.png)

```
<!-- bean.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"
    default-lazy-init="true">

    <description>SpringIoc</description>

    <bean id="food1" class="Food">
        <property name="foodType" value="面食"/>
        <property name="foodName" value="馄饨面"/>
        <property name="foodNum" value="1"/>
    </bean>

    <bean id="food2" class="Food">
        <property name="foodType" value="面食"/>
        <property name="foodName" value="重庆小面"/>
        <property name="foodNum" value="1"/>
    </bean>

    <bean id="person1" class="Person" scope="prototype" depends-on="food1,food2" >
        <property name="name" value="张三"/>
        <property name="foods" >
        <list>
            <ref bean="food1"/>
            <ref bean="food2"/>
        </list>
        </property>
    </bean>
</beans>

<!-- bean2.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"
    default-lazy-init="true">

    <description>SpringIoc</description>

    <bean id="food3" class="Food">
        <property name="foodType" value="炒菜"/>
        <property name="foodName" value="鱼香肉丝"/>
        <property name="foodNum" value="1"/>
    </bean>

    <bean id="food4" class="Food">
        <property name="foodType" value="炒菜"/>
        <property name="foodName" value="宫宝鸡丁"/>
        <property name="foodNum" value="1"/>
    </bean>

    <bean id="person2" class="Person" scope="prototype" depends-on="food3,food4" >
        <property name="name" value="李四"/>
        <property name="foods" >
        <list>
            <ref bean="food3"/>
            <ref bean="food4"/>
        </list>
        </property>
    </bean>
</beans>

```

- 测试代码：

```
/**
 * ApplicationContext Demo
 *
 * @author zhuhuix
 */
public class ApplicationContext {
    public static void main(String[] args) throws IOException {

        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("*.xml");
        // 通过applicationContext获取资源文件，并测试资源文件是否存在
        Resource resource1 = applicationContext.getResource("bean.xml");
        System.out.println("资源bean.xml是否存在：" + resource1.exists());

        Person person1 = (Person)applicationContext.getBean("person1");
        person1.haveLunch();

        // 通过applicationContext获取资源文件，并测试资源文件是否存在
        Resource resource2 = applicationContext.getResource("bean2.xml");
        System.out.println("资源bean2.xml是否存在：" + resource2.exists());

        Person person2 = (Person)applicationContext.getBean("person2");
        person2.haveLunch();

    }
}


```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803110903920.png)



## ApplicationContext与MessageSource

- ApplicationContext 除了实现了 ResourceLoader 以支持统一的资源加载，它还实现了 MessageSource 接口，通过该接口，我们统一了国际化信息的访问方式。传入相应的 Locale 、资源的键以及相应参数，就可以取得相应的信息。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803114805689.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)



```
public interface MessageSource {
String getMessage(String code, Object[] args, String defaultMessage, Locale locale);
String getMessage(String code, Object[] args, Locale locale) throws NoSuchMessageException;
String getMessage(MessageSourceResolvable resolvable, Locale locale) throws NoSuchMessageException;
}

```

- ApplicationContext 容器内使用messageSource， 具备国际化功能的实际

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803115134847.png)

- 定义一个id为MessageSource的 Bean配置文件

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="messageSource" class="org.springframework.context.support.ResourceBundleMessageSource">
        <property name="basenames">
            <list>
                <value>message</value>
            </list>
        </property>
    </bean>
</beans>

```

- 增加两份资源文件：

  - 第一份为英语的资源文件，文件名 message_en_US.properties

  > Welcome=Welcome to spring

  - 第二份为简体中文的资源文件，文件名 message_zh_CN.properties

  > Welcome=\u6b22\u8fce\u4f7f\u7528spring

  - 测试主程序

```
/**
 * ApplicationContext国际化
 *
 * @author zhuhuix
 */
public class Message {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("message.xml");
        Object[] objs = new Object[]{};
        // 英文输出
        String string1 = applicationContext.getMessage("Welcome", objs, Locale.US);
        System.out.println(string1);
        // 中文输出
        String string2 = applicationContext.getMessage("Welcome", objs, Locale.CHINESE);
        System.out.println(string2);
    }
}


```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080311571912.png)





# Spring完整揭秘（四）：Spring的IoC容器之基于注解的自动装配

## 背景

- 在[《Spring的IoC容器之BeanFactory》](https://blog.csdn.net/jpgzhu/article/details/107680906)与[Spring的IoC容器之ApplicationContext](https://blog.csdn.net/jpgzhu/article/details/107756558)两篇文章中，我们在xml文件中配置bean标签，实现了依赖注入，本文将介绍基于注解的方式实现自动装配。

### classpath-scanning

- 在前面的示例中我们需要将相应对象的bean定义，一个个地添加到IoC容器的配置文件中，如果bean的数量越来越多，配置文件会变得非常庞大（虽然我们可以将一个文件分解成多个文件）且容易出错，为了解决这个问题，Spring引入了classpath-scanning的功能：

> 使用相应的注解对组成应用程序的相关类进行标注之后，classpath-scanning功能可以从某一顶层包（base package）开始扫描。当扫描到某个类标注了相应的注解之后，就会提取该类的相关信息，构建对应的 BeanDefinition ，然后把构建完的 BeanDefinition注册到容器中。

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <description>SpringIoc</description>

    <context:component-scan base-package="com"/>
    
</beans>

```

- context:component-scan 将遍历扫描 com包下的所有类型定义，寻找标注了相应注解的类，并添加到IoC容器。

### 注解

- Spring可以在类路径下寻找以下注解的组件：
  1. @Service：用于标注业务层组件
  2. @Controller ：标注控制层组件
  3. @Repository 标注数据访问组件
  4. @Components 泛指组件，当组件不好归类的时候，可以用这个注解

```
/**
 * 使用 @Component 标注的Food类
 *
 * @author zhuhuix
 * @date 2020-07-30
 */
@Component
public class Food {
    // 类型
    private String foodType;
    // 名称
    private String foodName;
    // 数量
    private int foodNum;

    public Food(){
        System.out.println("Food对象创建");
    }

    public Food(String foodType, String foodName, int foodNum) {
        this.foodType = foodType;
        this.foodName = foodName;
        this.foodNum = foodNum;
    }

    public String getFoodType() {
        return foodType;
    }

    public void setFoodType(String foodType) {
        this.foodType = foodType;
    }

    public String getFoodName() {
        return foodName;
    }

    public void setFoodName(String foodName) {
        this.foodName = foodName;
    }

    public int getFoodNum() {
        return foodNum;
    }

    public void setFoodNum(int foodNum) {
        this.foodNum = foodNum;
    }

    @Override
    public String toString() {
        return "com.Food{" +
                "foodType='" + foodType + '\'' +
                ", foodName='" + foodName + '\'' +
                ", foodNum=" + foodNum +
                '}';
    }
}

```

### @Autowired

- @Autowired 是基于注解的依赖注入的核心注解，它的存在可以让容器知道需要为当前类注入哪些依赖。

```
/**
 * 使用@Autowired实现依赖注入
 * 
 * @author zhuhuix
 * @date 2020-08-04
 */
@Component
public class Student {
    private String name;
    @Autowired
    private Food food;

    public Student() {
        System.out.println("Student对象创建");
    }

    public void haveLunch(){
        System.out.println(this.name+"进食午餐："+this.food.toString());
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Food getFood() {
        return food;
    }

    public void setFood(Food food) {
        this.food = food;
    }
}

```

- 自动配置一般而言说的是spring的@Autowired，是spring的特性之一，我们可以看一下此注解的源码：

```
 * @author Juergen Hoeller
 * @author Mark Fisher
 * @author Sam Brannen
 * @since 2.5
 * @see AutowiredAnnotationBeanPostProcessor
 * @see Qualifier
 * @see Value
 */
@Target({ElementType.CONSTRUCTOR, ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {

	/**
	 * Declares whether the annotated dependency is required.
	 * <p>Defaults to {@code true}.
	 */
	boolean required() default true;

}

```

- 在该源码中，提到了需参考AutowiredAnnotationBeanPostProcessor类：

```
public class AutowiredAnnotationBeanPostProcessor implements SmartInstantiationAwareBeanPostProcessor,
		MergedBeanDefinitionPostProcessor, PriorityOrdered, BeanFactoryAware {
// 构造函数
public AutowiredAnnotationBeanPostProcessor() {
		// 支持@Autowired注解
		this.autowiredAnnotationTypes.add(Autowired.class);
		// 支持@Value注解
		this.autowiredAnnotationTypes.add(Value.class);
		try {
			this.autowiredAnnotationTypes.add((Class<? extends Annotation>)
					ClassUtils.forName("javax.inject.Inject", AutowiredAnnotationBeanPostProcessor.class.getClassLoader()));
			logger.trace("JSR-330 'javax.inject.Inject' annotation found and supported for autowiring");
		}
		catch (ClassNotFoundException ex) {
			// JSR-330 API not available - simply skip.
		}
	}
	...
}	

```

- 感兴趣地可以跟踪AutowiredAnnotationBeanPostProcessor类中postProcessMergedBeanDefinition这个过程：

```
@Override
	public void postProcessMergedBeanDefinition(RootBeanDefinition beanDefinition, Class<?> beanType, String beanName) {
		InjectionMetadata metadata = findAutowiringMetadata(beanName, beanType, null);
		metadata.checkConfigMembers(beanDefinition);
	}
	...
```

总体来说，Spring容器启动过程中遇到@Autowired注解，会使用后置处理器机制，来创建属性的对象实例，然后再利用反射机制，将实例化好的属性，赋值到对象上。

### 使用 @PostConstruct

@PostConstruct 不是服务于依赖注入的，它们主要用于标注对象生命周期管理相关方法，这与Spring的 InitializingBean 和 DisposableBean 接口，以及配置项中的init-method 和 destroy-method 起到类似的作用：

```
/**
 * 使用@Autowired实现依赖注入
 *
 * @author zhuhuix
 * @date 2020-08-04
 */
@Component
public class Student {
    private String name;
    @Autowired
    private Food food;

    public Student() {
        System.out.println("Student对象创建");
    }

    @PostConstruct
    public void setFood() {
        this.food.setFoodType("面食");
        this.food.setFoodName("阳春面");
        this.food.setFoodNum(1);
    }

    public void haveLunch(){
        System.out.println(this.name+"进食午餐："+this.food.toString());
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Food getFood() {
        return food;
    }


}


```

### 完整测试

```
/**
 * 自动装配测试
 *
 * @author zhuhuix
 * @date 2020-08-04
 */
public class ApplicationAutowired {
    
    public static void main(String[] args) {
        // 自动扫描包
        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("bean-autowired.xml");

        // 加载食物对象
        Food food = (Food) applicationContext.getBean("food");
        food.setFoodType("面食");
        food.setFoodName("阳春面");
        food.setFoodNum(1);

        // 加载学生对象
        Student student = (Student)applicationContext.getBean("student");
        student.setName("Jack");
        student.haveLunch();

    }
}


```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200804115235656.png)



# Spring完整揭秘（五）：Spring的AOP框架

## [AOP](https://so.csdn.net/so/search?q=AOP&spm=1001.2101.3001.7020)的概念

- AOP全称Aspect -Oriented Proramming，中文称为面向切面编程：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200805093700679.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

## AOP 中的基础要素：

- **Join point（连接点）**：程序能被拦截的某些目标，比如某个执行方法。
- **Advice（通知）**：是指在特定的连接点（Join point）要做的动作。通知分为方法执行前通知（Before Advice），方法执行后通知（After Advice），环绕通知（Around Advice）等。
- **Pointcut（切点）**: 用来切入Join point（连接点）的特定表述语言，比如拦截某个类的某些执行方法
- **Aspect（切面）**: 各种Advice（通知）与Pointcut（切点）相互组成的实体
- **Weaving（织入）**: 将Advice（通知）嵌入OOP程序中的过程

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200805103759678.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)



## Java平台AOP的实现

- AOP是一种编程理念，需要具体的实现机制，Java平台上的实现主要分为以下几类：
  1. 动态代理： 功能模块类需实现接口（Spring AOP默认采用这种机制）。
  2. 动态字节码增强：在运行期间，通过生成子类将切面逻辑动态加入到这些子类中。
  3. Java代码生成：比较古老的方式，基本已经淘汰。
  4. 自定义类加载器：在加载class文件期间，将切面逻辑添加到功能模块的类中。
  5. AOL扩展：用扩展语言实现AOP。

## Spring的AOP框架

- Spring的AOP采用JDK动态代理机制和CJLIB字节码生成技术实现 ：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200805113111825.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

### @ AspectJ形式的Spring AOP

AspectJ的acj编译器把aspect类编译成class字节码后，在java目标类再进行编译时织入，最终形成完整的Java类字节码文件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200805125557860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200805125844839.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)



### Spring AOP 应用案例

- 日志处理案例

```
/**
* 日志AOP
*/
@Aspect
public class LogAspect {
	// 日志服务类
    private final LogService logService;

    ThreadLocal<Long> currentTime = new ThreadLocal<>();
	// 构造方法注入
    public LogAspect(LogService logService) {
        this.logService = logService;
    }

    /**
     * 配置切入点
     */
    @Pointcut("@annotation(demo.aspectJ.annotation.Log)")
    public void logPointcut() {
        // 该方法无方法体,主要为了让同类中其他方法使用此切入点
    }

    /**
     * 配置环绕通知,使用在方法logPointcut()上注册的切入点
     *
     * @param joinPoint join point for advice
     */
    @Around("logPointcut()")
    public Object logAround(ProceedingJoinPoint joinPoint) throws Throwable {
        Object result;
        currentTime.set(System.currentTimeMillis());
        result = joinPoint.proceed();
        Log log = new Log("INFO",System.currentTimeMillis() - currentTime.get());
        currentTime.remove();
        HttpServletRequest request = RequestHolder.getHttpServletRequest();
        logService.save(getUsername(), StringUtils.getBrowser(request), StringUtils.getIp(request),joinPoint, log);
        return result;
    }

    /**
     * 配置异常通知
     *
     * @param joinPoint join point for advice
     * @param e exception
     */
    @AfterThrowing(pointcut = "logPointcut()", throwing = "e")
    public void logAfterThrowing(JoinPoint joinPoint, Throwable e) {
        Log log = new Log("ERROR",System.currentTimeMillis() - currentTime.get());
        currentTime.remove();
        log.setExceptionDetail(ThrowableUtil.getStackTrace(e).getBytes());
        HttpServletRequest request = RequestHolder.getHttpServletRequest();
        logService.save(getUsername(), StringUtils.getBrowser(request), StringUtils.getIp(request), (ProceedingJoinPoint)joinPoint, log);
    }
    ...
}

 	@Log("用户登录")
    public ResponseEntity<Object> login(@Validated @RequestBody UserDTO user, HttpServletRequest request) throws Exception {
        // 登录过程
        ...
  }

```



# Spring完整揭秘（六）：使用maven建立Spring AOP 的完整案例

## 项目工程

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200806164944913.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

## 导入依赖

- 首先新建一个maven项目，在项目的pom.xml中添加spring相关及AOP的依赖项：

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>spring</groupId>
    <artifactId>aopdemo</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <spring.version>5.2.2.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjrt</artifactId>
            <version>1.6.12</version>
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.6.12</version>
        </dependency>
        <dependency>
            <groupId>cglib</groupId>
            <artifactId>cglib</artifactId>
            <version>2.2</version>
        </dependency>
    </dependencies>

</project>

```

### 注入目标

- 新建一个用户类User及用户服务类UserService，是我们AOP注入的目标类：
- Service类中定义了2个方法，增加用户addUser方法，删除用户deleteUser方法并抛出运行时的异常。

```
/**
 * 用户类
 */
public class User {
    private String name;
    private String password;

    public User() {
    }

    public User(String name, String password) {
        this.name = name;
        this.password = password;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "demo.aop.User{" +
                "name='" + name + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}

/**
 * 用户服务类
 */
@Service
public class UserService {
    /**
     * 增加用户
     */
    public void addUser(User user) {
        System.out.println("增加用户:"+user.toString());
    }
	 /**
     * 删除用户
     */
    public void deleteUser(User user){
        System.out.println("删除用户:"+user.toString());
        throw new RuntimeException("edit person throw exception");
    }

}

```

### Aspect类

- Aspect类中定义pointCut()方法，此方法无任何执行内容，只有一个@Pointcut的注解，其他方法都会引用这个注解中指定的pointcut表达式。
- 该类中还包括了各种Advice类型的方法实现，且都可以通过JoinPoint实例来获得方法执行的上下文信息，参数信息。

```
/**
 * aop组件
 */
@Aspect
@Component
public class AspectComponent {

    @Pointcut("execution(* demo.aop.*Service*.*(..))")
    public void pointCut(){

    }

    @Before("pointCut()")
    public void before(JoinPoint joinPoint) {
        System.out.println("before aspect executed"+joinPoint.toString());
    }

    @After("pointCut()")
    public void after(JoinPoint joinPoint) {
        System.out.println("after aspect executed:"+joinPoint.toString());
    }


    @AfterReturning(pointcut = "pointCut()", returning = "returnVal")
    public void afterReturning(JoinPoint joinPoint, Object returnVal) {
        System.out.println("afterReturning executed, return result is "
                + returnVal +joinPoint.toString());
    }

    @Around("pointCut()")
    public void around(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("around start");
        try {
            pjp.proceed();
        } catch (Throwable ex) {
            System.out.println("error in around");
            throw ex;
        }
        System.out.println("around end");
    }

    @AfterThrowing(pointcut = "pointCut()", throwing = "error")
    public void afterThrowing(JoinPoint joinPoint, Throwable error) {
        System.out.println("error:" + error+joinPoint.toString());
    }
}


```

### Spring配置

- beans节点中需要指定aop命名空间
- 启用aop需要添加aop:aspectj-autoproxy/
- context:component-scan/节点用来指定自动扫描bean的命名空间。

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           http://www.springframework.org/schema/aop/spring-aop.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd">
    <aop:aspectj-autoproxy />
    <context:component-scan base-package="demo.aop" />
</beans>

```

### 测试

- 测试下aop的效果，需要新建一个Application类作为程序的入口：

```

/**
 * aop测试程序
 */
public class Application {
    public static void main(String[] args) {

        ClassPathXmlApplicationContext ctx = new ClassPathXmlApplicationContext("application.xml");

        // 测试用户服务aop过程
        UserService userService=ctx.getBean(UserService.class);
        User user = new User("jack","123456");
        userService.addUser(user);
        System.out.println("======================================================================");
        userService.deleteUser(user);

        ctx.close();
    }
}

```

观察执行结果可以看到：执行的Before，around，after以及around，afterReturning，afterThrowing都按正常的顺序执行。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200806170304432.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)





# Spring完整揭秘（七）：使用Spring JDBC访问数据



#### DAO模式

- 为了统一和简化软件系统的数据访问操作，在常规的Java软件系统分层中，都会定义DAO数据访问层，使用该模式，既可以分离业务逻辑与数据访问，又可以屏蔽各种数据底层操作的差异。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200810113121367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

##### DAO模式示例

- 使用DAO模式访问用户数据

```
/**
 * 用户数据访问层(DAO)接口
 *
 * @author zhuhuix
 * @date 2020-08-01
 */

public interface UserDAO {
    // 查找所有用户
    List<User> findAll();

    // 根据id查找用户
    User findById(Long id);

    // 新增用户
    Long addUser(User user);

    // 更新用户
    void updateUser(User user);

    // 删除用户
    void deleteById(Long id);

    // 自定义添加通过用户名称查找用户信息
    List<User> findByName(String name);
}

```

- 依赖DAO接口的业务逻辑层

```
public class UserService {
    private UserDAO userDAO;
    
    // 返回所有的用户
    public List<User> listUsers() {
        return userDAO.findAll();
    }

    // 保存用户
    public User saveUser(User user) {
        // 保存数据
        if (user.getId() != null && user.getId() != 0) {
            userDAO.updateUser(user);
        } else {
            userDAO.addUser(user);
        }
        return user;
    }

    // 删除用户
    public void deleteUser(Long id) {
        userDAO.deleteById(id);
    }

    // 查找用户
    public User findUser(Long id) {
        return userDAO.findById(id);
    }

    // 根据名称查找用户
    public List<User> searchUser(String name) {
        return userDAO.findByName(name);
    }
}

```

#### JDBC API

- 在Spring JdbcTemplate诞生之前，开发人员需要使用JDBC API实现数据访问层：

```
/**
 * 使用JDBC API实现用户数据访问层
 *
 * @author zhuhuix
 * @date 2020-08-10
 */
public class UserDAOImpl implements UserDAO {
    @Override
    public User findById(Long id) throws SQLException {
        Connection conn = null;
        try {
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/user_info", "root", "root");
            String sql = "select id,name,email from user where id=" + id;
            Statement st = conn.createStatement();
            ResultSet resultSet = st.executeQuery(sql);
            User user = new User();
            if (resultSet != null) {
                user.setId(resultSet.getArray("id"));
                user.setName(resultSet.getArray("name"));
                user.setEmail(resultSet.getArray("email"));
            }
        } catch (SQLException ex) {
            throw new SQLException(ex);
        } finally {
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException ex) {
                    throw new SQLException(ex);
                }
            }
        }

    }
...
}

```

- 由于JDBC API主要是面向底层的数据库操作，所以存在比较大的缺点：

1. 需要频繁的创建数据库连接；
2. 涉及到的增删改查等功能需要在各个java文件中编写大量代码
3. 对于底层事务、数据类型转换等都需要手动处理，效率低下



#### 基于 Spring JdbcTemplate的数据访问层实现

- 为了解决JDBC API的缺点，Spring框架构建Spring JdbcTemplate模板类，封装了所有基于JDBC API的数据访问代码，同时也将数据访问异常统一纳入Spring异常管理。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200810125150846.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)

```
/**
 * 使用JdbcTemplate模板类实现用户数据访问层
 *
 * @author zhuhuix
 * @date 2020-08-10
 */
@Repository
public class UserDAOImpl implements UserDAO {
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public List<User> findAll() {
        return jdbcTemplate.query("select id,name,email from user;",
                new Object[]{}, new BeanPropertyRowMapper<>(User.class));
    }

    @Override
    public User findById(Long id) {
        return jdbcTemplate.queryForObject("select id,name,email from user where id=?;",
                new Object[]{id}, new BeanPropertyRowMapper<>(User.class));
    }

    @Override
    public Long addUser(User user) {
        return Integer.toUnsignedLong(jdbcTemplate.update("insert into  user(name,email) values(?,?);"
                , user.getName(), user.getEmail()));
    }

    @Override
    public void updateUser(User user) {
        jdbcTemplate.update("update user set name=?,email=? where id =?;"
                , user.getName(), user.getEmail(), user.getId());
    }

    @Override
    public void deleteById(Long id) {
        jdbcTemplate.update("delete from user where id=?", new Object[]{id});
    }

    @Override
    public List<User> findByName(String name) {
        return jdbcTemplate.query("select id,name,email from user where name=?;",
                new Object[]{name}, new BeanPropertyRowMapper<>(User.class));
    }
}


```

- 从以上代码可以看出，使用Spring JdbcTemplate模板类，开发人员只需关心与数据访问逻辑相关的东西 ，对于JDBC API底层实现的相关细节不用过多地考虑。

##### 将SQLException转译到DataAccessException

- Spring JdbcTemplate对SQLException所提供的异常信息进行统一转译，将基于JDBC API的数据访问异常纳入Spring身的异常体系中，极大地简化了业务逻辑层对数据访问异常的处理。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200810140859953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pwZ3podQ==,size_16,color_FFFFFF,t_70)



- 转译抽象类源码

```
public abstract class AbstractFallbackSQLExceptionTranslator implements SQLExceptionTranslator {
	/**
	 * Pre-checks the arguments, calls {@link #doTranslate}, and invokes the
	 * {@link #getFallbackTranslator() fallback translator} if necessary.
	 */
	@Override
	@Nullable
	public DataAccessException translate(String task, @Nullable String sql, SQLException ex) {
		Assert.notNull(ex, "Cannot translate a null SQLException");

		DataAccessException dae = doTranslate(task, sql, ex);
		if (dae != null) {
			// Specific exception match found.
			return dae;
		}

		// Looking for a fallback...
		SQLExceptionTranslator fallback = getFallbackTranslator();
		if (fallback != null) {
			return fallback.translate(task, sql, ex);
		}

		return null;
	}
	...
}

```

##### SpringBoot使用JdbcTemplate的配置

- 在SpringBoot中使用JdbcTemplate需完成以下配置：

```
# application.yml
spring:
  datasource:
    # 数据库驱动
    driver-class-name: com.mysql.jdbc.Driver
    # 数据库地址
    url: jdbc:mysql://localhost:3306/user_info
    # 数据库用户名
    username: root
    # 数据库密码
    password: root

```

##### JdbcTemplate的常用方法

- 查询方法

|                  |                        |
| ---------------- | ---------------------- |
| query            | 查询并对结果集自行封装 |
| queryForObject() | 查询并返回一个对象     |
| queryForList()   | 查询并返回多条记录     |
| queryForMap()    | 查询并返回一条记录     |

- 操作方法

|             |                               |
| ----------- | ----------------------------- |
| execute     | 执行sql语句，无返回值         |
| update      | 执行sql语句，返回受影响的行数 |
| batchUpdate | 执行批量更新                  |

#### 完整案例

- 可参考本人文章[Spring全家桶的深入学习(三）:实现数据持久化](https://blog.csdn.net/jpgzhu/article/details/107119151)