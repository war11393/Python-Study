## Python短代码

### 今天给大家带来一些30秒就能学会的代码片段，这些代码潜力无限，蕴含了丰富的python编程思维，应用领域非常广泛，而且学起来非常简单。

**1."二维列表"**

**解读：**根据给定的长和宽，以及初始值，返回一个二维列表。

```
def initialize_2d_list(w, h, val=None):
    return [[val for x in range(w)] for y in range(h)]
```



**例：**

```
>>> initialize_2d_list(2,2)
[[None, None], [None, None]]

>>> initialize_2d_list(2,2,0)
[[0, 0], [0, 0]]
```



**2.函数切割数组**

**解读：**使用一个函数应用到一个数组的每个元素上，使得这个数组被切割成两个部分。如果说，函数应用到元素上返回的值为True，则该元素被切割到第一部分，否则分为第二部分。

```
def bifurcate_by(lst, fn):
    return [
      [x for x in lst if fn(x)],
      [x for x in lst if not fn(x)]
    ]
```



**例：**

```
>>> bifurcate_by(['beep', 'boop', 'foo', 'bar'], lambda x: x[0] == 'b')
[['beep', 'boop', 'bar'], ['foo']]
```



**3."交集点"**

**解读：** 两个数组在被一个函数应用后，从第一个数组中提取出共有的元素的**原元素**组成一个新的数组。

```
def intersection_by(a, b, fn):
    _b = set(map(fn, b))
    return [item for item in a if fn(item) in _b]
```



**例：**

```
>>> from math import floor
>>> intersection_by([2.1, 1.2], [2.3, 3.4],floor)
[2.1]
```



**4.最大值下标**

**解读：**返回数组中最大值的下标。

```
def max_element_index(arr):
    return arr.index(max(arr))
```



**例：**

```
>>> max_element_index([5, 8, 9, 7, 10, 3, 0])
4
```



**5.数组对称差**

**解读：**找出两个数组中不同的元素，并合成为一个新的数组。

```
def symmetric_difference(a, b):
    _a, _b = set(a), set(b)
    return [item for item in a if item not in _b] + [item for item in b if item not in _a]
```



**例：**

```
>>> symmetric_difference([1, 2, 3], [1, 2, 4])
[3, 4]
```



**6."夹数"**

**解读：**如果 num 落在一段数字范围内，则返回num，否则返回离这个范围最近的边界：

```
def clamp_number(num,a,b):
    return max(min(num, max(a,b)),min(a,b))
```



**例：**

```
>> clamp_number(2,3,10)
3

>> clamp_number(7,3,10)
7

>> clamp_number(124,3,10)
10
```



**7.键值映射**

**解读：**使用对象的键重新创建对象，并运行函数为每个对象的键创建值。
使用dict.keys()遍历对象的键， 通过函数生成一个新的值。

```
def map_values(obj, fn):
    ret = {}
    for key in obj.keys():
        ret[key] = fn(obj[key])
    return ret
```



**例：**

```
>>> users = {
...   'fred': { 'user': 'fred', 'age': 40 },
...   'pebbles': { 'user': 'pebbles', 'age': 1 }
... }

>>> map_values(users, lambda u : u['age'])
{'fred': 40, 'pebbles': 1}

>>> map_values(users, lambda u : u['age']+1)
{'fred': 41, 'pebbles': 2}
```



**8.大小写转换**

**解读：** 将英文单词的首字母大写改为小写。
upper_rest参数：设定是否将除首字母外的其他字母大小写转换。

```
def decapitalize(s, upper_rest=False):
    return s[:1].lower() + (s[1:].upper() if upper_rest else s[1:])
```



**例：**

```
>>> decapitalize('FooBar')
'fooBar'

>>> decapitalize('FooBar', True)
'fOOBAR'
```



**9.同键求和**

**解读：**对列表中的各个字典里相同键值的对象求和。

```
def sum_by(lst, fn):
    return sum(map(fn,lst))
```



**例：**

```
>>> sum_by([{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }], lambda v : v['n'])
14
```



**10.一行代码求出现次数**

**解读：**求出列表中某个数出现的次数和。

```
def count_occurrences(lst, val):
    return len([x for x in lst if x == val and type(x) == type(val)])
```



**例：**

```
>>> count_occurrences([1, 1, 2, 1, 2, 3], 1)
3
```



**11.数组再分组**

对一个列表根据所需要的大小进行细分：

![图片](https://mmbiz.qpic.cn/mmbiz_png/h6NqozYcCQ7Pxf8s47QVz0cvMzj6bOkTlyTyib5jYzRPUaOY6Nt0ED7B3ibPjWhrI0ewybh3H0XgakGEU8ut9InQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

```
chunk([1,2,3,4,5],2)
# [[1,2],[3,4],5]
```



return中，map的第二个参数是一个列表，map会将列表中的每一个元素用于调用第一个参数的 function 函数，返回包含每次 function 函数返回值的新列表。



**12.数字转数组**

同样是一则关于map的应用，将整形数字拆分到数组中：

```
def digitize(n):
    return list(map(int, str(n)))
```



效果如下：

```
digitize(123)
# [1, 2, 3]
```



它将整形数字n转化为字符串后，还自动对该字符串进行了序列化分割，最后将元素应用到map的第一个参数中，转化为整形后返回。

**13.非递归斐波那契**

还记得斐波那切数列吗，前两个数的和为第三个数的值，如0、1、1、2、3、5、8、13....

如果使用递归来实现这个算法，效率非常低下，我们使用非递归的方式实现：

![图片](https://mmbiz.qpic.cn/mmbiz_png/h6NqozYcCQ7Pxf8s47QVz0cvMzj6bOkTIOekHD8iaWSK7Lxfmiby9xrBffUewb9AGG6YhAR5icj51xyUXSJmmQ5Mg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

```
fibonacci(7)
# [0, 1, 1, 2, 3, 5, 8, 13]
```



这样看是很简单，但是思维要绕的过来哦。

**14.下划线化字符串**

批量统一变量名称或者字符串格式。

![图片](https://mmbiz.qpic.cn/mmbiz_png/h6NqozYcCQ7Pxf8s47QVz0cvMzj6bOkTZv596VOBicP833rhBaHJSK93u98tcvZriayyFdptThgrYfsvIYc1X15Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

```
snake('camelCase')# 'camel_case'

snake('some text')# 'some_text'

snake('some-mixed_string With spaces_underscores-and-hyphens')# 'some_mixed_string_with_spaces_underscores_and_hyphens'

snake('AllThe-small Things')# "all_the_small_things"
```


re.sub用于替换字符串中的匹配项。这里其实是一个“套娃”用法，一开始可能不太好理解，需要慢慢理解。

**第一个替换**，是将s字符串中，使用' '替换'-'。

**第二个替换**，是针对第一个替换后的字符串，对符合'([A-Z]+)'正则表达式的字符区段（全大写的单词）用r' \1'替换，也就是用空格区分开每一个单词。

**第三个替换**，是对第二个替换后的字符串，对符合'(\[A-Z][a-]+)'正则表达式的字符区段（也就是首字母大写，其他字母小写的词语）用r' \1'替换，也是将单词用空格分隔开。

