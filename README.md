# Oracle
2017.11.7  +8day___1day;
1、数据库介绍
  人工管理阶段：20世纪50年代
    科学计算、卡片磁带等硬件、无操作系统
  文件系统阶段：
    磁鼓、磁盘
    缺点：数据冗余、数据的不一致、数据之间联系弱
  数据库阶段：
    （大量海量数据）20世纪60年代末至今
    三大标志性事件：1) 1968 IBM--->IMS;
                   2) 1969 DBTG--->发布数据库和相关环境的规范
                   3）1970 IBM(E.F>Codd) 发表一系列论文，关系数据模型
    特点：使用更为复杂的数据结构、为用户提供方便的接口（sql，应用程序）、并发控制、数据库恢复、数据完整性、安全性方面控制功能、系统更加灵活。
    信息处理方式不再是以程序为中心，是以程序为中心
    
    数据库技术的几个术语
      数据（data）：数据库空存储的对象，包括文件、图像、声音等
      数据库（DB）:长期存储在计算机内、有组织、可共享的大量数据的集合。
      数据库管理系统（DBMS）：位于操作系统和用户之间的一层数据管理软件。科学的组织和存储数据，搞笑的获取和维护数据。
      数据库系统（DBS）:在计算机系统中引入数据库后的系统构成（数据库、数据库管理系统（及开发工具）、应用系统、数据库管理员、用户构成）。
      
    关系型数据库
      层次-->网状-->关系
      用二维表保存数据的数据库，称为关系型数据库。
      
      表头
      行（记录、实体）  。。  。。  。。  。。
                       。。
                       。。
                       。。
                       。。
                       。。
                       。。
                       列（字段、字段值）
    2.主流关系型数据库产品
    商用
    {
      Oracle 10g 11g 12c（甲骨文）
      DB2 IBM 
      sql server 微软
      sybase
    }
    开源
      Mysql Oracle
    3.SQL（Structured Query Language ） 结构化查询语言
    SQL在关系型数据库上执行数据操作、检索以及维护所使用的一种标准语言，可以用来查询数据、操作数据、定义数据、控制数据等
    SQL 分为：
      数据查询语句（DQL）:select  查询所需要的数据。使用最广、语法灵活、复杂 //importent
      数据操作语句（DML）:insert delet update  对数据增删改操作
      用于改变数据库表中的数据（DDL）：create drop alter 建立、删除、修改数据库对象
      事务控制语句（TCL）：conmmit rollback savepoint 用来维护数据库中数据的一致性
      数据库控制语句（DCL）:create user、grant、revoke 用于执行创建和回收权限、创建用户等
    4.远程登录
      开发工具
        SQL*PLUS:（Oracle提供的数据库进行交互的工具）被DBA和开发人员广泛使用的一个工具。功能强大、使用简单，可以运行在任何Oracle运行的平台上，
默认和数据库一起安装。
        SQL*PLUS是基于C/S结构的，命令提示符的工具
        oracle sql developer:图形化工具，oracle 官方提供。
      远程登录
        one_step:登录远程服务器
          telnet ip // telnet 172.30.6.10 172.30.6.20
          用户名：oracle      密码：oracle (for server)
        two_step:使用远程服务器上的
          sqlplus
          用户名：openlab      密码：open123（for DB）
          
       SQL>
          sqlplus命令：不用分号结尾
          sql语句：比喻用分号结尾
      5.查看表结构的命令
        desc 表明 （desc s_emp)
        SQL> desc s_emp
 Name       	  Null?              Type
 ----------------------------------------- -------- ----------------------------
 ID					   NOT NULL             NUMBER(7)     number(7)
 LAST_NAME	   NOT NULL             VARCHAR2(25)  varchar()
 FIRST_NAME					                VARCHAR2(25)  data()
 USERID 					                  VARCHAR2(8)
 START_DATE					                DATE
 COMMENTS					                  VARCHAR2(255)
 MANAGER_ID					                NUMBER(7)
 TITLE					              	    VARCHAR2(25)
 DEPT_ID				              	    NUMBER(7)
 SALARY 				              	    NUMBER(11,2)
 COMMISSION_PCT         				    NUMBER(4,2)

