

# 观前提示

本篇文章有5348字，看完需28分钟左右。

# 写在前面

本篇讲解的是一些Linux使用的一些基础常用的指令，非常适合Linux小白学习。所以那么如果你是刚刚开始接触Linux（无图形化操作界面）的小白，那么请从头到尾仔细地阅读这篇文章（也可以跟着操作），本篇文章将逐步为你讲解一些Linux系统中基础常用的指令，这些指令基本满足你在Linux系统中的日常操作需求。

当然，本篇文章的内容很干，看完甚至你会觉得没有什么收获，指令也压根记不住。但是没关系，因为这些指令事实上这些操作和指令只是Linux使用的一些基本的东西，没有什么技巧理论性可言。我们只需要能做到，认识这些操作和指令，然后在以后的日常Linux使用的时候，慢慢地熟悉这些指令和操作就行。所以，希望本篇文章能够帮助你初步熟悉Linux的操作。并初步建立对Linux系统的认知。

# ls指令

语法：ls [选项] [目录或文件]

功能：对于目录，该命令列出该目录下的所有子目录与文件。对于文件，将列出文件名以及其他信息

常用选项：

* -a 列出目录下的所有文件，包括以 . 开头的隐含文件。
* -d 将目录像文件一样显示，而不是显示其下的文件。如： ls -d 指定目录
* -i 输出文件的i节点的索引信息。如 ls -ai 指定文件
* -k 以k字节的形式表示文件的大小。ls -alk 指定文件
* -l 列出文件的详细信息。可简略为： ll 指定文件
* -n用数字的 UID,GID代替名称。UID,即用户id，GID，即所属组id
* -F 在每个文件名后附上一个字符以说明该文件的类型，"*"表示可执行的普通文件；"/"表示目录；"@"表
  示符号链接；"|"的表示FlFOs；"=''表示套接字(sockets)。（目录类型识别）
* -r 对目录反向排序。
* -t 以时间排序。
* -s 在文件名后输出该文件的大小。
* R 列出所有子目录下的文件。（递归）
* -1 一行只输出一个文件。

演示：

* ls	虽然没有指定对象，但是默认为当前目录即

  ![image-20221204142023369](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212041420417.png)

* ll	即ls -l的缩写

  ![image-20221204142058733](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212041420769.png)

* ls -al    即ls -a -l

  ![image-20221204142143147](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212041421192.png)

* ls 目录 与  ls -d 目录

  ![image-20221204142244219](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212041422256.png)

可以看出来以上**选项可以结合起来使用的**，事实上，对于Linux的大多数指令选项的使用也是如此。

而对于显示出来的内容，例如使用指令ll时显示的文件相较于ls显示的信息更加详细，那么这些具体多出来的一个个信息是什么呢？有一些简单的信息，例如时间，大小自然是很容易就能看出来，但是其他信息由于涉及到权限或者其他的问题，我就暂且现在这按下不表，之后会在关于Linux权限的博文里讲解。

还有，使用ls -a时相较于ls指令多出来两个目录，一个是一个点，另一个是两个点。这又是什么呢，为什么会有这个呢？首先，一个点代表的目录即是当前目录，两点代表的是上级目录。而为什么呢？对于初学者来说，目前我们只能建立的一个浅显的理解就是为了能够管理使用当前目录文件（例如ls指令不指定文件或目录默认当前目录）以及能在各级目录之间跳转。

# pwd指令

语法：pwd

功能：显示用户当前所在目录

使用演示：

![image-20221204142337467](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212041423505.png)

# cd指令

Linux系统中，磁盘上的文件和目录是以树的形式管理起来的，树上的每个节点都是目录或文件。对于有过win系统使用经验的人来说，理解起来很容易。通过树的形式，我们可以通过路径确定并找到磁盘中对应的文件而cd指令的功能就类似于此。

此外，在win系统中，通常将存储文件的集合叫做文件夹，而在Linux系统中，我们通常称之为目录。

