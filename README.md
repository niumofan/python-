#1 模式
r：只读，指针在开头，不能创建文件
w：只写，覆盖写，原内容会消失，指针在开头，可以创建文件
a：追加写，指针在结尾，可以创建文件
b：打开二进制文件，如图片，视频......
r+：读写，不能创建文件，指针在开头，写入时会覆盖所写长度的内容，如：原来：123456，写入：ab，结果：ab3456
w+:可读写，其他同w一样


#2 方法
open()  //其中可加参数encoding表示编码方式，如：encoding = "utf-8"
f.tell()  //返回当前指针的位置
f.seek(a,b) //移动指针，a表示偏移量，正右负左；b代表相对位置，0为开头（此时a不能为负，默认），1为当前位置，2为结尾（此时a不能为正）
f.readline()  //读一行
f.realines()  //读取所有行，每一行作为一个元素加入列表中
f.readable()  //检测文件是否可读
f.writable()  //检测文件是否可写
f.write() //可以返回写入的长度
f.flush //将缓冲区清空

os.rename(jiu, xin) //将文件或文件夹重命名，单级修改，即只能改动一个
例：os.rename("one.txt", "two.txt")
os.renames(jiu, xin)  //将文件和文件夹重命名，可以将一个路径上的所有文件或文件夹重命名
例：os.renames("one/one.txt", "two/two.txt")
os.remove(src)  //将文件删除
os.rmdir(dir) //将空文件夹删除
os.removedirs(dir)  //将路径上的所有空文件夹删除，直到遇到非空文件夹为止
os.mkdir(dir,0oxxx) //创建一个文件夹，不能同时创建多个。0oxxx表示访问权限，从左到右分别代表 文件拥有者、同组用户、其他用户 的访问权限；可读为4，可                       写为2，可执行为1，如0o777表示 文件拥有者、同组用户、其他用户 既可读，又可写，又可执行
os.getcwd() //获得当前目录
os.chdir(dir) //改变工作目录
os.listdir(dir) //获取dir中文件内容组成的列表。当dir为
os.path.isdir(dir)  //判断是否是目录
os.path.isfile(file)  //判断是否是文件



#3 文件复制 //以下均为例子
<1> 只能复制小文件，复制大文件内存会爆炸
from_file = open("1.png", "rb")
to_file = open("../copy.png", "wb")
content = from_file.read()
to_file.write(content)
from_file.close()
to_file.close()

<2> 可以复制大文件，方法为分次读取
from_file = open("1.png", "rb")
to_file = open("1/1.png", "wb")
while True:
  content = from_file.read(1024)
  if len(content) == 0:
    break
  to_file.write(content)
from_file.close()
to_file.close()



#4 文件移动 //以下均为例子
<1>将文件按后缀存放在不同文件夹中，文件夹按后缀命名
import os
import shutil

dirpath = "E:/Pycharm/程序"

if not os.path.exists(dirpath):
  exit()

name_list = os.listdir(dir)

for name in name_list:
  index = name.rfind('.')
  if index == -1:
    continue
  dir = name[index+1:]
  path = dir+'/'+name
  if not os.path.exists(dir):
    os.mkdir(dir)
  shutil.move(name, path)
附：容错处理一般反写，防止后面大片代码缩进



#5 列表清单，打印文件夹中的 文件 以及 子文件夹中的文件
<1>打印到屏幕上
def list_files(dir, count=0):
  filelist = os.listdir(dir)
  
  for filename in filelist:
    print('\t'*count)
    path = dir + '/' + filename
    if os.path.isdir(path):
      print(path)
      list_files(path, count+1)
    else:
      print(filename)
   
   dir_path = input("请输入路径：")
   list_files(dir_path)

<2>写入到文本文件中
import  os

def listFiles(dir, file, count=0):
    file_list = os.listdir(dir)
    for filename in file_list:
        file.write('\t'*count)
        path = dir + '/' + filename
        if os.path.isdir(path):
            file.write(path+'\n')
            listFiles(path, file, count+1)
        else:
            file.write(filename+'\n')

dir_path = input("请输入路径:")
file = open("try.txt", "a", encoding='gb2312')
listFiles(dir_path, file)

#3 注意
大文件读取，read()占内存，但效率高；for in省内存，但效率低；readline()折中
