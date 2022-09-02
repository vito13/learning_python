---
阅读进度
Python编程：从入门到实践（第2版）		继续第12章，后面都是东拼西凑先不用看了
python基础教程（第三版）				继续第12章，后面都是东拼西凑先不用看了
python语言及其应用						继续第4章
---
# 基础知识
> Python 最底层的基本数据类型：布尔型、整型、浮点型以及字符串型。如果把这些数据类型看作组成 Python 的原子，数据结构就像分子一样。我们把之前所学的基本 Python 类型以更为复杂的方式组织起来。这些数据结构以后会经常用到。在编程中，最常见的工作就是将数据进行拆分或合并，将其加工为特定的形式，而数据结构就是用以切分数据的钢锯以及合并数据的粘合枪。

## 数值
- 整型（整数，例如 42、100000000）
- 浮点型（小数，例如 3.14159，或用科学计数法表示的数字，例如 1.0e8，它表示1乘以10的8次方，也可写作100000000.0）
- 无论是哪种运算，只要有操作数是浮点数，Python默认得到的总是浮点数，即便结果原本为整数也是如此。
- 书写很大的数时，可使用下划线将其中的数字分组，如 universe_age = 14_000_000_000
- 可以同时赋值多个变量 x, y, z = 0, 0, 0
## bool
表示真假的类型，仅包含 True 和 False 两种取值
- bool()
- True
- False
```
print(bool('I think, therefore I am'))
print(bool(42))
print(bool(''))
print(True)
print(False)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
True
True
False
True
False
```

## 乘方
print(3 ** 2)
## 常量
Python没有内置的常量类型，通常使用全大写将某个变量视为常量，如MAX_CONNECTIONS = 5000
## 注释
用一个“#”
## min、max、sum、len
```
even_numbers = list(range(2, 11, 2))	# 可以指定步长
print(min(even_numbers))
print(max(even_numbers))
print(sum(even_numbers))
print(len(even_numbers))

```
## input、int、float
- int()可以取值
- int(False)也可以转换bool得到1和0
- float()可以将其他数字类型转换为浮点型
```
#!/usr/bin/python3
height = input("How tall are you, in inches? ")
height = int(height)
if height >= 48:
 print("\nYou're tall enough to ride!")
else:
 print("\nYou'll be able to ride when you're a little older.")

```
## 打印输出
```
print('Age:', 42) 
name = 'Gumby' 
salutation = 'Mr.' 
greeting = 'Hello,' 
print(greeting, salutation, name) 	# 多个变量间默认是空格，也可以设置间隔符，见下面
print(greeting, ',', salutation, name) 
print(greeting + ',', salutation, name)  # 将第一个变量与逗号连接的结果作为第一个参数
print("I", "wish", "to", "register", "a", "complaint", sep="_")  # 设置间隔符号 
print('Hello,', end='\n\n\n') # 设置打印的结束符号
print('world!')


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Age: 42
Hello, Mr. Gumby
Hello, , Mr. Gumby
Hello,, Mr. Gumby
I_wish_to_register_a_complaint
Hello,


world!
```
如果要打印的数据结构太大，一行容纳不下，可使用模块pprint中的函数pprint（而不是普通print语句）。pprint是个卓越的打印函数，能够更妥善地打印输出。

```
#!/usr/bin/python3
import sys, pprint 
pprint.pprint(sys.path) 

[huawei@n148 pytest]$ python3 pyth.py 
['/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest',
 '/usr/local/lib/python3.6/site-packages/setuptools-19.6-py3.6.egg',
 '/usr/lib64/python36.zip',
 '/usr/lib64/python3.6',
 '/usr/lib64/python3.6/lib-dynload',
 '/usr/local/lib64/python3.6/site-packages',
 '/usr/local/lib/python3.6/site-packages',
 '/usr/lib64/python3.6/site-packages',
 '/usr/lib/python3.6/site-packages']
```

## 随机数
- 随机整数 randint
- 随机列表元素 choice
```
#!/usr/bin/python3

from random import randint
print(randint(1, 6))
from random import choice
players = ['charles', 'martina', 'michael', 'florence', 'eli']
first_up = choice(players)
print(first_up)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
3
michael
```
## pass
防止在if里什么都不写无法运行，可暂时用pass占位
```
#!/usr/bin/python3
name = "Enid"
if name == 'Ralph Auldus Melish': 
	print('Welcome!') 
elif name == 'Enid': 
	# 还未完成……
	pass 
elif name == 'Bill Gates': 
	print('Access Denied')

```
在异常处理中如果没找到文件也就什么都不做了
```
def count_words(filename):
	try:
		with open(filename, encoding='utf-8') as f:
			contents = f.read()
	except FileNotFoundError:
		pass
	else:
		words = contents.split()
		num_words = len(words)
		print(f"The file {filename} has about {num_words} words.")


filenames = ['alice.txt', 'siddhartha.txt', 'moby_dick.txt', 'little_women.txt']
for filename in filenames:
	count_words(filename)

[huawei@n148 pytest]$ python3 pyth.py 
The file alice.txt has about 29465 words.
```
## del
不仅会删除到对象的引用，还会删除名称本身
## exec、eval
## 命名空间、作用域
vars函数返回当前作用域的字典，但不要修改它这样不安全...
```
x = 1 
scope = vars() 
print(scope['x'])
scope['x'] += 1 
print(x)
[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
1
2
```
## 全局变量
- 可使用函数globals来访问全局变量，返回一个包含全局变量的字典
```
def combine(parameter): # 与全局变量同名的参数
	print(parameter + globals()['parameter']) 

parameter = 'berry' 	# 全局变量
combine('Shrub') 

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Shrubberry
```
- 在函数内部给变量赋值时，该变量默认为局部变量，除非明确说明它是全局变量。
```
x = 1 
def change_global(): 
	global x 
	x = x + 1 

change_global() 
print(x)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
2
```
## 闭包

# 序列与映射
- 序列是一种数据结构，其中的元素带编号（编号从0开始）。
- 需要将一系列值组合成数据结构并通过编号来访问各个值时，列表很有用
- 列表、字符串和元组都属于序列，其中列表是可变的（你可修改其内容），而元组和字符串是不可变的（一旦创建，内容就是固定的）。
- 要访问序列的一部分，可使用切片操作：提供两个指定切片起始和结束位置的索引。
- 要修改列表，可给其元素赋值，也可使用赋值语句给切片赋值。
- 标准序列操作（索引、切片、乘法、成员资格检查、长度、最小值和最大值）
- 字典是Python中唯一的内置映射类型，其中的值不按顺序排列，而是存储在键下。键可能是数、字符串或元组（即k得是不可变的类型）。


# 字符串
- 字符组成的序列
- 字符串是不可变的，因此所有的元素赋值和切片赋值都是非法的。
- 多行的使用三个单引号，
## 多行的、单行的、还有图标的
```
#!/usr/bin/python3
print('''This is a very long string. It continues here. 
And it's not over yet. "Hello, world!" 
Still here.''')
print(r'C:\Program Files\fnord\foo\bar\baz\frozz\bozz')
print(r'Let\'s go!') 
print('C:\\nowhere') 
print(r'C:\Program Files\foo\bar' '\\') 
print("This is a cat: \N{Cat}")

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
This is a very long string. It continues here. 
And it's not over yet. "Hello, world!" 
Still here.
C:\Program Files\fnord\foo\bar\baz\frozz\bozz
Let\'s go!
C:\nowhere
C:\Program Files\foo\bar\
This is a cat: 🐈
```
## 大写、小写、首字母大小
```
#!/usr/bin/python3
name = "ada lovelace"
print(name.title())
print(name.upper())
print(name.lower())

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Ada Lovelace
ADA LOVELACE
ada lovelace
```
## str类型转换
```
print(str(123.321))
print(str(True))
```
## 字符串长度len
```
letters = 'abcdefghijklmnopqrstuvwxyz'
print(len(letters))
```
## 判断开头、结尾
```
letters = 'abcdefghijklmnopqrstuvwxyz'
print(letters.startswith('abc'))
print(letters.endswith('abc'))
[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
True
False
```
## 判断都是字母数字
poem.isalnum()
## 首字母变大写
setup.capitalize()
## 所有单词的开头字母变大写
setup.title()

## 所有字母都大写
setup.upper()

## 所有字母都小写
setup.lower()

## 所有字母大小写互换
setup.swapcase()
## 左对齐、右对齐、居中
- setup.ljust(30)
- setup.rjust(30)
- setup.center(30)

## 取字符
当做数据进行索引即可
```
letters = 'abcdefghijklmnopqrstuvwxyz'
print(letters[0])
print(letters[1])
print(letters[2])
print(letters[-1])
print(letters[-2])

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
a
b
c
z
y
```
## 格式化
- c风格%方式
- shell风格
- format方法，关于更多format控制符号参见《python基础继承第二版 3.3》
	- 要对字典执行字符串格式设置操作，不能使用format和命名参数，而必须使用format_map。见字典的format部分案例
- f方式，是Python 3.6引入的，用于简化format
```
#!/usr/bin/python3
from math import pi
from string import Template
from math import e
import math 

# c风格
format = "Hello, %s. %s enough for ya?"
values = ('world', 'Hot') 
sss = format % values
print(sss)	# Hello, world. Hot enough for ya?

# shell风格
tmpl = Template("Hello, $who! $what enough for ya?") 
sss = tmpl.substitute(who="Mars", what="Dusty")
print(sss)	# Hello, Mars! Dusty enough for ya?

# format风格，{}里使用需要则从0开始
sss = "{}, {} and {}".format("first", "second", "third") 
print(sss)	# first, second and third
print("{0}, {1} and {2}".format("first", "second", "third"))	# first, second and third
print("{3} {0} {2} {1} {3} {0}".format("be", "not", "or", "to"))	# to be or not to be
print("{name} is approximately {value:2f}".format(value=pi, name="π"))	# π is approximately 3.141593
print("{name} is approximately {value}.".format(value=pi, name="π")) 	# π is approximately 3.141592653589793.
print("{{ceci n'est pas une replacement field}}".format()) # {ceci n'est pas une replacement field}, 包含{}的字符串
print("{foo} {} {bar} {}".format(1, 2, bar=4, foo=3))	# 3 1 4 2
print("{foo} {1} {bar} {0}".format(1, 2, bar=4, foo=3))	# 3 2 4 1

print("Euler's constant is roughly {e}.".format(e=e))	# Euler's constant is roughly 2.718281828459045.
print(f"Euler's constant is roughly {e}.") # python3.6之后使用简写f，效果与上一句等价
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(full_name)	# ada lovelace
message = f"Hello, {full_name.title()}!"
print(message)	# Hello, Ada Lovelace!

fullname = ["Alfred", "Smoketoomuch"] 
print("Mr {name[1]}".format(name=fullname))	# Mr Smoketoomuch，也可以使用列表元素

tmpl = "The {mod.__name__} module defines the value {mod.pi} for π" 
sss = tmpl.format(mod=math)	# 还可以使用包（包名：mod.__name__、包里的变量：mod.pi）
print(sss)	# The math module defines the value 3.141592653589793 for π
```
## 居中
用指定字符填充两边
```
print("The Middle by Jimmy Eat World".center(39, "*")) 

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
*****The Middle by Jimmy Eat World*****
```
## 删两端空白或字符
- lstrip
- strip
	删除两端空格，也可删除通过参数指定的字符们，见下例
