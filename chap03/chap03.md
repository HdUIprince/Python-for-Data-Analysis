
# 内建数据结构、函数和文件

## 数据结构和序列

### 元组

- 元组是一种固定长度，不可变的Python对象序列
- 使用`tuple`函数将任意序列或者迭代器转换为元组
- 元组中的元素可以通过`[ ]`来获取，Python中的序列是从零开始的。
- 用加号`+`链接元组以生成更长的元组。
- 将元组乘以整数，会和列表一样生成含有多分拷贝的元组。对象自身没有复制，只是指向它们的引用发生了复制。


```python
tup = 4, 5, 6
tup
```




    (4, 5, 6)




```python
nested_tup = (4, 5, 6), (7, 8)
nested_tup
```




    ((4, 5, 6), (7, 8))




```python
tuple([4, 0, 2])
```




    (4, 0, 2)




```python
tup = tuple('string')
print(tup)
print(tup[0])
```

    ('s', 't', 'r', 'i', 'n', 'g')
    s
    


```python
tup = tuple(('foo', [1, 2], True))
# tup[2] = False wrong tuple不能被修改
tup[1].append(3)  # 列表是可变对象
print(tup)
```

    ('foo', [1, 2, 3], True)
    


```python
(4,  None, 'foo') + (6, 0) + ('bar', )
```




    (4, None, 'foo', 6, 0, 'bar')




