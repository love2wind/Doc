Linux 的命令确实非常多，然而熟悉 Linux 的人从来不会因为 Linux 的命令太多而烦恼。因为我们仅仅只需要掌握常用命令，就完全可以驾驭 Linux。

接下来，让我们一起来看看都有那些常用的 Linux 命令吧！

- [一些不常用命令](tech/linux2.md)

## 一、文件目录操作

## 1. ls 命令

ls 命令不仅可以查看 linux 文件夹包含的文件而且可以查看文件权限(包括目录、文件夹、文件权限)查看目录信息等等。

### 命令格式

ls 选项

### 常用参数

- -l ：列出长数据串，包含文件的属性与权限数据等
- -a ：列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用）
- -d ：仅列出目录本身，而不是列出目录的文件数据
- -h ：将文件容量以较易读的方式（GB，kB等）列出来
- -R ：连同子目录的内容一起列出（递归列出），等于该目录下的所有文件都会显示出来

### 使用实例

1.列出 home 目录下的所有文件和目录的详细资料。

```jboss-cli
ls -a -l /home
ls -al /home
```

2.列出当前目录下所有以"d"开头的文件目录详情内容。

```jboss-cli
ls -l d*
```

## 2.cd命令

最基本的命令语句，其他的命令语句要进行操作，都是建立在使用 cd 命令上的。用于切换当前目录至dirName。

### 命令格式

cd [目录名]

### 操作案例

1.从当前目录进入系统根目录。

```bash
cd /
```

2.跳转到 home/Code 目录。

```awk
cd /home/Code
```

## 3.pwd 命令

查看"当前工作目录"的完整路径。

### 命令格式：

pwd [选项]

### 常用参数：

- -P :显示实际物理路径，而非使用连接（link）路径
- -L :当目录为连接路径时，显示连接路径

### 操作案例

1.显示当前所在路径。

```bash
pwd
```

## 4.mkdir 命令

用来创建指定的名称的目录，要求创建目录的用户在当前目录中具有写权限，并且指定的目录名不能是当前目录中已有的目录。

### 命令格式

mkdir [选项] 目录

### 常用参数

- -m, --mode=模式，设定权限<模式> (类似 chmod)，而不是 rwxrwxrwx 减 umask
- -p, --parents 可以是一个路径名称。此时若路径中的某些目录尚不存在,加上此选项后,系统将自动建立好那些尚不存在的目录,即一次可以建立多个目录;
- -v, --verbose 每次创建新目录都显示信息
- --help 显示此帮助信息并退出
- --version 输出版本信息并退出

### 使用实例

1.创建一个空目录。

```stata
mkdir test
```

2.递归创建多个目录。

```stata
mkdir test/test1
```

3.创建权限为777的目录。

```apache
mkdir -m 777 test2
```

4.创建目录都显示信息。

```arduino
mkdir -v test4
```

## 5.rm 命令

删除一个目录中的一个或多个文件或目录，如果没有使用- r选项，则rm不会删除目录。如果使用 rm 来删除文件，通常仍可以将该文件恢复原状。

### 命令格式

rm [选项] 文件

### 常用参数

- -f, --force 忽略不存在的文件，从不给出提示。
- -i, --interactive 进行交互式删除
- -r, -R, --recursive 指示rm将参数中列出的全部目录和子目录均递归地删除。
- -v, --verbose 详细显示进行的步骤
- --help 显示此帮助信息并退出
- --version 输出版本信息并退出

### 使用实例

1.删除文件 test.txt,系统会提示是否删除。

```stata
rm test.txt
```

2.强制删除 test.txt，系统不再提示。

```powershell
rm -f test.txt
```

3.将 test 子目录及目录中所有档案删除。

```stata
rm -r test
```

## 6.rmdir 命令

该命令从一个目录中删除一个或多个子目录项，删除某目录时也必须具有对父目录的写权限。

### 命令格式

rmdir [选项] 目录

### 常用参数

- p 递归删除目录dirname，当子目录删除后其父目录为空时，也一同被删除。如果整个路径被删除或者由于某种原因保留部分路径，则系统在标准输出上显示相应的信息。
- -v, --verbose 显示指令执行过程

### 使用实例

1.删除空目录 test1，非空目录无法删除。

```arduino
rmdir test1
```

2.当子目录被删除后使它也成为空目录的话，则顺便一并删除

```arduino
rmdir -p test2 # test 目录下仅有 test2
```

## 7. mv 命令

可以用来移动文件或者将文件改名（move (rename) files）。当第二个参数类型是文件时，mv命令完成文件重命名。当第二个参数是已存在的目录名称时，源文件或目录参数可以有多个，mv命令将各参数指定的源文件均移至目标目录中。

### 命令格式

mv [选项] 源文件或目录 目标文件或目录

### 常用参数

- -b ：若需覆盖文件，则覆盖前先行备份
- -f ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖
- -i ：若目标文件 (destination) 已经存在时，就会询问是否覆盖
- -u ：若目标文件已经存在，且 source 比较新，才会更新(update)
- -t ： --target-directory=DIRECTORY move all SOURCE arguments into DIRECTORY，即指定mv的目标目录，该选项适用于移动多个源文件到一个目录的情况，此时目标目录在前，源文件在后

### 使用实例

1.将 test1.txt 重命名为 test2.txt。

```cos
mv test1.txt test2.txt
```

2.移动文件 test1.txt 到目录 test2

