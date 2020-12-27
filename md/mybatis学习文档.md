# 第一章mybatis概述



## 1 mybatis简介

MyBatis 是支持定制化 SQL、存储过程以及高级映射的优秀的持久层框架。

MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。

MyBatis可以使用简单的XML或注解用于配置和原始映射，将接口和Java的POJO（Plain Old Java Objects，普通的Java对象）映射成数据库中的记录。



## 2 mybatis历史

原是apache的一个开源项目iBatis, 2010年6月这个项目由apache software foundation 迁移到了google code，随着开发团队转投Google Code旗下，ibatis3.x正式更名为Mybatis ，代码于2013年11月迁移到Github（下载地址见后）。

iBATIS一词来源于“internet”和“abatis”的组合，是一个基于Java的持久层框架。iBATIS提供的持久层框架包括SQL Maps和Data Access Objects（DAO）



## 3 为什么要使用mybatis

MyBatis是一个半自动化的持久化层框架。

jdbc编程---当我们使用jdbc持久化的时候，sql语句被硬编码到java代码中。这样耦合度太高。代码不易于维护。在实际项目开发中会经常添加sql或者修改sql，这样我们就只能到java代码中去修改。

Hibernate和JPA

长难复杂SQL，对于Hibernate而言处理也不容易。

内部自动生产的SQL，不容易做特殊优化。

基于全映射的全自动框架，javaBean存在大量字段时无法只映射部分字段。导致数据库性能下降。

对开发人员而言，核心sql还是需要自己优化。

sql和java编码分开，功能边界清晰，一个专注业务、一个专注数据。

可以使用简单的XML或注解用于配置和原始映射，将接口和Java的POJO映射成数据库中的记录。成为业务代码+底层数据库的媒介

# 第二章mybatis的helloworld



## 1 创建一个数据库和表结构

```mysql
drop database if exists mybatis;

create database mybatis;

use mybatis;

## 创建单表
create table t_user(
	`id` int primary key auto_increment,
	`last_name`	varchar(50),
	`sex` int
);

insert into t_user(`last_name`,`sex`) values('wzg168',1);

select * from t_user;
```



| JavaBean类 | 以前    | mybatis中  |
| ---------- | ------- | ---------- |
| User       | UserDao | UserMapper |
| Book       | BookDao | BookMapper |

在mybatis中使用Mapper接口习惯命名如下（mybatis中不需要字节写实现类）

| JavaBean类 | Dao（Mapper）接口名 | sql语句配置文件名 |
| ---------- | ------------------- | ----------------- |
| User       | UserMapper          | UserMapper.xml    |
| Book       | BookMapper          | BookMapper.xml    |



## 2 myabtis-helloworld

### 2.1 创建一个java模块

### 2.2 导入所需要的jar包

![image-20201226180434924](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201226180434924.png)

### 2.3 编写数据库表所对应的JavaBean

```java
public class User {
    private Integer id;
    private String lastName;
    private int sex;
    //省略 setter 和 getter 方法
}
```



### 2.4 编写Mapper接口

```java
public interface UserMapper {

    /**
     * 根据用户Id 查询用户对象
     * @param id 用户Id
     * @return 返回 User 对象
     */
    public User selectByUserId(Integer id);
}
```



### 2.5 编写sql配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- namespace 命名空间 它的属性值 必须是对应接口的全类名 -->
<mapper namespace="com.spy.mybatis.mapper.UserMapper">
    <!--
        select 标签 是用来配置 select 查询语句的
        id 是属性配置的唯一标志
        resultType 是查询后每一条记录封装的对象类型
        #{id} 它是占位符 ？
    -->
    <select id="selectByUserId" resultType="com.spy.mybatis.entity.User">
        SELECT id, `last_name`,`sex`
        FROM t_user
        WHERE id =#{id}
    </select>
</mapper>
```



### 2.6 创建mybaits的核心配置文件mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--
        environments 表示配置数据库环境
    -->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <!-- 数据库驱动 -->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <!--
        mybatis 是把sql配置到xml配置文件中
        下面的配置是告诉Mybatis到哪里加载sql的配置文件
    -->
    <mappers>
        <mapper resource="com/spy/mybatis/mapper/UserMapper.xml"/>
    </mappers>
</configuration>

```



### 2.7 测试代码

```java
public class MybatisTest {
    /**
     * mybatis执行流程：
     * 先由Mybatis的核心配置文件mybatis-config.xml创建sqlSessionFactory类
     */
    @Test
    public void test01() {
        try {
            // Resources 类用于读取mybatis的核心配置文件
            InputStream resourceAsStream = Resources.getResourceAsStream("mybatis-config.xml");
            // SqlSessionFactoryBuilder专门用于创建SqlSessionFactory类
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
            System.out.println(sqlSessionFactory);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Test
    public void test02() throws IOException {
        //1、 Resources 类读取 mybatis 的核心配置文件
        InputStream resourceAsStream = Resources.getResourceAsStream("mybatis-config.xml");
        //2、 SqlSessionFactoryBuilder 专门用于创建 SqlSessionFactory类对象
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
        //3、 再由SqlSessionFactory 对象创建SqlSession (SqlSession 相当于JDBC编程中的Connection连接对象 ，每次用完需要关闭)
        SqlSession sqlSession = sqlSessionFactory.openSession();
        try {
            // 4、通过SqlSession 获取Mapper的实现类
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            //5、调用Mapper方法 获取实际的查询对象数据
            User user = userMapper.selectByUserId(1);
            System.out.println(user);
        } finally {
            sqlSession.close();
        }
    }
}
```



