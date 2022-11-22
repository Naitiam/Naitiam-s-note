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