name:字段
null？：字段是否允许为NULL not null 不允许为空
Type： 数据类型
      number(p, s): 数字类型
      p:精度  1 <= P <= 38
      s:精确到小数点前（后）多少位  -84 <= s <= 127 （默认0）
      
      varchar2(n):变长数组 1 <= n <= 4000(务默认值）
      char（n）: 定长字符串 1 <= n <= 2000（默认值1）
      
      date : 日期类型

2.select语句
  1.几个概念
  选择：部分行、所有列
  投影：全部行、部分列
  表链接：查询的数据来自于多张表
  2.select语句
  1）本语句： select... from ..；
    select 字段列表 from 表名；(查看一条数据）
    select 字段名，字段名 ..from ..;（查看多字段）
    select 字段，...from ；表名（查看所有）
    
    表中字段的算术运算（一般是数字、（日期） ）
    + - * /  （% 有特殊用处）
    列出每个员工的年输入：（工资+年终奖）
    select ID， first_name,salary, 12*salary+500 from s_emp;
    用双引号“”解决别名问题
    
    别名    {字段名|表达式} [as] 别名
    列出每个员工的年输入：（工资+年终奖）(
    select ID， first_name,salary, 12*salary+500 from s_emp;
    列出一个字段：
    
    表示字符串：‘’    ‘a’  ‘Hello world’
    字符串拼接：||  ‘hello’||'world' --->'helloworld'
    拼接last_name与first_name   select last_name||'_'||first_name from s_emp;
    
    转义字符 '''' first and last is '' /two is chang label /three is printed label
    空值（NULL）的处理   空值参与运算，会使得曾哥表达式结果为NULL
    使用函数nvl处理NULL   nvl（par1,par2)：如果par1部位null，返回par1    如果par1是NULL,返回par2
    **par1和par2类型必须相同**
    nvl(12*salary*(1+commission_pct/100), 12*salary);
    12*salary*(1+nvl(commission_pct, 0)/1000);
    
    数据的排重显示 distinct
    select title  from s_emp; //显示有重复的
    select distinct title from s_emp;//去重复显示
 ？ select distinct title,distinct dept_id from s_emp;//多次排重显示，必须出现在前面（distinct在前面不能出现字段字）
    
    
  2）where 子句
    根据条件 筛选符合条件的行 select 字段列表 from 表名 where 条件；
    select ID,first_name, salary from s_emp where salary >2000;
    select ID,first_name, salary from s_emp where salary =2000; 数据库不支持‘==’
    列出名字为‘Bela'
        select ID,first_name, salary from s_emp where last_name = 'Bela';  //字符串的值是区分大小写
        select ID,first_name, salary from s_emp where last_name = 'bela';  //sql语句中关键字、表名、字段名不区分大小写
    
    where 子句中的比较运算符
    > < <= >= = != (<>, ^=)//不等于三种符号
    
    sql中提供的运算符
    表达一个闭区间[a, b]   between a and b;
    where 字段名 between a and b;
    列出工资在[1200, 2000]之间的员工信息
    select first_name Name, salary from s_emp where salary between 1200 and 2000;
    select first_name Name, salary from s_emp where salary > 1200 and salary < 2000;
    beteween a and b !--->  not between a and b
    
    表示一个列表
    int（列表）
    where 字段名 in（值1， 值2，值3...)   //只要字段名中有值1，值2，值3...表达式就位true
    select id,first_name,dept_id from s_emp where dept_id in(31,21,34);
    select id,first_name,dept_id from s_emp where dept_id = 21 or dept_id = 31 or dept_id = 43;
    int (a, b) !---> not in (a, b)
    
    模糊查询
    %：代表任意长度的任意字符
    _：一位任意字符
    运算符：like
    where 字段 like ‘包含通配符的表达式’
    where name like ‘%龙%’
    select first_name from s_emp where first_name like '_a%'; 
    select first_name from s_emp where first_name like '%a%';
    查询内容包含%的数据库怎么办？
    select table_name from user_tables where table_name like ‘S_%’;
    如果要匹配的字符串中包含_或%，则需要使用转义escap‘转义字符’
    select table_name from user_tables where table_name like ‘S\_%' escape'\';
    
    NULL值的判断
    .不能用等号来判断是否为空只能用is,如果用等或者不等于其结果一定为假）
    where 字段 is null
    select id, first_name,title,manager_id from s_emp where manager_id is null；（OK）
    	ID FIRST_NAME		     TITLE		       MANAGER_ID
      ---------- ------------------------- ------------------------- ----------
	       1 Carmen		     President

    select id, first_name,title,manager_id from s_emp where manager_id = NULL;(NO)
    no rows selected
    
    sql提供的逻辑运算符
    and or not
    与 或  非
    between and  ---> not between and
    in()        ----> not in()
    like        ----> not like
    is null     ----> is not null
    select is, first_name, commission_pct from s_emp where commission_pct is not null;
    
  3）odrder by 子句(一定出现在一条语句的最后）
    select...from...
       [where 条件]
       ... ...
       [order by 子句]
    语法：order by 排序标准 排序方式
    desc :      降序 
    asc  ：默认  升序
    按照工资降序排序，列出员工Id, first_name,salary
    select id,first_name,salary from s_emp order by salary desc;
    多列排序：
    语法：order by  排序标1 排序方式， 排序标准2 排序方式2
    null 默认作为最大值处理
    select id, first_name, salary,title from s_emp order by manager_id;
  
  4）单行函数
    单行函数：针对SQL语句影响的数据，每行都做处理，每行产生一个结果。
    select upper (first_name) from s_emp;
    select lower (first_name) from s_emp;
    组函数：针对SQL语句影响的数据，分组处理每组产生一个结果。
    select count（first_name） from s_emp;
    COUNT(FIRST_NAME)
    -----------------
	       25

  5）表链接 (dual)
    desc--->count--->select
    
    字符串函数
    upper（str）; //返回str全大写形式
    lower（str）；//返回str全小写形式
    initcap(str); //返回str每个单词首字母大写，其他全小写的形式
    
    concat(s1,s2);  <----> || //字符串拼接
    substr(str,start=1，[length=0]://截取子字符串
      start 拜师截取的位置： >0从原字符串的左边开始 
                            <0从原字符串右边开始
      length:截取字符串的长度 ，缺省时表示截取位置到字符串末尾；//都是往后面截取的
    length（str）; //返回str的长度
    
    练习： 
      1、用两总方式 截取s_emp;表中first_name 的后三位；
      	first: select substr(first_name, -3, 3) from s_emp;
	second: select substr(first_name,(length(first_name)-2) from s_emp;
      2、列出s_emp表中每个员工ID，first_name，和年收入（考虑提成），筛选出年输入超过15000员工的信息，并对年收入降序排序
      测试:年收入的别名时候可以在where、order by 子句中使用；
      	select id,first_name,12*salary*(val(commission_pct,0)/100 + 1) YearSalary from s_emp where YearSalary > 15000 order by YearSalary desc; (**error**)
	select id,first_name,12*salary*(nvl(commission_pct, 0)+1) YearSalary from s_emp where 12*salary*(nvl(commission_pct, 0)+1) > 15000 order by 12*salary*(nvl(commission_pct, 0)+1) desc;(**right**) //12*salary*(val(commission_pct,0)/100 + 1) YearSalary 其中YearSalary 不能用于where 但能够在 order by 后面。
	
	from --->where --->select--->order by 执行顺序
	
	3、查看s_dept、s_region两表结构和数据。
                |        |
              部门表   地区表
<s_dept> SQL> select id,name,region_id from s_dept;

	ID NAME 		      REGION_ID
---------- ------------------------- ----------
	10 Finance			      1
	31 Sales			      1
	32 Sales			      2
	33 Sales			      3
	34 Sales			      4
	35 Sales			      5
	41 Operations			      1
	42 Operations			      2
	43 Operations			      3
	44 Operations			      4
	45 Operations			      5

	ID NAME 		      REGION_ID
---------- ------------------------- ----------
	50 Administration		      1
<s_region> SQL> select id,name from s_region;

	ID NAME
---------- --------------------------------------------------
	 1 North America
	 2 South America
	 3 Africa / Middle East
	 4 Asia
	 5 Europe
12 rows selected.

/2017.12.08 +8day two_day***********************************************************************************/

  6）数字函数和分组语句
     round（x[,y]） //四舍五入
     缺省y时，默认y=0 比如： round(4.67,1) = 4.7;  round(342.4532,-2) = 300
     trunc (x[,y]) //截断
     缺省y时，默认y=0 比如： trunc(4.67,1) = 4.6;  trunc(342.4532,-2) = 300
     floor(x) //<=x的最大整数
     ceil(x) //>=x的最小整数
     
     日期类型和常用日期函数
     	格式 dd_MON_yy 08_DEC_17 中文： dd_n月_yy
	系统日期 :sysdate  // select sysdate from dual;
	日期格式的各个部分：
		yy 两位数字的年 17		 mm 两位数字的月 12				    dd 两位数字的日 08
		yyyy 4位数字的年 2017	  MON(mon) 月份单词的前三个字母	DEC(dec)          DY(dy) 星期几单词的前三位 （FRI）fri
		year 年的全拼		   MONTH(month)月份单词的全拼 DECEMBER(december)    DAY(day) 星期几单词的全拼	FRIDAY(friday)
    		hh24 24小时两位数字 10 
		hh 12小时制 14-->02
		mi 两位数字分钟 30
		ss 两位数字的秒 22
		cc 世纪 21
		AM(am) 上午下午  AM(PM)/am(pm)
		
		select to_char(sysdate, 'yyyy-mm-dd hh24:mi:ss: day cc am') from dual;
	日期的算术运算	
		日期加一个数字
			select sysdate + 27 from dual;
		日期减一个数字 
			select sysdate - 27 from dual;
		一个日期减去另一个日期
			select sysdate - to_date('24-JAN-91') from dual;
		januray february match april may june july august september octorber november december
		monday tuesday wednesday thursday friday saturday  sunday weekend week workday weekday
		
		常用的日期函数
		add_moths(datel,n) : 在某个日期dat1上，加上n个月
			SQL> select sysdate, add_months(sysdate,3) from dual;
			SYSDATE   ADD_MONTH
			--------- ---------
			08-DEC-17 08-MAR-18
		months_between(datel, date2):两个日期相差的月数（带小数点）
			SQL> select sysdate, months_between(sysdate,'01-JAN-00') from dual;
			SYSDATE   MONTHS_BETWEEN(SYSDATE,'01-JAN-00')
			--------- -----------------------------------
			08-DEC-17			   215.241003
		next_day(detel, wd):返回dateld的下一个wd(星期几)
			SQL> select sysdate, next_day(sysdate,'sunday') from dual;//sunday 可以用数字代表1~7
			SYSDATE   NEXT_DAY(
			--------- ---------
			08-DEC-17 10-DEC-17
		last_day(datel):返回date1所在月份的最后一天
			SQL> select sysdate,last_day(sysdate) from dual;
			SYSDATE   LAST_DAY(
			--------- ---------
			08-DEC-17 31-DEC-1
		
		类型转换函数
		    to_char(date|n[,fmt])
		    	数字--->字符串 : select to_char(12) from dual;
		    	针对数字的格式化： 9  小数点前代表0——9，小数点后代表1——9
					 0  小数点代表前导0，小数点后代表0——9
					 .  小数点
					 $  美元符号
					 L  本地货币符号//环境配置决定的
					 ，  分割符号
			s格式字符串以‘fm’开头： ‘fm$999,999.0’   select to_char(1234.56, 'fm$099,999.000') from dual;
			
			日期--->字符串  ：select to_char(sysdate, 'yyyy-mm-dd hh:mi:ss') from dual;	
		   to_date(s[,fmt])		
		       select to_date('01-JAN-00') from dual;
		       select to_char(start_, 'yyyy-mm-dd hh24:mi:ss') from testdate;
		   to_number(s[,fmt])
		   	把字符串s按照给定的格式字符串fmt转换成数字
			隐式转换：
			    select id,first_name from s_emp where id='1'0;
			    select sysdate-to_number(5) from dual;
			    
			    select to_number('$001,234.56', '$099,999.00') from dual;
  7）询语句嵌套（子查询）
  	一个函数返回值作为另一个函数的参数。
	 select id,first_name,nvl(to_char(manager_id), 'BOOS') from s_emp ;
/*********************************************************************************************************************/
							第二章节
/ ********************************************************************************************************************/
2.表链接
  查询的数据来自于两张表：s_emp（id,fris_name）， s_dept （部门表）
  set pagesize 30 
  select s_emp.id, s_dept.frist_name,s_dept.name from s_emp,s_dept where s_emp.dept_id = s_dept.id;
  
  select s_emp.id, s_emp.first_name, s_dept.name from s_emp,s_dept where s_emp.dept_id = s_dept.id;
  
  表的别名 ： 语法 表名 别名 //**一旦命名别名，原表名及失效，就不能再使用原表名了**
  select e.id, e.frist_name, d.name from s_emp e,s_dept d where e.dept_id = d.id;
  
  关联的多张表中，字段名没有重复的可以省略字段名前面的表名或别名。
  select e.id, frist_name, name
  	from s_emp e,s_dept d
	where e.dept_id = d.id;
  表连接类型：
  	内连接： 等值连接 非等值连接 自连接
	外连接： 等值连接 非等值连接 自连接
  内连接：符合关联条件的行被选中，不符合条件的被过滤掉
  	update s_emp set dept_id = null where id = 1; commit; //等值连接使用=等号作为条件依据
	create tabel salgreade (
		grade nmber(7) primary key,
		losal number(11,2),
		hisal number(11,2)
		);   //创建表
	insert into salgrade values(1,700,1200); //表中插入数据
	
	非等值连接：
	s_emp:    id,first_name,salary
	salgrade: grade
	s关联字段： salary	losal、hisal
	s关联条件： salary between losal and hisal ||salary >= losal and salary <= hisal;
	select e.id,e.first_name,e.salary,g.grade
		from s_emp e,salgrade g
			where e.salary between g.losal and g.hisal;

？？？？
	自连接：在逻辑上，把一张表当成两张表，使用表链接的语法执行的查询操作。
	select e.id, e.first_name, m.id, m.manager_id
		from s_emp e, s_emp m
			where e.manager_id = m.id;
？？？？外链接
    	外链接的结果集 = 内连接的结果集 + 匹配不上的行 
	oracle 中的外链接语法 （+）
	关联条件：表1.字段（+） 运算符 表2.字段		 		表1.字段 运算符 表2.字段（+）
		 内连接的结果集（+）表2中匹配不上的数据			内连接的结果集 + 表1中匹配不上的数据
	自连接：
	需求：列出所有普通员工
	1)列出员工及领导的信息
	    select e.id, e.first_name,m.id,m.first_name
	    	from s_emp e, s_emp m
			where e.manager_id = m.id;
	2)结果中药包含领导表中的全部信息
	    select e.id, e.first_name,m.id,m.first_name
	    	from s_emp e, s_emp m
			where e.manager_id （+）= m.id;
	3）普通员工没有下属，筛选出所有普通员工
	    select e.id, e.first_name,m.id,m.first_name
	    	from s_emp e, s_emp m
			where e.manager_id （+）= m.id
				and e.id is null;
	4)去除员工信息（只保留领导表中的信息）
	    select m.id,m.first_name
	    	from s_emp e, s_emp m
			where e.manager_id （+）= m.id
				and e.id is null
	等值连接
	    列出所有员工的id,first_name和部门名称
	    select e.id,e.first_name ,d.name from s_emp e,s_dep d where e.dept_id = d.id(+);
	    列出员工的id,first_name和不猛名称，包括没有员工的部门
	    select e.id,e.first_name,d.name from s_emp e,s_dept d where e.dept_id(+) = d.id;
	非等值连接
	    列出员工及工资级别信息，包括所有级别
	    select s_emp e, salgrade g where e.salary(5) between g.losal and g.hisal;
	