```python
tup = ('foo', 'bar')
print('tup =', tup)
tup_times_four = tup * 4
print('tup =', tup)
print('tup_times_four =', tup_times_four)
```

    tup = ('foo', 'bar')
    tup = ('foo', 'bar')
    tup_times_four = ('foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'bar')
    

#### 元组拆包

- 将元组型的表达式赋值给变量时，Python会对等号右边的值进行拆包
- 元组的拆包可以交换变量；遍历元组或列表组成的序列；从函数返回多个值。
- 元组拆包还可以采集一些元素，使用`*rest`或者`*_`丢弃不想要的元素。


```python
tup = (4, 5, 6)
a, b, c = tup
b
```




    5




```python
tup = 4, 5, (6, 7)
a, b, (c, d) = tup
d
```




    7



```python
# 交换变量不用如此繁琐
temp = a
a = b
b = temp

###########
In [1]: a, b = 1, 2

In [2]: a
Out[2]: 1

In [3]: b
Out[3]: 2

In [4]: a, b = b, a

In [5]: a
Out[5]: 2

In [6]: b
Out[6]: 1
```


```python
# 遍历元组或列表组成的序列

seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
for a, b, c in seq:
    print('a={0}, b={1}, c={2}'.format(a, b, c))
```

    a=1, b=2, c=3
    a=4, b=5, c=6
    a=7, b=8, c=9
    


```python
values = [1, 2, 3, 4, 5]
a, b, *rest = values
print('a =', a)
print('b = ' + str(b))
print(str(rest) + ' ' + str(type(rest)))
```

    a = 1
    b = 2
    [3, 4, 5] <class 'list'>
    

#### 元组方法

- 元组的内容和长度是无法改变的，实例方法很少
- `count`方法用来计量某个数值在元组中出现的次数。


```python
a = (1, 2, 2, 2, 3, 4, 2)
# 2在此元组中出现的次数
a.count(2)
```




    4



### 列表

- 列表的长度是可变的，内容是可修改的。
- 可以使用中括号`[ ]`或者`list`函数来定义列表
- `list`函数用来将迭代器或生成器转化为列表


```python
a_list = [2, 3, 7, None]
tup = ('foo', 'bar', 'baz')
b_list = list(tup)  # 将元组转化为列表
print(b_list)
b_list[1] = 'peekaboo'  # 修改列表的元素
print(b_list)
```

    ['foo', 'bar', 'baz']
    ['foo', 'peekaboo', 'baz']
    


```python
gen = range(10)
print(gen)
print(list(gen))

```

    range(0, 10)
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    

#### 增加和移除元素

- `append`方法将元素添加到列表尾部,是直接在原列表上进行操作
- `insert`方法将元素插到指定的列表位置,插入位置范围是0到列表长度之间
- `insert`的反操作是`pop`该操作会将特定位置的元素移除并返回,默认是最后一个
- `remove`方法移除元素，该方法会定位第一个符合要求的值并移除。
- `in`检查一个值是否在列表中
- `not in`表示不在列表中
- 注意检查列表中是否含有某个值是十分缓慢的，线性扫描O(n),而字典或者集合速度较快(基于哈希表),为O(1)


```python
b_list.append('dwarf')
b_list
```




    ['foo', 'peekaboo', 'baz', 'dwarf']




```python
b_list.insert(1, 'red')
b_list
```




    ['foo', 'red', 'peekaboo', 'baz', 'dwarf']




```python
b_list.pop(2)
b_list
```




    ['foo', 'red', 'baz', 'dwarf']




```python
b_list.append('foo')
b_list
```




    ['foo', 'red', 'baz', 'dwarf', 'foo']




```python
b_list.remove('foo')
b_list
```




    ['red', 'baz', 'dwarf', 'foo']




```python
print('dwarf' in b_list)
print('dwarf' not in b_list)
```

    True
    False
    

#### 连接和联合列表

- 两个列表可以使用`+`连接
- `extend`方法用于向一个已经定义的列表中添加多个元素
- 连接时`extend`优于`+`


```python
[4, None, 'foo'] + [7, 8, (2, 3)]
```




    [4, None, 'foo', 7, 8, (2, 3)]




```python
x = [4, None, 'foo']
x.extend([7, 8, (2, 3)])
x
```




    [4, None, 'foo', 7, 8, (2, 3)]



#### 排序

- `sort`方法用于对列表进行内部排序(无需创建一个对象) 不可逆的
- `sort`方法指定二级排序参数`key`


```python
a = [7, 2, 5, 1, 3]
print(a)
print(a.sort())
print(a)
```

    [7, 2, 5, 1, 3]
    None
    [1, 2, 3, 5, 7]
    


```python
# 通过字符串的长度来进行排序
b = ['saw', 'small', 'He', 'foxes', 'six']
b.sort(key=len)
print(b)
```

    ['He', 'saw', 'six', 'small', 'foxes']
    

#### 二分搜索和已排序列表的维护

- 内建的`bisect`模块实现了二分搜索和已排序列表的插值
- `bisect.bisect`会找到元素应当插入的位置
- `bisect.insort`将元素插入到相应位置
- `bisect`模块的函数并不会检查列列是否已经排序，代价太大，因此有可能出错。


```python
import bisect
c = [1, 2, 2, 2, 3, 4, 7]
print(bisect.bisect(c, 2))
print(bisect.bisect(c, 5))
bisect.insort(c, 6)
print(c)
```

    4
    6
    [1, 2, 2, 2, 3, 4, 6, 7]
    

#### 切片

- 使用切片符号可以对打说书苏烈类型选取其子集,将`start:stop`传入索引符号`[]`中
- 起始的`start`包含，结尾的`stop`不包含，因此元素的数量是`stop - start`
- `start`和`stop`省略的刷则会默认传入序列的起始位置和结束位置
- 步进值`step`可以在第二个默哀好后面使用，意思是每隔多少个数取一个值。
- 令步进值`step`为1可以对列表或者元组进行翻转。


```python
seq = [7, 2, 3, 7, 5, 6, 0, 1]
seq[1: 5]
```




    [2, 3, 7, 5]




```python
seq[3:4] = [6, 3]
print(seq)
```

    [7, 2, 3, 6, 3, 3, 5, 6, 0, 1]
    


```python
seq[:5]
```




    [7, 2, 3, 6, 3]




```python
seq[3:]
```




    [6, 3, 3, 5, 6, 0, 1]




```python
seq[-4:]
```




    [5, 6, 0, 1]




```python
seq[-6:-2]
```




    [3, 3, 5, 6]




```python
seq[::2]
```




    [7, 3, 3, 5, 0]




```python
seq[::-1]
```




    [1, 0, 6, 5, 3, 3, 6, 3, 2, 7]



### 内建序列函数

#### enumerate

- `enumerate`构造一个字典，返回`(i, value)`的元组序列，将序列值映射到索引位置上

```python
i = 0
for i in collection:
    do something
    i += 1
    
# 等效于
for i, value in enumerate(collection):
    do something
```


```python
some_list = ['foo', 'bar', 'baz']
mapping = {}
for i, v in enumerate(some_list):
    mapping[i] = v
    
print(mapping)
```

    {0: 'foo', 1: 'bar', 2: 'baz'}
    

#### sorted

- `sorted`函数返回一个根据任意序列中的元素新建的已排序列表


```python
sorted([7, 1, 2, 6, 0, 3, 2])
```




    [0, 1, 2, 2, 3, 6, 7]



#### zip

- `zip`将列表、元组、或者其他序列的元素配对，新建一个元组构成的列表
- `zip`可以处理任意长度的序列，它生成的列表长度由其中最短的序列决定。
- `zip`常用场景为同时遍历多个序列，有时候会与`enumerate`同时使用。
- 给定一个已经配对的序列时，`zip`函数可以进行相关的拆分，或者说将行的列表转换为列的列表，使用`*name`作为`zip`的参数


```python
seq1 = ['foo', 'bar', 'baz']
seq2 = ['one', 'two', 'three']
zipped = zip(seq1, seq2)
print(zipped)
# 需要将转换之后的对象转换为一个列表
print(list(zipped))
```

    <zip object at 0x0000020598C51AC8>
    [('foo', 'one'), ('bar', 'two'), ('baz', 'three')]
    


```python
seq3 = [False, True]
zipped = zip(seq1, seq2, seq3)
# 克制生成列表的长度为2
print(list(zipped))
```

    [('foo', 'one', False), ('bar', 'two', True)]
    


```python
for i, (a, b) in enumerate(zip(seq1, seq2)):
    print('{0}:{1}, {2}'.format(i, a, b))
```

    0:foo, one
    1:bar, two
    2:baz, three
    


```python
pitchers = [('Naolan', 'Ryan'), ('Roger', 'Clemens'), ('Schilling', 'Curt')]
first_name, last_name = zip(*pitchers)
print(first_name)
print(last_name)
```

    ('Naolan', 'Roger', 'Schilling')
    ('Ryan', 'Clemens', 'Curt')
    

#### reversed

- `reversed`将序列中的元素倒序排列
- `reversed`是一个生成器，如果没有实例化将不会产生一个倒序的列表


```python
list(reversed(range(10)))
```




    [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]



### 字典

- 字典(dict),也叫做哈希表或者关联数组，键值对集合，键和值都是Python对象
- 访问、插入、设置字典的元素
- 使用`del`或者`pop`删除值，`pop`方法会在删除的同时返回被删的值，并删除键
- `keys`和`values`方法获得字典键和值的迭代器，然而键值对没有特定的顺序，这些函数的键值都是按照相同的顺序
- `update`方法将两个字典合并，其改变了字典中元素位置，因此对于任何原字典中已经存在的键，则它的值会被后面字典中的相应值所覆盖。


```python
empty_dict = {}
d1 = {'a':'some value', 'b':[1, 2, 3, 4]}
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4]}




```python
# 插入元素
d1[7] = 'an integer'
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer'}




```python
# 访问元素
d1['b']
```




    [1, 2, 3, 4]




```python
d1[5] = 'some value'
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer', 5: 'some value'}




```python
d1['dummy'] = 'another value'
d1
```




    {'a': 'some value',
     'b': [1, 2, 3, 4],
     7: 'an integer',
     5: 'some value',
     'dummy': 'another value'}




```python
del(d1[5])
d1
```




    {'a': 'some value',
     'b': [1, 2, 3, 4],
     7: 'an integer',
     'dummy': 'another value'}




```python
ret = d1.pop('dummy')
print(ret)
print(d1)
```

    another value
    {'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer'}
    


```python
print(d1.keys())
list(d1.keys())
```

    dict_keys(['a', 'b', 7])
    




    ['a', 'b', 7]




```python
print(d1.values())
print(type(d1.values()))
print(list(d1.keys()))
```

    dict_values(['some value', [1, 2, 3, 4], 'an integer'])
    <class 'dict_values'>
    ['a', 'b', 7]
    


```python
d1.update({'b':'foo', 'c':12})
d1
```




    {'a': 'some value', 'b': 'foo', 7: 'an integer', 'c': 12}



####  从序列生成字典

- 字典本身是2-元组的集合，因此字典可以接受2-元组的列表作为参数


```python
mapping = {}
for key, value in zipip(key_list, value_list):
    mapping[key] = value
```


```python
mapping = dict(zip(range(5), reversed(range(5))))
mapping
```




    {0: 4, 1: 3, 2: 2, 3: 1, 4: 0}



#### 默认值

- 带有默认值的`get`方法会在`key`参数不是字典的键时返回`None`，而`pop`会抛出异常


```python
if key in some_dict:
    value = some_dict[key]
else:
    value = some_dict[key]
```


```python
words = ['apple', 'bat', 'bar', 'atom', 'book']
by_letter = {}

for word in words:
    letter = word[0]   # 每个单词首字母
    if letter not in by_letter:
        by_letter[letter] = [word] # key=letter,value=list[words]
    else:
        by_letter[letter].append(word)
        
by_letter
```




    {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}




```python
by_letter1 = {}
for word in words:
    letter = word[0]
    by_letter1.setdefault(letter, []).append(word)
        
by_letter1
```




    {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}




```python
from collections import defaultdict
by_letter = defaultdict(list)
for word in words:
    by_letter[word[0]].append(word)
by_letter
```




    defaultdict(list, {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']})



#### 有效的字典键类型

- 字典的之后可以是任意Python对象，但是键必须是不可变的对象，比如标量类型(整数，浮点数，字符串)或元组(且元组内对象也必须是不可变对象)
- 哈希化，运用`hash`函数来检查一个对象是否可以哈希化(即是否可以作为字典的键)
- 将列表转化为元组之后才可以作为键
- 对于元组而言，只要其内部的元素都可以哈希化，则它自己可以哈希化。


```python
hash('string')
```




    -1018055484380657404




```python
hash((1, 2, (2, 3)))
# 会因为列表是可变的而失败
# hash((1, 2, [2, 3]))
```




    1097636502276347782




```python
d = {}
d[tuple([1, 2, 3])] = 5
d
```




    {(1, 2, 3): 5}



### 集合

- 集合是一种无序且元素唯一的容器
- 创建方式
    1. 使用`set`函数
    2. 用*字面值集*与大括号的方法
- 集合支持数学上的运算，并集，交集，差集，补集
- 与字典相似，集合的元素是不可变的，
- 当且仅当两个集合的内容完全一样时，两个集合才相等

Python集合操作

|函数|替代方法|描述|
|:-|:-|:-|
|a.add(x)|N/A|将元素x加入集合a|
|a.clear()|N/A|将集合重置为空，清空所有元素|
|a.remove(x)|N/A|从集合a移除某个元素|
|a.pop()|N/A|移除任意元素，如果集合是空的则抛出keyError|
|a.union(b)| a\|b| a和b中所有不同元素|
|a.update(b)| a\|=b |将a的内容设置为a和b的并集|
|a.intersection(b)| a&b | a、b中同时包含的元素|
|a.intersection_update(b) |a&=b|将a的内容设置为a和b的交集|
|a.difference(b)|a-b|在a不在b的元素|
|a.difference_update(b)| a-=b |将a的内容设为在a不在b的元素|
|a.symmetric_difference(b)|a^b|所有在a或b中，但不是同时在a，b中的元素|
|a.symmetric_difference_update(b)| a^=b|将a的内容设为所有在a或b中，但不是同时在a,b中的元素|
|a.issubset(b)| N/A|如果a包含于b,返回True|
|a.issuperset(b)|N/A|如果a包含b返回True|
|a.isdisjoint(b)|N/A|a、b没有交集返回True|


```python
set([2, 2, 2, 1, 3, 3])
```




    {1, 2, 3}




```python
{2, 2, 2, 1, 3, 3}
```




    {1, 2, 3}




```python
# 并集的实现
a = {1, 2, 3, 4, 5}
b = {3, 4, 5, 6, 7, 8}
print(a.union(b))
print(a | b)
```

    {1, 2, 3, 4, 5, 6, 7, 8}
    {1, 2, 3, 4, 5, 6, 7, 8}
    


```python
# 交集的实现
print(a.intersection(b))
print(a & b)
```

    {3, 4, 5}
    {3, 4, 5}
    


```python
c = a.copy()
c |= b
print(c)
```

    {1, 2, 3, 4, 5, 6, 7, 8}
    


```python
d = a.copy()
d &= b
print(d)
```

    {3, 4, 5}
    


```python
my_data = [1, 2, 3, 4]
# 先将可变的列表转化为不可变的元组，再将元组转化为集合
my_set = {tuple(my_data)}
print(my_set)
```

    {(1, 2, 3, 4)}
    


```python
# 判断是否是子集
a_set = {1, 2, 3, 4, 5}
print({1, 2, 3}.issubset(a_set))

# 判断是否是超集
print(a_set.issuperset({1, 2, 3}))

# 当两个集合的内容一样时，连个集合才相等
print({1, 2, 3} == {3, 2, 1})
```

    True
    True
    True
    

### 列表、集合和字典的推导式

- 过滤一个容器的元素，用一种简明的表达式转化传递给过滤器的元素，从而生成一个新的列表。
- 过滤条件是可以忽略的，只保留表达式

```python
expr for value in collection if condition

# 等价于下面的循环
result = []
for value in collection:
    if condition:
        result.append(expr)
```


```python
# 过滤出长度大于2并且将首字母大写
strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
[x.upper() for x in strings if len(x)>2]
```




    ['BAT', 'CAR', 'DOVE', 'PYTHON']



```python
# 字典推导式
dict_comp = {key-expr:value-expr for value in collection if condition}

# 集合推导式
set_comp = {expr for value in collection in condition}
```


```python
unique_length = {len(x) for x in strings}
print(unique_lengths)
```

    {1, 2, 3, 4, 6}
    


```python
set(map(len, strings))
```




    {1, 2, 3, 4, 6}




```python
loc_mapping = {val:index for index, val in enumerate(strings)}
print(loc_mapping)
```

    {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}
    

#### 嵌套列表推导式

- `for`表达式的顺序应该与写嵌套`for`循环来代替列表推导式的顺序一致


```python
all_data = [['John', 'Emily', 'Michael', 'Mary', 'Steven'],
           ['Maria', 'Juan', 'Javier', 'Natalia', 'Pilar']]

names_of_interest = []
for names in all_data:
    enough_es = [name for name in names if name.count('e')>=2]
    names_of_interest.extend(enough_es)
    
print(names_of_interest)
```

    ['Steven']
    


```python
# 使用一个嵌套列表推导式来完成
# for循环部分是在按照嵌套的顺序排列的，所有的过滤条件都放在最后

result = [name for names in all_data for name in names if name.count('e')>=2]
print(result)
```


```python
# 将含有整数元组的列表扁平化为一个简单的整数列表

some_tuples = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
flattened = [x for tup in some_tuples for x in tup]
print(flattened)
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9]
    


