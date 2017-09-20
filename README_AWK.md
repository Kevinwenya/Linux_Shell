## AWK常用操作
### awk基本语法
	awk [-F] "field-operator" 'comand' inputfiles
-F和field-operator一起使用，field-operator是域分隔符，如果不使用-F选项，则默认的域分隔符为空格。后面command命令一般需要用一堆“{}”括起来，然后进行必要的操作，比较全面一点的command命令：
> 	'{if($1~/^A/) print $1}'
	
翻译一下这个命令就是，如果第一列($1)里面有匹配(~)正则表达式(/^A/)的话，那么就输出(print)到标准输出。需要注意的是，条件必须要用一堆"()"括起来，正则表达式需要用“//”括起来。当然，完全可以不要条件匹配，可以直接输出指定列，如'{print $1}'
### 取文本固定几列
	awk -F\t '{print $1 $3}' file    ##（-F 后根据情况改分隔字符）
	awk '{print $1 $2}' filename     ##（打印完第一列，然后打印第二列 ）
	sed -n "2, 1p" filename | awk 'print $1'. ## 打印文本第二行第一列
### 将提取出的两列，写入临时文件
	paste file_n1.txt file_n2.txt > file_n1_n2.txt
### 找出两个文件之间的相同部分可以使用
	awk 'NR==FNR{a[$0]}NR>FNR{if($1 in a) print $0}' file1 file2
### file1 file2 找出文件2中不同的值
	awk 'NR==FNR{a[$0]}NR>FNR{ if(!($1 in a)) print $0}' file1 file2 
NR, 表示awk开始执行程序后所读取的数据行数。FNR与NR类似，不同的是awk每打开一个新文件，FNR便从0开始重新累计。
### ......