```cos
mv test1.txt test2
```

3.将文件 test1.txt、test2.txt、test3.txt 移动到目录 test3。

```stylus
mv test1.txt test2.txt test3.txt test3
```

## 8.cp 命令

将源文件复制至目标文件，或将多个源文件复制至目标目录。

### 命令格式

cp [选项] 源文件 目录 或 cp [选项] -t 目录 源文件

### 常用参数

- -t --target-directory 指定目标目录
- -i --interactive 覆盖前询问（使前面的 -n 选项失效）
- -n --no-clobber 不要覆盖已存在的文件（使前面的 -i 选项失效）
- -f --force 强行复制文件或目录，不论目的文件或目录是否已经存在
- -u --update 使用这项参数之后，只会在源文件的修改时间较目的文件更新时，或是对应的目的文件并不存在，才复制文件

### 使用实例

1.复制文件 test1.txt 到 test1 目录

```avrasm
cp test1.txt test1 # 若文件存在，会提示是否覆盖。若不存在直接完成复制
```

1. 复制 test1 整个目录到 test2

```avrasm
cp -a test1 test2
```

## 9. touch 命令

touch命令参数可更改文档或目录的日期时间，包括存取时间和更改时间。

### 命令格式

touch [选项] 文件

### 常用参数

- -a 或--time=atime或--time=access或--time=use 　只更改存取时间
- -c 或--no-create 　不建立任何文档
- -d 　使用指定的日期时间，而非现在的时间
- -f 　此参数将忽略不予处理，仅负责解决BSD版本touch指令的兼容性问题
- -m 或--time=mtime或--time=modify 　只更改变动时间
- -r 　把指定文档或目录的日期时间，统统设成和参考文档或目录的日期时间相同 -t 　使用指定的日期时间，而非现在的时间

### 使用实例

1.创建不存在的文件test.txt

```cmake
touch test.txt
```

2.更新 test.txt 的实践和 test1.txt 时间戳相同

```cmake
touch -r test.txt test1.txt
```

## 10.cat 命令

用来显示文件内容，或者将几个文件连接起来显示，或者从标准输入读取内容并显示，它常与重定向符号配合使用。

### 命令格式

cat [选项] [文件]

### 常用参数

- -A, --show-all 等价于 -vET
- -b, --number-nonblank 对非空输出行编号
- -e 等价于 -vE
- -E, --show-ends 在每行结束处显示 $
- -n, --number 对输出的所有行编号,由1开始对所有输出的行数编号
- -s, --squeeze-blank 有连续两行以上的空白行，就代换为一行的空白行
- -t 与 -vT 等价
- -T, --show-tabs 将跳格字符显示为 ^I
- -u (被忽略)
- -v, --show-nonprinting 使用 ^ 和 M- 引用，除了 LFD 和 TAB 之外

### 使用实例

1.把 test.log 的文件内容加上行号后输入 test1.log 这个文件里。

```stata
cat -n test.log  test1.log
```

1. 将 test.log 的文件内容反向显示。

```stata
tac  test.log
```

## 11. nl 命令

输出的文件内容自动的加上行号！其默认的结果与 cat -n 有点不太一样， nl 可以将行号做比较多的显示设计，包括位数与是否自动补齐 0 等等的功能。

### 命令格式

nl [选项] [文件]

### 常用参数

- -b ：指定行号指定的方式，主要有两种：
- -b a ：表示不论是否为空行，也同样列出行号(类似 cat -n)
- -b t ：如果有空行，空的那一行不要列出行号(默认值)
- -n ：列出行号表示的方法，主要有三种：
- -n ln ：行号在萤幕的最左方显示
- -n rn ：行号在自己栏位的最右方显示，且不加 0
- -n rz ：行号在自己栏位的最右方显示，且加 0
- -w ：行号栏位的占用的位数

### 使用实例

1. 用 nl 列出 test.log 的内容。

```stata
nl test.log
```

1. 用 nl 列出 test.log 的内容，空本行也加上行号。

```stata
nl -b a test.log
```

## 12.more 命令

more 命令和 cat 的功能一样都是查看文件里的内容，但有所不同的是more可以按页来查看文件的内容，还支持直接跳转行等功能。

### 命令格式

more [-dlfpcsu ] [-num ] [+/ pattern] [+ linenum] [file ... ]

### 常用参数

- +n 从笫n行开始显示
- -n 定义屏幕大小为n行
- +/pattern 在每个档案显示前搜寻该字串（pattern），然后从该字串前两行之后开始显示
- -c 从顶部清屏，然后显示
- -d 提示“Press space to continue，’q’ to quit（按空格键继续，按q键退出）”，禁用响铃功能
- -l 忽略Ctrl+l（换页）字符
- -p 通过清除窗口而不是滚屏来对文件进行换页，与-c选项相似
- -s 把连续的多个空行显示为一行
- -u 把文件内容中的下画线去掉

### 操作指令

- Enter：向下n行，需要定义。默认为1行
- Ctrl+F：向下滚动一屏
- 空格键：向下滚动一屏
- Ctrl+B：返回上一屏
- = ：输出当前行的行号
- ：f ：输出文件名和当前行的行号
- V ：调用vi编辑器
- !命令 ：调用Shell，并执行命令
- q ：退出more

### 使用实例

1.显示文件 test.log 第3行起内容。

```stata
more +3 test.log
```