语法：cd 目录名

功能：改变工作目录。将当前工作目录改变到指定的目录下

![](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011201921.jpg)

使用演示：

* 正常跳转

  ![image-20221201125506128](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011255216.png)

* cd ..  返回上级目录

  ![image-20221201145355453](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011453522.png)

* 绝对路径

  ![image-20221201151437926](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011514011.png)

* 相对路径

  ![image-20221201151813513](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011518604.png)

* cd ~ 返回家目录，即home下的以用户名文目录为名的目录

  ![image-20221201152212820](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011522906.png)

* cd - 返回最近访问目录

  ![image-20221201152459798](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011524883.png)

# touch指令

语法：touch [选项]  [文件]

功能：touch指令可更改文档或目录的日期时间，包括存取时间和更改时间，或者新建一个不存在的文件。

常用选项：

* -a 或--time=atime或--time=access或--time=use只更改存取时间。
* -c 或--no-create    不建立任何文档。
* -d 使用指定的日期时间，而非现在的时间
* -f  此参数将忽略不予处理，仅负责解决BSD版本touch指令的兼容性问题。
* -m 或--time=mtime或--time=modify    只更改变动时间。
* -r 把指定文档或目录的日期时间，统统设成和参考文档或目录的日期时间相同。
* -t 使用指定的日期时间，而非现在的时间.

使用演示：

* 创建新文件

  ![](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011410568.png)

* 更新文件时间，touch指定已存在文件，不加选项默认更新全部时间

  ![image-20221201144346795](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011443874.png)



# mkdir指令

语法：mkdir [选项] dirname

功能：在当前目录下创建一个名为"dirname"的目录

常用选项：

-p，--parents   可以是一个路径名称。此时若路径中的某些目录尚不存在，加上此选项后，系统自动建立好那些尚不存在的目录，即一次可以建立多个目录

使用演示：

![image-20221201154418526](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011544614.png)

# rmdir&&rm指令

与mkdir指令相对，rmdir是针对目录的删除命令

语法：rmdir [-p] [dirname]

适用对象：具有当前目录操作权限的所有使用者（对于权限的知识，我之后专门发表一篇blog讲解）

功能；删除空目录

常用选项：

-p 当子目录被删除后，如果父目录也变成空目录则连带空目录一并删除

使用演示：

![image-20221201163948005](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011639070.png)

而rm指令可以用来删除文件或目录

语法：rm [选项] [dirneme/filename]

适用对象：所有使用者

功能：删除文件或目录

常用选项：

* -f 即使文件属性为只读（即写保护，当然这部分知识是属于权限的内容），也直接删除
* -i 删除前逐一询问确认
* -r 删除目录及其下所有文件

使用演示：

* 删除普通文件

  ![image-20221201165807912](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011658957.png)

* 强制删除

  ![image-20221201171133895](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011711009.png)

* 删除目录

  ![image-20221201172902679](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011729770.png)



# man指令

学完以上几个指令会发现，Linux的指令常常带有很多选项，事实上上文的指令选项都是不齐的，那么这么多选项需要一个个记无疑大大提升Linux的使用成本，所以为了解决这个问题，Linux可以通过man指令访问联机手册来查询命令详情。

语法：man [选项] 命令

常用选项：

* -k 根据关键字搜索联机帮助

* num 即一个数字，只在第num章节找

* -a 将所有章节的对应内容都显示出来

* 简单解释一下，手册分为8章

  1 普通命令

  2 系统调用，如open,write之类的（通过这个，至少可以很方便的查到调用这个函数，需要加什么头文件）

  3 库函数，如printf,fread

  4 特殊文件，也就是/dev下的各种设备文件

  5 文件的格式，比如passwd，就会说明这个文件中各个字段的含义

  6 给游戏留的，由各个游戏自己定义

  7 附件以及一些变量，比如environ这种全局变量在这章就由说明

  8 系统管理用的命令，这些命令只能由root（超级管理员）使用，如ifconfig

