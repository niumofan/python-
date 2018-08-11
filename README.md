import time


//函数time.time()用于获取当前时间戳
  ticks = time.time()
  print("当前时间戳为：",ticks)
//输出：当前时间戳为: 1459994552.51
//时间戳单位最适于做日期运算。但是1970年之前的日期就无法以此表示了。太遥远的日期也不行，UNIX和Windows只支持到2038年。


//从返回浮点数的时间辍方式向时间元组转换，只要将浮点数传递给如localtime之类的函数
  localtime = time.localtime(time.time())
  print("本地时间为：",localtime)
  或
  localtime = time.localtime()
  print("本地时间为：",localtime)
//输出：本地时间为 : time.struct_time(tm_year=2016, tm_mon=4, tm_mday=7, tm_hour=10, tm_min=3, tm_sec=27, tm_wday=3, tm_yday=98,      tm_isdst=0)


//获取格式化的时间
  localtime = time.asctime(time.localtime(time.time()))
  print("本地时间为：",localtime)
  或
  localtime = time.asctime(time.localtime())
  print("本地时间为：",localtime)
  或
  localtime = time.asctime()
  print("本地时间为：",localtime)
//输出：本地时间为 : Thu Apr  7 10:05:21 2016


//格式化日期
  print(time.strftime("%Y-%m-%d %H:%M:%S",time.localtime()))
//输出：2018-08-11 15:04:33
  
  print(time.strftime("%a %b %d %H:%M:%S %Y",time.localtime()))
//输出：Sat Aug 11 15:04:33 2018
  
  a = "Sat Mar 28 22:24:24 2016"
  print(time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y")))
//输出：1459175064.0
//%y 两位数的年份表示（00-99）
  %Y 四位数的年份表示（000-9999）
  %m 月份（01-12）
  %d 月内中的一天（0-31）
  %H 24小时制小时数（0-23）
  %I 12小时制小时数（01-12）
  %M 分钟数（00=59）
  %S 秒（00-59）
  %a 本地简化星期名称
  %A 本地完整星期名称
  %b 本地简化的月份名称
  %B 本地完整的月份名称
  %c 本地相应的日期表示和时间表示
  %j 年内的一天（001-366）
  %p 本地A.M.或P.M.的等价符
  %U 一年中的星期数（00-53）星期天为星期的开始
  %w 星期（0-6），星期天为星期的开始
  %W 一年中的星期数（00-53）星期一为星期的开始
  %x 本地相应的日期表示
  %X 本地相应的时间表示
  %Z 当前时区的名称
  %% %号本身