- rstrip
	可用于在read文件后去除文件末尾多余的空白或换行，见文件读取案例
```
删除开头或末尾的指定字符，因此中间的星号未被删除。
print('*** SPAM * for * everyone!!! ***'.strip(' *!'))

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
SPAM * for * everyone
```
使用strip删除每行的两边空白
```
with open('pi_digits.txt') as file_object:
    lines = file_object.readlines()
pi_string = ''
for line in lines:
	pi_string += line.strip()
print(pi_string)
print(len(pi_string))

[huawei@n148 pytest]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
3.141592653589793238462643383279
32

[huawei@n148 pytest]$ cat pi_digits.txt 
3.1415926535 
  8979323846 
  2643383279
```
## 比较
依然使用==与!=
```
#!/usr/bin/python3
requested_topping = 'mushrooms'
if requested_topping != 'anchovies':
	print("Hold the anchovies!")
car = 'Audi'
print(car.lower() == 'audi')

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Hold the anchovies!
True
```
## n倍字符串
使用乘法*，效果同perl
```
print('python ' * 5) # python python python python python 
```
## 检测包含字符
```
permissions = 'rw' 
print('w' in permissions)	# True
subject = '$$$ Get rich now!!! $$$' 
print('$$$' in subject)		# True
```
## 查找 find、rfind
rfind是从后向前找，但返回的index还是从前向后的数的
```
# 返回index，否则返回-1。起点和终点值（第二个和第三个参数）指定的搜索范围包含起点，但不包含终点。
subject = "$$$ Get rich now!!! $$$"
print(subject.find('$$$')) 
print(subject.find('$$$', 1)) # 只指定了起点
print(subject.find('!!!'))
print(subject.find('!!!', 0, 16)) # 同时指定了起点和终点

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
0
20
16
-1
```
## join、split
split返回列表
```
#!/usr/bin/python3
seq = ['1', '2', '3', '4', '5'] 
sep = '-'
print(sep.join(seq)) # 1-2-3-4-5， 合并一个字符串列表
dirs = '', 'usr', 'bin', 'env' # 这是个元祖，首元素为空用于join后开头的“/”
print(dirs)
print('/'.join(dirs)) 	#  /usr/bin/env
print('C:' + '\\'.join(dirs))  # C:\usr\bin\env



print('1+2+3+4+5'.split('+'))	# ['1', '2', '3', '4', '5']
```
## 出现的次数 count
```
line = "Row, row, row your boat"
print(line.count('row'))
print(line.lower().count('row'))

[huawei@n148 pytest]$ python3 pyth.py 
2
3
```
## 统计单词数量
使用了异常处理，并且可以统计多本书的词数
```
def count_words(filename):
	try:
		with open(filename, encoding='utf-8') as f:
			contents = f.read()
	except FileNotFoundError:
		print(f"Sorry, the file {filename} does not exist.")
	else:
		words = contents.split()
		num_words = len(words)
		print(f"The file {filename} has about {num_words} words.")


filenames = ['alice.txt', 'siddhartha.txt', 'moby_dick.txt', 'little_women.txt']
for filename in filenames:
	count_words(filename)

[huawei@n148 pytest]$ python3 pyth.py 
The file alice.txt has about 29465 words.
Sorry, the file siddhartha.txt does not exist.
Sorry, the file moby_dick.txt does not exist.
Sorry, the file little_women.txt does not exist.
```
## 替换字符
由于字符串是不可变的，因此无法直接插入字符或改变指定位置的字符。下面方式是非法的
```
name = 'Henny'
name[0] = 'P'
```
可以使用replace或切片达到替换的效果
```
name = 'Henny'
print(name.replace('H', 'P'))
print('P' + name[1:])

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
Penny
Penny
```
## 替换 replace
参数：
- 需要被替换的子串
- 用于替换的新子串
- 以及需要替换多少处，省略此参数将替换所有
```
s1 = 'This is a test';
s2 = s1.replace('is', 'eez');	# 替换了两处
print(s1)
print(s2)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
This is a test
Theez eez a test
```
## 使用【start:end:step】切片
- 【:】 提取从开头到结尾的整个字符串
- 【start:】 从 start 提取到结尾
- 【:end】 从开头提取到 end - 1
- 【start:end】 从 start 提取到 end - 1
- 【start:end:step】 从 start 提取到 end - 1，每 step个字符提取一个
- 偏移量从左至右从 0、1 开始，依次增加
- 从右至左从-1、-2 开始，依次减小
- 如果省略 start，分片会默认使用偏移量0（开头）
- 如果省略 end，分片会默认使用偏移量 -1（结尾）
```

letters = 'abcdefghijklmnopqrstuvwxyz'
print(letters[:])	# abcdefghijklmnopqrstuvwxyz	提取整个字符串
print(letters[20:])	 # uvwxyz 	从偏移量 20 提取到字符串结尾
print(letters[10:])	# klmnopqrstuvwxyz 从偏移量 10 提取到结尾
print(letters[12:15]) # mno  从 12 到 14 的字符
print(letters[-3:])	# xyz 提取最后三个字符
print(letters[18:-3]) # stuvw	从偏移量为 18 的字符到倒数第 4 个字符, 注意与上一个
例子的区别：当偏移量 -3 作为开始位置时，将获得字符x；而当它作为终止位置时，分片实际
上会在偏移量 -4 处停止，也就是提取到字符 w

print(letters[-6:-2]) # uvwx	从倒数第 6 个字符到倒数第 3 个字符
print(letters[::7])	# ahov	从开头提取到结尾，步长设为 7
print(letters[4:20:3]) # ehknqt	从偏移量 4 提取到偏移量 19，步长设为 3
print(letters[19::4]) # tx	从偏移量 19 提取到结尾，步长设为 4
print(letters[:21:5]) # afkpu	从开头提取到偏移量 20，步长设为 5,记住，分片
中 end 的偏移量需要比实际提取的最后一个字符的偏移量多 1

# 如果指定的步长为负数会从右到左反向进行提取操作。
print(letters[-1::-1]) # zyxwvutsrqponmlkjihgfedcba   从右到左以步长为 1 进行提取，下面的
效果一样也更简单
print(letters[::-1]) # zyxwvutsrqponmlkjihgfedcba 效果同上

# 在分片中，小于起始位置的偏移量会被当作 0，大于终止位置的偏移量会被当作 -1，
print(letters[-50:]) # abcdefghijklmnopqrstuvwxyz 提取倒数 50 个字符
print(letters[-50:-51]) # 得到空，提取从倒数第 51 到倒数第 50 个字符
print(letters[:70])	# abcdefghijklmnopqrstuvwxyz  从开头提取到偏移量为 69 的字符
print(letters[70:71])  # 得到空， 从偏移量为 70 的字符提取到偏移量为 71 的字符
```
## 取字符串的一部分
其实就是切片操作...
```
with open('pi_digits.txt') as file_object:
    lines = file_object.readlines()
pi_string = ''
for line in lines:
	pi_string += line.strip()
print(pi_string)
print(f"{pi_string[:20]}...")
print(len(pi_string))

[huawei@n148 pytest]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
3.141592653589793238462643383279
3.141592653589793238...
32
```
# 列表【】 list
- 列表非常适合利用顺序和位置定位某一元素
- 列表元素是可变的
- 使用中括号定义
- 在列表中，具有相同值的元素允许出现多次

## 创建与访问元素
索引-1指向最后一个，-2则是倒数第二个，以此类推
```
#!/usr/bin/python3
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
print(bicycles[0])
print(bicycles[0].title())
print(bicycles[-1])
print(bicycles[-2])

message = f"My first bicycle was a {bicycles[0].title()}."
print(message)
[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['trek', 'cannondale', 'redline', 'specialized']
trek
Trek
specialized
redline
My first bicycle was a Trek.
```
### 使用range初始化
```
#!/usr/bin/python3
for value in range(1, 6):	# 产生列表[1,2,3,4,5]，注意没有6
	print(value)
numbers = list(range(1, 6))	# 产生列表赋值
print(numbers)
even_numbers = list(range(2, 11, 2))	# 可以指定步长
print(min(even_numbers))
print(max(even_numbers))
print(sum(even_numbers))

squares = [value**2 for value in range(1, 11)] # 类似perl map方法
print(squares)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
1
2
3
4
5
[1, 2, 3, 4, 5]
2
10
30
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
### 使用*初始化
生成包含n个指定初值元素的列表
```
sequence = [None] * 10  # [None, None, None, None, None, None, None, None, None, None]
```
### 使用list初始化
使用list()将其他数据类型转换成列表
- 字符串转字符列表
```
arr = list('Hello')
print(arr)	# ['H', 'e', 'l', 'l', 'o']

可以使用 ''.join(somelist) 再连起来
```
- 创建空的列表
```
another_empty_list = list()
```
- 元祖转列表
```
a_tuple = ('ready', 'fire', 'aim')
print(list(a_tuple))
```
## 使用=赋值（类似引用），使用copy()复制
- 如果将一个列表赋值给了多个变量，改变其中的任何一处会造成其他变量对应的值也被修改，即不能使用等号进行复制，见下例，这里的结果类似引用
```
#!/usr/bin/python3
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods
my_foods.append('cannoli')
print(my_foods)
print(friend_foods)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['pizza', 'falafel', 'carrot cake', 'cannoli']
['pizza', 'falafel', 'carrot cake', 'cannoli']
```
- copy类似深拷贝效果
  - 可以使用切片方式[:]
  - 还可以使用copy方法
  - 使用list方法
```
#!/usr/bin/python3
my_foods = ['pizza', 'falafel', 'carrot cake']

