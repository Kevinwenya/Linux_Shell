## sed常用操作
若想在文件开始或者结尾插入一列字符串，采用sed更容易实现。
> > 	sed  's/^/hello world &/g' data
> > 	sed 's/$/& hello world/g' data
> > 	sed -i 's/.$//' basic_seg.data  #去除最后一个字符
> > 	sed '/./{s/^/HEAD&/;s/$/&TAIL/}' data

这里的命令执行之后，结果会打印在终端屏幕上，如果想要将结果导入其他文件，可以在命令后面加上">文件名"，如果想直接在文件中修改，可在前面加上i选项。
##### 将文件第1到n行提取出来 如3-25
		sed -n '3,25p' file
......



