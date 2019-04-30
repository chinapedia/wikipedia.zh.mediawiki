'''异步IO'''是计算机操作系统对[[输入输出|输入输出]]的一种处理方式：发起IO请求的线程不等IO操作完成，就继续执行随后的代码，IO结果用其他方式通知发起IO请求的程序。与异步IO相对的是更为常见的“同步（阻塞）IO”：发起IO请求的线程不从正在调用的IO操作函数返回（即被阻塞），直至IO操作完成。
  
==类Unix操作系统与POSIX==
POSIX提供下述API函数：
{| class="wikitable"
|-
! !! 阻塞 !! 非阻塞
|-
! 同步
| write, read || write, read + poll / select
|-
! 异步
| - || aio_write, aio_read
|}
==Windows操作系统的异步IO==
Windows提供多种异步IO（也称[[重叠I/O|重叠IO]]）方式：<ref>[http://msdn.microsoft.com/en-US/library/kztecsys%28v=vs.100%29.aspx Description from .NET Framework Developer's Guide]</ref>
===设备内核对象 ===
IO设备在操作系统内核中表示为[[内核对象|内核对象]]，因此具有可等待（waitable）内核对象状态。例如：文件[[句柄|句柄]]，线程句柄等等。对于文件内核对象，当一个异步IO完成后，该文件句柄被置为触发态。使用这种方式获取异步IO完成的通知，缺点是如果在一个文件内核对象上同时有多个异步IO操作，只通过文件句柄的触发无法辨识哪个异步IO操作完成了。

例子：
<source lang="cpp">
HANDLE hFile = CreateFileW(L"d:\\a.txt", GENERIC_WRITE, 0, 0, CREATE_ALWAYS, FILE_FLAG_OVERLAPPED, 0); //设置异步IO的标志FILE_FLAG_OVERLAPPED
char buffer[10] = {"abcd"};
OVERLAPPED ol = { 0 };//用0初始化OVERLAPPED的结构
ol.Offset = 2;/从文件的第三个字节开始IO
BOOL rt = WriteFile(hFile, buffer, 5, NULL, &ol);//发起一个异步写操作
//SetFileCompletionNotificationModes(hFile, FILE_SKIP_SET_EVENT_ON_HANDLE);//如此设置则文件内核对象就不会被触发
if (rt == FALSE && GetLastError() == ERROR_IO_PENDING)//检查异步IO是否完成 
{
	WaitForSingleObject(hFile, INFINITE);//等待设备内核对象（文件）被触发。
}
CloseHandle(hFile); 
</source>

===GetOverlappedResult函数===
也可以使用[[Windows_API|Windows API]]函数GetOverlappedResult直接阻塞/非阻塞等待指定的异步IO操作是否完成。<ref>[https://msdn.microsoft.com/en-us/library/windows/desktop/ms683209(v=vs.85).aspx MSDN:GetOverlappedResult function]</ref>该函数检查OVERLAPPED结构中的Internal成员的值是否为STATUS_PENDING来判断异步IO是否完成。 
===异步IO操作的完成通知用[[事件_(同步原语)|事件]]内核对象===
在异步IO操作的read/write函数调用中给出的OVERLAPPED类型的参数中，可以指定一个内核[[事件_(同步原语)|事件]]对象。这个异步IO操作完成时，这个内核[[事件_(同步原语)|事件]]对象会被触发。从而，等待在这个事件对象上的程序就会知道这个异步IO操作完成。

例子：
<source lang="cpp">
HANDLE hFile = CreateFileW(L"d:\\a.txt", GENERIC_WRITE, 0, 0, CREATE_ALWAYS, FILE_FLAG_OVERLAPPED, 0); //设置异步IO的标志FILE_FLAG_OVERLAPPED
char buffer[10] = {"abcd"};
OVERLAPPED ol = { 0 };//用0初始化OVERLAPPED的结构
ol.Offset = 2;/从文件的第三个字节开始IO
HANDLE hEvent = CreateEvent(0, FALSE, FALSE, NULL);  
ol.hEvent = hEvent;//传递一个事件对象。  

BOOL rt = WriteFile(hFile, buffer, 5, NULL, &ol);//发起一个异步写操作 

if (rt == FALSE && GetLastError() == ERROR_IO_PENDING)//检查异步IO是否完成 
{
	WaitForSingleObject(ol.hEvent, INFINITE);//等待设备内核对象（文件）被触发。
}
CloseHandle(hEvent); 
CloseHandle(hFile); 
</source>
===[[可唤醒I/O|可唤醒I/O]] ===
异步[[可唤醒I/O|可唤醒I/O]]操作通过ReadFileEx/WriteFileEx函数指出完成过程回调函数。回调函数在该线程的可唤醒等待（alertable wait）中被执行。
===[[完成端口|完成端口]]===
使用CreateIoCompletionPort函数创建一个[[完成端口|完成端口]]。然后把文件句柄绑定到这个完成端口（通过CreateIoCompletionPort函数)。这个文件句柄上的异步IO操作完成时，会自动向这个完成完成端口发通知。线程通过GetQueuedCompletionStatus函数等待这个完成端口上的完成通知，然后从GetQueuedCompletionStatus的调用返回处恢复线程执行。

===[[线程池|线程池]]I/O完成对象===
使用CreateThreadpoolIo函数创建一个I/O完成对象，绑定了要执行异步I/O操作的文件句柄与待执行的回调函数。通过StartThreadpoolIo函数开始I/O完成对象的工作。每当绑定的文件句柄上的异步I/O操作完成，自动调用[[线程池|线程池]]上的线程执行指定的回调函数。

例子：
<source lang="cpp">
VOID CALLBACK OverlappedCompletionRoutine(PTP_CALLBACK_INSTANCE pInstance,  
                                          PVOID pvContext,  
                                          PVOID pOverlapped,  
                                          ULONG IoResult,  
                                          ULONG_PTR NumberOfBytesTransferred,  
                                          PTP_IO pIo)  
{  
    printf("OverlappedCompletionRoutine, transferred: %d bytes\n", NumberOfBytesTransferred);  
}  

HANDLE hFile = CreateFileW(L"d:\\a.txt", GENERIC_WRITE, 0, 0, CREATE_ALWAYS, FILE_FLAG_OVERLAPPED, 0); //设置异步IO的标志FILE_FLAG_OVERLAPPED

PTP_IO pio = CreateThreadpoolIo(hFile, OverlappedCompletionRoutine, NULL, NULL);//将设备对象和线程池的IO完成端口关联起来。  
StartThreadpoolIo(pio);
char buffer[10] = {"abcd"};
OVERLAPPED ol = { 0 };//用0初始化OVERLAPPED的结构
ol.Offset = 2;/从文件的第三个字节开始IO   

BOOL rt = WriteFile(hFile, buffer, 5, NULL, &ol);//发起一个异步写操作 
if(rt==FALSE && GetLastError()==ERROR_IO_PENDING))
{  
   ::Sleep(4000); 
   //do somethings... 
}
else
{
   CancelThreadpoolIo(pio); 
}
WaitForThreadpoolIoCallbacks(pio,false);
CloseHandle(hFile); 
CloseThreadpoolIo(pio);//关闭线程池io完成对象
</source>

