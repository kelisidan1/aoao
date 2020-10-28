

# MySQL

## 名词

**DB** :

​		DataBase(数据库，在硬盘上，以文件的形式存在)

**DBMS**：

​		DataBase Management System(数据库管理系统，常见的:MySQL  Oracle  DB2..)

**SQL**:

​	结构化查询语句，是一门标准通用的语言。标准的sql适合于所有的数据库产品

​	

## 什么是表？

​	表是数据库的基本组成单元，所有的数据都以表格的形式组织，目的是可读性强。

​	一个表包括行 和 列

​			行：数据/记录

​			列：字段

数据库当中的	String = varchar

​					 	 long = bigint

## SQL语句分类

+ DQL：Data Query Language   数据查询语言
+ DML：Data Manipulation Language 数据操作语言
+ DDL：Data Definition Language  数据定义语言
+ TCL：Transaction Control Language  事务控制语言
+ DCL：Data Control Language数据控制语言

## mysql 语句：

​	他是区别于sql语句的，mysql是管理系统。

	### 例子
	
	1. show databases;  (展示我有哪些数据库)
 	2. create database aombase; (建立一个数据库,名字就叫做aombase)
 	3. use aombase;(使用这个数据库，会进入数据库当中，可以进行进一步的操作)

####               进入数据库之后的操作

+ show tables;(展示表)

+ source   以.sql结尾的文件的路径    这样可以导入sql脚本(可以自动完成一大堆的操作)

  

+ 删除数据库：drop [name of database];

+ 查看表结构：desc [name of tables];

  ``` mysql
  mysql> show tables;
  +-------------------+
  | Tables_in_aombase |
  +-------------------+
  | dept              |
  | emp               |
  | salgrade          |
  +-------------------+
  3 rows in set (0.01 sec)
  
  mysql> desc dept;
  +--------+-------------+------+-----+---------+-------+
  | Field  | Type        | Null | Key | Default | Extra |
  +--------+-------------+------+-----+---------+-------+
  | DEPTNO | int         | NO   | PRI | NULL    |       |		部门编号
  | DNAME  | varchar(14) | YES  |     | NULL    |       |		部门名字
  | LOC    | varchar(13) | YES  |     | NULL    |       |		部门位置
  +--------+-------------+------+-----+---------+-------+
  3 rows in set (0.10 sec)
  
  mysql> desc emp;
  +----------+-------------+------+-----+---------+-------+
  | Field    | Type        | Null | Key | Default | Extra |
  +----------+-------------+------+-----+---------+-------+
  | EMPNO    | int         | NO   | PRI | NULL    |       |	员工编号
  | ENAME    | varchar(10) | YES  |     | NULL    |       |	员工姓名
  | JOB      | varchar(9)  | YES  |     | NULL    |       |	工作岗位
  | MGR      | int         | YES  |     | NULL    |       |	上级领导编号
  | HIREDATE | date        | YES  |     | NULL    |       | 	入职日期
  | SAL      | double(7,2) | YES  |     | NULL    |       |	月薪
  | COMM     | double(7,2) | YES  |     | NULL    |       |	补助
  | DEPTNO   | int         | YES  |     | NULL    |       |	部门编号
  +----------+-------------+------+-----+---------+-------+
  8 rows in set (0.01 sec)
  
  mysql> desc salgrade;
  +-------+------+------+-----+---------+-------+
  | Field | Type | Null | Key | Default | Extra |
  +-------+------+------+-----+---------+-------+
  | GRADE | int  | YES  |     | NULL    |       |	等级
  | LOSAL | int  | YES  |     | NULL    |       |	最低薪资
  | HISAL | int  | YES  |     | NULL    |       | 最高薪资
  +-------+------+------+-----+---------+-------+
  
  ```

  

4. 查看表

``` mysql
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```



5. select version();      查看版本号

6. exit；    退出

7. \c    结束一条语句

8. show create table emp;

9. 简单的查询语句(DQL)

   ​	语法格式：

   ​		select 字段名1，字段名2，字段名3，。。。from 表名    

``` mysql
mysql> select JOB from emp;
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| SALESMAN  |
| MANAGER   |
| SALESMAN  |
| MANAGER   |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
| SALESMAN  |
| CLERK     |
| CLERK     |
| ANALYST   |
| CLERK     |
+-----------+
```

​		mysql> select ename,sal * 12 as yearsal from emp;

解释：select ename   选择 ename字段的数据

