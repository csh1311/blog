---
title: spring
date: 2022-12-23
tags:
toc: false
published: false
---
# spring

## 1.spring简介

### 1.1spring是什么

- ​	spring是分层的java SE/EE应用full-stack轻量级开源框架，以Ioc（Inerse Of Control：反转控制）和AOP（Aspect Oriented Programming:面向切面编程）为内核			

## 2.spring快速入门

### 2.1开发步骤

1. 导入spring 开发的基本包坐标

   ```
   //在pom文件导入
   <dependency>
        <groupId>org.springframework</groupId>
         <artifactId>spring-context</artifactId>
         <version>5.3.22</version>
    </dependency>
   ```

2. 编写Dao接口和实现类

   ```spring
   package com.cfc.it.spring_ioc.dao;
   
   /**
    * Created with IntelliJ IDEA.
    * creator: 蔡芳灿
    * Date: 2022/10/15
    * Time: 16:48
    * 需求：接口
    */
   public interface UserDao {
       public void  save();
   }
   
   ```

   ```
   package com.cfc.it.spring_ioc.dao.impl;
   
   import com.cfc.it.spring_ioc.dao.UserDao;
   
   /**
    * Created with IntelliJ IDEA.
    * creator: 蔡芳灿
    * Date: 2022/10/15
    * Time: 16:49
    * 需求：实现类
    */
   public class UserDaoImpl implements UserDao {
   
       @Override
       public void save() {
           System.out.println("save running...");
       }
   }
   
   ```

   

3. 创建spring核心配置文件

   在resource下创建spring配置文件

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
   
   </beans>
   ```

4. 在spring配置文件中配置UserDaoImpl

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
   <!--    配置spring xml id的名字随便起 class指向UserDao实现类-->
       <bean id="userDao" class="com.cfc.it.spring_ioc.dao.impl.UserDaoImpl"></bean>
   
   </beans>
   ```

5. 使用spring 的API获得Bean实例

   ```
   package com.cfc.it.spring_ioc.demo;
   
   import com.cfc.it.spring_ioc.dao.UserDao;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   /**
    * Created with IntelliJ IDEA.
    * creator: 蔡芳灿
    * Date: 2022/10/15
    * Time: 16:56
    * 需求：
    */
   public class UserDaoDemo {
       public static void main(String[] args) {
   
           //使用spring 中ApplicationContext对象创建getBean
           ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
           //参数是spring xml配置的id名称
           UserDao userDao = (UserDao) app.getBean("userDao");
           userDao.save();
       }
   
   }
   
   ```

### 2.2 spring配置文件

#### 2.2.1 Bean标签基本配置

用于配置对象交由spring来创建

默认情况下它调用的是类中的无参构造函数，如果没有无参构造函数则不能创建成功

- 基本属性
  - id:Bean实例在sping容器中的唯一标识，不能重复
  - class：Bean的全限名称

#### 2.2.2Bean标签范围配置

scop：指对象的作用范围，取值如下

| 取值范围       | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| singleton      | 默认值，单例的                                               |
| prototype      | 多例的                                                       |
| request        | web项目中，Spring创建一个Bean的对象，将对象存入到request域中 |
| session        | web项目中，Spring创建一个Bean的对象，将对象存入到session域中 |
| global session | web项目中，应用在Portlet环境，如果没有Portlet环境那么global session相当于session |

```
//导入测试包
  <dependency>
     <groupId>junit</groupId>
     <artifactId>junit</artifactId>
     <version>3.8.2</version>
     <scope>test</scope>
  </dependency>
  
  2.配置spring xml文件scope 参数singleton或者 prototype
     <bean id="userDao" class="com.cfc.it.spring_ioc.dao.impl.UserDaoImpl" scope="singleton"></bean>
    
  3.测试
  package com.cfc.it.spring_ioc;

import com.cfc.it.spring_ioc.dao.UserDao;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;



/**
 * Created with IntelliJ IDEA.
 * creator: 蔡芳灿
 * Date: 2022/10/15
 * Time: 17:27
 * 需求：
 */
public class SpringTest {


    @Test
    //测试scope属性
    public void text1() {

        //使用spring 中ApplicationContext对象创建getBean
        ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
        //参数是spring xml配置的id名称
        UserDao userDao = (UserDao) app.getBean("userDao");
        UserDao userDao1 = (UserDao) app.getBean("userDao");
        //如果spring xml文件中bena参数scope 参数是singleton 两个地址值一样就是单例的
        System.out.println(userDao);  //com.cfc.it.spring_ioc.dao.impl.UserDaoImpl@72d818d1
        System.out.println(userDao1);  //com.cfc.it.spring_ioc.dao.impl.UserDaoImpl@72d818d1

        //如果spring xml文件中bena参数scope 参数是prototype  两个地址值不一样就是多例的
        System.out.println(userDao);  //com.cfc.it.spring_ioc.dao.impl.UserDaoImpl@5bcab519
        System.out.println(userDao1); //com.cfc.it.spring_ioc.dao.impl.UserDaoImpl@e45f292
    }

}

  
  
```

