[TOC]
# Python Reading Notes
## 推导式

* 列表推导式 `[expression for item in iterable if condition]`
    * ``` python
        a_list = [number for number in ranges(1, 6) if number % 2 == 1]
        ```
* 字典推导式 `{key_expression : value_expression for expression in iterable}`
* 集合推导式 `{expression for expression in iterale}`
* 生成器推导式
    * 元组没有推导式，圆括号之间的是生成器推导式
        *   ``` python
            number_thing = (number for number in range(1, 6))
            ```
## 函数类型
+ 位置参数
    + 命名的位置参数
        + 无默认值的位置参数
            +   ```python
                def power(x):
                    return x * x
        
                def power(x, n):
                    s = 1
                    while n > 0:
                        s = s * x
                        n = n - 1
                return s
                ```
        + 有默认值的位置参数
            +   ```python
                # 默认值必须是不变对象
                def power(x, n=2):
                    s = 1
                    while n > 0:
                        s = s * x
                        n = n - 1
                    return s 
                ```
    + 可变的参数（数量可变）
        +   ```python
            # Definition
            # 给函数传入的所有参数都会以元组tuple的形式返回输出
            def cal(*numbers):
                sum = 0
                for n in numbers:
                sum = sum + n * n
                return sum
    
            # Calling
            cal(1, 2, 3)
            nums = [1, 2, 3]
            cal(nums[1], nums[2], nums[3])
            cal(*nums)
            ```
+ 关键字参数
    + 命名的关键字参数
        + 无默认值的命名的关键字参数
            +   ```python
                # Define person_1
                def person_1(name, age, *, city, job):
                    print(name, age, city, job)
                
                # Call persion_1
                person_1('Jack', 24, city='Beijing', job='Engineer')
                
                # Define person_2
                def person_2(name, age, *args, city, job):
                    print(name, age, args, city, job)
                ```
            
        + 有默认值的命名的关键字参数
            +   ```python
                # Define person_3
                def person_3(name, age, *, city='Beijing', job):
                    print(name, age, city, job)
                
                # Call person_3
                person('Jack', 24, job='Engineer')
                # Output: Jack 24 Beijing Engineer
                ```
    + 可变的关键字参数（数量可变）
        +   ```python
            # Define person_4
            def person_4(name, age, **kw):
                if 'city' in kw:
                    # 有city参数
                    pass
                if 'job' in kw:
                    # 有job参数
                    pass
                print('name:', name, 'age:', age, 'other:', kw)
            ```

## 命名空间和作用域
每个程序的的主要部分定义了**全局**命名空间。因此，在这个命名空间的变量是**全局变量**。你可以在一个函数内得到某个全局变量的值：
```python
animal = 'fruitable'
def print_global():
    print('inside print_global:', animal)
    
print('at the top level:', animal)
# output: at the top level: fruitbat
print_global()
# output: inside print_global: fruitbat
```
但是，如果想在函数中得到一个全局变量的值并且**改变**它，会报错：
```python
def change_and_print_global():
    print('inside change_and_print_global:', animal)
    animal = 'wombat'
    print('after the change:', animal)

change_and_print_global()
# output:
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
#   File "<stdin>", line 2, in change_and_report_it
# UnboundLocalError: local variable 'animal' referenced before assignment
```
为了**读取并改变**全局变量而不是函数中的局部变量，需要在变量前面显示地添加关键字`global`:
```python
animal = 'fruitbat'
def change_and_print_global():
    global animal
    animal = 'wombat'
    print('inside change_and_print_global:', animal)
```

## 列表 List
### 删除list中的元素
```python
list_demo = ['A', 'B', 'C', 'D']
# 1st method
# del 就像是赋值语句(=)的逆过程：它将一个python对象与它的名字分离。如果这个对象无其他名称引用，则其占用空间也会被清除
del list_demo[1]

# 2nd method, 使用remove()删除具有指定值的元素
list_demo.remove('B')

# 使用 pop() 同样可以获取列表中指定位置的元素，但在获取完成后，该元素会被自动删除
# 如果你为 pop() 指定了偏移量，它会返回偏移量对应位置的元素；如果不指定，则默认使用-1。
# 因此，pop(0) 将返回列表的头元素，而 pop() 或 pop(-1) 则会返回列表的尾元素：
marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
marxes.pop()
# output: 'Zeppo'
marxes
# output: ['Groucho', 'Chico', 'Harpo']
marxes.pop(1)
# output: 'Chico'
marxes
# output: ['Groucho', 'Harpo']
```