使用演示：

* man man

  ![image-20221201183524839](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011835927.png)

  ![image-20221201183308639](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011833764.png)

  ![](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212011835538.png)

* man -a printf   前面说过，手册分别有8章，如果在选项带数字的话就定向在该章中寻找。如果不带任何选项的话就默认找到顺序搜索找到的第一个就停止。而-a选项则是会找完最后一个才停止，或者用户主动暂停。

  ![image-20221202152254315](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021522432.png)

  ![image-20221202152107556](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021521734.png)

  ![image-20221202152549758](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021525882.png)

  ![image-20221202152640112](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021526235.png)

  

# cp指令

语法：cp [选项] 源文件或目录 目标文件或目录

功能：复制文件或目录

说明：cp指令用于复制文件或目录，如果同时指定两个以上文件或目录，且最后目的地是一个已经存在的目录，则会把前面指定的所有文件或目录复制到此目录中。但是，同时指定复制多个文件或目录**且最后目的地并非是一个已存在的目录**则会出现错误信息。

常用选项：

* -f 或 --force强行复制文件或目录，不论目的文件或目录是否已经存在
* -i 或 --interactive覆盖文件之前先询问用户
* -r 递归处理，将指定目录下的文件与子目录一并处理。若源文件或目录的形态，不属于目录或符号链
  接，则一律视为普通文件处理
* -R 或 -recursive递归处理，将指定目录下的文件及子目录一并处理

使用演示：

简单演示一些cp -r

![image-20221202171027182](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021710410.png)



# mv指令

mv，即move的缩写，那么mv指令自然是用来移动文件的，除此之外，mv指令还能使文件重命名。

语法：mv [选项] 源文件或目录 目标文件或目录

功能：

* **最后一个参数名（目录名或文件名）对应的文件或目录是<u>存在</u>的时**，mv指令的功能就是**移动指定的文件或目录**，但是目标参数对应的必须是目录，如果是文件就会报错

* **最后一个参数名（目录名或文件名）对应的文件或目录是<u>不存在</u>的时**，mv指令的功能就是**将目录或文件重命名**

常用选项：

* -f 即force，强制的意思，如果目标文件已经存在，不会询问而直接覆盖

  ![image-20221202175846780](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021758915.png)

* -i 若指定文件在目标位置已经存在，就会询问是否覆盖‘

  ![image-20221202180118283](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021801425.png)

  

# cat指令

语法：cat [选项] [文件]

功能：查看目标文件的内容

常用选项：

* -b 对非空输出行编号
* -n 对输出的所有行编号
* -s 不输出多行空行

使用演示：

![image-20221202184023337](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021840460.png)



# more指令

功能类似于cat

语法：more [选项] [文件]

 常用选项：

* -n 对输出的所有行编号
* q 退出more

使用演示;

![image-20221202184141952](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021841080.png)

![image-20221202184527320](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212021845509.png)



# less指令

less工具也是对文件或其它输出进行分页显示的工具，可以说是linux正统查看文件内容的工具，功能极其强大。less的用法比起more更加的有弹性。**在more的时候，我们并没有办法向前面翻，只能往后面看**。但若使用了less时，就可以**使用[pageup]\[pagedown]等按键的功能来往前往后翻看文件，更容易用来查看一个文件的内容！**除此之外，在less里头可以拥有更多的搜索功能，不止可以向下搜，也可以向上搜

语法：less [参数] 文件

选项：

* -i 忽略搜索时的大小写
* -N 显示每行的行号
* / 字符串：向下搜索"字符串"的功能
* ? 字符串：向上搜索“字符串“的功能
* n 重复前一个搜索（与/或？有关）
* N 反向重复前一个搜索（与/或？有关）
* q quit

使用演示：