方法1：	friend_foods = my_foods[:]
方法2：	friend_foods = my_foods.copy()
方法3：	friend_foods = list(my_foods)

my_foods.append('cannoli')
print(my_foods)
print(friend_foods)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['pizza', 'falafel', 'carrot cake', 'cannoli']
['pizza', 'falafel', 'carrot cake']
```
## 合并 extend
- 使用加号连接，产生新的列表，原有列表不变
- 使用extend会更新原有列表，也可以使用 +=
```
a = [1, 2, 3] 
b = [4, 5, 6] 
a.extend(b) # 等于 a = a + b，但extend效率高，也可以 a[len(a):] = b （但可读性差）
print(a)	# [1, 2, 3, 4, 5, 6]
print(b)	# [4, 5, 6]
c = [7, 8, 9] 
d = b + c
print(b)	# [4, 5, 6]
print(c)	# [7, 8, 9]
print(d)	# [4, 5, 6, 7, 8, 9]
```
## 增删改查
- append	添加元素至尾部
- insert	在指定位置插入元素
- del	删除指定位置的元素
- remove	删除具有指定值的元素
- pop	获取并删除指定位置的元素
```
#!/usr/bin/python3
motorcycles = []	# 空列表
motorcycles.append('honda')	# 添加到列表末尾
motorcycles.append('yamaha')
motorcycles.append('suzuki')
print(motorcycles)
motorcycles[0] = 'ducati'	# 修改元素
print(motorcycles)
motorcycles.insert(1, 'aaa')	# 插入到指定位置，也可以使用切片的插入方式（参考切片操作）
print(motorcycles)
del motorcycles[1]	# 删除指定索引的元素，使用pop可以得到删除的值
print(motorcycles)
popped_motorcycle = motorcycles.pop()	# 删除并返回末尾元素，也可以指定位置，如下
print(motorcycles)
print(popped_motorcycle)
first_owned = motorcycles.pop(0)
print(f"The first motorcycle I owned was a {first_owned.title()}.")

print("----------------")
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
motorcycles.remove('ducati')	# 删除指定内容，默认仅去除第一个，全部去除需要循环，参考下面
print(motorcycles)
```
循环去除指定元素
```
#!/usr/bin/python3
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)
while 'cat' in pets:
	pets.remove('cat')
print(pets)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
['dog', 'dog', 'goldfish', 'rabbit']
```
## 清除
```
numbers.clear() 
```
## 排序sort、sorted
- 列表方法 sort() 会对原列表进行排序，改变原列表内容
- 通用函数 sorted() 则会返回排好序的列表副本，原列表内容不变
```
#!/usr/bin/python3
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort()	# 永久排序，改变元素
print(cars)
cars.sort(reverse=True)	# 倒序参数
print(cars)
print(sorted(cars))		# 返回排序后的结果，不改变内容
```
## 跌倒 reversed
- reverse将所有元素反序（直接修改列表）
- reversed
```
#!/usr/bin/python3
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.reverse()
print(cars)
[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['subaru', 'toyota', 'audi', 'bmw']
```

```
s = [4, 3, 6, 8, 3]
s2 = sorted(s)	# 返回一个列表
print(s)
print(s2)
s = 'Hello, world!'
s2 = sorted(s)
print(s)
print(s2)

s3 = list(reversed(s)) # reversed返回可迭代对象
print(s3)

s4 = ''.join(reversed(s)) 
print(s4)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
[4, 3, 6, 8, 3]
[3, 3, 4, 6, 8]
Hello, world!
[' ', '!', ',', 'H', 'd', 'e', 'l', 'l', 'l', 'o', 'o', 'r', 'w']
['!', 'd', 'l', 'r', 'o', 'w', ' ', ',', 'o', 'l', 'l', 'e', 'H']
!dlrow ,olleH
```
## 判断空列表
```
#!/usr/bin/python3
requested_toppings = []
if requested_toppings:
	for requested_topping in requested_toppings:
 		print(f"Adding {requested_topping}.")
else:
	print("Are you sure you want a plain pizza?")
```
## 长度 len
```
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(len(cars))
```
## 统计出现次数 count
计算指定的元素在列表中出现了多少次
```
print(['to', 'be', 'or', 'not', 'to', 'be'].count('to'))
x = [[1, 2], 1, 1, [2, 1, [1, 2]]] 
print(x.count(1))
print(x.count([1, 2]))

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
2
2
1
```
## 检查存在 in
表达式v in l（其中l是一个列表）查找的是值而不是索引
```
#!/usr/bin/python3
magicians = ['alice', 'david', 'carolina']
print('david' in magicians)
if 'xxx' not in magicians:
	print("not in")
```
只要元素类型一致即可进行检测
```
database = [ 
 ['albert', '1234'], 
 ['dilbert', '4242'], 
 ['smith', '7524'], 
 ['jones', '9843'] 
] 
username = 'smith'
pin = '7524'
if [username, pin] in database: print('Access granted')
```
## 查找 index
在列表中查找指定值第一次出现的索引，但找不到则err了...需要try才行
```
knights = ['We', 'are', 'the', 'knights', 'who', 'say', 'ni'] 
print(knights.index('who')) 	# 4
knights.index('herring')	# err
```
## 转字符串
```
marxes = ['Groucho', 'Chico', 'Harpo']
print(', '.join(marxes))

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
Groucho, Chico, Harpo
```
## 遍历
- foreach形式
```
#!/usr/bin/python3
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")

print("Thank you, everyone. That was a great magic show!")


words = ['this', 'is', 'an', 'ex', 'parrot'] 
for word in words:
    print(word) 
for word in [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]:
 	print(word) 
for number in range(1,11):
    print(number) 
```
- enumerate  
  即可以获得idx也能获得元素内容，有些时候可以代替下面的for
```
strings = "abcdefg"
for index, string in enumerate(strings): 
	print(index, string)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
0 a
1 b
2 c
3 d
4 e
5 f
6 g
```
- for形式
```
names = ['anne', 'beth', 'george', 'damon'] 
ages = [12, 45, 32, 102] 
for i in range(len(names)): 
	print(names[i], 'is', ages[i], 'years old') 
```
- while形式
```
#!/usr/bin/python3
# 首先，创建一个待验证用户列表
 # 和一个用于存储已验证用户的空列表。
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []
 # 验证每个用户，直到没有未验证用户为止。
 # 将每个经过验证的用户都移到已验证用户列表中。
while unconfirmed_users:
	current_user = unconfirmed_users.pop()
	print(f"Verifying user: {current_user.title()}")
	confirmed_users.append(current_user)
# 显示所有已验证的用户。
print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
	print(confirmed_user.title())
```
## 创建切片
- 使用切片（slicing）来访问特定范围内的元素。两个索引来指定切片的边界
- 第一个索引指定的元素包含在切片内，但第二个索引指定的元素不包含在切片内。
- 切片的步长默认为1，但也可以设置
- 切片都是副本，与原列表是不同内存，互不干涉
- 列表的切片仍然是一个列表

```
#!/usr/bin/python3
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[0:3])	# 0、1、2
print(players[1:4])	# 1、2、3
print(players[:4])	# 前4个，0、1、2、3
print(players[2:])	# 从第3个到最后，不含0、1的其余
print(players[-3:]) # 最后3个

for player in players[:3]:	# 遍历切片
	print(player.title())

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['charles', 'martina', 'michael']
['martina', 'michael', 'florence']
['charles', 'martina', 'michael', 'florence']
['michael', 'florence', 'eli']
['michael', 'florence', 'eli']
Charles
Martina
Michael
```
## 切片的步长
```
#!/usr/bin/python3
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 
print(numbers)
print(numbers[0:10:2])	# 从起点和终点之间每隔一个元素提取一个元素
print(numbers[::4])	# 从序列中每隔3个元素提取1个，只需提供步长4即可。
print(numbers[8:3:-1])
print(numbers[10:0:-2]) 
print(numbers[0:10:-2])
print(numbers[::-2])
print(numbers[5::-2]) 
print(numbers[:5:-2])

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[1, 3, 5, 7, 9]
[1, 5, 9]
[9, 8, 7, 6, 5]
[10, 8, 6, 4, 2]
[]
[10, 8, 6, 4, 2]
[6, 4, 2]
[10, 8]
```
## 切片的插入、删除、替换
```
#!/usr/bin/python3
name = list('Perl')
name[1:] = list('ython') # 相当于替换n个连续的元素，且无需数量一致
print(name)	# ['P', 'y', 't', 'h', 'o', 'n']


numbers = [1, 5] 
numbers[1:1] = [2, 3, 4] # 相当于插入n个元素（可读性比使用insert差很多）
print(numbers) # [1, 2, 3, 4, 5]
numbers[1:4] = []  # 相当于删除连续的n个元素，这里还加入步长（大于1或负数的步长），那就可以跳跃清除了
print(numbers)	# [1, 5]
```
## zip
- 便于同时迭代2个列表
- 返回由元组组成的可迭代序列
- 可使用list将其转换为列表

```
names = ['anne', 'beth', 'george', 'damon'] 
ages = [12, 45, 32, 102] 
for name, age in zip(names, ages): 
	print(name, 'is', age, 'years old') 

print(list(zip(range(5), range(100000000))))

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
anne is 12 years old
beth is 45 years old
george is 32 years old
damon is 102 years old
[(0, 0), (1, 1), (2, 2), (3, 3), (4, 4)]
```
# 元组（） tuple
- 与列表类似，元组也是由任意类型元素组成的序列。
- 与列表不同的是，元组是不可变的，这意味着一旦元组被定义，将无法再进行增加、删除或修改元素等操作。因此，元组就像是一个常量列表。
- 使用圆括号定义
- 空元组用两个不包含任何内容的圆括号表示
- 一个值的元组要有逗号
- 元组的切片还是元组
- 元组占用的空间较小
- 可以将元组用作字典的键
- 函数的参数是以元组形式传递的
- 命名元组可以作为对象的替代
```
#!/usr/bin/python3
dimensions = (200, 50)	# 定义tuple
print(dimensions[0])	# 取元素
print(dimensions[1])
# dimensions[0] = 250 	不能修改元素
dimensions = (400, 100)	# 能重新全部赋值
print(dimensions)	
for dimension in dimensions:	# 遍历
	print(dimension)