```python
[[x for x in tup] for tup in some_tuples]
```




    [[1, 2, 3], [4, 5, 6], [7, 8, 9]]



## 函数

- 可以有多条`return`语句，Python到大函数尾部仍然没有遇到`return`则自动返回`None`
- 每个函数都有`关键字参数`和`位置参数`
- `关键字参数`最常用于指定默认值或可选参数
- 函数参数的主要限制是`关键字参数`必须跟在`位置参数`的后面
- 可以按照任意顺序指定`关键字参数`
- 可以使用`关键字参数`向位置参数传参

```python
def my_function(x, y, z=1.5):
    if z > 1:
        return z*(x+y)
    else:
        return z/(x+y)
```

### 命名空间，作用域和本地函数

- 变量的作用域也即命名空间
- 在函数内部任意的变量都是默认分配到本地的命名空间
- 本地命名空间是在函数被调用时生成的，并立即由函数的参数填充。
- 当函数执行结束时，本地命名空间就会被销毁
- `global`关键字声明为全局变量


```python
# a会在函数退出时被销毁
def func():
    a = []
    for i in range(5):
        a.append(i)
    return a
print(func())
```

    [0, 1, 2, 3, 4]
    


```python
a = []
def func1():
    for i in range(5):
        a.append(i)

func1()
print(a)
```

    [0, 1, 2, 3, 4]
    


