###### 事务

1. 概念：

   如果一个包含多个步骤的操作被事务管理，这个操作要么同时成功，要么同时失败

   - 开启事务：start transaction;
   - 回滚：rollback;    ——出现异常
   - 提交：commit

   mysql 数据库中事务默认自动提交

   oracle数据库中事务默认手动提交

   查看事务默认提交方式:

   ```mysql
   select @@autocommit; --一般1代表自动提交 0代表手动提交
   ```

   修改事务默认提交方式：

   ```mysql
   set @@autocommit = 0; --默认手动提交
   ```

2. 事务四大特征

   - 原子性：是不可分割的最小操作单位，要么同时成功，要				么同时失败
   - 持久性:事务提交或回滚后，数据库会持久化的保存数据
   - 隔离性：多个事务之间，相互独立
   - 一致性：事务操作前后，数据总量不变

3. 事务的隔离级别（了解）

   多个事务之间本身相互隔离，相互独立。但如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别。

   - [ ] **访问问题**：
   
   - **脏读**：一个事务读到了另一个事务未提交的数据.
   - **虚读（不可重复读）**：一个事务读到了另一个事务已经提交(update)的数据。引发另一个事务，在事务中的多次查询结果不一致。
   - **虚读 /幻读**：一个事务读到了另一个事务已经提交(insert)的数据。导致另一个事务，在事务中多次查询的结果不一致。
   
   - [ ] **隔离级别：解决问题**
   
     数据库规范规定了4种隔离级别，分别用于描述两个事务并发的所有情况。
   
     1. **read uncommitted：读未提交**，一个事务读到另一个事务没有提交的数据。
        a)存在：3个问题（脏读、不可重复读、虚读）。
        b)解决：0个问题
     2. **read committed ：读已提交**，一个事务读到另一个事务已经提交的数据。
        a)存在：2个问题（不可重复读、虚读）。
        b)解决：1个问题（脏读）
     3. **repeatable read：可重复读**，在一个事务中读到的数据始终保持一致，无论另一个事务是否提交。
        a)存在：1个问题（虚读）。
        b)解决：2个问题（脏读、不可重复读）
     4. **serializable：串行化**，同时只能执行一个事务，相当于事务中的单线程。
        a)存在：0个问题。
        b)解决：3个问题（脏读、不可重复读、虚读）
   
     **安全和性能对比
     安全性**：
     serializable(**8**) > repeatable read(**4**) > read committed(**2**) > read uncommitted(**1**)
     **性能**：
     serializable < repeatable read < read committed < read uncommitted
     常见数据库的默认隔离级别：
     **MySql：repeatable read
     Oracle：read committed**
   
4. 设置数据库隔离级别

   - 查询数据库隔离级别

     ```mysql
     show variables like '%isolation%';
     或select @@tx_isolation;
     ```

   - 设置数据库的隔离级别

     sql语句设置

     ```mysql
     set session transactionisolation level 级别字符串
     ```

     ```mysql
     set global transaction isolation level repeatable read;
     ```

     java程序设置
     在**Connection接口**中，有设置事务隔离级别的方法：
     `void setTransactionIsolation(int level)` 尝试将此 Connection对象的事务隔离级别更改为给定的对象。

     ```java
     conn.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);
     ```

     

