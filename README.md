#1 偏函数  给某些变量固定一个值，即“偏爱”这些值
<1>
import functools)

def add(a,b,c,d=1):
  print(a+b+c+d)

newfunc = functools.partial(add, c=5)   //c固定为5，调用函数时不能更改，否则报错
newfunc(1,2)      //输出：9
newfunc(1,2,3)    //报错
newfunc(1,2,3,4)  //报错
newfunc(1,2,d=3)  //输出：11


<2>
def add(a,b,c,d=1):
  print(a+b+c+d)

def add2(a,b,c=2,d=3):
  add(a,b,c,d)
  
add2(a=1,b=2)
输出：8


<应用>
import functools
int2 = functools.partial(int, base=2)   //构造一个将二进制转换为十进制的函数
print(int2(100010))
输出：34



#2 高阶函数   函数的参数是其他函数
def sum(a,b):
  return a+b
 
def dif(a,b)
  return a-b

def cal(a,b,func):
  print(func(a,b))

cal(10,7,sum) //输出：17
cal(10,7,dif) //输出：3



#3 返回函数   返回值为函数
def get_func(c):
  def sum(a,b):
    return a+b
  def dif(a,b):
    return a-b
    
  if c == '+':
    return sum
  else:
    return dif
    
  func = get_func('+')
  print(func(5,3))
  输出：8
  

#4 闭包  外层函数 根据不同的参数 生成作用不同的函数
def test():                                                                     
  a = 10
  def test2():
    print(a)
  return test2
  
fun = test()  
fun()
输出：10

<应用>
def print_line(content, length):
  def line():
    print('-'*(length//2) + content + '-'*(length//2))
  return line

line1 = print_line("我是分割线", 20)
line2 = print_line("啦啦啦",50)
line1()
line1()
line2()

输出：
----------我是分割线----------
----------我是分割线----------
-------------------------啦啦啦-------------------------


<注意>
①内部函数直接赋值不能改变外部函数变量，除非用关键字nonlocal声明，且声明同时不能赋值
def test():
    num = 10
    def test2():
        num = 20
    print(num)
    test2()
    print(num)

test()
输出：10
      10

def test():
    num = 10
    def test2():
        nonlocal num
        num = 20
    print(num)
    test2()
    print(num)

test()
输出：10
      20



②注意内部函数起作用的时间
<1>
def test():
    funs = []
    for i in range(4):
        def test2():
            print(i, end=' ')
        funs.append(test2)
    return funs

new_fun = test()
new_fun[0]()
new_fun[1]()
new_fun[2]()
new_fun[3]()
输出：3 3 3 3

<2>
def test():
    funs = []
    for i in range(4):
        def test2(num):
            def inner():
                print(num，end=' ')
            return inner
        funs.append(test2(i))
    return funs

new_fun = test()
new_fun[0]()
new_fun[1]()
new_fun[2]()
new_fun[3]()
输出：0 1 2 3



#5 装饰器————闭包的应用     减少代码冗余度，提示信息修改方便且无需修改主过程
def checkLogin(func):
  def inner():
    print("登陆验证...")
    func()
  return inner

@checkLogin       //函数体前加@checkLogin相当于函数体后加fss = checkLogin(fsss)
def fss():
  print("发说说")

@checkLogin
def ftp():
  print("发图片")

btnIndex = 1
if btnIndex == 1:
  fss()
else:
  ftp()
输出：
登陆验证...
发说说


#附
numstr = "10010"
result = int(numstr, base=2)  //以二进制转换
print(result)
输出：18
