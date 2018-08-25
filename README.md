#生命周期
<实例计数>
class Person:
   count = 0
   def __init__(self):
      count += 1
   def __del__(self):
      count -= 1
   @classmethod
   def __log__(cls):
      print(cls.count)
p1 = Person()
p2 = Person()
p3 = Person()
del p2
Person.log()
输出：2



#垃圾回收
<1>引用计数器
import sys
class Person:
   pass
p1 = Person()
p2 = p1
print(sys.getrefcount(p1))
输出：3
解释：p2 = p1传递的是地址；在调用函数时p1又被引用一次，造成输出结果比实际引用次数大1

引用计数器增加：
1、p1 = Person
2、p1 = p2
3、对象作为一个参数传入到函数中，此时+2
4、对象作为一个元素，存储在容器中，如：l = [p1]
引用计数器减少：
1、引用对象被显式销毁，del p1
2、引用对象被赋予新的对象 p1 = 123
3、一个对象离开它的作用域
4、对象所在容器被销毁，或者从容器中移除该对象

import gc
启动 gc.enable()
停止 gc.disable()
判断 gc.isenabled()
查看参数  gc.get_threshold()
         例：输出（700，10，10）
         700代表阈值（对象引用数-消亡数），第一个10代表0代检测10次后触发0代和1代检测，第二个10代表1代检测10次后触发0代1代2代检测
设置参数  gc.set_threshold()
