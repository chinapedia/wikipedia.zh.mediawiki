{{NoteTA
|G1=IT
}}
[[File:Db_null.png|300px]]字符用来表示[[数据库理论|数据库理论]]中的Null。]]
'''空值'''（Null或NULL）是[[SQL|結構化查詢語言]]中使用的特殊標記，是中对数属性未知或缺失的一种标识，用於指示數據庫中不據值。由關係數據庫模型的創作者 E.F.科德所引入。SQL空值是用來滿足真實關係數據庫管理系統（RDBMS）中，支持“缺失資訊與不適用的資訊”的需求。科德還介紹了在數據庫理論中使用小寫的希臘字母（ω）符號來表示空值。在 SQL中則是以 NULL 用於標識空值的保留關鍵字。SQL null是一個狀態，而不是一個值。這種用法與大多數編程語言完全不同，其中參照的空值意味著不指向任何對象。

這不應與 0 數值混淆。空值表示缺少值－而與零值不同，與缺乏答案的方式不同，作為“否”的答案。例如，考慮“亞當擁有多少本書？”這個問題，答案可能是“零”（我們知道他沒有）或“空白”（我們不知道他擁有多少）。在數據庫表格中，回報此問題的列結果，將從沒有值（標記為Null）開始，並且在我們確定亞當沒有書籍之前，並不會更新為值“零”。

[[数据库表|数据库表]][[主键|主键]]的取值不能为[[空值|空值]]。另外，数据库中的[[统计|统计]][[计算|计算]]，一般将有空值的数据忽略不计。

==應用==
*作為插入資料時，欄位的預設值
*查詢時的條件式
:在SQL的Where條件式去判斷id欄位是否為Null時，像是 '''where id = null''' 是無法正確執行的，必須寫成 '''where id is null''' ；反之若要判斷為id欄位是否為非Null時，則用'''where id is not null'''
*查詢時的空值評估取代（n為評估式或欄位名稱，e為當n為null時要回傳的內容）
:* coalesce(n,e) 
:: 被Oracle DB、Microsoft SQL Server、IBM DB2、Postgre SQL、MySQL等資料庫支援
:* isnull(n,e)
:: 被Microsoft SQL Server、Microsoft-Access等資料庫支援
:* nvl(n,e)
:: 被Oracle DB資料庫支援
:* Nz(n,e) 
:: 被Microsoft-Access等資料庫支援

== 歷史 == 
EF Codd 在一篇 1975年的ACM - SIGMOD FDT報告的論文中提到了空值作為表示關係模型中缺失數據的一種方法。Codd最常被引用的與Null語義相關的論文（如 SQL中所採用的）是他 1979年在 ACM Transactions on Database Systems上發表的論文，其中他還介紹了他的 Relational Model/Tasmania，儘管其他許多提議後面的文章一直很模糊。1979年他的論文2.3節詳細描述了空值在做算術運算時散播的語義，以及比較空值時使用三值（三元）邏輯的比較；他還詳細說明了對其它集合操作的空值處理（後者目前仍存在爭議）。在數據庫理論界，Codd最初的建議（1975,1979）現在被稱為“Codd tables”。 Codd後來強化了他的要求，即在 ''ComputerWorld''雜誌上發表的一篇 1985年由兩部分組成的文章中，所有 RDBMS都支持 Null來表示缺失的數據。

在 IBM System R中實現原型後，1986年的 SQL標準基本上採用了 Codd的建議。雖然 Don Chamberlin認為nulls（和重複行一起）是 SQL最有爭議的特性之一，但他辯護 SQL中的 Nulls設計，並提出了實用的觀點，認為這是系統對缺少資訊支援最方便的形式，從而使程序員免受許多重複的應用程序級別檢查（請參閱semipredicate問題），同時也為數據庫設計人員提供了不願意使用 Null的選項; 例如，為了避免眾所周知的異常（在本文的語義部分討論）。Chamberlin還認為，除了提供一些缺失值功能之外，對於空值的實踐經驗也會導致依賴於空值的其它語言特性，如某些分組構造和外連接。最後，他認為在實踐中，Nulls最終也會被用作快速修補現有模式的一種方法，當它需要超出其原始意圖的時候，不是為了丟失而是為了不適用的數據編碼; 例如，一個數據庫如果有每英里加侖的欄位，需要快速新增值為電動汽車時。