2.从文件 test.log 查找第一个出现“day3”字符串的行，并从该处前2行开始显示输出。

```stata
more +/day3 test.log
```

1. 设置每屏显示行数

```stata
more -5 test.log
```

## 13. less 命令

less 与 more 类似，但使用 less 可以随意浏览文件，而 more 仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。

### 命令格式

less [参数] 文件

### 常用参数

- -b <缓冲区大小> 设置缓冲区的大小
- -e 当文件显示结束后，自动离开
- -f 强迫打开特殊文件，例如外围设备代号、目录和二进制文件
- -g 只标志最后搜索的关键词
- -i 忽略搜索时的大小写
- -m 显示类似more命令的百分比
- -N 显示每行的行号
- -o <文件名> 将less 输出的内容在指定文件中保存起来
- -Q 不使用警告音
- -s 显示连续空行为一行
- -S 行过长时间将超出部分舍弃
- -x <数字> 将“tab”键显示为规定的数字空格

### 操作命令

- /字符串：向下搜索“字符串”的功能
- ?字符串：向上搜索“字符串”的功能
- n：重复前一个搜索（与 / 或 ? 有关）
- N：反向重复前一个搜索（与 / 或 ? 有关）
- b 向后翻一页
- d 向后翻半页
- h 显示帮助界面
- Q 退出less 命令
- u 向前滚动半页
- y 向前滚动一行
- 空格键 滚动一行
- 回车键 滚动一页
- [pagedown]： 向下翻动一页
- [pageup]： 向上翻动一页

### 使用实例

1.查看文件 test.log。

```cmake
less test.log
```

## 14. head 命令

head 用来显示档案的开头至标准输出中，默认 head 命令打印其相应文件的开头 10 行。

### 命令格式

head [参数] [文件]

### 常用参数

- -q 隐藏文件名
- -v 显示文件名
- -c<字节> 显示字节数
- -n<行数> 显示的行数

### 使用实例

1.显示文件 test.log 的前 5 行

```stan
head -n 5 test.log
```

2.显示文件 test.log 前 20 个字节

```stan
head -c 20 test.log
```

## 15.tail 命令

显示指定文件末尾内容，不指定文件时，作为输入信息进行处理。常用查看日志文件。

### 命令格式

tail [必要参数] [选择参数] [文件]

### 常用参数

- -f 循环读取
- -q 不显示处理信息
- -v 显示详细的处理信息
- -c<数目> 显示的字节数
- -n<行数> 显示行数
- --pid=PID 与-f合用,表示在进程ID,PID死掉之后结束.
- -q, --quiet, --silent 从不输出给出文件名的首部
- -s, --sleep-interval=S 与-f合用,表示在每次反复的间隔休眠S秒

### 使用实例

1.显示文件 test.log 最后 5 行内容。

```stan
tail -n 5 test.log
```

2.循环查看文件内容

```stan
tail -f test.log
```

## 二、文件查找

## 16.which 命令

which指令会在PATH变量指定的路径中，搜索某个系统命令的位置，并且返回第一个搜索结果。

### 命令格式

which 可执行文件名称

### 常用参数

- -n 　指定文件名长度，指定的长度必须大于或等于所有文件中最长的文件名
- -p 　与-n参数相同，但此处的包括了文件的路径
- -w 　指定输出时栏位的宽度
- -V 　显示版本信息

### 使用实例

1.查找文件、显示命令路径。

```bash
which pwd
```

1. 用 which 去找出 which

```bash
which which
```

## 17.whereis 命令

whereis命令是定位可执行文件、源代码文件、帮助文件在文件系统中的位置。

### 命令格式

whereis [-bmsu] [BMS 目录名 -f ] 文件名

### 常用参数

- -b 定位可执行文件
- -m 定位帮助文件
- -s 定位源代码文件
- -u 搜索默认路径下除可执行文件、源代码文件、帮助文件以外的其它文件
- -B 指定搜索可执行文件的路径
- -M 指定搜索帮助文件的路径
- -S 指定搜索源代码文件的路径

### 使用实例

1.将和 svn 文件相关的文件都查找出来。

```ebnf
whereis svn
```

2.只将二进制文件查找出来。

```armasm
whereis -b svn
```

## 18.locate 命令

可以很快速的搜寻档案系统内是否有指定的档案。

### 命令格式

Locate [选择参数] [样式]

### 常用参数

- -e 将排除在寻找的范围之外。
- -1 如果 是 1．则启动安全模式。在安全模式下，使用者不会看到权限无法看到 的档案。这会始速度减慢，因为 locate 必须至实际的档案系统中取得档案的 权限资料。
- -f 将特定的档案系统排除在外，例如我们没有到理要把 proc 档案系统中的档案 放在资料库中。
- -q 安静模式，不会显示任何错误讯息。
- -n 至多显示 n个输出。
- -r 使用正规运算式 做寻找的条件。
- -o 指定资料库存的名称。
- -d 指定资料库的路径

### 使用实例

1.查找和 pwd 相关的所有文件。

```bash
locate pwd
```

1. 搜索etc 目录下，所有以 m 开头的文件。

```awk
locate /etc/m
```

## 19. find 命令

主要作用是沿着文件层次结构向下遍历，匹配符合条件的文件，并执行相应的操作。

### 命令格式

find [选项] [搜索路径] [表达式]

### 常用参数

