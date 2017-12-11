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
	    
/**************************************************************************************************************/

  SQL99标准中的表链接
  内连接：
      select 字段列表
          from 表1 inner jion 表2
	       on 关联条件
      select e.id,e.first_name, d.name
          from s_emp e inner join s_dept d 
	       on e.dept_id = d.id
	           where e.salary > 1400;
  外链接：
      左外链接：
          左外链接的结果集 = 内连接的结果集 + 左表匹配不上的数据
	  select 字段列表
	      from 左表 left [outer] join 右表
	          on 关联条件；
      右外链接：
          右外链接的结果集 = 内连接的结果集 + 右表匹配不上的数据
	  select 字段列表
	      from 左表 right [outer] join 右表
	          on 关联条件；
      全外链接：
          全外链接的结果集 = 内连接的结果集 + 两表匹配不上的数据
	  select 字段列表
	      from 左表 full [outer] join 右表
	          on 关联条件；
   minus:返回第一个结果集减去第二个结果集，剩余的记录
     select id from s_emp minus select is from s_dept;
   union：两个结果集的字段列表的数量和数据必须匹配
/************************************************************************************************************/ 
						第三章
/************************************************************************************************************/ 
3.组函数和分组
    组函数：
    常用组函数： 
    count 统计一组数据的行数 //参数是任何类型， 而且可以使用*
        select count(salary) form s_emp;
        select count(*) from s_emp where salary > 1400;
    max 统计一组数据的最大值
    min 统计一组数据的最小值
        参数可以 number date varchar2(char)
	select max(salary),min(salary) from s_emp;
	select max(start_date),min(start_date) from s_emp;
    sum 统计一组数据的和
    avg 统计一组数据的平均值
        select sum（salary），avg(salary) from s_emp;
    
    组函数的参数可以使用distinct
        select count(title),count(distinct title) from s_emp;
	
  分组：语法 group by 分组标准 （按照分组标准，把数据分到不同的组里） 	
        select 
	  from 
	    where
	      group by
	       ...
	       order by
        按照部门编号分组，统计每个部门的人数
	 select count(*) cnt
	   from s_emp
	     where 1=1
	       group by dept_id;
	按照部门标号分组，统计每个人部门工资大于1200的人数
	  select dept_id，count(*) cnt
	    from s_emp
	      where salary > 1200
	       group by dept_id;
        按照部门编号分组，统计每个部门工资大于1200的人，显示部门名称及人数。
	   select e.dept_id，count(d.id) cnt
	    from s_emp e, s_dept d
	      where salary > 1200 and e.dept_id = d.id
	       group by dept_id;  //错误，d.name不是分组标准
	       在分组语句中，能够列出的字段必须要是分组标准或 组函数的参数
            select e.dept_id,d.name,count(d.id) cnt
	    from s_emp e, s_dept d
	      where salary > 1200 and e.dept_id = d.id
	       group by e.dept_id, d.name; // right
        按照部门编号分组，统计工资超过1200的分数超过1个的部门 
	    select dept_id, count(id) cnt
	      from s_emp
	        where salary > 1200 and count(id) > 1
		 group by dept_id; //错误，在where子句不能使用组函数
            having 子句：
	      having 条件
	      功能：分组后，根据条件筛选符合条件的组
	      
	      select dept_id, count(id) cnt
	      from s_emp
	        where salary > 1200 
		 group by dept_id 
		   having count（id）> 1;//having 子句中也不能使用别名
		   
	语法顺序：
	      select                  ----字段
	        from                  ----表
		  where               ----从表中筛选符合条件的行
		    group by          ----根据分数标准 统计每组数据结果
		      having          ----根据条件筛选结果
		        order by      ----根据结果排序显示
			
/************************************************************************************************************/ 
						第四章
/************************************************************************************************************/