## 3 编写Mapper接口的注意事项



- mapper接口必须要和mapper.xml中名称空间值要一致；
- mapper接口中的方法名必须要和mapper.xml中的id值一致；
- mapper接口的参数类型必须要和mapper.xml中的parameterType类型一致；
- mapper接口中的返回值类型必须要和mapper.xml 中的resultType类型一致；



# 第三章 mybatis的CRUD



## 1 mapper接口代码

UserMapper 的实现类 是由mybatis 底层源码进行实现（JDK的动态代理）

```java
public interface UserMapper {

    /**
     * 根据用户Id 查询用户对象
     * @param id 用户Id
     * @return 返回 User 对象
     */
    public User selectByUserId(Integer id);

    /**
     * 查询全部
     * @return
     */
    public List<User> selectAll();
    /**
     * 更新用户
     * @param user
     * @return
     */
    public  int updateUser(User user);

    /**
     * 删除用户
     * @param id
     * @return
     */
    public int deleteUserById(Integer id);

    /**
     * 插入用户
     * @param user
     * @return
     */
    public int insertUser(User user);
}
```

## 2 mapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- namespace 命名空间 它的属性值 必须是对应接口的全类名 -->
<mapper namespace="com.spy.mybatis.mapper.UserMapper">
    <!--
        select 标签 是用来配置 select 查询语句的
        id 是属性配置的唯一标志
        resultType 是查询后每一条记录封装的对象类型
        #{id} 它是占位符 ？
    -->
    <select id="selectByUserId" resultType="com.spy.mybatis.entity.User">
        SELECT id, `last_name` lastName,`sex`
        FROM t_user
        WHERE id =#{id}
    </select>

    <select id="selectAll" resultType="com.spy.mybatis.entity.User">
        SELECT id, last_name lastName ,sex
        FROM  t_user
    </select>
    <!-- parameterType 和 resultType 都是在JavaBean类型的时候才写.-->
    <update id="updateUser" parameterType="com.spy.mybatis.entity.User">
        UPDATE t_user
        SET last_name =#{lastName}, sex =#{sex}
        WHERE id =#{id}
    </update>
    <delete id="deleteUserById">
        DELETE from t_user WHERE  id =#{id}
    </delete>
    <insert id="insertUser" parameterType="com.spy.mybatis.entity.User"
            useGeneratedKeys="true" keyProperty="id">
        INSERT INTO t_user(last_name,sex)
        values (#{lastName},#{sex})
    </insert>
</mapper>
```



## 3 测试代码

```java
static SqlSessionFactory sqlSessionFactory;

    /**
     * @BeforeClass 可以在Junit测试中标识一个static方法用于做初始化使用
     * 标识了 @BeforeClass 的注解的方法会在测试方法之前自动执行
     */
    @BeforeClass
    public static void start() throws IOException {
        System.out.println("开始执行带有@BeforeClass 注解的方法 >>> start()");
        InputStream resourceAsStream = Resources.getResourceAsStream("mybatis-config.xml");
        sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
    }

    /**
     * 根据用户Id 查询用户对象
     */
    @Test
    public void selectByUserId() {
        //sqlSession 相当于 JDBC编程中的Connection 连接对象 ，每次使用完一定要及时关闭
        SqlSession sqlSession = sqlSessionFactory.openSession();
        try {
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            User user = userMapper.selectByUserId(1);
            System.out.println(user);
        } finally {
            //关闭连接
            sqlSession.close();
        }
    }

    @Test
    public void selectAll(){
        SqlSession sqlSession = sqlSessionFactory.openSession();
        try {
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            List<User> users = userMapper.selectAll();
            users.forEach(user -> System.out.println(user));
        } finally {
            sqlSession.close();
        }
    }
    @Test
    public  void updateUser(){
        SqlSession sqlSession = sqlSessionFactory.openSession();
        try {
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            int rows = userMapper.updateUser(new User(1, "spy_test", 1));
            System.out.println("更新的行数"+rows);
            User user = userMapper.selectByUserId(1);
            System.out.println(user);
        } finally {
            sqlSession.close();
        }
    }
    @Test
    public void insertUser(){
        SqlSession sqlSession = sqlSessionFactory.openSession();
        try {
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            User user = new User("李富贵", 1);
            //返回 插入数据影响的行数
            int i = userMapper.insertUser(user);
            System.out.println(i);
            // user.getId() 查询返回的自增主键
            User user1 = userMapper.selectByUserId(user.getId());
            System.out.println(user1);
        } finally {
            sqlSession.close();
        }
    }
    @Test
    public void deleteUserById(){
        SqlSession sqlSession = sqlSessionFactory.openSession();
        try {
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            int i = userMapper.deleteUserById(2);
            System.out.println(i);
        } finally {
            sqlSession.close();
        }
    }
```

## 4 返回自增的主键



**useGeneratedKeys="true"**   表示使用( 返回 )数据库自增的主键值；

**keyProperty="id"** 表示将返回的主键值注入到id属性中；

```xml
<insert id="insertUser" parameterType="com.spy.mybatis.entity.User"
            useGeneratedKeys="true" keyProperty="id">
        INSERT INTO t_user(last_name,sex)
        values (#{lastName},#{sex})
</insert>
```

## 5 selectKey 标签的使用

selectKey是一个标签,常用于在insert标签里配置一个查询操作. 也是经常用来查询插入后生成的主键值。

