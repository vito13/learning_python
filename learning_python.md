---
阅读进度
Python编程：从入门到实践（第2版）		继续第9章
python基础教程（第三版）				继续2.3.2

---
# 基础知识
## 数值
- 无论是哪种运算，只要有操作数是浮点数，Python默认得到的总是浮点数，即便结果原本为整数也是如此。
- 书写很大的数时，可使用下划线将其中的数字分组，如 universe_age = 14_000_000_000
- 可以同时赋值多个变量 x, y, z = 0, 0, 0
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
## input、int
```
#!/usr/bin/python3
height = input("How tall are you, in inches? ")
height = int(height)
if height >= 48:
 print("\nYou're tall enough to ride!")
else:
 print("\nYou'll be able to ride when you're a little older.")

```
# 字符串
## 类型
多行的、原始的、还有图标的...
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
## 大写、小写、驼峰
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
## format
f字符串是Python 3.6引入的，否则需要使用format()方法
```
#!/usr/bin/python3
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(full_name)
message = f"Hello, {full_name.title()}!"
print(message)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
ada lovelace
Hello, Ada Lovelace!
```
## 去空白
- lstrip
- strip
- rstrip
  可用于在read文件后去除文件末尾多余的空白或换行，见文件读取案例
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
# 列表
列表非常适合用于存储在程序运行期间可能变化的数据集。列表元素是可以修改的。使用中括号定义
## 定义与访问
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
## 使用range初始化
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
## 使用*初始化
生成包含n个指定初值元素的列表
```
sequence = [None] * 10  # [None, None, None, None, None, None, None, None, None, None]
```
## 使用list初始化
```
arr = list('Hello')
print(arr)	# ['H', 'e', 'l', 'l', 'o']

可以使用 ''.join(somelist) 再连起来
```
## 复制列表
这里是2个列表对象
```
#!/usr/bin/python3
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods[:]
my_foods.append('cannoli')
print(my_foods)
print(friend_foods)

[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['pizza', 'falafel', 'carrot cake', 'cannoli']
['pizza', 'falafel', 'carrot cake']
```
这里成一个了
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
## 列表拼接（相加）
```
print([1, 2, 3] + [4, 5, 6])	# [1, 2, 3, 4, 5, 6]
```
## 增删改查
```
#!/usr/bin/python3
motorcycles = []	# 空列表
motorcycles.append('honda')	# 添加到列表末尾
motorcycles.append('yamaha')
motorcycles.append('suzuki')
print(motorcycles)
motorcycles[0] = 'ducati'	# 修改元素
print(motorcycles)
motorcycles.insert(1, 'aaa')	# 插入到指定位置
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
## 排序与反序
sort会保存，sorted是返回临时结果
```
#!/usr/bin/python3
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort()	# 永久排序，改变元素
print(cars)
cars.sort(reverse=True)	# 倒序参数
print(cars)
print(sorted(cars))		# 返回排序后的结果，不改变内容
```
reverse将所有元素反序
```
#!/usr/bin/python3
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.reverse()
print(cars)
[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
['subaru', 'toyota', 'audi', 'bmw']
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
## 长度
```
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(len(cars))
```
## 检查元素存在
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
## 遍历
for
```
#!/usr/bin/python3
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")

print("Thank you, everyone. That was a great magic show!")
```
while
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
# 切片
- 使用切片（slicing）来访问特定范围内的元素。两个索引来指定切片的边界
- 第一个索引指定的元素包含在切片内，但第二个索引指定的元素不包含在切片内。
- 切片的步长默认为1，但也可以设置

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
步长测试
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
# 元组
不能修改元素值的列表被称为元组。使用小括号定义
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
# 字典
## 创建访问增删改查
```
#!/usr/bin/python3
alien_0 = {'color': 'green', 'points': 5}		# 定义字典
print(alien_0['color'])		# 访问元素
# print(alien_0['color1'])	访问不存在的元素会error
point_value = alien_0.get('color1', 'No point value assigned.')	# 安全的获取元素方式，没有则返回第二个字符串
print(point_value)


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
del alien_0['points']		# 删除元素
print(alien_0)


[huawei@n148 pythontest]$ /usr/bin/python3 "/home/huawei/playground/pythontest/pyth.py"
green
No point value assigned.
{'color': 'green', 'points': 5}
{'color': 'green', 'points': 5, 'x_position': 0, 'y_position': 25}
{'color': 'green', 'points': 5}
The alien is now yellow.
{'color': 'yellow'}
```
## 遍历、keys、values、sort、set
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
if 'erin' not in favorite_languages.keys():	# 判断存在k
	print("Erin, please take our poll!")

for language in favorite_languages.values():	# 遍历values
	print(language.title())
for language in set(favorite_languages.values()):	# 对返回的values集合进行去重后再遍历
	print(language.title())


```
# 复杂数据结构
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
## and、or
```
(age_0 >= 21) and (age_1 >= 21)
(age_0 >= 21) or (age_1 >= 21)
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
## break、continue
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

## 传递任意个参数
效果类似perl的ARGV与@_

下例*toppings实则会变为元祖，内容为('mushrooms', 'green peppers', 'extra cheese')。也即一个*实际对应的是元祖，下面**user_info则对应字典
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
# 模块
## 定义
```
[huawei@n148 pythontest]$ cat pizza.py 
#!/usr/bin/python3
def make_pizza(size, *toppings):
        print(f"\nMaking a {size}-inch pizza with the following toppings:")
        for topping in toppings:
                print(f"- {topping}")
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

# 文件
open()的模式如下，如果省略，Python将以默认的只读模式打开文件。
- 读取模式 （'r' ）
- 写入模式 （'w' ）
- 附加模式 （'a' ）
- 读写模式 （'r+' ）
## 读取
一次读入所有
```
#!/usr/bin/python3
with open('pi_digits.txt') as file_object:
	contents = file_object.read()
print(contents.rstrip())
```
循环读取每一行
```
#!/usr/bin/python3
with open('pi_digits.txt') as file_object:
    lines = file_object.readlines()
for line in lines:
	print(line.rstrip())
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
# 异常处理
## try、except、else
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