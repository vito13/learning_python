---
阅读进度
Python编程：从入门到实践（第2版）		继续第12章，后面都是东拼西凑先不用看了

python基础教程（第三版）				继续第12章，后面都是东拼西凑先不用看了

python语言及其应用						继续第11章，后面都是东拼西凑先不用看了

流畅的Python							继续第16章（暂未看10-13）

Python Cookbook（第3版）

看漫画学Python							继续第11.3.3章
---
# 基础知识

> Python 最底层的基本数据类型：布尔型、整型、浮点型以及字符串型。

## 数据类型
- 在Python中所有的数据类型都是类，每个数据值都是类的“实例”。
- 在Python中有6种主要的内置数据类型：数字、字符串、列表、元组、集合和字典。
- 列表、元组、集合和字典可以容纳多项数据，统称为容器类型的数据。
- Python中的数字类型有4种：整数类型、浮点类型、复数类型和布尔类型。需要注意的是，布尔类型也是数字类型，它事实上是整数类型的一种。

如果把最底层的基本数据类型看作组成 Python 的原子，数据结构就像分子一样。在编程中，最常见的工作就是将数据进行拆分或合并，将其加工为特定的形式，而数据结构就是用以切分数据的钢锯以及合并数据的粘合枪。
## 变量
- 为了理解 Python 中的赋值语句，应该始终先读右边。对象在右边创建或获取，在此之后左边的变量才会绑定到对象上，这就像为对象贴上标注。因为变量只不过是标注，所以无法阻止为对象贴上多个标注。贴的多个标注，就是别名。
- 每个变量都有标识、类型和值。对象一旦创建，它的标识绝不会变；你可以把标识理解为对象在内存中的地址。is 运算符比较两个对象的标识；id() 函数返回对象标识的整数表示。


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
- 变量可以在模块中创建，作用域（变量的有效范围）是整个模块，被称为全局变量。
- 变量也可以在函数中创建，在默认情况下作用域是整个函数，被称为局部变量。

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
- Python不要求声明变量，但是假定在函数定义体中赋值的变量是局部变量，下个案例会err
```
b = 6
def f3(a):
	# global b		没有这行会认为b是下面的b，是未定义的局部变量
	print(a)
	print(b)
	b = 9

f3(3)
```
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


## range自然数序列
- range() 函数的用法类似于使用切片
- range(start，stop，step)
- start 的默认值为 0。唯一要求的参数值是 stop，产生的最后一个数的值是 stop 的前一个
- step 的默认值是1。当然，也可以反向创建自然数序列，这时 step 的值为 -1。
```
如：
list( range(0, 11, 2) )
for x in range(2, -1, -1):
for x in range(0,3):
list( range(0, 3) )
```

## 全局变量

函数内部使用global声明一下即可
```
animal = 'fruitbat'
def change_and_print_global():
	global animal
	animal = 'wombat'
	print('inside change_and_print_global:', animal)

print(animal)
change_and_print_global()
print(animal)

[huawei@n148 postdb_doc]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py"
fruitbat
('inside change_and_print_global:', 'wombat')
wombat
```

## 命名空间

Python 提供了两个获取命名空间内容的函数：
- locals() 返回一个局部命名空间内容的字典；
- globals() 返回一个全局命名空间内容的字典。

```
animal = 'fruitbat'
def change_local():
	animal = 'wombat'
	print('locals:',locals())


print(animal)
change_local()
print('globals:', globals())
print(animal)

[huawei@n148 postdb_doc]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py"
fruitbat
('locals:', {'animal': 'wombat'})
('globals:', {'__builtins__': <module '__builtin__' (built-in)>, '__file__': '/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py', '__package__': None, 'change_local': <function change_local at 0x7f9b8b392758>, 'animal': 'fruitbat', '__name__': '__main__', '__doc__': None})
fruitbat
```
# 命令行

## 参数sys.argv
是个列表
```
import sys
print('Program arguments:',sys.argv)

[huawei@n148 pltest]$ python3 pyth.py 
Program arguments: ['pyth.py']
[huawei@n148 pltest]$ python3 pyth.py  tra la la
Program arguments: ['pyth.py', 'tra', 'la', 'la']
[huawei@n148 postdb_doc]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py"
('Program arguments:', ['/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py'])
[huawei@n148 postdb_doc]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py" tra la la
('Program arguments:', ['/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py', 'tra', 'la', 'la'])
[huawei@n148 postdb_doc]$ 
```
# 序列的分类

## 扁平序列
是一段连续的内存空间。存放如字符、字节和数值这种基础类型，存储的是值而不是引用。体积更小、速度更快而且用起来更简单，但是它只能保存一些原子性的数据，比如数字、字符和字节。扁平序列因为只能包含原子数据类型，比如整数、浮点数或字符，所以不能嵌套使用。

- str
- bytes
- bytearray
- memoryview
- array.array

## 容器序列
可以存放任意类型的对象的引用。容器序列则比较灵活，但是当容器序列遇到可变对象时，用户就需要格外小心了，因为这种组合时常会搞出一些“意外”，特别是带嵌套的数据结构出现时，用户要多费一些心思来保证代码的正确。


- list
- tuple
- collections.deque

## 非容器序列
- 映射关系的容器dict
- 只有key的容器set
## 可变序列

list、bytearray、array.array、collections.deque 和 memoryview。

## 不可变序列

tuple、str 和 bytes。


# 推导和生成器表达式
列表推导和生成器表达式则提供了灵活构建和初始化序列的方式，这两个工具都异常强大。
## 列表推导
## 字典推导
将元祖的列表推导为字典
```
DIAL_CODES = [
	(86, 'China'),
	(91, 'India'),
	(1, 'United States'),
	(62, 'Indonesia'),
	(55, 'Brazil'),
	(92, 'Pakistan'),
	(880, 'Bangladesh'),
	(234, 'Nigeria'),
	(7, 'Russia'),
	(81, 'Japan'),
]

# 迭代列表，将item拆包为code与country，并使用此2构建字典
country_code = {country: code for code, country in DIAL_CODES}
print(country_code)
country_code = {code: country.upper() for country, code in country_code.items() if code < 66}
print(country_code)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
{'China': 86, 'India': 91, 'United States': 1, 'Indonesia': 62, 'Brazil': 55, 'Pakistan': 92, 'Bangladesh': 880, 'Nigeria': 234, 'Russia': 7, 'Japan': 81}
{1: 'UNITED STATES', 62: 'INDONESIA', 55: 'BRAZIL', 7: 'RUSSIA'}
```

## 集合推导
```
一个Latin-1 字符集合，该集合里的每个字符的 Unicode 名字里都有“SIGN”这个单词
# 从 unicodedata 模块里导入 name 函数，用以获取字符的名字。
from unicodedata import name
# 把编码在 32~255 之间的字符的名字里有“SIGN”单词的挑出来，放到一个集合里
s = {chr(i) for i in range(32, 256) if 'SIGN' in name(chr(i),'')}
print(s)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
{'®', '§', '±', '<', '%', '°', '©', '¥', '¶', '+', '¤', '#', '¬', '÷', '$', '=', '£', '>', '¢', 'µ', '×'}
```

# 字符串 str
- 字符组成的序列
- 字符串是不可变的，因此所有的元素赋值和切片赋值都是非法的。
- 多行的使用三个单引号
- Python3中的字符串中的字符使用Unicode编码方式，不是字节数组

## 三种表示方式
字符串有三种表示方式：
- 普通字符串  
普通字符串指用单引号（'）或双引号（＂）括起来的字符串。转义字符起作用。

 
- 原始字符串 raw string  
用r前缀的字符串内容不会转义
```
s2=r"hello\nworld"
print(s2)

[huawei@n161 ccc]$ python3 1.py
hello\nworld
```

- 长字符串  
使用3个引号（单双都可以）包围的字符串，会包含换行、排版、缩进等


还有图标的，见下例最后。
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
## 行连接符 \
```

alphabet = 'abcdefg' + \
'hijklmnop' + \
'qrstuv' + \
'wxyz'

print(alphabet)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
abcdefghijklmnopqrstuvwxyz
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
## str转int、float
```
print(int('80'))
print(float('80.0'))
print(int('AB', 16))	# 指定16进制可以转换
# print(int('AB'))	# 默认将参数进行十进制转换，会失败
# print(int('80.0'))	# 参数非十进制，浮点也失败

[huawei@n161 ccc]$ python3 1.py
80
80.0
171
```

## int、float、bool转str

```
print(str(321))
print(str(123.321))
print(str(True))

