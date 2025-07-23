# windows命令学习

每个人都更喜欢图形用户界面 （GUI）， 直到他们掌握命令行界面 （CLI）。这有很多原因。原因之一是 GUI 通常是直观的。如果有人为您提供了您不熟悉的 GUI 界面，您可以快速浏览并发现一个不平凡的部分。将此与处理 CLI（即提示）进行比较。

CLI 接口通常有一个学习曲线;但是，当您掌握命令行时，您会发现它更快、更高效。考虑这个微不足道的例子：使用图形桌面需要点击多少次才能找到您的 IP 地址？使用命令行界面，您甚至不需要将手从键盘上抬起。假设您想重新检查您的 IP 地址。您需要发出相同的命令，而不是将鼠标指针移动到屏幕的每个角落。

除了速度和效率之外，使用 CLI 还有许多其他优势。我们将提到一些：

- **资源使用率更低：**CLI 比图形密集型 GUI 需要更少的系统资源。换句话说，您可以在较旧的硬件或内存有限的系统上运行 CLI 系统。如果您使用的是云计算，您的系统将需要更少的资源，这反过来又会降低您的账单。
- **自动化** ：虽然您可以自动执行 GUI 任务，但使用需要重复的命令创建批处理文件或脚本要容易得多。
- **远程管理** ：CLI 使使用 SSH 管理远程系统（例如服务器、路由器或物联网设备）变得非常方便。这种方法适用于网络速度较慢和资源有限的系统。

## 学习目标

本教室的目的是教您如何使用 MS Windows 命令提示符 `cmd.exe`，这是 Windows 环境中默认的命令行解释器。我们将学习如何使用命令行来：

- **显示基本系统信息**
- **检查网络配置并排除故障**
- **管理文件和文件夹**
- **检查正在运行的进程**

## 基本系统信息

在下发命令之前，我们应该注意，我们只能在 Windows 路径中下发命令。您可以发出命令`set`以从命令行检查您的路径。下面的终端输出显示了 MS Windows 将执行命令的路径，如以 `Path=` 开头的行所示。

让我们使用 `ver` 命令来确定作系统 （OS） 版本。下面的终端显示了一个示例输出。

```
C:\>ver                                                                                                                                              
Microsoft Windows [Version 10.0.17763.1821]
```

热身够了。让我们更深入地了解该系统。我们可以运行 `**systeminfo**` 命令来列出有关系统的各种信息，例如作系统信息、系统详细信息、处理器和内存。下面的终端显示了显示输出的片段。**systeminfo**

## 网络配置

我们大多数人都习惯于 从 GUI 界面查找 MS Windows 网络配置。命令行界面提供了许多与网络相关的命令，用于查找当前配置、检查正在进行的连接以及排查网络问题。

您可以使用 `ipconfig` 检查您的网络信息。下面的终端输出显示了我们的 IP 地址、子网掩码和默认网关。

```
C:\>ipconfig

Windows IP Configuration

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : eu-west-1.compute.internal
   Link-local IPv6 Address . . . . . : fe80::90df:4861:ba40:f2a8%4
   IPv4 Address. . . . . . . . . . . : 10.10.230.237
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . : 10.10.0.1
```

您还可以使用 `ipconfig /all` 了解有关网络配置的更多信息。如下面的终端所示，我们可以查看我们的 DNS 服务器并确认 DHCP 已启用。

## 网络故障排除

1.一项常见的故障排除任务是检查服务器是否可以访问 Internet 上的特定服务器。命令语法为 `ping target_name`。受乒乓球的启发，我们发送特定的 ICMP 数据包并侦听响应。如果收到响应，我们就知道我们可以到达目标，并且目标可以到达我们。

让我们看看我们是否达到 `example.com`。在下面的终端输出中，我们可以看到我们已经成功收到了四个回复。此外，我们还得到了一些统计数据;例如，平均往返时间为 78 毫秒。

2.另一个有价值的故障排除工具是 `tracert`，它代表*跟踪路由* 。命令 `tracert target_name` **跟踪到达目标所遍历的网络路由**。在不涉及更多细节的情况下，它希望路径上的路由器在丢弃数据包时通知我们，因为其生存时间 （TTL） 已达到零。下面的终端输出显示，我们在到达目标之前通过了 15 个路由器。

## 更多网络命令

一个值得了解的网络命令是 `nslookup`。它查找主机或域并返回其 IP 地址。语法 `nslookup example.com` 将使用默认名称服务器查找 `example.com`;但是，`nslookup example.com 1.1.1.1` 将使用名称服务器 `one.one.one.one。` 下面的终端显示了这两个命令的输出。结果是相同的;但是，您可以看到答案是从不同的名称服务器检索的。

