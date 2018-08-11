import calendar

//获取某月日历
  cal = calendar.month(2016,1)
  print(car)
/*    
      January 2016
  Mo Tu We Th Fr Sa Su
               1  2  3
   4  5  6  7  8  9 10
  11 12 13 14 15 16 17
  18 19 20 21 22 23 24
  25 26 27 28 29 30 31
*/


//获取某年日历
  cal = calendar.calendar(2018, w=2, l=1, c=6)
  print(cal)
/*
                                  2018

      January                   February                   March
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7                1  2  3  4                1  2  3  4
 8  9 10 11 12 13 14       5  6  7  8  9 10 11       5  6  7  8  9 10 11
15 16 17 18 19 20 21      12 13 14 15 16 17 18      12 13 14 15 16 17 18
22 23 24 25 26 27 28      19 20 21 22 23 24 25      19 20 21 22 23 24 25
29 30 31                  26 27 28                  26 27 28 29 30 31

       April                      May                       June
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
                   1          1  2  3  4  5  6                   1  2  3
 2  3  4  5  6  7  8       7  8  9 10 11 12 13       4  5  6  7  8  9 10
 9 10 11 12 13 14 15      14 15 16 17 18 19 20      11 12 13 14 15 16 17
16 17 18 19 20 21 22      21 22 23 24 25 26 27      18 19 20 21 22 23 24
23 24 25 26 27 28 29      28 29 30 31               25 26 27 28 29 30
30

        July                     August                  September
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
                   1             1  2  3  4  5                      1  2
 2  3  4  5  6  7  8       6  7  8  9 10 11 12       3  4  5  6  7  8  9
 9 10 11 12 13 14 15      13 14 15 16 17 18 19      10 11 12 13 14 15 16
16 17 18 19 20 21 22      20 21 22 23 24 25 26      17 18 19 20 21 22 23
23 24 25 26 27 28 29      27 28 29 30 31            24 25 26 27 28 29 30
30 31

      October                   November                  December
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7                1  2  3  4                      1  2
 8  9 10 11 12 13 14       5  6  7  8  9 10 11       3  4  5  6  7  8  9
15 16 17 18 19 20 21      12 13 14 15 16 17 18      10 11 12 13 14 15 16
22 23 24 25 26 27 28      19 20 21 22 23 24 25      17 18 19 20 21 22 23
29 30 31                  26 27 28 29 30            24 25 26 27 28 29 30
                                                    31
*/


//查看每周起始日期设置
  print(calendar.firstweekday())
//默认情况下，首次载入calendar模块时返回0，即星期一。


//闰年
  calendar.leapdays(y1,y2)   //得到 y1~（y2-1）年之间的闰年次数
  calendar.islear(y) //判断闰年，True or False
  
  
//返回一个整数的单层嵌套列表。每个子列表装载代表一个星期的整数。每个子列表从星期一开始  
  calendar.monthcalendar(year, month) 
    例：print(calendar.monthcalendar(2018, 8)
    输出：[[0, 0, 1, 2, 3, 4, 5], [6, 7, 8, 9, 10, 11, 12], [13, 14, 15, 16, 17, 18, 19], [20, 21, 22, 23, 24, 25, 26], [27, 28, 29, 30, 31, 0, 0]]


//返回 本月第一天的星期数 和 本月的天数
  calendar.monthrange(year,month)
  例：print(calendar.monthrange(2018.8))
  输出（2，31）
  解释：0代表星期一，2代表星期三
  
  
 //设置每周的起始日期码。0（星期一）到6（星期日）。
  calendar.setfirstweekday(weekday)
  例：calendar.setfirstweekday(2)
      print(calendar.firstweekday())
  输出：2


//返回给定日期的日期码。0（星期一）到6（星期日）。  
calendar.weekday(year,month,day)
例：print(calendar.weekday(2018.8.11))
输出：5
  
