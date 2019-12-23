![]()
![image.png](https://img.hacpai.com/file/2019/09/image-7a90b8b8.png)

下载链接：https://leif.fun/downloads/books/Linux命令行与shell脚本编程大全.第3版.pdf

百度云：链接:[https://pan.baidu.com/s/1bV1S6Rb7A9han78-Y2j-PA](https://pan.baidu.com/s/1bV1S6Rb7A9han78-Y2j-PA) 密码:82v1
# 2019年09月19日
# 第一部分
## 第3章 基本的bash shell命令
### 3.4 浏览文件系统
常见Linux目录名称

| 目录 | 用途 | 
| --- | --- | 
| / | 虚拟目录的根目录。通常不会在这里存储文件 | 
| /bin | 二进制目录，存放许多用户级的GNU工具 | 
| /boot | 启动目录，存放启动文件 |
| /dev | 设备目录，Linux在这里创建设备节点 | 
| /etc | 系统配置文件目录 |
| /home| 主目录，Linux在这里创建用户目录 |
| /lib | 库目录，存放想IT和应用程序的库文件夹 |
| /media | 媒体目录，可移动媒体设备的常用挂载点 |
| /mnt | 挂载目录，另一个可移动媒体设备的常用挂载点 |
| /opt | 可选目录，常用于存放第三方软件包和数据文件 |
| /proc | 进程目录，存放现有硬件及当前进程的相关信息 |
| /root | root用户的主目录 |
| /sbin | 系统二进制目录，存放许多GNU管理员级工具 |
| /run | 运行目录，存放系统运作时的运行时数据|
| /srv | 服务目录，存放本地服务的相关文件 |
| /sys | 系统目录，存放系统硬件信息的相关文件 |
| /tmp | 临时目录，可以在该目录中创建和删除临时工作文件 |
| /usr | 用户二进制目录，大量用户级的GNU工具和数据文件都存储在这里 |
| /var | 可变目录，用以存放经常变化的文件，比如日志文件 |

### 3.5 文件和目录列表
#### 3.5.1 基本列表功能
`ls`命令最基本的形式会显示当前目录下的文件和目录：

```
root@ubuntu:~# ls
examples.desktop  公共的  模板  视频  图片  文档  下载  音乐  桌面
```

用带`—F`参数的`ls`命令区分文件和目录

```
root@ubuntu:~# ls -F
examples.desktop  公共的/  模板/  视频/  图片/  文档/  下载/  音乐/  桌面/
```
> `-F`会在可执行文件后面加上`*`号

显示隐藏文件和普通文件:

```
root@ubuntu:~# ls -a
.              .dbshell          .ICEauthority   .pm2              .sudo_as_admin_successful  模板
..             .dbus             .local          .presage          .viminfo                   视频
.bash_history  .dmrc             .mongorc.js     .profile          .wget-hsts                 图片
.bash_logout   examples.desktop  .mysql_history  .python_history   .Xauthority                文档
.bashrc        .gconf            .node-gyp       .rnd              .xinputrc                  下载
.cache         .gnupg            .npm            .selected_editor  .xsession-errors           音乐
.config        .hardinfo         .nvm            .ssh              公共的                      桌面
```

显示当前目录下包含的子目录中的文件:

```
root@ubuntu:~# ls -F -R
.:
examples.desktop  公共的/  模板/  视频/  图片/  文档/  下载/  音乐/  桌面/

./公共的:

./模板:

./视频:

./图片:

./文档:

./下载:

./音乐:

./桌面:
```

> 窍门：命令可以合并为`ls -FR`。
> 如果目录结构很庞大的话，输出内容会变得很长，故一般不推荐这么做

#### 3.5.2 显示长列表
`-l`参数会产生长列表格式输出

```
root@medcaptain-virtual-machine:~# ls -l
总用量 44
-rw-r--r-- 1 ubuntu ubuntu 8980 11月 20  2018 examples.desktop
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 公共的
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 模板
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 视频
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 图片
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 文档
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 下载
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 音乐
drwxr-xr-x 2 ubuntu ubuntu 4096 11月 20  2018 桌面
```
**信息解释**

* 文件类型，比如目录（d）、文件（-）、字符型文件（c）、或块设备（b）；
* 文件的权限；
* 文件的硬链接总数；
* 文件属主的用户名；
* 文件属组的组名；
* 文件的大小（字节单位）；
* 文件的上次修改时间；
* 文件名或目录名。

#### 3.5.3 过滤输出列表
简单文本匹配

```
root@ubuntu:~# ls -l examples.desktop
-rw-r--r-- 1 ubuntu ubuntu 8980 11月 20  2018 examples.desktop
```

ls可以识别标准通配符，并在过滤器中使用它们进行模式匹配：
* 问号（?）代表一个字符
* 星号（*）代表零个或多个字符

替代任意位置的单个字符

```
root@ubuntu:~# ls -l my_scr?pt
-rw-r--r-- 1 root root 0 9月  18 11:43 my_scrapt
-rw-r--r-- 1 root root 0 9月  18 11:43 my_script
```

```
root@ubuntu:~# ls -l my*
-rw-r--r-- 1 root root 0 9月  18 11:45 my_file
-rw-r--r-- 1 root root 0 9月  18 11:43 my_scrapt
-rw-r--r-- 1 root root 0 9月  18 11:43 my_script
```

```
root@ ubuntu:~# ls -l my_s*t
-rw-r--r-- 1 root root 0 9月  18 11:43 my_scrapt
-rw-r--r-- 1 root root 0 9月  18 11:43 my_script
```

> 在过滤器中使用星号和问号被称为`文件扩展匹配`，指的是使用通配符进行模式匹配的过程。通配符正式的名称叫做`元字符通配符`。除了星号和问号之外，还有更多的元字符通配符可用用于文件扩展匹配。如中括号`[]`

```
root@ubuntu:~# ls -l my_scr[ai]pt
-rw-r--r-- 1 root root 0 9月  18 11:43 my_scrapt
-rw-r--r-- 1 root root 0 9月  18 11:43 my_script
```

> 使用了中括号以及在特定位置上可能出现的两中字符：a或i。中括号表示一个字符位置并给出多个可能的选择

也可以指定字符范围，例如`[a-i]`

```
root@ubuntu:~# ls -l f[a-i]ll
-rw-r--r-- 1 root root 0 9月  18 13:50 fall
-rw-r--r-- 1 root root 0 9月  18 13:50 fell
-rw-r--r-- 1 root root 0 9月  18 13:50 fill
```

可以使用感叹号`!`将不需要的内容排除在外

```
root@ubuntu:~# ls -l f[!a]ll
-rw-r--r-- 1 root root 0 9月  18 13:50 fell
-rw-r--r-- 1 root root 0 9月  18 13:50 fill
```

### 3.6 处理文件

#### 3.6.1 创建文件

创建空文件

```
root@ubuntu:~# touch test_one
root@ubuntu:~# ls -l test_one
-rw-r--r-- 1 root root 0 9月  18 13:58 test_one
```

改变文件的修改时间，此操作并不会更改文件内容

```
root@ubuntu:~# ls -l test_one
-rw-r--r-- 1 root root 0 9月  18 13:58 test_one
root@ubuntu:~# touch test_one
root@ubuntu:~# ls -l test_one
-rw-r--r-- 1 root root 0 9月  18 13:59 test_one
```

若指向改变访问时间，可使用`-a`参数

```
root@ubuntu:~# ls -l test_one
-rw-r--r-- 1 root root 0 9月  18 13:59 test_one
root@ubuntu:~# touch -a test_one
root@ubuntu:~# ls -l test_one
-rw-r--r-- 1 root root 0 9月  18 13:59 test_one
root@ubuntu:~# ls -l --time=atime test_one
-rw-r--r-- 1 root root 0 9月  18 14:02 test_one
```

> 只是用`ls -l`命令，并不会显示访问时间，这是因为默认显示的是修改时间，若想查看访问时间，需要加入参数：`--time=atime`


#### 3.6.2 复制文件

使用cp复制文件时，若目标文件已经存在，则建议加上`-i`选项，强制shell询问是否覆盖已有文件。

```
root@ubuntu:~# cp -i test_one test_two
cp：是否覆盖'test_two'？ n
```

> `cp` 也支持`*`通配符

#### 3.6.4 链接文件

在系统上需维护同一文件的两份或多份副本，可以采用保存一份物理文件副本和多个虚拟副本的方式，这种虚拟的副本就成为`链接`。链接是目录中指向文件真实路径的占位符，在Linux中有两种不同类型的文件链接：
* 符号链接
* 硬链接

符号链接：实实在在的文件，指向存放在虚拟目录结构中某个地方的另一个文件，这两个通过符号链接在一起的文件，彼此的内容并不相同
要创建一个文件的符号链接，则此原始文件必须存在，然后使用`ln`命令以及`-s`选项来创建符号链接

```
root@ubuntu:~# ls -l data_file
-rw-r--r-- 1 root root 0 9月  18 14:12 data_file
root@ ubuntu:~# ln -s data_file sl_data_file
root@ ubuntu:~# ls -l *data_file
-rw-r--r-- 1 root root 0 9月  18 14:12 data_file
lrwxrwxrwx 1 root root 9 9月  18 14:13 sl_data_file -> data_file
```
> sl_data_file 和 data_file这两个文件大小并不一样，这是因为sl_data_file仅仅只是指向data_file而已，它们的内容并不相同，是两个完全不同的文件（**类似Windows下的快捷方式和执行程序的区别**）
> 
> 另一种证明链接文件是否是独立文件的方法是查看inode编号，这是识别文件或目录的唯一数字，给`ls`命令加`-i`参数即可

```
root@ubuntu:~# ls -i *data_file
31591688 data_file  31591689 sl_data_file
```

> 注意:删除原始文件过后，符号链接的文件也会跟着消失，虽然ls命令也会看到文件存在的踪迹，但是你无法打开它,它们前后显示的颜色会不一样

![image.png](https://img.hacpai.com/file/2019/09/image-2836ff8d.png)

![image.png](https://img.hacpai.com/file/2019/09/image-b810608b.png)

```
root@ubuntu:~# cat sl_data_file
cat: sl_data_file: 没有那个文件或目录
```

硬链接会创建独立的虚拟文件，其中包含了原始文件的信息及位置。但是他们才能够根本上而言是同一个文件。引用硬链接文件等同于引用了源文件。要创建硬链接，原始文件也必须事先存在，只不过这次使用`ln`命令时不需要加额外参数。

```
root@ubuntu:~# ln code_file h1_code_file
root@ubuntu:~# ls -li *code_file
31591688 -rw-r--r-- 2 root root 0 9月  18 14:31 code_file
31591688 -rw-r--r-- 2 root root 0 9月  18 14:31 h1_code_file
```

> 由上述inode编号得知，它们为同一个文件，它们的大小也一模一样，另外，链接计数（列表中第三项）显示这两个文件都有两个链接。（**类似拷贝文件**）

> 注意：只能对同一个存储媒体的文件创建硬链接。要想在不同存储媒体的文件之间创建链接，只能用符号链接
> 
> 复制文件时，可以直接创建原始文件的另一个链接。同一个文件可以拥有多个链接，但是千万别创建软链接文件的软链接。这回形成混乱的链接链，不仅容易断裂，还会造成各种麻烦。
> 当源文件删除时，不会影响链接文件，硬链接的创建，不会像符号链接那样有明显的`->`标志

### 3.7 处理目录
#### 3.7.2 删除目录

删除目录命令：`rmdir`
默认情况下`rmdir`只能删除空目录，若想使用这一命令，则必须先把改文件夹下的所有内容删除掉，而且`rmdir`没有`-i`选项

### 3.8 查看文件内容
#### 3.8.1 查看文件类型
`file`命令

```
root@ubuntu:~# file my_file
my_file: ASCII text
```
> 上述例子中的文件是一个文本文件，file命令不仅可以确定文件中包含的文本信息，还能确定该文本文件中的字符编码，ASCII


文件夹

```
root@ubuntu:~# file new_dir
new_dir: directory
```

链接文件

```
root@ubuntu:~# file sl_data_file
sl_data_file: broken symbolic link to data_file
```

#### 3.8.2 查看整个文件

**1.cat命令**

显示文本文件中所有内容

```
cat test1
```

给所有行加上行号

```
cat -n test1
```

只给有文本的行加上行号

```
cat -b test1
```

隐藏制表符（TAB）

```
cat -T test1
```

> `—T`参数会用`^I`字符组合去替换稳重的所有制表符。


**2.more命令**

```
more <file_name>
```

![image.png](https://img.hacpai.com/file/2019/09/image-a738a945.png)

> `more`命令只支持文本文件中的基本移动，高级功能可以参考`less`命令

**3.less命令**

```
less <file_name>
```
less作为more的升级版，可以实现在文本文件中前后翻动，而且还有一些高级搜索的功能

> less命令是支持鼠标滚动的，可以识别键盘上下键以及上下翻页键而more只支持键盘操控，支持空格和回车翻页，但是不支持上下键

#### 3.8.3 查看部分文件
**1.tail命令**
tail默认显示文本末尾10行内容

```
tail <file_name>
```

若想修改显示行数，请加`-n`参数

```
tail -n <line_num> <file_name>
```

> 若其他进程使用该文件，你可以使用`-f`参数实时预览文件内容变化，实时监控系统日志可以用到。

**2.head命令**
head命令默认显示文件头部10行内容

```
head <file_name>
```

类似`tail`命令，`head`也支持`-n`参数

```
head -n <line_num> <file_name>
```

> 因为文件头内容通常不会改变，所以`head`不支持`-f`参数和特性


扩展：如何查看一个文件第m行到第n行的数据
例如一个文件test，内容为：

```
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
```
现需要查询第3行到第10行的数据，分两种情况：
1.知道一共有多少行的情况

```
head -10 test | tail -8
或
tail -13 test | head -8
```

即：

```
head -<结束行号> file | tail -<结束行号-初始行号+1>
或
tail -<总行数-初始行号+1> file | head -<束行号-初始行号+1>
```
2.不知道一共有多少行的情况

```
head -10 test | tail -8
```
即：

```
head -<结束行号> file | tail -<结束行号-初始行号+1>
```

# 2019年09月27日
## 第4章 更多的bash shell命令
### 4.1检测程序
#### 4.1.1 探查进程
ps命令只会显示运行在当前控制台下的属于当前用户的进程。

Linux系统中使用GNU ps命令支持3中不同类型的命令行参数：

* Unix风格的参数，前面加单破折线；
* BSD风格的参数，前面不加破折线
* GNU风格的长参数，前面加双破折线

##### 1.Unix风格的参数

|    参数   | 描述 |
| -------- | --------------------------------------------- | 
|    -A    |                  显示所有进程                   |
|    -N    |            显示与指定参数不符的所有进程            |
|    -a    |显示除控制进程(session leader)和无终端进程外的所有进程|
|    -d    |             显示除控制进程外的所有进程             |
|    -e    |                   显示所有进程                  |
|-C cmdlist|           显示包含在cmdlist列表中的进程           |
|-G grplist|           显示组ID在grplist列表中的进程           |
|-U userlist|       显示属主的用户ID在userlist列表中的进程      |
|-g grplist|         显示会话或组ID在grplist列表中的进程        |
|-p pdilist|            显示PDI在pdilist列表中的进程          |
|-s sessionlist|显示会话ID在sessionlist列表中的进程|
|-t ttylist|显示终端ID在ttylist列表中的进程|
|-u userlist|显示有效用户ID在userlist列表中的进程|
|-F|显示更多额外输出（相对-t参数而言）|
|-O format|显示默认的输出列以及format列表指定的特定列|
|-M|显示进程的安全信息|
|-c|显示进程的额外调度器信息|
|-f|显示完整的格式输出|
|-j|显示任务信息|
|-l|显示长列表|
|-o format|仅显示由format指定的列|
|-y|不要显示进程标记(process flag，表明进程状态的标记)|
|-z|显示安全标签(security context)信息|
|-H|用层级格式来显示进程（树状，用来显示父进程）|
|-n namelist|定义了WCHAN列显示的值|
|-w|采用宽输出模式，不限宽度显示|
|-L|显示进程中的线程|
|-V|显示ps命令的版本号|

> session leader的概念可参考《Unix环境高级编程（第三版）》第九章内容。
> 
> grplist在不同的Linux发行版中可能不尽相同，有的发行版中grplist代表会话ID，有的发行版中grplist代表有效组ID。
> 
> security context也叫security label，是SELinux采用的声明资源的一种机制。

使用ps命令的关键在于记住最有用的那些参数。每个Linux系统管理员都应该有自己的一组参数，要牢牢记住。

如果想查看系统上运行的所有进程，可用`-ef`参数组合（ps命令允许将多个参数组合在一起）

```
$ ps -ef
UID PID PPID C STIME TTY TIME CMD
root 1 0 0 11:29 ? 00:00:01 init [5]
root 2 0 0 11:29 ? 00:00:00 [kthreadd]
root 3 2 0 11:29 ? 00:00:00 [migration/0]
root 4 2 0 11:29 ? 00:00:00 [ksoftirqd/0]
root 5 2 0 11:29 ? 00:00:00 [watchdog/0]
root 6 2 0 11:29 ? 00:00:00 [events/0]
root 7 2 0 11:29 ? 00:00:00 [khelper]
root 47 2 0 11:29 ? 00:00:00 [kblockd/0]
root 48 2 0 11:29 ? 00:00:00 [kacpid]
68 2349 1 0 11:30 ? 00:00:00 hald
root 3078 1981 0 12:00 ? 00:00:00 sshd: rich [priv]
rich 3080 3078 0 12:00 ? 00:00:00 sshd: rich@pts/0
rich 3081 3080 0 12:00 pts/0 00:00:00 -bash
rich 4445 3081 3 13:48 pts/0 00:00:00 ps -ef 
```
参数解释：

* -e:指定显示所有运行在系统上的进程；
* -f:扩展了输出，这些扩展的列包含了有用的进程：
* UID：启动这些进程的用户
* PID：进程的进程ID
* PPID：父进程的进程号（如果该进程是由另一个进程启动的）
* C:进程声明周期中的CPU利用率
* STIME：进程启动时的系统时间
* TTY：进程启动时的终端设备
* TIME：运行进程需要的累计CPU时间
* CMD：启动的程序名称

若想获得更多的信息，可采用`-l`参数，它会残生一个长格式输出

```
$ ps -l
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
0 S 500 3081 3080 0 80 0 - 1173 wait pts/0 00:00:00 bash
0 R 500 4463 3081 1 80 0 - 1116 - pts/0 00:00:00 ps 
```

多出的参数：

* F：内核分配给进程的系统标记。
* S：进程的状态（O代表正在运行；S代表在休眠；R代表可运行，正等待运行；Z代表僵
化，进程已结束但父进程已不存在；T代表停止）。
* PRI：进程的优先级（越大的数字代表越低的优先级）。
* NI：谦让度值用来参与决定优先级。
* ADDR：进程的内存地址。
* SZ：假如进程被换出，所需交换空间的大致大小。
* WCHAN：进程休眠的内核函数的地址。


##### 2. BSD风格的参数
|参 数| 描 述|
| --- | --- |
|T |显示跟当前终端关联的所有进程|
|a |显示跟任意终端关联的所有进程|
|g |显示所有的进程，包括控制进程|
|r |仅显示运行中的进程|
|x |显示所有的进程，甚至包括未分配任何终端的进程|
|U |userlist 显示归userlist列表中某用户ID所有的进程|
|p |pidlist 显示PID在pidlist列表中的进程|
|t |ttylist 显示所关联的终端在ttylist列表中的进程|
|O |format 除了默认输出的列之外，还输出由format指定的列|
|X |按过去的Linux i386寄存器格式显示|
|Z |将安全信息添加到输出中|
|j |显示任务信息|
|l |采用长模式|
|o |format 仅显示由format指定的列|
|s |采用信号格式显示|
|u |采用基于用户的格式显示|
|v |采用虚拟内存格式显示|
|N |namelist 定义在WCHAN列中使用的值|
|O |order 定义显示信息列的顺序|
|S |将数值信息从子进程加到父进程上，比如CPU和内存的使用情况|
|c |显示真实的命令名称（用以启动进程的程序名称）|
|e |显示命令使用的环境变量|
|f |用分层格式来显示进程，表明哪些进程启动了哪些进程|
|h |不显示头信息|
|k |sort 指定用以将输出排序的列|
|n |和WCHAN信息一起显示出来，用数值来表示用户ID和组ID|
|w |为较宽屏幕显示宽输出|
|H |将线程按进程来显示|
|m |在进程后显示线程|
|L |列出所有格式指定符|
|V |显示ps命令的版本号|

在使用BSD参数时，ps命令会自动改变输出以模仿BSD格式。下例是使用`l`参数的输出：

```
$ ps l
F UID PID PPID PRI NI VSZ RSS WCHAN STAT TTY TIME COMMAND
0 500 3081 3080 20 0 4692 1432 wait Ss pts/0 0:00 -bash
0 500 5104 3081 20 0 4468 844 - R+ pts/0 0:00 ps l 
```

> 注意，其中大部分的输出列跟使用Unix风格参数时的输出是一样的，只有一小部分不同。

* VSZ：进程在内存中的大小，以千字节（KB）为单位。
* RSS：进程在未换出时占用的物理内存。
* STAT：代表当前进程状态的双字符状态码。
许多系统管理员都喜欢BSD风格的l参数。它能输出更详细的进程状态码（STAT列）。双字
符状态码能比Unix风格输出的单字符状态码更清楚地表示进程的当前状态。
第一个字符采用了和Unix风格S列相同的值，表明进程是在休眠、运行还是等待。第二个参
数进一步说明进程的状态。

* <：该进程运行在高优先级上。
* N：该进程运行在低优先级上。
* L：该进程有页面锁定在内存中。
* s：该进程是控制进程。
* l：该进程是多线程的。
* +：该进程运行在前台。

> 从前面的例子可以看出，bash命令处于休眠状态，但同时它也是一个控制进程（在我的会
话中，它是主要进程），而ps命令则运行在系统的前台。

##### 3. GNU长参数

|参 数 |描 述|
| --- | --- |
|--deselect |显示所有进程，命令行中列出的进程|
|--Group grplist |显示组ID在grplist列表中的进程|
|--User userlist |显示用户ID在userlist列表中的进程|
|--group grplist |显示有效组ID在grplist列表中的进程|
|--pid pidlist |显示PID在pidlist列表中的进程|
|--ppid pidlist |显示父PID在pidlist列表中的进程|
|--sid sidlist |显示会话ID在sidlist列表中的进程|
|--tty ttylist |显示终端设备号在ttylist列表中的进程|
|--user userlist |显示有效用户ID在userlist列表中的进程|
|--format format |仅显示由format指定的列|
|--context |显示额外的安全信息|
|--cols n |将屏幕宽度设置为n列|
|--columns n |将屏幕宽度设置为n列|
|--cumulative |包含已停止的子进程的信息|
|--forest |用层级结构显示出进程和父进程之间的关系|
|--headers |在每页输出中都显示列的头|
|--no-headers |不显示列的头|
|--lines n |将屏幕高度设为n行|
|--rows n |将屏幕高度设为n排|
|--sort order |指定将输出按哪列排序|
|--width n |将屏幕宽度设为n列|
|--help |显示帮助信息|
|--info |显示调试信息|
|--version |显示ps命令的版本号|

可以将GNU长参数和Unix或BSD风格的参数混用来定制输出。GNU长参数中一个着实让人
喜爱的功能就是--forest参数。它会显示进程的层级信息，并用ASCII字符绘出可爱的图表。

```
1981 ? 00:00:00 sshd
3078 ? 00:00:00 \_ sshd
3080 ? 00:00:00 \_ sshd
3081 pts/0 00:00:00 \_ bash
16676 pts/0 00:00:00 \_ ps 
```


#### 4.1.2 实时监测进程

top

![image.png](https://img.hacpai.com/file/2019/09/image-96eff688.png)

参数解释：

* PID：进程的ID。
* USER：进程属主的名字。
* PR：进程的优先级。
* NI：进程的谦让度值。
* VIRT：进程占用的虚拟内存总量。
* RES：进程占用的物理内存总量。
* SHR：进程和其他进程共享的内存总量。
* S：进程的状态（D代表可中断的休眠状态，R代表在运行状态，S代表休眠状态，T代表
跟踪状态或停止状态，Z代表僵化状态）。
* %CPU：进程使用的CPU时间比例。
* %MEM：进程使用的内存占可用内存的比例。
* TIME+：自进程启动到目前为止的CPU时间总量。
* COMMAND：进程所对应的命令行名称，也就是启动的程序名。


#### 4.1.3 结束进程
进程信号

| 信 号 | 名 称| 描 述 |
| --- | --- | --- |
|1| HUP |挂起|
|2| INT |中断|
|3| QUIT |结束运行|
|9| KILL |无条件终止|
|11| SEGV |段错误|
|15| TERM |尽可能终止|
|17| STOP |无条件停止运行，但不终止|
|18| TSTP |停止或暂停，但继续在后台运行|
|19| CONT |在STOP或TSTP之后恢复执行|

##### 1. kill命令

只能用进程的PID而不能用命令名
要发送进程信号，你必须是进程的属主或登录为root用户。

```
$ kill 3940
-bash: kill: (3940) - Operation not permitted
```

如果有不服管教的进程，那它通常会忽略这个请求。如果要强制终止，-s参数支持指定其他信号（用信号名或信号值）。
你能从下例中看出，kill命令不会有任何输出。

```
# kill -s HUP 3940 
```

要检查kill命令是否有效，可再运行ps或top命令，看看问题进程是否已停止。

##### 2. killall命令
支持通过进程名而不是PID来结束进程。killall命令也支持通
配符，这在系统因负载过大而变得很慢时很有用。

> 注意，使用这个命令需要安装`psmisc`

```
# killall http*
```

> 警告: 以root用户身份登录系统时，使用killall命令要特别小心，因为很容易就会误用通配符
而结束了重要的系统进程。这可能会破坏文件系统。

# 2019年10月10日

### 4.2 检测磁盘空间
#### 4.2.1 挂载存储媒体
##### 1.mount命令
默认情况下，mount会输出当前系统上挂载的设备列表

```
$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw) sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw) /dev/sdb1 on /media/disk type vfat (rw,nosuid,nodev,uhelper=hal,shortname=lower,uid=503)
```
mount命令提供如下四部分信息:

* 媒体的设备文件名
* 媒体挂载到虚拟目录的挂载点 
* 文件系统类型
* 已挂载媒体的访问状态

上面例子的最后一行输出中，U盘被GNOME桌面自动挂载到了挂载点/media/disk。vfat文件
系统类型说明它是在Windows机器上被格式化的。

手动在虚拟目录中挂载设备，需要以root身份执行

```
mount -t type device directory
```
> type参数指定了磁盘被格式化的文件系统类型

文件类型如下：

* vfat:Windows长文件系统。
* ntfs:Windows NT、XP、Vista以及Windows 7中广泛使用的高级文件系统。 
* iso9660:标准CD-ROM文件系统。

手动将U盘/dev/sdb1挂载到/media/disk

```
mount -t vfat /dev/sdb1 /media/disk
```

mount命令的参数如下：

|参数|描述|
| --- | --- |
|-a|挂载/etc/fstab文件中指定的所有文件系统|
|-f|使mount命令模拟挂载设备，但并不真的挂载|
|-F|和-a参数一起使用时，会同时挂载所有文件系统|
|-v|详细模式，将会说明挂载设备的每一步|
|-I|不启用任何/sbin/mount.filesystem下的文件系统帮助文件|
|-l|给ext2、ext3或XFS文件系统自动添加文件系统标签|
|-n|挂载设备，但不注册到/etc/mtab已挂载设备文件中|
|-p num|进行加密挂载时，从文件描述符num中获得密码短语|
|-s|忽略该文件系统不支持的挂载选项|
|-r|将设备挂载为只读的|
|-w|将设备挂载为可读写的(默认参数)|
|-L label|将设备按指定的label挂载|
|-U uuid|将设备按指定的uuid挂载|
|-O|和-a参数一起使用，限制命令只作用到特定的一组文件系统上|
|-o|给文件系统添加特定的选项|

-o参数允许在挂载文件系统时添加一些以逗号分隔的额外选项。以下为常用的选项。

* ro:以只读形式挂载。
* rw:以读写形式挂载。
* user:允许普通用户挂载文件系统。 
* check=none:挂载文件系统时不进行完整性校验。
* loop:挂载一个文件。


##### 2.umount命令

> Linux上不能直接弹出已挂载的CD。如果你在从光驱中移除CD时遇到麻烦，通常是因为 该CD还挂载在虚拟目录里。先卸载它，然后再去尝试弹出。

```
umount [directory | device ]
```

卸载一个设备之前确保该设备中没有文件正在被使用，否则卸载失败

```
[root@testbox mnt]# umount /home/rich/mnt
umount: /home/rich/mnt: device is busy
umount: /home/rich/mnt: device is busy 12 [root@testbox mnt]# cd /home/rich
[root@testbox rich]# umount /home/rich/mnt
[root@testbox rich]# ls -l mnt
total 0
```

> 如果在卸载设备时，系统提示设备繁忙，无法卸载设备，通常是有进程还在访问该设备或使用该设备上的文件。 这时可用lsof命令获得使用它的进程信息，然后在应用中停止使用该设备或停止该进程。lsof命令的用法很简 单:lsof /path/to/device/node，或者lsof /path/to/mount/point。


#### 4.2.2 使用df命令

```
$ df
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             18251068   7703964   9605024  45% /
/dev/sda1               101086     18680     77187  20% /boot
tmpfs                   119536         0    119536   0% /dev/shm
/dev/sdb1               127462    113892     13570  90% /media/disk
```

命令输出如下：

* 设备的设备文件位置;
* 能容纳多少个1024字节大小的块; 
* 已用了多少个1024字节大小的块; 
* 还有多少个1024字节大小的块可用; 
* 已用空间所占的比例;
* 设备挂载到了哪个挂载点上。


输出中 的磁盘空间按照用户易读的形式显示

```
$ df -h
文件系统        容量    已用  可用  已用% 挂载点
udev           927M     0  927M    0% /dev
tmpfs          190M  1.3M  189M    1% /run
/dev/sda2      117G   11G  100G   10% /
tmpfs          949M     0  949M    0% /dev/shm
tmpfs          5.0M  4.0K  5.0M    1% /run/lock
tmpfs          949M     0  949M    0% /sys/fs/cgroup
/dev/sda1      511M  6.1M  505M    2% /boot/efi
tmpfs          190M  4.0K  190M    1% /run/user/1000
```

> 说明:Linux系统后台一直有进程来处理文件或使用文件。df命令的输出值显示的是Linux系统认 为的当前值。有可能系统上有运行的进程已经创建或删除了某个文件，但尚未释放文件。 这个值是不会算进闲置空间的

#### 4.2.3 使用du命令

```
$ du
484     ./.gstreamer-0.10
8       ./Templates
8       ./Download
8       ./.ccache/7/0
24      ./.ccache/7
368     ./.ccache/a/d
384     ./.ccache/a
424     ./.ccache
8       ./Public
8       ./.gphpedit/plugins
32      ./.gphpedit
72      ./.gconfd
128     ./.nautilus/metafiles
384     ./.nautilus
72      ./.bittorrent/data/metainfo
20      ./.bittorrent/data/resume
144     ./.bittorrent/data
152     ./.bittorrent
8       ./Videos 9 8 ./Music
16      ./.config/gtk-2.0
40      ./.config
8       ./Documents
```

> 注意，这个列表是从目录层级的最 底部开始，然后按文件、子目录、目录逐级向上。

下面是能让du命令用起来更方便的几个命令行参数。

* -c:显示所有已列出文件总的大小。
* -h:按用户易读的格式输出大小，即用K替代千字节，用M替代兆字节，用G替代吉字节。（输出每个文件夹的大小和总占用）
* -s:显示每个输出参数的总计。

![image.png](https://img.hacpai.com/file/2019/10/image-db118e2c.png)

![image.png](https://img.hacpai.com/file/2019/10/image-a7df44b7.png)

![image.png](https://img.hacpai.com/file/2019/10/image-1d206263.png)


### 4.3 处理数据文件

#### 4.3.1 排序数据

按照字母顺序将文件从大到小输出

```
$ du -sh * | sort -nr
1008k   mrtg-2.9.29.tar.gz
972k    bldg1
888k    fbs2.pdf
760k    Printtest
680k    rsync-2.6.6.tar.gz
660k    code
516k    fig1001.tiff
496k    test
496k    php-common-4.0.4pl1-6mdk.i586.rpm
448k    MesaGLUT-6.5.1.tar.gz
400k    plp
```

> 注意，-r参数将结果按降序输出，这样就更容易看到目录下的哪些文件占用空间最多。

#### 4.3.2 搜索数据
grep：在某个文件中查找某个内容

```
grep [options] pattern [file]
```

```
$ grep three file1
three
$ grep t file1
two
three
```

反向搜索(输出不匹配该模式的行)，可加-v参数

```
$ grep -v t file1
one
four
five
```

显示匹配模式的行所在的行号，可加-n参数

```
$ grep -n t file1
2:two
3:three
```

知道有多少行含有匹配的模式，可用-c参数

```
$ grep -c t file1
2
```

指定多个匹配模式，可用-e参数来指定每个模式

```
$ grep -e t -e f file1
two
three
four
five
```

使用正则表达式

```
$ grep [tf] file1
two
three
four
five
```

> egrep命令是grep的一个衍生，支持POSIX扩展正则表达式。POSIX扩展正则表达式含有更 多的可以用来指定匹配模式的字符(参见第20章)。fgrep则是另外一个版本，支持将匹配模式 指定为用换行符分隔的一列固定长度的字符串。这样就可以把这列字符串放到一个文件中，然后 在fgrep命令中用其在一个大型文件中搜索字符串了。


#### 4.3.3 压缩数据

Linux上的文件压缩工具

|工具|文件扩展名|描述|
| --- | --- | --- |
|bzip2|.bz2|采用Burrows-Wheeler块排序文本压缩算法和霍夫曼编码|
|compress|.Z|最初的Unix文件压缩工具，已经快没人用了|
|gzip|.gz|GNU压缩工具，用Lempel-Ziv编码|
|zip|.zip|Windows上PKZIP工具的Unix实现|

gzip工具

* gzip:用来压缩文件。
* gzcat:用来查看压缩过的文本文件的内容。 
* gunzip:用来解压文件。

> 这些工具基本上跟bzip2工具的用法一样。

```
$ gzip myprog
$ ls -l my*
-rwxrwxr-x 1 rich rich 2197 2007-09-13 11:29 myprog.gz
```

使用通配符

```
$ gzip my*
```

#### 4.3.4 归档数据
下面是tar命令的格式:

```
tar function [options] object1 object2 ...
```

|功能|长名称|描述|
| --- | --- | --- |
|-A|--concatenate|将一个已有tar归档文件追加到另一个已有tar归档文件|
|-c|--create|创建一个新的tar归档文件|
|-d|--diff|检查归档文件和文件系统的不同之处|
||--delete|从已有tar归档文件中删除|
|-r|--append|追加文件到已有tar归档文件末尾|
|-t|--list|列出已有tar归档文件的内容|
|-u|--update|将比tar归档文件中已有的同名文件新的文件追加到该tar归档文件中|
|-x|--extract|从已有tar归档文件中提取文件|

|选项|描述|
| --- | --- |
|-C dir|切换到指定目录|
|-f file|输出结果到文件或设备file|
|-j|将输出重定向给bzip2命令来压缩内容|
|-p|保留所有文件权限|
|-v|在处理文件时显示文件|
|-z|将输出重定向给gzip命令来压缩内容|


```
tar -cvf test.tar test/ test2/
```

上面的命令创建了名为test.tar的归档文件，含有test和test2目录内容。接着，用下列命令:

```
tar -tf test.tar
```
列出tar文件test.tar的内容(但并不提取文件)。最后，用命令:

```
tar -xvf test.tar
```

> 窍门: 下载了开源软件之后，你会经常看到文件名以.tgz结尾。这些是gzip压缩过的tar文件可以 用命令tar -zxvf filename.tgz来解压。

补充：
打包

```
tar czvf xx.tar xx
```
```
zip -r xx.zip xx
```

解压到当前目录

```
tar xzvf xx.tar
```
```
unzip xx.zip
```

解压到指定目录

```
tar xzvf xx.tar -C <dir>
```
```
unzip zz.zip -d <dir>
```