- -print find 命令将匹配的文件输出到标准输出
- -exec find 命令对匹配的文件执行该参数所给出的
- shell 命令
- -name 按照文件名查找文件
- -type 查找某一类型的文件

### 使用实例

1.打印当前目录文件目录列表。

```arduino
find . -print
```

2.打印当前目录下所有不以.txt 结尾的文件名。

```routeros
find . ! -name "*.txt"
```

3.打印当前目录下所有权限为 777 的 php 文件。

```sqf
find . -type f -name "*.php" -perm 777
```

4.找到当前目录下所有 php 文件，并显示其详细信息。

```sqf
find . -name "*.php" -exec ls -l {} \;
```

5.查找当前目录下所有 c 代码文件，统计总行数。

```sqf
find . -type f -name "*.c" | xargs wc -l
```

> xargs 命令可以从标准输入接收输入，并把输入转换为一个特定的参数列表。
> 命令格式: command | xargs [选项] [command]
> xargs 命令应该紧跟在管道操作符之后，因为它以标准输入作为主要的源数据流。
> 常用参数
>
> - -n 指定每行最大的参数数量
> - -d 指定分隔符

## 三、文件打包上传和下载

## 20.tar 命令

用来压缩和解压文件。tar本身不具有压缩功能。他是调用压缩功能实现的。

### 命令格式

tar [必要参数] [选择参数] [文件]

### 常用参数

必要参数：

- -A 新增压缩文件到已存在的压缩
- -B 设置区块大小
- -c 建立新的压缩文件
- -d 记录文件的差别
- -r 添加文件到已经压缩的文件
- -u 添加改变了和现有的文件到已经存在的压缩文件
- -x 从压缩的文件中提取文件
- -t 显示压缩文件的内容
- -z 支持gzip解压文件
- -j 支持bzip2解压文件
- -Z 支持compress解压文件
- -v 显示操作过程
- -l 文件系统边界设置
- -k 保留原有文件不覆盖
- -m 保留文件不被覆盖
- -W 确认压缩文件的正确性

可选参数：

- -b 设置区块数目
- -C 切换到指定目录
- -f 指定压缩文件
- --help 显示帮助信息
- --version 显示版本信息

### 使用实例

1.将文件打全部打包成tar包。

```cmake
tar -cvf test.tar test.log    # 仅打包，不压缩！ 

tar -zcvf test.tar.gz test.log  # 打包后，以 gzip 压缩 

tar -zcvf test.tar.bz2 test.log # 打包后，以 bzip2 压缩
```

2.将 tar 包解压缩

```cmake
tar -zxvf test.tar.gz
```

## 21.gzip 命令

使用广泛的压缩程序，文件经它压缩过后，其名称后面会多出".gz"的扩展名。

### 命令格式

gzip [参数] [文件或者目录]

### 常用参数

- -a或--ascii 　使用ASCII文字模式。
- -c或--stdout或--to-stdout 　把压缩后的文件输出到标准输出设备，不去更动原始文件。
- -d或--decompress或----uncompress 　解开压缩文件。
- -f或--force 　强行压缩文件。不理会文件名称或硬连接是否存在以及该文件是否为符号连接。
- -h或--help 　在线帮助。

### 使用实例

1.把 test1 目录下的每个文件压缩成.gz 文件。

```crystal
test6 $ gzip *
```

## 四、文件权限设置

## 22.chmod 命令

用于改变linux系统文件或目录的访问权限。

### 命令格式

chmod [-cfvR] [--help] [--version] mode file

### 常用参数

必要参数：

- -c 当发生改变时，报告处理信息
- -f 错误信息不输出
- -R 处理指定目录以及其子目录下的所有文件
- -v 运行时显示详细处理信息
- 选择参数：
- --reference=<目录或者文件> 设置成具有指定目录或者文件具有相同的权限
- --version 显示版本信息
- <权限范围>+<权限设置> 使权限范围内的目录或者文件具有指定的权限
- <权限范围>-<权限设置> 删除权限范围的目录或者文件的指定权限
- <权限范围>=<权限设置> 设置权限范围内的目录或者文件的权限为指定的值

权限范围：

- u ：目录或者文件的当前的用户
- g ：目录或者文件的当前的群组
- o ：除了目录或者文件的当前用户或群组之外的用户或者群组
- a ：所有的用户及群组

权限代号：

- r：读权限，用数字4表示
- w：写权限，用数字2表示
- x：执行权限，用数字1表示
- -：删除权限，用数字0表示

### 使用实例

1.增加文件所有用户组可执行权限

```livecodeserver
chmod a+x test.log
```

1. 删除所有用户的可执行权限

```livecodeserver
chmod a-x test.log
```

## 23.chgrp 命令

可采用群组名称或群组识别码的方式改变文件或目录的所属群组。

### 命令格式

chgrp [选项] [组] [文件]

### 常用参数

必要参数:

- -c 当发生改变时输出调试信息
- -f 不显示错误信息
- -R 处理指定目录以及其子目录下的所有文件
- -v 运行时显示详细的处理信息
- --dereference 作用于符号链接的指向，而不是符号链接本身
- --no-dereference 作用于符号链接本身

选择参数:

- --reference=<文件或者目录>
- --help 显示帮助信息
- --version 显示版本信息

### 使用实例

1.改变文件的群组属性

```stata
chgrp -v bin test.log
```

2.改变文件test1.log 的群组属性，使得文件test1.log的群组属性和参考文件test.log的群组属性相同