​		   sal  月薪        sal * 12   年薪       as yearsal   起了个名字   叫yearsal    from emp   从emp表中拿出的

注意：字符串如果是中文，需要用**单引号**引上!!!!!!

​	

```mysql 
mysql> select ename,sal * 12 as yearsal from emp;
+--------+----------+
| ename  | yearsal  |
+--------+----------+
| SMITH  |  9600.00 |
| ALLEN  | 19200.00 |
| WARD   | 15000.00 |
| JONES  | 35700.00 |
| MARTIN | 15000.00 |
| BLAKE  | 34200.00 |
| CLARK  | 29400.00 |
| SCOTT  | 36000.00 |
| KING   | 60000.00 |
| TURNER | 18000.00 |
| ADAMS  | 13200.00 |
| JAMES  | 11400.00 |
| FORD   | 36000.00 |
| MILLER | 15600.00 |
+--------+----------+

mysql> select ename,sal * 12 as '年薪' from emp;
+--------+----------+
| ename  | 年薪     |
+--------+----------+
| SMITH  |  9600.00 |
| ALLEN  | 19200.00 |
| WARD   | 15000.00 |
| JONES  | 35700.00 |
| MARTIN | 15000.00 |
| BLAKE  | 34200.00 |
| CLARK  | 29400.00 |
| SCOTT  | 36000.00 |
| KING   | 60000.00 |
| TURNER | 18000.00 |
| ADAMS  | 13200.00 |
| JAMES  | 11400.00 |
| FORD   | 36000.00 |
| MILLER | 15600.00 |
+--------+----------+

as  其实是可以省略的

mysql> select ename,sal * 12 '年薪' from emp;
+--------+----------+
| ename  | 年薪     |
+--------+----------+
| SMITH  |  9600.00 |
| ALLEN  | 19200.00 |
| WARD   | 15000.00 |
| JONES  | 35700.00 |
| MARTIN | 15000.00 |
| BLAKE  | 34200.00 |
| CLARK  | 29400.00 |
| SCOTT  | 36000.00 |
| KING   | 60000.00 |
| TURNER | 18000.00 |
| ADAMS  | 13200.00 |
| JAMES  | 11400.00 |
| FORD   | 36000.00 |
| MILLER | 15600.00 |
+--------+----------+
```



9. 查询所有字段？

   select * from emp;   //平时用可以，但是开发的时候不能使用.

10. 条件查询

    ​	语法格式

    + select		字段，字段。。。

      ​	from		表名

      ​		where    条件;

