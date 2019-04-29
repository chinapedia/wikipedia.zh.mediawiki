{{Overly detailed|date=2017年5月}}
{{noteTA
|G1=IT
|1=zh-tw:欄位;zh-cn:字段;
}}
'''SELECT'''是[[SQL|SQL]][[資料操縱語言|資料操縱語言]]（DML）中用於查詢表格内欄位資料的指令，可搭配條件限制的子句<small>(如'''where''')</small>或排列順序的子句<small>（如'''order'''）</small>來获取查詢結果。

'''SELECT'''的基本語句格式。

{{quote|<source lang="sql">
SELECT [ALL | DISTINCT] 欄位名 [,欄位名...]
 FROM 資料表名 [,資料表名...]
 [WHERE 篩選條件式]
 [GROUP BY 欄位名[,欄位名...]]
 [ORDER BY 欄位名[,欄位名...]]
</source>}}

==简单範例==

假設下方範例表格名稱為「T」；表格中有存有二列資料並以C1、C2 兩欄區分資料內容。

{| class="wikitable" style="float: center; clear:right; margin: 1em" border="1"
! C1 !! C2
|-
| wiki || 10
|-
| wikipedia  || 100
|}

===欄位查詢===
以「*」代表回傳全部的欄位內容   
{| class="wikitable" style="float: center; clear:right; margin: 1em" border="1"
!查詢語句
!回傳結果
|-
||<source lang="sql">SELECT * FROM T;</source>
|align="center"|
{|
|-
| wiki || 10
|-
| wikipedia  || 100
|}
|}

或指定只查詢C1欄位資料
{| class="wikitable" style="float: center; clear:right; margin: 1em" border="1"
!查詢語句
!回傳結果
|-
||<source lang="sql">SELECT C1 FROM T;</source>
|align="center"|
{|
|-
| wiki 
|-
| wikipedia 
|}
|}

===條件限制===
以「where」來限制回傳C1欄位中完全符合條件的資料
{| class="wikitable" style="float: center; clear:right; margin: 1em" border="1"
!查詢語句
!回傳結果
|-
||<source lang="sql">SELECT * FROM T WHERE C1 = 'wiki';</source>
|align="center"|
{|
|-
| wiki || 10
|}
|}

以「where」搭配「like」來回傳C1欄位中相似符合條件的資料
{| class="wikitable" style="float: center; clear:right; margin: 1em" border="1"
!查詢語句
!回傳結果
|-
||<source lang="sql">SELECT * FROM T WHERE C1 like 'wiki%';</source>
|align="center"|
{|
|-
| wiki || 10
|-
| wikipedia || 100
|}
|}

利用運算比較式來回傳C2欄位中符合數值大小的資料
{| class="wikitable" style="float: center; clear:right; margin: 1em" border="1"
!查詢語句
!回傳結果
|-
||<source lang="sql">SELECT * FROM T WHERE C2 > 50;</source>
|align="center"|
{|
|-
| wikipedia || 100
|}
|}
==语义==
SELECT语句内部各组成部分的理论计算顺序，依次为：<ref>Itzik Ben-Gan:《Microsoft Sql Server 2012 high-performance T-sql using windows functions》</ref>
#FROM的表连接；
## 笛卡尔积
## ON连接条件筛选（完成了内部连接）
## 添加外部连接的行
#WHERE子句篩選出满足條件的行集；
#GROUP BY子句对行集中的行做分组合并，使得多个行对应于结果集中的一行；
#应用HAVING子句从中间结果筛选出满足条件的行的集合；
#SELECT的结果列中的表达式，然后是DISTINCT关键字处理（如果有的话）。因此，在SELECT中给结果集中的列指定别名，是无法被WHERE子句或者GROUP BY子句或者HAVING可见并使用的。
#应用ORDER BY子句对结果集中的行排序。
#如果存在TOP或OFFSET/FETCH，对结果行的挑选。

如果使用了GROUP BY子句做分组合并，之后要引用的列必须是或者出现在GROUP BY子句中，或者被包含在聚合函数（如SUM、COUNT等）中。否则编译会报错。这是因为，上述两种情形的列对于每一个分组都有确定的单一值；而上述两种情形以外的列，对于每一个分组，有可能对应于原始行集的多个行从而具有多个不同的值，那么选择哪个值作为该分组的该列的值？无从选择。聚合函数计算时忽略掉列值为NULL的行。

HAVING子句是在分组后再做筛选，所以HAVING子句中可以包含聚合函数；而WHERE子句就不能包含聚合函数，因为WHERE子句是在分组之前计算的，那时根本无从计算聚合函数。例如，对销售表依据客户名称做分组合并，然后筛选出每个客户的订单合计金额大于100万元的情形，从而得到规模以上大客户的清单。

