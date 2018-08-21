#实例方法
class Person:
   def eat(self, food):
      print("在吃", food)

p = Person()
p.eat("屎")  //调用实例方法时不需要传入第一个参数self
Person.eat(123,456)
输出：在吃 屎
      在吃 456
附：
func1 = p.eat
func1(123)
func2 = Person.eat
func2(123, 456)
      
      
      
#类方法
class Person:
   @classmethod
   def leifangfa(cls, a)
   print("这是一个类方法", a)
   
p = Person()
p.leifangfa(123)
Person.leifangfa(456)
输出：这是一个类方法 123
      这是一个类方法 456
附：
func1 = p.leifangfa
func1(123)
func2 = Person.leifangfa
func2(456)



#受保护的属性  _a
受保护的属性访问权限：类和实例内部可以访问，一个程序内部（除类和实例）可以访问，但会警告。程序外部分情况：通过from import <具体内容>可以访问，通过from import *不能访问，如但果在上一个程序中说明 __all__ = ['变量名']，那么可以访问

#私有属性 __a
私有属性的访问权限：只能在类的内部访问，子类不能访问，一个程序的内部（除类和实例）不能访问。程序外部访问情况同 受保护的属性 _a 相同



#只读属性设置
<1>
思想：将属性设置为私有属性，构造一个读取函数，不构造写入函数
class Person:
  def __init__(self):
    self.__age = 10
  def getAge(self):
    return self.__age

<2> 在<1>的基础上的优化
class Person(object):
  def __init__(self):
    self.__age = 10
  @property //装饰器，可以 以使用属性的方法 来调用 这个方法
  def age(self):
    return self.__age
    
 p = Person()
 print(p.age)
 
 
 
#property在新式类中的应用————让私有属性如同正常属性一样调用
<1>
class Person(object):  //在python3中创建类时默认为object类，即新式类，括号可以省略；在python2中默认为经典类，加上括号才为新式类
   def __init__(self):
      self.__age = 18
   
   def get_age(self):
      return self.__age
   def set_age(self, value):
      self.__age = value
      
   age = property(get_age, set_age)

p = Person()
p.age = 10
print(p.age)

<2>
class Person(object):
   def __init__(self):
      delf.__age = 18
   
   @property
   def age(self):
      return self.__age
   
   @age.setter
   def age(self, value):
      self.__age = value
   
p = Person()
p.age = 10
print(p.age)
#注意
1、类中的属性不能通过 类名.__dict__[] 或 类名.__dict__ = {} 的方式添加或修改。
   对象中的属性可以通过 对象名.__dict__[] 或 对象名.__dict__ = {} 的方式添加或修改。但是，第二种方法会删除对象原先中的所有直系的属性。
   直系属性：对象中存在，但对象所属的类中不存在的属性

2、一个对象可通过 对象名.__class__ = 新类名 的方式更改所属的类。更改后保留其直系属性

3、del 方法可删除对象的直系属性，但不能删除其父类的属性。当对象为其父类属性重新赋值后（哪怕 赋的新值 和 旧值 一样），父类属性会删除，但此对象的属性不会    删除。

4、在类的定义中可通过 __slots__ = ['属性名1', '属性名2',...] 限定对象新增的直系属性。对象只能添加列表中规定的属性，不能添加没有规定的属性

5、python中的私有属性是伪私有属性，可以通过其他手段访问。其原理是程序编译时改变了私有属性的名字，不同的编译器采用的方式不一样

6、命名方式：当变量名与关键字冲突时，习惯上可采用关键字_,如：class_, int_
            __xx__是系统内置的一些命名，自己命名时应避免