```mysql
mysql> select ename from emp where sal = 5000;
+-------+
| ename |
+-------+
| KING  |
+-------+
				大于等于等于查询
mysql> select job,ename from emp where sal >=1000;
+-----------+--------+
| job       | ename  |
+-----------+--------+
| SALESMAN  | ALLEN  |
| SALESMAN  | WARD   |
| MANAGER   | JONES  |
| SALESMAN  | MARTIN |
| MANAGER   | BLAKE  |
| MANAGER   | CLARK  |
| ANALYST   | SCOTT  |
| PRESIDENT | KING   |
| SALESMAN  | TURNER |
| CLERK     | ADAMS  |
| ANALYST   | FORD   |
| CLERK     | MILLER |
+-----------+--------+

				不等于查询      <>
mysql> select job,ename from emp where sal <> 1000;
+-----------+--------+
| job       | ename  |
+-----------+--------+
| CLERK     | SMITH  |
| SALESMAN  | ALLEN  |
| SALESMAN  | WARD   |
| MANAGER   | JONES  |
| SALESMAN  | MARTIN |
| MANAGER   | BLAKE  |
| MANAGER   | CLARK  |
| ANALYST   | SCOTT  |
| PRESIDENT | KING   |
| SALESMAN  | TURNER |
| CLERK     | ADAMS  |
| CLERK     | JAMES  |
| ANALYST   | FORD   |
| CLERK     | MILLER |
+-----------+--------+

				固定范围内的查找		
底下的这个句子，还能写成
mysql> select job,ename from emp where sal between 1000 and 3000;
mysql> select job,ename from emp where sal >= 1000 and sal<=3000;
+----------+--------+
| job      | ename  |
+----------+--------+
| SALESMAN | ALLEN  |
| SALESMAN | WARD   |
| MANAGER  | JONES  |
| SALESMAN | MARTIN |
| MANAGER  | BLAKE  |
| MANAGER  | CLARK  |
| ANALYST  | SCOTT  |
| SALESMAN | TURNER |
| CLERK    | ADAMS  |
| ANALYST  | FORD   |
| CLERK    | MILLER |
+----------+--------+

				(非)空值的查询（特殊）     使用   is NULL(is not NULL)语句
mysql> select ENAME,COMM,SAL from emp where COMM is NULL;
+--------+------+---------+
| ENAME  | COMM | SAL     |
+--------+------+---------+
| SMITH  | NULL |  800.00 |
| JONES  | NULL | 2975.00 |
| BLAKE  | NULL | 2850.00 |
| CLARK  | NULL | 2450.00 |
| SCOTT  | NULL | 3000.00 |
| KING   | NULL | 5000.00 |
| ADAMS  | NULL | 1100.00 |
| JAMES  | NULL |  950.00 |
| FORD   | NULL | 3000.00 |
| MILLER | NULL | 1300.00 |
+--------+------+---------+ 

		and 和 or 联合起来使用： 找出薪资大于1000的并且部门的编号是20或30部门的员工
				
mysql> select ename,comm,sal from emp where sal>1000 and (deptno=20 or deptno=30);
+--------+---------+---------+
| ename  | comm    | sal     |
+--------+---------+---------+
| ALLEN  |  300.00 | 1600.00 |
| WARD   |  500.00 | 1250.00 |
| JONES  |    NULL | 2975.00 |
| MARTIN | 1400.00 | 1250.00 |
| BLAKE  |    NULL | 2850.00 |
| SCOTT  |    NULL | 3000.00 |
| TURNER |    0.00 | 1500.00 |
| ADAMS  |    NULL | 1100.00 |
| FORD   |    NULL | 3000.00 |
+--------+---------+---------+

				in 等同于 or:			括号当中写的东西
										就相当于   deptno = 20  或者   deptno = 30
												而不是说我的deptno是在20到30之间的数字
mysql> select ename,comm,sal from emp where sal>1000 and deptno in(20,30);
+--------+---------+---------+
| ename  | comm    | sal     |
+--------+---------+---------+
| ALLEN  |  300.00 | 1600.00 |
| WARD   |  500.00 | 1250.00 |
| JONES  |    NULL | 2975.00 |
| MARTIN | 1400.00 | 1250.00 |
| BLAKE  |    NULL | 2850.00 |
| SCOTT  |    NULL | 3000.00 |
| TURNER |    0.00 | 1500.00 |
| ADAMS  |    NULL | 1100.00 |
| FORD   |    NULL | 3000.00 |
+--------+---------+---------+

			模糊查询   like
			必须掌握两个特殊的符号     %      					_
								任意多个字符				任意一个字符
mysql> select ename from emp where ename like '%o%';
+-------+
| ename |
+-------+
| JONES |
| SCOTT |
| FORD  |
+-------+

			找出第二个字母是A的

mysql> select ename from emp where ename like '_a%';
+--------+
| ename  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+

			找出名字当中带有下划线的_			加转义字符
			
			
```

11、排序

| 升序 | 降序 |
| :--: | :--: |
| asc  | desc |

​		语法： select ename , sal from emp **order by** sal;

```mys
						//按照sal的大小，升序排列（默认）
mysql> select ename,sal from emp order by sal;
+--------+---------+
| ename  | sal     |
+--------+---------+
| SMITH  |  800.00 |
| JAMES  |  950.00 |
| ADAMS  | 1100.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
| MILLER | 1300.00 |
| TURNER | 1500.00 |
| ALLEN  | 1600.00 |
| CLARK  | 2450.00 |
| BLAKE  | 2850.00 |
| JONES  | 2975.00 |
| SCOTT  | 3000.00 |
| FORD   | 3000.00 |
| KING   | 5000.00 |
+--------+---------+

				//按照sal的大小，降序排列
mysql> select ename,sal from emp order by sal desc;
+--------+---------+
| ename  | sal     |
+--------+---------+
| KING   | 5000.00 |
| SCOTT  | 3000.00 |
| FORD   | 3000.00 |
| JONES  | 2975.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| MILLER | 1300.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| SMITH  |  800.00 |
+--------+---------+
14 rows in set (0.00 sec)
				//当薪资相同的时候，就按照名字来进行排序
mysql> select ename,sal from emp order by sal desc,ename asc;
+--------+---------+
| ename  | sal     |
+--------+---------+
| KING   | 5000.00 |
| FORD   | 3000.00 |
| SCOTT  | 3000.00 |
| JONES  | 2975.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| MILLER | 1300.00 |
| MARTIN | 1250.00 |
| WARD   | 1250.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| SMITH  |  800.00 |
+--------+---------+

select ename,job,sal from emp where job = 'salesman' order by sal desc;
	
	+--------+----------+---------+
    | ename  | job      | sal     |
    +--------+----------+---------+
    | ALLEN  | SALESMAN | 1600.00 |
    | TURNER | SALESMAN | 1500.00 |
    | WARD   | SALESMAN | 1250.00 |
    | MARTIN | SALESMAN | 1250.00 |
    +--------+----------+---------+
```

