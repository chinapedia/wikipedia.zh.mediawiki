{{NoteTA|G1=IT}}
{{Refimprove|time=2015-10-25}}

:''「概念」(concept)已于2009年7月份的 C++ 委员会会议中被投票否决，已经从 C++0X标准中正式被移除。'''<ref>[http://www.informit.com/guides/content.aspx?g=cplusplus&seqNum=441 InformIT: The Removal of Concepts From C++0x]</ref><ref>[http://blog.csdn.net/goodbee/archive/2009/07/21/4368235.aspx  C++0x中concept的移除]</ref> '''本文紀錄的是最後一篇有出現「概念」的工作文件。<ref>[http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2009/n2914.pdf Working Draft, Standard for Programming Language C++ (version of 2009-06-22)]</ref>''
在針對 C++ 進行修訂的 C++0x 中，概念 (concept) 和與其相關的一組公設 (axiom) 被提出作為 C++ [[模板_(C++)|模板]]系統的擴充。它們被設計用來增進編譯器發現問題代碼所產生的錯誤訊息，並讓程序員能在他們所編寫的樣板中定義樣板參數所具備的屬性。這些屬性讓代碼能指引編譯器做某些優化(除了增進可讀性之外)，同時也可能透過[[形式验证|形式验证]]工具來檢驗實作與規格是否相符以增進可靠性。

2009年7月，因為概念被認為還未準備好進入 C++0x，C++0x 委員會決定從標準草案中將其移除。目前有些非正式的計劃以某種形式將概念再次納入標準，但仍未有正式的決定。一個針對概念的初步實作是{{tsl|pl|ConceptGCC}}。
== 動機 ==
模板類別和函式有必要的對他們使用的型別加上限制。例如[[STL|STL]]容器要求它所包含的型別必須是可賦值的。不像動態多型所展現的類別繼承階級，接受<code>Foo&</code>型別的函式可以接受<code>Foo</code>的任何子類別；只要支援所有模板內使用的操作，任何類別都可以被提供作為模版參數。對函式來說，引數的要求是明確的(必需是<code>Foo</code>的子類別)；但是對模版來說，物件必須符合的介面是不明確的。「概念」(concept)提供了一種機制，要求模板參數必須符合特定條件。

引入 concept 的主要目的，是為了改善編譯器發現問題代碼所產生的錯誤訊息。若程序員嘗試在模板中使用不符合其介面需求的型別，編譯器應當回報錯誤。問題在於與模板使用相關的錯誤訊息極難解讀，尤其不利於新手。主要有兩個原因：首先，錯誤訊息往往將模板參數以原名全數列出，造成訊息長度暴增。某些編譯器甚至會對簡單的錯誤產生數千字节的錯誤訊息。其次，錯誤訊息通常不會立即指出真正發生問題之處。例如，當程序員試圖將不帶有拷貝建構子的型別置入<code>vector</code>中，第一個錯誤幾乎總是指向<code>vector</code>內部使用拷貝建構之處。程序員必須有足夠的經驗和技巧才能夠了解真正的錯誤，是由於使用的型別不滿足<code>vector</code>類的要求(需要拷貝建構子)。

為了解決上述的問題，C++0x 加入了 ''concept'' 這種語言特性。Concept 是一種具名的構造，用來描述型別的需求或是條件限制。在 OOP 中，類似的做法是利用基底類別的定義，當作衍生類別的最小需求("is-a"的繼承方式，衍生類別都帶有基底類別的介面)。而 concept 的定義不限於作為模板參數的限制條件，也可以適用於模板定義(如最後的 concept <code>Stack</code>)。

模板使用 concept 的一種方法是以 concept 名稱取代模板型別指示字<code>class</code>或<code>typename</code>。在下面的例子中，若傳入模板函式<code>min</code>的型別不滿足 concept <code>LessThanComparable</code>的要求，編譯時將會產生錯誤，告知使用者具現化(instantiate)模板的型別不符合concept <code>LessThanComparable</code>。

<source lang="cpp">
template<LessThanComparable T>
  const T& min(const T &x, const T &y)
  {
    return y < x ? y : x;
  }
</source>

相較於上例的簡式用法，更為泛用的concept使用形式如下：

<source lang="cpp">
template<typename T> requires LessThanComparable<T>
  const T& min(const T &x, const T &y)
  {
    return y < x ? y : x;
  }
</source>

泛用形中，使用關鍵字 requires 作為型別需求表列的開始。需求表列由 concept 所構成，可以利用"非"(!) 與 "且"(&&)的符號，將數個 concept 結合，如同邏輯運算式。若使用者想避免某個特定的 concept 被模板套用，可以用這樣的語法：<code>requires !LessThanComparable<T></code>。在模板特化或偏特化中，可以指定型別使用特定的模板實作；而否定的 concept 語法，可以顯式地在模板或 concept 中指明被排除的型別條件為何。另外，若需要在需求表列中表達"且"(logical-and)的語意，使用"&&"將多個 concept 連結起來即可。例如若模板中的型別需要設值(assignment)以及拷貝建構(copy-construct)，可以使用<code>requires Assignable<T>&&CopyConstructible<T></code>。

== 定義概念 ==
定義 concept 的方式如下：

<source lang="cpp">
auto concept LessThanComparable<typename T>
{
  bool operator<(T, T);
}
</source>

此處為 concept <code>LessThanComparable</code> 宣告，說明若型別 <code>T</code> 有一個雙參數的函式：<code>operator <</code>，且函式傳回值為<code>bool</code>，則型別 <code>T</code> 滿足 concept <code>LessThanComparable</code>。函式 <code>operator <</code> 可以是全域或是成員函式。

