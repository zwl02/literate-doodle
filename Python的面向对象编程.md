# Python的面向对象编程

## 面向对象

+ 类提供了一种将数据和功能捆绑在一起的方法。创建一个新类即创建一个新类型的可创建新实例的对象。每个类的实例都可以有其附加的属性。

+ Python的类机制可以以最少的新语法和语义来新建类。
+ Python类提供了面向对象编程的所有标准的特征。
  + 类继承机制允许多个基类。
  + 派生类可以重载其基类或类的任何方法，并且其方法可以调用基类中具有相同名称的方法。

## 类与对象

### 1.相关术语

* **类(Class):** 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。
* **对象：**通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。
* **类变量：**类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。
* **实例变量：**在类的声明中，属性是用变量来表示的，这种变量就称为实例变量，实例变量就是一个用 self 修饰的变量。
* **数据成员：**类变量或者实例变量用于处理类及其实例对象的相关的数据。
* **方法：**类中定义的函数。
* **方法重写：**如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。

### 2.类的定义

```python
class Student(object):

	pass
```

### 3.对象的创建

#### 3.1对象的创建

* 类对象支持两种操作：属性引用和实例化。

* 属性引用使用和 Python 中所有的属性引用一样的标准语法：**obj.name**。

* 类实例化使用函数表示法。

  * ```python
    x=Student()
    #以上创建了该类的新实例并将该对象分配给局部变量x，x为空的对象。
    ```

* 当一个类定义了_ int _()方法时,类实例会自动为新创建的类实例调用。

#### 3.2对象实例化

* 实例对象理解的唯一操作是属性引用。有两种有效的属性名称，数据属性和方法属性。

### 4.类的方法

+ 在类的内部，使用 **def** 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 self, 且为第一个参数，self 代表的是类的实例。

```python
#类定义
class people:
    #定义基本属性
    name = ''
    age = 0
    #定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0
    #定义构造方法
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s 说: 我 %d 岁。" %(self.name,self.age))
 
# 实例化类
p = people('runoob',10,30)
p.speak()
```

+ 两个下划线开头，声明该方法为私有方法，只能在类的内部调用 ，不能在类的外部调用。

## 继承

+ 通过继承机制可以实现代码的重用。

+ 子类（派生类）会继承父类（基类）的属性和方法。

+ ```python
  class Parent:#定义父类
      parentAttr=90
      def _init_(self):
          print("调用父类构造函数")
      def parentMethod(self):
          print("调用父类方法")
      def setAttr(self,attr):
          Parent.parentAttr=attr
      def getAttr(self):
          print("父类属性:",Parent.parentAttr)
  class Child(Parent):#定义子类
      def _init_(self):
          print("调用子类构造方法")
          Parent._init_(self)
      def childMethod(self):
          print("调用子类方法")
          Parent.parentMethod(self)
  c=Child()			#实例化子类
  c.childMethod()		#调用子类的方法
  c.parentMethod()	#调用父类的方法
  c.setAttr(100)		#再次调用父类的方法 设置属性
  c.getAttr()			#再次调用父类的方法 获取属性
  ```

+ **方法重写**：如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法。

+ **多态**：即使不知道一个变量所引用的对象到底是什么类型，仍然可以通过这个变量调用方法，在运行过程中根据变量所引用对象的类型，动态决定调用哪个对象中的方法。

+ **多重继承**：通过多重继承，一个子类就可以同时获得多个父类的所有功能。

```python
class Beef(Meat,Expensive)
```

