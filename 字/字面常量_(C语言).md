{{TA
|G1=IT
}}
'''字面常量'''（literal constant），是[[C程序设计语言|C程序设计语言]]与[[C++语言|C++语言]]的词法上的概念（lexical conventions），<ref>[[C++11|C++2011]] ISO/IEC 14882 §2.14 Literals</ref>是指源程序中表示固定值的符号（token）。<ref>C++11标准§2.14.1的脚注21：The term “literal” generally designates, in this International Standard, those tokens that are called “constants” in ISO C. 即C语言的constants与C++的literal是一码事，属于词法分析时的token。</ref> 

下述内容遵从[[C11|C11]]与[[C++11|C++11]]语言标准。

==整型字面常量 ==
包括下述的数值进制：
*10进制： 如1234;
*8进制：如0373;
*16进制：如0x2a7;
*2进制（从[[C++14|C++14]]开始）：如0b101; 或者0B0101;
整型字面量转化为整数类型表示，依照下述顺序：<ref>C99标准，第6.4.4.1节，条款5</ref>
*int
*unsigned int
*long int
*unsigned long int
*long long int
*unsigned long long int
其中，10进制表示的字面量仅考虑有符号的整数类型；而8进制或16进制的字面量先考虑能否用有符号的整数类型表示，如不能再考虑能否用同样长度的无符号整数类型表示。例如，字面量0x87654321，这是一个正值，用4字节长的int无法表示，编译器就会自动选用unsigned int来表示该字面量。 

整型字面量可以使用后缀u U ul UL ull ULL明确表示各种无符号整型；使用后缀l L ll LL表示该字面量至少为long或为long long型。 

[[C++14|C++14]]引入了千分位分隔符。例如：
     auto integer_literal = 1'000'000;

C++14还引入了二进制字面量，例如：
     auto perm = 0b100110111;

==浮点型字面常量==
包括下述的数值进制：
*10进制：如 2.3  2e-3  2.e-5  2.12e15等。如果不是[[科学计数法|科学计数法]]形式，就必须有小数点，小数点前或后的数字可省略；
*16进制（C语言特有，C99引入）：如 0x1p10（值为1024<sub>10</sub>） 0x1.0004p10（值为1024.0625<sub>10</sub>）等。

没有后缀的浮点型字面量具有double类型。使用后缀 f F l L表示float或long double类型。

[[C++14|C++14]]引入了千分位分隔符。例如：
     auto dd = 1'234.567'8;

==字符型字面常量==
普通的字符字面量，如：'a' 。字符字面量的值等于该字符在[[执行字符集|执行字符集]]（execution character set）中的编码值。实际上，编译器在token分析阶段，通常就会把字符与字符串在源文件中的编码串转换为指定或者执行字符集的编码串。例如，源文件是[[Latin-1|Latin-1]]编码，执行字符集为[[utf-8|utf-8]]，则<code>char c='ö';</code>中的字符值将被编译器从Latin-1编码的单字节的0xD6自动转为utf-8编码的双字节的0xC3B6，在[[目标文件|目标文件]]与[[可执行文件|可执行文件]]中字符c的值是'ö'的utf-8编码值的最后一个字节值即0xB6。

需要注意的是，在C语言中字符常量'a'具有int类型，sizeof('a')等于sizeof(int)；在C++语言中字符字面量'a'具有char类型，sizeof('a')为1。

使用前缀L u U分别表示wchar_t  char16_t char32_t等字符类型的字面量。例如<code>u'y'</code>。一个wchar_t类型的字面量的值，就是该字符在[[执行宽字符集|执行宽字符集]]（execution wide-character set）中的编码值。一个char16_t类型的字面量的值，就是该字符在[[Unicode|Unicode]]编码中的16比特的[[码位|码位]]；显然该字符必须属于Unicode中的[[基本多文種平面|基本多文種平面]]才能用16比特来编码。一个char32_t类型的字面量的值，就是该字符在[[Unicode|Unicode]]编码中的32比特的[[码位|码位]]。这些字符类型在[[x86|x86]]平台均为[[小端序|小端序]]表示。

由于字符型字面量可能不属于C/C++的token的字符范围，这就需要用反斜线<code>\</code>开始的[[转义序列|转义序列]]来表示一个字符值：
*简单转义序列：\' \" \? \\ \a \b \f \n \r \t \v 共计11个字符；
*八进制转义序列：如 \1 \12 \123等等，最多使用3位八进制数字；
*十六进制转义序列：如 \x1abf4 ，可以使用任意多的十六进制数字，直至不是十六进制数字为止；
*16位的通用字符名（universe-character name）：<code>\u</code>后面必须跟4个十六进制数字（不足四位前面用零补齐），表示[[Unicode|Unicode]]中在0至0xFFFF之内的[[码位|码位]]（但不能表示0xD800到0xDFFF之内的码点，Unicode标准规定这个范围内的码位保留，不表示字符）；
*32位的通用字符名：<code>\U</code>后面必须跟8个十六进制数字（不足八位前面用零补齐），表示Unicode中所有可能的码位（除0xD800到0xDFFF之外）。 

上述两种Unicode转义序列的字符表示法，由[[编译器|编译器]]自动转换为相应的字符内部编码格式。如为wchar_t字符。

为支持老的代码，C语言规定了[[三字符组与双字符组|三字符组]]替换，在扫描处理C语言源文件时，替换下述的3字符出现为1个字符：
{|class="wikitable"
|-
! 三字符组 !! 替换为
|-
| <code>??=</code> || <code>#</code>
|-
| <code>??/</code> || <code>\</code>
|-
| <code>??'</code> || <code>^</code>
|-
| <code>??(</code> || <code><nowiki>[</nowiki></code>
|-
| <code>??)</code> || <code><nowiki>]</nowiki></code>
|-
| <code>??!</code> || <code><nowiki>|</nowiki></code>
|-
| <code>??<</code> || <code>{</code>
|-
| <code>??></code> || <code>}</code>
|-
| <code>??-</code> || <code>~</code>
|}