---



12. 分组函数

+ count 
+ sum
+ avg
+ max
+ min

```my
                                                求薪资的总额
mysql> select sum(sal) as salary from emp;
+----------+
| salary   |
+----------+
| 29025.00 |
+----------+

mysql> select avg(sal) as salary from emp;
+-------------+
| salary      |
+-------------+
| 2073.214286 |
+-------------+
1 row in set (0.00 sec)

mysql> select count(sal) as salary from emp;
+--------+
| salary |
+--------+
|     14 |
+--------+
1 row in set (0.00 sec)

mysql> select min(sal) as salary from emp;
+--------+
| salary |
+--------+
| 800.00 |
+--------+

```

注意：	

​		分组函数不可直接使用在where子句当中

count(*)和count(comm)区别

​	*是总的纪录条数

​	字段是统计不为空的字段的个数

---



13. group by 和 having

    ​		group by : 按照某个字段或者某些字段进行分组

    ​		having : 对分组之后的数据进行再次过滤

    ​				案例：找出每个工作岗位的最高薪资

    ​				select max(sal) from emp group by job;

    ​						这句话的执行顺序：1、from emp

    ​														2、group by job

    ​														3、select max

    ​				

    ​	先进行分组（按照工作岗位），然后进行查找

    ```mysql
    mysql> select max(sal) from emp group by job;
    +----------+
    | max(sal) |
    +----------+
    |  1300.00 |
    |  1600.00 |
    |  2975.00 |
    |  3000.00 |
    |  5000.00 |
    +----------+
    ```

    

    + 注意：分组函数一般都会和group by 一起联合使用。

    + 案例:找出工资高于平均值的员工

      ```mysql
      mysql> select ename,job,sal from emp where sal > (select avg(sal) from emp);
      +-------+-----------+---------+
      | ename | job       | sal     |
      +-------+-----------+---------+
      | JONES | MANAGER   | 2975.00 |
      | BLAKE | MANAGER   | 2850.00 |
      | CLARK | MANAGER   | 2450.00 |
      | SCOTT | ANALYST   | 3000.00 |
      | KING  | PRESIDENT | 5000.00 |
      | FORD  | ANALYST   | 3000.00 |
      +-------+-----------+---------+
      ```

      

14. sql语句的执行顺序

    select

    ​	...	5

    from

    ​	...	1

    where

    ​	...	2

    group by

    ​	....	3

    having

    ​	...	4

    order by

    ​	....	6

15. **group by 需要注意的地方**

    当使用group by 的时候，select 后边只能够跟上参加分组的那个字段，添加其他的之后，展示出来的表格没有任何的意义。

    ​																		why?

    ```mysql
    mysql> select ename,max(sal),job from emp group by job;
    +-------+----------+-----------+
    | ename | max(sal) | job       |
    +-------+----------+-----------+
    | SMITH |  1300.00 | CLERK     |
    | ALLEN |  1600.00 | SALESMAN  |
    | JONES |  2975.00 | MANAGER   |
    | SCOTT |  3000.00 | ANALYST   |
    | KING  |  5000.00 | PRESIDENT |
    +-------+----------+-----------+
    5 rows in set (0.00 sec)
    
    mysql> select * from emp;
    +-------+--------+-----------+------+------------+---------+---------+--------+
    | EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
    +-------+--------+-----------+------+------------+---------+---------+--------+
    |  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
    |  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
    |  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
    |  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
    |  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
    |  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
    |  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
    |  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
    |  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
    |  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
    |  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
    |  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
    |  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
    |  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
    +-------+--------+-----------+------+------------+---------+---------+--------+
    ```

    底下的这张表毫无疑问是正确的，但是对照上边的表，ename是随机生成的，就是因为select 后边只能够加上参与分组的那些个字段。

**记住一个规则**：当一条语句当中有group by 的话， select 后边只能跟上分组函数和参与分组的字段