```

## 使用()创建元组
```
empty_tuple = ()	# 可以用 () 创建一个空元组
print(empty_tuple)
one_marx = 'Groucho',	# 创建只包含一个元素的元祖要有逗号。定义元组真正靠的是每个元素的后缀逗号，而不是（）
print(one_marx)
marx_tuple = 'Groucho', 'Chico', 'Harpo'	# 创建的元组所包含的元素数量超过 1，最后一个元素后面的逗号可以省略
print(marx_tuple)
a, b, c = marx_tuple	# 将元组赋值给多个变量
print(a)
print(b)
print(c)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
()
('Groucho',)
('Groucho', 'Chico', 'Harpo')
Groucho
Chico
Harpo

```

## 序列解包
将一个序列（或任何可迭代对象）解包，并将得到的值存储到一系列变量中。可用于  
- 并行赋值
- 交换变量值
- 将序列赋值给元祖values
- 解开元祖到多个变量
- 使用*接收多个值到列表中
- 函数参数传递（主要是上一种方式）

```
x, y, z = 1, 2, 3 # 并行赋值
print(x, y, z) 
x, y = y, x	# 交换变量值
print(x, y) 
values = 10, 20, 30 # 将序列赋值给元祖values
print(values)
x, y, z = values # 解开元祖到多个变量
print(x, y, z) 

scoundrel = {'name': 'Robin', 'girlfriend': 'Marion'} 
key, value = scoundrel.popitem() # 返回元祖赋值给k和v
print(key, value)
a, b, *rest = [1, 2, 3, 4] 	# 可使用星号运算符（*）来收集多余的值，这样无需确保值和变量的个数相同，rest为列表
print(rest)

name = "Albus Percival Wulfric Brian Dumbledore" 
first, *middle, last = name.split() # *变量也可在其他位置
print(middle)

a, *b, c = "abc" # 带星号的变量始终也是列表，即使元素仅1个
print(a, b, c)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
1 2 3
2 1
(10, 20, 30)
10 20 30
girlfriend Marion
[3, 4]
['Percival', 'Wulfric', 'Brian']
a ['b'] c
```
## 使用tuple()创建元组

函数tuple的工作原理与list很像：它将一个序列作为参数，并将其转换为元组。如果参数
已经是元组，就原封不动地返回它。
```
print(3 * (40 + 2))	# 这个不是元祖，因为没有逗号
print(3 * (40 + 2,))
print(tuple([1, 2, 3]))
print(tuple('abc'))
print(tuple((1, 2, 3)))
x = 1, 2, 3
print(x[0:2])

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
126
(42, 42, 42)
(1, 2, 3)
('a', 'b', 'c')
(1, 2, 3)
(1, 2)
```
# 字典 { } dict
- 字典由键及其相应的值组成，这种键值对称为项（item）。
- 每个键与其值之间都用冒号（:）分隔，项之间用逗号分隔，而整个字典放在花括号内。
- 空字典（没有任何项）用两个花括号表示，类似于下面这样：{}。
- 在字典（以及其他映射类型）中，键必须是独一无二的，而字典中的值无需如此。
- 字典的键必须为不可变对象，因此列表、字典以及集合都不能作为字典的键，但元组可以作为字典的键
## 构建方法
- 使用dict方法
- 使用{}
- 使用dict.fromkeys构建所有v都一样的字典
```
# dict（tuple列表形式）,tuple必须2个元素，否则失败
items = [('name', 'Gumby'), ('age', 42)] 
d = dict(items)  
print(d)	# {'name': 'Gumby', 'age': 42}
print(d['name'])	# Gumby

# dict（嵌套列表形式）,内部列表只能2个元素，否则失败
lol = [ ['a', 'b'], ['c', 'd'], ['e', 'f'] ] 
m = dict(lol)
print(m)	# {'a': 'b', 'c': 'd', 'e': 'f'}

# 使用dict方法构建，kv形式，kv要齐全，否则失败
d = dict(name='Gumby', age=42) 	
print(d) # {'name': 'Gumby', 'age': 42}

empty_dict = {} # 空字典

# 使用键值对方式构建，kv要齐全，否则出错
phonebook = {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}
print(phonebook)	# {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}


# 双字符的字符串组成的列表，只能2个字符，否则出错
m = [ 'ab', 'cd', 'ef' ]
print(dict(m))	# {'a': 'b', 'c': 'd', 'e': 'f'}

# 双字符的字符串组成的元组，只能2个字符，否则出错
m = ( 'ab', 'cd', 'ef' )
print(dict(m))	# {'a': 'b', 'c': 'd', 'e': 'f'}


# 使用dict.fromkeys
print(dict.fromkeys(['name', 'age']))	# {'name': None, 'age': None}
print(dict.fromkeys(['name', 'age'], '(unknown)'))	# {'name': '(unknown)', 'age': '(unknown)'}
```
## 访问【】、get
- [ ]
	访问不存在的元素会error
- get
	安全的获取元素方式，没有则返回指定的字符串
- setdefault
	获取与指定键相关联的值，字典不包含指定的键时，在字典中添加指定的键值对。也可指定默认的字符串作为v，如果没有指定，默认v为None。
```
#!/usr/bin/python3
alien_0 = {'color': 'green', 'points': 5}		# 定义字典
print(alien_0['color'])		# green,	访问元素
# print(alien_0['color1'])	访问不存在的元素会error，下句使用get进行安全访问
point_value = alien_0.get('not', 'No point value assigned.') # 安全的获取元素方式，没有则返回第二个字符串
print(point_value)	# No point value assigned.		
print(alien_0)	# {'color': 'green', 'points': 5}
point_value  = alien_0.setdefault('not')	# 没有找到就添加到字典中
print(point_value)	# None
print(alien_0)	# {'color': 'green', 'points': 5, 'not': None}
```
## 增删改查
- del	删除具有指定键的元素

```
#!/usr/bin/python3
alien_0 = {'color': 'green', 'points': 5}		# 定义字典
print(alien_0)
alien_0['x_position'] = 0		# 添加元素
alien_0['y_position'] = 25
print(alien_0)

alien_0 = {}			# 创建空字典，这里其实是把上面的字典清了
alien_0['color'] = 'green'
alien_0['points'] = 5
print(alien_0)
alien_0['color'] = 'yellow'		# 修改元素
print(f"The alien is now {alien_0['color']}.")
del alien_0['points']		# 删除元素，删除还有pop
print(alien_0)


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
{'color': 'green', 'points': 5}
{'color': 'green', 'points': 5, 'x_position': 0, 'y_position': 25}
{'color': 'green', 'points': 5}
The alien is now yellow.
{'color': 'yellow'}
```
## 合并 update
可以将一个字典的键值对复制到另一个字典中去。字典有此k则更新v，没有k则添加到字典里
```
d = { 
'title': 'Python Web Site', 
'url': 'http://www.python.org', 
'changed': 'Mar 14 22:09:15 MET 2016' 
} 

x = {'title': 'Python Language Website'} 
d.update(x)
print(d);

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
{'title': 'Python Language Website', 'url': 'http://www.python.org', 'changed': 'Mar 14 22:09:15 MET 2016'}
```
## pop、popitem
```
phonebook = {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}
print(phonebook.pop('Beth'))	# 9102	返回指定k进行pop的v
print(phonebook)	# {'Alice': '2341', 'Cecil': '3258'}	剩余2个kv
print(phonebook.popitem())	# ('Cecil', '3258')	返回随机pop的kv，返回值是元祖，但测试每次都相同
print(phonebook)	# {'Alice': '2341'}		剩余1个kv
key, value = phonebook.popitem() # 将pop的元祖赋值给k和v
print(key, value)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
{'Alice': '2341', 'Cecil': '3258'}
('Cecil', '3258')
{'Alice': '2341'}
Alice 2341
```
## 检测K存在 in
表达式k in d（其中d是一个字典）查找的是键而不是值
```
phonebook = {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}	# 使用键值对方式构建
print(phonebook)	# {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}
print('Beth' in phonebook);	# True
```
## 字典视图 items
-	返回值属于一种名为字典视图的特殊类型。字典视图可用于迭代，还可执行len与in检测。其中每个元素都为键值对，且顺序不确定。
-	修改字典后视图会同步，但视图是只读的不允许修改
```
phonebook = {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}
pairs = phonebook.items() 
print("修改前")
print(pairs)
print(len(pairs))
print(phonebook)
print(('Beth', '9102') in pairs)
print(phonebook.get('Beth', "not find") == '9102');


print("修改字典后")
phonebook['Beth'] = '9999'
print(pairs)
print(phonebook)
print(('Beth', '9102') in pairs)
print(phonebook.get('Beth', "not find") == '9102');

print("修改视图后")
pairs[1] = ('Beth', '0000')  不支持赋值
print(pairs)
print(phonebook)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
修改前
dict_items([('Alice', '2341'), ('Beth', '9102'), ('Cecil', '3258')])
3
{'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}
True
True
修改字典后
dict_items([('Alice', '2341'), ('Beth', '9999'), ('Cecil', '3258')])
{'Alice': '2341', 'Beth': '9999', 'Cecil': '3258'}
False
False
修改视图后
Traceback (most recent call last):
  File "/home/huawei/playground/pythontest/pyth.py", line 20, in <module>
    pairs[1] = ('Beth', '0000')
TypeError: 'dict_items' object does not support item assignment
```
## 遍历
```
d = {'x': 1, 'y': 2, 'z': 3} 
for key in d: 
	print(key, 'corresponds to', d[key]) 
for key, value in d.items(): 
	print(key, 'corresponds to', value) 

```
## keys、values、items、sort、set
- keys
  	获取仅包含字典中的键的视图（dict_keys()，它是键的迭代形式）
- values
	返回一个由字典中的值组成的字典视图，如果字典中有重复的v则视图中也包含这些重复内容。
- items
  	函数可以获取字典中所有的键值对
- keys、values、items的返回结果均可作为list()方法的参数，返回列表
```
#!/usr/bin/python3
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python',
}
for name, language in favorite_languages.items():	# 遍历kv
	print(f"{name.title()}'s favorite language is {language.title()}.")
for name in favorite_languages.keys():		# 遍历k
	print(name.title())
