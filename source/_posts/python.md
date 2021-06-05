---
title: Python 学习笔记
date: 2020-08-08 00:00:00
categories: "小记"
tags: [Python]
thumbnail: ""
toc: true
excerpt: "为方便个人学习建立的 Python 学习笔记。"
---
### 转义序列
转义字符|功能
:--:|-
\\|反斜杠（\）
\*|单引号（'）
\"|双引号（"）
\a|ASCII响铃符（BEL）
\b|ASCII退格符（BS）
\f|ASCII进纸符（FF）
\n|ASCII换行符（LF）
\N{name}|Unicode 数据库中的字符名，其中 name 是它的名字
\r|ASCII回车符（CR）
\t|ASCII水平制表符（TAB）
\uxxxx|值为16位十六进制值xxxx的字符
\Uxxxxxxxx|值为12位十六进制xxxxxxxx的字符
\v|ASCII垂直制表符（VT）
\ooo|值为八进制xxx的字符
\xhh|值为十六进制hh的字符

### 模块

https://www.runoob.com/python/python-modules.html

#### import 语句

```
import module1[, module2[,... moduleN]]
```

#### from…import 语句

```
from modname import name1[, name2[, ... nameN]]
```
例如，要导入模块 fib 的 fibonacci 函数，使用如下语句：
```
from fib import fibonacci
```
把一个模块的所有内容全都导入到当前的命名空间也是可行的，只需使用如下声明：
```
from modname import *
```

#### 函数调用

**import 模块**：导入一个模块；注：相当于导入的是一个文件夹，是个相对路径。

**from…import**：导入了一个模块中的一个函数；注：相当于导入的是一个文件夹中的文件，是个绝对路径。

所以使用上的的区别是当引用文件时是:
```
import   //模块.函数

from…import  // 直接使用函数名使用就可以了
```
#### sys

`sys.argv` 是一个 list,包含所有的命令行参数.    
`sys.stdout` `sys.stdin` `sys.stderr` 分别表示标准输入输出,错误输出的文件对象.    
`sys.stdin.readline()` 从标准输入读一行 sys.stdout.write("a") 屏幕输出a    
`sys.exit(exit_code)` 退出程序    
`sys.modules` 是一个dictionary，表示系统中所有可用的module    
`sys.platform` 得到运行的操作系统环境    
`sys.path` 是一个list,指明所有查找module，package的路径.  

#### os

`os.environ` 一个dictionary 包含环境变量的映射关系   
`os.environ["HOME"]` 可以得到环境变量HOME的值     
`os.chdir(dir)` 改变当前目录 os.chdir('d:\\outlook')   
注意windows下用到转义     
`os.getcwd()` 得到当前目录     
`os.getegid()` 得到有效组id os.getgid() 得到组id     
`os.getuid()` 得到用户id os.geteuid() 得到有效用户id     
`os.setegid` `os.setegid()` `os.seteuid()` `os.setuid()`     
`os.getgruops()` 得到用户组名称列表     
`os.getlogin()` 得到用户登录名称     
`os.getenv` 得到环境变量     
`os.putenv` 设置环境变量     
`os.umask` 设置umask     
`os.system(cmd)` 利用系统调用，运行cmd命令   

#### 内置模块

不用import就可以直接使用。常用内置函数：

`help(obj)` 在线帮助, obj可是任何类型    
`callable(obj)` 查看一个obj是不是可以像函数一样调用    
`repr(obj)` 得到obj的表示字符串，可以利用这个字符串eval重建该对象的一个拷贝    
`eval_r(str)` 表示合法的python表达式，返回这个表达式    
`dir(obj)` 查看obj的name space中可见的name    
`hasattr(obj,name)` 查看一个obj的name space中是否有name    
`getattr(obj,name)` 得到一个obj的name space中的一个name    
`setattr(obj,name,value)` 为一个obj的name space中的一个name指向vale这个object    
`delattr(obj,name)` 从obj的name space中删除一个name    
`vars(obj)` 返回一个object的name space。用dictionary表示    
`locals()` 返回一个局部name space,用dictionary表示    
`globals()` 返回一个全局name space,用dictionary表示    
`type(obj)` 查看一个obj的类型    
`isinstance(obj,cls)` 查看obj是不是cls的instance    
`issubclass(subcls,supcls)` 查看subcls是不是supcls的子类  

#### 类型转换

