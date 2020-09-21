#### 数据库连接池

概念：容器（集合），存放数据库连接的容器。

​			当系统初始化后，容器被创建，容器中会申请一些连接对象，当用户来发访问数据库时，从容器中获取连接对象，用户访问完之后将连接对象归还给容器。

优点：节约资源、高效

实现：

1. 标准接口：`DataSource`   `javax.sql`包下的
2. 获取连接：`getConnection()`
3. 归还连接：如果连接对象Connection是从连接池中获取的，那么调用`Connection.close()`方法，则不会关闭连接池。而是归还连接。
4. 一般我们不予实现，由数据库厂商实现（开源）
   1. C3P0：数据库连接池技术
   2. Druid：数据库连接池技术，阿里巴巴提供



**C3P0实现：**

1. 导入jar包：`c3p0-0.9.5.2.jar` 和 `mchange-commons-java-0.2.12.jar`和数据库驱动jar包

2. 定义配置文件

   名称：`c3p0.properties` or `c3p0.config.xml`

   路径：直接将文件放在`src`目录下即可

3. 创建核心对象 数据库连接池对象 `CombopooledDatasource`

4. 获取连接：`getConnection`



**Druid实现：**

1. 导入jar包：`druid-1.0.9.jar`
2. 定义配置文件：
   1. 是properties形式的
   2. 可以叫任意名称，可以放在任意目录下（手动加载）
   3. 获取数据库连接池对象：通过工厂类来获取 `DruidDataSourcefactory`
   4. 获取连接：`getConnection`



**定义工具类：**

1. 定义一个类 `JDBCUtils`
2. 提供静态代码加载配置文件，初始化连接池对象
3. 提供方法：
   1. 获取连接方法：通过数据库连接池获取连接
   2. 获取连接池方法
   3. 释放资源



#### Spring JDBC：JDBC Template

概念：Spring框架对JDBC的简单封装。它提供一个`JDBCTemplate`对象简化JDBC开发

实现：

1. 导入jar包

2. 创建`JDBCTemplate`对象，依赖于数据源`DataSource`

   ```java
   jdbcTemplate template = new jdbcTemplate(datasource);
   ```

3. 调用方法完成CRUD操作

   `update()`：执行DML语句。增、删、改

   `queryForMap()`：查询结果将结果封装为map集合

   `queryForList()`：查询结果将结果集封装为List集合

   `query()`：查询结果，将结果封装为`javaBean`对象

   `queryForObject()`：查询结果，将结果封装为对象