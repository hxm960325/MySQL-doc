# Git简介
> GIT 是一个分布式版本控制软件,最初目的是为更好地管理Linux内核开发而设计,是目前世界上最先进的分布式版本控制系统。
# 安装Git
1. 执行命令：sudo apt-get install git
2. 执行命令：git clone https://github.com/wangleihd
# Git的使用
1. 创建版本库   
  > 先创建一个目录，用来存放仓库  
  >> 创建目录：mkdir 目录名  
  >> 切换到该目录：cd 目录名
  
  > 初始化仓库  
  >> 初始化：git init  
  >> 提示初始化成功，存在一个空的仓库：Initialized empty Git repository in /home/user/目录名/.git/ 
  
  > 查看创建状态  
  >> 查看当前所有文件：ls -al  
  >> 存在.git文件，创建成功
2. 提交文件到仓库    
  > 增加文件  
  >> 先在目录里创建一个文件： touch 文件名  
  >> 编辑文件： vim 文件名  
  >> 按Esc切换到命令行，wq保存退出  
  >> 查看当前目录文件的状态： git status  
  >> 将文件添加关注，加入仓库中：git add 文件名  
  >> 再次查看状态时，文件已经被关注  
  >> 提交到仓库：git commit,此时编辑提交的状态，按Ctrl+x，y+enter退出保存  
  >> 查看所有提交状态：git log  
  
  > 在第一次提交时，要配置用户信息，执行如下命令：  
  >> git config --global user.name，填写github用户名  
  >> git config --global user.email，填写github用户邮箱  
  >> git config --global core.editor vim，配置提交时的编辑器  
3. 基本命令
  > 删除文件恢复  
  >> 删除文件：rm 文件名 
  >> 此时查看文件状态：git status  
  >> 恢复文件：git checkout 文件名  
  >> 查看当前目录文件的状态： git status  
  >> 查看文件是否存在：ls -al   
  
  > 版本回退，即每次修改后提交到仓库的版本，回退到某一版本  
  >> 版本回退：git reset --hard commitID 
  >> 此时查看版本信息：git log，不会看到所有的信息，没有了回退版本的信息 
  >> 查看最后一次提交信息：git reflog 
4. 从仓库中删除文件
  > 执行git rm 文件名  
  > 提交到仓库：git commit  
5. 从仓库中忽略文件，执行：touch .gitignore
6. 版本之间对比
  > git diff  
 git diff commitID1 commitID2  
7. 打patch
  > 查看所有提交信息：git log，看共有几次提交  
 git生成patch：git format-patch -p5，假设有5次提交    
 git打patch：git am patch-name  