使用ORDER BY子句，可以按照单个列排序，也可以依次按照多个列排序，也可以按照结果集中列的别名排序，还可以使用结果集之外的列排序。但是，如果已经指定了SELECT DISTINCT或者该语句包含了GROUP BY子句，或是包含了UNION运算符，则排序列必须包含在结果集的列中。这是因为，在上述情形，原数据或者中间表的多个行对应于结果集中的一行；排序列如果不出现在结果集的列中，那么就可能使结果集中的一行对应于多行从而有了多个排序列的值，这行的排序情况就不唯一导致无从确定其排序后的顺位。可以使用ASC或者DESC关键字制定升序或降序，缺省为升序。

对于排序来说，更复杂的是不同字符编码所带来的比较规则的不同。例如，ASCII字符串的字典序比较与Unicode字符串的字典序比较，就完全不同。可以使用COLLATE子句指定显式排序规则。比较运算符以及MAX、MIN、BETWEEN、LIKE、IN等运算符都涉及到排序规则。

筛选条件表达式，可以使用=（相等）、>、<、>=、<=、<>等比较运算符，NOT逻辑非、AND、OR等逻辑运算符，BETWEEN或者NOT BETWEEN表示开区间或者其补集的所有值，IN关键字列出所有可行值（特别是在子查询中），LIKE关键字用于模式匹配查询。模式包括%代表任意字符串，_代表单个任意字符，[]表示指定范围内的单个字符，[^]表示不在指定范围内的单个字符。可以用ESCAPE关键字定义[[转义字符|转义字符]]，或者用[]包含按照字面使用的字符。

NULL值计算使用[[三值逻辑|三值逻辑]]。谓词计算结果为TRUE、FALSE或者UNKNOWN。对于筛选条件表达式，SQL只接受TRUE。对于CHECK约束则是拒绝FALSE。两个NULL值是否相等，这取决于是否遵从ANSI标准。可以使用谓词IS NULL或者IS NOT NULL使得结果确定且唯一。 在GROUP BY或者ORDER BY子句，分组或排序时两个NULL视为相等。

对结果集中的列，可以使用关键字TOP选项，限制结果集中返回行数或者行数所占百分比。还可以紧随其后使用关键字WITH TIES，返回原结果集中最后一行的排序字段相等的所有行。例如，返回原始数据表中某列最大的那一行，如果使用关键字WITH TIES就会把并列最大的多行全部返回。

在SELECT之后紧随关键字DISTINCT，使得结果集中不含重复的行。关键字DISTINCT也可用于函数参数。

'''子查询'''是嵌套于SELECT、INSERT、UPDATE、DELETE等语句中的查询。按照子查询返回结果的数量，分为标量子查询和多值子查询；按照对外部查询的依赖性，分为独立子查询和相关子查询。子查询出现在SELECT语句的结果列表中，那么子查询应该是返回单一值；这种子查询往往可以用表的Join操作代替。子查询用在WHERE子句的表达式中，可以返回单一值用于比较运算符（>、<、>=等等）之后；也可以返回多值且有ANY、SOME、ALL等关键字前缀用于比较运算符之后；还可以返回多值与关键字IN、EXISTS、NOT IN、NOT EXISTS连用。子查询可以嵌套子查询。

==資料參考==
{{reflist}}
*{{cite book |title=深入淺出SQL (HeadFirst SQL) |year=2008 |publisher=[[歐萊禮|歐萊禮]] (O'REILLY) |isbn=978-986-6840-16-6 | }}
*{{cite book |title=MySQL 5 徹底研究 第三版 (The Definitive Guide to MySQL5 3ed) |year=2006 |publisher=博碩文化 |isbn=957-527-908-5|}}

==外部連結==
*[http://msdn.microsoft.com/en-us/library/ms189499.aspx SELECT Syntax（Microsoft SQL Server）]
*[http://www.firebirdsql.org/rlsnotesh/rlsnotes210.html#rnfb20x-dml-select-syntax SELECT Syntax（Firebird）]
*[http://dev.mysql.com/doc/refman/5.1/en/select.html  SELECT Syntax（MySql）]
*[http://www.postgresql.org/docs/current/static/sql-select.html SELECT Syntax（PostgreSQL）]
*[http://www.sqlite.org/lang_select.html  SELECT Syntax（SQLite）]

{{-}}
{{SQL}}
{{Databases}}

[[Category:SQL关键字|Category:SQL关键字]]