for name in sorted(favorite_languages.keys()):	# 对返回的keys排序后再遍历
 	print(f"{name.title()}, thank you for taking the poll.") 
if 'erin' not in favorite_languages.keys():	# 判断存在k，此处是检测一个值在不在列表里，非检测k in d
	print("Erin, please take our poll!")

for language in favorite_languages.values():	# 遍历values
	print(language.title())
for language in set(favorite_languages.values()):	# 对返回的values集合进行去重后再遍历
	print(language.title())


```
## 格式化format
只要在字典中有此kv则就可以替换到format的参数里
```
#!/usr/bin/python3
template = '''<html> 
<head><title>{title}</title></head> 
<body> 
<h1>{title}</h1> 
<p>{text}</p> 
</body>''' 
data = {'title': 'My Home Page', 'text': 'Welcome to my home page!'} 
print(template.format_map(data)) 


print("Cecil's phone number is {Cecil}.".format_map({'Beth': '9102', 'Alice': '2341', 'Cecil': '3258'}))


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
<html> 
<head><title>My Home Page</title></head> 
<body> 
<h1>My Home Page</h1> 
<p>Welcome to my home page!</p> 
</body>
Cecil's phone number is 3258.
```
## 清除 clear
```
x.clear() 
```
## 使用=赋值，使用copy()复制
- 等号依然仅是引用，不是复制......
- 浅拷贝
  
  2个字典中machines的v（值是列表）y修改后x的也跟着变了，说明指向同一个堆地址
```
x = {'username': 'admin', 'machines': ['foo', 'bar', 'baz']} 
y = x.copy() 
y['username'] = 'mlh' 
y['machines'].remove('bar') 
print(x)
print(y)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
{'username': 'admin', 'machines': ['foo', 'baz']}
{'username': 'mlh', 'machines': ['foo', 'baz']}
```
- 深拷贝
	- 使用copy
	- 使用函数deepcopy进行拷贝
```
signals = {'green': 'go', 'yellow': 'go faster', 'red': 'smilefor the camera'}
original_signals = signals.copy()
signals['blue'] = 'confuse everyone'
print(signals)
print(original_signals)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
{'green': 'go', 'yellow': 'go faster', 'red': 'smilefor the camera', 'blue': 'confuse everyone'}
{'green': 'go', 'yellow': 'go faster', 'red': 'smilefor the camera'}
```  
```
#!/usr/bin/python3
from copy import deepcopy
x = {'username': 'admin', 'machines': ['foo', 'bar', 'baz']} 
y = deepcopy(x)  
y['username'] = 'mlh' 
y['machines'].remove('bar') 
print(x)
print(y)

d = {} 
d['names'] = ['Alfred', 'Bertrand'] 
c = d.copy() 
dc = deepcopy(d) 
d['names'].append('Clive') 
print(c)
print(dc)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
{'username': 'admin', 'machines': ['foo', 'bar', 'baz']}
{'username': 'mlh', 'machines': ['foo', 'baz']}
{'names': ['Alfred', 'Bertrand', 'Clive']}
{'names': ['Alfred', 'Bertrand']}
```
# 集合 set
尽管都由花括号包裹，集合仅仅是一系列值组成的序列，而字典是一个或多个键值对组成的序列。

## 创建
- 使用set()创建集合
- 使用set()将其他类型转换为集合
```
empty_set = set()	# 空set
print(empty_set)
even_numbers = {0, 2, 4, 6, 8}	# 普通构建方式
print(even_numbers)
print(set('letters'))	# 基于字符串
print(set(['Dasher', 'Dancer', 'Prancer', 'Mason-Dixon']))	# 基于列表
print(set(('Ummagumma', 'Echoes', 'Atom Heart Mother')))	# 基于元组
print(set({'apple': 'red', 'orange': 'orange', 'cherry': 'red'}))	# 基于字典，仅使用k

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
set()
{0, 2, 4, 6, 8}
{'s', 'l', 'e', 't', 'r'}
{'Dancer', 'Dasher', 'Prancer', 'Mason-Dixon'}
{'Atom Heart Mother', 'Echoes', 'Ummagumma'}
{'orange', 'cherry', 'apple'}
```
## 增删查、clear、len、copy
- add
- update
- remove
- discard
- pop
- len
- clear
- copy
- 
```
set1 = {'pear', 'banana', 'orange', 'apple'}
set1.add('kkk')	# 添加一个元素
print(set1)
set1.update({'kkk', 'ppp'})	# 添加多个元素
print(set1)

# 方法remove()和方法discard()的区别在于，方法remove()在移除元素时，如果元素不存在，会报错，中止程序运行，而方法discard()不会。
set1.remove('pear')	# 将指定元素从集合中移除
print(set1)
set1.pop()	# 随机删除集合中的一个元素
print(set1)
print(len(set1))	# 得到集合中元素的个数
set1.clear()	# 清空集合
print(set1)	
set1 = {'pear', 'banana', 'orange', 'apple'}
bool1 = 'apple' in set1	# 检测存在
print(bool1)
x = set1.copy()	# 深拷贝
print(x)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
{'apple', 'kkk', 'banana', 'pear', 'orange'}
{'ppp', 'apple', 'kkk', 'banana', 'pear', 'orange'}
{'ppp', 'apple', 'kkk', 'banana', 'orange'}
{'apple', 'kkk', 'banana', 'orange'}
4
set()
True
{'banana', 'pear', 'orange', 'apple'}
```
## 检测 in
使用in测试k是否存在
```
drinks = {
'martini': {'vodka', 'vermouth'},
'black russian': {'vodka', 'kahlua'},
'white russian': {'cream', 'kahlua', 'vodka'},
'manhattan': {'rye', 'vermouth', 'bitters'},
'screwdriver': {'orange juice', 'vodka'}
}
for name, contents in drinks.items():
	if 'vodka' in contents and not ('vermouth' in contents or 'cream' in contents):
		print(name)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
black russian
screwdriver
```
## 交集、并集、差集
https://blog.csdn.net/wenhao_ir/article/details/125424671
# 复杂数据结构
## 元祖里存列表
```
marxes = ['Groucho', 'Chico', 'Harpo']
pythons = ['Chapman', 'Cleese', 'Gilliam', 'Jones', 'Palin']
stooges = ['Moe', 'Curly', 'Larry']
tuple_of_lists = marxes, pythons, stooges
print(tuple_of_lists)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
(['Groucho', 'Chico', 'Harpo'], ['Chapman', 'Cleese', 'Gilliam', 'Jones', 'Palin'], ['Moe', 'Curly', 'Larry'])
```
## 字典的k是元祖
```

houses = {
	(44.79, -93.14, 285): 'My House',
	(38.89, -77.03, 13): 'The White House'
}

print(houses)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
{(44.79, -93.14, 285): 'My House', (38.89, -77.03, 13): 'The White House'}
```
## 列表里存列表
```
small_birds = ['hummingbird', 'finch']
extinct_birds = ['dodo', 'passenger pigeon', 'Norwegian Blue']
carol_birds = [3, 'French hens', 2, 'turtledoves']
all_birds = [small_birds, extinct_birds, 'macaw', carol_birds]

print(all_birds)
print(all_birds[0])
print(all_birds[1][0])

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
[['hummingbird', 'finch'], ['dodo', 'passenger pigeon', 'Norwegian Blue'], 'macaw', [3, 'French hens', 2, 'turtledoves']]
['hummingbird', 'finch']
dodo
```
## 列表里存字典
```
#!/usr/bin/python3
# 创建一个用于存储外星人的空列表。
aliens = []
# 创建30个绿色的外星人。
for alien_number in range (30):
	new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
	aliens.append(new_alien)
for alien in aliens[:3]:
	if alien['color'] == 'green':
		alien['color'] = 'yellow'
		alien['speed'] = 'medium'
		alien['points'] = 10
# 显示前5个外星人。
for alien in aliens[:5]:
	print(alien)
print("...")

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
...
```
## 字典里存列表
```
#!/usr/bin/python3
favorite_languages = {
	'jen': ['python', 'ruby'],
	'sarah': ['c'],
	'edward': ['ruby', 'go'],
	'phil': ['python', 'haskell'],
}
for name, languages in favorite_languages.items():
	print(f"\n{name.title()}'s favorite languages are:")
	for language in languages:
		print(f"\t{language.title()}")

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"

Jen's favorite languages are:
        Python
        Ruby

Sarah's favorite languages are:
        C

Edward's favorite languages are:
        Ruby
        Go

Phil's favorite languages are:
        Python
        Haskell
```
## 字典里存字典
```
#!/usr/bin/python3
users = {
	'aeinstein': {
		'first': 'albert',
		'last': 'einstein',
		'location': 'princeton',
	},
	'mcurie': {
		'first': 'marie',
		'last': 'curie',
		'location': 'paris',
	},
}
for username, user_info in users.items():
	print(f"\nUsername: {username}")
	full_name = f"{user_info['first']} {user_info['last']}"
	location = user_info['location']
	print(f"\tFull name: {full_name.title()}")
	print(f"\tLocation: {location.title()}")


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"

Username: aeinstein
        Full name: Albert Einstein
        Location: Princeton

Username: mcurie
        Full name: Marie Curie
        Location: Paris
```
### 通讯录案例
演示了通过"[][]"来访问内层字典的元素值
```
#!/usr/bin/python3

people = { 
 'Alice': { 
 'phone': '2341', 
 'addr': 'Foo drive 23' 
 }, 
 'Beth': { 
 'phone': '9102', 
 'addr': 'Bar street 42' 
 }, 
'Cecil': { 
 'phone': '3158', 
 'addr': 'Baz avenue 90' 
 } 
}

