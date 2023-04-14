# 第一章、JDBC

## 1、概念

JDBC就是使用Java语言操作关系型数据库的一套API

全称 Java Data Base Connectivity Java数据库连接

### **本质**

定义的一套操作所有关系数据库的规则，即接口

![img](https://img-blog.csdnimg.cn/d16e15bbdb3545189dc1c9481d6c25c9.png)

### 快速入门

![img](https://img-blog.csdnimg.cn/3c6af59096104f5ca0ce7950d250d60d.png)

```java
import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) {
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        try {
            // 加载MySQL驱动程序
            Class.forName("com.mysql.jdbc.Driver");
            // 建立与数据库的连接
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "123456");
            // 创建Statement对象
            stmt = conn.createStatement();
            // 执行查询语句
            rs = stmt.executeQuery("SELECT * FROM users");
            // 处理查询结果集
            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                int age = rs.getInt("age");
                System.out.println("id: " + id + ", name: " + name + ", age: " + age);
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 释放资源
            try {
                if (rs != null) rs.close();
                if (stmt != null) stmt.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```



## 2、API详解

### 2.1、DriverManager

驱动管理类 作用：

1. 注册驱动

   ```java
   Class.forName("com.mysql.jdbc.Driver");
   ```

2. 获取数据库连接

   ![img](https://img-blog.csdnimg.cn/d146c6b0f27a41b6ab19621f8e0a0ca0.png)

### 2.2、Connection

数据库连接对象

作用：

1. 获取执行SQL的对象
2. 管理事务

- 普通执行SQL对象

  ```java
  //如果加了形参true;则表示开启自动提交事务
  Statement createStatement();
  ```

- 预编译SQL的执行SQL对象：防止SQL注入

  ```java
  PreparedStatement prepareStatement(sql);
  ```

- 执行存储过程的对象

  ```java
  CallableStatement prepareCall(sql);
  ```

![img](https://img-blog.csdnimg.cn/4d2f02a2e2294387bb6eb3e65009b447.png)

### 2.3、Statement

作用：执行sql语句

```java
executeUpdate(sql);  //执行DML、DDL语句  返回int类型
//返回值：（1）DML语句影响的行数    （2）DDL语句执行后，执行成功也可能返回0
executeQuery(sql);  //执行DQL语句  返回ResultSet类型
//返回值：（1）ResultSet jie'guo'ji
```

DML, DDL和DQL是数据库中的三种不同的语言类型，分别是：

1. DML(Data Manipulation Language)：数据操作语言，主要用于对数据库中的数据进行增、删、改、查操作，例如 SELECT、INSERT、UPDATE、DELETE 等。
2. DDL(Data Definition Language)：数据定义语言，主要用于定义数据库中的各种对象，如创建表、修改表结构、删除表等操作，例如 CREATE、ALTER、DROP 等。
3. DQL(Data Query Language)：数据查询语言，主要用于查询数据库中的数据，例如 SELECT、FROM、WHERE 等。

总的来说，DML主要用于操作数据，DDL主要用于定义数据，DQL主要用于查询数据。

**执行DDL语句的返回值可能是0**

### 2.4、ResultSet

结果集对象：封装了DDL查询语句的结果

```java
stmt.executeQuery(sql);   //执行DQL语句，返回ResultSet对象
```

![img](https://img-blog.csdnimg.cn/c4a6f09b02ea43629925bfd29c3fd6e6.png)

使用步骤：

1. 游标向下移动一行，并判断改行是否有数据：next（）
2. 获取数据：getXxx(参数)

```java
//循环判断游标是否是最后一行末尾
while(rs.next()){
	rs.getXxx(参数);
}
```

### 2.5、PreparedStatement

作用：

1. 预编译SQL语句并执行：预防SQL注入问题

SQL注入：通过操作输入来修改事先定义好的SQL语句，用以达到执行代码对服务器进行攻击的方法。

![img](https://img-blog.csdnimg.cn/c9a363e887794a6f8628888db55df089.png)

原理：

![img](https://img-blog.csdnimg.cn/4eeefd79a21d452daed0d5301244c1a1.png)

好处：

1. 预编译SQL，性能更高。
2. 防止SQL注入，将敏感字符进行转义。（例如输入‘or’1'='1）

![img](https://img-blog.csdnimg.cn/adde5501ccff47cf877b304a8fea55dd.png)

## 3、数据库连接池

### 3.1、简介

数据库连接池是一个容器，负责分配，管理数据库连接（connection）。

它允许应用程序重复使用一个现有的数据库连接，而不是再重新建立一个。

释放空闲时间超过最大空闲时间的数据库连接来避免因为没有释放数据库连接而引起的数据库连接遗漏

好处：

1. 资源重用
2. 提升系统响应时间
3. 避免数据库连接遗漏。

### 3.2、常用的数据库连接池

1. DBCP
2. C3P0
3. Druid:(德鲁伊) 阿里巴巴开源的数据库连接池项目，功能强大，性能优秀，是Java语言最好的数据库连接池之一

### 3.3、使用步骤

![img](https://img-blog.csdnimg.cn/c4416035ccd6484399d26fa8fffe15ee.png)

官方提供的数据库连接池标准接口，由第三方组织实现此接口。

```java
Connection     getConnection();
```

#### 3.3.1、添加依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.10</version>
</dependency>
```

#### 3.3.2、配置

在配置文件中添加Druid连接池的配置，例如在Spring Boot项目中可以在application.properties文件中添加：

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
spring.datasource.filters=stat,wall,log4j
spring.datasource.maxActive=20
spring.datasource.initialSize=1
spring.datasource.minIdle=1
spring.datasource.maxWait=60000
spring.datasource.timeBetweenEvictionRunsMillis=60000
spring.datasource.minEvictableIdleTimeMillis=300000
spring.datasource.validationQuery=SELECT 1
spring.datasource.testWhileIdle=true
spring.datasource.testOnBorrow=false
spring.datasource.testOnReturn=false
spring.datasource.poolPreparedStatements=true
spring.datasource.maxPoolPreparedStatementPerConnectionSize=20
spring.datasource.connectionProperties=druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000
```

这里的配置包括了数据库连接相关的配置，如url、username、password、driver-class-name等，以及Druid连接池的配置，如maxActive、initialSize、minIdle等。

#### 3.3.3、获取数据库

在代码中获取Druid连接池的数据源，例如在Spring Boot项目中可以使用注入方式：

```java
@Autowired
private DataSource dataSource;
```

然后就可以使用dataSource来获取数据库连接了：

```java
javaConnection conn = dataSource.getConnection();
```

以上就是使用Druid连接池的基本步骤，需要注意的是，Druid连接池还支持一些高级特性，如监控、防御SQL注入等，可以根据具体需求进行配置。

# 第二章、MyBatis

## 1、定义

1. 是一款优秀的持久层框架，用于简化JDBC开发
2. 是Apache的一个开源项目

**持久层**

负责将数据保存到数据库的那一层代码

JavaEE三层构架：表现层、业务层、持久层

**框架**

+ 框架就是一个半成品软件，是一套可重用的、通用的、软件基础代码模型
+ 在框架的基碰之上构建软件编写更加高效、规范、通用、可扩展

**JDBC缺点**

+ 硬编码
  + 注册驱动，获取链接
  + SQL语句

+ 操作繁琐
  + 手动设置参数
  + 手动封装结果集

**MyBatis免除了几乎所有的JDBC代码以及设置参数和获取结果集的工作**

## 2、流程

1. 引入 MyBatis 的依赖库，可以通过 Maven 或 Gradle 等构建工具来管理依赖。
2. 创建 MyBatis 的配置文件（通常为 mybatis-config.xml），配置数据源、事务管理器、类型别名、映射器等信息。以下是一个示例配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
    "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <typeAliases>
    <typeAlias type="com.example.User" alias="User"/>
  </typeAliases>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/test"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="com/example/UserMapper.xml"/>
  </mappers>
</configuration>
```

3. 创建映射器（Mapper）接口，定义 SQL 语句和参数映射。以下是一个示例 Mapper 接口：

```java
public interface UserMapper {
    User getUserById(int id);
    void insertUser(User user);
}
```

4. 创建映射器的 XML 文件（通常为 Mapper 接口名加上 “.xml” 后缀，例如 UserMapper.xml），配置 SQL 语句和结果映射。以下是一个示例 Mapper XML 文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.UserMapper">
  <select id="getUserById" resultType="User">
    select * from user where id = #{id}
  </select>
  <insert id="insertUser" parameterType="User">
    insert into user (name, age) values (#{name}, #{age})
  </insert>
</mapper>
```

5. 在应用程序中配置 MyBatis，创建 SqlSessionFactory，并从中获取 SqlSession 对象。以下是一个示例代码：

```java
String resource = "mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
SqlSession sqlSession = sqlSessionFactory.openSession();
UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
User user = userMapper.getUserById(1);
sqlSession.close();
```

## 3、Mybatis核心配置

+ configuration(配置）
  + properties(属性)
  + settings(设置)
  + typeAliases(类型别名)
  + typeHandlers(类型处理器）
  + objectFactory(对象工厂)
  + plugins(插件)
  + environments(环境配置)
    + environment(环境变量）
      + transactionManager(事务管理器)
      + dataSource(数据源）

+ + databaseldProvider(数据库商识）
  + mappers(映射器）

==注意：配置各个标签时，需要遵守前后顺序==

## 4、查询操作

### 4.1、查询所有

**实体类属性名和数据库表列名不一致，不能自动封装数据**

#### 4.1.2、起别名

缺点：每一次都要定义一次别名

```xml
<select id="selectAll" resultType="brand">
	select id,brand_name as brandName,company_name as companyName,ordered,description,status from tb_brand;
</select>
```

#### 4.1.2、定义sql代码片段

缺点：不灵活

```xml
<sql id="brand_column">
	id,brand_name as brandName,company_name as companyName,ordered,description,status
</sql>
<select id="selectAll"resultType="brand">
	select
		<include refid="brand_column"/>
	from tb_brand;
</select>
```

#### 4.1.3、resultMap

定义<resultMap>完成不一致的属性名和列名的映射

```xml
<!--
	id:唯一标识
	type:映射的类型，支特别名
-->
<resultMap id="brandResultMap" type="brand">
<!--
	id:完成主健字段的映射
		column:表的列名
		property:实体类的属性名
	result:完成一般字段的映射
		column:表的列名
		property:实体类的属性名
-->
<result column="brand_name" property="brandName"/>
<result column="company_name" property="companyName"/>
</resultMap>
<select id="selectAll" resultType="brand">
	select * from tb_brand;
</select>
```

### 4.2、查询详情

查询详情就是指传了个参数

```xml
<select id="selectById" resultMap="brandResultMap">
select * from tb_brand where id = #{id};
</select>
```

1.参数占位符：

+ #:执行SQL时，会将#{}占位符替换为？，将来自动设置参数值
+ `${}`:拼SQL。会存在SQL注入问题
+ 使用时机：
  + 参数传递，都使用#{}
  + 如果要对表名、列名进行动态设置，只能使用${}进行sql拼接。

2. parameterType:
   用于设置参数类型，该参数可以省略(比如设置parameterType="int",则id只能为int)
3. SQL语句中特殊字符处理：（比如<,>等）
   + 转义字符 (`&lt`);
   + <I[CDATA[内容]>(输入cd即可)

### 4.3、条件查询

```xml
<select id="selectByCondition" resultType="brandResultMap">
	select * from tb_brand where
	status=#{status}
	and company_name=#{companyName}
	and brand_name like #{brandname}
</select>
```

#### 4.3.1、散装参数

如果方法中有多个参数，需要使用@Param("SQL中的参数占位符名称")

```java
List<Brand> selectBycondition(@Param("status")int status,@Param("companyName")String company,@Param("brandname")String brandname);

int status = 1;
string companyName = "华为";
string brandname = "%brandname%"  //因为是like所以需要要模糊查找
```

#### 4.3.2、对象参数

只需要保证SQL中的参数名和实体类属性名对应上，即可设置成功

```java
List<Brand> selectBycondition(Brand brand);

Brand brand = new Brand();
brand.setStatus(status);
brand.setcompanyName(companyName);
brand.setbrandname(brandname);
```

#### 4.3.3、Map集合

只需要保证sQL中的参数名和map集合的键的名称对应上，即可设置成功

```java
List<Brand> selectBycondition(Map map);

Map map = new  HashMap();
map.put("status",status);
map.put("companyName",companyName);
map.put("brandname",brandname);
```

### 4.4、动态查询

#### 4.4.1、多条件

```xml
<select id="selectByCondition"resultMap="brandResultMap">
	select *
	from tb_brand
	/*where 11*/
	<where>
		<if test="status!=null">
			and status =#{status}
		</if>
		<if test="companyName!=null and companyName !=""
			and company_name like #{companyName}
		</if>
		<if test="brandName !null and brandName !=""
			and brand_name like #{brandName}
		</if>
</where>
```

#### 4.4.1、多条件选其一

choose(when,itherwise)类似Java的switch语句

```xml
<select id="selectByConditionSingle"resultMap="brandResultMap">
	select
	from tb brand
	<where>
	<choose><-类似于switch->
    <when test=-"status=null"><l-类似于case->
		status #(status)
	</when>
	<when test="companyName !=null and companyName !=''"
		company_name like #(companyName)
	</when>
	<when test="brandName !=null and brandName !=''"
		brand_name like #(brandName)
	</when>
	<!--<otherwise><!--类似于default->
		1=1
	</otherwise>->
	</choose>
</select>
```

## 5、添加操作

```xml
<insert id="add">
insert into tb_brand (brand_name,company_name,ordered,description,status)
values (#{brandName,#{companyName},#{ordered},#{description},#{status});
</insert>
```

==注意：这里需要手动提交事务==

```java
sqlSession.commit();
```

#### 5.1、主键返回

```
<insert useGenerateKeys="true" keyProperty="id">
```

## 6、修改操作

### 6.1、修改全部字段

```xml
<update id="update">
update tb brand
set brand_name =#{brandName},
company_name =#{companyName}，
ordered =#{ordered}，
description =#{description},
status =#{status},
where id =#{id};
</update>
```

### 6.2、修改动态片段

```xml
<update id="update">
update tb brand
<set>
<if test="brandName !=null and brandName !=''"
brand_name =#{brandName),
</if>
<if test="companyName !=null and companyName !=''"
company_name =#{companyName},
</if>
<if test="ordered !=null">
ordered =#fordered},
</if>
<if test="description !=null and description !=''"
description =#{description},
</if>
<if test="status !=null">
status =#{status},
</if>
</set>
where id =#{id};
</update>
```

## 7、删除操作

### 7.1、删除一个

```xml
<delete id="deleteByld">
delete from tb brand where id =#{id}
</delete>
```

### 7.2、删除多个

```xml
<delete id="deleteBylds">
delete from tb brand
where id in
<foreach collection="ids"item="id"separator=","open="(" close=")">
#{id}    //ids必须要加@param注解,或者写成array
</foreach>
</delete>
```

```java
void deleteByIds(@Param("ids") int[] ids);


int[] ids={1,2,3};
brandMapper.deleteByIds(ids);
```

## 8、注解完成增删改查

![image-20230408114557540](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230408114557540.png)

## 9、@param注解详解

### 9.1、使用

@Param注解一般用于在MyBatis中映射SQL语句中的参数，通常情况下，如果方法参数只有==一个且是基本类型或者String类型，可以不使用@Param注解==。但是在以下情况下需要使用@Param注解：

1. 方法参数有多个，需要使用@Param注解来指定每个参数对应的占位符名称。

例如：

```java
java@Update("UPDATE user SET name = #{name}, age = #{age} WHERE id = #{id}")
void updateUser(@Param("name") String name, @Param("age") int age, @Param("id") Long id);
```

2. 方法参数是自定义对象，需要使用@Param注解来指定对象属性对应的占位符名称。

例如：

```java
java@Select("SELECT * FROM user WHERE name = #{user.name} AND age = #{user.age}")
List<User> getUserList(@Param("user") User user);
```

3. SQL语句中有多个占位符需要使用@Param注解来指定每个占位符对应的参数值。

例如：

```java
java@Select("SELECT * FROM user WHERE name = #{name} AND age BETWEEN #{minAge} AND #{maxAge}")
List<User> getUserList(@Param("name") String name, @Param("minAge") int minAge, @Param("maxAge") int maxAge);
```

### 9.2、不使用

以下是不使用@Param注解的情况：

1. 方法参数只有一个，且是基本类型或String类型。

例如：

```java
java@Select("SELECT * FROM user WHERE id = #{id}")
User getUserById(Long id);
```

2. SQL语句中只有一个占位符，且占位符名称与方法参数名称相同。

例如：

```java
java@Select("SELECT * FROM user WHERE name = #{name}")
List<User> getUserList(String name);
```

3. 方法参数是Map类型，且Map中的key与SQL语句中的占位符名称相同。

例如：

```java
java@Select("SELECT * FROM user WHERE name = #{name} AND age = #{age}")
List<User> getUserList(Map<String, Object> params);
```

总之，如果方法参数与SQL语句中的占位符名称一致，或者只有一个参数且是基本类型或String类型，就可以不使用@Param注解。
