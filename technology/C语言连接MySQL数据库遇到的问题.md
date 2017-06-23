# C语言连接MySQL数据库遇到的问题
1. 在配置MySQL时，修改代码鼠标不能粘贴，解决方法如下：  
  * 切换到根目录，执行命令：cd
  * 执行命令：vim .vimrc
  * 将第18行删除，保存退出    
2. 插入中文数据出现乱码，解决方法如下：
  * 终端命令行切换到MySQL下，执行：mysql -u root -p 回车输入密码
  * 删除数据库，执行：drop stu；
  * show variables like 'character%';
  * set character_set_server=utf8;
  * set character_set_database=utf8;
  * 在add.c中加入mysql_query(db,"set character set utf8");
3. 在写HTML文件时，按钮切换不能使用，在同学的帮助下得以解决，解决方法如下：
  * 将自己创建的HTML最开始的链接修改为如下语句：
```html
<link href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
```
  * 将自己创建的HTML文件最后的script修改为如下语句：
```html
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/3.3.7/bootstrap.min.js"></script>
```
4. 在学生及老师的功能中，修改与删除学生信息出现该学生不存在数据库中也可以修改删除，解决方法：
> 在c程序中在修改与删除的.c文件中连接数据库后，先进行查询，然后再判断该学生是否在数据库中，如果存在则可以操作，不存在则输出提示信息
```c
//连接数据库
	db = mysql_real_connect(db, "127.0.0.1", "root", "123456", "stu",  3306, NULL, 0);
	if (db == NULL)
	{
		fprintf(cgiOut,"mysql_real_connect fail:%s\n", mysql_error(db));
		mysql_close(db);
		return -1;
	}
	sprintf(sql, "select * from information where sid='%s' ",sid);
	if ((ret = mysql_real_query(db, sql, strlen(sql) + 1)) != 0)
	{
		fprintf(cgiOut,"mysql_real_query fail:%s\n", mysql_error(db));
		mysql_close(db);
		return -1;
	}
	MYSQL_RES *res;
	res = mysql_store_result(db);
	if (res == NULL)
	{
		fprintf(cgiOut,"mysql_store_result fail:%s\n", mysql_error(db));
		return -1;
	}
	int num = (int)res->row_count;
	if(num){
		sprintf(sql, "update information set sname='%s', sex='%s', age= %d, scid='%s' where sid = '%s'",sname, sex, atoi(age), scid, sid);
		if ((ret = mysql_real_query(db, sql, strlen(sql) + 1)) != 0)
		{
			fprintf(cgiOut,"mysql_real_query fail:%s\n", mysql_error(db));
			mysql_close(db);
			return -1;
		}
		fprintf(cgiOut, "修改学生信息成功！\n");
	}else{
		fprintf(cgiOut, "该学生不存在\n");
	}
```
5. 对于学生信息的删除操作（真删假删），作如下解决：
> 在学生信息表information中增加一个状态位statu，默认值为1.当statu=1时，该学生的信息在查询时可以查看，当statu=0时，该学生信息在查询时不能显示
>> 真删除：执行删除操作，根据学生学号删除，从数据库彻底删除该学生的信息
```c
sprintf(sql, "delete from information where sid='%s'",sid);
```
>> 假删除：执行修改操作，将statu的直修改为0，该学生信息还存在于数据库
```c
sprintf(sql, "update information set statu=0 where sid='%s'",sid);
```