总结

1. 当scope的取值为singleton时
   - bean的实例化个数：1个
   - bean的实例化时机：当spring核心文件被加载时，实例化配置的bean实例
   - Bean的生命周期
     - 对象创建：当应用加载，创建容器时，对象就被创建了
     - 对象运行：只要容器在，对象就一直活着
     - 对象销毁：当应用卸载，销毁容器时，对象就被销毁了
2. 当scope的取值为prototype时
   - Bean的实例化个数：多个
   - Bean的实例化时机：当调用getBean()方法时实例化Bean
   - Bean的生命周期
     - 对象创建：当使用对象时，创建新的对象实例
     - 对象运行：只要对象在使用中，就一直活着
     - 对象销毁：当对象长时间不用时，被java的垃圾回收器回收了

#### 2.2.3Bean实例化三种方式

- 无参构造方法实例化

  - 调用默认时无参构造实例化对象

- 工厂静态方法实例化

  ```
  package com.cfc.it.spring_ioc.factoy;
  
  import com.cfc.it.spring_ioc.dao.UserDao;
  import com.cfc.it.spring_ioc.dao.impl.UserDaoImpl;
  
  /**
   * Created with IntelliJ IDEA.
   * creator: 蔡芳灿
   * Date: 2022/10/30
   * Time: 0:35
   * 需求：
   */
  
  public class StaticFactory {
  
      //工厂静态方法实例化
      private static UserDao getUserDao(){
          return new UserDaoImpl();
      }
  }
  
  
   
  ```

  ```
   #spring配置文件
   
   <bean id="userDao" class="com.cfc.it.spring_ioc.factoy.StaticFactory" factory-method="getUserDao" ></bean
  ```

  

- 工厂实例方法实例化

  ```
  package com.cfc.it.spring_ioc.factoy;
  
  import com.cfc.it.spring_ioc.dao.UserDao;
  import com.cfc.it.spring_ioc.dao.impl.UserDaoImpl;
  
  /**
   * Created with IntelliJ IDEA.
   * creator: 蔡芳灿
   * Date: 2022/10/30
   * Time: 0:47
   * 需求：
   */
  public class DynamicFactory {
  
      //工厂实例方法实例化
      public UserDao getUserDao(){
          return new UserDaoImpl();
      }
  
  }
  
  ```

  ```
  <!--    工厂实例方法实例化配置-->
      <bean id="factory" class="com.cfc.it.spring_ioc.factoy.DynamicFactory"></bean>
      <bean id="userDao" factory-bean="factory" factory-method="getUserDao"></bean>
  ```

### 2.3spring Bean依赖注入

- ​	依赖注入（dependency Injection）：它是spring框架核心IOC的具体实现

- 在编写程序时，通过控制反转，把对象的创建交给了spring，但是代码中不可能出现没有依赖情况

  IOC解耦只是减低它们的依赖关系，但不会消除。列如：业务层会调用持久层

- 那这种业务层和持久层的依赖关系，在使用spring之后，就让spring维护了

  简单的说，就是坐等框架把持久层对象传入业务层，而不用我们自己去获取

#### 2.3.1Bean依赖注入方式

怎么将UserDao怎么样注入到UserService内部呢？

dao层

```
package com.cfc.it.spring_ioc.dao.impl;

import com.cfc.it.spring_ioc.dao.UserDao;

/**
 * Created with IntelliJ IDEA.
 * creator: 蔡芳灿
 * Date: 2022/10/15
 * Time: 16:49
 * 需求：
 */
public class UserDaoImpl implements UserDao {

    @Override
    public void save() {
        System.out.println("save running...");
    }
}
```

```
package com.cfc.it.spring_ioc.dao;

/**
 * Created with IntelliJ IDEA.
 * creator: 蔡芳灿
 * Date: 2022/10/15
 * Time: 16:48
 * 需求：
 */
public interface UserDao {
    public void  save();
}

```



