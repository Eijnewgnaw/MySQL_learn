#### 操作表

1. C（Create）：创建

   - ```mysqlSQ
     create table 表名(
     
     列名1 数据类型1,
     
     列名2 数据类型2,
     
     .	.	.
     
     列名n 数据类型n)；
     ```

   - 类型举例：

     - [ ] score double(5,2); - -2位小数5位有效数字
     - [ ] date:日期，只包含年月日，YYYY-MM-DD
     - [ ] datetime:日期，包含年月日时分秒 YYYY-MM-DD HH:mm:ss
     - [ ] timestamp:时间戳类型，包含年月日时分秒  YYYY-MM-DD HH:mm:ss（默认系统赋值)
     - [ ] varchar(20):最多可包含20字符的可变长字符串

2. R（Retrieve）：查询

   - 查询某个数据库中所有表的名称

     `show databases;`

   - 查询表结构

     `desc 表名;`

3. U（update）：修改

   - 修改表名

     `alter table 表名 rename 新的表名;`

   - 修改表的字符集

     `alter table 表名 character set 字符集名称;`

   - 添加一列

     `alter table 表名 add 列名 数据类型;`

   - 修改列名称 类型

     `alter table 表名 change 列名 新列名 新数据类型;`

     `alter table 表名 modify 列名 新数据类型;`

4. D（Delete）：删除

   - `drop table 表名;`
   - `drop table if exists 表名;`

