1. linux目录结构
	绝对路径	/
	
	相对路径	.当前目录	..上一级目录	临近目录切换-	主目录~

	ann@ecs-bd1b~:$	ann当前登陆用户    @at   ecs-bd1b主机名    ~当前工作目录位置    $普通用户    #超级用户

	bin 可执行的系统级的二进制命令
	boot 系统开机是需要加载的一些文件和配置
	dev 设备文件所在目录
	etc 包含当前操作系统用户所有配置的相关信息
	home 当前操作系统所安装用户的主目录
	lib 库文件以及相关的配置都放在此目录下
	media 系统自动挂载目录
	mnt 手动挂载目录
	opt 第三方协议软件安放位置
	root root用户宿主目录
	sbin 超级用户需要用到的一些二进制命令
	usr unix软件资源包管理目录，存放当前用户下的一些东西
	srv 一些网络服务器启动后，这些服务器需要取用的资料目录
	proc 内核提供的一个接口，存储系统统计信息
	run 存放系统运行时需要的一些文件

ls
	-a 包含隐藏文件内容
	-r 反序
	-l 文件权限，所有者，文件大小等信息

cd
	cd ./robertohuang   相对路径
	cd /home/ann    绝对路径
	..
	.当前目录
	

pwd    print working directory

创建
	文件     touch + 文件名
	目录     mkdir + 目录名		mkdir world       mkdir -p world/a/b  创建多级目录加参数-p

删除
	rm file.txt
	rm -rf dir
	-r 递归删除	-i 提示用户是否需要删除目录和文件	-f 强制删除（默认）

cp 
	cp file.txt filecopy.txt  不存在创建，存在覆盖
	cp -r dir1 dir2 将目录dir1中的内容拷贝到dir2中

scp
	scp 用户名@ip:文件位置 需要保存位置   将ip上的文件拷贝到本地
	scp 文件位置 用户名@ip:需要保存的位置
	scp -i 本机中该ip的密钥位置 文件位置 用户名@ip:需要保存的位置

cat	将文件内容全部输出到终端

more	more file 将文件内容分页输出到终端，不能上下滑	回车：下一行	空格：下一页	ctrl+c或q：退出
less	less file 将文件内容分页输出到终端，可以自由上下浏览  回车：下一行    空格：下一页    ctrl+c或q：退出
head	head -5 file 查看前5行内容
tail	tail -5 file 查看后5行内容

wc	wc file 查看文件字数，字节数，行数	-C只显示字节数	-l只显示行数	-w只显示字数
od	查看二进制文件信息
du	查看某个目录的大小
df	查看磁盘的使用情况

which	查看指定命令所在的路径

whoami	查看当前登陆用户

chmod	change mode修改访问权限
	文字设定法	chmod [who] [+-=] [mode] 文件名
		[who] u(user用户) g(group)同组用户 o(other其他用户)  a(all所有用户)
		+ 添加权限	- 取消权限	=赋予给定权限并取消其他权限
		mode: r读	w写	x执行
	数字设定法

chown 将指定文件的拥有者改为指定用户或组
	chown yang text.txt
	chown yang:yang text.txt

chgrp	chgrp yang text.txt

find	find 路径 -name 文件名
	find 路径 -size 范围	+100k | -100k | 100M(代表等于)	(M必须大写 k必须小写)
	find 路径 -type 类型	f(普通文件) | d(目录) | l(符号链接) | b(块设备文件) | c(字符设备文件) | s(socket文件) | p(管道)

grep -r "查找关键字" 路径

tar xvf file.tar		解压
tar cvf file.tar DirName	打包

gunzip file.gz		gzip -d file.gz
gzip filename

tar -zxf file.tar.gz
tar -zcf file.tar.gz DirName

bunzip file.bz2		bzip2 -d file.bz2
bzip -z file.bz2

tar jxvf file.tar.bz2
tar jcvf file.tar.bz2 DirName

bunzip2 file.bz		bzip2 -d file.bz

tar jxvf file.tar.bz

uncompress file.Z
compress file.Z

tar Zxvf file.tar.Z
tar Zcvf file.tar.Z DirName

unzip file.zip
zip file.zip DirName

unrar e text.rar	unrar x test.rar path

lha -e file.lha

who 查看当前在线用户的情况

ps 系统内部所运行的进程状况
	-a(all) 	-u(查看进程的所有者及其他的一些信息)   -x(显示没有控制终端的进程--不能与用户进行交互的进程)
	-e(显示所有进程)   -f
	ps aux

kill	kill -9 666
env	查看当前进程环境变量
top	任务管理器

ifconfig	获取网络接口配置信息
ping  [param: -c   -i]  
nslookup


useradd [-s /bin/bsh] [-g grouptest] [-d /home/usertest] -m[用户家目录不存在是，自动创建该目录]
groupadd 用户组名
deluser
userdel -r usertest	把用户的主目录一起删除
su passwd 用户名	设置密码
exit	退出登陆用户

clear
man

echo 字符串 | $PATH 

free -m | -g | -k

shutdown -t | -r | -h | -n | -f | -F | -c	

声明变量
A=1

撤销变量
unset A

声明静态变量 readonly B=1
不能unset，重启时自动消失

变量定义规则
变量名称可以由字母、数字和下划线组成，但是不能以数字开头，**环境变量名建议大写**
**等号两侧不能有空格**
在bash中，变量默认类型都是字符串类型，无法直接进行数值运算
变量的值如果有空格，需要使用双引号或单引号括起来
	D="I love banzhang"
	echo $D
可把变量提升为全局环境变量，可供其他Shell程序使用
	export 变量名


$n
功能描述：n为数字，$0代表该脚本名称，$1-$9代表第一到第九个参数，十以上的参数，十以上的参数需要用大括号包含，如${10}

