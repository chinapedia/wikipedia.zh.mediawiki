{{noteTA
|G1=IT
}}
[[Image:Pipeline.svg|thumb]]

在[[Unix-like|类Unix]][[操作系统|操作系统]]（以及一些其他借用了这个设计的操作系统，如Windows）中，'''管道'''（{{lang-en|Pipeline}}）是一系列将[[标准流|标准输入输出]]链接起来的[[进程|进程]]，其中每一个进程的[[stdout|输出]]被直接作为下一个进程的[[stdin|输入]]。 每一个链接都由匿名管道实现{{来源请求}}。管道中的组成元素也被称作{{link-en|过滤程序|Filter_(software)}}。

这个概念是由[[道格拉斯·麥克羅伊|道格拉斯·麥克羅伊]]为[[Unix_shell|Unix 命令行]]发明的，因与物理上的[[管道|管道]]相似而得名。

==例子==

===简单样例===
<source lang="bash">
ls -l | less
</source>

在这个例子中，<code>[[ls|ls]]</code>用于在Unix下列出目录内容，<code>[[less_(Unix)|less]]</code>是一个有搜索功能的交互式的文本[[终端分页器|分页器]]。这个管线使得用户可以在列出的目录内容比屏幕长时目录上下翻页。

以<code>less</code>結束的管道（或[[more|more]]，這是個相似的分頁工具）是最常被使用的。這讓使用者可以閱覽尚未顯示的大量文字（受可用緩存限制，控制台的屏幕大小、屏幕缓存大小往往有限，不足以一次先输出所有输出内容，也不能自由滚动内容），若少了這工具則這些文字將會捲過終端機而無法閱讀到。換句話說，他们将程序员从为自己的软件开发分页器的负担中解放了出来：他们只需要把他们的输出用过“管道”导入到<code>less</code>程序中即可，甚至也可以完全不顾分页问题，去假定他们的用户会在需要将输出分页的时候自己去这样做。

===复杂样例===
以下是一個管線的範例，執行由一[[URL|URL]]標示的[[全球資訊網|全球資訊網]]資源的一種[[拼寫檢查|拼寫檢查器]]。之後是關於這個其作用的說明。注意「\」是用來把這六行轉為一個命令列。

<source lang="bash">
curl "http://en.wikipedia.org/wiki/Pipeline_(Unix)" | \
sed 's/[^a-zA-Z ]/ /g' | \
tr 'A-Z ' 'a-z\n' | \
grep '[a-z]' | \
sort -u | \
comm -23 - /usr/share/dict/words | \
less
</source>

# '''<tt>[[CURL|curl]]</tt>''' 取得該網頁的[[HTML|HTML]]內容（在有些系統上可以使用<tt>wget</tt>）。
# '''<tt>[[sed|sed]]</tt>''' 移除非空格的[[字元|字元]]和網頁內容的字母，並以空格取代之。
# '''<tt>[[tr|tr]]</tt>''' 把大寫字母改成小寫字母，並把行列裡的空格換成新行（每個詞現在各占有獨立的一行）。
# '''<tt>[[grep|grep]]</tt>''' 过滤得到那些至少有一个小写字母的行（删除空行）。
# '''<tt>[[Sort_(Unix)|sort]]</tt>''' 将“单词”（也就是每一个行）按照字母顺序排序，并且通过命令行的<tt>-u</tt>参数来删除重复的行。
# '''<tt>[[comm_(Unix)|comm]]</tt>''' 查找两个文件中的共同行，<tt>-23</tt>过滤掉只有第二个文件拥有的行、两个文件共有的行，仅仅留下只在第一个文件中有的行。在文件名的位置上的<tt>-</tt>参数表示要求<tt>comm</tt>使用标准输入（在这个例子里，他的标准输入来自于管道上游的标准输出）作为输入，而不是以普通文件作为输入。最终得到一串没有出现在/usr/share/dict/words之中的“单词”（也就是一行）。
# '''<tt>[[less_(Unix)|less]]</tt>''' 允许用户翻页浏览结果。

这个特殊的“|”字符告诉命令行解释器（[[Shell|Shell]]）将前一个命令的输出通过“管道”导入到接下来的一行命令作为输入。也就是说，<tt>curl</tt>命令的输出被作为<tt>sed</tt>命令的输入，后面的命令也是这样。

== 命令行界面中的管线 ==
所有广泛应用于UNIX和Windows中的shell程序都有特殊的语法构建管线。典型语法是使用[[ASCII|ASCII]]中的垂直线“|”（正是由于这个原因，这个符号常被称为管道符）。当出现这样的语法时shell会启动各个进程，并调整各个进程的[[标准流|标准流]]之间的连接（还包括安排一些[[缓存|缓存]]）。