# 电话号码和地址的描述性标签，供打印输出时使用
labels = { 
 'phone': 'phone number', 
 'addr': 'address' 
} 
name = input('Name: ') 
# 要查找电话号码还是地址？
request = input('Phone number (p) or address (a)? ') 
# 使用正确的键：
if request == 'p': key = 'phone' 
if request == 'a': key = 'addr' 
# 使用get提供默认值
person = people.get(name, {}) 
label = labels.get(key, key) 
result = person.get(key, 'not available') 
print("{}'s {} is {}.".format(name, label, result)) 


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Name: Beth
Phone number (p) or address (a)? a
Beth's address is Bar street 42.
[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Name: Cecil
Phone number (p) or address (a)? p
Cecil's phone number is 3158.
```
# 判断
## 比较数值与字符串
```
#!/usr/bin/python3
requested_topping = 'mushrooms'
if requested_topping != 'anchovies':
	print("Hold the anchovies!")
car = 'Audi'
print(car.lower() == 'audi')

answer = 17
if answer != 42:
	print("That is not the correct answer. Please try again!")

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Hold the anchovies!
True
That is not the correct answer. Please try again!
```
## 比较运算符
- 0 < age < 100  
  Python支持链式比较，可同时使用多个比较运算符
- == 用来检查两个对象是否相等
- x != y  
  x不等于y
- x is y  
  is用来检查两个对象是否相同（是同一个对象）
```
names = ['Mrs. Entity', 'Mrs. Thing'] 
n = names[:] 
print(n is names)
print(n == names)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
False
True
```
- x is not y  
  x和y是不同的对象
- x in y  
  x是容器（如序列）y的成员
- x not in y  
  x不是容器（如序列）y的成员

## if else
```
#!/usr/bin/python3
age = 17
if age >= 18:
	print("You are old enough to vote!")
	print("Have you registered to vote yet?")
else:
	print("Sorry, you are too young to vote.")
	print("Please register to vote as soon as you turn 18!")
	
```
## 条件表达式
即都写在一行里
```
status = "friend" if name.endswith("Gumby") else "stranger" 
```
## else if
```
#!/usr/bin/python3
age = 12
if age < 4:
	price = 0
elif age < 18:
	price = 25
elif age < 65:
	price = 40
else:
	price = 20
print(f"Your admission cost is ${price}.")
```
```
#!/usr/bin/python3
requested_toppings = ['mushrooms', 'extra cheese']
if 'mushrooms' in requested_toppings:
	print("Adding mushrooms.")
elif 'pepperoni' in requested_toppings:
	print("Adding pepperoni.")
elif 'extra cheese' in requested_toppings:
	print("Adding extra cheese.")
print("\nFinished making your pizza!")
```
## 布尔运算符 and、or
```
(age_0 >= 21) and (age_1 >= 21)
(age_0 >= 21) or (age_1 >= 21)
如果是简单的比较则可以使用链式 1 <= number <= 10
```
## 断言
```
age = 10 
assert 0 < age < 100 
age = -1 
assert 0 < age < 100, 'The age must be realistic'  # 可以自定义输出，否则就是默认
assert 0 < age < 100 
```
# 循环
## while
```
#!/usr/bin/python3
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "
message = ""
while message != 'quit':
 message = input(prompt)
 if message != 'quit':
     print(message)
```
## for
```
words = ['this', 'is', 'an', 'ex', 'parrot'] 
for word in words:
    print(word) 

for word in [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]:
 	print(word) 

for number in range(1,11):
    print(number) 

d = {'x': 1, 'y': 2, 'z': 3} 
for key in d: 
	print(key, 'corresponds to', d[key]) 
for key, value in d.items(): 
	print(key, 'corresponds to', value) 


names = ['anne', 'beth', 'george', 'damon'] 
ages = [12, 45, 32, 102] 
for i in range(len(names)): 
	print(names[i], 'is', ages[i], 'years old') 
```
## break、continue
```
from math import sqrt 
for n in range(99, 0, -1): 
	root = sqrt(n) 
	if root == int(root): 
		print(n) 
		break

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
81		
```		
# 函数
## 定义、传值、默认值
```
#!/usr/bin/python3
def describe_pet(pet_name, animal_type='dog'):
	"""显示宠物的信息。"""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('hamster', 'harry')
describe_pet(pet_name='harry', animal_type='hamster')
describe_pet(pet_name='willie')
```
## 返回值
```
def get_formatted_name(first_name, last_name, middle_name=''):
	if middle_name:
		full_name = f"{first_name} {middle_name} {last_name}"
	else:
		full_name = f"{first_name} {last_name}"
	return full_name.title()

musician = get_formatted_name('jimi', 'hendrix')
print(musician)
musician = get_formatted_name('john', 'hooker', 'lee')
print(musician)
```
## （传址）传列表、传字典
实际是传引用，在函数内删掉后外面也都没了
```
#!/usr/bin/python3

def fun1(arr):
	while(arr):
		arr.pop()

unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']
print(unprinted_designs)
fun1(unprinted_designs)
print(unprinted_designs)



def fun2(dict):
	del dict['color']

alien_0 = {'color': 'green', 'points': 5}
print(alien_0)
fun2(alien_0)
print(alien_0)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['phone case', 'robot pendant', 'dodecahedron']
[]
{'color': 'green', 'points': 5}
{'points': 5}
```
## （传值）传列表切片
实则传递的是列表的副本，外面和里面不是同一份数据
```
#!/usr/bin/python3

def fun1(arr):
	while(arr):
		arr.pop()

unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']
print(unprinted_designs)
fun1(unprinted_designs[:])
print(unprinted_designs)



def fun2(dict):
	del dict['color']

alien_0 = {'color': 'green', 'points': 5}
print(alien_0)
fun2(alien_0)
print(alien_0)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['phone case', 'robot pendant', 'dodecahedron']
['phone case', 'robot pendant', 'dodecahedron']
{'color': 'green', 'points': 5}
{'points': 5}

```

## 传递任意个参数（收集参数）
- 参数前面的星号将提供的所有值都放在一个元组中，也就是将这些值收集起来。
- 效果类似perl的ARGV与@_
- 一个*实际对应的是元祖
- **user_info则对应字典

下例* toppings实则会变为元祖，内容为('mushrooms', 'green peppers', 'extra cheese')。
```
#!/usr/bin/python3

def make_pizza(size, *toppings):
	print(f"\nMaking a {size}-inch pizza with the following toppings:")
	for topping in toppings:
		print(f"- {topping}")
make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')


def build_profile(first, last, **user_info):
	user_info['first_name'] = first
	user_info['last_name'] = last
	return user_info
user_profile = build_profile('albert', 'einstein', location='princeton', field='physics')
print(user_profile)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"

Making a 16-inch pizza with the following toppings:
- pepperoni

Making a 12-inch pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
{'location': 'princeton', 'field': 'physics', 'first_name': 'albert', 'last_name': 'einstein'}
```
- 如果在定义和调用函数时都使用*或**，将只能传递元组或字典。反而不便

如下，两种方式结果一样
```
def with_stars(**kwds): 
	print(kwds['name'], 'is', kwds['age'], 'years old') 

def without_stars(kwds): 
	print(kwds['name'], 'is', kwds['age'], 'years old') 

args = {'name': 'Mr. Gumby', 'age': 42} 
with_stars(**args) 
without_stars(args) 

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Mr. Gumby is 42 years old
Mr. Gumby is 42 years old
```
- 只有在定义函数（允许可变数量的参数）或调用函数时（拆分字典或序列）使用，星号才能发挥作用

使用这些拆分运算符来传递参数很有用，因为这样无需操心参数个数之类的问题，如下这在调用超类的构造函数时特别有用
```
def foo(x, y, z, m=0, n=0): 
	print(x, y, z, m, n) 
def call_foo(*args, **kwds): 
	print("Calling foo!") 
	foo(*args, **kwds) 
```
综合演示
```
def story(**kwds): 
	return 'Once upon a time, there was a {job} called {name}.'.format_map(kwds)
def power(x, y, *others): 
	if others: 
		print('Received redundant parameters:', others) 
	return pow(x, y) 
def interval(start, stop=None, step=1): 
	'Imitates range() for step > 0' 
	if stop is None: # 如果没有给参数stop指定值，
		start, stop = 0, start # 就调整参数start和stop的值
	result = [] 
	i = start # 从start开始往上数
	while i < stop:  # 数到stop位置
		result.append(i) # 将当前数的数附加到result末尾
		i += step # 增加到当前数和step（> 0）之和
	return result

print(story(job='king', name='Gumby')) 
print(story(name='Sir Robin', job='brave knight')) 
params = {'job': 'language', 'name': 'Python'} 
print(story(**params)) 
del params['job'] 
print(story(job='stroke of genius', **params)) 
print(power(2, 3))
print(power(3, 2))
print(power(y=3, x=2))
params = (5,) * 2 
print(power(*params))
print(power(3, 3, 'Hello, world'))
print(interval(10))
print(interval(1, 5))
print(interval(3, 12, 4))
print(power(*interval(3, 7)))

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Once upon a time, there was a king called Gumby.
Once upon a time, there was a brave knight called Sir Robin.
Once upon a time, there was a language called Python.
Once upon a time, there was a stroke of genius called Python.
8
9
8
3125
Received redundant parameters: ('Hello, world',)
27
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 2, 3, 4]
[3, 7, 11]
Received redundant parameters: (5, 6)
81
```
# 模块
## 定义
- 普通函数模块，另见类模块
```
[huawei@n148 pythontest]$ cat pizza.py 
#!/usr/bin/python3
def make_pizza(size, *toppings):
        print(f"\nMaking a {size}-inch pizza with the following toppings:")
        for topping in toppings:
                print(f"- {topping}")
```
## site-packages
- 模块sys的变量path所包含的路径列表即模块的搜索路径
- 模块位于类似于site-packages这样的地方，所有的程序就都能够导入它

```
#!/usr/bin/python3
import sys, pprint 
pprint.pprint(sys.path) 

[huawei@n148 pytest]$ python3 pyth.py 
['/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest',
 '/usr/local/lib/python3.6/site-packages/setuptools-19.6-py3.6.egg',
 '/usr/lib64/python36.zip',
 '/usr/lib64/python3.6',
 '/usr/lib64/python3.6/lib-dynload',
 '/usr/local/lib64/python3.6/site-packages',
 '/usr/local/lib/python3.6/site-packages',
 '/usr/lib64/python3.6/site-packages',
 '/usr/lib/python3.6/site-packages']
```
## 导入类
类模块的定义在上面
```
#!/usr/bin/python3
from car import Car
my_new_car = Car('audi', 'a4', 2019)
print(my_new_car.get_descriptive_name())
my_new_car.odometer_reading = 23
my_new_car.read_odometer()

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
2019 Audi A4
This car has 23 miles on it.
```

## 导入整个模块
使用import导入文件主干名，调用需要作用域
```
[huawei@n148 pythontest]$ cat making_pizzas.py 
#!/usr/bin/python3
import pizza
pizza.make_pizza(16, 'pepperoni')
pizza.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
[huawei@n148 pythontest]$ python3 making_pizzas.py 