16. 多个字段能不能联合起来一块分组？(where    having   group by)

    **案例：**找出每个部门不同工作岗位的最高薪资

    ```mysql
    mysql> select deptno,job,max(sal) from emp group by deptno,job;
    +--------+-----------+----------+
    | deptno | job       | max(sal) |
    +--------+-----------+----------+
    |     20 | CLERK     |  1100.00 |
    |     30 | SALESMAN  |  1600.00 |
    |     20 | MANAGER   |  2975.00 |
    |     30 | MANAGER   |  2850.00 |
    |     10 | MANAGER   |  2450.00 |
    |     20 | ANALYST   |  3000.00 |
    |     10 | PRESIDENT |  5000.00 |
    |     30 | CLERK     |   950.00 |
    |     10 | CLERK     |  1300.00 |
    +--------+-----------+----------+
    ```

    **案例：**找出所有工资大于2900的岗位

    ```mysql
    mysql> select deptno,job,max(sal) from emp where sal>2900 group by deptno,job;
    +--------+-----------+----------+
    | deptno | job       | max(sal) |
    +--------+-----------+----------+
    |     20 | MANAGER   |  2975.00 |
    |     20 | ANALYST   |  3000.00 |
    |     10 | PRESIDENT |  5000.00 |
    +--------+-----------+----------+
    ```

    **案例：**找出每个部门的平均薪资，要求显示薪资大于2000的数据

    ```mysql
    mysql> select deptno,job,avg(sal) from emp group by deptno having avg(sal)>2000;
    +--------+---------+-------------+
    | deptno | job     | avg(sal)    |
    +--------+---------+-------------+
    |     20 | CLERK   | 2175.000000 |
    |     10 | MANAGER | 2916.666667 |
    +--------+---------+-------------+
    ```

    

17. 总结一个完整的DQL语句怎么写？

    select

    ​	...		5

    from

    ​	...		1

    where

    ​	...		2

    group by

    ​	...		3

    having

    ​	...		4

    order by

    ​	...		6



## Day 2

----

1. 关于查重结果集的去重

   ​	**distinct**   关键字

   ​		使用方法：

   ```mysql
   						原本的：
   mysql> select job deptno from emp ;
   +-----------+
   | deptno    |
   +-----------+
   | CLERK     |
   | SALESMAN  |
   | SALESMAN  |
   | MANAGER   |
   | SALESMAN  |
   | MANAGER   |
   | MANAGER   |
   | ANALYST   |
   | PRESIDENT |
   | SALESMAN  |
   | CLERK     |
   | CLERK     |
   | ANALYST   |
   | CLERK     |
   +-----------+
   14 rows in set (0.00 sec)
   					使用了去重：
   mysql> select distinct job deptno from emp ;
   +-----------+
   | deptno    |
   +-----------+
   | CLERK     |
   | SALESMAN  |
   | MANAGER   |
   | ANALYST   |
   | PRESIDENT |
   +-----------+
   					distinct后边使用了多个字段
   注意:这里看起来是有重复的字段，但是distinct之后有两个字段，所以，只要这两个字段不同时一样，那么就认为不是相同的字段
   mysql> select distinct job,deptno from emp ;
   +-----------+--------+
   | job       | deptno |
   +-----------+--------+
   | CLERK     |     20 |
   | SALESMAN  |     30 |
   | MANAGER   |     20 |
   | MANAGER   |     30 |
   | MANAGER   |     10 |
   | ANALYST   |     20 |
   | PRESIDENT |     10 |
   | CLERK     |     30 |
   | CLERK     |     10 |
   +-----------+--------+
   		
   ```

   **注意**：distinct 只能出现在所有字段的最前面

   案例： 统计岗位的数量

   ```mysql
   mysql> select count(distinct job) as countOfJob from emp;
   +------------+
   | countOfJob |
   +------------+
   |          5 |
   +------------+
   ```

   

2. 连接查询

   1. 什么是连接查询？

   ​	在实际的开发当中，大部分的情况下都不是从单表当中查询数据，一般都是多张联合查询去除最终的结果。

   ​	在开发中，一般一个业务都会对应多张表，比如：学生和班级，起码两张表

   2. 根据表的连接方式，表的连接方式包括

    + 内连接：
      	+ 等值连接
      	+ 非等值连接
      	+ 自连接
    + 外连接
      	+ 左连接
      	+ 有连接
   	+ 全连接（不用了）