Codd在其 1990年出版的“數據庫管理關係模型第2版”中指出，SQL標準所要求的單一 Null 類型是不夠的，應該用兩種不同的 Null 類型標記來替代，以表明數據丟失的原因。在 Codd的書中，這兩個 Null型標記分別被稱為“A值”和“I值”，分別表示“缺失但適用”和“缺失但不適用”。 Codd的建議將要求擴展 SQL的邏輯系統以適應四值邏輯系統。由於這種額外的複雜性，具有不同定義類型的多個空值概念，尚未在數據庫領域廣泛接受。儘管如此，它仍然是一個活躍的研究領域，許多論文還在發表。

=== 挑戰 ===
由於其相關的[[三值逻辑|三值邏輯（3VL）]]，它在 SQL連接中使用的特殊要求，以及聚合函數和 SQL分組操作符所需的特殊處理，空值一直是爭議的焦點和爭議的來源。計算機科學教授 Ron van der Meyden將各種問題總結為：“SQL標準中的不一致，意味著不可能將任何直觀的邏輯語義歸於 SQL中的空值處理”。 儘管為解決這些問題提出了各種建議，但候選方案的複雜性阻礙了它們的廣泛採用。

== 空值的散播 ==
由於 Null不是數據值，而是缺少值的標記，因此以數學運算符使用 Null會給出未知結果。
=== 算術運算 ===
該結果由空值表示。下例中將 Null乘以 10將導致Null：
<source lang="sql">
10 * NULL          -- Result is NULL
</source>
這可能會有出乎意料的結果。例如，當試圖將 Null除以零時，平台可返回 Null值而不會拋出預期的“除以零－數據異常”。雖然這種行為不是由 ISO SQL標准定義的，但許多 DBMS供應商都以類似的方式處理這一操作。例如，Oracle，PostgreSQL，MySQL服務器和 Microsoft SQL Server平台都會針對以下內容返回空值結果：
<source lang="sql">
NULL / 0
</source>
=== 字串連接 ===
在 SQL中常見的字串連接操作，在其中一個操作元為 Null時也會導致 Null。下例演示了使用 Null與 SQL 字串連接運算符 || 返回的 Null結果：
<source lang="sql">
'Fish ' || NULL || 'Chips'   -- Result is NULL
</source>
對於數據庫實作來說並非都是如此。在 Oracle RDBMS中，例如 NULL和空字符串被認為是相同的，因此<code>'Fish'|| NULL || '芯片'</code>字串連接的結果是 'Fish芯片'。

== NULL和三值邏輯的比較 ==
由於 Null不是任何數據域的成員，因此它不被視為“值”，而是指缺失值的標記（或佔位符）。因此與 Null進行比較永遠不會導致 True或 False，而總變成在三值邏輯的 Unknown 結果中。下面表達式的邏輯結果是將值 10 與 Null進行比較，得到的結果會成為未知：
<source lang="sql">
SELECT 10 = NULL       -- Results in Unknown
</source>
但是，如果缺失值與操作結果無關，則對 Null的某些操作可以返回值。考慮下面的例子：
<source lang="sql">
SELECT NULL OR TRUE   -- Results in True
</source>
在這種情況下，OR 左邊的未知值這一事實是無關緊要的，因為 OR 的操作結果將是 True，而不管左邊的值如何。

SQL實現了三值邏輯，因此 SQL的實作必須提供專門的三值邏輯（3VL）。SQL三值邏輯的規則如下表所示（<math>p</math>和<math>q</math> 表示邏輯狀態）“ SQL使用 AND，OR和 NOT 的真值表，對應於 Kleene和 Łukasiewicz三值邏輯的常見片段，有價值的邏輯（它們的含義定義不同，但 SQL沒有定義這樣的操作）
{| class="wikitable"
 ! ''p'' !! ''q'' !! ''p'' OR ''q'' !! ''p'' AND ''q'' !! ''p'' = ''q''
 |-
 | {{yes2|True}} || {{yes2|True}} || {{yes2|True}} || {{yes2|True}} || {{yes2|True}}
 |-
 | {{yes2|True}} || {{no2|False}} || {{yes2|True}} || {{no2|False}} || {{no2|False}}
 |-
 | {{yes2|True}} || {{Unknown}} || {{yes2|True}} || {{Unknown}} || {{Unknown}}
 |-
 | {{no2|False}} || {{yes2|True}} || {{yes2|True}} || {{no2|False}} || {{no2|False}}
 |-
 | {{no2|False}} || {{no2|False}} || {{no2|False}} || {{no2|False}} || {{yes2|True}}
 |-
 | {{no2|False}} || {{Unknown}} || {{Unknown}} || {{no2|False}} || {{Unknown}}
 |-
 | {{Unknown}} || {{yes2|True}} || {{yes2|True}} || {{Unknown}} || {{Unknown}}
 |-
 | {{Unknown}} || {{no2|False}} || {{Unknown}} || {{no2|False}} || {{Unknown}}
 |-
 | {{Unknown}} || {{Unknown}} || {{Unknown}} || {{Unknown}} || {{Unknown}}
|}