Making a 16-inch pizza with the following toppings:
- pepperoni

Making a 12-inch pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
```
## 导入指定函数
调用可以直接函数名，不需要带作用域了，其实还可以全部都导入，如 from pizza import *
```
[huawei@n148 pythontest]$ cat making_pizzas.py 
#!/usr/bin/python3
from pizza import make_pizza
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
make_pizza(16, 'pepperoni')
[huawei@n148 pythontest]$ python3 making_pizzas.py 

Making a 12-inch pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese

Making a 16-inch pizza with the following toppings:
- pepperoni
```
## 给模块或函数指定别名
用于防止名称重复冲突
```
#!/usr/bin/python3
from pizza import make_pizza as mp
mp(12, 'mushrooms', 'green peppers', 'extra cheese')
mp(16, 'pepperoni')
```
```
#!/usr/bin/python3
import pizza as p
p.make_pizza(16, 'pepperoni')
p.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
## 类模块

### 定义模块文件
这里将多个类定义在一个文件里了，其实也可以分散开（见模块导入模块）
```
文件名 car.py

#!/usr/bin/python3
class Car:
	def __init__(self, make, model, year):
		self.make = make
		self.model = model
		self.year = year
		self.odometer_reading = 0

	def get_descriptive_name(self):
		long_name = f"{self.year} {self.make} {self.model}"
		return long_name.title()
	def read_odometer(self):
		print(f"This car has {self.odometer_reading} miles on it.")
	def update_odometer(self, mileage):
		if mileage >= self.odometer_reading:
			self.odometer_reading = mileage
		else:
			print("You can't roll back an odometer!")
	def increment_odometer(self, miles):
		self.odometer_reading += miles


class Battery:
	def __init__(self, battery_size=75):
		self.battery_size = battery_size
	def describe_battery(self):
		print(f"This car has a {self.battery_size}-kWh battery.")
	def get_range(self):
		if self.battery_size == 75:
			range = 260
		elif self.battery_size == 100:
			range = 315
		print(f"This car can go about {range} miles on a full charge.")


class ElectricCar(Car):
	def __init__(self, make, model, year):
		super().__init__(make, model, year)
		self.battery = Battery()
	def describe_battery(self):
		print(f"This car has a {self.battery_size}-kWh battery.")
```
### 使用类模块
- 这里分别导入了基类与子类
```
#!/usr/bin/python3
from car import Car
my_new_car = Car('audi', 'a4', 2019)
print(my_new_car.get_descriptive_name())
my_new_car.odometer_reading = 23
my_new_car.read_odometer()

from car import ElectricCar
my_tesla = ElectricCar('tesla', 'model s', 2019)
print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
my_tesla.battery.get_range()


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
2019 Audi A4
This car has 23 miles on it.
2019 Tesla Model S
This car has a 75-kWh battery.
This car can go about 260 miles on a full charge.

```
- 其实也可以从一次从模块中导入多个类
```
#!/usr/bin/python3
from car import Car, ElectricCar
my_beetle = Car('volkswagen', 'beetle', 2019)
print(my_beetle.get_descriptive_name())
my_tesla = ElectricCar('tesla', 'roadster', 2019)
print(my_tesla.get_descriptive_name())

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
2019 Volkswagen Beetle
2019 Tesla Roadster
```
- 还可以导入整个模块
```
#!/usr/bin/python3

import car
my_beetle = car.Car('volkswagen', 'beetle', 2019)
print(my_beetle.get_descriptive_name())
my_tesla = car.ElectricCar('tesla', 'roadster', 2019)
print(my_tesla.get_descriptive_name())
```

## 模块导入模块
即将不同类分散到不同文件中
- 基类模块
```
[huawei@n148 pythontest]$ cat car.py 
#!/usr/bin/python3

class Car:
        def __init__(self, make, model, year):
                self.make = make
                self.model = model
                self.year = year
                self.odometer_reading = 0

        def get_descriptive_name(self):
                long_name = f"{self.year} {self.make} {self.model}"
                return long_name.title()
        def read_odometer(self):
                print(f"This car has {self.odometer_reading} miles on it.")
        def update_odometer(self, mileage):
                if mileage >= self.odometer_reading:
                        self.odometer_reading = mileage
                else:
                        print("You can't roll back an odometer!")
        def increment_odometer(self, miles):
                self.odometer_reading += miles
```
- 子类模块，此模块需导入基类模块
```
[huawei@n148 pythontest]$ cat electric_car.py 
#!/usr/bin/python3
from car import Car

class Battery:
        def __init__(self, battery_size=75):
                self.battery_size = battery_size
        def describe_battery(self):
                print(f"This car has a {self.battery_size}-kWh battery.")
        def get_range(self):
                if self.battery_size == 75:
                        range = 260
                elif self.battery_size == 100:
                        range = 315
                print(f"This car can go about {range} miles on a full charge.")


class ElectricCar(Car):
        def __init__(self, make, model, year):
                super().__init__(make, model, year)
                self.battery = Battery()
        def describe_battery(self):
                print(f"This car has a {self.battery_size}-kWh battery.")
```
- 使用的代码，导入多个模块即可
```
#!/usr/bin/python3

from car import Car
from electric_car import ElectricCar
my_beetle = Car('volkswagen', 'beetle', 2019)
print(my_beetle.get_descriptive_name())
my_tesla = ElectricCar('tesla', 'roadster', 2019)
print(my_tesla.get_descriptive_name())

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
2019 Volkswagen Beetle
2019 Tesla Roadster
```
## 模块的测试方法
```
模块文件提供了一个方法与测试函数，根据__name__变量的值来进行判断是否运行test方法
[huawei@n148 pytest]$ cat hello.py 
#!/usr/bin/python3
def hello(): 
        print("Hello, world!") 
def test(): 
        hello() 

print(__name__)
if __name__ == '__main__': test() 

下面是main代码
[huawei@n148 pytest]$ cat pyth.py 
#!/usr/bin/python3
import hello;
hello.hello()

执行模块自身则会调用test
[huawei@n148 pytest]$ python3 hello.py
__main__
Hello, world!

执行main代码则不触发test
[huawei@n148 pytest]$ python3 pyth.py 
hello
```
## 包
- 包是一个目录，目录内必须包含文件__init__.py
- 如果像普通模块一样导入包，文件__init__.py的内容就将是包的内容
- 要将模块加入包中，只需将模块文件放在包目录中即可
- 包中可以嵌套其他包，即目录可以多层，如下
	- ~/python/ PYTHONPATH中的目录
	- ~/python/drawing/ 包目录（包drawing）
	- ~/python/drawing/__init__.py 包代码（模块drawing）
	- ~/python/drawing/colors.py 模块colors
	- ~/python/drawing/shapes.py 模块shapes
```
	完成这些准备工作后，下面的语句都是合法的：
	import drawing # (1) 导入drawing包
	import drawing.colors # (2) 导入drawing包中的模块colors 
	from drawing import shapes # (3) 导入模块shapes
```

# unittest

## 测试函数
```
定义一个方法
[huawei@n148 pytest]$ cat name_function.py 
#!/usr/bin/python3
def get_formatted_name(first, last, middle=''):
	if middle:
		full_name = f"{first} {middle} {last}"
	else:
		full_name = f"{first} {last}"
	return full_name.title()



下面是测试代码
[huawei@n148 pytest]$ cat test_name_function.py 
import unittest
from name_function import get_formatted_name

class NamesTestCase(unittest.TestCase):
	def test_first_last_name(self):
		formatted_name = get_formatted_name('janis', 'joplin')
		self.assertEqual(formatted_name, 'Janis Joplin')
	def test_first_last_middle_name(self):
		formatted_name = get_formatted_name('wolfgang', 'mozart', 'amadeus')
		self.assertEqual(formatted_name, 'Wolfgang Amadeus Mozart')

if __name__ == '__main__':
	unittest.main()


运行结果
[huawei@n148 pytest]$ python3 test_name_function.py 
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```
## unittest的setUp和tearDown

方法setUp和tearDown，它们将分别在每个测试方法之前和之后执行。可使用这些方法来执行适用于所有测试的初始化代码和清理代码

## 测试类


```
[huawei@n148 pytest]$ cat survey.py 
#!/usr/bin/python3
class AnonymousSurvey:
        def __init__(self, question):
                self.question = question
                self.responses = []
        def show_question(self):
                print(self.question)
        def store_response(self, new_response):
                self.responses.append(new_response)
        def show_results(self):
                print("Survey results:")
                for response in self.responses:
                        print(f"- {response}")


[huawei@n148 pytest]$ cat test_survey.py 
import unittest
from survey import AnonymousSurvey
class TestAnonymousSurvey(unittest.TestCase):
        def setUp(self):
                question = "What language did you first learn to speak?"
                self.my_survey = AnonymousSurvey(question)
                self.responses = ['English', 'Spanish', 'Mandarin']
        def test_store_single_response(self):
                self.my_survey.store_response(self.responses[0])
                self.assertIn(self.responses[0], self.my_survey.responses)
        def test_store_three_responses(self):
                for response in self.responses:
                        self.my_survey.store_response(response)
                for response in self.responses:
                        self.assertIn(response, self.my_survey.responses)

if __name__ == '__main__':
        unittest.main()


[huawei@n148 pytest]$ python3 test_survey.py 
..
----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK
```
## 测试的输出
运行测试用例时，每完成一个单元测试，Python都打印一个字符
- 测试通过时打印一个句点
- 测试引发错误时打印一个E
- 测试导致断言失败时则打印一个F
# 文件
## open模式

open()的模式如下，如果省略，Python将以默认的只读模式打开文件。
- 读取模式 （'r' ）
- 写入模式 （'w' ）
- 附加模式 （'a' ）
- 读写模式 （'r+' ）
- 'b' 二进制模式（与其他模式结合使用）
- 't' 文本模式（默认值，与其他模式结合使用）

