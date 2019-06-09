## manjaro 安装MySQL 8.*

1. > sudo pacman -S mysql 

2. 初始化MySQL

   > ```bash
   > sudo mysqld --initialize --user=mysql --basedir=/usr --datadir=/var/lib/mysql
   > ```
   >
   > 如果成功,出现以下信息
   >
   > ```bash
   > 2019-04-20T07:26:57.102370Z 0 [Warning] [MY-010915] [Server] 'NO_ZERO_DATE', 'NO_ZERO_IN_DATE' and 'ERROR_FOR_DIVISION_BY_ZERO' sql modes should be used with strict mode. They will be merged with strict mode in a future release.
   > 2019-04-20T07:26:57.102435Z 0 [System] [MY-013169] [Server] /usr/bin/mysqld (mysqld 8.0.15) initializing of server in progress as process 8658
   > 2019-04-20T07:26:59.145584Z 5 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: Wh-ikE;;I1Fl
   > 2019-04-20T07:27:00.000278Z 0 [System] [MY-013170] [Server] /usr/bin/mysqld (mysqld 8.0.15) initializing of server has completed
   > 
   > ```
   >
   > 在`root@localhost: Wh-ikE;;I1Fl`中, `Wh-ikE;;I1Fl为`初始密码

3. 连接数据库

   > mysql  -u root -p

   按照提示输入密码即可

4. 修改密码:在连接上MySQL之后输入:

   ```sql
   ALTER user 'root'@'localhost' IDENTIFIED BY 'New Passwd'
   ```

   

Enjoy it !