### 使用 index() 查询具有特定值的元素位置
```python
marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
marxes.index('Chico')
# output: 1
```

### 使用 in 判断值是否存在
```python
marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
'Groucho' in marxes
# output: True
'Bob' in marxes
# output: False
```
同一个值可能出现在列表的多个位置，但只要至少出现一次，in 就会返回True

### 对 List 中的元素排序
- 列表方法sort() 会对原列表进行排序，改变原列表内容
- 通用函数sorted() 则会返回排好序的列表副本，原列表内容不变

### 将一个列表的值复制到另一个新的列表中
- 列表 copy() 函数
- list() 转换函数
- 列表分片[:]

### 使用 count() 记录特定值出现的次数
```python
marxes = ['Groucho', 'Chico', 'Harpo']
marxes.count('Harpo')
# output: 1
marxes.count('Bob')
# output: 0
snl_skit = ['cheeseburger', 'cheeseburger', 'cheeseburger']
snl_skit.count('cheeseburger')
# output: 3
```

## 字典 Dict
### 使用 dict() 转换为字典
可以用 dict() 将包含双值子序列的序列转换成字典。
```python
lol = [ ['a', 'b'], ['c', 'd'], ['e', 'f'] ]
dict(lol)
# output: {'c': 'd', 'a': 'b', 'e': 'f'}

lot = [ ('a', 'b'), ('c', 'd'), ('e', 'f') ]
dict(lot)
# output: {'c': 'd', 'a': 'b', 'e': 'f'}

tol = ( ['a', 'b'], ['c', 'd'], ['e', 'f'] )
dict(tol)
# output: {'c': 'd', 'a': 'b', 'e': 'f'}

los = [ 'ab', 'cd', 'ef' ]
dict(los)
# output: {'c': 'd', 'a': 'b', 'e': 'f'}

tos = ( 'ab', 'cd', 'ef' )
dict(tos)
# output: {'c': 'd', 'a': 'b', 'e': 'f'}
```

### 使用 update() 合并字典
```python
>>> first = {'a': 1, 'b': 2}
>>> second = {'b': 'platypus'}
>>> first.update(second)
>>> first
{'b': 'platypus', 'a': 1}
```

## Unicode
Python 3 中的字符串是**Unicode字符串**而不是字节数组。这是与Python 2 相比最大的差别。在Python 2 中，我们需要区分普通的以字节为单位的字符串以及Unicode字符串。

如果你知道某个字符的Unicode ID，可以直接在Python 字符串中引用这个ID 获得对应字符。下面是几个例子。

