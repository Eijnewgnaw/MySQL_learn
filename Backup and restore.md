1. 命令行：

   备份:

   ```mysql
   mysqldump -u用户名 -p密码 数据库名称 > 保存路径
   ```

   ```mysql
   mysqldump -uroot -p123 db1 > d:\\a.sql;
   ```

   还原:

   1. 登录数据库	`mysql -uroot -p123;`
   2. 创建数据库    `create database db1;`
   3. 使用数据库    `use db1;`
   4. 执行文件。	source 文件路径    `source d:\\a.sql;`

2. 图像工具

   备份：导出

   还原：执行sql脚本