3. 在表的连接查询方面有一种现象称为：笛卡尔积现象。

   ​	案例：找出每一个员工的部门名称，要求显示员工名和部门名；（在最下边）

   ```mysql
   mysql> select ename,deptno from emp;
   +--------+--------+
   | ename  | deptno |
   +--------+--------+
   | SMITH  |     20 |
   | ALLEN  |     30 |
   | WARD   |     30 |
   | JONES  |     20 |
   | MARTIN |     30 |
   | BLAKE  |     30 |
   | CLARK  |     10 |
   | SCOTT  |     20 |
   | KING   |     10 |
   | TURNER |     30 |
   | ADAMS  |     20 |
   | JAMES  |     30 |
   | FORD   |     20 |
   | MILLER |     10 |
   +--------+--------+
   14 rows in set (0.00 sec)
   
   mysql> select * from emp;
   +-------+--------+-----------+------+------------+---------+---------+--------+
   | EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
   +-------+--------+-----------+------+------------+---------+---------+--------+
   |  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
   |  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
   |  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
   |  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
   |  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
   |  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
   |  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
   |  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
   |  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
   |  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
   |  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
   |  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
   |  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
   |  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
   +-------+--------+-----------+------+------------+---------+---------+--------+
   14 rows in set (0.00 sec)
   
   mysql> select * from dept;
   +--------+------------+----------+
   | DEPTNO | DNAME      | LOC      |
   +--------+------------+----------+
   |     10 | ACCOUNTING | NEW YORK |
   |     20 | RESEARCH   | DALLAS   |
   |     30 | SALES      | CHICAGO  |
   |     40 | OPERATIONS | BOSTON   |
   +--------+------------+----------+
   4 rows in set (0.04 sec)
   
   mysql> select ename,dname from emp,dept;
   +--------+------------+
   | ename  | dname      |
   +--------+------------+
   | SMITH  | ACCOUNTING |
   | SMITH  | RESEARCH   |
   | SMITH  | SALES      |
   | SMITH  | OPERATIONS |
   | ALLEN  | ACCOUNTING |
   | ALLEN  | RESEARCH   |
   | ALLEN  | SALES      |
   | ALLEN  | OPERATIONS |
   | WARD   | ACCOUNTING |
   ..........................................
   	   					别名的用法：
   mysql> select e.ename,d.dname from emp e, dept d;
   +--------+------------+
   | ename  | dname      |
   +--------+------------+
   | SMITH  | ACCOUNTING |
   | SMITH  | RESEARCH   |
   | SMITH  | SALES      |
   | SMITH  | OPERATIONS |
   | ALLEN  | ACCOUNTING |
   | ALLEN  | RESEARCH   |
   | ALLEN  | SALES      |
   | ALLEN  | OPERATIONS |
   | WARD   | ACCOUNTING |
   | WARD   | RESEARCH   |
   | WARD   | SALES      |
   | WARD   | OPERATIONS |
   | JONES  | ACCOUNTING |
   | JONES  | RESEARCH   |
   | JONES  | SALES      |
   | JONES  | OPERATIONS |
   | MARTIN | ACCOUNTING |
   | MARTIN | RESEARCH   |
   | MARTIN | SALES      |
   | MARTIN | OPERATIONS |
   | BLAKE  | ACCOUNTING |
   ......................................................
   
   mysql> select e.ename, d.dname from emp e,dept d where d.deptno = e.deptno;
   +--------+------------+
   | ename  | dname      |
   +--------+------------+
   | SMITH  | RESEARCH   |
   | ALLEN  | SALES      |
   | WARD   | SALES      |
   | JONES  | RESEARCH   |
   | MARTIN | SALES      |
   | BLAKE  | SALES      |
   | CLARK  | ACCOUNTING |
   | SCOTT  | RESEARCH   |
   | KING   | ACCOUNTING |
   | TURNER | SALES      |
   | ADAMS  | RESEARCH   |
   | JAMES  | SALES      |
   | FORD   | RESEARCH   |
   | MILLER | ACCOUNTING |
   +--------+------------+
   ```

   **关于表的别名**：

   	+ mysql> select ename,dname from emp,dept;
   	+ mysql> select e.ename,d.dname from emp e, dept d;

   ​	**注意**：这两者的查询结果没有任何的区别，但是第二句的查询速度要更快一些，因为第一句话中没有限制ename是在哪个表当中进行查找，所以他也从dept中进行查找，但是dept当中根本没有那个字段，所以白查了。

   ​	**优点：**查询效果好，可读性强！

