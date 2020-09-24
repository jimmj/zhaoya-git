# Shell脚本

## 变量定义

```shell
your_name="runoob.com"
```

- 使用变量：`$your_name`【变量名前加$符号，也可将变量使用花括号包裹】`${your_name}`

- 只读变量：`readonly your_name`【变量名前加readonly 即可】

## 字符串

- 字符串虽然使用双引号和单引号包裹都可以，但是还是用双引号包裹，双引号中可以包含变量

```shell
str="Hello,$your_name"
echo $str
```

- **获取字符串长度**

```shell
string="abcd"
echo ${#string} #输出结果为：4
```

- **截取字符串**

```shell
string="abcd"
# 索引从0开始
echo ${#string:1:3} #输出结果为：bcd
```

> 1. **#**、**##** 表示从左边开始删除。一个 **#** 表示从左边删除到第一个指定的字符；两个 **#** 表示从左边删除到最后一个指定的字符。
>
> 2. **%**、**%%** 表示从右边开始删除。一个 **%** 表示从右边删除到第一个指定的字符；两个 **%** 表示从左边删除到最后一个指定的字符。
>
> ```shell
> 假设有变量 var=http://www.aaa.com/123.htm
> 1. # 号截取，删除左边字符，保留右边字符。
> echo ${var#*//}
> 其中 var 是变量名，# 号是运算符，*// 表示从左边开始删除第一个 // 号及左边的所有字符
> 即删除 http://
> 结果是 ：www.aaa.com/123.htm
> 
> 2. ## 号截取，删除左边字符，保留右边字符。
> echo ${var##*/}
> ##*/ 表示从左边开始删除最后（最右边）一个 / 号及左边的所有字符
> 即删除 http://www.aaa.com/
> 结果是 123.htm
> 
> 3. %号截取，删除右边字符，保留左边字符
> echo ${var%/*}
> %/* 表示从右边开始，删除第一个 / 号及右边的字符
> 结果是：http://www.aaa.com
> 
> 4. %% 号截取，删除右边字符，保留左边字符
> echo ${var%%/*}
> %%/* 表示从右边开始，删除最后（最左边）一个 / 号及右边的字符
> 结果是：http:
> 
> 5. 从左边第几个字符开始，及字符的个数
> echo ${var:0:5}
> 其中的 0 表示左边第一个字符开始，5 表示字符的总个数。
> 结果是：http:
> 
> 6. 从左边第几个字符开始，一直到结束。
> echo ${var:7}
> 其中的 7 表示左边第8个字符开始，一直到结束。
> 结果是 ：www.aaa.com/123.htm
> 
> 7. 从右边第几个字符开始，及字符的个数
> echo ${var:0-7:3}
> 其中的 0-7 表示右边算起第七个字符开始，3 表示字符的个数。
> 结果是：123
> 
> 8. 从右边第几个字符开始，一直到结束。
> echo ${var:0-7}
> 表示从右边第七个字符开始，一直到结束。
> 结果是：123.htm
> ```

- **查找子字符串**

```shell
# 查找字符 i 或 o 的位置(哪个字母先出现就计算哪个)
string="runoob is a great site"
echo `expr index "$string" io`  # 输出 4
# 使用的是反引号，不是单引号
```

## shell 数组

> bash支持一维数组，且不限定数组大小

- 定义数组

**在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开**

`array_name=(value0 value1 value2 value3)`

或

```shell
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
```

- 获取数组元素

```shell
value=${array_name[1]}
# 使用@可获取全部元素
value=${array_name[@]}
```

- 获取数组长度

```shell
# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
```

## Shell参数传递

- **向脚本传递参数，脚本内获取参数的格式为：`$n`。`n` 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……**

