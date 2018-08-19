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



#注意
1、类中的属性不能通过 类名.__dict__[] 或 类名.__dict__ = {} 的方式添加或修改。
   对象中的属性可以通过 对象名.__dict__[] 或 对象名.__dict__ = {} 的方式添加或修改。但是，第二种方法会删除对象原先中的所有直系的属性。
   直系属性：对象中存在，但对象所属的类中不存在的属性

2、一个对象可通过 对象名.__class__ = 新类名 的方式更改所属的类。更改后保留其直系属性

3、del 方法可删除对象的直系属性，但不能删除其父类的属性。当对象为其父类属性重新赋值后（哪怕 赋的新值 和 旧值 一样），父类属性会删除，但此对象的属性不会    删除。

4、在类的定义中可通过 __slots__ = ['属性名1', '属性名2',...] 限定对象新增的直系属性。对象只能添加列表中规定的属性，不能添加没有规定的属性

