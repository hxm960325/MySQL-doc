# MySQL安装与配置
### MySQL介绍
MySQL是一个关系型数据库管理系统，是最流行的关系型数据库管理系统之一。在WEB应用方面，MySQL是最好的RDMS应用软件。
MySQL是一种关系数据库管理系统，关系数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。 
MySQL所使用的 SQL 语言是用于访问数据库的最常用标准化语言。
MySQL是开源的，支持大型的数据库，允许于多个系统上，并且支持多种语言。
### MySQL安装配置
1. 更新源
   * 用vim打开源列表文件，使用命令：sudo vim /etc/apt/sources.list
   * 将以下源码粘贴到源列表里：   
   deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse   
   deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse   
   deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse   
   deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse   
   `##` 测试版源   
   deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
   `#`  源码   
   deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse   
   deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse   
   deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse   
   deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse 
   `##` 测试版源   
   deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse   
   `#` Canonical 合作伙伴和附加   
   deb http://archive.canonical.com/ubuntu/ xenial partner   
   deb http://extras.ubuntu.com/ubuntu/ xenial main
2. Ubuntu安装MySQL  
   1. 执行sudo apt-get update      
   2. 执行sudo apt-get install tasksel      
   3. 执行sudo tasksel   
   
   