我们将在本室介绍的最后一个网络命令是 `netstat`**。此命令显示当前网络连接和侦听端口**。一个没有参数的基本 `netstat` 命令将显示已建立的连接，如下所示。在这种情况下，我们只有一个 SSH 连接;我们发现它是 SSH，因为它绑定到端口 22。

如果您对其他选项感到好奇，可以运行 `netstat -h`，其中 `-h` 显示帮助页面。我们选择了以下选项：

- `-a` 显示所有已建立的连接和侦听端口
- `-b` 显示与每个侦听端口和已建立连接关联的程序
- `-o` 显示与连接关联的进程 ID （PID）
- `-n` 使用数字形式表示地址和端口号

我们将这四个选项组合起来并执行 `netstat -abon` 命令。结果很长，但我们在下面的终端中显示前几行。现在很明显，可执行 `sshd.exe` 负责侦听端口 22 上的传入连接，如第一行所示。我们还可以看到与每个连接关联的进程 ID （PID）。



## 文件和磁盘管理

您已经学会了查找基本系统信息和检查网络配置。现在，让我们了解如何浏览目录和移动文件。

### 使用目录

您可以使用不带参数的 `cd` 来显示当前驱动器和目录。这相当于问系统， *我在哪里？*

您可以使用 `dir` 查看子目录。

请注意，您可以将以下选项与 `dir` 一起使用：

- `dir /a` - 同时显示隐藏文件和系统文件。
- `dir /s` - 显示当前目录和所有子目录中的文件。

您可以键入 `tree` 来直观地表示子目录和子目录。

```
C:\Users\strategos>tree
Folder PATH listing
Volume serial number is A8A4-C362
C:.
├───Desktop
├───Documents
├───Downloads
├───Favorites
├───Links
├───Music
├───Pictures
├───Saved Games
```

您可以使用命令 `cd target_directory` 更改为任何目录;这相当于双击桌面上的 `target_directory`。此外，您可以使用 `cd ..` 来提升一个级别。下面的终端输出中显示了一个示例。

要创建目录，请使用 `mkdir directory_name`;`mkdir` 代表 *make directory*。要删除目录，请使用 `rmdir directory_name`;`rmdir` 代表*删除目录* 。下面的终端输出显示了创建和删除目录。

### 使用文件

您正在使用命令行。您对特定文本文件的内容感到好奇。您可以轻松查看具有命令`type`文本文件。此命令将文本文件的内容转储到屏幕上;这对于适合终端窗口的文件来说很方便。对于较长的文本文件，您可能需要考虑`more `。此命令**将显示足够的文本文件内容来填充您的终端窗口**。换句话说，对于长文本文件，` more`显示单个页面，并等待您按`空格键`移动一页（翻页）或`按 Enter` 移动一行。

`copy` 命令允许您将文件从一个位置复制到另一个位置。以下终端输出提供了一个示例

```
C:\example>dir
 Directory of C:\example

05/02/2024  08:12 AM    <DIR>          .
05/02/2024  08:12 AM    <DIR>          ..
05/02/2024  07:57 AM                17 test.txt
               1 File(s)             17 bytes
               2 Dir(s)  14,983,409,664 bytes free

C:\example>copy test.txt test2.txt
        1 file(s) copied.

C:\example>dir
 Directory of C:\example

05/02/2024  08:12 AM    <DIR>          .
05/02/2024  08:12 AM    <DIR>          ..
05/02/2024  07:57 AM                17 test.txt
05/02/2024  07:57 AM                17 test2.txt
               2 File(s)             34 bytes
               2 Dir(s)  14,983,409,664 bytes free
```



同样，您可以使用 `move` 命令移动文件。下面的终端输出中显示了一个示例。

```
C:\example>dir
 Directory of C:\example

05/02/2024  08:12 AM    <DIR>          .
05/02/2024  08:12 AM    <DIR>          ..
05/02/2024  07:57 AM                17 test.txt
05/02/2024  07:57 AM                17 test2.txt
               2 File(s)             34 bytes
               2 Dir(s)  14,983,409,664 bytes free

C:\example>move test2.txt .. 
        1 file(s) moved. 

C:\example>dir 
 Directory of C:\example

05/02/2024  08:13 AM    <DIR>          .
05/02/2024  08:13 AM    <DIR>          ..
05/02/2024  07:57 AM                17 test.txt
               1 File(s)             17 bytes
               2 Dir(s)  14,983,409,664 bytes free
```

最后，我们可以使用 `del` 或 `erase` 删除文件。