```mel
chgrp --reference=test.log test1.log
```

## 24.chown 命令

通过chown改变文件的拥有者和群组。

### 命令格式

chown [选项] [所有者] [:[组]] 文件

### 常用参数

必要参数:

- -c 显示更改的部分的信息
- -f 忽略错误信息
- -h 修复符号链接
- -R 处理指定目录以及其子目录下的所有文件
- -v 显示详细的处理信息
- -deference 作用于符号链接的指向，而不是链接文件本身

选择参数:

- --reference=<目录或文件> 把指定的目录/文件作为参考，把操作的文件/目录设置成参考文件/目录相同拥有者和群组
- --from=<当前用户：当前群组> 只有当前用户和群组跟指定的用户和群组相同时才进行改变
- --help 显示帮助信息
- --version 显示版本信息

### 使用实例

1.改变拥有者和群组

```stata
chown mail:mail test.log
```

## 五、磁盘存储

## 25. df 命令

显示指定磁盘文件的可用空间。

### 命令格式

df [选项] [文件]

### 常用参数

必要参数：

- -a 全部文件系统列表
- -h 方便阅读方式显示
- -H 等于“-h”，但是计算式，1K=1000，而不是1K=1024
- -i 显示inode信息
- -k 区块为1024字节
- -l 只显示本地文件系统
- -m 区块为1048576字节
- --no-sync 忽略 sync 命令
- -P 输出格式为POSIX
- --sync 在取得磁盘信息前，先执行sync命令
- -T 文件系统类型

选择参数：

- --block-size=<区块大小> 指定区块大小
- -t<文件系统类型> 只显示选定文件系统的磁盘信息
- -x<文件系统类型> 不显示选定文件系统的磁盘信息
- --help 显示帮助信息
- --version 显示版本信息

### 使用实例

1.显示指定磁盘使用情况

```excel
df -t ext3
```

## 26. du 命令

显示每个文件和目录的磁盘使用空间。

### 命令格式

du [选项] [文件]

### 常用参数

- -a或-all 显示目录中个别文件的大小。
- -b或-bytes 显示目录或文件大小时，以byte为单位。
  -- -c或--total 除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和。
- -k或--kilobytes 以KB(1024bytes)为单位输出。
- -m或--megabytes 以MB为单位输出。
- -s或--summarize 仅显示总计，只列出最后加总的值。
- -h或--human-readable 以K，M，G为单位，提高信息的可读性。
- -x或--one-file-xystem 以一开始处理时的文件系统为准，若遇上其它不同的文件系统目录则略过。
- -L<符号链接>或--dereference<符号链接> 显示选项中所指定符号链接的源文件大小。
- -S或--separate-dirs 显示个别目录的大小时，并不含其子目录的大小。
- -X<文件>或--exclude-from=<文件> 在<文件>指定目录或文件。
- --exclude=<目录或文件> 略过指定的目录或文件。
- -D或--dereference-args 显示指定符号链接的源文件大小。
- -H或--si 与-h参数相同，但是K，M，G是以1000为换算单位。
- -l或--count-links 重复计算硬件链接的文件。

### 使用实例

1.显示指定目录或文件所占空间

```cmake
du test # 目录
du test.log # 文件
```

## 六、性能监控和优化命令

## 27.top 命令

显示当前系统正在执行的进程的相关信息，包括进程ID、内存占用率、CPU占用率等。

### 命令格式

top [参数]

### 常见参数

- -b 批处理
- -c 显示完整的治命令
- -I 忽略失效过程
- -s 保密模式
- -S 累积模式
- -i<时间> 设置间隔时间
- -u<用户名> 指定用户名
- -p<进程号> 指定进程
- -n<次数> 循环显示的次数

### 使用实例

1. 显示进程信息。

```coq
top
```

## 28.free 命令

显示系统使用和空闲的内存情况，包括物理内存、交互区内存(swap)和内核缓冲区内存。

### 命令格式

free [参数]

### 常见参数

- -b 　以Byte为单位显示内存使用情况
- -k 　以KB为单位显示内存使用情况
- -m 　以MB为单位显示内存使用情况
- -g 以GB为单位显示内存使用情况
- -o 　不显示缓冲区调节列
- -s<间隔秒数> 　持续观察内存使用状况
- -t 　显示内存总和列。
- -V 　显示版本信息。

### 使用实例

1.显示内存情况。

```gams
free
free -g #以GB为单位
free -m #以MB为单位
```

## 29. vmstat

用来显示虚拟内存的信息。

### 命令格式

- vmstat [-a] [-n] [-S unit] [delay [ count]]
- vmstat [-s] [-n] [-S unit]
- vmstat [-m] [-n] [delay [ count]]
- vmstat [-d] [-n] [delay [ count]]
- vmstat [-p disk partition] [-n] [delay [ count]]
- vmstat [-f]
- vmstat [-V]

### 常见参数

- -a：显示活跃和非活跃内存
- -f：显示从系统启动至今的fork数量
- -m：显示slabinfo
- -n：只在开始时显示一次各字段名称
- -s：显示内存相关统计信息及多种系统活动数量
- delay：刷新时间间隔。如果不指定，只显示一条结果
- count：刷新次数。如果不指定刷新次数，但指定了刷新时间间隔，这时刷新次数为无穷
- -d：显示磁盘相关统计信息
- -p：显示指定磁盘分区统计信息
- -S：使用指定单位显示。参数有 k 、K 、m 、M ，分别代表1000、1024、1000000、1048576字节（byte）。默认单位为K（1024 bytes）