{| class="wikitable"
 ! ''p'' !! NOT ''p''
 |-
 | {{yes2|True}} || {{no2|False}}
 |-
 | {{no2|False}} || {{yes2|True}}
 |-
 | {{Unknown}} || {{Unknown}}
|}
=== WHERE子句中的未知效應 ===
在數據操縱語言（DML）和查詢的比較謂詞中，若遇到 SQL三值邏輯，該 WHERE子句會導致 DML語句僅對那些謂詞評估為  True的列結果起作用；若是 INSERT，UPDATE 或者 DELETE 等 DML語句，則因為此謂詞計算的結果為假、或是未知列，不會執行，並放棄 SELECT查詢。將 Unknown 解釋成 False 相同的邏輯結果，是處理空值時會遇到的常見錯誤，下面的簡單例子說明了這個謬誤：
<source lang="sql">
SELECT *
FROM t
WHERE i = NULL;
</source>
上例的查詢邏輯一定返回零列，因為 i 欄位與 Null 比較的結果一定是傳回“未知”，即使對於那些 i 為 Null 的資料列也是如此。未知結果導致 SELECT語句立即丟棄每一列。（但在實作中，一些 SQL工具將使用與 Null的比較來檢索列。）
=== 空值指定和3VL特定比較謂詞 ===
基本 SQL比較運算符在與 Null進行比較時，始終返回“未知”，因此 SQL標準提供了兩個特定的 Null 比較謂詞： <code>IS NULL</code>和 <code>IS NOT NULL</code>（使用後綴語法），來檢測數據是不是空值。

SQL標準包含一個擴展 F571“真值測試”，它引入了三個額外的邏輯一元運算符（實際上，如果我們計算它們的否定，它們是其語法的一部分），也使用了後綴表示法。他們有以下真值表：
{| class="wikitable"
|-
! p !! true !! false !! unknown
|-
| p IS TRUE || true || false || false
|-
| p IS NOT TRUE || false || true || true
|-
| p IS FALSE || false || true || false
|-
| p IS NOT FALSE || true || false || true
|-
| p IS UNKNOWN || false || false || true
|-
| p IS NOT UNKNOWN || true || true || false
|}
F571擴展與 SQL中布林數據類型的存在正交（本文稍後討論），儘管語法相似，但 F571不會在語言中引入布林值或三值文字。1999年，在布林型數據類型被引入標準之前，F571擴展實際上存在於 SQL92中。然而，F571擴展只有少數系統實作；PostgreSQL是實作它的數據庫之一。

加入三值邏輯中的其它運算符使 SQL 的三值邏輯功用完善，這意味著它的邏輯運算符可以表示（以組合）任何可能的三值邏輯函數。

在不支持 F571擴展的系統上可以遍歷每種可能組合，使表達式 p Unknown的參數來模擬 IS UNKNOWN p，並使用 IS NULL或其他 NULL特定函數來測試這些參數，雖然這樣子可能更繁瑣。

=== WHERE子句的排中律 ===

=== 空值在其它構造式中的影響 ===
==== 連接(JOIN) ====
==== CASE表達式 ====
SQL提供了兩種風格的條件表達式。一為“簡單 CASE”並像 switch 語句一樣操作。另一在標準中稱為“搜索 CASE”，並像 if ... elseif一樣運行。