```
C:\example>dir
 Directory of C:\example

05/02/2024  08:16 AM    <DIR>          .
05/02/2024  08:16 AM    <DIR>          ..
05/02/2024  07:57 AM                17 test.txt
05/02/2024  07:57 AM                17 test2.txt
               2 File(s)             34 bytes
               2 Dir(s)  14,983,409,664 bytes free

C:\example>erase test2.txt

C:\example>dir 
 Directory of C:\example

05/02/2024  08:16 AM    <DIR>          .
05/02/2024  08:16 AM    <DIR>          ..
05/02/2024  07:57 AM                17 test.txt
               1 File(s)             17 bytes
               2 Dir(s)  14,983,409,664 bytes free
```



我们可以使用通配符 `*` 来引用多个文件。例如，`copy *.md C：\Markdown` 会将扩展名为 `md` 的所有文件复制到目录 `C：\Markdown`。

## 任务和流程管理

您必须熟悉 MS Windows 任务管理器，并且可能熟悉终止无响应的进程。让我们来了解如何使用命令行实现类似的功能。

我们可以使用 `tasklist` 列出正在运行的进程。

```
C:\>tasklist

Image Name                     PID Session Name        Session#    Mem Usage 
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0         88 K
Registry                        84 Services                   0     50,700 K
smss.exe                       276 Services                   0      1,132 K
csrss.exe                      372 Services                   0      5,264 K
wininit.exe                    448 Services                   0      6,892 K
csrss.exe                      456 Console                    1      5,028 K
winlogon.exe                   516 Console                    1     11,144 K
services.exe                   584 Services                   0      7,492 K
lsass.exe                      592 Services                   0     16,108 K
svchost.exe                    704 Services                   0     23,432 K
fontdrvhost.exe                736 Console                    1      4,256 K
[...]
```

一些筛选很有帮助，因为输出预计会很长。您可以通过使用 `tasklist /？`.假设我们想要搜索与 `sshd.exe` 相关的任务，我们可以使用命令 `tasklist /FI "imagename eq sshd.exe"` 来实现。请注意，`/FI` 用于将筛选条件*图像名称设置为等于* `sshd.exe`。

//FI 用于筛选 

在已知进程 ID （PID） 的情况下，我们可以使用 `taskkill /PID target_pid` 终止任何任务。例如，如果我们想用 PID`4567` 杀死进程，我们将发出命令 `taskkill /PID 4567`

## 总结1：

我们故意省略了一些常用命令，因为我们没有看到将它们包含在初学者房间中的真正价值。我们在下面提到它们，以便您知道命令行可用于其他任务。

- `chkdsk`：检查文件系统和磁盘卷是否存在错误和坏扇区。
- `driverquery`：显示已安装设备驱动程序的列表。
- `SFC /scannow`：扫描系统文件以查找损坏，并在可能的情况下修复它们。

记住前面任务中介绍的所有命令非常重要;此外，知道 `/？` 可以与大多数命令一起使用来显示帮助页面也同样重要。

在这个房间里，我们`more`地以两种方式使用命令：

- 显示文本文件：` more file.txt`
- 管道长输出以逐页查看：`some_command | more`

有了这些知识，我们现在知道如何显示新命令的帮助页面以及如何一次显示一页的长输出。