### 使用实例

1.显示活跃和非活跃内存。

```apache
vmstat -a 5 5 # 5秒时间内进行5次采样
```

## 30.lostat 命令

通过iostat方便查看CPU、网卡、tty设备、磁盘、CD-ROM 等等设备的活动情况, 负载信息。

### 命令格式

iostat [参数] [时间] [次数]

### 常见参数

- -C 显示CPU使用情况
- -d 显示磁盘使用情况
- -k 以 KB 为单位显示
- -m 以 M 为单位显示
- -N 显示磁盘阵列(LVM) 信息
- -n 显示NFS 使用情况
- -p[磁盘] 显示磁盘和分区的情况
- -t 显示终端和CPU的信息
- -x 显示详细信息

### 使用实例

1.定时显示所有信息。

```apache
iostat 2 3 #每隔 2秒刷新显示，且显示3次
```

## 31. lsof 命令

用于查看你进程开打的文件，打开文件的进程，进程打开的端口(TCP、UDP)。

### 命令格式

lsof [参数] [文件]

### 常见参数

- -a 列出打开文件存在的进程
- -c<进程名> 列出指定进程所打开的文件
- -g 列出GID号进程详情
- -d<文件号> 列出占用该文件号的进程
- +d<目录> 列出目录下被打开的文件
- +D<目录> 递归列出目录下被打开的文件
- -n<目录> 列出使用NFS的文件
- -i<条件> 列出符合条件的进程。（4、6、协议、:端口、 @ip ）
- -p<进程号> 列出指定进程号所打开的文件
- -u 列出UID号进程详情

### 使用实例

1.查看谁正在使用bash文件，也就是说查找某个文件相关的进程。

```awk
lsof /bin/bash
```

## 七、网络命令

## 32.ipconfig 命令

ifconfig 命令用来查看和配置网络设备。

### 命令格式

ifconfig [网络设备] [参数]

### 常见参数

- up 启动指定网络设备/网卡
- down 关闭指定网络设备/网卡。
- arp 设置指定网卡是否支持ARP协议
- -promisc 设置是否支持网卡的promiscuous模式，如果选择此参数，网卡将接收网络中发给它所有的数据包
- -allmulti 设置是否支持多播模式，如果选择此参数，网卡将接收网络中所有的多播数据包
- -a 显示全部接口信息
- -s 显示摘要信息（类似于 netstat -i）
- add 给指定网卡配置IPv6地址
- del 删除指定网卡的IPv6地址

### 使用实例

1.启动关闭指定网卡

```x86asm
ifconfig eth0 up
ifconfig eth0 down
```

2.用ifconfig修改MAC地址

```elixir
ifconfig eth0 hw ether 00:AA:BB:CC:DD:EE
```

## 33. route 命令

Route命令是用于操作基于内核ip路由表，它的主要作用是创建一个静态路由让指定一个主机或者一个网络通过一个网络接口，如eth0。

### 命令格式

route [-f] [-p] [Command [Destination] [mask Netmask] [Gateway] [metric Metric]] [if Interface]]

### 常见参数

- -c 显示更多信息
- -n 不解析名字
- -v 显示详细的处理信息
- -F 显示发送信息
- -C 显示路由缓存
- -f 清除所有网关入口的路由表。
- -p 与 add 命令一起使用时使路由具有永久性。
- add:添加一条新路由。
- del:删除一条路由。
- -net:目标地址是一个网络。
- -host:目标地址是一个主机。
- netmask:当添加一个网络路由时，需要使用网络掩码。
- gw:路由数据包通过网关。注意，你指定的网关必须能够达到。
- metric：设置路由跳数。
- Command 指定您想运行的命令 (Add/Change/Delete/Print)。
- Destination 指定该路由的网络目标。

### 使用实例

1.显示当前路由

```pf
route 
route -n
```

2.添加网关/设置网关

```nginx
route add -net 224.0.0.0 netmask 240.0.0.0 dev eth0
```

## 34. ping 命令

确定网络和各外部主机的状态；跟踪和隔离硬件和软件问题；测试、评估和管理网络。

### 命令格式

ping [参数] [主机名或IP地址]

### 常见参数

- -d 使用Socket的SO_DEBUG功能
- -f 极限检测。大量且快速地送网络封包给一台机器，看它的回应
- -n 只输出数值
- -q 不显示任何传送封包的信息，只显示最后的结果
- -r 忽略普通的Routing Table，直接将数据包送到远端主机上。通常是查看本机的网络接口是否有问题
- -R 记录路由过程
- -v 详细显示指令的执行过程
- -c 数目：在发送指定数目的包后停止
- -i 秒数：设定间隔几秒送一个网络封包给一台机器，预设值是一秒送一次 -I 网络界面：使用指定的网络界面送出数据包 -l 前置载入：设置在送出要求信息之前，先行发出的数据包 -p 范本样式：设置填满数据包的范本样式 -s 字节数：指定发送的数据字节数，预设值是56，加上8字节的ICMP头，一共是64ICMP数据字节 -t 存活数值：设置存活数值TTL的大小

### 使用实例

1. ping 网关

```nginx
ping -b 192.168.120.1
```

## 35.traceroute 命令

让你追踪网络数据包的路由途径，预设数据包大小是40Bytes，用户可另行设置。