簡單 <code>CASE</code> 表達式使用隱式相等比較，它們的執行和 DML的 <code>WHERE</code> 子句處理 Null 的規則是相同的。因此，一個簡單 <code>CASE</code> 表達式無法直接檢查 Null 的存在。在簡單 <code>CASE</code> 表達式中檢查 Null 總會導致結果為未知，如下所示：
<source lang="sql">
SELECT CASE i WHEN NULL THEN 'Is Null'  -- This will never be returned
              WHEN    0 THEN 'Is Zero'  -- This will be returned when i = 0
              WHEN    1 THEN 'Is One'   -- This will be returned when i = 1
              END
FROM t;
</source>
不管 i 列所包含的的值是什麼（即使它包含Null），該表達式的計算結果都為“未知” ，<code>'Is Null'</code> 字串將永遠不會返回。

另一方面，“搜索” <code>CASE</code>表達式可以使用謂詞 <code>IS NULL</code> 和 <code>IS NOT NULL</code> 條件。下例顯示如何使用搜索 <code>CASE</code>表達式來正確檢查 Null：
<source lang="sql">
SELECT CASE WHEN i IS NULL THEN 'Null Result'  -- This will be returned when i is NULL
            WHEN     i = 0 THEN 'Zero'         -- This will be returned when i = 0
            WHEN     i = 1 THEN 'One'          -- This will be returned when i = 1
            END
FROM t;
</source>

Oracle的 SQL 方言提供了一個內置函數 <code>DECODE</code>，可以用它來代替簡單的 CASE表達式，並考慮兩個相等的空值。
<source lang="sql">
SELECT DECODE(i, NULL, 'Null Result', 0, 'Zero', 1, 'One') FROM t;
</source>

如果最後都沒有與條件相匹配的結果，所有這些結構將會返回 NULL；它們有一個預設的 <code>ELSE NULL</code> 子句。

==== 程序擴展中的 IF語句 ====
SQL/PSM（SQL預存持續模組）定義 SQL的預存程序擴展，例如 IF 語句。但歷史上主要的 SQL供應商都包含了他們自己專有的程序擴展。循環和比較的程序擴展在空值比較規則下運行，類似於 DML 語句和查詢。以下預存程序的片段以 ISO SQL 標準格式演示了在 IF 語句中使用 3VL的 Null 。
<source lang="plpgsql">
IF i = NULL THEN
      SELECT 'Result is True'
ELSEIF NOT(i = NULL) THEN
      SELECT 'Result is False'
ELSE
      SELECT 'Result is Unknown';
</source>
該IF語句僅對那些評估為 True 的比較執行操作。對於評估為 False 或未知的 IF 語句，該語句將控制傳遞給 ELSEIF 子句，最後傳遞給 ELSE 子句。上面代碼將因與 Null 的比較始終評估為未知，結果一定會是 <code>'Result is Unknown'</code> 。

== 分析SQL空值的語義 ==
=== 選擇和預測：代表性弱 ===
=== 如果考慮連接或聯合：甚至不表示弱 ===


== 檢查約束和外鍵 ==
== 外連接 ==
SQL 的外連接、左外連接和右外連接，會自動生成空值以作為結果表中缺失值的佔位符。如對於左外連接會產生空值，代替左外連接操作後，右側表中欄位缺少值的列。下例使用兩個表來示範左外連接操作產生的空值佔位符。第一個表（Employee）包含員工編號和姓名，而第二個表（PhoneNumber）包含相關的員工編號和電話號碼，如下。
{|
| valign="top" |
{| class="wikitable"
|-
|+ Employee
|-
! ID
! LastName
! FirstName
|-
| 1
| Johnson
| Joe
|-
| 2
| Lewis
| Larry
|-
| 3
| Thompson
| Thomas
|-
| 4
| Patterson
| Patricia
|-
|}
| valign="top" |
{| class="wikitable"
|-
|+ PhoneNumber
|-
! ID
! Number
|-
| 1
| 555-2323
|-
| 3
| 555-9876
|-
|}
|}
以下示例 SQL查詢對這兩個表執行左外連接。
<source lang="sql">
SELECT e.ID, e.LastName, e.FirstName, pn.Number
FROM Employee e
LEFT OUTER JOIN PhoneNumber pn
ON e.ID = pn.ID;
</source>
此查詢生成的結果集演示 SQL如何使用 Null作為右側（PhoneNumber）表中缺少的值的佔位符，如下所示。
{| class="wikitable"
|-
|+ Query result
|-
! ID
! LastName
! FirstName
! Number
|-
| 1
| Johnson
| Joe
| 555-2323
|-
| 2
| Lewis
| Larry
|  {{Null result}}
|-
| 3
| Thompson
| Thomas
| 555-9876
|-
| 4
| Patterson
| Patricia
|  {{Null result}}
|-
|}