```python
a = None
def bind_a_variable():
    global a
    a = []

bind_a_variable()
print(a)
```

    []
    

### 返回多个值

- 返回多个值实际上是返回一个`元组对象`,元组之后又被拆包为多个变量。


```python
def f():
    a = 5
    b = 6
    c = 7
    return a, b, c

a, b, c = f()
print(a, b, c)
```

    5 6 7
    


```python
return_value = f()
print(return_value)
```

    (5, 6, 7)
    


```python
def f():
    a = 5
    b = 6
    c = 7
    return {'a':a, 'b':b, 'c':c}

print(f())
```

    {'a': 5, 'b': 6, 'c': 7}
    

### 函数是对象

- Python的函数是对象


```python
states = ['   Alabama ', 'Georgia!', 'Georgia', 'georgia', 'FlOrIda',
          'south    carolina##', 'West virginia']
```


```python
import re

def clean_strings(strings):
    result = []
    for value in strings:
        value = value.strip()
        value = re.sub('[!#?]', '', value)
        value = value.title()
        result.append(value)
    return result

print(clean_strings(states))
```

    ['Alabama', 'Georgia', 'Georgia', 'Georgia', 'Florida', 'South    Carolina', 'West Virginia']
    


```python
def remove_punctuation(value):
    return re.sub('[!#?]', '', value)

clean_ops = [str.strip, remove_punctuation, str.title]

def clean_strings(strings, ops):
    result = []
    for value in strings:
        for function in ops:
            value = function(value)
        result.append(value)
    return result

clean_strings(states, clean_ops)
```




    ['Alabama',
     'Georgia',
     'Georgia',
     'Georgia',
     'Florida',
     'South    Carolina',
     'West Virginia']



