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
   