4.子查询
  子查询就是一条select 语句嵌入到另一条SQL语句中，作为其中的一部分，被嵌入的select语句称为子查询。
  外层的SQL语句可以称为父查询。
  
  先执行括号里面的语句在执行其他语句。
  
  where子句中
    单行单列的结果
    子查询的结果集是单值的时候，可以使用比较运算符（>、=等）
        查询 职位和‘ben’的职位相同的员工信息
	select title from s_emp where first_name = ‘ben’;
	
	select id, first_name,title from s_emp where titl = (select title from s_emp where first_name = ‘ben’);
	
    多行多列的结果集
    子查询的结果集是多行的，
    where子句中使用的运算符必须是可以处理多值的，比如in、not in、 all、 any等（all、 any需要和比较符号配合使用，>all、 <any等）。
    
    --使用子查询列出s_emp表中的领导信息。
    1）列出所有领导的编号
    select distinct manager from s_emp；
    2）根据编号在累出其他信息
    select id,first_name,title from s_emp where id in(select distinct manager_id from s_emp);
    
    select id,first_name,title from s_emp where id not in(select distinct manager_id from s_emp);//error
    结果为空用=或！=结果永远为假
    select id,first_name, title from s_emp where id not in (select distinct namager from s_emp where manager_id is not null);//right
    
    子查询中需要引用外层查询的字段数据，可以使用exists关键字。
    --列出有员工的部门信息：
     select * form s_dept d where exists (select * form s_emp e where e.dept_id = d.id);
     
     也可以在having后面使用子查询
     按照部门编号分组，统计每个部门的平均工资，显示出平均工资高于编号为42的。
     1）列出平均工资高于1000的部门信息
     select avg(salary) from s_emp where dept_id = 42;
     2)列出结果
     select avg(salary) from s_emp  group by dept_id having avg(salary) >(select avg(salary) from s_emp where dept_id = 42);
     
     form子句中
     任何一条合法的select语句 ,都会在内存中创建一个临时的内存表。 
     如果要在一个子查询的语句中继续查询，那么则子查询就会出现在from语句中，这个子查询可以称为一个匿名试图。
     --列出人数操作2个的部门：
     select dept_id,count(id) cnt from s_emp group by dept_id having count(id)>2;
     select *  from (select dept_id,count(id) cnt from s_emp group by dept_id) where cnt>2;//在from后面表达式必须取别名 否则只能写表达式；
     
     --列出工资高于本部门平均工资的员工的信息
     select e.di, e.first_name, e.salary,a.avg from s_emp e, (select dept_id,avg(salary) avg from s_emp group by dept_id) a where
     a.id = e.dept_id and a.avg < e.salary;
     
     select 之后
     把子查询放到select子句中，可以认为是外链接的另一种方式，使用更为灵活。
     --列出所有员工的编号、名字、工资和所在部门的名称。
     select e.id,e.first_name,e.dept_id,d.name from s_emp e,s_dept d where e.dept_id = d.id（+）;
     select e.id,e.first_name,e.salary,(select name from s_dept d where d.id = e.dept_id) from s_emp e;
     
     --练习
     列出工资比公司所有人的平均工资高的员工的信息。
     select id,first_name, salary from s_emp where salary > (select avg(salary) from s_emp); //在where中不能用组函数操作
     列出人数超过两个的部门信息，包括部门名称和人数。
     select e.dept_id, d.name, count(e.id) from s_emp e, s_dept d where e.dept_id = d.id group by d.name,e.dept_id having count(e.id) > 2;
     
/************************************************************************************************************/ 
						第五章
/************************************************************************************************************/
  命名规格：对象名_姓名缩写_座位号
表操作：
  标识符命名
  1）只能使用英文字母、数字、_、$、#
  2)第一个字符必须是字母开始
  3）不能喝关键字重名
  4）不能喝其他的数据库对象重名
  5）1~30位
创建和删除表
   create table 表名 （
   字段名 数据类型， 
   ... ...
   字段名 数据类型
   ）；
   
   --举例
   创建一个员工表，包含以下字段：
   编号 数字 
   名字 字符串
   工资 数字
   入职日期 日期
   create table emp_new_1(
     id number(7),
     name varchar2(25),
     salary number(11.2),
     start_date date
   );
   create table emp_new_1(
  2  id number(7),
  3  name varchar2(25),
  4  salary number(11,2),
  5  start_date date);
  
   删除表
   语法：
   drop table 表名；
   举例： drop table emp_new_1；
   
  DML语句
  insert
    语法： insert into 表名[（字段列表）] values （值列表）；
    字段列表和值列表的数量、顺序和数据类型必须一致
    字段列表缺省时，表示表中的全部字段，并且顺序和表结构一致
    举例：
    insert into emp_new_1（id, name, salary, start_date) values(1, 'test1',1200, '11-DEC-17');
    commit;//提交
    	ID NAME 			 SALARY START_DAT