### 命令格式

traceroute [参数] [主机]

### 常见参数

- -d 使用Socket层级的排错功能
- -f 设置第一个检测数据包的存活数值TTL的大小
- -F 设置勿离断位
- -g 设置来源路由网关，最多可设置8个
- -i 使用指定的网络界面送出数据包
- -I 使用ICMP回应取代UDP资料信息
- -m 设置检测数据包的最大存活数值TTL的大小
- -n 直接使用IP地址而非主机名称
- -p 设置UDP传输协议的通信端口
- -r 忽略普通的Routing Table，直接将数据包送到远端主机上
- -s 设置本地主机送出数据包的IP地址
- -t 设置检测数据包的TOS数值
- -v 详细显示指令的执行过程
- -w 设置等待远端主机回报的时间
- -x 开启或关闭数据包的正确性检验

### 使用实例

1.traceroute 用法简单、最常用的用法

```nginx
traceroute www.baidu.com
```

1. 跳数设置

```apache
traceroute -m 10 www.baidu.com
```

## 36.netstat 命令

用于显示与IP、TCP、UDP和ICMP协议相关的统计数据，一般用于检验本机各端口的网络连接情况。

### 命令格式

netstat [-acCeFghilMnNoprstuvVwx] [-A<网络类型>] [--ip]

### 常见参数

- -a或–all 显示所有连线中的Socket
- -A<网络类型>或–<网络类型> 列出该网络类型连线中的相关地址
- -c或–continuous 持续列出网络状态
- -C或–cache 显示路由器配置的快取信息
- -e或–extend 显示网络其他相关信息
- -F或–fib 显示FIB
- -g或–groups 显示多重广播功能群组组员名单
- -h或–help 在线帮助
- -i或–interfaces 显示网络界面信息表单
- -l或–listening 显示监控中的服务器的Socket
- -M或–masquerade 显示伪装的网络连线
- -n或–numeric 直接使用IP地址，而不通过域名服务器
- -N或–netlink或–symbolic 显示网络硬件外围设备的符号连接名称
- -o或–timers 显示计时器
- -p或–programs 显示正在使用Socket的程序识别码和程序名称
- -r或–route 显示Routing Table
- -s或–statistice 显示网络工作信息统计表
- -t或–tcp 显示TCP传输协议的连线状况
- -u或–udp 显示UDP传输协议的连线状况
- -v或–verbose 显示指令执行过程
- -V或–version 显示版本信息
- -w或–raw 显示RAW传输协议的连线状况
- -x或–unix 此参数的效果和指定”-A unix”参数相同
- –ip或–inet 此参数的效果和指定”-A inet”参数相同

### 使用实例

1. 列出所有端口

```css
netstat -a
```

## 37.telnet 命令

执行telnet指令开启终端机阶段作业，并登入远端主机。

### 命令格式

telnet [参数] [主机]

### 常见参数

- -8 允许使用8位字符资料，包括输入与输出
- -a 尝试自动登入远端系统
- -b<主机别名> 使用别名指定远端主机名称
- -c 不读取用户专属目录里的.telnetrc文件
- -d 启动排错模式
- -e<脱离字符> 设置脱离字符
- -E 滤除脱离字符
- -f 此参数的效果和指定"-F"参数相同

### 使用实例

1.远程服务器无法访问

```nginx
telnet 192.168.120.206
```

## 八、其他命令

## 38.ln 命令

为某一个文件在另外一个位置建立一个同步的链接.当我们需要在不同的目录，用到相同的文件时，我们不需要在每一个需要的目录下都放一个必须相同的文件，我们只要在某个固定的目录，放上该文件，然后在 其它的目录下用ln命令链接（link）它就可以，不必重复的占用磁盘空间。

### 命令格式

ln [参数] [源文件或目录] [目标文件或目录]

### 常用参数

必要参数:

- -b 删除，覆盖以前建立的链接
- -d 允许超级用户制作目录的硬链接
- -f 强制执行
- -i 交互模式，文件存在则提示用户是否覆盖
- -n 把符号链接视为一般目录
- -s 软链接(符号链接)
- -v 显示详细的处理过程

选择参数:

- -S “-S<字尾备份字符串> ”或 “--suffix=<字尾备份字符串>”
- -V “-V<备份方式>”或“--version-control=<备份方式>”

### 使用实例

1.为 test.log文件创建软链接linktest。

```stata
ln -s test.log linktest
```

2.为 test.log创建硬链接lntest。

```livecodeserver
ln test.log lntest
```

## 39.diff 命令

比较单个文件或者目录内容。

### 命令格式

diff [参数] [文件1或目录1] [文件2或目录2]

### 常用参数

- -c 上下文模式，显示全部内文，并标出不同之处
- -u 统一模式，以合并的方式来显示文件内容的不同
- -a 只会逐行比较文本文件
- -N 在比较目录时，若文件 A 仅出现在某个目录中，预设会显示：Only in 目录。若使用 -N 参数，则 diff 会将文件 A 与一个空白的文件比较
- -r 递归比较目录下的文件

### 使用实例

1.显示 test1.txt 和 test2.txt 两个文件差异。

```maxima
diff test1.txt test2.txt
```

## 40.grep 命令

一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹 配的行打印出来。

### 命令格式

grep [option] pattern file

### 常用参数

