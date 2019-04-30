'''特权'''（privilege）是Windows操作系统的帐户权限，如用户、用户群、系统服务、计算机等执行不同的系统操作，如关机、装入设备驱动、改编系统时间等。<ref>[https://msdn.microsoft.com/en-us/library/windows/desktop/aa379306(v=vs.85).aspx MSDN:Privileges]</ref>特权不同于访问权限（access right）：
* 特权控制访问系统资源或系统相关任务，访问特权控制访问可安全对象（securable object）；
* 系统管理员赋予特权给用户或用户群；而系统允许或拒绝对可安全对象的访问，这是基于对象的自主访问控制列表（DACL）中的访问控制项（ACE）。
 
系统有一个帐户数据库，存储了用户或用户群的特权。当用户登录后，系统产生一个[[访问令牌_(Windows)|访问令牌]]（access token）包含了用户的特权清单，这包含用户所在群的特权。注意特权仅限于本地计算机，域帐户在不同计算机上有不同特权。 

当用户试图执行一个特权操作，系统检查用户的访问令牌以确定使用是否具有必要的特权。调用GetTokenInformation函数可以检查特权。 

[[Windows_API|Windows API]]在Winnt.h定义了一套字符串常量，如SE_ASSIGNPRIMARYTOKEN_NAME，辨识不同的特权。见“Privilege Constants”。API函数使用LUID类型来标识不同的特权。LUID随不同的计算机启动任务而变化，因此要用LookupPrivilegeValue函数查出LUID与“Privilege Constants”的对应。使用LookupPrivilegeName函数把LUID转化为对应的字符串常量。

系统给特权一套用于显示的描述字符串。使用LookupPrivilegeDisplayName函数获取对应于字符串常量的特权的描述字符串。例如特权SE_SYSTEMTIME_NAME的描述字符串是"Change the system time"。

可以用PrivilegeCheck函数检查一个访问令牌是否具有指定的特权集。

系统管理员可以用Local Security Authority (LSA)系列函数管理特权。LsaAddAccountRights与LsaRemoveAccountRights函数增减特权。LsaEnumerateAccountRights函数枚举指定帐户的特权。LsaEnumerateAccountsWithUserRight函数枚举具有指定特权的帐户清单。 

==参考文献==
<references/>
[[Category:Microsoft_Windows|Category:Microsoft Windows]]