- 构造方法

  - service层

    ```
    package com.cfc.it.spring_ioc.service.impl;
    
    import com.cfc.it.spring_ioc.dao.UserDao;
    import com.cfc.it.spring_ioc.service.UserService;
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 蔡芳灿
     * Date: 2022/10/30
     * Time: 1:05
     * 需求：
     */
    public class UserServiceImpl implements UserService {
    
    
        //这时候通过构造方法依赖注入，这里配置了但是spring不知道
        //需要在spring 配置文件配置
        private UserDao userDao;
    
        public UserServiceImpl(UserDao userDao) {
            this.userDao = userDao;
        }
    
        public UserServiceImpl() {
        }
    
        @Override
        public void service() {
            userDao.save();
        }
    }
    
    ```

    ```
    package com.cfc.it.spring_ioc.service;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 蔡芳灿
     * Date: 2022/10/30
     * Time: 1:04
     * 需求：
     */
    public interface UserService {
        
        public void service();
    
    }
    ```

  - controller

    ```
    package com.cfc.it.spring_ioc.controller;
    
    import com.cfc.it.spring_ioc.service.UserService;
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 
     * Date: 2022/10/30
     * Time: 1:08
     * 需求：
     */
    public class UserController {
    
        public static void main(String[] args) {
            ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
            UserService userService = (UserService) applicationContext.getBean("userService");
            userService.service();
        }
    }
    ```

  - xml配置

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <!--    配置spring xml id的名字随便起 class指向UserDao实现类-->
        <bean id="userDao" class="com.cfc.it.spring_ioc.dao.impl.UserDaoImpl"></bean>
    
    
        <bean id="userService" class="com.cfc.it.spring_ioc.service.impl.UserServiceImpl">
            <constructor-arg name="userDao" ref="userDao"></constructor-arg>
        </bean>
    
    </beans>
    ```

    

- set方法

  - service层

    ```
    package com.cfc.it.spring_ioc.service.impl;
    
    import com.cfc.it.spring_ioc.dao.UserDao;
    import com.cfc.it.spring_ioc.service.UserService;
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 蔡芳灿
     * Date: 2022/10/30
     * Time: 1:05
     * 需求：
     */
    public class UserServiceImpl implements UserService {
    
    
        //这时候通过set方法依赖注入，这里配置了但是spring不知道
        //需要在spring 配置文件配置property
        private UserDao userDao;
    
        public void setUserDao(UserDao userDao) {
            this.userDao = userDao;
        }
    
        @Override
        public void service() {
            userDao.save();
        }
    }
    
    ```

    ```
    package com.cfc.it.spring_ioc.service;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 蔡芳灿
     * Date: 2022/10/30
     * Time: 1:04
     * 需求：
     */
    public interface UserService {
        
        public void service();
    
    }
    
    ```

    

  - controller

    ```
    package com.cfc.it.spring_ioc.controller;
    
    import com.cfc.it.spring_ioc.service.UserService;
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 
     * Date: 2022/10/30
     * Time: 1:08
     * 需求：
     */
    public class UserController {
    
        public static void main(String[] args) {
            ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
            UserService userService = (UserService) applicationContext.getBean("userService");
            userService.service();
        }
    }
    
    ```

  - xml配置

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <!--    配置spring xml id的名字随便起 class指向UserDao实现类-->
        <bean id="userDao" class="com.cfc.it.spring_ioc.dao.impl.UserDaoImpl"></bean>
    
    
    
        <bean id="userService" class="com.cfc.it.spring_ioc.service.impl.UserServiceImpl">
    		    
            <property name="userDao" ref="userDao"></property>
        </bean>
    
    </beans>
    ```

    - set方法注入xml配置P命名空间注入

      - P命名空间注入本质也是set方法注入，但比起上述的set方法注入更加方便，主要体现在配置文件中：如下

        首先，需要引入P命名空间

        ```
        xmlns:p="http://www.springframework.org/schema/p
        ```

        其次，需要修改注入方式

        ```
        <bean id="userService" class="com.cfc.it.spring_ioc.service.impl.UserServiceImpl" p:userDao-ref="userDao"></bean>
        ```

#### 2.3.2Bean的依赖注入的数据类型