- 用`\u`及4个十六进制的数字可以从Unicode 256 个基本多语言平面中指定某一特定字符。其中，前两个十六进制数字用于指定平面号（00到FF），后面两个数字用于指定该字符位于平面中的位置索引。00 号平面即为原始的ASCII字符集，字符在该平面的位置索引与它的ASCII 编码一致。
- 我们需要使用更多的比特位来存储那些位于更高平面的字符。Python为此而设计的转义序列以`\U` 开头，后面紧跟着8个十六进制的数字，其中最左一位需为0。
- 你也可以通过`\N{name}`来引用某一字符，其中name 为该字符的标准名称，这对所有平面的字符均适用。在Unicode字符名称索引页（[http://www.unicode.org/charts/charindex.html](Unicode字符名称索引页)）可以查到字符对应的标准名称。

Python 中的unicodedata模块提供了下面两个方向的转换函数：
- `lookup()`——接受不区分大小写的标准名称，返回一个Unicode 字符；
- `name()`——接受一个Unicode 字符，返回大写形式的名称。
下面的例子中，我们将编写一个测试函数，它接受一个Python Unicode字符，查找它对应的名称，再用这个名称查找对应的Unicode 字符（它应该与原始字符相同）：
```python
>>> def unicode_test(value):
... import unicodedata
... name = unicodedata.name(value)
... value2 = unicodedata.lookup(name)
... print('value="%s", name="%s", value2="%s"' % (value, name, value2))
...
```
用一些字符来测试一下吧。首先试一下纯ASCII 字符：

```python
>>> unicode_test('A')
value="A", name="LATIN CAPITAL LETTER A", value2="A"
```
### 使用UTF-8编码和解码
对字符串进行处理时，并不需要在意Python 中Unicode字符的存储细节。但当需要与外界进行数据交互时则需要完成两件事情：
- 将字符串**编码**为字节；
- 将字**节解码**为字符串。
#### 编码
编码是将字符串转化为一系列字节的过程。字符串的encode() 函数所接收的第一个参数是编码方式名。
```python
>>> snowman = '\u2603'
>>> len(snowman)
1
>>> ds = snowman.encode('utf-8')
>>> len(ds)
3
>>> ds
b'\xe2\x98\x83'
```
#### 解码
解码是将字节序列转化为Unicode 字符串的过程。
```python
>>> place = 'caf\u00e9'
>>> place
'café'
>>> type(place)
<class 'str'>

>>> place_bytes = place.encode('utf-8')
>>> place_bytes
b'caf\xc3\xa9'
>>> type(place_bytes)
<class 'bytes'>

>>> place2 = place_bytes.decode('utf-8')
>>> place2
'café'
```

## 迭代器
我们已经知道，可以直接作用于`for`循环的数据类型有以下几种：
- 一类是集合数据类型，如`list`、`tuple`、`dict`、`set`、`str`等；
- 一类是`generator`，包括生成器和带`yield`的generator function。
这些可以直接作用于`for`循环的对象统称为可迭代对象：`Iterable`。

可以使用`isinstance()`判断一个对象是否是`Iterable`对象：
```python
>>> from collections import Iterable
>>> isinstance([], Iterable)
True
>>> isinstance({}, Iterable)
True
>>> isinstance('abc', Iterable)
True
>>> isinstance((x for x in range(10)), Iterable)
True
>>> isinstance(100, Iterable)
False
```

而生成器不但可以作用于`for`循环，还可以被`next()`函数不断调用并返回下一个值，直到最后抛出`StopIteration`错误表示无法继续返回下一个值了。

可以被`next()`函数调用并不断返回下一个值的对象称为迭代器：`Iterator`。

可以使用`isinstance()`判断一个对象是否是`Iterator`对象：
```python
>>> from collections import Iterator
>>> isinstance((x for x in range(10)), Iterator)
True
>>> isinstance([], Iterator)
False
>>> isinstance({}, Iterator)
False
>>> isinstance('abc', Iterator)
False
```

生成器都是`Iterator`对象，但`list`、`dict`、`str`虽然是`Iterable`，却不是`Iterator`。

把`list`、`dict`、`str`等`Iterable`变成`Iterator`可以使用`iter()`函数：
```python
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True
```
你可能会问，为什么`list`、`dict`、`str`等数据类型不是`Iterator`？

这是因为Python的`Iterator`对象表示的是一个数据流，`Iterator`对象可以被`next()`函数调用并不断返回下一个数据，直到没有数据时抛出`StopIteration`错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过`next()`函数实现按需计算下一个数据，所以`Iterator`的计算是惰性的，只有在需要返回下一个数据时它才会计算。

`Iterator`甚至可以表示一个无限大的数据流，例如全体自然数。而使用`list`是永远不可能存储全体自然数的。
### 小结

凡是可作用于`for`循环的对象都是`Iterable`类型；凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；集合数据类型如`list`、`dict`、`str`等是`Iterable`但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。

Python的`for`循环本质上就是通过不断调用`next()`函数实现的，例如：
```python
for x in [1, 2, 3, 4, 5]:
    pass
```
实际上完全等价于：
```python
# 首先获得Iterator对象:
it = iter([1, 2, 3, 4, 5])
# 循环:
while True:
    try:
        # 获得下一个值:
        x = next(it)
    except StopIteration:
        # 遇到StopIteration就退出循环
        break
```