C++0x 為了避免 concept 的誤用，除非使用者顯式指明，編譯器不會主動認定型別符合 concept (隱式套用 concept)。為了避免繁瑣的指明，此處關鍵字<code>auto</code> 代表只要型別帶有 concept 中指定的操作，它即是符合該 concept 的一個型別。若沒有加上<code>auto</code>，則必須使用<code>concept_map</code>來指明型別符合特定的 concept。

concept 也可以包含多種型別。例如以下的 concept <code>Convertible</code>，表示型別 <code>T</code> 可轉換為 <code>U</code>。

<source lang="cpp">
auto concept Convertible<typename T, typename U>
{
  operator U(const T&);
}
</source>

在模板中使用涉及多型別的 concept，必須使用泛用形式：

<source lang="cpp">
template<typename U, typename T> requires Convertible<T, U>
  U convert(const T& t)
  {
    return t;
  }
</source>

Concept 可以是其他 concept 的構件。在下例中，<code>InputIterator</code> 的第一個參數 <code>Iter</code> 必須符合 concept <code>Regular</code>：

<source lang="cpp">
concept InputIterator<typename Iter, typename Value>
{
  requires Regular<Iter>;
  Value operator*(const Iter&);
  Iter& operator++(Iter&);
  Iter operator++(Iter&, int);
}
</source>

另一方面，concept 之間也能帶有衍生關係。如同類的繼承，滿足衍生 concept 的型別也必須滿足基底 concept，語法上也和類繼承相同：

<source lang="cpp">
concept ForwardIterator<typename Iter, typename Value> : InputIterator<Iter, Value>
{
  // 在此加上 ForwardIterator 的其它要求
}
</source>

Concept 中也可宣告關聯型別(associated type)，以 typename 宣告。模板使用 concept 時，模板引數必須要提供相關型別的定義。

<source lang="cpp">
concept InputIterator<typename Iter>
{
  typename value_type;
  typename reference;
  typename pointer;
  typename difference_type;
  requires Regular<Iter>;
  requires Convertible<reference, value_type>;
  reference operator*(const Iter&); // 解參考
  Iter& operator++(Iter&); // 前置遞增
  Iter operator++(Iter&, int); // 後置遞增
  // ...
}
</source>

== 映射概念 ==
<code>Concept map</code> 可以將型別"-{映射}-"到特定的 concept，告知編譯器使用的型別是"如何"符合 concept。

<source lang="cpp">
concept_map InputIterator<char*>
{
  typedef char value_type ;
  typedef char& reference ;
  typedef char* pointer ;
  typedef std::ptrdiff_t difference_type ;
};
</source>

這個 <code>concept_map</code> 定義 <code>char*</code> 符合 concept <code>InputIterator</code>，並且一一聲明所需的關聯型別。

<code>concept_map</code> 可以宣告成模板，下面的例子聲明所有的指針型別都符合 concept <code>InputIterator</code>。

<source lang="cpp">
template<typename T> concept_map InputIterator<T*>
{
  typedef T value_type ;
  typedef T& reference ;
  typedef T* pointer ;
  typedef std::ptrdiff_t difference_type ;
};
</source>

<code>concept_map</code> 可以作為一個迷你型別，在其中置入函式的定義與其它用來定義類的相關構件。

<source lang="cpp">
concept Stack<typename X>
{
  typename value_type;
  void push(X&, const value_type&);
  void pop(X&);
  value_type top(const X&);
  bool empty(const X&);
};

template<typename T> concept_map Stack<std::vector<T> >
{
  typedef T value_type;
  void push(std::vector<T>& v, const T& x) { v.push_back(x); }
  void pop(std::vector<T>& v) { v.pop_back(); }
  T top(const std::vector<T>& v) { return v.back(); }
  bool empty(const std::vector<T>& v) { return v.empty(); }
};
</source>

在這裡，concept <code>Stack</code> 定義了需要的函式以及關聯型別，而 <code>concept_map</code> 定義如何以 <code>std::vector</code> 實現底層的操作，每個 concept Stack 裡的函式都可以轉接到 <code>std::vector</code> 的函式調用。因此，<code>concept_map</code>能在不改變原型別(類別)的定義下，
完成介面轉換(interface adaptation)。

最後值得一提的是，一些模板的要求可以使用編譯期斷言(static assertion)。它們可以驗證一些模板的要求，不過實際上是針對不同的問題。

== 公設 ==
C++0x 提供了公設 (axiom) 用來表達概念的語意屬性。舉例來說，我們可以用公設 <code>Associativity</code> 來定義概念 <code>Semigroup</code>:

<source lang="cpp">
concept Semigroup< typename Op, typename T> : CopyConstructible<T>
{
  T operator()(Op, T, T);

  axiom Associativity(Op op, T x, T y, T z)
  {
    op(x, op(y, z)) == op(op(x, y), z);
  }
}
</source>

編譯器可以利用公設所表達的語意做些原本不被允許的優化，因為這些優化可能會在程序可見的行為上有副作用 (其除了少數的例外，其中之一是回返值優化 (RVO))。在上述的例子中，編譯器可能會重新安排 <code>operator()</code> 呼叫的次序。前提是 <code>Op</code> 和 <code>T</code> 與概念 <code>Semigroup</code> 有映射關係。

公設也能在軟體驗證，軟體測試以及其它程序分析和轉換上有所幫助。

== 參考資料 ==
<references />
== 外部連結 ==
*[http://bartoszmilewski.wordpress.com/2010/06/24/c-concepts-a-postmortem/ C++ Concepts: a Postmortem]

[[Category:C++|Category:C++]]