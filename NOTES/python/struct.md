#### struct 模块学习

[Python官方参考文档](https://docs.python.org/2/library/struct.html#struct-format-strings)

#### 用处

- 按照指定格式将Python数据转换为字符串，该字符串为字节流，如在网络传输中，不能传输int类型，此时就需要将int转换为字节流再发送
- 按照指定格式将字节流转换为Python指定数据库类型
- 用struct处理二进制文件，需要用‘wb’, ‘rb’读取二进制
- 处理C语言结构体

#### 模块中的函数

| function                              | return      | explain                                  |
| ------------------------------------- | ----------- | ---------------------------------------- |
| pack(fmt, v1, v2)                     | string      | 按照给定的fmt格式，将数据转换为字符串(字节流),并将该字符串返回       |
| pack_into(fmt, buffer, offset,v1, v2) | None        | 按照给定fmt格式将数据转换为字符串，并将字节流写入以offset开始的buffer中(buffer为可写缓冲区，可用array模块) |
| unpack(fmt, v1, v2)                   | tuple       | 按照给定fmt格式解析字节流，并返回结果                     |
| pack_from(fmt, buffer, offset)        | tuple       | 按照给定的格式解析以offset开始的缓存区，并返回解析结果           |
| calcsize(fmt)                         | size of fmt | 计算给定格式占用多少字节的内存，注意对齐方式                   |

#### 对齐方式

为了同c中的结构体交换数据，还要考虑c或者C++编译器使用了字节对齐，通常是以4个字节为单位的32位系统，故而struct根据本地机器字节顺序转换，可用格式中国的第一个字符来改变对齐方式，定义如下：

| Character  | byte order  | size | alignment  |
| ---------- | ----------- | ---- | ---------- |
| @(default) | 本机          | 本机   | 本机， 凑够4字节  |
| =          | 本机          | 标准   | none，按原字节数 |
| <          | 小端          | 标准   | none，按原字节数 |
| >          | 大端          | 标准   | none，按原字节数 |
| ！          | network(大端) | 标准   | none，按原字节数 |

#### 格式符

| 格式符     | C语言类型              | Python类型           | Standard size |
| ------- | ------------------ | ------------------ | ------------- |
| x       | pad byte(填充字节)     | no value           |               |
| c       | char               | string of length 1 | 1             |
| b       | signed char        | integer            | 1             |
| B       | unsigned char      | integer            | 1             |
| ?       | _Bool              | bool               | 1             |
| h       | short              | integer            | 2             |
| H       | unsigned short     | integer            | 2             |
| i       | int                | integer            | 4             |
| I(大写的i) | unsigned int       | integer            | 4             |
| l(小写的L) | long               | integer            | 4             |
| L       | unsigned long      | long               | 4             |
| q       | long long          | long               | 8             |
| Q       | unsigned long long | long               | 8             |
| f       | float              | float              | 4             |
| d       | double             | float              | 8             |
| s       | char[]             | string             |               |
| p       | char[]             | string             |               |
| P       | void *             | long               |               |

> note:
>
> 1. _Bool在C99中定义,如果没有这个类型,则将这个类型视为char,一个字节;
> 2. q和Q只适用于64位机器;
> 3. 每个格式前可以有一个数字,表示这个类型的个数,如s格式表示一定长度的字符串,4s表示长度为4的字符串;4i表示四个int;
> 4. P用来转换一个指针,其长度和计算机相关;
> 5. f和d的长度和计算机相关;

#### 代码实例

```python
#!/usr/bin/python
# -*- coding:utf-8 -*-
'''测试struct模块'''
from struct import *
import array

def fun_calcsize():
    print 'ci:',calcsize('ci')#计算格式占内存大小
    print '@ci:',calcsize('@ci')
    print '=ci:',calcsize('=ci')
    print '>ci:',calcsize('>ci')
    print '<ci:',calcsize('<ci')
    print 'ic:',calcsize('ic')#计算格式占内存大小
    print '@ic:',calcsize('@ic')
    print '=ic:',calcsize('=ic')
    print '>ic:',calcsize('>ic')
    print '<ic:',calcsize('<ic')

def fun_pack(Format,msg = [0x11223344,0x55667788]):
    result = pack(Format,*msg)
    print 'pack'.ljust(10),str(type(result)).ljust(20),
    for i in result:
        print hex(ord(i)), # ord把ASCII码表中的字符转换成对应的整形,hex将数值转化为十六进制
    print

    result = unpack(Format,result)
    print 'unpack'.ljust(10),str(type(result)).ljust(20),
    for i in result:
        print hex(i),
    print 

def fun_pack_into(Format,msg = [0x11223344,0x55667788]):
    r = array.array('c',' '*8)#大小为8的可变缓冲区,writable buffer
    result = pack_into(Format,r,0,*msg)
    print 'pack_into'.ljust(10),str(type(result)).ljust(20),
    for i in r.tostring():
        print hex(ord(i)),
    print

    result = unpack_from(Format,r,0)
    print 'pack_from'.ljust(10),str(type(result)).ljust(20),
    for i in result:
        print hex(i),
    print

def IsBig_Endian():
    '''判断本机为大/小端'''
    a = 0x12345678
    result = pack('i',a)#此时result就是一个string字符串，字符串按字节同a的二进制存储内容相同。
    if hex(ord(result[0])) == '0x78':
        print '本机为小端'
    else:
        print '本机为大端'

def test():
    a = '1234'
    for i in a:
        print '字符%s的二进制:'%i,hex(ord(i))#字符对应ascii码表中对应整数的十六进制

    '''
    不用unpack()返回的数据也是可以使用pack()函数的,只要解包的字符串符合解包格式即可,
    pack()会按照解包格式将字符串在内存中的二进制重新解释(说的感觉不太好...,见下例)
    '''
    print '大端:',hex(unpack('>i',a)[0])#因为pack返回的是元组,即使只有一个元素也是元组的形式
    print '小端:',hex(unpack('<i',a)[0])


if __name__ == "__main__":
    print '判断本机是否为大小端?',
    IsBig_Endian()

    fun_calcsize()

    print '大端:'
    Format = ">ii"
    fun_pack(Format)
    fun_pack_into(Format)

    print '小端:'
    Format = "<ii"
    fun_pack(Format)
    fun_pack_into(Format)

    print 'test'
    test()
    '''
    result:
    判断本机是否为大小端? 本机为小端
    ci: 8
    @ci: 8
    =ci: 5
    >ci: 5
    <ci: 5
    ic: 5
    @ic: 5
    =ic: 5
    >ic: 5
    <ic: 5
    大端:
    pack       <type 'str'>         0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88
    unpack     <type 'tuple'>       0x11223344 0x55667788
    pack_into  <type 'NoneType'>    0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88
    pack_from  <type 'tuple'>       0x11223344 0x55667788
    小端:
    pack       <type 'str'>         0x44 0x33 0x22 0x11 0x88 0x77 0x66 0x55
    unpack     <type 'tuple'>       0x11223344 0x55667788
    pack_into  <type 'NoneType'>    0x44 0x33 0x22 0x11 0x88 0x77 0x66 0x55
    pack_from  <type 'tuple'>       0x11223344 0x55667788
    test
    字符1的二进制: 0x31
    字符2的二进制: 0x32
    字符3的二进制: 0x33
    字符4的二进制: 0x34
    大端:0x31323334
    小端:0x34333231
    '''
```

