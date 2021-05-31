# Python异常处理

## 1.Python中的异常

| 异常            | 描述                         |
| --------------- | ---------------------------- |
| **NameError**   | 访问未知的对象属性引发的错误 |
| **IndexError**  | 序列中没有此索引             |
| **ImportError** | import模块无法找到请求的模块 |
| **KeyError**    | 字典中没有该键               |
| **ValueError**  | 传入无效的参数               |

## 2.try-except结构

+ 先执行try中的语句，如果try中出现异常，会执行except中的语句，没有异常，except中内容不再执行。

```python
a=int(input('请输入整数a：'))
b=int(input('请输入整数b：'))
def fun(a,b):
    c=a/b
    return c
try:
    print(fun(a,b))
except ZeroDivisionError:
    print('除数不能为0')
except NameError:
    print('输入应为数字')
```

+ **try-expect-else**:如果try后语句没有异常，将执行else后语句，出现异常，不再执行else语句内的内容。

## 3.finally结构

+ 无论异常是否发生，都会运行finally后的语句。

## 4.异常抛出

```python
def fun(a,b):
    if a<10:
        raise ValueError('输出应大于10')
    c=a/b
    return c
try:
    print(fun(5,1))
except ValueError as error:
    print('出错了'，error)
```

## 5.自定义异常

```python
class ErrorName(Exception):
    block
```