==参见==
*[[IOCP|IOCP]] 

==参考文献==
<references />

==外部链接==
*[https://www.webcitation.org/6ICibHuyd?url=http://www.kegel.com/c10k.html The C10K Problem]; a survey of asynchronous I/O methods with emphasis on scaling – by Dan Kegel
*Article "[http://www.ibm.com/developerworks/library/l-async Boost application performance using asynchronous I/O]" by [[M._Tim_Jones|M. Tim Jones]]
*Article "[http://www.usenix.org/event/usenix04/tech/general/full_papers/elmeleegy/elmeleegy_html/html.html Lazy Asynchronous I/O For Event-Driven Servers]" by [[Willy_Zwaenepoel|Willy Zwaenepoel]], [[Khaled_Elmeleegy|Khaled Elmeleegy]], [[Anupam_Chanda|Anupam Chanda]] and [[Alan_L._Cox|Alan L. Cox]]
*[https://www.gnu.org/software/libc/manual/html_node/Asynchronous-I_002fO.html Perform I/O Operations in Parallel]
*[http://opengroup.org/onlinepubs/009695399/basedefs/aio.h.html Description from POSIX standard]
*[https://web.archive.org/web/20101101112358/http://doc.sch130.nsc.ru/www.sysinternals.com/ntw2k/info/comport.shtml Inside I/O Completion Ports] by [[Mark_Russinovich|Mark Russinovich]]
*[http://www.flounder.com/asynchexplorer.htm Asynchronous I/O and The Asynchronous Disk I/O Explorer]
*[http://software.schmorp.de/pkg/IO-AIO.html IO::AIO is a Perl module offering an asynchronous interface for most I/O operations]
*[https://web.archive.org/web/20170623060116/http://www.cs.wustl.edu/~schmidt/PDF/proactor.pdf ACE Proactor]
 
[[Category:并发控制|Category:并发控制]]