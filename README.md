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
 
<3>class Person:
  #当我们通过“ 实例.属性 = 值 ” 给一个实例增加一个属性，或者，修改这个属性值的时候，都会调用这个方法
  #在这个方法内部，才会真正的把这个属性以及对应的数据添加到字典__dict__中
  def __setattr__(self, key, value):
     if key == 'age' and key in self.__dict__.keys():
        print("这个属性是只读属性，不能设置数据")
     else:
        self.__dict__[key] = value
        #注意：上面不能写成 self.key = value，否则会一直调用这个方法造成死循环
 p = Person()
 p.age = 18
 print(p.age)  输出：18
 p.age = 999   //设置失败
 print(p.age)  输出：18
 
 
 
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



#内置函数
<1> def __init__(self, 参数1，参数2，...) 用于初始化

<2> def __str__   return "字符串" 用于更改print(实例/对象)的输出信息

<3> def __repr__ return "字符串"  用于更改repr(对象/实例)的输出信息，当__str__没有重新定义时，也会改变print(对象/实例)的输出信息

<4> __call__ 是对象具备当作函数调用的能力
class Person:
   def __call__(self, *args, **kwargs):
      print("xxx", args, kwargs)
p = Person()
p(123,456, name='sz')
输出：xxx (123, 456) {'name':'sz}

实例：一个参数（笔的类型）变化较少，另一个参数（笔的颜色）变化较多
class PenFactory:
   def __init__(self, p_type):
      self.p_type = p_type
   def __call__(self, p_color):
      print("创建了类型为 %s 的画笔，颜色为 %s" % (self.p_type, p_color))
gangbiF = PenFactory("钢笔")
gangbiF("黄色")
gangbiF("红色")
gangbiF("绿色")
qianbiF = PenFactory("铅笔")
qianbiF("蓝色")
qianbiF("紫色")
qianbiF("灰色")
输出：
创建了 钢笔 类型的画笔，颜色为 黄色
创建了 钢笔 类型的画笔，颜色为 红色
创建了 钢笔 类型的画笔，颜色为 绿色
创建了 铅笔 类型的画笔，颜色为 蓝色
创建了 铅笔 类型的画笔，颜色为 紫色
创建了 铅笔 类型的画笔，颜色为 灰色

<5>索引操作：__set/get/delitem__
class Person:
   def __init__(self):
      self.cache = {}
   def __setitem__(self, key, value):
      print("setitem", key, value)
      self.cache[key] = value
   def __getitem__(self,item)
      print("getitem", item)
      return self.getitem[item]
   def __delitem__(self, key)
      print("delitem", key)
      del self.cache[key]
p = Person()
p['name'] = 'nb'
name = p['name']
print(name)
del p['name']
print(p.cache)
输出：
setitem name nb
getitem name
nb
delitem name
{}

<6>切片操作： __set/get/delitem__  //只能修改，不能新增
class Person:
   def __init__(self):
      self.items = [1, 2, 3, 4, 5, 6]
   def __setitem(self, key, value):
      self.items[key] = value
   def __getitem(self, item):
      return self.items[item]
   def __delitem(self, key)
      del self.items[key]
p = Person()
p[0:4:2] = ['a', 'b']
print(p[0:6])
del p[4:6]
print(p)
print(p.items)
输出：
['a', 2, 'b', 4, 5, 6]
['a', 2, 'b', 4]

<7>比较操作
Ⅰ
class Person:
   def __init__(self, age):
      self.age = age
   def __eq__(self, other):
      return self.age == other.age
   def __ne__(self, other):
      return self.age != other.age
   def __gt__(self, other):
      return self.age > other.age
   def __ge__(self, other):
      return self.age >= other.age
   def __lt__(self, other):
      return self.age < other.age
   def __le__(self, other):
      return self.age <= other.age
p1 = Person(18)
p2 = Person(17)
print(p1>p2)
输出：True

Ⅱ
import functools
@functools.total_ordering
class Person:
   def __init(self, age):
      self.age = age
   def __eq__(self, other):
      self.age = other.age
   def __gt__(self, other):
      self.age > other.age
解释：这个装饰器可以根据已写的比较规则来生成其他比较规则。"==" 和 "!="，可以相互生成；">"、"<"、">="、"<="可以相互生成。因此，要生成全部的6个比较规       则，至少要编写两个



<8>条件语句中的应用 __bool__(self)
class Person:
   def __bool__(self):
      return True
p = Person()
if p  //条件成立

class Person:
   age = 20
   def __bool__(self)
      return age > 18
p = Person()
if p  //条件成立

综上，__bool__(self)函数的返回值会替代if中的实例
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


7、私有化方法和私有化属性命名方式相同，伪装的原理相同