[huawei@n161 ccc]$ python3 1.py
321
123.321
True
```
## 字符数量 len
字符串函数 len 可以计算字符串中 Unicode 字符的个数，而不是字节数

```
letters = 'abcdefghijklmnopqrstuvwxyz'
print(len(letters))
```

## 字节数量
取字节数见编码encode案例
## 判断开头、结尾
```
letters = 'abcdefghijklmnopqrstuvwxyz'
print(letters.startswith('abc'))
print(letters.endswith('abc'))
[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
True
False
```
获取指定扩展名文件列表
```
filenames = [ 'Makefile', 'foo.c', 'bar.py', 'spam.c', 'spam.h' ] 
print([name for name in filenames if name.endswith(('.c', '.h')) ])

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
['foo.c', 'spam.c', 'spam.h']
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

详细居左保留数位等参加python语言及其应用7.1.2 格式化

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


## 编码 encode
- 字符的标识，即码位，是 0~1 114 111 的数字（十进制），在 Unicode 标准中以 4~6 个十六进制数字表示，而且加前缀“U+”。约 10% 的有效码位有对应的字符。
- 字符的具体表述取决于所用的编码（如utf8）。编码是在码位和字节序列之间转换时使用的算法。
- 编码是将码位转换成字节序列的过程
- encode支持第二个参数用于指定当目标编码无此字符时是异常还是忽略的操作

	如果你想要使用 ascii 方式进行编码，必须保证待编码的字符串仅包含 ASCII 字符集里的字符，不含有任何其他的 Unicode 字符，否则会出现错误
- 尽可能统一使用 UTF-8 编码。出错率低，兼容性好，可以表达所有的 Unicode 字符，编码和解码的速度又快
- 可以把字节序列想成晦涩难懂的机器磁芯转储，把 Unicode 字符串想成“人类可读”的文本。那么，把字节序列变成人类可读的文本字符串就是解码，而把字符串变成用于存储或传输的字节序列就是编码。

```
snowman = '\u2603'	# 将Unicode 字符串 '\u2603' 赋值给 snowman。
print(snowman)
print(len(snowman))	# snowman 是一个仅包含一个字符的 Unicode 字符串，这与它存储所需的字节数没有任何关系
ds = snowman.encode('utf-8')	# 将Unicode字符编码为字节序列。UTF-8 是一种变长编码方式，ds是一个bytes类型的变量
print(len(ds))	# 占用了 3 字节的空间，注意不是所有单个 Unicode字符都是3
print(ds)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
☃
1
3
b'\xe2\x98\x83'
```
## 解码 decode

- 解码是将字节序列转换成码位的过程
```
place = 'caf\u00e9'	# unicode字符串
print(place)
print(len(place))
print(type(place))
place_bytes = place.encode('utf-8')	# 将它以 UTF-8 格式编码为 bytes 型变量
print(place_bytes)
print(len(place_bytes))
print(type(place_bytes))
place2 = place_bytes.decode('utf-8') # 再解回来
print(place2)
print(len(place2))
print(type(place2))

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
café
4
<class 'str'>
b'caf\xc3\xa9'
5
<class 'bytes'>
café
4
<class 'str'>
```
## 统一字符编码侦测包 Chardet
能识别所支持的 30 种编码 https://pypi.python.org/pypi/chardet

# 列表【】 list
- 列表非常适合利用顺序和位置定位某一元素
- 列表元素是可变的
- 使用中括号定义
- 在列表中，具有相同值的元素允许出现多次
- 可以同时容纳不同类型的元素，但是实际上这样做并没有什么特别的好处，比如不能对列表进行排序。元组则恰恰相反，它经常用来存放不同类型的的元素。这也符合它的本质，元组就是用作存放彼此之间没有关系的数据的记录。


## 创建与访问元素
### 手动初始化数据
- [元素1，元素2，元素3，⋯]：指定具体的列表元素，元素之间以逗号分隔，列表元素需要使用中括号括起来。
- 索引-1指向最后一个，-2则是倒数第二个，以此类推
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
使用list(iterable)将其他数据类型转换成列表，函数的参数iterable是可迭代对象（字符串、列表、元组、集合和字典等）。

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
- 使用切片方式[:]与list方法得到的也哟可能还是浅拷贝，取决于列表是否嵌套
- 使用copy、deepcopy进行深拷贝解决问题
```
#!/usr/bin/python3
my_foods = ['pizza', 'falafel', 'carrot cake']

方法1有可能还是浅拷贝：	friend_foods = my_foods[:]
方法2：	friend_foods = my_foods.copy()
方法3有可能还是浅拷贝：	friend_foods = list(my_foods)

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
- 参数reverse为t是降序，默认f
- 还支持一个key回调用于自定义比较方法
```

fruits = ['grape', 'raspberry', 'apple', 'banana']
print(sorted(fruits))
print(fruits)
print(sorted(fruits, reverse=True))
print(sorted(fruits, key=len))	此处使用长度进行排序
print(sorted(fruits, key=len, reverse=True))
print(fruits)
fruits.sort()
print(fruits)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
['apple', 'banana', 'grape', 'raspberry']
['grape', 'raspberry', 'apple', 'banana']
['raspberry', 'grape', 'banana', 'apple']
['grape', 'apple', 'banana', 'raspberry']
['raspberry', 'banana', 'grape', 'apple']
['grape', 'raspberry', 'apple', 'banana']
['apple', 'banana', 'grape', 'raspberry']
```
## 颠倒 reversed
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
## 成员测试 in、not in
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
- 如果赋值的对象是一个切片，那么赋值语句的右侧必须是个可迭代对象。
- 即便只有单独一个值，也要把它转换成可迭代的序列。
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
- 便于同时迭代n个列表
- 返回由元组组成的可迭代序列
- 可使用list将其转换为列表
- 可使用dict将其转换为字典

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
```
english = 'Monday', 'Tuesday', 'Wednesday'
french = 'Lundi', 'Mardi', 'Mercredi'
print(list(zip(english, french)))
print(dict(zip(english, french)))

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pytest/pyth.py"
[('Monday', 'Lundi'), ('Tuesday', 'Mardi'), ('Wednesday', 'Mercredi')]
{'Monday': 'Lundi', 'Tuesday': 'Mardi', 'Wednesday': 'Mercredi'}
```
# 元组 ( ) tuple
- 元组经常用来存放不同类型的的元素。这也符合它的本质，元组就是用作存放彼此之间没有关系的数据的记录。
- 与列表类似，元组也是由任意类型元素组成的序列。
- 与列表不同的是，元组是不可变的，这意味着一旦元组被定义，将无法再进行增加、删除或修改元素等操作。因此，元组就像是一个常量列表。
- 不要把可变对象放在元组里面。
- 使用圆括号定义
- 空元组用两个不包含任何内容的圆括号表示
- 一个值的元组要有逗号
- 元组的切片还是元组
- 元组占用的空间较小
- 可以将元组用作字典的键
- 函数的参数是以元组形式传递的
- 命名元组可以作为对象的替代
- 元组与多数 Python 集合（列表、字典、集，等等）一样，保存的是对象的引用。

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
（元素1，元素2，元素3，⋯）：指定具体的元组元素，元素之间以逗号分隔。对于元组元素，可以使用小括号括起来，也可以省略小括号。

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
## 打印元素
```
lax_coordinates = (33.9425, -118.408056)
city, year, pop, chg, area = ('Tokyo', 2003, 32450, 0.66, 8014)
traveler_ids = [('USA', '31195855'), ('BRA', 'CE342567'), ('ESP', 'XDA205856')]
for passport in sorted(traveler_ids):
	print('%s/%s' % passport)		# passport代表每个元组, %能匹配到对应的元组元素上
for country, _ in traveler_ids:		# 元祖拆包后的第二个元素没有，用占位符代替
	print(country)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
BRA/CE342567
ESP/XDA205856
USA/31195855
USA
BRA
ESP
```

## 拆包
可认为创建元祖为打包，反操作即为拆包。将元祖解包，并将得到的值存储到一系列变量中。可用于  
- 并行赋值
- 交换变量值
- 将序列赋值给元祖values
- 解开元祖到多个变量
- 使用*接收多个值到列表中，*句法让元组拆包的便利性更上一层楼，让用户可以选择性忽略不需要的字段
- 函数参数传递（主要是上一种方式）
- 函数可以用元组的形式返回多个值

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

## 拆包嵌套元组

```
metro_areas = [
	('Tokyo','JP',36.933,(35.689722,139.691667)),
	('Delhi NCR', 'IN', 21.935, (28.613889, 77.208889)),
	('Mexico City', 'MX', 20.142, (19.433333, -99.133333)),
	('New York-Newark', 'US', 20.104, (40.808611, -74.020386)),
	('Sao Paulo', 'BR', 19.649, (-23.547778, -46.635833)),
]
print('{:15} | {:^9} | {:^9}'.format('', 'lat.', 'long.'))
fmt = '{:15} | {:9.4f} | {:9.4f}'
for name, cc, pop, (latitude, longitude) in metro_areas:
	if longitude <= 0:
		print(fmt.format(name, latitude, longitude))

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
                |   lat.    |   long.  
Mexico City     |   19.4333 |  -99.1333
New York-Newark |   40.8086 |  -74.0204
Sao Paulo       |  -23.5478 |  -46.6358

```
## 使用tuple()创建元组

函数tuple的工作原理与list很像：它将一个序列（字符串、列表、元组、集合和字典等）作为参数，并将其转换为元组。如果参数
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
## 具名元祖 namedtuple
- 命名元组是元组的子类，既可以通过名称（使用 .name）来访问其中的值，也可以通过位置进行访问（使用[offset]）
- 它无论看起来还是使用起来都和不可变对象非常相似
- 具名元组的实例也很节省空间，与使用对象相比，使用命名元组在时间和空间上效率更高。
- 可以使用点号（.）对特性进行访问，而不需要使用字典风格的方括号
- 可以把它作为字典的键
- 用以构建只有少数属性但是没有方法的对象

简单使用
```
from collections import namedtuple
Duck = namedtuple('Duck', 'bill tail')
duck = Duck('wide orange', 'long')
print(duck)
print(duck.bill)
print(duck.tail)

parts = {'bill': 'wide orange', 'tail': 'long'} # 用字典来构造命名元组
duck2 = Duck(**parts) # **作用是将 parts 字典中的键和值抽取出来作为参数提供给 Duck() 使用。等同于 duck2 = Duck(bill = 'wide orange', tail = 'long')
print(duck2)
duck3 = duck2._replace(tail='magnificent', bill='crushing')	# 命名元组是不可变的，但可以替换其中某些域的值并返回一个新的命名元组
print(duck3)


duck_dict = {'bill': 'wide orange', 'tail': 'long'}
print(duck_dict)
duck_dict['color'] = 'green'	# 可以向字典里添加新的键值对
print(duck_dict)

duck.color = 'green'	# err 但无法对命名元组这么做

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
Duck(bill='wide orange', tail='long')
wide orange
long
Duck(bill='wide orange', tail='long')
Duck(bill='crushing', tail='magnificent')
{'bill': 'wide orange', 'tail': 'long'}
{'bill': 'wide orange', 'tail': 'long', 'color': 'green'}
Traceback (most recent call last):
  File "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py", line 22, in <module>
    duck.color = 'green'        # 但无法对命名元组这么做
AttributeError: 'Duck' object has no attribute 'color'
```


高级使用，类似struct，可以快速定义结构并创建变量，但仅有属性不能有方法
- _fields
- _make()
- _asdict()

```
from collections import namedtuple
City = namedtuple('City', 'name country population coordinates')	# 参数是类名，另一个是类的各个字段的名字
tokyo = City('Tokyo', 'JP', 36.933, (35.689722, 139.691667))	# 创建对象
print(tokyo)	# 访问
print(tokyo.population)
print(tokyo.coordinates)
print(tokyo[1])
print(City._fields)	# _fields 属性是一个包含这个类所有字段名称的元组。


LatLong = namedtuple('LatLong', 'lat long')
delhi_data = ('Delhi NCR', 'IN', 21.935, LatLong(28.613889, 77.208889))
delhi = City._make(delhi_data)	# 用_make()通过接受一个可迭代对象来生成这个类的一个实例，它的作用跟City(*delhi_data)是一样的

print(delhi._asdict())	#_asdict()把具名元组以collections.OrderedDict的形式返回，下面是迭代每一项
for key, value in delhi._asdict().items():
	print(key + ':', value)



[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
City(name='Tokyo', country='JP', population=36.933, coordinates=(35.689722, 139.691667))
36.933
(35.689722, 139.691667)
JP
('name', 'country', 'population', 'coordinates')
OrderedDict([('name', 'Delhi NCR'), ('country', 'IN'), ('population', 21.935), ('coordinates', LatLong(lat=28.613889, long=77.208889))])
name: Delhi NCR
country: IN
population: 21.935
coordinates: LatLong(lat=28.613889, long=77.208889)
```
## 元组的相对不可变性
- 下面的描述貌似眼熟，详见代码说明，感觉就像是改变常量指针指向的内容。。。
- 元组与多数 Python 集合（列表、字典、集，等等）一样，保存的是对象的引用。1 如果引用的元素是可变的，即便元组本身不可变，元素依然可变。
```
t1 = (1, 2, [30, 40])
t2 = (1, 2, [30, 40])
print(t1 == t2)		# 虽然 t1 和 t2 是不同的对象，但是二者相等，因为==比值
print(id(t1[-1]))
t1[-1].append(99)	# 重点在此，t1 不可变，但是 t1[-1] 可变。即t1[-1] 的标识没变，只是值变了。（可以理解为栈上的指针没指向别处，但是堆上的数据变了）
print(t1)
print(id(t1[-1]))
print(t1 == t2)

[huawei@n161 aaa]$ python3 test.py 
True
140324783818056
(1, 2, [30, 40, 99])
140324783818056
False
```


# 字典 { } dict
- 字典由键及其相应的值组成，这种键值对称为项（item）。
- 每个键与其值之间都用冒号（:）分隔，项之间用逗号分隔，而整个字典放在花括号内。
- 空字典（没有任何项）用两个花括号表示，类似于下面这样：{}。
- 在字典（以及其他映射类型）中，键必须是独一无二的，而字典中的值无需如此。
- 字典的键必须为不可变对象，因此列表、字典以及集合都不能作为字典的键，但元组可以作为字典的键
- 字典是Python中唯一的内置映射类型，其中的值不按顺序排列，而是存储在键下。键可能是数、字符串或元组（即k得是不可变的类型）。
- 所有的字典方法见流程的python3.3
## 构建方法
- 使用dict方法
- {key1：value1，key2：value2，...，key_n：value_n}：指定具体的字典键值对，键值对之间以逗号分隔，最后用大括号括起来。
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
- 集合（set）是一种可迭代的、无序的、不能包含重复元素的容器类型的数据。
- 尽管都由花括号包裹，集合仅仅是一系列值组成的序列，而字典是一个或多个键值对组成的序列。
- 所有方法见流程的python3.8.3
  
## 创建
- {元素1，元素2，元素3，⋯}：指定具体的集合元素，元素之间以逗号分隔。对于集合元素，需要使用大括号括起来。
- 使用set()创建空集合
- 使用set(iterable)将其他类型转换为集合，参数iterable是可迭代对象（字符串、列表、元组、集合和字典等）。
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
## 交集、并集
给定两个集合 a 和 b，a | b 返回的是它们的合集，a & b 得到的是交集，而 a - b 得到的是差集
https://blog.csdn.net/wenhao_ir/article/details/125424671
## 差集
a-b得到的是差集

```
计算差集，然后排序，得到类的实例没有而函数有的属性列表

class C: pass
obj = C()
def func(): pass
print(sorted(set(dir(func)) - set(dir(obj))))


[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
['__annotations__', '__call__', '__closure__', '__code__', '__defaults__', '__get__', '__globals__', '__kwdefaults__', '__name__', '__qualname__']
```
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
- 简单的使用
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
- 相对复杂一点的

两种方式结果相同
```
方式1
board = [['_'] * 3 for i in range(3)]
print(board)
board[1][2] = 'X'
print(board)

方式2
board = []
for i in range(3):
	row=['_'] * 3
	board.append(row)
print(board)
board[2][0] = 'X'
print(board)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
[['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]
[['_', '_', '_'], ['_', '_', 'X'], ['_', '_', '_']]


[['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]
[['_', '_', '_'], ['_', '_', '_'], ['X', '_', '_']]

```
错误的赋值演示
```
weird_board = [['_'] * 3] * 3	# weird_board包含 3 个指向同一个列表的引用
print(weird_board)
weird_board[1][2] = 'O'
print(weird_board)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
[['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]
[['_', '_', 'O'], ['_', '_', 'O'], ['_', '_', 'O']]
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

# 其它类型与容器

## 数组 array
- 数组支持所有跟可变序列有关的操作包括 .pop、.insert 和 .extend。
- 数组还提供从文件读取和存入文件的更快的方法，如 .frombytes 和 .tofile。
- 创建数组需要一个类型码，这个类型码用来表示在底层的 C 语言应该存放怎样的数据类型。
- 具体数组支持的方法参加“流畅的python 2.9.1”
- 下面的‘d’代表字节类型，即byte，-128~127
```
from array import array
from random import random
floats = array('d', (random() for i in range(10**7)))	# 双精度浮点数组生成器
print(floats[-1])	# 最末元素
fp = open('floats.bin', 'wb')
floats.tofile(fp)	# 写入二进制文件
fp.close()
floats2 = array('d')	# 新建数组
fp = open('floats.bin', 'rb')
floats2.fromfile(fp, 10**7)	# 将文件内容写到数组里
fp.close()
print(floats2[-1])	# 最末元素
print(floats2 == floats)	# 判断数组相同

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
0.4028576664776865
0.4028576664776865
True
```

## 字节 bytes
- 字节bytes是不可变的，像字节数据组成的元组
- bytes 类型值的表示以 b 开头，接着是一个单引号，后面跟着由十六进制数（例如 \x02）或 ASCII 码组成的序列，最后以配对的单引号结束
- Python 会将这些十六进制数或者 ASCII 码转换为整数，如果该字节的值为有效 ASCII编码则会显示 ASCII 字符。
- 使用 8 比特序列存储小整数的方式进行存储，每 8比特（即一字节）可以存储从 0~255 的值
- 打印 bytes 或 bytearray 数据时，Python 会以 \xxx 的形式表示不可打印的字符
- 以 ASCII 字符的形式表示可打印的字符（以及一些转义字符，例如 \n 而不是 \x0a）

```
blist = [1, 2, 3, 255]
the_bytes = bytes(blist)	# 使用列表创建一个bytes 类型的变量
print(the_bytes)
# the_bytes[1] = 127	# err，不可改变
print(b'\x61')	# 显示a，因为61对应ascii的a
print(b'\x01abc\xff')	# 无对应，原样显示
the_bytes = bytes(range(0, 256))	# 建一个包含 0到255 的所有数的bytes 
print(the_bytes)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
b'\x01\x02\x03\xff'
b'a'
b'\x01abc\xff'
b'\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c\r\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f !"#$%&\'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff'
```

## 字节数组 bytearray

- 字节数组bytearray是可变的，像字节数据组成的列表。
- 打印bytearray通常手动加入换行用于显示效果，如一行显示 16 个字节

```
blist = [1, 2, 3, 255]
the_byte_array = bytearray(blist) # 使用列表创建一个bytearray类型的变量
print(the_byte_array)
the_byte_array[1] = 127	# bytearray 类型的变量是可变的
print(the_byte_array)
the_byte_array = bytearray(range(0, 256))	# 建一个包含 0到255 的所有数的bytearray
print(the_byte_array)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
bytearray(b'\x01\x02\x03\xff')
bytearray(b'\x01\x7f\x03\xff')
bytearray(b'\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c\r\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f !"#$%&\'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff')
```
## 内存视图 memoryview
## NumPy
## SciPy

## 双向队列 deque
- 是一个线程安全、可以快速从两端添加或者删除元素的数据类型。
- 主要的方法参见“流畅的python 2.9.4”
```
from collections import deque
dq = deque(range(10), maxlen=10)	# maxlen 是一个可选参数，代表这个队列可以容纳的元素的数量，而且一旦设定，这个属性就不能修改了。
print(dq)
dq.rotate(3)	# 队列的旋转操作接受一个参数 n，当 n > 0 时，队列的最右边的 n 个元素会被移动到队列的左边。当 n < 0 时，最左边的 n 个元素会被移动到右边。
print(dq)
dq.rotate(-4) 
print(dq)
dq.appendleft(-1)	# 当试图对一个已满（len(d) == d.maxlen）的队列做头部添加操作的时候，它尾部的元素会被删除掉。注意在下一行里，元素 0 被删除了。
print(dq)
dq.extend([11, 22, 33])	# 在尾部添加 3 个元素的操作会挤掉 -1、1 和 2。
print(dq)
dq.extendleft([10, 20, 30, 40])	# extendleft(iter) 方法会把迭代器里的元素逐个添加到双向队列的左边，因此迭代器里的元素会逆序出现在队列里。
print(dq)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
deque([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)
deque([7, 8, 9, 0, 1, 2, 3, 4, 5, 6], maxlen=10)
deque([1, 2, 3, 4, 5, 6, 7, 8, 9, 0], maxlen=10)
deque([-1, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)
deque([3, 4, 5, 6, 7, 8, 9, 11, 22, 33], maxlen=10)
deque([40, 30, 20, 10, 3, 4, 5, 6, 7, 8], maxlen=10)
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
- == 用来检查两个对象是否相等，比值（对象中保存的数据）
- x != y  
  x不等于y

```
names = ['Mrs. Entity', 'Mrs. Thing'] 
n = names[:] 
print(n is names)
print(n == names)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
False
True
```
## is、is not、id()
is 运算符比较两个对象的标识（标识的描述见“变量”）；id() 函数返回对象标识的整数表示。对象 ID 的真正意义在不同的实现中有所不同。在 CPython 中，id() 返回对象的内存地址，但是在其他 Python 解释器中可能是别的值。关键是，ID 一定是唯一的数值标注，而且在对象的生命周期中绝不会变。


- x is y  
  is用来检查两个对象是否相同（是同一个对象）
- x is not y  
  x和y是不同的对象

```
charles = {'name': 'Charles L. Dodgson', 'born': 1832}
print(charles)
lewis = charles	# lewis与charles指向同一地址
print(lewis is charles)	 # is比地址，所以相同
print(id(charles))
print(id(lewis))
lewis['balance'] = 950
print(charles)

alex = {'name': 'Charles L. Dodgson', 'born': 1832, 'balance': 950}
print(alex == charles)	# 字典的==（即__eq__）是比值，所以相同
print(alex is not charles)	# 但is是比地址

[huawei@n161 aaa]$ python3 test.py 
{'name': 'Charles L. Dodgson', 'born': 1832}
True
140107530622368
140107530622368
{'name': 'Charles L. Dodgson', 'born': 1832, 'balance': 950}
True
True
```

## in、not in
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
## else
- for  
仅当 for 循环运行完毕时（即 for 循环没有被 break 语句中止）才运行 else 块。
- while  
仅当 while 循环因为条件为假值而退出时（即 while 循环没有被 break 语句中止）才运
行 else 块。
- try  
仅当 try 块中没有异常抛出时才运行 else 块。

# 迭代

## 迭代器
- 迭代器是这样的对象：实现了无参数的 __next__ 方法，返回序列中的下一个元素；
- 如果没有元素了，那么抛出 StopIteration 异常。
- Python 中的迭代器还实现了 __iter__ 方法，因此迭代器也可以迭代。

## 生成器函数 yield
- 只要 Python 函数的定义体中有 yield 关键字，该函数就是生成器函数。
- 调用生成器函数时，会返回一个生成器对象。也就是说，生成器函数是生成器工厂。
- 普通的函数与生成器函数在句法上唯一的区别是，在后者的定义体中有yield 关键字。
- 调用生成器函数返回生成器对象；生成器产出或生成值。
- 把生成器传给next函数时，生成器函数会向前，执行到函数定义中的下一个yield语句，返回产出的值


```
def gen_AB():
	print('start')
	yield 'A'
	print('continue')
	yield 'B'
	print('end.')

for c in gen_AB():	# for 机制会捕获StopIteration 异常，因此循环终止时没有报错。
	print('-->', c)

a = gen_AB()	# 创建生成器对象
print(next(a))	# 打印start、A
print(next(a))	# 打印continue、B
print(next(a))	# 打印end.后由于没有后续元素，生成器对象会抛出 StopIteration 异常


[huawei@n161 ccc]$ python3 1.py
start
--> A
continue
--> B
end.
start
A
continue
B
end.
Traceback (most recent call last):
  File "1.py", line 16, in <module>
    print(next(a))
StopIteration
```
## 标准库提供的生成器

详见流畅的python14.9、14.11
### 用于过滤的生成器函数
```
import itertools
 
# itertools.compress(it,selector_it)
# 并行处理两个可迭代对象，如果selector_it中的元素是真值，产出it中对应的元素
print([i for i in itertools.compress(range(10), [0, 0, 1, 1])])
 
# itertools.takewhile(predicate,it)
# 使用传入的生成器生成另一个生成器，predicate指定终止条件
print([i for i in itertools.takewhile(lambda n: n < 5, range(10))])
 
# itertools.dropwhile(prdicate,it)
# 与itertools.takewhile的作用相反
print([i for i in itertools.dropwhile(lambda n: n < 5, range(10))])
 
# filter(predicate,it)
# 将it中的各个元素传给predicate，如果为真，则产出it中对应的元素
print([i for i in filter(lambda a: a % 2, range(10))])  # 保留奇数
 
# itertools.filterfalse(predicate,it)
# 与filter的作用相反
print([i for i in itertools.filterfalse(lambda a: a % 2, range(10))])  # 保留偶数
 
# itertools.islice(it,stop)或者itertools.islice(it,start,stop,step=1)
# 产出it的切片 实现的是惰性操作
print([i for i in itertools.islice(range(10), 2)])
print([i for i in itertools.islice(range(10), 2, 9, 3)])

[huawei@n161 ccc]$ python3 1.py
[2, 3]
[0, 1, 2, 3, 4]
[5, 6, 7, 8, 9]
[1, 3, 5, 7, 9]
[0, 2, 4, 6, 8]
[0, 1]
[2, 5, 8]
```

### 用于映射的生成器函数
```
import itertools
import fractions
import operator
 
# itertools.accumulate(it,func)
# 产出累积的总和，如果提供了func，那么把前两个元素传给它，然后把计算的结果和下一个元素传给它，以此类推
print([i for i in itertools.accumulate(range(10), lambda a, b: a + b)])  # 计算前n项的和
 
# enunerate(it,start=0)
# 产出由两个元素构成的元组 结构是(index,item) index从start开始，每次加一 item的值中it中取
print([i for i in enumerate(range(10), start=10)])
 
# map(func,iter,[it2,...itn])
# 把it中的各个元素传给func，产出结果，如果传入n个it，func的参数必须有n个
print([i for i in map(lambda a, b, c: a + b + c, range(-10, 0, 1), range(10), range(10, 20))])  # 对it1，it2，it3对应位置的元素进行求和
# itertools.startmap(func,it)
# 把it中的各个元素传给func，产出结果
print([i for i in itertools.starmap(operator.mul, enumerate('hello world', 1))])  # 从1开始，根据字母所在位置，把字母重复相应的次数

[huawei@n161 ccc]$ python3 1.py
[0, 1, 3, 6, 10, 15, 21, 28, 36, 45]
[(10, 0), (11, 1), (12, 2), (13, 3), (14, 4), (15, 5), (16, 6), (17, 7), (18, 8), (19, 9)]
[0, 3, 6, 9, 12, 15, 18, 21, 24, 27]
['h', 'ee', 'lll', 'llll', 'ooooo', '      ', 'wwwwwww', 'oooooooo', 'rrrrrrrrr', 'llllllllll', 'ddddddddddd']
```

### 合并多个可迭代对象的生成器函数
```
import itertools
 
# itertools.chain(it1,[it2...it2])
# 先产出it1中的元素，然后产出it2中的元素，以此类推，无缝连接在一起
print([i for i in itertools.chain(range(10), range(11, 20), 'hello world')])
 
# itertools.chain.from_iterable(it)
# 功能同itertools.chain 不过传入的参数的结构有所变化   it的结构：it=[iter1,[iter2...itern]]
print([i for i in itertools.chain.from_iterable([range(10), 'hello'])])
 
# itertools.product(it1,...itn,repeat=1)
# 计算笛卡尔积，从输入的各个可迭代对象中获取元素，合并成由N个元素组成的元组，与嵌套的for循环效果一样，repeat指明重复处理多少次输入的可迭代对象
print([i for i in itertools.product(range(3), 'hello', 'world', repeat=1)])
 
# zip(it1,...itn)
# 并行从输入的各个可迭代对象中获取元素，产出由N个元素组成的元组，只要有一个可迭代对象到了头，迭代就终止
print([i for i in zip(range(5), 'hello')])
 
# zip_longest(it1,..itn,fillvalue=None)
# 与zip作用一样，但是终止条件是最长的可迭代对象到头了才终止，其他可迭代对象空缺的值用fillvalue进行补充
print([i for i in itertools.zip_longest(range(10), 'hello', fillvalue='world')])

[huawei@n161 ccc]$ python3 1.py
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 13, 14, 15, 16, 17, 18, 19, 'h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 'h', 'e', 'l', 'l', 'o']
[(0, 'h', 'w'), (0, 'h', 'o'), (0, 'h', 'r'), (0, 'h', 'l'), (0, 'h', 'd'), (0, 'e', 'w'), (0, 'e', 'o'), (0, 'e', 'r'), (0, 'e', 'l'), (0, 'e', 'd'), (0, 'l', 'w'), (0, 'l', 'o'), (0, 'l', 'r'), (0, 'l', 'l'), (0, 'l', 'd'), (0, 'l', 'w'), (0, 'l', 'o'), (0, 'l', 'r'), (0, 'l', 'l'), (0, 'l', 'd'), (0, 'o', 'w'), (0, 'o', 'o'), (0, 'o', 'r'), (0, 'o', 'l'), (0, 'o', 'd'), (1, 'h', 'w'), (1, 'h', 'o'), (1, 'h', 'r'), (1, 'h', 'l'), (1, 'h', 'd'), (1, 'e', 'w'), (1, 'e', 'o'), (1, 'e', 'r'), (1, 'e', 'l'), (1, 'e', 'd'), (1, 'l', 'w'), (1, 'l', 'o'), (1, 'l', 'r'), (1, 'l', 'l'), (1, 'l', 'd'), (1, 'l', 'w'), (1, 'l', 'o'), (1, 'l', 'r'), (1, 'l', 'l'), (1, 'l', 'd'), (1, 'o', 'w'), (1, 'o', 'o'), (1, 'o', 'r'), (1, 'o', 'l'), (1, 'o', 'd'), (2, 'h', 'w'), (2, 'h', 'o'), (2, 'h', 'r'), (2, 'h', 'l'), (2, 'h', 'd'), (2, 'e', 'w'), (2, 'e', 'o'), (2, 'e', 'r'), (2, 'e', 'l'), (2, 'e', 'd'), (2, 'l', 'w'), (2, 'l', 'o'), (2, 'l', 'r'), (2, 'l', 'l'), (2, 'l', 'd'), (2, 'l', 'w'), (2, 'l', 'o'), (2, 'l', 'r'), (2, 'l', 'l'), (2, 'l', 'd'), (2, 'o', 'w'), (2, 'o', 'o'), (2, 'o', 'r'), (2, 'o', 'l'), (2, 'o', 'd')]
[(0, 'h'), (1, 'e'), (2, 'l'), (3, 'l'), (4, 'o')]
[(0, 'h'), (1, 'e'), (2, 'l'), (3, 'l'), (4, 'o'), (5, 'world'), (6, 'world'), (7, 'world'), (8, 'world'), (9, 'world')]
```

### 把输入的各个元素扩展成多个输出元素的生成器函数
```

import itertools
 
# itertools.combinations(it,out_len)  组合 和顺序无关
# 把it产出的out_len个元素组合在一起，然后产出
print([i for i in itertools.combinations('ABC', 2)])  # 产出两两组合的元素
 
# itertools.combinations_with_replacement 组合
# 功能同itertools.combinations，但是也包含自己和自己的组合
print([i for i in itertools.combinations_with_replacement('ABC', 2)])
 
# itertools.count(start=0,step=1)
# 从start开始，以step为步长，不断产出数字
for i in itertools.count(1, 2):
    print(i, end=' ')
    if i > 10: break
print()
 
# itertools.permutations(it,out_len=len(list(it)))
# 把it产出的out_len个元素排列在一起  排列  和顺序有关
print([i for i in itertools.permutations('ABC', 2)])
 
# repeat(item,[times])
# 重复不断的产出指定的元素，除非提供times指定次数
print([i for i in itertools.repeat('hello', 10)])
 
# itertools.cycle(it)
# 从it中产出各个元素，存储各个元素的副本，然后按顺序重复不断地产出各个元素
cy = itertools.cycle('ABC')  # 将it首位相连
while True:
    print(next(cy))
    break

[huawei@n161 ccc]$ python3 1.py
[('A', 'B'), ('A', 'C'), ('B', 'C')]
[('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
1 3 5 7 9 11 
[('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
['hello', 'hello', 'hello', 'hello', 'hello', 'hello', 'hello', 'hello', 'hello', 'hello']
A
```

### 用于重新排列元素的生成器函数
```
import itertools
 
# itertools.groupby(it,key=None)
# 产出由练个元素组成的元素，形式为(key,group)，其中key是分组标准，group是生成器，用于产出分组里的元素
strs_list = ['hello', 'world', 'we', 'price', 'the', 'things', 'when', 'we', 'have', 'lost', 'them', '.']
strs_list.sort(key=len)  # 先排序
for key, group in itertools.groupby(strs_list, key=len):  # 根据元素的长度进行分组
    print(key, list(group))
 
# reversed(seq)
# 从后向前，倒序产出seq seq必须是序列，或者是实现了__reversed__的对象
print(list(reversed(strs_list)))
 
# itertools.tee(it,n=2)
# 产出一个由n个生成器组成的元组，每个生成器用于单独产出输入的可迭代对象中的元素
g1, g2 = itertools.tee('ABC')
print(list(g1))
print(list(g2))

[huawei@n161 ccc]$ python3 1.py
1 ['.']
2 ['we', 'we']
3 ['the']
4 ['when', 'have', 'lost', 'them']
5 ['hello', 'world', 'price']
6 ['things']
['things', 'price', 'world', 'hello', 'them', 'lost', 'have', 'when', 'the', 'we', 'we', '.']
['A', 'B', 'C']
['A', 'B', 'C']
```
### 可迭代的归约函数
```
import functools
import itertools
 
# 归约函数:接受一个可迭代对象，然后返回单个结果的函数。
 
# all(it)
# it中的所有元素都为真时返回True，否者返回False
print(all(range(10)))  # 因为出现了0，所以返回False
 
# any(it)
# 只有有一个元素是True就返回True，否者返回False
print(any(range(10)))
 
# max(it,[key=],[default=])
# 返回it中的最大值，key指定排序规则，如果it为空，返回default的值
print(max(['apple', 'banana', 'orange', 'peach'], key=len, default='apple'))  # 按照长度进行比较
 
# min(it,[key=],[default=])
# 返回it中的最小值，key指定排序规则，如果it为空，返回default的值
print(min([1, 2, -4, -9, 6], key=abs, default=0))  # 按照绝对值进行比较
 
# itertools.reduce(func,it,[initial])
# 把前两个元素传给func，然后把计算结果和第三个元素传给func，以此类推，返回最后的结果，如果提供了initial
# 就会把它当做第一个元素传入
print(functools.reduce(lambda a, b: a * b, range(1, 11)))  # 计算10！
print(list(itertools.accumulate(range(1, 11), lambda a, b: a * b)))  # 依次计算1! 2! 3!...10!
 
# sum(it,start=0)
# it中所有元素的总和，如果提供可选的start，会把它加上
# 0+1+2+10=13
print(sum(range(3), 10))

[huawei@n161 ccc]$ python3 1.py
False
True
banana
1
3628800
[1, 2, 6, 24, 120, 720, 5040, 40320, 362880, 3628800]
13
```

## yield from
https://blog.csdn.net/max_LLL/article/details/124242358

## 生成器表达式
- 生成器表达式可以理解为列表推导的惰性版本：不会迫切地构建列表，而是返回一个生成器，按需惰性生成元素。
- 如果列表推导是制造列表的工厂，那么生成器表达式就是制造生成器的工厂。
- 如果生成器表达式要分成多行写，则推荐使用生成器函数，以便提高可读性。此外，生成器函数有名称，因此可以重用。
- 生成器表达式是创建生成器的简洁句法，这样无需先定义函数再调用。不过，生成器函数灵活得多，可以使用多个语句实现复杂的逻辑，也可以作为协程使用
  
```
def gen_AB():
	print('start')
	yield 'A'
	print('continue')
	yield 'B'
	print('end.')

res1 = [x*3 for x in gen_AB()]	# 打印start、continue、end.此处是列表推导，全创建出来了，非lazy
for i in res1:
    print('-->', i)	# 打印AAA、BBB
print("------------")
res2 = (x*3 for x in gen_AB())	# lazy，生成器表达式会产出生成器对象，未执行生成器内的代码
for i in res2:	# 循环时刻才执行生成器内的代码
    print('-->', i)

[huawei@n161 ccc]$ python3 1.py
start
continue
end.
--> AAA
--> BBB
------------
start
--> AAA
continue
--> BBB
end.
```


## 可迭代对象

- 使用 iter 内置函数可以获取迭代器的对象。
- 如果对象实现了能返回迭代器的 __iter__ 方法，那么对象就是可迭代的。
- 序列都可以迭代；
- 实现了 __getitem__ 方法，而且其参数是从零开始的索引，这种对象也可以迭代。


### 迭代函数 __getitem__
如果没有实现 __iter__ 方法，但是实现了 __getitem__ 方法，Python 会创建一个迭代器，尝试按顺序（从索引 0 开始）获取元素。此对象则是可迭代的
```
#!/usr/bin/python3
import re
import reprlib
RE_WORD = re.compile('\w+')
class Sentence:
	def __init__(self, text):
		self.text = text
		self.words = RE_WORD.findall(text)
	def __getitem__(self, index):
		return self.words[index]
	def __len__(self):
		return len(self.words)
	def __repr__(self):
		return 'Sentence(%s)' % reprlib.repr(self.text)

s = Sentence('"The time has come," the Walrus said,')

for word in s:
    print(word)
print(s)
print(s[0])
print(s[-1])



[huawei@n161 ccc]$ python3 1.py
The
time
has
come
the
Walrus
said
Sentence('"The time ha... Walrus said,')
The
said
```
### 迭代函数 iter、next
- iter()函数的功能是：接受一个可迭代对象，将其转换成一个迭代器
- 还可以有2个参数，第一个参数中的对象不断产出值，如果产出的值和第二个参数是一样的，就停止产出

一般用法
```
a=[1,2,3]
a_iter=iter(a)
print(a_iter)
print(next(a_iter))
print(next(a_iter))


[huawei@n161 ccc]$ python3 1.py
<list_iterator object at 0x7fea017d3240>
1
2
```
一般用法
```
#!/usr/bin/python3
import re
import reprlib
RE_WORD = re.compile('\w+')
class Sentence:
	def __init__(self, text):
		self.text = text
		self.words = RE_WORD.findall(text)
	def __getitem__(self, index):
		return self.words[index]
	def __len__(self):
		return len(self.words)
	def __repr__(self):
		return 'Sentence(%s)' % reprlib.repr(self.text)

s3 = Sentence('Pig and Pepper')
print(list(iter(s3)))	# ['Pig', 'and', 'Pepper']，使用it构建了list，此时it已经用完了。如果想再次迭代，要重新构建迭代器
it = iter(s3)	# 又重新构建了it
print(it)	# <iterator object at 0x7f27cb075dd8> 打印了地址
print(next(it))	# Pig
print(next(it))	# and
print(list(it))	# ['Pepper']，使用it构建了list，此时it用完了
print(list(it))	# []，it已经用完了，所以构建出空list
print(next(it))	# err，it没有数据了。。。

[huawei@n161 ccc]$ python3 1.py
['Pig', 'and', 'Pepper']
<iterator object at 0x7f329c5eddd8>
Pig
and
['Pepper']
[]
Traceback (most recent call last):
  File "1.py", line 24, in <module>
    print(next(it))
StopIteration
[huawei@n161 ccc]$ 
```


高级用法：随机产生1到10的数字，如果产出数字是5就停止。
```
from random import randint
 
def d10():
    return randint(1, 10)
 
# 随机产生1~10之间的数，遇到5就停止
for i in iter(d10, 5):
    print(i)
```




# 函数
## 定义、传值、默认值、类型
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
- Python中的任意一个函数都有数据类型，这种数据类型是function，被称为函数类型。
- 下面是一个传递引用且有默认值的使用方式，总结如下：
- 除非这个方法确实想修改通过参数传入的对象，否则在类中直接把参数赋值给实例变量之前一定要三思，因为这样会为参数对象创建别名。如果不确定，那就创建副本。
- 此案例具有代表意义，详见流畅的Python8.4.2
```
def __init__(self, passengers=None):
	if passengers is None:
		self.passengers = []
	else:
		self.passengers = list(passengers)
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

## 可变参数（*与**）
- 分为基于元组的可变参数（*可变参数）与基于字典的可变参数（**可变参数）
- 效果类似perl的ARGV与@_

```
下例* toppings实则会变为元祖，内容为('mushrooms', 'green peppers', 'extra cheese')。

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
综合的简单案例
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
复杂的案例
```
def tag(name, *content, cls=None, **attrs):
	if cls is not None:
		attrs['class'] = cls
	if attrs:
		attr_str = ''.join(' %s="%s"' % (attr, value) for attr, value in sorted(attrs.items()))
	else:
		attr_str = ''
	if content:
		return '\n'.join('<%s%s>%s</%s>' % (name, attr_str, c, name) for c in content)
	else:
		return '<%s%s />' % (name, attr_str)

print(tag('br'))	传入单个定位参数，生成一个指定名称的空标签。
print(tag('p', 'hello'))	第一个参数后面的任意个参数会被 *content 捕获，存入一个元组
print(tag('p', 'hello', 'world'))
print(tag('p', 'hello', id=33))	tag 函数签名中没有明确指定名称的关键字参数会被 **attrs 捕获，存入一个字典。
print(tag('p', 'hello', 'world', cls='sidebar'))	cls 参数只能作为关键字参数传入
print(tag(content='testing', name="img"))	调用 tag 函数时，即便第一个定位参数也能作为关键字参数传入。

my_tag = {'name': 'img', 'title': 'Sunset Boulevard','src': 'sunset.jpg', 'cls': 'framed'}
print(tag(**my_tag))	在 my_tag 前面加上 **，字典中的所有元素作为单个参数传入，同名键会绑定到对应的
具名参数上，余下的则被 **attrs 捕获。


[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
<br />
<p>hello</p>
<p>hello</p>
<p>world</p>
<p id="33">hello</p>
<p class="sidebar">hello</p>
<p class="sidebar">world</p>
<img content="testing" />
<img class="framed" src="sunset.jpg" title="Sunset Boulevard" />
```

## 函数指针
可以将变量指向函数，此变量类型是function，虽都是function但不同函数签名的底层并不同
```
def add(a,b):
    return a+b

def sub(a,b):
    return a-b

def square(a):
    return a*b

def calc(opr):
    if opr=='+':
        return add
    else:
        return sub

f1 = calc('+')
f2 = calc('-')
print("10+5={0}".format(f1(10,5)))
print("10-5={0}".format(f2(10,5)))
print(type(f1))
print(type(f2))
print(type(square))

[huawei@n161 ccc]$ python3 1.py
10+5=15
10-5=5
<class 'function'>
<class 'function'>
<class 'function'>
```
## 过滤函数 filter
filter（）函数用于对容器中的元素进行过滤处理。下面是粗糙的案例，还可以参考[用于过滤的生成器函数](#用于过滤的生成器函数)
```
def f1(x):
    return x>50

data1 = [10, 30, 60, 100]
data2 = filter(f1, data1)
data3 = list(data2)
print(data3)

[huawei@n161 ccc]$ python3 1.py
[60, 100]

```
## 映射函数 map
map（）函数用于对容器中的元素进行映射（或变换）。下面是粗糙的案例，还可以参考[用于映射的生成器函数](#用于映射的生成器函数)
```
def f1(x):
    return x*2

data1 = [10, 30, 60, 100]
data2 = map(f1, data1)
data3 = list(data2)
print(data3)

[huawei@n161 ccc]$ python3 1.py
[20, 60, 120, 200]
```

## 传递函数

其实传的是个对象
```
def sum_args(*args):
	return sum(args)

def run_with_positional_args(func, *args):
	return func(*args)

print(run_with_positional_args(sum_args, 1, 2, 3, 4))	# 10
```
## 内部函数
```
def outer(a, b):
	def inner(c, d):
		return c + d
	return inner(a, b)

print(outer(4, 7))	# 11
```


## lambda
- lambda 关键字在 Python 表达式内创建匿名函数。
- lambda 函数的定义体中不能赋值，也不能使用 while 和 try 等语句，仅可一条语句，不用写return
- lambda 句法只是语法糖：与 def 语句一样，lambda 表达式会创建函数对象。  

语法：“lambda 参数列表：labmda体”，无需小括号与return

```
简单的额lambda使用演示
def calc(opr):
    if opr == '+':
        return lambda a, b: (a+b)
    else:
        return lambda a, b: (a-b)

f1 = calc('+')
f2 = calc('-')
print("10+5={0}".format(f1(10,5)))
print("10-5={0}".format(f2(10,5)))

[huawei@n161 ccc]$ python3 1.py
10+5=15
10-5=5

演示2
def edit_story(words, func):
	for word in words:
		print(func(word))

def enliven(word):
	return word.capitalize() + '!'


stairs = ['thud', 'meow', 'thud', 'hiss']
print("-----func:")
edit_story(stairs, enliven)

print("-----lambda:")
edit_story(stairs, lambda word: word.capitalize() + '!')

[huawei@n148 postdb_doc]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py"
-----func:
Thud!
Meow!
Thud!
Hiss!
-----lambda:
Thud!
Meow!
Thud!
Hiss!

```
将前面的filter与map换为lambda形式
```
data1 = [10, 30, 60, 100]
data2 = filter(lambda x: (x > 50), data1)
data3 = list(data2)
print(data3)
data2 = map(lambda x: (x * 2), data1)
data3 = list(data2)
print(data3)

[huawei@n161 ccc]$ python3 1.py
[60, 100]
[20, 60, 120, 200]
```
## 装饰器
- 装饰器是可调用的对象，其参数是另一个函数（被装饰的函数）。
- 函数装饰器在导入模块时立即执行，而被装饰的函数只在明确调用时运行。这突出了所谓的导入时和运行时之间的区别。
- 装饰器和被装饰的函数可以在2个不同模块里
- 装饰器内返回的结果可以是值也可以是函数对象（不是传入的函数，而是会定义一个内部函数，然后将其返回，替换被装饰的函数）
- Python 内置了三个用于装饰方法的函数：property、classmethod 和 staticmethod。

简单的演示案例
```
registry = []
def register(func):	# register 的参数是一个函数
	print('running register(%s)' % func)
	registry.append(func)
	return func	# 返回 func：必须返回函数；这里返回的函数与通过参数传入的一样。

@register		# f1 和 f2 被 @register 装饰
def f1():
	print('running f1()')
@register
def f2():
	print('running f2()')
def f3():		# f3 没有装饰
	print('running f3()')
def main():
	print('running main()')
	print('registry ->', registry)	# 打印列表，执行f1f2f3
	f1()
	f2()
	f3()
if __name__=='__main__':
	main()

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
running register(<function f1 at 0x7fe2d585b1e0>)	# register 在模块中其他函数之前运行了两次
running register(<function f2 at 0x7fe2d585b268>)	# 如果仅仅是导入此py则只会打印出这两句，因不会执行main函数
running main()
registry -> [<function f1 at 0x7fe2d585b1e0>, <function f2 at 0x7fe2d585b268>]
running f1()
running f2()
running f3()
```
## 参数化的装饰器

## 闭包

闭包是一个可以由另一个函数动态生成的函数，并且可以改变和存储函数外创建的变量的值，其实内部函数可以看作为闭包，只不过没有体现出精髓而已。
- 闭包指延伸了作用域的函数，其中包含函数定义体中引用的但又没在定义体中定义的非全局变量
- 函数是不是匿名的没有关系，关键是它能访问定义体之外定义的非全局变量

通过下案例介绍闭包特点：
- inner2() 直接使用外部的 saying 参数，而不是通过另外一个参数获取。（与上面内部函数的案例中的参数传递方式对比查看即可）
- knights2() 返回值为 inner2 函数，而不是调用它。（对比同上）
- inner2() 函数可以得到 saying 参数的值并且记录下来。
- return inner2 准确的说是返回1个没有被调用过的函数对象（是一个闭包：一个被动态创建的可以记录外部变量的函数）。


```
def knights2(saying):
	def inner2():
		return "We are the knights who say: '%s'" % saying
	return inner2

a = knights2('Duck')
print(type(a))	# a的type是函数
print(a)	# 这样打印出来的内容貌似是a的地址
print(a())	# 调用函数对象


b = knights2('Hasenpfeffer')
print(type(b))
print(b)
print(b())


[huawei@n148 postdb_doc]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pltest/pyth.py"
<type 'function'>
<function inner2 at 0x7f814caec7d0>
We are the knights who say: 'Duck'
<type 'function'>
<function inner2 at 0x7f814caec848>
We are the knights who say: 'Hasenpfeffer'
```
## nonlocal
如果为 nonlocal 声明的变量赋予新值，闭包中保存的绑定会更新。  
```
下例中count、total可以在闭包里更新

def make_averager():
	count = 0
	total = 0
	def averager(new_value):
		nonlocal count, total
		count += 1
		total += new_value
		return total / count
	return averager

avg = make_averager()
print(avg(10))
print(avg(20))
print(avg(30))

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
10.0
15.0
20.0
```

# 模块
- 类支持继承，但模块不支持。Python 模块是单例
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
## 模块搜索路径

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
- 貌似也可以叫init.py。这个文件可以是空的，但是 Python 需要它，以便把该目录作为一个包。
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
# 文件读写

## open模式

open()的模式如下，如果省略，Python将以默认的只读模式打开文件。
- 读取模式 （'r' ）
- 写入模式 （'w' ）
- 附加模式 （'a' ）
- 读写模式 （'r+' ）
- 'b' 二进制模式（与其他模式结合使用）
- 't' 文本模式（默认值，与其他模式结合使用）

## 使用with自动关闭文件
Python 的上下文管理器（context manager）会清理一些资源，例如打开的文件。使用方式见下面的案例
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
- 函数 write() 返回写入文件的字节数
- 其实也可以使用print()，见python语言及其应用8.1.1
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

## 写二进制文件
如果文件模式字符串中包含 'b'，那么文件会以二进制模式打开。这种情况下，读写的是字节而不是字符串。


```
一次性写入

bdata = bytes(range(0, 256))
fout = open('bfile', 'wb')
fout.write(bdata)
fout.close()
```

```
分块写入

fout = open('bfile2', 'wb')
size = len(bdata)
offset = 0
chunk = 100
while True:
	if offset > size:
		break
	fout.write(bdata[offset:offset+chunk])
	offset += chunk
fout.close()

```

## 读二进制文件
```
fin = open('bfile', 'rb')
bdata = fin.read()
print(len(bdata))
fin.close()
```
## seek、tell
待完善
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
## cvs

# 文件与目录
## 文件操作
- exists
- isfile
- isdir
- isabs
- rename
- copy
- link
- symlink
- islink
- realpath
- chmod
- chown
- abspath
- remove
```
import os
os.path.exists('bfile')	# 文件或目录是否存在，支持相对或者绝对路径名
os.path.isfile('bfile')	# 是否为文件
os.path.isdir('bfile')	# 判断文件夹
os.path.isabs('bfile')	# 判断绝对路径
os.rename('bfile', 'ohwell.txt')	# 把文件重命名为ohno.txt

import shutil
shutil.copy('ohwell.txt', 'ohno.txt')	# 把文件复制到ohno.txt

os.link('ohno.txt', 'yikes.txt')	# 把已有文件硬链接到一个新文件yikes.txt
os.symlink('ohno.txt', 'jeepers.txt')	# symlink()创建一个符号链接
os.path.islink('jeepers.txt')	# islink() 函数会检查参数是文件还是符号链接
os.path.realpath('jeepers.txt')	# 获取符号文件指向的文件路径名


print(os.path.abspath('pyth.py'))	# 相对转绝对路径
os.remove('oops.txt')	# 删除

```
## 目录操作
```
os.mkdir('poems')
os.chdir('poems')	
os.listdir('.')	# 获取目录列表
os.rmdir('poems')
```
## grob
```
import glob
print(glob.glob('m*'))
```
# 日期与时间
## 当前日期
```
import datetime
halloween = datetime.date(2014, 10, 31)
print(halloween)
halloween = datetime.date(2014,10,31)
print(halloween.day)
print(halloween.month)
print(halloween.year)
print(halloween.isoformat())
now = datetime.datetime.today()
print(now)
print(now.strftime("%Y:%m:%d %H:%M:%S"))

strdate = "2022:10:08 17:15:39";
data = datetime.datetime.strptime(strdate, "%Y:%m:%d %H:%M:%S");
print(data)

[huawei@n161 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/ccc/1.py"
2014-10-31
31
10
2014
2014-10-31
2022-10-08 17:17:43.038717
2022:10:08 17:17:43
2022-10-08 17:15:39
```
## 日期加减
- date 的范围 是 date.min（ 年 = 1， 月 = 1， 日 = 1） 到date.max（ 年 = 9999， 月 = 12， 日 = 31）。不能使用它来进行和历史或者天文相关的计算。


```
from datetime import date
from datetime import timedelta
one_day = timedelta(days=1)
now = date.today()
tomorrow = now + one_day
print(tomorrow)
print(now + 17*one_day)
yesterday = now - one_day
print(yesterday)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
2022-09-09
2022-09-25
2022-09-07
```
## 时间
```
import time
now = time.time()
print(now)
print(time.ctime(now))
print(time.localtime(now))
print(time.gmtime(now))

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
1662626412.5671046
Thu Sep  8 16:40:12 2022
time.struct_time(tm_year=2022, tm_mon=9, tm_mday=8, tm_hour=16, tm_min=40, tm_sec=12, tm_wday=3, tm_yday=251, tm_isdst=0)
time.struct_time(tm_year=2022, tm_mon=9, tm_mday=8, tm_hour=8, tm_min=40, tm_sec=12, tm_wday=3, tm_yday=251, tm_isdst=0)
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


# 正则 re
建议字符串都使用原始字符串即r""  

## 匹配 match
使用match（pattern ,string ,flags ）函数进行字符串匹配，re.match()方法要求必须从字符串的开头进行匹配，如果字符串的开头不匹配，整个匹配就失败了

- pattern : 是匹配的规则内容
- string : 要匹配的字符串
- flag : 可选，表示匹配模式，比如忽略大小写，多行模式等，具体参数为：
	- re.I 忽略大小写
	- re.L 表示特殊字符集 \w, \W, \b, \B, \s, \S 依赖于当前环境
	- re.M 多行模式
	- re.S 即为 . 并且包括换行符在内的任意字符（. 不包括换行符）
	- re.U 表示特殊字符集 \w, \W, \b, \B, \d, \D, \s, \S 依赖于 Unicode 字符属性数据库
	- re.X 为了增加可读性，忽略空格和 # 后面的注释
- 如果匹配成功，则返回一个Match对象（匹配对象），否则返回None。

```
import re
str_content = "Python is a good language"  # 要匹配的内容, 对应match 里面的string
str_pattern = "Python"  # pattern 匹配的规则
re_content = re.match("Python", str_content)
print(re_content)

re_content = re.match("Python", str_content).span()
print(re_content)

re_content = re.match("PYTHON", str_content, re.I)
if re_content:
    print(re_content.group())
else:
    print("没有匹配到内容")

[huawei@n161 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/ccc/1.py"
<_sre.SRE_Match object; span=(0, 6), match='Python'>
(0, 6)
Python
```
## 查找 search
使用re.search(pattern, string, flags=0)方法扫描整个字符串，并返回第一个成功的匹配。如果匹配失败，则返回None。
- pattern : 正则中的模式字符串。
- string : 要被查找替换的原始字符串。
- flags : 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。
```
import re
content = 'Hello 123456789 Word_This is just a test 666 Test'
result = re.search('(\d+).*?(\d+).*', content)  
 
print(result)
print(result.group())    # print(result.group(0)) 同样效果字符串
print(result.groups())
print(result.group(1))
print(result.group(2))

[huawei@n161 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/ccc/1.py"
<_sre.SRE_Match object; span=(6, 49), match='123456789 Word_This is just a test 666 Test'>
123456789 Word_This is just a test 666 Test
('123456789', '666')
123456789
666

```

## 查找 findall
findall（p，text）：在text字符串中查找所有匹配的内容，如果找到，则返回所有匹配的字符串列表；如果一个都没有匹配，则返回None。p是正则表达式。

- findall()返回的是括号所匹配到的结果，多个括号就会返回多个括号分别匹配到的结果，
- 如果没有括号就返回就返回整条语句所匹配到的结果。
- 这个特性是正则表达式特有的，而不仅仅只是python语言。
```
import re
kk = re.compile(r'\d+')
print(kk.findall('one1two2three3four4'))
#[1,2,3,4]
 
#注意此处findall()的用法，可传两个参数;
kk = re.compile(r'\d+')
print(re.findall(kk,"one123"))
#[1,2,3]



string="abcdefg  acbdgef  abcdgfe  cadbgfe"
#带括号与不带括号的区别
#不带括号,regex 中带有2个括号，我们可以看到其输出是一个list中包含2个tuple。
regex=re.compile("((\w+)\s+\w+)")
print(regex.findall(string))
#输出：[('abcdefg  acbdgef', 'abcdefg'), ('abcdgfe  cadbgfe', 'abcdgfe')]

# regex 中带有1个括号，其输出的内容就是括号匹配到的内容，而不是整个表达式所匹配到的结果。
regex1=re.compile("(\w+)\s+\w+")
print(regex1.findall(string))
#输出：['abcdefg', 'abcdgfe']

# regex 中不带有括号，其输出的内容就是整个表达式所匹配到的内容。
regex2=re.compile("\w+\s+\w+")
print(regex2.findall(string))
#输出：['abcdefg  acbdgef', 'abcdgfe  cadbgfe']


[huawei@n161 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/ccc/1.py"
['1', '2', '3', '4']
['123']
[('abcdefg  acbdgef', 'abcdefg'), ('abcdgfe  cadbgfe', 'abcdgfe')]
['abcdefg', 'abcdgfe']
['abcdefg  acbdgef', 'abcdgfe  cadbgfe']
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
## 使用property()操作属性
作用类似setter、getter
```
class Duck():
	def __init__(self, input_name):
		self.hidden_name = input_name
	def get_name(self):
		print('inside the getter')
		return self.hidden_name
	def set_name(self, input_name):
		print('inside the setter')
		self.hidden_name = input_name
	name = property(get_name, set_name)	# 此句是重点

fowl = Duck('Howard')
print(fowl.name)	# 会调用 get_name
fowl.get_name()
fowl.name = 'Daffy'	# 会调用 set_name
print(fowl.name)
fowl.set_name('Daffy')
print(fowl.name)


[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
inside the getter
Howard
inside the getter
inside the setter
inside the getter
Daffy
inside the setter
inside the getter
Daffy
```

## 使用setter()、@property操作属性
```

class Duck():
	def __init__(self, input_name):
		self.hidden_name = input_name
	@property	# @property，用于指示 getter 方法；
	def name(self):
		print('inside the getter')
		return self.hidden_name
	@name.setter	# @name.setter，用于指示 setter 方法
	def name(self, input_name):
		print('inside the setter')
		self.hidden_name = input_name

fowl = Duck('Howard')
print(fowl.name)
fowl.name = 'Donald'
print(fowl.name)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
inside the getter
Howard
inside the setter
inside the getter
Donald
```

## __私有变量
Python对那些需要刻意隐藏在类内部的特性有命名规范：由连续的两个下划线开头
```
class Duck():
	def __init__(self, input_name):
		self.__name = input_name
	@property
	def name(self):
		print('inside the getter')
		return self.__name
	@name.setter
	def name(self, input_name):
		print('inside the setter')
		self.__name = input_name
 
fowl = Duck('Howard')
print(fowl.name)
fowl.name = 'Donald'
print(fowl.name)
print(fowl.__name)	此句会err，外部无法访问，print(fowl._Duck__name)就行。。。
```
## 实例方法
- 以self作为第一个参数的方法都是实例方法。当被调用时Python把调用该方法的对象作为self参数传入



## 类方法classmethod与类变量
- 在类定义内部，用前缀修饰符 @classmethod 指定的方法都是类方法。
- 第一个参数是类本身（这个参数常被写作cls，即class）。
- 作用于整个类，对类作出的任何改变会对它的所有实例对象产生影响
```
class A():
	count = 0	类变量，此变量不属于self
	def __init__(self):
		A.count += 1	注意这里的调用方式不是self
	def exclaim(self):
		print("I'm an A!")
	@classmethod
	def kids(cls):	类方法使用classmethod装饰，参数1代表当前类，还可以使用更多参数
		print("A has", cls.count, "little objects.")

easy_a = A()
breezy_a = A()
wheezy_a = A()
A.kids()

[huawei@n161 aaa]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/v2.py"
('A has', 3, 'little objects.')
```

## 静态方法 staticmethod
- 静态方法使用@staticmethod装饰器，它既不需要 self 参数也不需要 class 参数
- 其实静态方法就是普通的函数，只是定义在了类体中，而不是在模块里

```
class Demo:
	@classmethod
	def klassmeth(*args):
		return args
	@staticmethod
	def statmeth(*args):
		return args

print(Demo.klassmeth())		第一个参数始终是 Demo 类
print(Demo.klassmeth('spam'))
print(Demo.statmeth())		行为与普通的函数相似
print(Demo.statmeth('spam'))



[huawei@n161 aaa]$ python -u "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/v2.py"
(<class __main__.Demo at 0x7fbaf2b19530>,)
(<class __main__.Demo at 0x7fbaf2b19530>, 'spam')
()
('spam',)
```


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
## 综合大案例
使用特殊方法和约定的结构，定义行为良好且符合 Python 风格的类。

```
from array import array
import math

class Vector2d:
	typecode = 'd'
	def __init__(self, x, y):
    # 把x和y转换成浮点数，把属性标记为私有的（即__开头）
		self.__x = float(x)
		self.__y = float(y)
	@property
	# property装饰器把读值方法标记为特性，读值方法与公开属性同名，都是x，直接返回self.__x
	def x(self):
		return self.__x
	@property
	def y(self):
		return self.__y
	def __iter__(self):
    # 把实例变成可迭代的对象，这样才能拆包,如x,y=my_vector
    # 通过 self.x 和 self.y 读取公开特性，而不必读取私有属性
    # 调用生成器表达式一个接一个产出分量
    # 也可以写成 yield self.x; yield.self.y
		return (i for i in (self.x, self.y))	
	def __repr__(self):
    # 使用 {!r} 获取各个分量的表示形式，然后插值，构成一个字符串；因为
    # Vector2d 实例是可迭代的对象，所以 *self 会把 x 和 y 分量提供给 format 函数。
		class_name = type(self).__name__
		return '{}({!r}, {!r})'.format(class_name, *self)
	def __str__(self):
    # 从可迭代的 Vector2d 实例中可以轻松地得到一个元组，显示为一个有序对
		return str(tuple(self))
	def __bytes__(self):
    # 把typecode转换成字节序列，并迭代Vector2d实例，得到一个数组，再把数组转换成字节序列
		return (bytes([ord(self.typecode)]) + bytes(array(self.typecode, self)))
	def __eq__(self, other):
    # 此实现比较元组，但副作用是Vector(3, 4)==[3, 4]也会返回正确
		return tuple(self) == tuple(other)
	# 为了把 Vector2d 实例变成可散列的，要有__hash__、__eq__，还要让向量不可变
	# 使用位运算符异或（^）混合各分量的散列值
	def __hash__(self):
 		return hash(self.x) ^ hash(self.y)
	def __abs__(self):
    # 模是 x 和 y 分量构成的直角三角形的斜边长
		return math.hypot(self.x, self.y)
	def __bool__(self):
    # 计算模然后把结果转换成布尔值
		return bool(abs(self))
	def __format__(self, fmt_spec=''):
    # 如果格式代码以 'p' 结尾，使用极坐标
		if fmt_spec.endswith('p'):
    # 从 fmt_spec 中删除 'p' 后缀。
			fmt_spec = fmt_spec[:-1]
	# 构建一个元组，表示极坐标：(magnitude, angle)。
			coords = (abs(self), self.angle())
			outer_fmt = '<{}, {}>'
		else:
    # 如果不以 'p' 结尾，使用 self 的 x 和 y 分量构建直角坐标。
			coords = self
			outer_fmt = '({}, {})'
	# 使用format函数把fmt_spec应用到各个分量上，构建一个可迭代的格式化字符串
		components = (format(c, fmt_spec) for c in coords)
		return outer_fmt.format(*components)
	@classmethod
	# 类方法装饰器，从字节序列转换成 Vector2d实例
	def frombytes(cls, octets):
    # 读取第一个字节赋值给typecode
		typecode = chr(octets[0])
	# 使用传入的 octets 字节序列创建一个 memoryview，然后使用 typecode 转换
		memv = memoryview(octets[1:]).cast(typecode)
	# 拆包转换后的 memoryview，得到构造方法所需的一对参数
		return cls(*memv)

	# 计算角度
	def angle(self):
		return math.atan2(self.y, self.x)


v1 = Vector2d(3, 4)
print(v1.x, v1.y)
x, y = v1	# 拆包
print(x, y)
v1_clone = eval(repr(v1))
print(v1 == v1_clone)	# 调用比较__eq__
print(v1)	# 会调用__str__
octets = bytes(v1)	# 调用 __bytes__
print(octets)
print(abs(v1))	# 调用 __abs__
print(bool(v1), bool(Vector2d(0, 0))) # 调用 __bool__

v1_clone = Vector2d.frombytes(bytes(v1))
print(v1_clone)
print(v1 == v1_clone)

print(format(v1))
print(format(v1, '.2f'))	# 调用__format__
print(format(v1, '.3e'))

print(Vector2d(0, 0).angle())
print(Vector2d(1, 0).angle())
epsilon = 10**-8
print(abs(Vector2d(0, 1).angle() - math.pi/2) < epsilon)
print(abs(Vector2d(1, 1).angle() - math.pi/4) < epsilon)

print(format(Vector2d(1, 1), 'p'))
print(format(Vector2d(1, 1), '.3ep'))
print(format(Vector2d(1, 1), '0.5fp'))


print(v1.x, v1.y)
# v1.x = 123	不能修改属性

v1 = Vector2d(3, 4)
v2 = Vector2d(3.1, 4.2)
print(hash(v1), hash(v2))
print(len(set([v1, v2])))

print(v1.__dict__)
print(v1._Vector2d__x)

[huawei@n161 aaa]$ python3 v2.py
3.0 4.0
3.0 4.0
True
(3.0, 4.0)
b'd\x00\x00\x00\x00\x00\x00\x08@\x00\x00\x00\x00\x00\x00\x10@'
5.0
True False
(3.0, 4.0)
True
(3.0, 4.0)
(3.00, 4.00)
(3.000e+00, 4.000e+00)
0.0
0.0
True
True
<1.4142135623730951, 0.7853981633974483>
<1.414e+00, 7.854e-01>
<1.41421, 0.78540>
3.0 4.0
7 384307168202284039
2
{'_Vector2d__x': 3.0, '_Vector2d__y': 4.0}
3.0

```
## __slots__属性
- 默认情况下，Python 在各个实例中名为 __dict__ 的字典里存储实例属性。
- 通过 __slots__ 类属性，能节省大量内存，方法是让解释器在元组中存储实例属性，而不用字典
- 具体见流畅的Python9.8
## 操作符重载 __eq__
演示了重载等号，还有很多其它符号，详见python语言及其应用6.12
```
class Word():
	def __init__(self, text):
		self.text = text
	def __eq__(self, word2):
		return self.text.lower() == word2.text.lower()

first = Word('ha')
second = Word('HA')
third = Word('eh')
print(first == second)
print(first == third)
```
## 用户定义的可调用类型 __call__
- 不仅 Python 函数是真正的对象，任何 Python 对象都可以表现得像函数。为此，只需实现实例方法 __call__。
- 其实就是对象名称后接（）进行函数调用，可以理解为类似重载操作符（）
```
import random
class BingoCage:
	def __init__(self, items):
		self._items = list(items)	# 接受任何可迭代对象；在本地构建一个副本
		random.shuffle(self._items)
	def pick(self):
		try:
			return self._items.pop()
		except IndexError:	# 如果 self._items 为空，抛出异常，并设定错误消息。
			raise LookupError('pick from empty BingoCage')
	def __call__(self):
		return self.pick()	# bingo.pick() 的快捷方式是 bingo()。

bingo = BingoCage(range(3))
print(bingo.pick())
print(bingo())

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/bbb/src/pyth.py"
0
2
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
## 多继承
当子类继承多个父类时，如果在多个父类中有相同的成员方法或成员变量，则子类优先继承左边父类中的成员方法或成员变量，从左到右继承级别从高到低。

案例见看漫画学python9.6.2

## 添加新方法
```
class Car():
	def exclaim(self):
		print("I'm a Car!")

class Yugo(Car):
	def exclaim(self):
		print("I'm a Yugo! Much like a Car, but more Yugo￾ish.")
	def need_a_push(self):
		print("A little help here?")

give_me_a_car = Car()
give_me_a_yugo = Yugo()
give_me_a_yugo.need_a_push()
# give_me_a_car.need_a_push()	父类没有此方法，会报错
```

## 重写父类方法 override

```
class A: 
	def hello(self): 
		print("Hello, I'm A.") 
class B(A): 
	def hello(self): 	在子类中，可以覆盖任何父类的方法，包括 __init__()，见下例
 		print("Hello, I'm B.") 

a = A() 
b = B() 
a.hello() 
b.hello() 

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
Hello, I'm A.
Hello, I'm B.
```

- 如果没有覆盖父类的 __init__() 方法，Python 会自动调用父类的初始化函数 __init__()
- 如果子类重写了init，则不会自动调用父类的init，但可以手动调用，见super案例

```
#!/usr/bin/python3
class Person():
	def __init__(self, name):
		self.name = name

class MDPerson(Person):
	def __init__(self, name):
		self.name = "Doctor " + name

class JDPerson(Person):
	def __init__(self, name):
		self.name = name + ", Esquire"

person = Person('Fudd')
doctor = MDPerson('Fudd')
lawyer = JDPerson('Fudd')
print(person.name)
print(doctor.name)
print(lawyer.name)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
Fudd
Doctor Fudd
Fudd, Esquire
```
## 调用父类方法 super
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
另一个在子类构造中调用父类构造的案例
```
class Person():
	def __init__(self, name):
		self.name = name

class EmailPerson(Person):
	def __init__(self, name, email):
		super().__init__(name)
		self.email = email

bob = EmailPerson('Bob Frapples', 'bob@frapples.com')
print(bob.name)
print(bob.email)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
Bob Frapples
bob@frapples.com
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
另一个案例
```
class Bill():
	def __init__(self, description):
		self.description = description
class Tail():
	def __init__(self, length):
		self.length = length
class Duck():
	def __init__(self, bill, tail):
		self.bill = bill
		self.tail = tail
	def about(self):
		print('This duck has a', self.bill.description, 'bill and a', self.tail.length, 'tail')

tail = Tail('long')
bill = Bill('wide orange')
duck = Duck(bill, tail)
duck.about()

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
This duck has a wide orange bill and a long tail
```
# 多态
## 垃圾实现
这种方式有时被称作鸭子类型（duck typing），这个命名源自一句名言：如果它像鸭子一样走路，像鸭子一样叫，那么它就是一只鸭子。

```
#!/usr/bin/python3

class Quote():
	def __init__(self, person, words):
		self.person = person
		self.words = words
	def who(self):
		return self.person
	def says(self):
		return self.words + '.'
class QuestionQuote(Quote):
	def says(self):
		return self.words + '?'
class ExclamationQuote(Quote):
	def says(self):
		return self.words + '!'

hunter = Quote('Elmer Fudd', "I'm hunting wabbits")
print(hunter.who(), 'says:', hunter.says())
hunted1 = QuestionQuote('Bugs Bunny', "What's up, doc")
print(hunted1.who(), 'says:', hunted1.says())
hunted2 = ExclamationQuote('Daffy Duck', "It's rabbit season")
print(hunted2.who(), 'says:', hunted2.says())




class BabblingBrook():
	def who(self):
		return 'Brook'
	def says(self):
		return 'Babble'

def who_says(obj):
		print(obj.who(), 'says', obj.says())

brook = BabblingBrook()
who_says(hunter)
who_says(hunted1)
who_says(hunted2)
who_says(brook)

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
Elmer Fudd says: I'm hunting wabbits.
Bugs Bunny says: What's up, doc?
Daffy Duck says: It's rabbit season!
Elmer Fudd says I'm hunting wabbits.
Bugs Bunny says What's up, doc?
Daffy Duck says It's rabbit season!
Brook says Babble

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
- else是未触发异常的路径
- finally 子句中的代码通常用于释放重要的资源，或者还原临时变更的状态
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

## 上下文管理器与with
- 上下文管理器协议包含 __enter__ 和 __exit__ 两个方法。
- with 语句开始运行时，会在上下文管理器对象上调用 __enter__ 方法。
- with 语句运行结束后，会在上下文管理器对象上调用 __exit__ 方法
- with 语句的目的是简化 try/finally 模式。
- 这种模式用于保证一段代码运行完毕后执行某项操作，即便那段代码由于异常、return 语句或 sys.exit() 调用而中止，也会执行指定的操作。

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

# 进程与线程
## 进程信息
```
import os
os.getpid()		# 当前Python解释器的进程号
os.getcwd()		# 当前工作目录
os.getuid()		# 用户 ID 
os.getgid()		# 用户组 ID
```
## 创建进程
- getoutput
	- 只是在shell中运行其他程序并返回输出（标准输出和标准错误输出）
	- 参数是一个字符串，可以表示一个完整的shell命令
	- 可以使用参数、管道、I/O 重定向等
- check_output
	- 接受一个命令和参数列表。
	- 默认情况下，它返回的不是字符串，而是字节类型的标准输出。
	- 并没有使用 shell
- getstatusoutput
	- 可以获取退出状态，返回一个包含状态码和输出的元组
- call
	- 程序的输出会打印到对应的std中，只返回退出状态
	- 在 Unix 类操作系统中，退出状态 0 通常表示运行成功

```
import subprocess
ret = subprocess.getoutput('date')
print(ret)	# Thu Sep  8 15:43:03 CST 2022
ret = subprocess.getoutput('date -u | wc')
print(ret)	#       1       6      29
ret = subprocess.check_output(['date', '-u'])	
print(ret)	# b'Thu Sep  8 07:51:23 UTC 2022\n'

ret = subprocess.getstatusoutput('date')
print(ret)	# (0, 'Thu Sep  8 15:53:54 CST 2022')

下面3种效果一样
ret = subprocess.call('date')
ret = subprocess.call('date -u', shell=True)
ret = subprocess.call(['date', '-u'])
print(ret)
```

## 简单多进程
```
import multiprocessing
import os
def do_this(what):
	whoami(what)
def whoami(what):
	print("Process %s says: %s" % (os.getpid(), what))

if __name__ == "__main__":
	whoami("I'm the main program")
	for n in range(4):
		p = multiprocessing.Process(target=do_this, args=("I'm function %s" % n,))
		p.start()

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
Process 54726 says: I'm the main program
Process 54727 says: I'm function 0
Process 54728 says: I'm function 1
Process 54729 says: I'm function 2
Process 54730 says: I'm function 3
```

## 终止进程
- 使用terminate()终止进程
- 注意没有用于线程的终止方法！
```
import multiprocessing
import time
import os
def whoami(name):
	print("I'm %s, in process %s" % (name, os.getpid()))
def loopy(name):
	whoami(name)
	start = 1
	stop = 1000000
	for num in range(start, stop):
 		print("\tNumber %s of %s. Honk!" % (num, stop))
 		time.sleep(1)

if __name__ == "__main__":
	whoami("main")
	p = multiprocessing.Process(target=loopy, args=("loopy",))
	p.start()
	time.sleep(5)
	p.terminate()


[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
I'm main, in process 54825
I'm loopy, in process 54826
        Number 1 of 1000000. Honk!
        Number 2 of 1000000. Honk!
        Number 3 of 1000000. Honk!
        Number 4 of 1000000. Honk!
        Number 5 of 1000000. Honk!
```

## 简单多进程并发
使用multiprocessing的JoinableQueue队列实现
```
import multiprocessing as mp
def washer(dishes, output):
	for dish in dishes:
		print('Washing', dish, 'dish')
		output.put(dish)

def dryer(input):
	while True:
		dish = input.get()
		print('Drying', dish, 'dish')
		input.task_done()

dish_queue = mp.JoinableQueue()
dryer_proc = mp.Process(target=dryer, args=(dish_queue,))
dryer_proc.daemon = True
dryer_proc.start()
dishes = ['salad', 'bread', 'entree', 'dessert']
washer(dishes, dish_queue)
dish_queue.join()


[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
Washing salad dish
Washing bread dish
Washing entree dish
Washing dessert dish
Drying salad dish
Drying bread dish
Drying entree dish
Drying dessert dish
```

## 简单多线程
```
import threading
def do_this(what):
	whoami(what)
def whoami(what):
	print("Thread %s says: %s" % (threading.current_thread(), what))

if __name__ == "__main__":
	whoami("I'm the main program")
	for n in range(4):
 		p = threading.Thread(target=do_this, args=("I'm function %s" % n,))
 		p.start()

[huawei@n148 postdb_doc]$ /usr/bin/python3 "/home/huawei/hwwork/postdb_doc/mdbooks/aaa/pyth.py"
Thread <_MainThread(MainThread, started 140689071798080)> says: I'm the main program
Thread <Thread(Thread-1, started 140688941364992)> says: I'm function 0
Thread <Thread(Thread-2, started 140688932972288)> says: I'm function 1
Thread <Thread(Thread-3, started 140688924579584)> says: I'm function 2
Thread <Thread(Thread-4, started 140688916186880)> says: I'm function 3
```