`chr(i)` 把一个ASCII数值,变成字符    
`ord(i)` 把一个字符或者unicode字符,变成ASCII数值    
`oct(x)` 把整数x变成八进制表示的字符串    
`hex(x)` 把整数x变成十六进制表示的字符串    
`str(obj)` 得到obj的字符串描述    
`list(seq)` 把一个sequence转换成一个list    
`tuple(seq)` 把一个sequence转换成一个tuple    
`dict()`,`dict(list)` 转换成一个dictionary    
`int(x)` 转换成一个integer    
`long(x)` 转换成一个long interger    
`float(x)` 转换成一个浮点数    
`complex(x)` 转换成复数    
`max(...)` 求最大值    
`min(...)` 求最小值

### 读写文件

#### open()方法

[open()](https://www.runoob.com/python/file-methods.html) 方法用于打开一个文件，并返回文件对象，在对文件进行处理过程都需要使用到这个函数，如果该文件无法被打开，会抛出 OSError。

注意：使用 open() 方法一定要保证关闭文件对象，即调用 close() 方法。

open() 函数常用形式是接收两个参数：文件名(file)和模式(mode)。

```
open(file, mode='r')
```

|模式|描述|
|:-:|-|
|t|文本模式 (默认)。|
|x|写模式，新建一个文件，如果该文件已存在则会报错。|
|b|二进制模式。|
|+|打开一个文件进行更新(可读可写)。|
|U|通用换行模式（不推荐）。|
|r|以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。|
|rb|以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。|
|r+|打开一个文件用于读写。文件指针将会放在文件的开头。|
|rb+|以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。|
|w|打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。|
|wb|以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。|
|w+|打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。|
|wb+|以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。|
|a|打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。|
|ab|以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。|
|a+|打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。|
|ab+|以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。|

#### file 对象
- **close**: 关闭文件。
- **read**: 读取文件中内容。
- **readline**: 只读取文本文件中的一行。
- **turncate**: 清空文件。
- **write('stuff')**: 将“stuff”写入文件。
- **seek(0)**: 将读写位置移动到文件开头。

>document.seek(os.SEEK_SET); #设置指针回到文件最初

### List 方法

以下内容全部来自[菜鸟教程](https://www.runoob.com/)。编集仅供个人查阅使用。

#### len()

[len()](https://www.runoob.com/python/att-list-len.html) 方法返回列表元素个数。
```
len(list)
```
`list` -- 要计算元素个数的列表。

返回列表元素个数。

---

#### max() & min()

[max()](https://www.runoob.com/python/att-list-max.html) /[min()](https://www.runoob.com/python/att-list-min.html) 方法返回列表元素中的最大/小值。
```
max(list)
min(list)
```

`list` -- 要返回最大/小值的列表。

返回列表元素中的最大、小值。

---

#### list()

[list()](https://www.runoob.com/python/att-list-list.html) 方法用于将元组转换为列表。

>元组与列表是非常类似的，区别在于元组的元素值不能修改，元组是放在括号中，列表是放于方括号中。

```
aTuple = (123, 'xyz', 'zara', 'abc');
aList = list(aTuple)
 
print "列表元素 : ", aList
```
```
列表元素 :  [123, 'xyz', 'zara', 'abc']
```
---

#### pop()

[pop()](https://www.runoob.com/python/att-list-pop.html) 函数用于移除列表中的一个元素（默认最后一个元素），并且返回该元素的值。

```
list.pop([index=-1])
```

```
list1 = ['Google', 'Runoob', 'Taobao']
list_pop=list1.pop(1)
print "删除的项为 :", list_pop
print "列表现在为 : ", list1
```
```
删除的项为 : Runoob
列表现在为 :  ['Google', 'Taobao']
```

---

#### append()
[append()](https://www.runoob.com/python/att-list-append.html) 方法用于在列表末尾添加新的对象。

```
list.append(obj)
```
```
aList = [123, 'xyz', 'zara', 'abc'];
aList.append( 2009 );
print "Updated List : ", aList;
```

```
Updated List :  [123, 'xyz', 'zara', 'abc', 2009]
```

#### join()
[join()](https://www.runoob.com/python/att-string-join.html) 方法用于将序列中的元素以指定的字符连接生成一个新的字符串。

```
str.join(sequence)
```

`sequence` -- 要连接的元素序列。

```
str = "-";
seq = ("a", "b", "c"); # 字符串序列
print str.join( seq );
```
```
a-b-c
```

---

#### shuffle()

[shuffle()](https://www.runoob.com/python3/python3-func-number-shuffle.html) 方法将序列的所有元素随机排序。

```
import random

random.shuffle (lst )
```
`lst` -- 列表。
>注意：shuffle() 是不能直接访问的，需要导入 random 模块，然后通过 random 静态对象调用该方法。
```
import random
 
list = [20, 16, 10, 5];
random.shuffle(list)
print ("随机排序列表 : ",  list)
 
random.shuffle(list)
print ("随机排序列表 : ",  list)
```

```
随机排序列表 :  [20, 5, 16, 10]
随机排序列表 :  [5, 20, 10, 16]
```

### Dictionary 方法

### update()

[update()](https://www.runoob.com/python/att-dictionary-update.html) 函数把字典dict2的键/值对更新到dict里。

```
dict.update(dict2)
```

`dict2` -- 添加到指定字典dict里的字典。

```
dict = {'Name': 'Zara', 'Age': 7}
dict2 = {'Sex': 'female' }

dict.update(dict2)
print "Value : %s" %  dict
```

```
Value : {'Age': 7, 'Name': 'Zara', 'Sex': 'female'}
```


### 其他方法

#### split()

[split()](https://www.runoob.com/python/att-string-split.html) 通过指定分隔符对字符串进行切片，如果参数 num 有指定值，则分隔 num+1 个子字符串

```
str.split(str="", num=string.count(str)).
```

`str` -- 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。

`num` -- 分割次数。默认为 -1, 即分隔所有。

```
str = "Line1-abcdef \nLine2-abc \nLine4-abcd";
print str.split( );       # 以空格为分隔符，包含 \n
print str.split(' ', 1 ); # 以空格为分隔符，分隔成两个
```
```
['Line1-abcdef', 'Line2-abc', 'Line4-abcd']
['Line1-abcdef', '\nLine2-abc \nLine4-abcd']
```

---

#### str()

str() 函数将对象转化为适于人阅读的形式。

```
class str(object='')
```

`object` -- 对象。

```
>>>s = 'RUNOOB'
>>> str(s)
'RUNOOB'
>>> dict = {'runoob': 'runoob.com', 'google': 'google.com'};
>>> str(dict)
"{'google': 'google.com', 'runoob': 'runoob.com'}"
>>>
```
---

#### capitalize()

[capitalize()](https://www.runoob.com/python3/python3-string-capitalize.html)将字符串的第一个字母变成大写,其他字母变小写。

```
str.capitalize()
```

该方法返回一个首字母大写的字符串。

```
str = "this is string example from runoob....wow!!!"

print ("str.capitalize() : ", str.capitalize())
```
```
str.capitalize() :  This is string example from runoob....wow!!!
```
---

#### lower()

[lower()](https://www.runoob.com/python3/python3-string-lower.html) 方法转换字符串中所有大写字符为小写。

```
str.lower()
```

返回将字符串中所有大写字符转换为小写后生成的字符串。

```
str = "Runoob EXAMPLE....WOW!!!"

print( str.lower() )
```

```
runoob example....wow!!!
```
---

#### eval()

[eval()](https://www.runoob.com/python/python-func-eval.html) 函数用来执行一个字符串表达式，并返回表达式的值。

```
eval(expression[, globals[, locals]])
```

`expression` -- 表达式。

`globals` -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。

`locals` -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。

```
>>>x = 7
>>> eval( '3 * x' )
21
>>> eval('pow(2,2)')
4
>>> eval('2 + 2')
4
>>> n=81
>>> eval("n + 4")
85
```

---

#### count()

[count()](https://www.runoob.com/python/att-string-count.html) 方法用于统计字符串里某个字符出现的次数。可选参数为在字符串搜索的开始与结束位置。

```
str.count(sub, start= 0,end=len(string))
```

`sub` -- 搜索的子字符串

`start` -- 字符串开始搜索的位置。默认为第一个字符，第一个字符索引值为0。

`end` -- 字符串中结束搜索的位置。字符中第一个字符的索引为 0。默认为字符串的最后一个位置。

该方法返回子字符串在字符串中出现的次数。

```
str = "this is string example....wow!!!";
 
sub = "i";
print "str.count(sub, 4, 40) : ", str.count(sub, 4, 40)
sub = "wow";
print "str.count(sub) : ", str.count(sub)
```
```
str.count(sub, 4, 40) :  2
str.count(sub) :  1
```

#### replace()

[replace()](https://www.runoob.com/python/att-string-replace.html) 方法把字符串中的 old（旧字符串） 替换成 new(新字符串)，如果指定第三个参数max，则替换不超过 max 次。

```
str.replace(old, new[, max])
```

`old` -- 将被替换的子字符串。
`new` -- 新字符串，用于替换old子字符串。
`max` -- 可选字符串, 替换不超过 max 次

返回字符串中的 old（旧字符串） 替换成 new(新字符串)后生成的新字符串，如果指定第三个参数max，则替换不超过 max 次。

```
str = "this is string example....wow!!! this is really string";
print str.replace("is", "was");
print str.replace("is", "was", 3);
```
```
thwas was string example....wow!!! thwas was really string
thwas was string example....wow!!! thwas is really string
```
### 基本断言方法
基本的断言方法提供了测试结果是True还是False。所有的断言方法都有一个msg参数，如果指定msg参数的值，则将该信息作为失败的错误信息返回。

|断言方法|断言描述|
|:-:|-|
|assertEqual(arg1, arg2, msg=None)|验证arg1=arg2，不等则fail|
|assertNotEqual(arg1, arg2, msg=None)|验证arg1 != arg2, 相等则fail|
|assertTrue(expr, msg=None)|验证expr是true，如果为false，则fail|
|assertFalse(expr,msg=None)|验证expr是false，如果为true，则fail|
|assertIs(arg1, arg2, msg=None)|验证arg1、arg2是同一个对象，不是则fail|
|assertIsNot(arg1, arg2, msg=None)|验证arg1、arg2不是同一个对象，是则fail|
|assertIsNone(expr, msg=None)|验证expr是None，不是则fail|
|assertIsNotNone(expr, msg=None)|验证expr不是None，是则fail|
|assertIn(arg1, arg2, msg=None)|验证arg1是arg2的子串，不是则fail|
|assertNotIn(arg1, arg2, msg=None)|验证arg1不是arg2的子串，是则fail|
|assertIsInstance(obj, cls, msg=None)|验证obj是cls的实例，不是则fail|
|assertNotIsInstance(obj, cls, msg=None)|验证obj不是cls的实例，是则fail|

### 常见问题

**`from sysy import argv` 是什么意思？**

sys 是一个软件包。这句话的意思是从该软件包中取出 argv 这个特性。

**`*args`里的'*'是什么意思？**

它的功能是告诉 Python 把函数的所有参数都接收过来，然后放到名叫 args 的列表中去。

**`open(filename, 'w')`中的'W'是什么意思？**

它只是一个只有一个字符的特殊字符串，用来表示文件的访问模式。如果你用了'w'，那么你的文件就是“写入”（write）格式。除'w'之外，我们还有'r'表示“读取”（read），'a'表示“追加”（append）。

**如何读取用户输入的数并进行数学计算？**

`x = int(input())`，它会从 `input()` 获取字符串形式的数值，然后用 `int()` 把它转化成整数。

**为什么文件里会有间隔空行？**

readlines()函数返回的内容中包含文件本来就有的`\n`，而 print 在打印时又会添加一个 `\n` ，这样一来就会多出一个空行了。解决方法是在 print 函数中多加一个参数 `end=""` ，这样 print 就不会为每一行多打印 `\n` 出来了。

**Decode bytes, encode strings**

解码字节串，编码字符串。`b''`告诉 Python 这是字节。

```
bytes = b'\xe6\x96\x87\xe8\xa8\x80'
string = "文言"
string = bytes.decode()
bytes = string.encode()
```
**为什么 "text" and "text"返回"text"，1 and 1 返回 1，而不是返回 True 呢？**

Python 和很多编程语言一样，都是给布尔表达式返回两个被操作对象中的一个，而非 True 或 False。这意味着，如果你写的是 False and 1，得到的是都一个操作数（False），而非第二个操作数（1）。但如果你写的是 True and 1，得到的是第二个操作数（1）。

**怎样判断一个数是否处于某个至值域内？**

有两种办法，经典语法是使用 1 < x < 10 或 1 <= x < 10，用 x in range(1, 10)也可以。

**如何创建二维列表？**

就是在列表中包含列表，如{[1,2,3],[4,5,6]}。

**为什么 for 1 in range (1, 3)只循环 2 次而非 3 次？**
`range()`函数会从第一个数到最后一个数，但不包含最后一个数。所以，它到 2 的时候就停止了，而不会数到 3。

**为什么你会写 while TRUE？**
这样可以创建一个无限循环。

**exit(0) 有什么功能？**
exit(0)可以中止某个程序，而其中的数字参数用来表示程序是否遇到错误而中止。exit(1)表示发生了错误，而 exit(0) 则表示程序是正常退出的。

**result = sentence[:]是什么意思？**
这是 Python 中复制列表的方法。你正在使用“列表切片”（List slicing）语法[:]对列表中的所有元素进行切片操作。
```
s = 'abcdefg'
# 返回从起始位置到索引位置 2 处的字符串切片
print(s[:3]) # 输出 'abc'

# 返回从第三个索引位置到结尾的字符串切片
print(s[3:]) # 输出 'defg'

# 字符串逆序输出
print(s[::-1]) # 输出 'gfedcba'

# 输出从开始位置间隔一个字符组成的字符串
print(s[::2]) # 输出 'aceg'
print(range(10)[::2])  # 输出偶数：[0, 2, 4, 6, 8]

# 它们也可以相互结合使用。
# 从索引位置 6 到索引位置 2，逆向间隔一个字符
print(s[6:2:-2]) # 输出'ge'
```