## 一次读入所有
```
#!/usr/bin/python3
with open('pi_digits.txt') as file_object:
	contents = file_object.read()
print(contents.rstrip())
```
## 读取所有行
```
#!/usr/bin/python3
with open('pi_digits.txt') as file_object:
    lines = file_object.readlines()
for line in lines:
	print(line.rstrip())
```
## 读取指定字节
```
with open('pi_digits.txt') as file_object:
	contents = file_object.read(5)
print(contents.rstrip())

[huawei@n148 pytest]$ cat alice.txt | python3 pyth.py
3.141
```
## 每次读一个字符或字节
读取二进制文件即为字节~
```
with open(filename) as f: 
	while True: 
		char = f.read(1) 
		if not char: break 
		print(char) 
```
也可以一次读取，遍历字符
```
with open(filename) as f: 
	for char in f.read(): 
 		process(char) 
```
## 每次读一行
```
filename = 'username.json';
with open(filename) as f: 
	while True: 
		line = f.readline() 
		if not line: break 
		print(line) 
```
也可以一次读取到字符串数组，然后迭代此数组
```
with open(filename) as f: 
 	for line in f.readlines(): 
		process(line) 
```

## 连接文件所有行
使用strip去除每行的两端空白，然后相连，办法感觉很繁琐
```
with open('pi_digits.txt') as file_object:
    lines = file_object.readlines()
pi_string = ''
for line in lines:
	pi_string += line.strip()
print(pi_string)
```
## 写入与追加
```
#!/usr/bin/python3
filename = 'programming.txt'
with open(filename, 'w') as file_object:
	file_object.write("I love programming.\n")
	file_object.write("I love creating new games.\n")


with open(filename, 'a') as file_object:
	file_object.write("I also love finding meaning in large datasets.\n")
	file_object.write("I love creating apps that can run in a browser.\n")

[huawei@n148 pythontest]$ cat programming.txt 
I love programming.
I love creating new games.
I also love finding meaning in large datasets.
I love creating apps that can run in a browser.
```
## 读取后改再写回
```
#!/usr/bin/python3
fname = 'username.json';
f = open(fname) 
lines = f.readlines()
f.close() 
lines[0] = "new test" 
f = open(fname, 'w') 
f.writelines(lines) 
f.close() 
```

## json
写json
```
#!/usr/bin/python3
import json
numbers = [2, 3, 5, 7, 11, 13]
filename = 'numbers.json'
with open(filename, 'w') as f:
	json.dump(numbers, f)
```
读json
```
#!/usr/bin/python3
import json
filename = 'numbers.json'
numbers = []
with open(filename) as f:
	numbers = json.load(f)
print(numbers)
```
读写案例  
没有记录则写文件，有记录则读文件并展示
```
#!/usr/bin/python3

import json
def get_stored_username():
	filename = 'username.json'
	try:
		with open(filename) as f:
			username = json.load(f)
	except FileNotFoundError:
		return None
	else:
		return username

def get_new_username():
	username = input("What is your name? ")
	filename = 'username.json'
	with open(filename, 'w') as f:
		json.dump(username, f)
	return username

def greet_user():
	username = get_stored_username()
	if username:
		print(f"Welcome back, {username}!")
	else:
		username = get_new_username()
		print(f"We'll remember you when you come back, {username}!")

greet_user()
```
# 管道
## 简单使用
依然是使用管道符号进行操作，python从stdin中进行读取
```
import sys 
text = sys.stdin.read() 
words = text.split() 
wordcount = len(words) 
print('Wordcount:', wordcount) 

[huawei@n148 pytest]$ cat alice.txt | python3 pyth.py
Wordcount: 29465
```
也可以迭代stdin
```
import sys 
for line in sys.stdin: 
	process(line) 
```
# 类
## 构造函数 __init__
```
class Dog:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	def sit(self):
 		print(f"{self.name} is now sitting.")
	def roll_over(self):
		print(f"{self.name} rolled over!")

my_dog = Dog('Willie', 6)
your_dog = Dog('Lucy', 3)
print(f"My dog's name is {my_dog.name}.")
print(f"My dog is {my_dog.age} years old.")
my_dog.sit()
print(f"\nYour dog's name is {your_dog.name}.")
print(f"Your dog is {your_dog.age} years old.")
your_dog.sit()

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
My dog's name is Willie.
My dog is 6 years old.
Willie is now sitting.

Your dog's name is Lucy.
Your dog is 3 years old.
Lucy is now sitting.
```
参数也可以有默认值
```
class FooBar: 
	def __init__(self, v = 1): 
		self.somevar = v

f = FooBar("aaaaaaaaaaaaaaa")  调用可以传递参数
print(f.somevar)
```

## 析构函数 __del__
- 函数名__del__，通常无需手动调用
## 修改成员变量值
- 直接修改属性的值，即直接通过对象进行赋值，如 my_new_car.odometer_reading = 23
- 封装成员方法更改属性值

## 私有方法
```
class Secretive: 
	def __inaccessible(self): 
		print("Bet you can't see me ...") 
	def accessible(self): 
		print("The secret message is:") 
		self.__inaccessible() 

s = Secretive() 
s.accessible()
s.__inaccessible()	不能调用私有方法，会失败
```
## 函数property
## 静态方法和类方法
- 静态方法貌似全局的static
- 类方法貌似类的static
- @名为装饰器
```
class MyClass: 
	@staticmethod 
	def smeth(): 
 		print('This is a static method') 
	@classmethod 
	def cmeth(cls): 
		print('This is a class method of', cls) 
  
MyClass.smeth() 
MyClass.cmeth()

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
This is a static method
This is a class method of <class '__main__.MyClass'>
```
# 继承
## 简单继承
```
class A: 
	def hello(self): 
		print("Hello, I'm A.") 
class B(A): 
	pass

a = A() 
b = B() 
a.hello() 
b.hello() 

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Hello, I'm A.
Hello, I'm A.
```
调用父类构造函数，添加子类新属性与方法
```

```
## 重写普通方法
```
class A: 
	def hello(self): 
		print("Hello, I'm A.") 
class B(A): 
	def hello(self): 
 		print("Hello, I'm B.") 

a = A() 
b = B() 
a.hello() 
b.hello() 

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Hello, I'm A.
Hello, I'm B.
```
## 调用父类方法
注意没有super()那句则会失败，因为子类重新实现了自己的构造，且未调用父类构造，所以没有对应的成员hungry
```
class Bird: 
	def __init__(self): 
		self.hungry = True 
	def eat(self): 
		if self.hungry: 
 			print('Aaaah ...') 
 			self.hungry = False 
		else:
 			print('No, thanks!') 
    
class SongBird(Bird): 
	def __init__(self): 
		super().__init__()
		self.sound = 'Squawk!' 
	def sing(self): 
		print(self.sound)

sb = SongBird() 
sb.sing() 
sb.eat() 
sb.eat() 

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Squawk!
Aaaah ...
No, thanks!
```

## 组合
案例演示了组合类的使用方式，汽车父类、电动车子类，并且电动车类组合了电池类
```
#!/usr/bin/python3

class Car:
	def __init__(self, make, model, year):
		self.make = make
		self.model = model
		self.year = year
		self.odometer_reading = 0

	def get_descriptive_name(self):
		long_name = f"{self.year} {self.make} {self.model}"
		return long_name.title()
	def read_odometer(self):
		print(f"This car has {self.odometer_reading} miles on it.")
	def update_odometer(self, mileage):
		if mileage >= self.odometer_reading:
			self.odometer_reading = mileage
		else:
			print("You can't roll back an odometer!")
	def increment_odometer(self, miles):
		self.odometer_reading += miles

class Battery:
	def __init__(self, battery_size=75):
		self.battery_size = battery_size
	def describe_battery(self):
		print(f"This car has a {self.battery_size}-kWh battery.")
	def get_range(self):
		if self.battery_size == 75:
			range = 260
		elif self.battery_size == 100:
			range = 315
		print(f"This car can go about {range} miles on a full charge.")


class ElectricCar(Car):
	def __init__(self, make, model, year):
		super().__init__(make, model, year)
		self.battery = Battery()
	def describe_battery(self):
		print(f"This car has a {self.battery_size}-kWh battery.")


my_tesla = ElectricCar('tesla', 'model s', 2019)
print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
my_tesla.battery.get_range()

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
2019 Tesla Model S
This car has a 75-kWh battery.
This car can go about 260 miles on a full charge.

```

# 异常处理

## 抛出异常
- 使用raise语句，并将一个类（必须是Exception的子类）或实例作为参数。
- 将类作为参数时，将自动创建一个实例，捕获到的即是此对象
```
raise Exception('hyperdrive overload') 
也可不指定类型，那样下面的信息就会减少一些


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Traceback (most recent call last):
  File "/home/huawei/playground/pythontest/pyth.py", line 2, in <module>
    raise Exception('hyperdrive overload') 
Exception: hyperdrive overload
```
## 异常类型
见python基础教程第三版p133
## 自定义的异常类
继承自Exception

class SomeCustomException(Exception): pass 
## try、except、else、finally
else是未触发异常的路径
```
#!/usr/bin/python3
filename = 'alice.txt'
try:
	with open(filename, encoding='utf-8') as f:
		contents = f.read()
except FileNotFoundError:
	print(f"Sorry, the file {filename} does not exist.")
else:
	print("loaded")

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Sorry, the file alice.txt does not exist.
```
也可以有多个捕获
```
try: 
 	x = int(input('Enter the first number: ')) 
	y = int(input('Enter the second number: ')) 
	print(x / y) 
except ZeroDivisionError: 
	print("The second number can't be zero!") 
except TypeError: 
	print("That wasn't a number, was it?") 
```
这样更精简
```
try: 
	x = int(input('Enter the first number: ')) 
	y = int(input('Enter the second number: ')) 
	print(x / y) 
except (ZeroDivisionError, TypeError, NameError): 
 	print('Your numbers were bogus ...') 
```
带有finally
```
#!/usr/bin/python3
try: 
	1 / 0 
except NameError: 
	print("Unknown variable") 
else: 
	print("That went well!") 
finally: 
	print("Cleaning up.") 
```
## 捕获对象
下面的e即是异常对象
```
try: 
	x = int(input('Enter the first number: ')) 
	y = int(input('Enter the second number: ')) 
	print(x / y) 
except (ZeroDivisionError, TypeError) as e: 
	print(e) 
```
## 捕获所有
- 在except语句中不指定任何异常类即可
- 更好的选择是使用except Exception as e并对异常对象进行检查。这样做将让不是从Exception派生而来的为数不多的异常成为漏网之鱼，其中包括SystemExit和KeyboardInterrupt，因为它们是从BaseException（Exception的超类）派生而来的。

```
try: 
	x = int(input('Enter the first number: ')) 
	y = int(input('Enter the second number: ')) 
	print(x / y) 
except: 
	print('Something wrong happened ...') 
```