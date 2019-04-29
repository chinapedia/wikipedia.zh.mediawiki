{{NoteTA
|T = zh-cn:比较C#和Java; zh-tw:比較C#和Java;
}}
{{RoughTranslation}}

本文对比[[C_Sharp|C#]]与[[Java_(编程语言)|Java编程语言]]。
因为这两种语言都具有[[垃圾回收_(计算机科学)|自动垃圾回收]]以及[[JIT|运行时编译执行]]的特点，并且他们的语法都是继承自[[C语言|C语言]]/[[C++|C++]]，因此二者有很多相似之处。

但由于C#也被描述为一个C++和Java的混合体，并添加了一些新特性，引入了一些变化，因此C#和Java自然也有很多不一样的地方。

这个条目描述了二者总体上的相似性，并列举了二者的不同点。

== 语言 ==
=== 对象处理 ===
C#和Java都被设计成一个使用[[动态调度|动态调度]]的类似于[[C++|C++]]语法的完全的[[面向对象编程|面向对象]]语言。（C++又是源自于[[C语言|C]]）。但是，这两种语言都不是c或者c++的一个扩展集。C#和Java都使用[[垃圾回收_(计算机科学)|垃圾回收]]作为一种回收内存资源的手段，而不是直接的释放内存。C#和Java都包含[[线程|线程]]同步机制作为他们语法的一部分。

==== 引用 ====
C#允许[[指针|指针]]的有限功能的使用，指针和运算指针在一个操作的环境中是存在潜在的不安全性的，因为他们的使用可以避开对象的一些严格访问规则。C#中使用指针的代码段或者方法的地址要用unsafe关键字进行标记，这样，这些代码的使用者就会知道这个代码相比其他的代码而言是不具有安全性的。编译器需要unsafe关键字时将使用此代码的程序转换成是允许被编译的。一般来说，不安全代码的使用可能是为了非托管的[[API|API]]（应用程序编程接口）的更好[[互用|互用]]，或者是为了（存在内在不安全性的）系统调用，也有可能是出于提高性能等方面的原因。而Java中不允许指针或者算术指针的使用。

=== 数据类型 ===
java和C#语言都有原始数据类型的概念，C#/.NET语言中支持的原始数据（所有的，除了string类型）都是值类型。但C#比java支持更多的原始数据类型，比如整型和十进制浮点数，尤其是java缺少无符号的BYTE类型，而C#的BYTE类型默认是无符号的。在两种语言中string其值都是不可改变的一个类，但是特殊的是C#为其提供了特殊的构造方法，同时C#还可以像值类型一样的使用string的值就而不需要进行拆箱操作。
既允许自动装箱和拆箱，把它们从对象类型转换为原始数据。实际上，这使得原始类型成为对象类型的子类型。在C＃中这也意味着，原始类型可以定义方法，如覆盖的对象的ToString()的方法。在Java中，单独的原始包装类提供这种功能。在Java中原始值不含隐式装箱和一个显示的类型转换都需要一个实例称为原始值的((Integer)42).toString()而不是C#中调用实例 42.ToString()。另一个不同之处在于，java使大量使用装箱类型(见下文)，这样可以让一个隐式拆箱转换(在C ＃这需要一个类型转换)。由于这些隐性拆箱转换可能会抛出空指针例外,现代集成开发环境和编译器可以配置为突出它们。
<!--==== Value types ====-->
值类型
C#允许程序员用关键字<code>struct</code>创建用户自定义的值类型([[value_type|value type]])。
从程序员的角度来讲，它们可以被看做轻量级的类。

不同于一般类，而像标准基本类，这种值类型被分配在栈内存([[stack-based_memory_allocation|stack]])而不是堆内存([[heap-based_memory_allocation|heap]])。
结构体通常有一系列的限制，因为结构体没有空值的概念并且可以在数组中无需初始化而直接使用，这种类型也有必须用0来初始化内存空间的默认构造函数。
<!--The programmer can only define additional constructors with one or more arguments.-->
程序员只能定义另外的带有一个或多个参数的构造函数。
 <!--This also means that structs lack a [[virtual_method_table|virtual method table]], and because of that (and the fixed memory footprint), they cannot allow inheritance (but can implement interfaces).-->

这也意味着结构体缺少一个虚方法表，正因为这样（还有固定的内存空间），它们不允许继承（但可以实现接口）。

==== 数组 ====
数组和集合类同样在语法中给出了重要意义，感谢基于迭代器的预声明循环。在C#里一个数组反映为一个数组类的对象，而在JAVA每个数组都是一个直接的对象集的子集（但是可以映射为一个以它真正的成员类为父类的一个数组），并且不实现任何的集合界面。C#拥有真正的多维数组，如同Java中可用到的数组的数组（在C#中通常称为锯齿数组）。多维数组可以因为增强位置（就像有一个单一的指示器解除参照，代替数组的每一维作为锯齿数组的容器）在某些情况下增强性能。另一个优点是整个多维数组可以用单一的new操作符申请而赋值，而锯齿数组需要对每一维进行循环和赋值。注意，尽管Java为分配多维的锯齿数组提供依据句法的整齐的数组长度（在C#术语中是一个矩形数组），循环和多样的分配被虚拟机完成不需要外在的来源。

==== 内部类 ====
java与C#都允许设置内部类，即在一个类内部定义的另一个类。在java中，这些内部类可以访问外部类的静态和非静态成员（除非这个内部类定义为静态的，在这种情况下只能访问外部类的静态成员）。局部内部类可以定义在一个方法中并访问这个方法中声明为final类型的局部变量，匿名局部类允许构造类的实例用来重写类的方法。

C#也提供内部类，与Java不同的是它需要外部类的非静态成员的一个明确引用。同时C#提供匿名类作为一个结构用来访问局部变量和方法（参见[[#事件处理|事件处理]]）。局部类和匿名类不能被访问。

==== 部分类 ====
C#使用''部分类''允许一个类的定义分割在几个源文件中。每一个部分必须用关键字<code>partial</code>标记。作为一个单一的汇编的部分所有的部分都必须提交给编译器。每个部分可以引用其它部分的成员。每个部分都可以实现接口，并且某个部分可以定义一个基类。这个功能在代码生成时非常有用，也就是一个代码发生器提供一部分代码，开发商提供另一部分代码，两种代码在一起编译。因此开发商可以编辑他们的部分代码而不用冒着代码发生器在以后覆盖这部分代码的危险。和类扩展机制不同，部分类在它的部分之间允许循环依赖，因为它们在编译的时候都保证被解决。Java没有类似的概念。

==== 泛型 ====
泛型编程

现在的编程语言都支持泛型编程，但它们却采用了不同的实现方式。

[[Java中的泛型|Java中的泛型]]仅是语言层面上的一种结构，它们只能通过编译器来实现。生成的类文件中所包含的类签名仅由元数据组成（允许编译器对这些新类进行反编译）。运行时并不知道通用类型系统，这意味着JVM只需要进行一小部分的更新便可处理新的类格式。

为了实现这个目标，编译器用泛型类型的上界来替换它们，并且在用到这些泛型的各个地方适当地插入一些“角色”。结果生成的字节码将不包含任何对这些泛型类型的引用或将它们作为参数。这种实现泛型的技术被称作[[类型擦除|类型擦除]]。这意味着实际上的类型的信息在运行时不可用，并且强行加入了一些限制，例如不能创建泛型的新实例或数组。(参见[[Java中的泛型|Java中的泛型]])。

C#采用了另一种实现方式。它对泛型的支持是集成在虚拟执行系统中的，并且最早出现在.NET2.0中。这门语言后来就发展为在执行系统中支持基本泛型的前端。而在Java中，编译器提供了静态类型安全检查，但是，加之又有即时编译器（JIT）[[加载|加载]]来核实其正确性。关于泛型类型的信息在运行时完全被保护起来了，并且允许完全的反射和实例化泛型类型。

Java不允许用基本数据类型来声明为泛型类，然而C#却允许不管是引用类型还是值类型被声明为泛型，包括基本数据类型。Java却允许被封装的类型作为泛型类的类型参数来使用(例如：用List<Integer>代替List<int>)，但是由于所有这一类的值需要在堆上分配而需付出一定的“代价”。
在Java和C#两者中，泛型的定义都使用了不同的引用类型来分享等效的底层代码，但是对C#来说[[公共语言运行时|公共语言运行时]]（CLR）为值类型的实例化动态的生成优化代码。

=== 符号和特殊功能 ===
==== 特殊功能关键字 ====
{| class="wikitable"
! 关键字 !! 功能，实例
|-
| <code>checked</code>, <code>unchecked</code> || 在C#里, <code>checked</code> 声明块或表达式可以在运行时检查算术的溢出。
|-
| <code>get</code>, <code>set</code> || C#实现属性作为语言语法的一部分，而且选用相应的<code>get</code> 和<code>set</code> 访问器, 而Java的访问方法, 不是一种语言功能，而是基于方法命名公约的编码方式。
|-
| <code>goto</code> || C#中支持goto关键字。goto有时候是有用的, 举个例子，实现有限的状态机或者生成的代码, 但是通常建议使用更加合理控制流程的结构化方法(见goto语句的评论)。 Java 允许使用breaks和continues弥补了goto语句的的许多用途。
<source lang="csharp">
switch(color)
{
    case Color.Blue:
         Console.WriteLine("Color is blue"); break;
    case Color.DarkBlue:
         Console.WriteLine("Color is dark");
         goto case Color.Blue;
    // ...
}
</source>
|-
| <code>out</code>, <code>ref</code> || C#支持输出参数和引用参数。这使得c#可以从一个方法返回多个值或者通过引用传递多个值。
|-
| <code>strictfp</code> || Java 使用关键字 <code>[[strictfp|strictfp]]</code> 确保跨平台时浮点运算的结果保持不变。
|-
| <code>switch</code> || 在C#里, switch 语句也操作于string型和long型，但是只允许失败的空白语句。 Java switch 语句在Java7之後才支援操作strings；不能操作于<code>long</code> 的原始类型 但是能通过所有的空白语句(不包括那些含有 '<code>break</code>'的语句)。
|-
| <code>throws</code> || <!--Java requires every method to declare the checked exceptions or superclasses of the checked exceptions that it can throw. Any method can also optionally declare the unchecked exception that it throws. C# has no such syntax.-->Java中要求每个方法都要声明它能抛出检测异常或者检测异常的父类。任何方法也可以随意的定义它所抛出的非检测异常,C#中却没有这样的语法规则。
<source lang="Java">
public int readItem() throws java.io.IOException
{
    // ...
}
</source>
|-
| <code>using</code> || <!--C#'s <code>using</code> causes the <code>Dispose</code> method (implemented via the <code>IDisposable</code> interface) of the object declared to be executed after the code block has run or when an exception is thrown within the code block.-->C#中的using指令使得对象的Dispose方法（通过IDisposable接口被执行）定义为在代码块执行之后或者在代码块之中的异常被抛出时才被执行。
<source lang="csharp">
//创建一个小文件"test.txt",写一个字符串,
//... 并且把它关闭（即使发生了异常）
using (StreamWriter file = new StreamWriter("test.txt"))
{
    file.Write("test");
}
</source>
|-
| <code>yield</code> || C#语言中允许使用yield关键字来表示迭代器。在Java中，迭代器只能用类（可以是匿名的）来定义，且需要很多的样板代码。下面是一个能够读取可迭代的输入（可以是数组）并且返回所有偶数成员的迭代器的例子。

<source lang="csharp">
public static IEnumerable<int> GetEven(IEnumerable<int> numbers)
{
    foreach (int i in numbers)
    {
        if (i % 2 == 0)
            yield return i;
    }
}
</source>
|}
<!-- /T3 -->
<!-- T5 -->

==== 回调和事件处理 ====

=== 数值应用 ===
多种语言特色的存在是为了充分的支持应用程序在数学和金融领域计算。<ref name="computation">{{Cite web |url=http://www.pds.ewi.tudelft.nl/pubs/papers/scicomp01.pdf |title=Java for Scientific Computation: Prospects and Problems |access-date=2009-05-01 |archive-url=https://web.archive.org/web/20070922004052/http://www.pds.ewi.tudelft.nl/pubs/papers/scicomp01.pdf |archive-date=2007-09-22 |dead-url=yes }}</ref>在这一类中，Java提供关键字[[strictfp|strictfp]]可以在代码段中使浮点运算严格执行。这可以保证运算在所有的平台上都返回相同精确的结果。
与此不同C#为确保十进制小数浮点运算准确，在 <code>decimal </code>类型中内嵌了这种机制。但在二进制小数浮点运算中舍弃了这种机制（<code>float</code>, <code>double</code>）。
<!-- Such binary representations are not suited to accurately represent decimal numbers and hence introduce rounding errors. For financial applications, an accurate decimal type is essential. -->
在二进制所有的类型中描述十进制数因为不精确会存在舍入误差。所以在金融应用方面十进制小数类型的精确显得很重要。
<!-- The {{Javadoc:SE|java/math|BigDecimal}} class also provides such characteristics for Java. <code>BigDecimal</code> and {{Javadoc:SE|java/math|BigInteger}} are types provided with Java that allow arbitrary-precision representation of numbers. -->
Java中{{Javadoc:SE|java/math|BigDecimal}}类也提供了这些特性。任意精度小数算法 (<code>BigDecimal</code>) 和任意精度整数算法 ({{Javadoc:SE|java/math|BigInteger}} ) 的类为其提供任意精度的数值运算。
<!-- The current release of the .NET framework (3.5) does not currently include such classes, although third party implementations exist (see [[Arbitrary-precision_arithmetic#Arbitrary-precision_software|Arbitrary-precision arithmetic]]). -->
尽管有第三方实现了这些类，但是.NET框架(3.5)的现行版本当前并没有提供这些。（参见[[Arbitrary-precision_arithmetic#Arbitrary-precision_software|Arbitrary-precision arithmetic]]）
<!-- In Java there is no way to provide the same level of integration for library-defined types such as <code>BigDecimal</code> or [[complex_number|complex number]]s as there is for the primitive types. For this purpose, C# provides the following: -->
Java不能为库定义类型（高精度小数、复数等原始类型）提供一个统一标准，为了达到这个目的，C#提供了如下内容：
<!-- * [[Operator_overloading|Operator overloading]] and indexers providing convenient syntax (see below). -->
* 能够提供方便语法的运算符重载和索引（看下面）。
<!-- * Implicit and explicit conversions; allow conversions such as exist for the built-in <code>int</code> type that can implicitly convert to <code>long</code>. -->
* 隐性和显性转换；允许诸如嵌入式int 类型隐性转换为long类型的存在。
<!-- * Valuetypes and generics based on valuetypes; in Java every custom type must be allocated on the heap, which is detrimental for performance of both custom types and collections. -->
* 值类型和基于值类型的属性；在Java中每个常规类型必须被存放在堆栈中，它对常规类型和存储类型的性能是不利的。
<!-- In addition to this, C# can help mathematic applications with the <code>checked</code> and <code>unchecked</code> operators that allow to enable or disable run-time checking for [[arithmetic_overflow|arithmetic overflow]] for a region of code. It also offers rectangular arrays, that have advantages over regular nested arrays for certain applications.<ref name="computation" /> -->
除此之外，C#能用checked和unchecked运算符帮助数学计算，当在一段代码中出现算数溢出时它能够检测出是否能够继续运行。它也提供在内嵌数组的某些应用方面有优势的矩阵。<ref name="computation" />
<!-- /T1 -->
<!-- T2 -->

==== 运算符重载 ====
相比Java，C#包含了许多可数的便利。其中，例如运算符重载、用户自定义类型，许多都被大批的C++程序员所熟悉。
它还具有“外在的成员实现”，这样可以让一个类明确的实现一个接口中的方法，与自己类中的方法分离。或者为分别来自两个接口中，具有相同函数名和签名的函数提供不同的实现。
C#包含了“索引器”，它可以当作是一种特殊的运算符（像C++中的<code>operator[]</code>），或者是用
<code>get</code>/<code>set</code> 访问器来访问类属性。一个索引器用<code>this[]</code>来标明，
并且需要至少一个索引参数，该参数可以为任意类别：
<source lang="csharp">
myList[4] = 5;
string name = xmlNode.Attributes["name"];
orders = customerMap[theCustomer];
</source>
Java没有提供运算符重载是为了阻止特征滥用，还有为了语言的简单。<ref>[http://www.cafeaulait.org/1998august.html August 1998 Java News]</ref>
C#允许运算符重载（以确定的几个限制来确保逻辑上的一致为条件），如果小心地使用，可以使代码更加简洁和易读。<!-- /T2 -->
<!-- T3 -->

<!--=== Methods ===
''Methods'' in C# are non-[[Virtual_function|virtual]] by default, and have to be declared virtual explicitly if desired. In Java, all non-static non-private methods are virtual. Virtuality guarantees that the most recent [[Method_overriding_(programming)|override]] for the method will always be called, but incurs a certain runtime cost on invocation as these invocations cannot be normally [[Inline_expansion|inlined]], and require an indirect call via the [[virtual_method_table|virtual method table]]. However, some JVM implementations, including the Sun reference implementation, implement inlining of the most commonly called virtual methods.-->

=== 方法 ===
在C#中，方法在默认状态下是非虚拟的，如果希望得到一个虚方法则必须明确地用 virtual 修饰符进行声明，而在Java当中，所有非静态、非私有的方法都是虚方法。虚方法保证被调用的总是该方法最近被重写的那个实现。但是，由于各个重载方法之间不能被正常地进行内联，而使得在方法调用上需要花费一个相当长的运行时间，并且需要通过虚方法列表进行间接的调用。然而，包括Sun公司所推荐的实现方法在内的一些Java虚拟机的实现方法，则会对最普遍被调用的那些虚方法执行内联。在java中，方法在默认状态下是虚拟的。（尽管他们能通过使用“final“修饰符来密封以使他不允许被覆盖）。没有什么办法让subclass或derived class以同样的名字定义一个新的、无关联的方法。 这就会产生一个问题，即当一个基类由一个不同的人定义，这时就有可能出现一个与派生类中已经定义过的一些方法有着相同的名字和标签的新的版本的方法定义。在Java中，这种情况将意味着派生类中的同名方法会隐式的重写基类中的方法，尽管这种结果不是所有设计者的真正意图。为了防止这种版本问题，C#中要求将派生类中需要重写虚方法的部分进行显示的声明。 如果一个方法需要被重写，那么必须指定override修饰符。如果不希望进行方法重写，而且类的设计者仅仅希望引出一个新的方法以影射旧的方法，那么就必须含有new关键字。New关键字和override关键字也避免了由于基类中的protecte方法或public方法在它的某一个派生类中被使用时所带来的问题。Java中重新编译将导致编译器把派生类中的这种方法当做是基类方法的重写，而这可能并不是基类的开发者想要的。 

而C＃编译器将会把这种方法默认为new关键字已经被指定，但仍会对这种结果发出警告。为了部分地容纳这些版本问题， Java 5.0中引入了@override注释，但为了保护它的向后兼容这种做法不会被当作是强制性的，所以它并不能阻止上述意外的重写情况。然而对于C＃中的override关键字，它能有助于确保基类中具有相同签名的方法仍然存在，并且能被正确的重写。

==== 显式接口实现 ====
如果在多个接口中有一个方法（或C ＃中的属性）具有相同名称和签名，当一个类在实现这些接口时这些重名的成员就会产生冲突。一个解决方法是通过为所有接口实现一个默认共同的方法。如果必须要分开来实现（因为这个方法确实要实现某个特殊的目的，或者是因为各个接口的返回值不一样）。C#显示接口的实现将解决这一问题。在java中消除命名冲突的问题只能通过重构或者是定义更多的接口来避免。C#的显示接口实现还能隐藏底层基础的类和接口，因此使得减少类和接口的复杂性。

==== 開包 ====
当一个函数作为一个参数来传递并为后面的程序调用，这时候会出现一个问题：当这个方法调用了它自己作用域内的变量时会怎样呢？C#中有真正的開包功能，方法的引用会完全的获得它自己作用域范围内的变量。Java中，匿名内部类只能调用到作用域内的常方法，想要调用和更新内部类的话，就必须通过开发人员的手工声明额外的间接的父类来实现。

==== Lambdas和表达树 ====
C#中的一个特殊类型称" lambdas"。 他们不是方法也不可能构成类接口的部分; 他们只是在[[功能模块|功能模块]]中。 在lambda函数顶部可以定义的一个详细结构体称为表达树。 不管他们是被当成执行函数还是数据结构都起决于编辑器类型，并且不管什么类型变量或参量都要赋值。 Lambdas和表示树在[[LINQ|LINQ]]中都是重要角色。 Java中没有以lambdas或表达树为特色的; 它的主要机制和方法定义是匿名内部类句法。

==== 部分方法 ====
与"部分类"相关 C#允许部分方法在部分类之内指定。 一个部分方法是方法的一个故意声明并且在签名上有一定的约束。 这些约束指定，如果任何类成员没有被定义，那么可以安全地删除。 这个特点允许代码提供大量的监听点(像GoF设计模式中的"模板方法")而不用花费多余时间，如果另一个类成员在编译时没有引用它们。而 Java没有对应的概念。

<!-- /T5 -->
<!-- T1 -->

==== 扩展方法 ====
用一个特殊的''this''指定在一个方法的第一个参数C#允许这个方法扮演成第一个参数类型的一个成员函数。这个外来类的“扩展”是完全句法的。这个扩展方法需要变为静态的，而且定义在一个完全的静态类中。它必须服从在外部静态方法上的任何限定，因此它不能摧毁对象封装。这个“扩展”仅仅是在静态宿主类的命名空间被引进的范围内是活跃的。在java里面，相同的效果可以通过一个另一个类的一般方法得到，但语法将是一个函数调用，而不是方法调用类的C#语法扩展。

==== 发生器方法 ====
发生器方法是一个C#方法 ，这个方法被声明为返回<code>IEnumerable</code>,<code>IEnumerator</code>接口或者这些接口的一般版本，该方法可以用 <code>yield</code>语法实现。它是一个无限的表现形式, 编译器生成的补遗集，可大大减少所需的代码遍历或生成序列；虽然代码只是通过编译器生成。这个特征过去也经常被用作实现无穷大的序列，就像[[斐波那契数列|斐波那契数列]]。java是没有相应的概念。

=== 条件编译 ===
与Java不同，C#使用预编译指令实现了条件编译的功能。它还提供了条件属性，使方法只有在定义了编译常量的时候才被执行。这样一来，只有在定义了DEBUG常量时，Debug.Assert()方法才会执行，断言成为了framework的特色。从1.4版本开始，Java开始提供断言，默认情况下在运行时被关闭，但也可以在调用JVM时使用 "-enableassertions" 或者 "-ea" 打开。

=== 名字空间和源文件 ===
C#的命名空间和C++类似，但不同于Java的包机制，C#命名空间不会以任何方式依赖于源文件的位置，这与Java不同，Java的常规结构要求源文件的位置必须和包目录结构相符。
这两种语言都允许引入类库( 例:import java.util.* ,Java方式)，在引入类库后，使用类时就可以直接通过类名引用。不同名字空间或包中可以具有相同名字的类，这样类在使用时可以通过全限定名来引用，或者通过不同的名字只引入必要的类。基于这个问题，Java允许引入单个类(例:import java.util.List)。C#允许在引入类库时 使用语句: using Console = System.Console来为一个类库定义一个新名，它同样允许以using IntList = System.Collections.Generic.List<int>的形式，引入特殊类库。

Java有允许使用某些或所有，具有较短名字的静态方法/领域的静态import句法在类中(例如，允许foo(bar)可以从另一个类中被静态的引进).C#有静态类句法(不与Java的静态内在类混淆),制约类只包含静态方法。 C# 3.0介绍的[[引申方法|引申方法]]允许用户静态地增加方法到类型(比如，允许foo.bar 的地方可以是研究foo的种类的一个引进的引申方法)。 

[[Sun_Microsystems|Sun Microsystems]] 软件公司的Java编译器要求，源文件的文件名必须匹配在它里面的唯一的公开类，而C#允许在同一个文件的多公开类，并且投入制约。 C# 2.0和以后的版本允许类定义被分割成几个文件，通过使用在原始代码的关键字partial。

=== 异常处理 ===
Java支持检查异常(checked exception)。C＃中只支持非检查异常情况。检查异常强制程序员要么在方法中声明一个异常抛出，要么用try-catch来捕获异常。检查异常可以有助于良好的编程习惯，以确保所有的错误都得到处理。但是[[Anders_Hejlsberg|Anders Hejlsberg]]，C#语言首席设计师，和其他人争辩说，他们都在一定程度上对Java进行了拓展但是它们没有被证明是有价值的除了几个程序中的小例子。有一个评论介绍在检查异常时鼓励程序员使用空的catch块,安静的吃掉异常而不是让异常传播到更高水平的常规的异常处理：catch (Exception e) {}.另一种对于检查异常的评论说一个新方法的执行可能会引起意想不到的检查异常被抛出，这是一个合同突破性变化.这可能发生在一个方法实现一个接口或者当一个方法的基本实现改变时，此接口仅声明有限的异常。为这种意料之外的的异常被抛出,一些程序员简单的声明这种方法能抛出任何类型的异常（“抛出异常”），这使检查异常的目的无法实现。不过在某些情况下，异常链（[[exception_chaining|exception chaining]]）能用于代替,捕获异常后再抛出一个异常异常.例如,如果一个对象访问数据库而不是文件时被改变,那么可以捕获 {{Javadoc:SE|java/sql|SQLException}}异常并且作为{{Javadoc:SE|java/io|IOException}}异常重新抛出. 因为调用者也许并不需要知道对象内部的工作方式。

在处理<code>try-finally</code>的声明时两种语言也是有差别的。即使<code>try</code>块包含像<code>throw</code>和<code>return</code>的control-passing语句，finally块也总是要执行。在Java中，这可能导致意外的行为，如果try块最后有<code>return</code>语句返回一个值，然后执行后的<code>finally</code>块也会有<code>return</code>语句返回一个不同的值。 C#利用禁止任何像return或者break的control-passing语句来解决这一问题。
<!--A common reason for using try-finally blocks is to guard resource managing code, so that precious resources are guaranteed to be released in the finally block. C# features the <code>using</code> statement as a syntactic shorthand for this common scenario, in which the <code>Dispose()</code> method of the object of the <code>using</code> is always called.-->使用try-finally 块的普遍原因是为了保护管理代码的资源，所以珍贵的资源被保证在finally 块中发布。作为句法速记为共同的设想的using语句在C#中处于显著地位,其中using的对象的Dispose()方法总是被调用。

==== Finally块和未捕捉的异常 ====
(C# 派生的异常特点)对CLI（公共语言基础）的ECMA（欧洲电脑厂商协会）标准指出在堆栈的两次搜索中处理异常。[http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-335.pdf ECMA-355 4th Edition 12.4.2.5 Overview of exception handling]首次通过尝试找到一个匹配的 catch 块，如果没有找到就终止该程序。只有当找到匹配的 catch 块时，才会在第二步执行，从而运行干预的finally块。这使得问题在程序状态还没第一次被finally块修改前被诊断；它也消除了当程序在未知状态下，finally块可能有副作用的风险（例如，外部数据的损坏或进一步引发的异常）。

Java语言规范中指出finally块中的代码总会执行即使异常没有被捕获，并且举出实例代码演示期待的结果。<ref name="finallyjava">[http://java.sun.com/docs/books/jls/third_edition/html/statements.html#14.20.2 Java Language Spec. 3rd Edition 14.20.2 Execution of try-catch-finally]</ref>

=== 底层的代码 ===
[[Java_native_interface|Java Native Interface]] (JNI)的特征是允许Java代码调用非Java代码。然而，JNI要求被调用的代码必须遵循Java提供的一些在类型和名称上的约定。这种方法是为了适应Java和其他代码更好的交互。这些代码必须是非Java代码，常常是C或者C++代码。[[JNA|JNA]]提供一种更加方便的Java代码与其他代码的交互，仅仅需要写一些Java编写的接口代码，但是性能会付出一点代价。

另外，第三方类库为JAVA－COM提供桥接，像[http://jacob-project.sourceforge.net/ JACOB] ([[自由软件|自由软件]])，[http://j-integra.intrinsyc.com/products/com/ J-Integra for COM] ([[专有软件|专有软件]])

.NET平台调用([[Platform_Invocation_Services|P/Invoke]])通过允许从C#调用微软称之为[[不受托管代码|不受托管代码]]提供同样的的功能，通过元数据属性程序员可以精确的控制如何调用参数和结果，因此可以避免额外编译代码的需要。平台调用允许几乎完全的对程序的API的访问(像Win32或POSIX)但是限制对c++类库的访问。另外，.NET框架也提供一个.NET－COM网桥，允许对COM组件的的访问就像是访问本地的.NET组件。

C＃中还允许程序员禁用正常类型检查和CLR中其他的安全保证功能 ，这样就使得指针变量的使用成为可能。当此功能被使用时，程序员必须用unsafe关键字将相应的代码段进行标记。JNI ，P/Invoke，和“unsafe”的代码段是相当冒险的部分，它揭露了可能的安全漏洞和应用不稳定。使用unsafe的一个优势是，通过P/Invoke或JNI运行于托管运行环境中的代码是让程序员在比较熟悉的C ＃环境中继续工作以完成某些任务，否则将需要调用非托管代码。使用不安全代码的程序或程序集必须通过进行特殊的转换才能被编译并且将依此被标记。这使得运行时环境在潜在地执行有危险的代码前要采取特别的预防措施。

== 参考文献 ==
{{Reflist|32em}}

== 外部連結 ==
* [http://www.ondotnet.com/pub/a/dotnet/2001/06/14/csharp_4_java.html Contrasting C# and Java Syntax]
* [http://www.javacamp.org/javavscsharp/ Java vs. C# - Code for Code Comparison]
* [http://www.osnews.com/story.php?news_id=5602 Nine Language Performance Round-up]
* [https://web.archive.org/web/20090415190024/http://www.csharphelp.com/archives/archive96.html Java and C-Sharp Compared]
* [[Microsoft_Developer_Network|MSDN]]: [http://msdn.microsoft.com/en-us/library/ms228602.aspx The C# Programming Language for Java Developers]
* [http://www.ecma-international.org/publications/standards/Ecma-334.htm Standard ECMA-334 C# Language specification]
* [http://java.sun.com/docs/books/jls/ Java Language Specification (Sun)]
* [https://web.archive.org/web/20090504053246/http://www.geeks.ltd.uk/Knowledgebase/Compare-c-sharp-java.html 31 Differences between C# and Java]

{{-}}
{{DotNET}}

[[Category:程序语言比较|Category:程序语言比较]]
[[Category:Java|Category:Java]]