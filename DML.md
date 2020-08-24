#### 修改数据

1. 添加数据

   ```mysql
   insert into 表名(列名1,列名2,...,列名n)values(值1,值2,...,值n);
   ```

   - 如果表名后不定义列名，则默认给所有列添加值

2. 删除数据

   ```mysql
   delete from 表名 where 条件;
   ```

   - 如：

     ```mysql
     delete from stu where id=1;
     ```

   - 不给`where 条件`就会挨条全部删除（不推荐）

   ```mysql
   truncate table 表名;
   ```

   - 删除表，然后再创建一个一模一样的空表

3. 修改数据

   ```mysql
   update 表名 set 列名1=值1,列名2=值2,...,where 条件;
   ```

   - 如：

     ```mysql
     update stu set age = 17 where id=3, score = 100 where id=2;
     ```

   - 不给`where 条件`就会挨条全部修改

