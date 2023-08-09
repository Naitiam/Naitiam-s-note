> I don't know 这玩意儿有啥用，我觉得不如python

.sh文件

$变量

#! /bin/bash

bash greeting.sh 读取并执行脚本(可无执行权限)

source greeting.sh 读取并执行脚本(可无执行权限)

chmod +x greeting.sh  没有权限添加权限

./xxx.sh 运行程序

```shell
expr `expr 2 + 3` \* 4
# 运算符左右要有空格
```

```
#!/bin/bash
#a Simple shell Script Example
#a Function
function say_hello(){
echo "Enter Your Name,Please.:"
read name
echo "Hello $name"
}
echo "Programme Starts Here......"
say_hello
echo "Programme Ends."

#!/bin/sh
NAME[0]=”aaa"
NAME[1]="bbb"
echo "first :${NAME[0]}"
echo "${NAME[*]}"
echo "${NAME[@]}"
# aaa
# aaa bbb
# aaa bbb

a=(1 2 3 4 5)
echo ${#a[*]}  # 输出数组大小 5
echo ${#a[@]}  # 同上 5
b=(two three) 
echo ${#b[0]}  # 3
echo ${#b[1]}  # 5

read name sex age
echo $name
echo $sex
echo $age

echo ${title:="aaaa"}!
echo ${title:+"aaaa"}!
echo ${title:-"aaaa"}!
var="thing"
echo ${var:2:3}    #ing
字符串比较
root_home="/root"
tom_home="/home/root"
[ $root_home=$tom_home ] #注意括号空格
echo $? # 0
数值比较
var1=200
var2=300
[ $var1 -eq $var2 ]
echo $?   # 1
var2=250
[ $var1 -eq $var2 ]
echo $?   # 0
```





函数的参数：

- $0：脚本文件名
- $1、…、$n：第n个参数
- $#：参数个数
- $*：作为一个整体的所有参数
- $@：作为集合的所有参数

**使用if语句判断并显示输入文件的属性**

```shell
#!/bin/bash
#an example script of if
clear
echo "Input a file or directory name,please"
read path_name
if [ -d $path_name ]
then
        echo "$path_name is a directory"
elif [ -f $path_name ]
then
        echo "$path_name is a regular file"
        if [ -r $path_name ]
        then
                echo "$path_name is a readable file"
        fi
        if [ -w $path_name ]
        then
                echo "$path_name is a writeable file"
        fi
        if [ -x $path_name ]
        then
                echo "$path_name is a executable file"
        fi
```

**以命令的返回值作为判断条件**

```shell
#!/bin/bash
#another example script of if
echo "Input a directory,please!"
read dir_name
if cd $dir_name > /dev/null 2>&1 ;then
        echo "enter directory:$dir_name succeed"
else
        echo "enter directory:$dir_name failded"
fi
```

```shell
#!/bin/bash
#an example script of case
clear
echo "Are you like Linux?"
read like_it
case $like_it in
y|Y|yes|Yes)echo "Linux is a good friend of us."
        ;;
n|N|no|No)echo "Try it, and you will like it."
        ;;
*)echo "you answer is: $like_it"
        ;;
esac
```

until循环语句

```shell
#!/bin/bash
#an example script of  while
clear
loop=0
until [ $loop -eq 10 ]
do
        let loop=$loop+1
        echo "currnet value of loop is:$loop"
done
```

```sh
#!/bin/bash
#an example script of  while
clear
loop=0
while [ $loop -ne 10 ]
do
        let loop=$loop+1
        echo "currnet value of loop is:$loop"
done
```