| 参数处理 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| $#       | 传递到脚本的参数个数                                         |
| $*       | 以一个单字符串显示所有向脚本传递的参数。<br>如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。 |
| $$       | 脚本运行的当前进程ID号                                       |
| $!       | 后台运行的最后一个进程的ID号                                 |
| $@       | 与$*相同，但是使用时加引号，并在引号中返回每个参数。<br>如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数 |
| $-       | 显示Shell使用的当前选项，与[set命令](https://www.runoob.com/linux/linux-comm-set.html)功能相同 |
| $?       | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误  |

> **如果包含空格，应该使用单引号或者双引号将该参数括起来，以便于脚本将这个参数作为整体来接收**

- **<u>Shell脚本中中括号的用法</u>[链接](https://www.runoob.com/w3cnote/shell-summary-brackets.html)**

## Shell运算符

- 算术运算符

| 运算符 | 说明 |      举例       |
| :----: | :--: | :-------------: |
|   +    | 加法 | `expr $a + $b`  |
|   -    | 减法 | `expr $a - $b`  |
|   *    | 乘法 | `expr $a \* $b` |
|   /    | 除法 | `expr $a / $b`  |
|   %    | 取余 | `expr $a % $b`  |

- 字符串运算符

| 运算符 | 说明 | 举例 |
| :------: | :----: | :----: |
| = | 检测两个字符串是否相等，相等返回true | `[[ $a = $b ]]` |
| != | 检测两个字符串是否相等，不相等返回true | `[[ $a = $b ]]` |
| -z | 检测字符串长度是否为0，为0返回true | `[[ -z $a ]]` |
| -n | 检测字符串长度是否不为0，不为0返回true | `[[ -n $a ]]` |
| $ | 检测字符串是否为空，为空返回true | `[[ $a ]]` |

## Shell printf命令

```shell
#test.sh
#!/bin/bash

printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg
printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234
printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543
printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876

zhaoya@zhaoya:~/test$ ./test.sh 
姓名     性别   体重kg
郭靖     男      66.12
杨过     男      48.65
郭芙     女      47.99
```

- **%-10s 指一个宽度为10个字符（-表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来**
- **%-4.2f 指格式化为小数，其中.2指保留2位小数**

## Shell 流程控制

### if else

- **语法格式**

```shell
if condition
then
    command1 
    command2
    ...
    commandN 
fi
#或
if condition
then
    command1 
    command2
    ...
    commandN
else
    command
fi
#嵌套
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

### for循环

- **语法格式**

```shell
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

### while循环

- **语法格式**

```shell
while condition
do
    command
done
```

```shell
#!/bin/bash
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done
```

### until循环

> - **until 循环执行一系列命令直至条件为 true 时停止**
>
> - **until 循环与 while 循环在处理方式上刚好相反，一般 while 循环优于 until 循环，但在某些时候—也只是极少数情况下，until 循环更加有用**

- **语法格式**

```shell
until condition
do
    command
done
```

- **condition 一般为条件表达式，如果返回值为 false，则继续执行循环体内的语句，否则跳出循环**

### case

> **Shell case语句为多选择语句。可以用case语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令**

- **语法格式**

```shell
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
# 或
case 值 in
模式1)
    command1
    command2
    command3
    ;;
模式2）
    command1
    command2
    command3
    ;;
*)
    command1
    command2
    command3
    ;;
esac
```

```shell
#!/bin/bash

echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```

### break

```shell
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```

### continue

```shell
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字: "
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的!"
            continue
            echo "游戏结束"
        ;;
    esac
done
```

## Shell 函数

```shell
#!/bin/bash

demoFun(){
    echo "这是我的第一个 shell 函数!"
}
echo "-----函数开始执行-----"
demoFun
echo "-----函数执行完毕-----"

#  带有return语句的函数
funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"
```

## Shell 重定向

| 命令         | 说明                 |
| ------------ | -------------------- |
| 命令 > file  | 输出重定向到file文件 |
| 命令< file   | 输入重定向到file     |
| 命令 >> file | 将输出追加到file文件 |

## Shell 文件包含

- 格式

**test.sh文件**

```shell
#!/bin/bash

url="http://www.runoob.com"
```

**test2.sh文件**

```shell
#!/bin/bash

#使用 . 号来引用test1.sh 文件
. ./test1.sh

# 或者使用以下包含文件代码
# source ./test1.sh

echo "菜鸟教程官网地址：$url"
```

