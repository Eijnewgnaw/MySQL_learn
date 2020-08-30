#### 查询

```mysql
select 字段列表 from 表名列表 group by 分组字段 having 分组之后的条件 order by 排序 limit 分页限定;
```

1. 基础查询

   - 多个字段的查询

     ```mysql
     select name,age from student;
     ```

   - 去除重复

     ```mysql
     select distinct address from student;
     ```

     ——查询结果不包含重复地址

     - [ ] 注意空格字符也会被识别成两个不同字符串
     - [ ] 多条列名查询去重要`结果集`完全不同才会被去重

   - 计算列

     ```mysql
     select math,english,math+english from student;
     ```

     - [ ] 有null参与的计算结果都为null

       ```mysql
       select math,English,Math+ IFNULL(English,0) from student;
       ```

       如果English为null则归为0

   - 起别名

     ```mysql
     select math,English,Math+ IFNULL(English,0)as 总分from student;
     ```

2. 条件查询

   - where子句后跟条件

   - 运算符

     特殊：IN(集合)、LIKE、IS NULL、=（等于）

     推荐使用英文单词表示逻辑关系

     null不可被=、！=判断，可用is、is not判断

     - 模糊查询

     ```
     select * from student where name like "%马%";
     ```

     查询姓名中包含马字

   - 排序查询

     ```mysql
     order by 子句
     order by 排序字段1 排序方式1,排序字段2 排序方式2
     ```

     排序方式：

     ​	ASC：升序，默认的

     ​	DESC：降序

     ```mysql
     select * from student order by math; --升序 
     ```

     ```mysql
     select * from student order by math DESC; --降序
     ```

     ```mysql
     select * from student order by math ASC, english ASc; --数学升序排，一样,则按英语升序排
     ```

   - 聚合函数：

     将一列数据作为一个整体，进行纵向计算

     count：计算个数（会忽略null，建议用主键列）

     max：计算最大值

     min：计算最小值

     sum：计算和

     avg：计算平均值

     - [ ] count：

     ```mysql
     select count(name) from  student;--结果是单行单列
     ```

     ```mysql
     select count(ifnull(english,0)) from student;--把null包括其中
     ```

     - [ ] max、min、sum、avg：

       ```mysql
       select max(math) from student;
       select min(math) from student;
       select sum(math) from student;
       select ang(math) from student;
       ```

3. 分组查询

   - group by

     ```mysql
     select sex,avg(math) from student group by sex;--男女平均分分组查询,可以多字段查询
     ```

     ```mysql
     select sex,avg(math) from student where math>70 group by sex; --加入条件限制分组
     ```

   - having

     where 和 having 的区别：

     1. where 在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如不满足结果，则不会被查询。
     2. where 后不可以跟聚合函数，having 可以进行聚合函数的判断

     ```mysql
     select sex,avg(math),count(ip) as p from student where math>70 group by sex having p>2;
     ```

4. 分页查询

   - limit

     ```mysql
     select * from student limit 0,3;--从索引0开始查询往后3条记录
     ```

     开始的索引=（当前的页码 -1）*（每页显示的条数）

     select * from student limit 0,3; ——第1页

     select * from student limit 3,3;——第2页

     select * from student limit 6,3;——第3页

     - [ ] 分页操作是一个MySQL“方言”