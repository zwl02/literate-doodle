# C语言查缺补漏

## 运算符

### 逻辑运算符

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| &&     | 称为逻辑与运算符。如果两个操作数都非零，则条件为真。         |
| \|\|   | 称为逻辑或运算符。如果两个操作数中有任意一个非零，则条件为真。 |
| ！     | 称为逻辑非运算符。用来逆转操作数的逻辑状态。如果条件为真则逻辑非运算符将使其为假。 |

### 位运算符

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| &      | 按位与操作，按二进制位进行"与"运算。                         |
| \|     | 按位或运算符，按二进制位进行"或"运算。                       |
| ^      | 异或运算符，按二进制位进行"异或"运算。两值不同时为1，相同时为0。 |
| ~      | 取反运算符，按二进制位进行"取反"运算。                       |
| <<     | 二进制左移运算符。将一个运算对象的各二进制位全部左移若干位（左边的二进制位丢弃，右边补0）。 |
| >>     | 二进制右移运算符。将一个数的各二进制位全部右移若干位，正数左补0，负数左补1，右边丢弃。 |

### 杂项运算符

| 运算符   | 描述                                               |
| -------- | -------------------------------------------------- |
| sizeof() | 返回变量的大小。                                   |
| &        | 返回变量的地址。                                   |
| *        | 指向一个变量。                                     |
| ? :      | 条件表达式。如果条件为真 ? 则值为 X : 否则值为 Y。 |

## 结构体

### 定义

```c
struct tag { //结构体标签
    member-list//标准的变量定义
    member-list 
    member-list  
    ...
} variable-list ;//结构变量
struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
} book = {"C 语言", "RUNOOB", "编程语言", 123456};//赋初值
```

### 访问

+ 使用**成员访问运算符（.）**

### 指向结构的指针

```c
struct Books *struct_pointer;//定义指向结构的指针
struct_pointer = &Book1;//查找结构变量的地址
struct_pointer->title;//使用指向该结构的指针访问结构的成员
```