== 聚合函數 ==
SQL定義了聚合函數以簡化伺服器端的數據聚合計算。除 <code>COUNT(*)</code>函數外，所有集合函數都會執行 Null-elimination 步驟，因此計算的最終結果中不包含 Null。

請注意，消除 Null不等於用零替換 Null。例如下表中 <code>AVG(i)</code>（求 <code>i</code> 欄位的平均值）將給出與 <code>AVG(j)</code>不同的結果：
{| class="wikitable" style="font-family:monospace"
|-
! i
! j
|-
| 150
| 150
|-
| 200
| 200
|-
| 250
| 250
|-
| {{Null result}}
| 0
|}
這裡的 <code>AVG(i)</code> 是 200（150, 200 和 250的平均），而 <code>AVG(j)</code> 則是 150（150, 200, 250 和 0 的平均）。在 SQL 聚合函數中，<code>AVG(z)</code>不等於 <code>SUM(z)/COUNT(*)</code>，這是一個眾所周知的副作用。

聚合函數的輸出也可以是空值。這裡是一個例子：
<source lang="sql">
SELECT COUNT(*), MIN(e.Wage), MAX(e.Wage)
FROM Employee e
WHERE e.LastName LIKE '%Jones%';
</source>
此查詢將始終輸出一行，計算姓氏中包含“Jones”的員工人數，並給出這些員工的最低和最高工資。但是，如果沒有員工符合給定的標準會發生什麼？計算空集的最小值或最大值是不可能的，所以這些結果必須為NULL，表示沒有答案。這不是未知值，它是表示沒有值的空值。結果是：
{| class="wikitable" style="font-family:monospace"
! COUNT(*)
! MIN(e.Wage)
! MAX(e.Wage)
|-
| 0
| {{Null result}}
| {{Null result}}
|}
== 當兩個空值相等時：分組，排序和一些設置操作 ==
由於 SQL：2003將所有 Null標記定義為彼此不相等，因此需要特殊定義才能在執行某些操作時將 Null分組在一起。SQL將“任何兩個彼此相等的值或任何兩個空值”定義為“不同”。<code>not distinct</code>的這個定義允許 SQL在使用 GROUP BY 子句（和執行分組的其他關鍵字）時對 SQL進行分組和排序。

其他 SQL操作，子句和關鍵字在處理空值時使用“不明顯”。這些包括以下內容：

*PARTITION BY 排序和開窗功能的 ROW_NUMBER子句
*UNION，INTERSECT和 EXCEPT操作符，它們將NULL視為用於行比較/消除目的相同
*DISTINCT SELECT查詢中使用的關鍵字

SQL規範中的 UNION操作符效果會違反空值不相等的原則（它們確實相互確定了空值）。因此某些 SQL操作（如聯合或區別）可能產生不能表示確定信息的結果，這與涉及與 NULL進行顯式比較的操作（例如 WHERE上面討論的子句中的那些操作）不同。在 1979年的 Codd提案中（基本上被SQL92採納），通過論證刪除集合操作中的重複項“在比檢索操作的評估中的等式測試更低的細節層次上發生”這種語義不一致性是合理的。

SQL標準沒有明確定義空值的默認排序順序。相反，在符合性的系統上，子句 ORDER BY可以分別使用列表 NULLS FIRST或 NULLS LAST，分別在所有數據值之前或之後，對空值進行排序。然而，並非所有資料庫供應商都實現了這一功能。不實現此功能的供應商可能會在 DBMS中，為空值的排序指定不同的處理方法。
== 對索引操作的影響 ==
某些 SQL產品不可以建立包含 NULL 的索引鍵。例如，PostgreSQL 8.3 版本之前 B樹索引的文件說明，
{{quote|
B－樹可以處理數據的等式和範圍查詢，這些數據可以按照某種順序排序。特別是，PostgreSQL查詢規劃器會在使用< ≤ {{=}} ≥ > 這些運算符進行比較時，涉及索引列時考慮使用 B－樹索引：

< ≤ {{=}} ≥ > 等效於這些運算符（如 BETWEEN 和 IN）組合的構造也可以用 B－樹索引搜索實現。（但請注意，IS NULL 不是等於而且不可索引。）:
}}

