#1 模式
r：只读，指针在开头，不能创建文件
w：只写，覆盖写，原内容会消失，指针在开头，可以创建文件
a：追加写，指针在结尾，可以创建文件
b：打开二进制文件，如图片，视频......
r+：读写，不能创建文件，指针在开头，写入时会覆盖所写长度的内容，如：原来：123456，写入：ab，结果：ab3456
w+:可读写，其他同w一样


#2 方法
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
os.mkdir(dir,0oxxx) //创建一个文件夹，不能同时创建多个。0oxxx表示访问权限，从左到右分别代表 文件拥有者、同组用户、其他用户 的访问权限；可读为4，可写为                       2，可执行为1，如0o777表示 文件拥有者、同组用户、其他用户 既可读，又可写，又可执行
os.getcwd() //获得当前目录
os.chdir(dir) //改变工作目录
os.listdir(dir) //获取dir中文件内容组成的列表。当dir为

#3 注意
大文件读取，read()占内存，但效率高；for in省内存，但效率低；readline()折中