![image-20221202221425067](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212022214475.png)



# head&&tail指令

head和tail指令的功能正如名字所写，用于显示开头或结尾n行的文字块。

head用于显示档案的开头至标准输出中，默认显示10行

语法：head [参数] [文件]

选项：

-n<行数> 显示的行数

使用演示：

![image-20221202230834896](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212022308024.png)

tail命令从指定点开始将文件写到标准输出。不指定文件时用于对输入信息进行处理，最常见的场景还是查看日志文件。

使用tail命令的-f选项可以方便的**查阅正在改变的日志文件**，**tail -f filename会把filename里最尾部的内容显示在屏幕上，并且不断刷新**，为你显示最新的文件内容。

语法：tail [必要参数] [选择参数] [文件]

常用选项：

* -f 循环读取
* -n<行数> 显示行数】、

使用演示：

![Untitled ‑ Made with FlexClip](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212031347886.gif)

可以看到，我在右边窗口对demo文件进行写入时，[tail -f demo]命令在实时的更新显示内容。

# 时间相关的指令

## date显示

date指定格式显示时间：date +%Y:%m:%d

语法：date [OPTION]... [+FORMAT]

常用参数：

1. 设定显示格式，使用加号，在加号后接标记，常用标记如下：

   * %H：小时（00~23）
   * %M：分钟（00~59）
   * %S：秒（00~60）
   * %X：相当于 %H:%M:%S
   * %d：日（01~31）
   * %m：月份（01~12）
   * %Y：完整年份（0000~9999）
   * %F：相当于%Y-%m-%d

2. 设定时间：

   * date -s //设置当前时间，只有root（超级管理员）权限才能设置，其他只能查看
   * date -s 20080523 //设置成20080523， 这样会把具体时间设置成空00:00:00
   * date -s 01:01:01 //设置具体时间，不会对日期做更改
   * date -s “01:01:01 2008-05-23” //这样可以设置全部时间
   * date -s “01:01:01 20080523” //这样可以设置全部时间
   * date -s “2008-05-23 01:01:01” //这样可以设置全部时间
   * date -s “20080523 01:01:01” //这样可以设置全部时间

3. 时间戳

   时间 -> 时间戳：date +%s

   时间戳 -> 时间：date -d@"时间戳"

   ![image-20221203152919741](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212031529943.png)

   Unix时间戳 （英文为Unix epoch,Unix time,POSIX time或Unix timestamp)是从1970年1月1日 （UTC/GMT的午夜）开始所经过的秒数，不考虑闰秒。



# cal指令

用于显示公历（日历）的指令。没有参数时默认显示当前月份，只有一个数字作参数默认当作年份（1~9999）显示该年月历。

语法：cal [参数] [月份] [年份]

常用选项：

* -3 显示系统前一个月，当前月，下一个月的月历
* -j 显示在当年中的第几天（一年日期按天算，从1月1号算起，默认显示当前月在一年中的天数）
* -y 显示当前年份的日历

使用演示：

![image-20221203161140933](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212031611318.png)

# find指令

在Linux系统中，可以使用find命令**在目录结构（文件树）中搜索文件，并执行指定的操作**。find命令提供了相当多的查找条件，功能很强大。一个强大的搜索指令的选项自然很多，其中大部分选项都值得我们花时间来了解一下。即使系统中含有网络文件系统（NFS），find命令在该文件系统中同样有效，只要你**具有相应的权限**。对于，Linux使用来说，这是一个**很常用很重要**的命令。

在运行一个非常消耗资源的find命令时，很多人都倾向于把它放在后台执行，因为遍历一个大的文件系统可能会花费很长的时间（这里是指30G字节以上的文件系统）。

语法：find pathname -options

常用选项：

-name 按照文件名查找文件

使用演示：

![image-20221203165916189](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212031659590.png)

# grep指令

关键字检索筛选，可与find命令结合使用。

语法：grep [选项] "搜寻字符串" 文件