### 匿名(Lambda)函数

- 匿名函数(lambda函数)是一种通过单个语句生成函数的方式，其结果总是返回值。
- 匿名函数总是使用关键字`lambda`定义
- 在很多案例中数据变形函数可以作为函数的参数，作为参数进行传值更加简单。
- `lambda`函数没有一个显示的`__name__`属性


```python
def short_function(x):
    return x*2

equiv_anon = lambda x : x*2
```


```python
# 列表中的函数值组成的一个新的列表
def apply_to_list(some_list, f):
    return [f(x) for x in some_list]

ints = [4, 0, 1, 5, 6]
print(apply_to_list(ints, lambda x : x*2))
```

    [8, 0, 2, 10, 12]
    


```python
strings = ['foo', 'card', 'bar', 'aaaa', 'abab']
strings.sort(key=lambda x : len(set(list(x))))
print(strings)
```

    ['aaaa', 'foo', 'abab', 'bar', 'card']
    

### 柯里化：部分参数应用

- 柯里化表示将通过部分参数应用的方式将已有的函数中衍生出新的函数
- 使用`functool`模块的`pratial`函数可以简化这种处理。


```python
# 将两个数加到一起
def add_numbers(x, y):
    return x+y

# 使用这个函数可以衍生出一个只有一个变量的函数
# 定义了一个新的函数`add_five`，且这个函数是调用应经存在的函数
add_five = lambda y: add_numbers(5, y)
```


