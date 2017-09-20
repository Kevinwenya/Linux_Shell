# 了解Shell脚本(*.sh)的基本语法
打开文本编辑器(可以使用 vi/vim 命令来创建文件)，新建一个文件test.sh，扩展名为sh（sh代表shell)
输入一些代码，第一行一般是这样:
#!/bin/bash
#! 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。

#Shell 变量
your_name="wenya.com"
注意，变量名和等号之间不能有空格，这可能和你熟悉的所有编程语言都不一样。同时，变量名的命名须遵循如下规则：
        首个字符必须为字母（a-z，A-Z）。
        中间不能有空格，可以使用下划线（_）。
        不能使用标点符号。
        不能使用bash里的关键字（可用help命令查看保留关键字）。
# 使用变量
使用一个定义过的变量，只要在变量名前面加美元符号即可，如：
echo $your_name
只读变量,使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。

# Shell 字符串
str='this is a string'
单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
单引号字串中不能出现单引号（对单引号使用转义符后也不行）。
str="Hello, I know you are \"$your_name\"! \n"
双引号里可以有变量
双引号里可以出现转义字符

# 拼接字符串
your_name="wenya"
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting $greeting_1

#获取字符串长度
string="wenya"
echo ${#string} #输出 5

# 提取子字符串
以下实例从字符串第 2 个字符开始截取 4 个字符：
string="my name is wenya"
echo ${string:1:4} # 输出 y na

#Shell 注释
以"#"开头的行就是注释，会被解释器忽略。
多行注释：
法一：
:<<!
语句1
语句2
语句3
语句4
!

#shell 传递参数
脚本内获取参数的格式为：$n。n 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……

#Shell 数组
Shell 数组用括号来表示，元素用"空格"符号分割开，语法格式如下：
my_array=(A B "C" D)
echo "第一个元素为: ${my_array[0]}"
echo "第二个元素为: ${my_array[1]}"
echo "第三个元素为: ${my_array[2]}"
echo "第四个元素为: ${my_array[3]}"
echo "数组元素个数为: ${#my_array[*]}

#shell 基本运算符
Shell 和其他编程语言一样，支持多种运算符，包括：
        算数运算符
        关系运算符
        布尔运算符
        字符串运算符
        文件测试运算符
#!/bin/bash
val=`expr 2 + 2`
echo "两数之和为 : $val"
上面的表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。
完整的表达式要被 ` ` 包含，注意这个字符不是常用的单引号，在 Esc 键下边。表示将计算的结果取值赋给变量val。

假定变量 a 为 10，变量 b 为 20：
算术运算符：
        加法：`expr $a + $b` 结果为 30。
        减法：`expr $a - $b` 结果为 -10。
        乘法：`expr $a \* $b` 结果为  200。
        除法：`expr $b / $a` 结果为 2。
        取余：`expr $b % $a` 结果为 0。
        赋值：a=$b 将把变量 b 的值赋给 a。
        相等：[ $a == $b ] 返回 false。
        不相等：[ $a != $b ] 返回 true。
关系运算符：
        -eq：检测两个数是否相等，相等返回 true。                   [ $a -eq $b ] 返回 false。
        -ne：检测两个数是否相等，不相等返回 true。	          [ $a -ne $b ] 返回 true。
        -gt：检测左边的数是否大于右边的，如果是，则返回 true。	      [ $a -gt $b ] 返回 false。
        -lt：检测左边的数是否小于右边的，如果是，则返回 true。	      [ $a -lt $b ] 返回 true。
        -ge：检测左边的数是否大于等于右边的，如果是，则返回 true。    [ $a -ge $b ] 返回 false。
        -le：测左边的数是否小于等于右边的，如果是，则返回 true。      [ $a -le $b ] 返回 true。
布尔运算符：
        !：非运算，表达式为 true 则返回 false，否则返回 true。	  [ ! false ] 返回 true。
        -o：或运算，有一个表达式为 true 则返回 true。	            [ $a -lt 20 -o $b -gt 100 ] 返回 true。
        -a：与运算，两个表达式都为 true 才返回 true。	            [ $a -lt 20 -a $b -gt 100 ] 返回 false。
逻辑运算符：
        &&：逻辑的 AND	[[ $a -lt 100 && $b -gt 100 ]] 返回 false
        ||：逻辑的 OR	[[ $a -lt 100 || $b -gt 100 ]] 返回 true
文件测试运算符：
        -d file：检测文件是否是目录，如果是，则返回 true。
        -s file：检测文件是否为空（文件大小是否大于0）

#Shell read命令、echo命令、printf 命令、test 命令
        read 命令从标准输入中读取一行,并把输入行的每个字段的值指定给 shell 变量
        echo命令用于字符串的输出
        printf命令使用引用文本或空格分隔的参数，外面可以在printf中使用格式化字符串
        test命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。
        read name 
        echo "$name It is a test"
        printf "%-10s %-8s %-4s\n" 姓名 性别 体重
        if test -e ./bash
        then
                echo '文件已存在!'
        else
                echo '文件不存在!'
        fi
# Shell 流程控制
if 语句语法格式：
        if condition
        then
            command1 
            command2
            ...
            commandN 
        fi
        或者
        if condition
        then
            command1 
            command2
            ...
            commandN
        else
            command
        fi
        再或者
        if condition1
        then
            command1
        elif condition2 
        then 
            command2
        else
            commandN
        fi
for循环一般格式为：
        for var in item1 item2 ... itemN
        do
            command1
            command2
            ...
            commandN
        done
while 语句格式为：
        while condition
        do
            command
        done
case语法格式：        
Shell case语句为多选择语句。可以用case语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。case语句格式如下：
        case 值 in
        模式1)
            command1
            command2
            ...
            commandN
            ;;
        模式2）
            command1
            command2
            ...
            commandN
            ;;
        esac
case工作方式如上所示。取值后面必须为单词in，每一模式必须以右括号结束。取值可以为变量或常数。匹配发现取值符合某一模式后，其间所有命令开始执行直至 ;;。

break命令与continue命令：
break命令允许跳出所有循环（终止执行后面的所有循环），continue命令与break命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。

# Shell 函数
linux shell 可以用户定义函数，然后在shell脚本中可以随便调用。
shell中函数的定义格式如下：
        funWithParam(){
            echo "第一个参数为 $1 !"
            echo "第二个参数为 $2 !"
        }
        funWithParam 1 2
        
#Shell 输入/输出重定向
n > file： 将文件描述符为 n 的文件重定向到 file。
n >> file：将文件描述符为 n 的文件以追加的方式重定向到 file。
一般情况下，每个 Unix/Linux 命令运行时都会打开三个文件：
标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据。
标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据。
标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息。
如下面这个命令：
command > file 2>&1
0 是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）。
2>1 代表将stderr重定向到当前路径下文件名为1的regular file中，而2>&1代表将stderr重定向到文件描述符为1的文件(即/dev/stdout)中，这个文件就是stdout在file system中的映射
而&>file是一种特殊的用法，也可以写成>&file，二者的意思完全相同。