===错误流===
通常，管线中的进程的[[stderr|标准错误流]]("stderr")不会通过管道传输；它们被合并输出到[[命令行界面|控制台]]。然而，很多Shell提供一些扩充的语法去改变这一行为。比如在[[C_shell|csh]] Shell和[[bash|bash]]中，使用“|&”代替“|”来表示错误流也需要被合并进入标准输出，并传递给下一个进程。[[Bourne_shell|Bourne shell]]也可以合并错误流，通过 <tt>2>&1</tt> 也可以将错误流重定向到一个不同的文件。

===Pipemill===
在一些常用的简单管线中，shell仅仅只是用管道来连接每个子进程，然后在子进程中执行外部命令。因此shell本身没有通过管线来处理数据。

然而，shell也有可能直接处理管线数据。构建这样的语法像这样：
<source lang="bash">
command | while read var1 var2 ...; do
   # process each line, using variables as parsed into $var1, $var2, etc
   # (note that this is a subshell: var1, var2 etc will not be available
   # after the while loop terminates)
   done
</source>
... 这样的语法叫 "pipemill" 。

== 在程序中创造管道 ==

===匿名管道===
使用[[C语言|C语言]]在UNIX中使用pipe(2)[[系统调用|系统调用]]时，这个函数会让系统构建一个[[匿名管道|匿名管道]]，这样在进程中就打开了两个新的，打开的[[文件描述符|文件描述符]]：一个只读端和一个只写端。管道的两端是两个普通的，匿名的文件描述符，这就让其他进程无法连接该管道。
为了避免[[死锁|死锁]]并利用进程的[[并行运行|并行运行]]的好处，有一个或多个管道的UNIX进程通常会调用<code>[[Fork_(系统调用)|fork(2)]]</code>产生新进程。并且每个子进程在开始读或写管道之前都会关掉不会用到的管道端。或者进程会产生一个子[[线程|线程]]并使用管道来让线程进行数据交换。
实现代码：
<source lang="c">
 
#include <sys/wait.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>

int
main(int argc, char *argv[])
{
  int pipefd[2];
  pid_t cpid;
  char buf;

  if (argc != 2) {
    fprintf(stderr, "Usage: %s <string>\n", argv[0]);
    exit(EXIT_FAILURE);
  }

  if (pipe(pipefd) == -1) {
    perror("pipe");
    exit(EXIT_FAILURE);
  }

  cpid = fork();
  if (cpid == -1) {
    perror("fork");
    exit(EXIT_FAILURE);
  }

  if (cpid == 0) {    /* Child reads from pipe */
    close(pipefd[1]);          /* Close unused write end */
    while (read(pipefd[0], &buf, 1) > 0)
      write(STDOUT_FILENO, &buf, 1);

    write(STDOUT_FILENO, "\n", 1);
    close(pipefd[0]);
    _exit(EXIT_SUCCESS);

  } else {            /* Parent writes argv[1] to pipe */
    close(pipefd[0]);          /* Close unused read end */
    write(pipefd[1], argv[1], strlen(argv[1]));
    close(pipefd[1]);          /* Reader will see EOF */
    wait(NULL);                /* Wait for child */
    exit(EXIT_SUCCESS);
  }
}
</source>

===具名管道===
[[具名管道|具名管道]]可以通过调用<code>[[mkfifo|mkfifo(2)]]</code>或<code>[[mknod|mknod(2)]]</code>来构建，当被调用时表现为输入或输出的文件。这样可以允许建立多个管道，并且将其同标准错误重定向或<code>[[tee_(command)|tee]]</code>结合起来使用更为有效。
实现代码：
<source lang="c">
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h> 
#include <sys/stat.h> 
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
  char filename[] = "test_fifo";
  if (!mkfifo(filename,S_IRUSR | S_IWUSR| S_IRGRP|S_IWGRP)){
    pid_t pid = fork();
    if (pid == 0){	//child
      int fd = open(filename, O_WRONLY);
      if (fd < 0)
	perror("child open()");
      else{
	if (strlen(argv[1]) != write(fd, argv[1], strlen(argv[1])))
	  perror("child write error");
	else
	  close(fd);
      }
    }
    else if (pid > 0){	//father
      int fd = open(filename, O_RDONLY);
      if (fd < 0)
	perror("father open()");
      else{
	char buffer[200];
	int readed = read(fd, buffer, 199);
	close(fd);
	buffer[readed] = '\0';
	printf("%s\n",buffer);
      }
    }
    else
      perror("fork()");
  }
  else
    perror("mkfifo() error:");
}
</source>
以上代码在编译后运行时给出一个参数，子进程会将该参数内容写入管道（该管道在当前目录下，文件名为“test_fifo”），父进程从管道中读取内容并显示出来

==实现==
在大多数类UNIX操作系统中，管线上的所有进程同时启动，输入输出流也已经被正确地连接，并且这些进程被[[调度|调度]]程序所管理。最为重要的一点就是，所有的UNIX管道和其他管道实现不一样的地方就是缓存的概念：输出进程可能会以每秒5000 [[byte|byte]]的速度输出，但是接收进程也许每秒只能接收100 byte，但不会有数据丢失。原因就是管道上游的进程的所有输出都会被放入一个[[队列|队列]]中。当下游进程开始接收数据时，操作系统就会将数据从队列传至接收进程，并将传完的数据从队列中移除。当缓存队列空间不足时，上游进程会被终止，直到接收进程读取数据为上游进程腾出空间。在[[Linux|Linux]]中，缓存队列的大小是65536 byte。