功能：在文件中搜索字符串，将找到的行打印出来

常用选项：

* -i 忽略大小写的不同， 所以大小写视为相同
* -n 顺便输出行号
* -v 反向选择， 亦即显示出没有"搜寻字符串"内容的那一行

使用演示：

![image-20221203170748952](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212031707216.png)

# zip/unzip指令

.zip文件应该都不陌生吧。在Linux中，zip指令用于压缩文件，将目录或文件压缩成zip格式。

语法：zip [参数] [打包后的文件名] [目录或文件]

常用选项：

-r 递归处理，将指定目录下的所有文件和子目录一并处理

使用演示：

![image-20221203215827945](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032158034.png)

语法：unzip [参数] [待解压文件]

常用选项：

-d 指定解压路径

使用演示：

* 直接解压

  ![image-20221203221017058](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032210092.png)

* 指定路径解压

  ![image-20221203221241272](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032212349.png)

# tar指令

**打包/解包**命令，同样是一个非常实用的命令。

语法：tar [选项]  [文件或目录]

常用选项：

* -c：建立一个压缩文件的参数指令（create的意思）
* -x：解开一个压缩文件的参数指令！
* -t：查看tarfile里面的文件！
* -z：是否同时具有gzip的属性？亦即是否需要用gzip压缩？
* -j：是否同时具有bzip2的属性？亦即是否需要用bzip2压缩？
* -v：压缩的过程中显示文件！这个常用，但不建议用在背景执行过程！
* -f：使用档名，请留意，在f之后要立即接档名喔！不要再加参数！
* -C：解压到指定目录（catalogue）

使用演示：

* 打包

  参数f之后的文档名是自己取的，但是，我们通常习惯以.tar为标识。

  如果加z参数，则以.tar.gz或.tgz来代表gzip压缩过的tar file

  如果加j参数，则以.tart.bz2为标识

  ![image-20221203232706610](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032327707.png)

* 查看打包/压缩文件的信息 -t

  ![image-20221203233517190](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032335269.png)

* 解压缩 -x

  ![image-20221203234140313](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032341411.png)

* 只解压缩压缩文件中的一个文件，与前面查看压缩包信息配合使用

  ![image-20221203234619411](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032346493.png)



# bc指令

用于浮点运算，bash（按下不表，之后会有提及）内置了对整数四则运算的支持，但不支持浮点数，故有bc指令。

![image-20221203234855108](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212032348199.png)

# uname指令

语法：uname [选项]

功能：uname用来获取主机所有硬件的名称、操作系统的版本等相关信息

常用选项：

-a 或-all详细输出所有信息，依次为内核名称，主机名，内核版本号，内核版本，硬件名，处理器类型，硬件平台类型，操作系统名称

演示：

![image-20221204000142781](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212040001902.png)

# “|”管道符（扩展）

管道符|，也是一个非常实用的符号，本篇文章就已经多次使用过此符号。管道在显示生活中是一种用来传输某种物质的工具，而Linux系统中，管道符也是用来传输东西的！**在Linux系统中，管道符会将管道符左侧指令原本需要输出的信息传输到管道右侧的指令，为该指令提供操作对象，即左侧命令的输出会变成右侧命令的输入。**并且可以同时使用多个管道符。

演示：

![image-20221204113006453](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202212041130524.png)



# 结语

以上就是关于Linux中一些基本操作及指令的讲解，就如开头我所写，本篇内容基本上都是干货，读起来大概会枯燥乏味，而如果你能读到这里，那么恭喜你啃完了这些“用处不大”，非常基本非常基础的东西，日后只需要在Linux使用中慢慢多使用，多熟悉，自然就能消化了。

如果你觉得本篇写得还不错的话请多多点赞收藏加分享，当然如果发现我写的有错误或者对文章内容排版之类的有建议给我的话也欢迎在评论区或者私信告诉我。
