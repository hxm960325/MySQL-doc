# C语言连接MySQL数据库遇到的问题
1. 插入中文数据出现乱码，解决方法如下：
  * 终端命令行切换到MySQL下，执行：mysql -u root -p 回车输入密码
  * 删除数据库，执行：drop stu；
  * show variables like 'character%';
  * set character_set_server=utf8;
  * set character_set_database=utf8;
  * 在add.c中加入mysql_query(db,"set character set utf8");