- 注入数据的三种数据类型

  - 普通数据类型

    dao

    ```
    package com.cfc.it.spring_ioc.dao.impl;
    
    import com.cfc.it.spring_ioc.dao.UserDao;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 蔡芳灿
     * Date: 2022/10/15
     * Time: 16:49
     * 需求：
     */
    public class UserDaoImpl implements UserDao {
    
    
    
        private String username;
        private int age;
    
        public String getUsername() {
            return username;
        }
    
        public void setUsername(String username) {
            this.username = username;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    
        @Override
        public void save() {
            System.out.println(username+"===="+age);
            System.out.println("save running...");
        }
    }
    
    ```

    ```
    <!--    配置spring xml id的名字随便起 class指向UserDao实现类-->
        <bean id="userDao" class="com.cfc.it.spring_ioc.dao.impl.UserDaoImpl">
            <property name="username" value="zhangsan"></property>
            <property name="age" value="18"></property>
         </bean>
    
    ```

    

  - 引用数据类型

    - 就是之前的userDao注入到userService就是引用数据类型

  - 集合数据类型

    ```
    package com.cfc.it.spring_ioc.dao.impl;
    
    import com.cfc.it.spring_ioc.dao.UserDao;
    import com.cfc.it.spring_ioc.model.User;
    
    import java.util.List;
    import java.util.Map;
    import java.util.Properties;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 蔡芳灿
     * Date: 2022/10/15
     * Time: 16:49
     * 需求：
     */
    public class UserDaoImpl implements UserDao {
    
    
        private List<String> list;
        private Map<String, User> userMap;
        private Properties properties;
    
    
        public List<String> getList() {
            return list;
        }
    
        public void setList(List<String> list) {
            this.list = list;
        }
    
        public Map<String, User> getUserMap() {
            return userMap;
        }
    
        public void setUserMap(Map<String, User> userMap) {
            this.userMap = userMap;
        }
    
        public Properties getProperties() {
            return properties;
        }
    
        public void setProperties(Properties properties) {
            this.properties = properties;
        }
    
        @Override
        public void save() {
            System.out.println(list);
            System.out.println(userMap);
            System.out.println(properties);
            System.out.println("save running...");
        }
    }
    
    ```

    ```
    
    <!--    配置spring xml id的名字随便起 class指向UserDao实现类-->
        <bean id="userDao" class="com.cfc.it.spring_ioc.dao.impl.UserDaoImpl">
    <!--        集合list注入-->
            <property name="list">
                <list>
                    <value>aaa</value>
                    <value>ccc</value>
                    <value>ddd</value>
                    <value>bbb</value>
                </list>
            </property>
    
    <!--        集合map注入-->
            <property name="userMap">
                <map>
                    <entry key="u1" value-ref="user"></entry>
                    <entry key="u2" value-ref="user2"></entry>
                </map>
            </property>
    
        <property name="properties" >
            <props>
                <prop key="dddd">1</prop>
                <prop key="dda">2</prop>
            </props>
        </property>
    
         </bean>
    
    
        <bean id="user" class="com.cfc.it.spring_ioc.model.User">
            <property name="username" value="zhangsan"></property>
            <property name="age" value="18"></property>
        </bean>
        <bean id="user2" class="com.cfc.it.spring_ioc.model.User">
            <property name="username" value="lisi"></property>
            <property name="age" value="20"></property>
        </bean>
    
    ```

    

#### 2.3.4<import>标签：导入其他的spring分件

- 在实际开发中有很多配置但是只有一个主文件，那么我们份文件配置可以使用以下import引入

```
 <import resource="applicationContext_user.xml"></import>
```

![image-20221030230947237](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20221030230947237.png)

### 总结

![image-20221030231228880](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20221030231228880.png)

## 3.spring相关API

- ClassPathXmlApplicationContext

  ```
   ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
  ```

- FileSystemXmlApplicationContext

  ```
  ApplicationContext applicationContext = new FileSystemXmlApplicationContext("D:\\课上\\JAVA\\spring\\spring_ioc\\src\\main\\resources\\applicationContext.xml");
  ```

  

![image-20221030231643599](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20221030231643599.png)

## 4.spring配置数据源

### 4.1数据源（连接池）的作用

- 数据源（连接池）是提高程序性能如出现的
- 事先实例化数据源，初始化部分连接资源
- 使用连接资源时从数据源获取
- 使用完毕后将i按揭资源归还给数据源

常见数据源（连接池）：DBCP、C3P0、BoneCP、Druid等

### 4.2数据源的开发步骤

- 导入数据源的坐标和数据库驱动坐标
- 创建数据源的对象
- 设置数据源的基本连接数据
- 使用数据源获取连接资源和归还连接资源