```python
add_five(6)
```




    11




```python
from functools import partial 
add_five = partial(add_numbers, 5)
add_five(7)
```




    12



### 生成器

- 通过一致的方式遍历序列，如列表中的对象或者文件中的一行行内容，这个特性是基于迭代器协议来实现的。
- 迭代器协议是一种令对象可遍历的通用方式
- 生成器是构造新的可遍历对象的一种非常简洁的方式。
- 生成器返回一个多结果序列，在每一个元素产生之后暂停，直到下一个请求
- 创建一个生成器，将函数中将关键字`return`换为`yield`即可


```python
some_dict = {'a':1, 'b':2, 'c':3}
for key in some_dict:
    print(key)
```

    a
    b
    c
    


```python
def squares(n=10):
    print('Generating squares from 1 to {0}.'.format(n ** 2))
    for i in range(1, n+1):
        yield i**2
        
gen = squares()
print(gen)
```

    <generator object squares at 0x0000018A3892DF68>
    


```python
for x in gen:
    print(x, end = ' ')
```

    Generating squares from 1 to 100.
    1 4 9 16 25 36 49 64 81 100 

#### 生成器表达式

- 用生成器表达式来创建生成器更为简单
- 将列表推导式中的中括号`[]`换为`()`即可
- 在很多情况下，生成器表达式可以作为函数参数用于替代列表推导式


```python
gen = (x ** 2 for x in range(100))
print(gen)
```

    <generator object <genexpr> at 0x0000018A3892D3B8>
    


```python
# 与上面的生成器代码等价
def _make_gen():
    for i in range(100):
        yield x ** 2
        
gen = _make_gen()
```


```python
sum(x ** 2 for x in range(100))
```




    328350




```python
dict((i, i**2) for i in range(5))
```




    {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}



#### itertools模块

- 标准库中的`itertools`模块适用于大多数数据算法的生成器集合
- `groupby`可以根据任意的序列和一个函数，通过很熟的返回值对序列中连续的元素进行分组


```python
import itertools

first_letter = lambda x : x[0]
names = ['Alan', 'Adam',  'Wes', 'Will', 'Albert', 'Steven']
for letter, names in itertools.groupby(names, first_letter):
    print(letter, list(names))  # names是一个生成器
```

    A ['Alan', 'Adam']
    W ['Wes', 'Will']
    A ['Albert']
    S ['Steven']
    

一些有用的`itertools`函数