在強制唯一性的建立索引執行情況下，欄位為 NULL值會從索引中被排除，並且不會在 NULL之間強制執行唯一性。再次引用 PostgreSQL文件：
{{quote|
當索引被宣告是唯一時，將不允許具有相同索引值的多個表行。空值不被視為相等。多列唯一索引只會拒絕所有索引列在兩行中相等的情況。
}}

這種作法符合 SQL：2003-純量空值比較的規範。

索引空值的另一種方法涉及按照 SQL：2003定義的行為將它們處理為不明顯。例如，Microsoft SQL Server文檔聲明如下：
{{quote|
為了建立索引，NULL比較相等。因此，如果鍵在多行中為 NULL，則無法創建唯一索引或 UNIQUE 約束。當選擇唯一索引或唯一約束的列時，選擇定義為 NOT NULL 的列。
}}
這兩種索引策略都與 SQL：2003定義的 Null行為一致。因為索引方法沒有被 SQL：2003標準明確定義，所以空值的索引策略完全由供應商來設計和實現。

== 空值處理函數 ==
SQL定義了兩個函數來顯式處理空值：''NULLIF'' 和 ''COALESCE''。這兩個函數都是 CASE表達式的縮寫。
=== NULLIF ===
NULLIF 函數接受兩個參數。如果第一個參數等於第二個參數，則 NULLIF 返回 Null。否則，返回第一個參數的值。
<source lang="sql">
NULLIF(value1, value2)
</source>
因此，NULLIF是以下 CASE表達式的縮寫：
<source lang="sql">
CASE WHEN value1 = value2
     THEN
         NULL
     ELSE
         value1
END
</source>
=== COALESCE ===
COALESCE 函數接受參數列表，從列表中返回第一個非 Null值：
<source lang="sql">
COALESCE(value1, value2, value3, ...)
</source>
COALESCE被定義為以下SQL CASE表達式的簡寫：
<source lang="sql">
CASE WHEN value1 IS NOT NULL THEN value1
     WHEN value2 IS NOT NULL THEN value2
     WHEN value3 IS NOT NULL THEN value3
     ...
     END
</source>
一些 SQL DBMS 供應商實作特定的功能類似 COALESCE 函數。某些系統（例如 Transact-SQL）實作為 ISNULL函數，或者功能類似 COALESCE 的其他函數。
=== NVL ===
ORACLE NVL函數接受兩個參數。它返回第一個非 NULL參數，如果所有參數都是 NULL，則返回 NULL。

COALESCE 表達式可被轉換成等效的 NVL表達式這樣的：
<source lang="mysql">
COALESCE ( val1, ... , val{n} )
</source>
變成：
<source lang="mysql">
NVL( val1 , NVL( val2 , NVL( val3 , … , NVL ( val{n-1} , val{n} ) … )))
</source>
這個函數的用例是在一個表達式中用某一特定值替換 NULL，例如 <code>NVL(SALARY, 0)</code>，意為'若薪資欄位缺少值，則以 0 替換它'。但有一個明顯例外，在大多數實作中 COALESCE 只評估其參數列表到逹第一個非 NULL值，這有幾個重要的原因：第一個非 NULL 參數之後的參數可能是一個函數，它可能在計算成本上很昂貴、無效、或者可能會產生意料之外的副作用；然而 NVL 將評估參數列表其中的所有參數。

== 數據類型為空和未知 ==
== BOOLEAN數據類型 ==

== 爭論 ==
=== 常見錯誤 ===
=== 批評 ===
=== 閉環世界的假設 ===


== 参考文献 ==
{{Reflist}}

== 延伸讀物 ==

== 外部鏈接 ==

== 参见 ==
* [[SQL|SQL]]

{{-}}
{{SQL}}
{{Databases}}
{{Nulls}}

{{DEFAULTSORT:NULL}}
[[Category:SQL关键字|Category:SQL关键字]]