现在，您已经了解了 Windows 命令行，是时候转到 [Windows PowerShell](https://tryhackme.com/r/room/windowspowershell) Room 了。

## 学习目标2

这是 [Command Line](https://tryhackme.com/module/command-line) 模块中的第二个 room。它是 PowerShell 的入门室， 是专为 Windows 作系统构建的第二个（历史上唯一一个）命令行实用程序。

- 了解什么是 PowerShell 及其功能。
- 了解 PowerShell 语言的基本结构。
- 学习并运行一些基本的 PowerShell 命令。
- 了解 PowerShell 在网络安全行业的众多应用。

PowerShell 是 Microsoft 推出的一款功能强大的工具，专为任务自动化和配置管理而设计。**它结合了命令行界面和基于 .NET Framework 构建的脚本语言。与旧的基于文本的命令行工具不同，PowerShell 是面向对象的，这意味着它可以处理复杂的数据类型并更有效地与系统组件交互**。PowerShell 最初是 Windows 独有的，最近扩展到支持 macOS 和 Linux，使其成为跨不同作系统的 IT 专业人员的多功能选择。

## PowerShell 简史

PowerShell 的开发是为了克服 Windows 中现有命令行工具和脚本环境的局限性。在 2000 年代初期，随着 Windows 越来越多地用于复杂的企业环境，`cmd.exe` 和批处理文件等传统工具在自动化和管理这些系统方面存在不足。Microsoft 需要一种能够处理更复杂的管理任务并与 Windows 的现代 API 交互的工具。

Microsoft 工程师 Jeffrey Snover 意识到 Windows 和 Unix 处理系统作的方式不同——Windows 使用结构化数据和 API，而 Unix 将所有内容都视为文本文件。这种差异使得将 Unix 工具移植到 Windows 变得不切实际。**Snover 的解决方案是开发一种面向对象的方法，将脚本编写的简单性与 .NET 框架的强大功能相结合。**PowerShell 于 2006 年发布，允许管理员通过作对象更有效地自动执行任务，从而提供与 Windows 系统的更深入集成。

随着 IT 环境的发展以包含各种作系统，对多功能自动化工具的需求也在增长**。2016 年，Microsoft 发布了 PowerShell Core，这是一个在 Windows、macOS 和 Linux 上运行的开源跨平台版本。**

## PowerShell 中的强大功能

要充分掌握 PowerShell 的强大功能，我们首先需要了解此上下文中的**对象**是什么。

在编程中， **对象**表示具有**属性** （特征caruactors）和**方法** （作actions）的项目。例如，` 汽车`对象可能具有 `Color`、`Model` 和 `FuelLevel` 等属性，以及 `Drive（）、``HonkHorn（）` 和 `Refuel（）` 等方法。

同样，在 PowerShell 中，对象是封装数据和功能的基本单元，使管理和作信息变得更加容易。PowerShell 中的对象可以包含文件名、用户名或大小作为数据（ **属性** ），并携带复制文件或停止进程等函数（ **方法** ）。

传统 Command Shell 的基本命令是基于文本的，这意味着它们以纯文本的形式处理和输出数据。相反，当 **cmdlet**（发音为 *command-let*）在 PowerShell 中运行时，它会返回保留其属性和方法的对象。这允许更强大和灵活的数据作，因为这些对象不需要对文本进行额外的解析。

我们将在接下来的部分中详细探讨 PowerShell 的 cmdlet 及其功能。



在继续我们的 PowerShell 旅程之前，让我们连接到我们的实验室环境。按下 `Start Machine` 按钮，然后按下此页面顶部的 `Start AttackBox` 按钮启动 **AttackBox**。AttackBox 机器将在**分屏视图中**启动。如果它不可见，请使用页面顶部的蓝色 `Show Split View` 按钮。

您可以按照以下步骤使用 Remmina 客户端通过 SSH 连接到目标 VM。

1. 点击 **应用** 在下面的屏幕截图中标有数字 1。选择 **Internet** （数字 2），然后选择 **Remmina** （数字 3）。

![The AttackBox desktop with a number 1 next to the Applications menu at the top left. The dropdown menu is open and displays a number 2 next to the option Internet, and a number 3 next to the option Remmina in the nested dropdown.](D:\Typora\保存文档\网络安全\assets\66b36e2379a5d0220fc6b99e-1728349600926.png)

2.将出现一个弹出窗口，提示您输入密码以解锁 AttackBox 的钥匙圈。单击 `“取消”` 以忽略提示。

3.从下拉列表中选择 **SSH** 选项（下面屏幕截图中的数字 1），然后将目标 IP：`10.10.222.15` 粘贴到顶部的栏中（数字 2）。最后，单击 `Enter`。

![A Remmina client window with a number 1 attached to a dropdown currently showing the option SSH. A number 2 is attached to a text bar, where an IP has been typed.](D:\Typora\保存文档\网络安全\assets\66b36e2379a5d0220fc6b99e-1728351863693.png)

4.在下一个窗口中，输入下面卡片中的凭据，然后单击确定。



或者，可以通过键入 `powershell` 并按 `Enter` 从命令提示符 （`cmd.exe`） 启动 PowerShell。

在我们的例子中，我们只能访问目标 VM 的命令提示符，这就是我们将使用的方法。

## 基本语法：动词-名词

如前所述，PowerShell 命令称为 `cmdlet`（发音为 `command-lets`）。它们比传统的 Windows 命令强大得多，并允许更高级的数据作。

Cmdlet 遵循一致的`动词-名词`命名约定。通过此结构，可以轻松了解每个 cmdlet 的作用。` 动词`描述作，` 名词`指定要对其执行作的对象。例如：

- `Get-Content`：**检索（获取）文件的内容并将其显示在控制台中。**
- `Set-Location`：**更改（设置）当前工作目录。**

## 基本 Cmdlet

要列出可在当前 PowerShell 会话中执行的所有可用 cmdlet、函数、别名和脚本，我们可以使用 `Get-Command`。它是发现可以使用哪些命令的重要工具。

```
PS C:\Users\captain> Get-Command

CommandType     Name                                               Version    Source 
-----------     ----                                               -------    ------ 

Alias           Add-AppPackage                                     2.0.1.0    Appx                                                                                                                                       
Alias           Add-AppPackageVolume                               2.0.1.0    Appx                                                                                                                                       
Alias           Add-AppProvisionedPackage                          3.0        Dism                                                                                                                                       
[...]
Function        A:
Function        Add-BCDataCacheExtension                           1.0.0.0    BranchCache                                                                                                                                
Function        Add-DnsClientDohServerAddress                      1.0.0.0    DnsClient
[...]
Cmdlet          Add-AppxPackage                                    2.0.1.0    Appx
Cmdlet          Add-AppxProvisionedPackage                         3.0        Dism                                                                                                                                       
Cmdlet          Add-AppxVolume                                     2.0.1.0    Appx
[...]
```



对于 cmdlet 检索的每个 `CommandInfo` 对象，控制台上会显示一些基本信息（属性）。可以根据显示的属性值筛选命令列表。例如，如果我们想只显示 “function” 类型的可用命令，我们可以使用 `-CommandType “Function”`，如下所示：

```
PS C:\Users\captain> Get-Command -CommandType "Function"

CommandType     Name                                               Version    Source                                                                                                                                     
-----------     ----                                               -------    ------
Function        A:
Function        Add-BCDataCacheExtension                           1.0.0.0    BranchCache
Function        Add-DnsClientDohServerAddress                      1.0.0.0    DnsClient
Function        Add-DnsClientNrptRule                              1.0.0.0    DnsClient
[...]
```

在接下来的任务中，我们将学习更有效的方法来筛选 cmdlet 的输出。

另一个需要保留在我们的工具带中的重要 cmdlet 是 `Get-Help`：**它提供有关 cmdlet 的详细信息，包括用法、参数和示例。它是学习如何使用 PowerShell 命令的首选 cmdlet。**

如上面的结果所示，`Get-Help` 告诉我们，我们可以通过将一些选项附加到基本语法来检索有关 cmdlet 的其他有用信息。例如，通过将 `-examples` 附加到上面显示的命令，我们将看到可以使用所选 cmdlet 的常见方式列表。

为了方便 IT 专业人员进行转换，PowerShell 为许多传统 Windows 命令提供了别名，这些别名是 cmdlet 的快捷方式或备用名称。`Get-Alias` 对于已经熟悉其他命令行工具的用户来说是必不可少的，它列出了所有可用的别名。例如，`dir` 是 `Get-ChildItem` 的别名，`cd` 是 `Set-Location` 的别名。Get-Alias | Where-Object { $_.Definition -eq "Get-Alias" }

## 在何处查找和下载 Cmdlet

PowerShell 的另一个强大功能是可以通过从在线存储库下载其他 cmdlet 来扩展其功能。

**注意：** 请注意，本部分中列出的 cmdlet 需要有效的 Internet 连接才能查询联机存储库。连接的计算机无法访问 Internet，因此这些命令在此环境中不起作用。

若要在 PowerShell 库等联机存储库中搜索模块（cmdlet 集合），可以使用 `Find-Module`。有时，如果我们不知道模块的确切名称，搜索具有相似名称的模块可能会很有用。我们可以通过筛选 `Name` 属性并将通配符 （`*`） 附加到模块的部分名称来实现此目的，使用以下标准 PowerShell 语法：`Cmdlet -Property “pattern*”`。

What is the command to retrieve some example usage for the cmdlet `New-LocalUser`?

Get-Help New-LocalUser -examples



##  导航文件系统和处理文件

PowerShell 提供了一系列用于导航文件系统和管理文件的 cmdlet，其中许多 cmdlet 在传统 Windows CLI 中具有对应项。

与命令提示符中的 `dir` 命令（或类似 Unix 系统中的 `ls`）类似，`Get-ChildItem` 在使用 `-Path` 参数指定的位置列出文件和目录。它可用于浏览目录并查看其内容。如果未指定 `Path`，则 cmdlet 将显示当前工作目录的内容。

要导航到其他目录，我们可以使用 `Set-Location` cmdlet。它会更改当前目录，将我们带到指定的路径，类似于命令提示符中的 `cd` 命令。

传统的 Windows CLI 使用单独的命令来创建和管理不同的项目（如目录和文件），而 PowerShell 通过提供一组 cmdlet 来处理文件和目录的创建和管理，从而简化了此过程。

要在 PowerShell 中创建项，我们可以使用 `New-Item`。**我们需要指定项目的路径及其类型（无论是文件还是目录）。**

```
PS C:\Users\captain\Documents> New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType "Directory"

    Directory: C:\Users\captain\Documents\captain-cabin

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----          9/4/2024  12:20 PM                captain-wardrobe

PS C:\Users\captain\Documents> New-Item -Path ".\captain-cabin\captain-wardrobe\captain-boots.txt" -ItemType "File"     

    Directory: C:\Users\captain\Documents\captain-cabin\captain-wardrobe

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          9/4/2024  11:46 AM              0 captain-boots.txt  
```

同样，`Remove-Item` cmdlet 删除目录和文件，而在 Windows CLI 中，我们有单独的命令 `rmdir` 和 `del`。

我们可以分别使用 `Copy-Item`（相当于 `copy`）和 `Move-Item`（相当于 `move`）来复制或移动文件和目录。

最后，要读取和显示文件的内容，我们可以使用 `Get-Content` cmdlet，它的工作原理类似于命令提示符中的 `type` 命令（或类 Unix 系统中的 `cat`）。

## 管道、过滤和排序数据Piping, Filtering, and Sorting Data

**管道**是命令行环境中使用的一种技术，**它允许将一个命令的输出用作另一个命令的输入**。这将创建一个作序列，其中数据从一个命令流向下一个命令。管道由 `|` 符号表示，广泛用于 Windows CLI（如本模块前面所述）以及基于 Unix 的 shell。

在 PowerShell 中，管道功能更加强大，因为它传递**对象**而不仅仅是文本。这些对象不仅携带数据，还携带描述数据并与数据交互的属性和方法。

例如，如果要获取目录中的文件列表，然后按大小对它们进行排序，则可以在 PowerShell 中使用以下命令：

```
PS C:\Users\captain\Documents\captain-cabin> Get-ChildItem | Sort-Object Length

    Directory: C:\Users\captain\Documents\captain-cabin

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          9/4/2024  12:50 PM              0 captain-boots.txt
-a----          9/4/2024  12:14 PM            264 captain-hat2.txt
-a----          9/4/2024  12:14 PM            264 captain-hat.txt
-a----          9/4/2024  12:37 PM           2116 ship-flag.txt
d-----          9/4/2024  12:50 PM                captain-wardrobe
```

在这里，`Get-ChildItem` 检索文件（作为对象），管道 （`|`） 将这些文件对象发送到 `Sort-Object，然后 Sort-Object` 按其 `Length` （size） 属性对它们进行排序。这种基于对象的方法允许更详细、更灵活的命令序列。

在上面的示例中，我们利用了 `Sort-Object` cmdlet 根据指定的属性对对象进行排序。除了排序之外，PowerShell 还提供了一组 cmdlet，**当与管道结合使用时，这些 cmdlet 允许进行高级数据作和分析。**

若要根据指定条件筛选对象，仅返回满足条件的对象，可以使用 `Where-Object` cmdlet。例如，要仅列出目录中的 `.txt` 文件，我们可以使用：

```
PS C:\Users\captain\Documents\captain-cabin> Get-ChildItem | Where-Object -Property "Extension" -eq ".txt" 

    Directory: C:\Users\captain\Documents\captain-cabin

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          9/4/2024  12:50 PM              0 captain-boots.txt
-a----          9/4/2024  12:14 PM            264 captain-hat.txt
-a----          9/4/2024  12:14 PM            264 captain-hat2.txt
-a----          9/4/2024  12:37 PM           2116 ship-flag.txt
```

在这里，`Where-Object` 按其 `Extension` 属性过滤文件，确保仅列出扩展名等于 （`-eq`） 的 `.txt` 的文件。

运算符 `-eq`（即“ **等于** ”）是与其他脚本语言（例如 Bash、Python）共享的一组**比较运算符**的一部分。为了显示 PowerShell 过滤的潜力，我们从该列表中选择了一些最有用的运算符：

- `-ne`： “ **不相等** ”。此运算符可用于根据指定的条件从结果中排除对象。
- `-gt`： “ **大于** ”。此运算符将仅过滤超过指定值的对象。需要注意的是，这是一个严格的比较，这意味着等于指定值的对象将被排除在结果之外。
- `-ge`：“ **大于或等于** ”。这是上一个运算符的非严格版本。`-gt` 和 `-eq` 的组合。
- `-lt`： “ **小于** ”。与它的对应项“大于”一样，这是一个严格的运算符。它将仅包括严格低于特定值的对象。
- `-le`：“ **小于或等于** ”。就像它的对应项 `-ge` 一样，这是前一个运算符的非严格版本。`-lt` 和 `-eq` 的组合。

下面，另一个示例显示，还可以通过选择与指定模式匹配（`-like`）的属性来过滤对象：

```
PS C:\Users\captain\Documents\captain-cabin> Get-ChildItem | Where-Object -Property "Name" -like "ship*"  

    Directory: C:\Users\captain\Documents\captain-cabin

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          9/4/2024  12:37 PM           2116 ship-flag.txt
```

下一个筛选 cmdlet `Select-Object` 用于从对象中选择特定属性或限制返回的对象数。它对于优化输出以仅显示所需的详细信息非常有用。

```
PS C:\Users\captain\Documents\captain-cabin> Get-ChildItem | Select-Object Name,Length 

Name              Length
----              ------
captain-wardrobe
captain-boots.txt 0
captain-hat.txt   264
captain-hat2.txt  264
ship-flag.txt     2116
```

可以通过添加更多命令来扩展 cmdlet 管道，因为该功能不仅限于两个 cmdlet 之间的管道。作为练习，请尝试生成 cmdlet 管道来对输出进行排序和筛选，目标是显示 `C:\Users\captain\Documents\captain-cabin` 目录中最大的文件。

```
Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1

    Directory: C:\Users\captain\Documents\captain-cabin

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          9/4/2024  12:37 PM           2116 ship-flag.txt
```

这组筛选 cmdlet 中的最后一个是 `Select-String`。此 cmdlet 搜索文件中的文本模式，类似于基于 Unix 的系统中的 `grep` 或 Windows 命令提示符中的 `findstr`。它通常用于查找日志文件或文档中的特定内容。

```
PS C:\Users\captain\Documents\captain-cabin> Select-String -Path ".\captain-hat.txt" -Pattern "hat" 

captain-hat.txt:8:Don't touch my hat!
```



## 系统和网络信息

PowerShell 的创建是为了满足对强大的自动化和管理工具日益增长的需求，以帮助系统管理员和 IT 专业人员。因此，它提供了一系列 cmdlet，允许检索有关系统配置和网络设置的详细信息。

`Get-ComputerInfo` cmdlet 检索全面的系统信息，包括作系统信息、硬件规格、BIOS 详细信息等。它在单个命令中提供整个系统配置的快照。它的传统对应项 `systeminfo` 只检索一小部分相同的细节。

```
PS C:\Users\captain> Get-ComputerInfo

WindowsBuildLabEx                                       : 20348.859.amd64fre.fe_release_svc_prod2.220707-1832
WindowsCurrentVersion                                   : 6.3
WindowsEditionId                                        : ServerDatacenter
WindowsInstallationType                                 : Server Core
WindowsInstallDateFromRegistry                          : 4/23/2024 6:36:29 PM
WindowsProductId                                        : 00454-60000-00001-AA763
WindowsProductName                                      : Windows Server 2022 Datacenter
[...]
```

`Get-LocalUser` 对于管理用户帐户和了解计算机的安全配置至关重要，它列出了系统上的所有本地用户帐户。默认输出显示每个用户的用户名、账户状态和描述。

```
PS C:\Users\captain> Get-LocalUser

Name               Enabled Description 
----               ------- -----------
Administrator      True    Built-in account for administering the computer/domain
captain            True    The beloved captain of this pirate ship.
DefaultAccount     False   A user account managed by the system.
Guest              False   Built-in account for guest access to the computer/domain
WDAGUtilityAccount False   A user account managed and used by the system for Windows Defender Application Guard scenarios.
```

与传统的 `ipconfig` 命令类似，以下两个 cmdlet 可用于检索有关系统网络配置的详细信息。

`Get-NetIPConfiguration` 提供有关系统上网络接口的详细信息，包括 IP 地址、DNS 服务器和网关配置。

```
PS C:\Users\captain> Get-NetIPConfiguration

InterfaceAlias       : Ethernet
InterfaceIndex       : 5
InterfaceDescription : Amazon Elastic Network Adapter
NetProfile.Name      : Network 3
IPv4Address          : 10.10.178.209
IPv6DefaultGateway   :
IPv4DefaultGateway   : 10.10.0.1
DNSServer            : 10.0.0.2
```

如果我们需要有关分配给网络接口的 IP 地址的特定详细信息，`Get-NetIPAddress` cmdlet 将显示系统上配置的所有 IP 地址的详细信息，包括当前未处于活动状态的 IP 地址。

```
PS C:\Users\captain> Get-NetIPConfiguration

InterfaceAlias       : Ethernet
InterfaceIndex       : 5
InterfaceDescription : Amazon Elastic Network Adapter
NetProfile.Name      : Network 3
IPv4Address          : 10.10.178.209
IPv6DefaultGateway   :
IPv4DefaultGateway   : 10.10.0.1
DNSServer            : 10.0.0.2
```

如果我们需要有关分配给网络接口的 IP 地址的特定详细信息，`Get-NetIPAddress` cmdlet 将显示系统上配置的所有 IP 地址的详细信息，包括当前未处于活动状态的 IP 地址。

**Get-ChildItem -Path . -Recurse -File | Select-String -Pattern "THM"**



## 实时系统分析

为了收集更高级的系统信息，尤其是关于动态方面（如正在运行的进程、服务和活动网络连接）的信息，我们可以利用一组超越静态计算机详细信息的 cmdlet。

`Get-Process` 提供所有当前正在运行的进程的详细视图，包括 CPU 和内存使用情况，使其成为监控和故障排除的强大工具。

同样，`Get-Service` gsv**允许检索有关计算机上服务状态的信息，例如哪些服务正在运行、已停止或已暂停。它被广泛用于系统管理员的故障排除，也被取证分析师用于寻找系统上安装的异常服务。**

```
PS C:\Users\captain> Get-Service

Status   Name               DisplayName                           
------   ----               -----------
Stopped  Amazon EC2Launch   Amazon EC2Launch
Running  AmazonSSMAgent     Amazon SSM Agent
Stopped  AppIDSvc           Application Identity
Running  BFE                Base Filtering Engine
Running  CertPropSvc        Certificate Propagation
Stopped  ClipSVC            Client License Service (ClipSVC)
[...]
```

为了监视活动网络连接，`Get-NetTCPConnection` 显示当前的 TCP 连接，从而深入了解本地和远程终结点。此 cmdlet 在事件响应或恶意软件分析任务期间特别方便，因为它可以发现隐藏的后门或与攻击者控制的服务器建立的连接。

此外，我们还将提到 `Get-FileHash` 作为生成文件哈希的有用 cmdlet，这在事件响应、威胁搜寻和恶意软件分析中特别有价值，因为它有助于验证文件完整性并检测潜在的篡改。

```
PS C:\Users\captain\Documents\captain-cabin> Get-FileHash -Path .\ship-flag.txt    

Algorithm       Hash                      Path 
---------       ----                      ----
SHA256          54D2EC3C12BF3D[...]       C:\Users\captain\Documents\captain-cabin\ship-flag.txt
```

```
Get-NetTCPConnection | Select-Object LocalAddress, LocalPort, OwningProcess, @{Name = "ProcessName"; Expression = { (Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue).Name }}
```

##  脚本编写

**脚本编写**是编写和执行文本文件（称为脚本）中包含的一系列命令的过程，以自动执行通常在 shell（如 PowerShell）中手动执行的任务。

简单来说，脚本就像给计算机一个待办事项列表，脚本中的每一行都是计算机将自动执行的任务。这可以节省时间，减少出错的机会，并允许执行过于复杂或乏味而无法手动完成的任务。随着您对 shell 和脚本的了解越来越多，您会发现脚本可以成为管理系统、处理数据等的强大工具。

使用 PowerShell 学习脚本超出了本会议室的范围。尽管如此，我们必须明白，它的力量使其成为所有网络安全角色的关键技能。

- 对于事件响应人员、恶意软件分析师和威胁猎手等**蓝队**专业人员，PowerShell 脚本可以自动执行许多不同的任务，包括日志分析、检测异常和提取入侵指标 （IOC）。这些脚本还可用于对恶意代码（恶意软件）进行逆向工程或自动扫描系统以查找入侵迹象。
- 对于包括渗透测试人员和道德黑客在内的**红队**来说，PowerShell 脚本可以自动执行系统枚举、执行远程命令以及制作混淆脚本以绕过防御等任务。它与所有类型的系统的深度集成使其成为模拟攻击和测试系统抵御现实世界威胁的强大工具。
- 在网络安全的背景下， **系统管理员**受益于 PowerShell 脚本，用于自动执行完整性检查、管理系统配置和保护网络，尤其是在远程或大规模环境中。PowerShell 脚本可以设计为实施安全策略、监控系统运行状况并自动响应安全事件，从而增强整体安全态势。

无论是防御性还是进攻性使用，PowerShell 脚本都是网络安全工具包中的**一项基本功能。**

在结束有关脚本的这项任务之前，我们不能不提到 `Invoke-Command` cmdlet。

`Invoke-Command` 对于在远程系统上执行命令至关重要，使其成为系统管理员、安全工程师和渗透测试人员的基础。`Invoke-Command` 可实现高效的远程管理，并将其与脚本相结合，**跨多台计算机实现任务自动化。它还可用于在渗透测试人员或攻击者等交战期间在目标系统上执行有效负载或命令。**

让我们通过查阅 `Get-Help`“示例”页面来发现这个强大的 cmdlet 的一些示例用法：

```
PS C:\Users\captain> Get-Help Invoke-Command -examples

NAME
    Invoke-Command
    
SYNOPSIS
    Runs commands on local and remote computers.
    
    ------------- Example 1: Run a script on a server -------------
    
    Invoke-Command -FilePath c:\scripts\test.ps1 -ComputerName Server01
    
    The FilePath parameter specifies a script that is located on the local computer. The script runs on the remote computer and the results are returned to the local computer.

    --------- Example 2: Run a command on a remote server ---------

    Invoke-Command -ComputerName Server01 -Credential Domain01\User01 -ScriptBlock { Get-Culture }

    The ComputerName parameter specifies the name of the remote computer. The Credential parameter is used to run the command in the security context of Domain01\User01, a user who has permission to run commands. The ScriptBlock parameter specifies the command to be run on the remote computer.

    In response, PowerShell requests the password and an authentication method for the User01 account. It then runs the command on the Server01 computer and returns the result.
[...]
```



















