|函数|描述|
|:-|:-|
|combinations(iterable, k)|根据iterable参数中的所有元素生成一个包含所有可能K-元组的序列，忽略元素的顺序，也不进行替代(需要替代请参考函数combinations_with_replacement)|
|permutions(iterable, k)|根据iterable参数中的所有元素按顺序生成包含所有可能K元组的序列|
|groupby(iterable\[, keyfunc\]|根据每一个独一的key生成(key,subiterable)元组|
|product(\*iterablesm repeat=1) |以元组的形式，根据输入的可遍历对象生成笛卡尔积，与嵌套的for循环类似|

### 错误和异常处理

- 很多函数只能处理特定的输入,需要增加异常处理
- 通过讲多个异常类型写成元组的方式同时捕获多个异常(小括号是必不可少的)
- 一部分代码无论`try`代码块是否报错都要执行，则使用`finally`关键字


```python
float('1.2345')
```




    1.2345




```python
float('something')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-2-2649e4ade0e6> in <module>()
    ----> 1 float('something')
    

    ValueError: could not convert string to float: 'something'



```python
def attempt_float(x):
    try:
        return float(x)
    except:
        return x

print(attempt_float('1.2345'))
print(attempt_float('something'))
```

    1.2345
    something
    


```python
# float()还会抛出其他异常

float((2, 3))
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-4-e6712a6bea26> in <module>()
          1 # float()还会抛出其他异常
          2 
    ----> 3 float((2, 3))
    

    TypeError: float() argument must be a string or a number, not 'tuple'



```python
# 如果只想处理ValueError,需要在except后面指定
```


```python
def attempt_float(x):
    try:
        return float(x)
    except ValueError:
        return x
    
attempt_float((2, 3))
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-5-4c2e29b76014> in <module>()
          5         return x
          6 
    ----> 7 attempt_float((2, 3))
    

    <ipython-input-5-4c2e29b76014> in attempt_float(x)
          1 def attempt_float(x):
          2     try:
    ----> 3         return float(x)
          4     except ValueError:
          5         return x
    

    TypeError: float() argument must be a string or a number, not 'tuple'



```python
def attempt_float(x):
    try:
        return float(x)
    except (ValueError, TypeError):
        return x
```

```python
# f在程序结束之后总是关闭
f = open(path, 'w')
try:
    write_to_file(f)
finally:
    f.close()
```

```python
# 使用else表示try执行之后要执行的语句
f = open(path, 'w')
try:
    write_to_file(f)
except:
    print('Failed')
else:
    print('Succeeded')
finally:
    f.close()
```

#### IPython中的异常

- 如果正在使用`%run`执行一个脚本或者执行任何语句时报错，IPython将会默认打印出完整的调用堆栈跟踪(报错追溯),会将堆栈中每个错误点附近的几行上下文代码打印出
- 使用`-xmode`命令来控制上下文的数量。可以从`Plain`模式切换到`Verbose`(模式)显示函数的参数值以及更多的有用信息
- 错误发生之后使用`%debug`或者`%pdb`进入交互式调试


```python
%run ipython_bug.py
```


    ---------------------------------------------------------------------------

    AssertionError                            Traceback (most recent call last)

    D:\PythonCourse\Jupyter Notebook\Book\Python for Data Analysis\chap03\ipython_bug.py in <module>()
         13     throws_an_exception()
         14 
    ---> 15 calling_things()
    

    D:\PythonCourse\Jupyter Notebook\Book\Python for Data Analysis\chap03\ipython_bug.py in calling_things()
         11 def calling_things():
         12     works_fine()
    ---> 13     throws_an_exception()
         14 
         15 calling_things()
    

    D:\PythonCourse\Jupyter Notebook\Book\Python for Data Analysis\chap03\ipython_bug.py in throws_an_exception()
          7     a = 5
          8     b = 6
    ----> 9     assert(a + b == 10)
         10 
         11 def calling_things():
    

    AssertionError: 


## 文件和操作系统

- 打开文件进行读取，需要使用内建函数open和绝对、相对路径:
- 默认情况下，文件是以只读方式`'r'`打开的
- 行内容会在航结尾标识符`(EOF)`完整的情况下从文件中全部读出
- 当使用`open`创建文件对象时，在结束操作时显式的关闭文件非常重要，关闭文件会将资源放回操作系统
- 使用`with`语句，文件会在`with`代码块结束后自动关闭


```python
path = './segismundo.txt'
f = open(path)
for line in f:
    pass
```


```python
# 将文件中的内容读出形成不带`EOF`的列表
lines = [x.rstrip() for x in open(path)]
lines
```




    ['Sue帽a el rico en su riqueza,',
     'que m谩s cuidados le ofrece;',
     '',
     'sue帽a el pobre que padece',
     'su miseria y su pobreza;',
     '',
     'sue帽a el que a medrar empieza,',
     'sue帽a el que afana y pretende,',
     'sue帽a el que agravia y ofende,',
     '',
     'y en el mundo, en conclusi贸n,',
     'todos sue帽an lo que son,',
     'aunque ninguno lo entiende.',
     '']




```python
# 关闭文件
f.close()
```


```python
# 使用with语句自动关闭文件
with open(path) as f:
    lines = [x.rstrip() for x in f]
    
lines
```




    ['Sue帽a el rico en su riqueza,',
     'que m谩s cuidados le ofrece;',
     '',
     'sue帽a el pobre que padece',
     'su miseria y su pobreza;',
     '',
     'sue帽a el que a medrar empieza,',
     'sue帽a el que afana y pretende,',
     'sue帽a el que agravia y ofende,',
     '',
     'y en el mundo, en conclusi贸n,',
     'todos sue帽an lo que son,',
     'aunque ninguno lo entiende.',
     '']



- `read`方法通过读取的字节数来推进文件句柄所在的位置
- `tell`方法可以给出句柄当前的位置
- `seek`方法可以将句柄位置改变带文件中特定的字节


```python
f = open(path)
f.read(10)
```




    'Sue帽a el r'




```python
# 以二进制的形式打开
f2 = open(path, 'rb')

f2.read(10)
```




    b'Sue\xc3\xb1a el '




```python
print(f.tell())
print(f2.tell())
```

    11
    10
    


```python
import sys

sys.getdefaultencoding()
```




    'utf-8'




```python
print(f.seek(3))
print(f.read(1))
```

    3
    帽
    


```python
f.close()
f2.close()
```

Python文件模式

|模式|描述|
|:-|:-|
|r|只读模式|
|w|只写模式，创建新文件(清除路径下的同名文件中的数据)|
|x|只写模式,创建新文件(但存在同名路径时就会创建失败)|
|a|添加到已经存在的文件(如果不存在就创建)|
|r+|读写模式|
|b|二进制文件的模式，添加到别的模式中，比如'rb'或者'wb'|
|t|文件的文本模式(自动将字节解码为Unicode).如果没有指名模式，默认使用此模式，可以添加到别的模式中(比如'rt'或'xt')|


```python
with open('tmp.txt', 'w') as handle:
    handle.writelines(x for x in open(path) if len(x)>1)
```


```python
with open('tmp.txt') as f:
    lines = f.readlines()

lines    
```




    ['Sue帽a el rico en su riqueza,\n',
     'que m谩s cuidados le ofrece;\n',
     'sue帽a el pobre que padece\n',
     'su miseria y su pobreza;\n',
     'sue帽a el que a medrar empieza,\n',
     'sue帽a el que afana y pretende,\n',
     'sue帽a el que agravia y ofende,\n',
     'y en el mundo, en conclusi贸n,\n',
     'todos sue帽an lo que son,\n',
     'aunque ninguno lo entiende.\n']




```python
[x for x in open(path)]
```




    ['Sue帽a el rico en su riqueza,\n',
     'que m谩s cuidados le ofrece;\n',
     '\n',
     'sue帽a el pobre que padece\n',
     'su miseria y su pobreza;\n',
     '\n',
     'sue帽a el que a medrar empieza,\n',
     'sue帽a el que afana y pretende,\n',
     'sue帽a el que agravia y ofende,\n',
     '\n',
     'y en el mundo, en conclusi贸n,\n',
     'todos sue帽an lo que son,\n',
     'aunque ninguno lo entiende.\n',
     '\n']




```python
with open('segismundo.txt') as f:
    lines = f.readlines()
    
lines
```




    ['Sue帽a el rico en su riqueza,\n',
     'que m谩s cuidados le ofrece;\n',
     '\n',
     'sue帽a el pobre que padece\n',
     'su miseria y su pobreza;\n',
     '\n',
     'sue帽a el que a medrar empieza,\n',
     'sue帽a el que afana y pretende,\n',
     'sue帽a el que agravia y ofende,\n',
     '\n',
     'y en el mundo, en conclusi贸n,\n',
     'todos sue帽an lo que son,\n',
     'aunque ninguno lo entiende.\n',
     '\n']



重要的Python文件方法或属性

|方法|描述|
|:-|:-|
|read(\[size\])|将文件数据作为字符串返回。可选参数size控制读取的字节数|
|readlines(\[size\])|返回文件中行内容的列表,size参数可选|
|write(str)|将字符串写入文件|
|writelines(strings)|将字符串序列写入文件|
|close()|关闭文件|
|flush()|将内部的I/O缓冲器内容刷新到硬盘|
|seek()|移动到指定的位置(整数)|
|tell()|返回当前的文件位置，返回值是整数|
|closed|如果文件已关闭，则为True|

### 字节与Unicode文件

- 当从文件中请求一定量的字符时，Python从文件中读取了足够的字节(少至10字节，多至40字节)并进行解码。
- 只有每个已编码的Unicode字符是完整的情况下才能进行解码。
- 利用`open`方法的`encoding`选项参数，Python提供了一种方便的方法将文件内容从Unicode编码转换为其他类型的编码


```python
with open(path) as f:
    chars = f.read(10)
chars
```




    'Sue帽a el r'




```python
# 以只读二进制形式打开文件
with open(path, 'rb') as f:
    data = f.read(10)
data
```




    b'Sue\xc3\xb1a el '




```python
data.decode('utf8')
```




    'Sueña el '




```python
data[:4].decode('utf8')
```


    ---------------------------------------------------------------------------

    UnicodeDecodeError                        Traceback (most recent call last)

    <ipython-input-47-0ad9ad6a11bd> in <module>()
    ----> 1 data[:4].decode('utf8')
    

    UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc3 in position 3: unexpected end of data



```python
sink_path = 'sink.txt'
with open(path) as source:
    with open(sink_path, 'xt', encoding='iso-8859-1') as sink:
        sink.write(source.read())
        
with open(sink_path, encoding='iso-8859-1') as f:
    print(f.read(10))
```


    ---------------------------------------------------------------------------

    UnicodeEncodeError                        Traceback (most recent call last)

    <ipython-input-49-81123e98c93d> in <module>()
          2 with open(path) as source:
          3     with open(sink_path, 'xt', encoding='iso-8859-1') as sink:
    ----> 4         sink.write(source.read())
          5 
          6 with open(sink_path, encoding='iso-8859-1') as f:
    

    UnicodeEncodeError: 'latin-1' codec can't encode character '\u5e3d' in position 3: ordinal not in range(256)



```python
f= open(path)
f.read(5)
```




    'Sue帽a'




```python
f.seek(4)
```




    4




```python
f.read(1)
```




    '盿'


