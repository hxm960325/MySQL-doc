## 数据库设计

1. 创建数据库
2. 创建六个表:  
 * 学校信息表  
 * 学生信息表   
 * 课程表    
 * 学生成绩表       
 * 教师表     
 * 选课表
##### 学校信息表设计
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|  
| 学校代码 | scid | char(10) |   | 主键，不为空 |  
| 学校名称 | scname | char(10) |   | 不为空 |  
| 院系 | sdept | char(10) |   | 不为空 |  
| 专业 | smajor | char(10) |   | 不为空 |
| 班级 | sclass | char(10) |   | 不为空 | 
##### 创建学校信息表
```mysql
create table school(
scid char(10) not null primary key,
cname char(10) not null,
sdept char(10) not null,
smajor char(10) not null,
sclass char(10) not null
)default charset=utf8;
```
##### 学生信息表设计
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|  
| 学号 | sid | char(12) |   | 主键，不为空 |  
| 姓名 | sname | char(10) |   | 不为空 |  
| 性别 | sex | char(10) |   | 只能选择'男'或'女' |  
| 年龄 | age | smallint | 1 | 只能在1~150之内 |
| 学校代码 | scid | char(10) |   | 外键 |
##### 创建学生信息表
```mysql
create table information(
sid char(12) not null primary key,
sname char(10) not null,
sex char(10) check(sex in('男','女')),
age smallint default '1' check(age in('1','150')),
scid char(10),
foreign key(scid) references school(scid)
)default charset=utf8;
```
##### 课程表
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|  
| 课程号 | cid | char(10) |   | 主键，不为空 |  
| 课程名 | cname | char(10) |   | 不为空 |   
| 学分 | credit | smallint |  | 不为空 |
##### 创建课程表
```mysql
create table course(
cid char(10) not null primary key,
cname char(10) not null,
credit smallint not null
)default charset=utf8;
```
##### 学生成绩表设计
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|  
| 学号 | sid | char(12) |   | 主键，不为空；外键 |  
| 课程号 | cid | char(10) |   | 主键，不为空；外键 |   
| 成绩 | grade | smallint | 0 | 只能在1~100之间 |
##### 创建学生成绩表
```mysql
create table score(
sid char(12) not null,
cid char(10) not null,
grade smallint default '0' check(grade>=0 and grade<=100),
primary key(sid,cid),
foreign key(sid) references information(sid),
foreign key(cid) references course(cid)
)default charset=utf8;
```
##### 教师表
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|
| 教师编号 | tid | char(12) |   | 不为空，主键 |
| 教师姓名 | tname | char(10) |   | 不为空 |
| 教师性别 | tsex | char(10) |   |只能选择‘男’或‘女’ |
##### 创建教师表
```mysql
create table teacher(
tid char(12) not null,
tname char(10) not null,
cid char(10) not null,
tsex char(10) check(sex in('男','女')),
primary key(tid,cid),
foreign key(cid) references course(cid)
)default charset=utf8;
```
##### 选课表
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|
| 学生学号 | sid | char(12) |   | 不为空，主键；外键 |
| 课程号 | cid | char(10) |   | 不为空，主键；外键 |
| 课程名 | cname | char(10) |   | 不为空 |
##### 创建选课表
```mysql
create table sc(
sid char(12) not null,
cid char(10) not null,
cname char(10) not null,
primary key(sid,cid),
foreign key(sid) references information(sid),
foreign key(cid) references course(cid)
)default charset=utf8;
```
3. 创建2个视图： 
 * 学生课程成绩
 * 教师教授的课程
##### 学生课程成绩表设计
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|
| 学生学号 | sid | char(12) |   |   |
| 学生姓名 | sname | char(12) |   |   |
| 课程号 | cid | char(10) |   |   |
| 课程名 | cname | char(10) |   |   |
| 成绩 | grade | smallint |   |   |
##### 创建视图学生课程成绩
```mysql
create view stu_infor(sid,sname,cid,cname,grade)
as
select information.sid,information.sname,course.cid,course.cname,score.grade
from information,course,score
where information.sid=score.sid and course.cid=score.cid;
```
##### 教师教授的课程
| 中文名称 | 表名 | 字段属性 | 默认值 | 备注 |
|---------|-----|---------|--------|-----|
| 教师编号 | tid | char(12) |   |   |
| 课程号 | cid | char(10) |   |   |
| 课程名 | cname | char(10) |   |   |
##### 创建视图教师教授的课程
```mysql
create view tc(tid,cid,cname)
as
select teacher.tid,course.cid,course.cname
from teacher,course
where teacher.cid=course.cid;
```
4. 整体功能设计   
> 学生根据学号登录系统   
>> 查询学生信息
>> 修改学生信息     
>> 查看课程成绩     
>> 查看所选课程      
>> 学生选课

> 教师根据教工号登录系统    
>> 添加学生信息    
>> 查询学生信息    
>> 删除学生信息    
>> 永久删除学生信息    
>> 录入学生成绩    
>> 查看教授课程
