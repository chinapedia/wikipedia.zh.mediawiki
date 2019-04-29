{{ Infobox Software
| name                   = jOOQ
| logo                   = 
| screenshot             = 
| caption                = 
| developer              = Data Geekery GmbH
| status                 = Active
| latest release version = 3.3.0
| latest release date    = {{release date|2014|02|14}}
| latest preview version = 
| latest preview date    = 
| operating system       = [[跨平台|跨平台]]
| platform               = [[Java平台|Java]]
| programming language   = [[Java|Java]]
| genre                  = [[对象关系映射|对象关系映射]]
| license                = Dual-licensed: [[Apache许可证|ASL 2.0]] and commercial
| website                = http://www.jooq.org
}}
'''面向Java对象查询'''（{{lang-en|'''J'''ava '''O'''bject '''O'''riented '''Q'''uerying}}，[[縮寫|縮寫]]：'''JOOQ'''），是一个轻量级的JAVA数据库映射类库。它实现了[[Active_Record|Active Record]]，同时面向“关系”和“对象”提供[[领域特定语言|领域特定语言]]以构造查询语句。

== 编程范式 ==

jOOQ主张，在任何数据库集成中，都应首先考虑发挥[[SQL|SQL]]的作用。这样一来，就不必再引入新的查询语言，而只是通过jOOQ对象以及依照数据库架构自动生成的代码来创建普通的SQL。jOOQ通过[[JDBC|JDBC]]来完成底层的SQL查询。
与诸如[[Hibernate|Hibernate]]等通常[[ORM|ORM]]类库不同的是，jOOQ并不提供过多的功能，复杂性也不高，它只是提供了JDBC之上更便捷的抽象层封装而已。

== 代码范例 ==

嵌套查询一个起了别名的表

<source lang="sql">
  -- 选取已售罄书籍的作者
  SELECT * FROM AUTHOR a
        WHERE EXISTS (SELECT 1
                   FROM BOOK
                  WHERE BOOK.STATUS = 'SOLD OUT'
                    AND BOOK.AUTHOR_ID = a.ID);
</source>

等价的jOOQ

<source lang="java">
  // 在Select语句中使用别名
  create.selectFrom(AUTHOR.as("a"))
        .where(exists(selectOne()
                     .from(BOOK)
                     .where(BOOK.STATUS.equal(BOOK_STATUS.SOLD_OUT))
                     .and(BOOK.AUTHOR_ID.equal(a.ID))));
</source>

== 详见 ==

* [[Hibernate|Hibernate]]
* [[MyBatis|MyBatis]]
* [[Ebean|Ebean]]
* [[对象关系映射软件列表|对象关系映射软件列表]]
* [[SQL|SQL]]

== 外部链接 ==

* [http://www.jooq.org jOOQ Home]
* [http://java.net/projects/el-spec/pages/CollectionOperations JSR-341]
* [http://www.h2database.com/html/jaqu.html JaQu]
* [https://github.com/julianhyde/linq4j Linq4j]
* [https://web.archive.org/web/20140131202006/http://quaere.codehaus.org/ Quaere]
* [http://www.querydsl.com QueryDSL]

{{Java (Sun)}}

[[Category:Java平台|Category:Java平台]]
[[Category:Java企业平台|Category:Java企业平台]]