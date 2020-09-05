###### 管理用户，授权

1. 查询用户：

   ```mysql
   use mysql;				--切换到mysql数据库
   select * from user;		--查询user表
   ```

   通配符：%表示可以在任意主机使用用户登录数据库

2. 创建用户

   ```mysql
   creat user '用户名'@'主机名'isentified by '密码';
   ```

3. 删除用户

   ```mysql
   drop user '用户名'@'主机名';
   ```

4. 修改用户密码

   ```mysql
   update user password = password('新密码') where user = '用户名';		--sql语句形式
   ```

   ```mysql
   set password for '用户名'@'主机名'  = password('新密码');
   ```

   一般情况下用root用户改别人的密码

   如果：**root密码忘了！！**

   1. cmd->net stop mysql 停止mysql服务
   2. mysqld - -skip-grant-tables
   3. 开新窗口，mysql回车直接登录
   4. 改密码，关闭两个窗口
   5. 任务管理器关闭mysqld 进程
   6. 正常启动服务，通过新的密码登录

5. 权限管理

   1. 查询权限：

      ```mysql
      show grants for '用户名'@'主机名';
      ```

   2. 授予权限

      ```mysql
      grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';
      ```

      all  ——所有权限

      "*"——所有库所有表("星点星")

   3. 撤销权限

      ```mysql
      revoke 权限列表  on 数据库名.表名 from'用户名'@'主机名';
      ```

      

