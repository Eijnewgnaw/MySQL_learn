###### 多表查询

准备sql

<img src="Multi-table%20query.assets/image-20200904200620564.png" alt="image-20200904200620564" style="zoom:150%;" />

- 基本查询语法：

```mysql
select 列名列表 from 表名列表 where 条件列表;
```

```mysql
select * from emp,dept;    --产生笛卡尔积
```

笛卡尔积：多个集合的组合情况（如：上表5 x 3）

​					就会产生冲突数据，完成多表查询 ，消除无用数据组

- 多表查询分类：

  - [ ] 内连接查询：

    注意：

    - 从哪些表中查询数据
    - 条件是什么
    - 查询哪些字段

    1、隐式内连接：使用 where 条件

    ```mysql
    select 
    	emp.name,
    	emp.gender,
    	dep.name 
    from 
    	emp,dept 
    where 
    	emp.dep_id=dpt.id;
    ```

    2、显式内链接：
    select 字段列表 from 表名1 inner join 表名2 on 条件

    ```mysql
    select 
    	* from emp 
    inner join 
    	dept 
    on 
    	emp.dept_id =  dpt.id;	
    	--inner 可以省略
    ```

    

  - [ ] 外连接查询

    1、左外连接

    ```mysql
    select * from 表A left [outer] join 表B on 表A.主键=表B.外键;
    ```

    \- 左外连接查询以左边的表为主：
    \- 左边有的数据，右边没有，使用空代替
    \- 左边没有的数据，右边也不能出现

    2、右外连接

    ```mysql
    select * from 表A right [outer] join 表B on 表A.主键=表B.外键;
    ```

    注意：
    \- 右外连接查询以右边的表为主：
    \- 右边有的数据，左边没有，使用空代替
    \- 右边没有的数据，左边也不能出现

  - [ ] 子查询

    - 一条sql语句的查询结果，作为另外一条sql语句的查询条件
      格式：

      ```mysql
      select 
      	* from 表B 
      where 
      	字段 = (select 字段 from 表A 
                [where 条件])
      ```

      ```mysql
      select 
      	* from emp 
      where 
      	emp.salary = (select Max(salary) from emp);
      	--使用运算符+条件（单行单列）
      ```

      ```mysql
      select 
      	* from emp 
      where 
      	dept_id in
      	(select 
           	id from dept
      	 where 
           	name in("财务部"，"市场部"));
           	--多行单列
      ```

      

    - 一条sql语句的查询结果，作为另一条sql语句的一张表(隐式内连接查询)
      格式：

      ```mysql
      select
      	* from 
      		(select 
               	* from 表A 
               [where 条件]),表B
      where 
      	表A.主键=表B.外键;
      ```

      ```mysql
      select 
      	* from dept as t1,
      (select 
       	* from emp 
       where 
       	emp.join_date >"2011-11-11") as t2 
      where 
      	t1.id=t2.dept_id;
      	--多行多列
      ```

      可以用普通内连接