- -c 计算找到‘搜寻字符串’（即 pattern）的次数
- -i 忽略大小写的不同，所以大小写视为相同
- -n 输出行号
- -v 反向选择，打印不匹配的行
- -r 递归搜索
- --color=auto 将找到的关键词部分加上颜色显示

### 使用实例

1.将 /etc/passwd 文件中出现 root 的行取出来，关键词部分加上颜色显示。

```gradle
grep "root" /etc/passwd --color=auto
cat /etc/passwd | grep "root" --color=auto
```

2.将 /etc/passwd 文件中没有出现 root 和 nologin 的行取出来。

```gradle
grep -v "root" /etc/passwd | grep -v "nologin"
```

## 41.wc 命令

用来显示文件所包含的行、字和字节数。

### 命令格式

wc [选项] [文件]

### 常用参数

- -c 统计字节数
- -l 统计行数
- -m 统计字符数，这个标志不能与 -c 标志一起使用
- -w 统计字数，一个字被定义为由空白、跳格或换行字符分隔的字符串
- -L 打印最长行的长度

### 使用实例

1.统计文件的字节数、行数和字符数。

```cmake
wc -c test.txt
wc -l test.txt
wc -m test.txt
```

2.统计文件的字节数、行数和字符数，只打印数字，不打印文件名。

```stata
cat test.txt | wc -c
cat test.txt | wc -l
cat test.txt | wc -m
```

## 42.ps 命令

用来显示当前进程的状态。

### 命令格式

ps[参数]

### 常用参数

- a 显示所有进程
- -a 显示同一终端下的所有程序
- -A 显示所有进程
- c 显示进程的真实名称
- -N 反向选择
- -e 等于“-A”
- e 显示环境变量
- f 显示程序间的关系
- -H 显示树状结构
- r 显示当前终端的进程
- T 显示当前终端的所有程序
- u 指定用户的所有进程
- -au 显示较详细的资讯
- -aux 显示所有包含其他使用者的行程
- -C<命令> 列出指定命令的状况
- --lines<行数> 每页显示的行数
- --width<字符数> 每页显示的字符数

### 使用实例

1.显示所有进程信息。

```css
ps -A
```

1. 显示指定用户信息。

```ebnf
ps -u root
```

1. 显示所有进程信息，连同命令行。

```ebnf
ps -ef
```

## 43.watch 命令

可以将命令的输出结果输出到标准输出设备，多用于周期性执行命令/定时执行命令。

### 命令格式

watch [参数] [命令]

### 常用参数

- -n或--interval watch缺省每2秒运行一下程序，可以用-n或-interval来指定间隔的时间。
- -d或--differences 用-d或--differences 选项watch 会高亮显示变化的区域。 而-d=cumulative选项会把变动过的地方(不管最近的那次有没有变动)都高亮显示出来。
- -t 或-no-title 会关闭watch命令在顶部的时间间隔,命令，当前时间的输出。
- -h, --help 查看帮助文档

### 使用实例

1.每隔一秒高亮显示网络链接数的变化情况

```apache
watch -n 1 -d netstat -ant
```

2.每隔一秒高亮显示http链接数的变化情况

```nginx
watch -n 1 -d 'pstree|grep http'
```

## 44. at 命令

在一个指定的时间执行一个指定任务，只能执行一次。（需开启atd进程）

### 命令格式

at [参数] [时间]

### 常用参数

- -m 当指定的任务被完成之后，将给用户发送邮件，即使没有标准输出
- -I atq的别名
- -d atrm的别名
- -v 显示任务将被执行的时间
- -c 打印任务的内容到标准输出
- -V 显示版本信息
- -q<列队> 使用指定的列队
- -f<文件> 从指定文件读入任务而不是从标准输入读入
- -t<时间参数> 以时间参数的形式提交要运行的任务

### 使用实例

1.3天后的下午5点执行/bin/ls

```xquery
at 5pm+3 days 
at> /bin/ls
at> <EOT>
```

## 45.crontab 命令

在固定的间隔时间执行指定的系统指令或 shell script脚本。时间间隔的单位可以是分钟、小时、日、月、周及以上的任意组合。(需开启crond服务)

### 命令格式

crontab [-u user] file 或

crontab [-u user] [ -e | -l | -r ]

### 常用参数

- -u user：用来设定某个用户的crontab服务，例如，“-u ixdba”表示设定ixdba用户的crontab服务，此参数一般有root用户来运行。
- file：file是命令文件的名字,表示将file做为crontab的任务列表文件并载入crontab。如果在命令行中没有指定这个文件，crontab命令将接受标准输入（键盘）上键入的命令，并将它们载入crontab。
- -e：编辑某个用户的crontab文件内容。如果不指定用户，则表示编辑当前用户的crontab文件。
- -l：显示某个用户的crontab文件内容，如果不指定用户，则表示显示当前用户的crontab文件内容。
- -r：从/var/spool/cron目录中删除某个用户的crontab文件，如果不指定用户，则默认删除当前用户的crontab文件。
- -i：在删除用户的crontab文件时给确认提示。

### 使用实例

1.列出 crontab 文件。

```ebnf
crontab -l
```

2.编辑crontab 文件。

```ebnf
crontab -e
```

### Crontab 任务实例

1.每1分钟执行一次command

```markdown
* * * * * command
```

2.每小时的第3和第15分钟执行

```markdown
3,15 * * * * command
```

3.在上午8点到11点的第3和第15分钟执行

```apache
3,15 8-11 * * * command
```