$#
功能描述：获取所有输入参数个数，常用于循环

$\*
功能描述：这个变量代表命令行中所有的参数，$\*把所有的参数看成一个整体

$@
功能描述：这个变量也代表命令行中所有的参数，不过$@把每个参数区分对待

$?
功能描述：最后一次执行的命令的返回状态。如果这个变量的值为0，证明上一个命令正确执行；如果这个变量的值为非0（具体是哪个数，由命令自己来决定），则证明上一个命令执行不正确了

**运算符**
“$((运算式))”或“$[运算式]”
expr  + , - , \*,  /,  %   加，减，乘，除，取余	**注意：expr运算符间要有空格**
expr `expr 2 + 3` \* 4  
expr 3 - 2

条件判断
[ condition ]（注意condition前后要有空格）
注意：条件非空即为true，[ atguigu ]返回true，[] 返回false

两个整数之间比较
= 字符串比较
-lt 小于（less than）		-le 小于等于（less equal）
-eq 等于（equal）		-gt 大于（greater than）
-ge 大于等于（greater equal）	-ne 不等于（Not equal

按照文件权限进行判断
-r 有读的权限（read）		-w 有写的权限（write）		-x 有执行的权限（execute）


按照文件类型进行判断
-f 文件存在并且是一个常规的文件（file）		-e 文件存在（existence）	-d 文件存在并是一个目录（directory）

[ -w helloworld.sh ]
echo $?
0

多条件判断（&& 表示前一条命令执行成功时，才执行后一条命令，|| 表示上一条命令执行失败后，才执行下一条命令）
[atguigu@hadoop101 ~]$ [ condition ] && echo OK || echo notok
OK
[atguigu@hadoop101 datas]$ [ condition ] && [ ] || echo notok
notok

**流程控制**

if
if [ 条件判断式 ];then 
  程序 
fi 
或者 
if [ 条件判断式 ] 
  then 
    程序 
fi
**注意事项：**
（1）[ 条件判断式 ]，中括号和条件判断式之间必须有空格
（2）if后要有空格


case 语句
case $变量名 in 
 "值1"） 
    如果变量的值等于值1，则执行程序1 
    ;; 
  "值2"） 
    如果变量的值等于值2，则执行程序2 
    ;; 
  …省略其他分支… 
  \*） 
    如果变量的值都不是以上的值，则执行此程序 
    ;; 
esac
**注意事项：**
    1) case行尾必须为单词“in”，每一个模式匹配必须以右括号“）”结束。
    2) 双分号“;;”表示命令序列结束，相当于java中的break。
    3) 最后的“*）”表示默认模式，相当于java中的default。

for 循环
for (( 初始值;循环控制条件;变量变化 )) 
  do 
    程序 
  done

for 变量 in 值1 值2 值3… 
do 
    程序 
done

比较$\*和$@区别
$\*和$@都表示传递给函数或脚本的所有参数，不被双引号“”包含时，都以$1 $2 …$n的形式输出所有参数
当它们被双引号“”包含时，“$\*”会将所有的参数作为一个整体，以“$1 $2 ... $n”的形式输出所有参数；“$@”会将各个参数分开，以“$1” “$2”…”$n”的形式输出所有参数


**while 循环**
while [ 条件判断式 ] 
  do 
    程序
  done


**read读取控制台输入**
read(选项)(参数)
选项：
-p：指定读取值时的提示符；
-t：指定读取值时等待的时间（秒）

basename基本语法
basename [string / pathname] [suffix] 
功能描述：basename命令会删掉所有的前缀包括最后一个（‘/’）字符，然后将字符串显示出来

dirname基本语法
dirname 文件绝对路径	
功能描述：从给定的包含绝对路径的文件名中去除文件名（非目录的部分），然后返回剩下的路径（目录的部分）

自定义函数
[ function ] funname[()]
{
	Action;
	[return int;]
}
funname

必须在调用函数地方之前，先声明函数，shell脚本是逐行运行。
函数返回值，只能通过$?系统变量获得，可以显示加：return返回，如果不加，将以最后一条命令运行结果，作为返回值。return后跟数值n(0-255)

cut
cut的工作就是“剪”，具体的说就是在文件中负责剪切数据用的。cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段输出

cut [选项参数]  filename
默认分隔符是制表符

-f	列号，提取第几列
-d	分隔符，按照指定分隔符分割列

sed
sed是一种**流编辑器**，它一次处理一行内容。处理时，把当前处理的行存储在临时缓冲区中，称为“模式空间”，接着用sed命令处理缓冲区中的内容，处理完成后，把缓冲区的内容送往屏幕。接着处理下一行，这样不断重复，直到文件末尾。文件内容并没有改变，除非你使用重定向存储输出

sed [选项参数]  ‘command’  filename
选项参数
-e	直接在指令列模式上进行sed的动作编辑。
命令功能描述
a	新增，a的后面可以接字串，在下一行出现
d	删除
s	查找并替换 


awk
一个强大的文本分析工具，把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行分析处理

awk [选项参数] ‘pattern1{action1}  pattern2{action2}...’ filename
pattern：表示AWK在数据中查找的内容，就是匹配模式
action：在找到匹配内容时所执行的一系列命令

选项参数说明
-F	指定输入文件折分隔符
-v	赋值一个用户定义变量
注意：
只有匹配了pattern的行才会执行action
BEGIN 在所有数据读取行之前执行；END 在所有数据执行之后执行


awk的内置变量
FILENAME	文件名
NR		已读的记录数
NF		浏览记录的域的个数（切割后，列的个数）

sort
sort(选项)(参数)

-n	依照数值的大小排序
-r	以相反的顺序来排序
-t	设置排序时所用的分隔字符
-k	指定需要排序的列
















