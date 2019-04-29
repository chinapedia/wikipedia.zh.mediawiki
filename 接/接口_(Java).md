{{noteTA
|G1=IT
|1=zh-cn:接口; zh-hk:介面; zh-tw:介面;
|2=zh-cn:类; zh-hk:類別; zh-tw:類別;
}}
{{cleanup-jargon|time=2013-01-19T19:01:28+00:00}}

'''介面'''（{{lang-en|Interface}}），在[[Java|Java程式語言]]中是一個{{tsl|en|Abstract_type|抽象型別}}（Abstract Type），它被用來要求[[类_(计算机科学)|類別]](Class)必須實作指定的方法，使不同類別的物件可以利用相同的界面進行溝通。介面通常以'''<code>interface</code>'''來宣告，它僅能包含[[方法簽名|方法簽名]]（Method Signature）以及[[常數|常數]]宣告（變數宣告包含了 <code>[[Static_variable#Static_Variables_as_Class_Variables|static]]</code> 及 <code>[[Final_(Java)|final]]</code>），一個介面不會包含[[方法_(電腦科學)|方法]]的實作（僅有定義）。

介面無法被实例化，但是可以被實作。一個實作介面的類別，必須實作介面內所描述的所有方法，否則就必須宣告為{{tsl|en|Abstract_class|抽象類別}}（Abstract Class）。另外，在Java中，介面型別可用來宣告一個變數，他們可以成為一個空指標，或是被綁定在一個以此介面實現的物件。

其中一個使用介面的優勢是，可以利用他們模擬[[多重继承|多重继承]]，類別在JAVA中不允許多重继承，所有在JAVA中的類別必須而且僅能有一個父類別，而{{Javadoc:SE|package=java.lang|java/lang|Object}}（JAVA型別系統中最頂層的型別）是唯一一個例外。

JAVA的類別可以被實作許多個介面，然而一個介面則無法實作其他的介面。

== 概觀 ==
介面被用來統一類別的共通行為，當不同的類別需要進行資訊共享時，是不需要特別去建立類別間的關係。舉例來說，一個人（Human）及一隻鸚鵡（Parrot）都會吹口哨（whistle），然而<code>Human</code>及<code>Parrot</code>不應該為<code>Whistler</code>的子類別，最好的做法是令他們為<code>Animal</code>的子類別，而他們可以使用<code>Whistler</code>的介面進行溝通。<br/>

還有一種介面的使用方法，則是當一個[[对象_(计算机科学)|物件]]有實現特定介面時，我們使用它是不需要知道它的類別，例如，一個事物因為口哨的噪音影響到其他人，對於其他人而言，就不需要知道噪音來源是來自人還是鸚鵡，因為他們可以確定，一個會吹口哨的事物正在吹口哨。舉一個更實際的例子，[[排序算法|排序算法]]可能會期待物件的型別是可以被{{Javadoc:SE|java/lang|比較}}的，於是它只需要知道物件的型別可以被以某種方式進行排序即可，這與物件的型別無關。<code>whistler.whistle()</code>將會呼叫物件的實現方法<code>whistle</code>，而不需要知道物件是以哪個類別來實現<code>Whistler</code>。

例如：

<source lang="Java">
  interface Bounceable {
      void setBounce();  // 注意分號
                         // 介面的方法（method）是公開（public）、抽象（abstract）、永遠不會是最尾端的型別（final）
                         // 把它們想成只是個模型，所以沒有任何方法有被實現
  }
</source>

== 使用方法 ==
=== 介面的宣告 ===
下列的語法為介面的宣告方式：

 [''存取修飾''] interface '''''介面名稱''''' [extends ''其他的介面''] {
         ''常數宣告''
         ''抽象方法宣告''
 }

介面的主體包含著抽象[[方法_(電腦科學)|方法]]，但所有方法在介面內（定義上）都是抽象（Abstract）方法，所以<code>abstract</code>的關鍵字在介面內則不被需要。由於介面代表著一個對外行為的集合，所以任何方法在介面內都是<code>public</code>(公開的)。

所以，一個簡單的介面可以這麼寫
<source lang="java">
public interface Predator {
       boolean chasePrey(Prey p);
       void eatPrey(Prey p);
}
</source>

介面內的成員皆為靜態（static）、final及公開（public），反之，他們可以成為任何類別或介面的型別<ref>{{cite web|url=http://java.sun.com/docs/books/jls/third_edition/html/interfaces.html#9.5|title=The Java Language Specification}}</ref>'''

實現一個介面的語法，可以使用這個公式：
 ... implements ''介面名稱''[, ''其他介面'', ''其他的...'', ...] ...

類別可以用來實現介面，舉例來說
<source lang="java">
public class Lion implements Predator {

        public boolean chasePrey(Prey p) {
               // programming to chase prey p (specifically for a lion)
        }

        public void eatPrey (Prey p) {
               // programming to eat prey p (specifically for a lion)
        }
}
</source>
如果一個類別實現了一個介面，而沒有實現介面的所有方法，則它必須被標注為<code>abstract</code>(抽象類別)。一個抽象類別的子類別必須實現它未完成的方法，假如該項子類別仍不會實現介面的所有方法，那麼該項子類別依然需要被標注為<code>abstract</code>。

類別可以同時實現多項介面
<source lang="Java">
 public class Frog implements Predator, Prey { ... }
</source>

介面通常被使用在Java程式語言，用來做[[回调函数|回调函数]]使用<ref>{{cite web|url=http://www.javaworld.com/javaworld/javatips/jw-javatip10.html|title=Java World}}</ref> 。Java並不允许方法作為參數傳遞使用，因此，其中一個解決辦法則是可以定義一個介面，把這個介面當成方法的參數，以此來使用該項物件的方法簽名。

=== 子介面 ===
介面可以被延伸為數個不同的介面，可以使用上述所描述的方法，舉例來說：
<source lang="java">
 public interface VenomousPredator extends Predator, Venomous {
         //介面主體
 }
</source>
以上的程式片段是合法定義的子介面，與類別不同的是，介面允許多重繼承，而<code>Predator</code> 及 <code>Venomous</code> 可能定義或是繼承相同的方法，比如說<code>kill(Prey prey)</code>，當一個類別實現<code>VenomousPredator</code>的時候，它將同時實現這兩種方法。

== 範例 ==
有些泛用的[[Java|Java]]介面可供參考：
* {{Javadoc:SE|java/lang|Comparable}} 擁有一個方法{{Javadoc:SE|name=compareTo|java/lang|Comparable|compareTo(T)}}，用以描述兩個物件是否相等，或是其中一個物件大於另外一個物件。[[泛型|泛型]]允許已經實現的類別，其物件可以用來互相比較。
* {{Javadoc:SE|java/io|Serializable}} 是一個[[marker_interface|marker interface]] 沒有任何介面或是欄位，僅有一個空的主體，它被用來表示一個類別可以被[[序列化|序列化]]。它的[[Javadoc|Javadoc]]描述了他是如何運作，而且不需要被強制編程。

== 另見 ==
* [[Mixin|Mixin]]
* [[Trait_(computer_programming)|Traits]]

== 參考文獻 ==
{{reflist}}

== 外部連結 ==
* [http://10kloc.wordpress.com/2012/12/03/abstract-interfaces-the-mystery-revealed/ Skeletal Implementations in Java Explained]
* [http://java.sun.com/docs/books/tutorial/java/concepts/interface.html What Is an Interface?]
* [http://javapapers.com/?p=17 Difference between a Java interface and a Java abstract class]

[[Category:Java|Category:Java]]

[[de:Schnittstelle_(Objektorientierung)|de:Schnittstelle_(Objektorientierung)]]
[[pl:Interfejs_(Java)|pl:Interfejs (Java)]]
[[ru:Интерфейс_(объектно-ориентированное_программирование)|ru:Интерфейс (объектно-ориентированное программирование)]]