===网络管线===
根据[[Unix哲学|Unix哲学]]——“一切都是文件”，<code>[[netcat|netcat]]</code>和<code>[[socat|socat]]</code>这样的工具可以将管道连接到TCP/IP[[套接字|套接字]]。

==歷史==
<!-- Image with inadequate rationale removed: [[Image:Automator_Icon.png|thumb]]  -->
管道的概念以及垂直线的记号(|)都是由[[道格拉斯·麥克羅伊|道格拉斯·麥克羅伊]]发明的，他是早期[[Unix_Shell|命令行外壳]]的作者。他发现他常常将一个程序的输出作为另一个程序的输入，于是便发明了“管道。它的想法在1973年被实现，[[Ken_Thompson|Ken Thompson]]将管道添加到了[[UNIX|UNIX]]操作系统。<ref>http://www.linfo.org/pipe.html Pipes: A Brief Introduction by The Linux Information Project (LINFO)</ref>这个点子最终被移植到了其他的操作系统，比如[[DOS|DOS]]、[[OS/2|OS/2]]、[[Microsoft_Windows|Microsoft Windows]]和[[BeOS|BeOS]]，而且常常使用相同的记号(垂直线)。

虽然管道概念是独立发展的，但是 Unix 管道相似于、也确实晚于由Ken Lochner在20世纪60年代为[[Dartmouth_Time_Sharing_System|Dartmouth Time Sharing System]]开发的'communication files'。<ref>http://www.cs.rit.edu/~swm/history/DTSS.doc</ref><ref>http://cm.bell-labs.com/who/dmr/hist.html{{dead link|date=2018年1月 |bot=InternetArchiveBot |fix-attempted=yes }}</ref>

在[[苹果电脑|苹果]][[Automator_(software)|Automator]]（类似管道一样将多个重复的命令链接起来）的那个机器人拿着一根管子的图标也是对于最初Unix管道概念的纪念。

===其他作業系統===
{{Main|管道 (軟體)}}
其他作業系統的這個特色源自於[[Unix|Unix]]，例如 [[Taos|Taos]] 和 [[MS-DOS|MS-DOS]]，最終成為[[軟體工程|軟體工程]]的[[管道_(軟體)|管道與過濾器設計樣本]]

==参见==
* [[匿名管道|匿名管道]]，一個用於[[行程間通訊|行程間通訊]]的 [[FIFO|FIFO]] 架構。
* [[GStreamer|GStreamer]]，一個基於管道的多媒體架構。
* {{tsl|en|Hartmann pipeline|哈特曼管道}}
* [[命名管道|命名管道]]，用于[[进程间通信|进程间通信]]的持久性管道
* [[流水线_(计算机)|流水线 (计算机)]]，与计算机相关的其他管线
* {{tsl|en|Pipeline (software)|流水线 (软件)}}，软件管线的基本概念
* [[重定向_(计算机)|重定向 (计算机)]]
* [[tee|tee]]，将管线内容取出的一个通用程序
* {{tsl|en|XML pipeline|XML管道}}，处理XML的管线

==引用==
{{Reflist}}
{{Refbegin}}
*[[Sal_Soghoian|Sal Soghoian]] on [[MacBreak|MacBreak]] Episode 3 "Enter the Automatrix"
{{Refend}}

==外部链接==
* [http://cm.bell-labs.com/cm/cs/who/dmr/hist.html#pipes History of Unix pipe notation]
** [http://doc.cat-v.org/unix/pipes/ Doug McIlroy’s original 1964 memo], proposing the concept of a pipe for the first time
*{{manlink|sh|pipe|SUS|create an interprocess channel}}
*[http://www.linfo.org/pipe.html Pipes: A Brief Introduction] by The Linux Information Project (LINFO)
*[http://www.softpanorama.org/Scripting/pipes.shtml Unix Pipes – powerful and elegant programming paradigm (Softpanorama)]
*[http://en.wikibooks.org/w/index.php?title=Ad_Hoc_Data_Analysis_From_The_Unix_Command_Line ''Ad Hoc Data Analysis From The Unix Command Line'' at Wikibooks] – Shows how to use pipelines composed of simple filters to do complex data analysis.
*[http://www.debian-administration.org/articles/145 Use And Abuse Of Pipes With Audio Data] – Gives an introduction to using and abusing pipes with netcat, nettee and fifos to play audio across a network.
*[http://stackoverflow.com/questions/19122/bash-pipe-handling stackoverflow.com] – A Q&A about bash pipeline handling.

[[Category:进程间通信|Category:进程间通信]]
[[Category:Unix|Category:Unix]]

[[sv:Vertikalstreck#Datavetenskap|sv:Vertikalstreck#Datavetenskap]]