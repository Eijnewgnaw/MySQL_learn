###### 概念：对表中的数据进行限定，保证数据的正确性、有效性、完整性。

###### 分类:

- 主键约束：primary key
- 非空约束：not null
- 唯一约束：unique
- 外键约束：foreign key

1. 非空约束：not null

   ```mysql
   create table stu(
   	id int;
   	name varchar(20) not null;	--创建表时添加约束
   );
   ```

   ```mysql
   alter table stu modify name varchar(20) not null;	--修改表时可添加约束  
   ```

   ```mysql
   alter table stu modify name varchar(20);--修改表时可删除约束
   ```

2. 唯一约束：unique

   - [ ] 唯一可为null，null表示不确定，多个null不重复

   ```mysql
   create table stu(
   	id int,
   	phone_number varchar(20) unique --创建表时添加约束
   );
   ```

   ```mysql
   alter table stu drop index phone_number;--删除唯一约束
   ```

   ```mysql
   alter table stu modify phone_number varchar(20) unique;--修改表时添加约束
   ```

3. 主键约束：primary key

   - [ ] 含义：非空且唯一
   - [ ] 一张表只能一个主键，主键是表中记录的唯一标识

   ```mysql
   create table stu(
   	id int primary key,
   	name varchar(20)
   );	--创建表时添加主键约束
   ```

   ```mysql
   alter table stu drop primary key;	--删除约束
   ```

   ```mysql
   alter table stu modify id int primary key;	--修改表时添加约束
   ```

   - [ ] 自动增长：如果某一列是数值类型的，使用auto_increase可以完成值的自动增长
   - [ ] 自动增长是根据上一条记录增长的

   ```mysql
   create table stu(
   	id int primary key auto_increment,
   	name varchar(20)
   );	--给id添加主键约束
   ```

   ```mysql
   alter table stu modify id int;	--删除自动增长
   ```

   ```mysql
   alter table stu modify id int auto_increase;--添加自动增长
   ```

4. 外键约束：foregin key

   - [ ] 外键列创建格式：constraint 外键名称 foreign key 外键名称 references 主表名称(主表列名称)
   - [ ] 外键让表与表产生关系，保证数据正确性
   - [ ] 外键值可以为null，不可以为不存在的外键值

   ```mysql
   create table stu(
   	id int primary key auto_increment,
   	name varchar(20),
   	tea_id int,	--设置当前表外键列，命名对应主键
   	constraint stu_tea_fk foreign (tea_id) reference teacher(id)
   );
   ```

   - [ ] stu_tea_fk:外键名称自取，没有实际意义
   - [ ] tea_id:外键名称，在本张表中对应的字段，显示这是外键
   - [ ] teacher:另一张表
   - [ ] teacher(id)：关联的是teacher表的id列（一般为主键列）
   - [ ] 在关联之前要确认关联的表已经创立好 
   - [ ] 外键名称可以不注明，由系统自己创建（创建外键从”foreign“开始）

   ```mysql
   alter table stu drop foreign key stu_tea_fk;--删除外键
   ```

   ```mysql
   alter table stu add comstraint stu_tea_fk foreign key(tea_id) references tea;--添加外键
   ```

5. 级联操作

   ```mysql
   constraint stu_tea_fk foreign (tea_id) reference teacher(id) on cascade on delete cascade;
   ```

   - [ ] on cascade级联更新后，外键自动同步
   - [ ] on delete cascade级联删除
   - [ ] 多重关联不建议级联操作