---------- ------------------------- ---------- ---------
	 1 test 			   1200 11-DEC-17
    insert into emp_new_1 (id, name, start_date, salary) values (2, 'test2', sysdate, 1300);
    	ID NAME 			 SALARY START_DAT
---------- ------------------------- ---------- ---------
	 1 test 			   1200 11-DEC-17
	 2 test2			   1300 11-DEC-17

    insert into emp_new_1 values(3, 'test3', 1500, sysdate); //error
    insert into emp_new_1 values(4,'test4',  sysdate)//error
    值列表值提供部分值，必须给出字段列表，所有没有给出值的字段，必须允许为NULL；
    insert into emp_new_1 (id, name, start_date, salary) values （4,'test4',  sysdate）；
    insert into emp_new_1 (id, name, salary, start_date) values(4, 'test3',null, sysdate);
    	ID NAME 			 SALARY START_DAT
---------- ------------------------- ---------- ---------
	 1 test 			   1200 11-DEC-17
	 2 test2			   1300 11-DEC-17
	 4 test3				11-DEC-17
	 
  update
    update 表名 set 字段=新值[,字段=新值，...]
        [where 子句]
    举例：
    update emp_new_1 set salary = 2000 where salary is null;
    	ID NAME 			 SALARY START_DAT
---------- ------------------------- ---------- ---------
	 1 test 			   1200 11-DEC-17
	 2 test2			   1300 11-DEC-17
	 4 test3			   2000 11-DEC-17
    update emp_new_1 set salary = salary + 500;
    	ID NAME 			 SALARY START_DAT
---------- ------------------------- ---------- ---------
	 1 test 			   1700 11-DEC-17
	 2 test2			   1800 11-DEC-17
	 4 test3			   2500 11-DEC-17

  delete
  删除表中的数据：
  语法 delete[from] 表名 [where子句]；
  delete emp_new_1；
  rollback; //撤回
  
  delete from emp_new_1 where id = 1;
  commit;
  
  truncate table emp_new_1;//删除无法撤销  属于 ddl语句 不能撤销
  
  TCL语句（事务控制语句）
  事务控制语句的含义： 
  commit； 确认事务 提交所有没提交的操作
  rollback；回滚事务 撤销所有没有提交的操作
  savepoint 保存点； 创建保存点
  rollback to 保存点 撤销到保存点的位置
  
    select和事务无关 
    ddl自动隐式提交事务
    dml语句默认属于显示提交
  
  事务具有的特性（acid）
  1)a.原子性（Atomicity） 事务中的语句是一个不可分割的整体。
    if a&&b
      commit;
    else 
      rollback;
  2)c.一致性（Consistency） 事务执行的结果必须是数据库从一种状态变为另一种一致性状态 //既a和b的总和不变
  3）i.隔离性（Isolation） 一个事务对数据所做的改变，在提交之前，对于其他的事务是不可见的。
  4）d.持久性（Durability） 事务一旦提交，对数据库数据所做的改变就是永久的。
  
  部分成功部分失败
    insert into t values(1,'1');
    savepoint a;
    insert into t values(2,'2');
    savepoint b;
    insert into t values(3,'3');
    savepoint c;
    insert into t values(4,'4');
    savepoint d;
    rollback to b;
    commit;
    
    练习：
    --1.使用查询语句创建表
    create table 表名 as  select 语句；
    create table emp_new_1  as select * from s_emp;
    --2.给‘Carmen’的多有下属涨工资
    查询 编号 ，根据编号找下属，  根据下属编号涨工资
    --3.删除与‘ben’同一部门的员工
    查询‘ben’部门编号， 更具部门编号删除员工
