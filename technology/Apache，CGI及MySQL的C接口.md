# Apache，CGI及MySQL的C接口
### atom下载安装
1. 在虚拟机的浏览器中打开www.atom.io，选择other platforms，列表中找到atom.amd64.deb，复制地址连接，在虚拟机终端执行wget -c atom.amd64.deb的地址
2. 在搜索栏搜索atom，进入atom下载atom editor环境使用的插件
### Apache安装
1. sudo apt-get update
2. sudo apt-get install tasksel
3. sudo tasksel
### CGI
1. Apache中开启cgi支持，执行：sudo ln -s /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/cgi.load
2. 重启Apache服务器，执行：service apache2 restart
3. 需要运行的cgi文件的存放路径，执行：sudo /usr/lib/cgi-bin
4. 修改目录权限，执行：
   * sudo mkdir /usr/lib/cgi-bin/sx
   * sudo chmod 777 /usr/lib/cgi-bin/sx
5. 安装MySQL的C语言库
   * 切换到根目录，更新源sudo apt-get update
   * 进行安装，执行：sudo apt-get install libmysqlclient-dev
### atom代码导入以及连接数据库
1. 进入nts.newbieol.com实训，在资料中下载压缩包cgi-stu
2. 解压压缩包cgi-stu，将cgi-stu文件夹拷贝到github下，执行如下命令：
   * 切换到根目录，执行cd
   * 切换到github文件夹，执行cd github
   * 切换到cgi-stu文件夹，执行：cd cgi-stu
   * 进入atom，执行atom .
   * 初始化仓库：git init
   * 创建.gitignore，执行：touch .gitignore
   * 查看状态，执行：git status
   * 将所有文件添加关注，执行：git add .
   * 将修改信息提交，执行：git commit -a -m "init commit"
   * 查看所有提交：git log
   * 切换路径，执行：cd /var/www/html
   * ls查看目录，执行：pwd
   * 回到浏览器在网址栏打开localhost，进入学生管理系统
   * 执行cd -切换回到上级目录
   * 进入stu，执行：cd stu/
   * 复制到atom，执行：cp -r public/ index.html /var/www/html
   * 修改Makefile，在atom中打开Makefile，在最后添加install:，回车Tab键cp *.cgi /usr/lib/cgi-bin/sx
   * 执行make，修改warning，在atom中打开add.c、sel.c、del.c、mod.c，修改数据库名称以及密码，在警告行修改为return -1；
   * 再次执行make，所有警告都没有了，此时进行提交。
   * 执行：make install，将cgi拷贝到/usr/lib/cgi-bin/sx
3. 回到浏览器进行测试，进入localhost学生管理系统，进行增删改查均成功。
4. 获取表单数据   
```c
cgiFormResultType   cgiFormString(char *name, char *result, int max);
参数：  name, 指定要获取的表单项的名字
       result,将获得的数据存储到result中
       max， 指定最多读取的字符个数
```
5. fprintf函数
``` c
int fprintf(FILE *stream, const char *format, ...);
//功能： 将格式化的语句输出到指定的流
fprintf(stdin, "helloworld\n")  
//等价于 printf("helloworld\n);
```
6. atoi函数
```c
int atoi(const char *nptr);
//功能：将一个字符串转换成对应的数字，比如：“1234” ==》 1234
```
7. 接口介绍
```c
MYSQL *mysql_init(MYSQL *mysql)
//功能：初始化函数，参数为NULL即可，接收返回值。
//失败，NULL
```

```c
MYSQL *mysql_real_connect(MYSQL *mysql, const char *host, const char *user, const char *passwd, const char *db, unsigned int port, const char *unix_socket, unsigned long client_flag)
//功能：连接mysql服务器
//失败，NULL
```

```c
void mysql_close(MYSQL *mysql)
//功能：关闭服务器连接
```

```c
int mysql_real_query(MYSQL *mysql, const char *stmt_str, unsigned long length)
//功能：执行sql语句，sql语句不能以“；”结尾
//成功，0
//失败， 非0
```

```c
int mysql_query(MYSQL *mysql, const char *stmt_str)
//功能：执行sql语句，sql语句不能以“；”结尾
```

```c
void mysql_free_result(MYSQL_RES *result)
//功能：释放空间
```
