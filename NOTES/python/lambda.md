### lambda表达式使用规则

#### lambda即为函数的一种简单表达方式

```python
# 普通函数

def func(arg):
  return arg+1

res = func(12)

# lambda
my_lambda = lambda arg : arg+1
res = my_lambda(12) 
```

#### 内置函数

##### map

>  遍历序列，对序列中每一个元素进行操作

```pyt
li = [1, 2, 3]
new_list = map(lambda a: a+100, li)
```

```python
li = [1, 2, 3]
ls = [4, 5, 6]
new_list = map(lambda a,b: a+b, li, ls)
```

```python
# 列表解析可实现和map同样功能，往往速度快于map
print [x**2 for x in range(10)]
print map((lambda x: x**2), range(10))

# 列表解析往往更加强大
print [x+y for x in range(5) if x%2 == 0 for y in range(10) if y%2 ==1]  
```



#### filter

> 对序列元素进行筛选，最终获得符合条件的序列

```python
li = [1, 2, 3]
new_list = filter(lambda arg: arg>22, li)

# filter 第一个参数为空则返回原序列
```

##### reduce

> 对序列元素进行累积操作

```python
li = [1, 2, 3]

res = reduce(lambda arg1, arg2: arg1+arg2, li)

# reduce的第一个参数，函数必须要有两个参数
# reduce第二个参数为循环的序列
# reduce第三个参数为初始值
```