如果希望在源程序中有两个连续的问号，且不希望被预处理器替换，这种情况出现在字符字面常量、字符串字面常量或者是程序注释中，可选办法是用字符串的自动连接：<code>"...?""?..."</code>或者[[转义序列|转义序列]]：<code>"...?\?..."</code>。
   
从[[Microsoft_Visual_C++|Microsoft Visual C++]] 2010版开始，该编译器默认不再自动替换三字符组。如果需要使用三字符组替换（如为了兼容古老的软件代码），需要设置编译器命令行选项/Zc:trigraphs

[[gcc|gcc]]默认不识别三字符组，并会给出编译警告。在指定了C/C++标准时，gcc才会识别三字符组，但仍会给出编译警告。

==字符串字面常量==
C语言经典的'''ASCII-0字符串'''，例如"Hello world!"。

由<code>R"''<someChars>''<sub>opt</sub>(</code> 与 <code>)''<someChars>''<sub>opt</sub>"</code>括起来的字符串字面量叫做raw string literal，这可以避免大量使用反斜线转义字符造成的令人眼花缭乱的[[倾斜牙签综合征|倾斜牙签综合征]]，特别适用于定义[[正则表达式|正则表达式]]的模式字符串时。例如：
  std::string filePath = R"(C:\Foo\Bar.txt)";
  std::regex re{ R"abc(s/"\([^"]*\)"/'\1'/g)abc" }; //如果字符串包含了''')"'''这两个字符的组合，可选别的分界符，如<code>abc</code>。但这个分界符序列的长度最多16。
 
字符串字面量的值默认为工作字符集的编码。<ref>具体是哪一种工作字符集编码，由[[编译器|编译器]]采用缺省设置，如[[Visual_C++|Visual C++]]默认使用当前操作系统的缺省[[代码页|代码页]]，简体中文Windows就是[[gbk|gbk]]编码，[[Linux|Linux]]上的[[gcc|gcc]]一般默认为[[utf8|utf8]]编码；也可以作为命令行参数指定给编译器，如gcc的"-fexec-charset=   ".</ref>使用编码前缀（encoding-prefix）： u8 u U L 指出字符串字面量的值为[[UTF-8|UTF-8]]、char16_t、char32_t、wchar_t的编码序列。例如，
  char ss[]=u8"Hi世界";// ss数组内保存的是'H'、'i'、'世'、'界'这四个字符的[[UTF-8|UTF-8]]的编码值

相邻的两个字符串将被编译器自动连接为一个字符串。如：
  char ss[]="Hello" " world.";
==枚举常量==
[[枚举|枚举]]类型实质上是取有限个值的整型。根据C与C++98标准，枚举常量属于定义了枚举类型的那个作用域，而不属于这个枚举类型的内部作用域。C++发明人[[Bjarne_Stroustrup|Bjarne Stroustrup]]称之为枚举常量的作用域不受限（unscoped）现象，这会造成命名冲突，与枚举常量是“有类型的常量”的初衷不符，与面向对象程序设计的原则严重相悖。例如：
 enum FileAccess {
     Read = 0x1,
     Write = 0x2,
 };
 FileAccess access = ::Read; // 正确
 FileAccess access = FileAccess::Read; // 错误
 enum FileShare {
    Read = 0x1, // 重定义错误
    Write = 0x2, // 重定义错误
 };

C++11为解决上述问题，引入了“枚举类”（enum class）。在定义枚举类型时，enum[[关键字|关键字]]后面加上class关键字（或struct关键字）；引用枚举常量时，必须加上枚举类型名使其为作用域限定 （scoped）。这避免了枚举常量的命名冲突；同时也避免了不同枚举类型的值的隐式类型转换，从而保证了枚举类型是强类型（strongly typed）的。例如：
 enum class Color { RED, BLACK }; 
 Color c = Color::RED;

C++11还允许指定枚举类型的存储类型，这使得枚举类型的前向声明（forward declaration）成为可能。例如：
 enum class Color : char ; // forward declaration
 void foo (Color *p);// ...
 // ...
 enum class Color : char { RED, BLUE }; // definition
==布尔型字面常量==
有两个bool类型的字面常量：true  false
==指针型字面常量==
{{main|nullptr}}
C++11定义了一个字面常量[[nullptr|nullptr]]，其类型是std::nullptr_t。但std::nullptr_t既不是指针类型也不是到成员的指针类型。

==用户定义的字面量==
{{main|用户定义字面量}}
C++11新增加了用户定义的字面常量（user defined literal）。由用户给出字面常量的后缀，并给出字面量运算符函数（或模板）的定义。编译器可在[[运行期|运行期]]或[[编译期|编译期]]把带有这样后缀的整型、浮点型、字符型、字符串型的字面量通过调用用户的字面量运算符函数（或模板），生成指定数据类型的对象。例如，
<source lang="cpp">
#include<iostream>
struct S{
    int value;
};
S operator ""_mysuffix(unsigned long long v)  //用户定义字面量运算符的实现
{
     S s_;
     s_.value=(int)v;
     return s_;
}

int main()
{
   S sv;
   sv=101_mysuffix;  //这里的101是类型S的字面量
   std::cout<<sv.value<<std::endl;
   return 0;
}
</source>
==参考文献==
<references/>

[[Category:C语言|Category:C语言]]
[[Category:C++|Category:C++]]