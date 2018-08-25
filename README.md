import win32com.client

class Caculator:
  @staticmethod
  def __speaker(word):
    speak = win32com.client.Dispatch("SAPI.SpVoice")
    speak.Speak(word)
  
  def __speak(word=""):
    def __say(func):
      def inner(self, n)
        self.__speaker(word+str(n))
        return func(self, n)
      return inner
    return __say

  def __check(func):
    def inner(self, n):
      if not (isinstance(n, int) or isinstance(n, float)):
        raise TypeError(str(n)+"不是一个数")
      return func(self, n)
  
  @__check
  @__speak()
  def __init__(self, n):
    self.__result = n
  
  @__check
  @__speak("加")
  def jia(self, n):
    self.__result += n
    return self
  
  @__check
  @__speak("减")
  def jian(self, n):
    self.__result -= n
    return self
  
  @__check
  @__speak("乘")
  def cheng(self, n):
    self.__result *= n
    return self
    
  @__check  
  @__speak("除以")  
  def chu(self, n):
    self.__result /= n
    return self
  
  def show(self):
    self.__speaker("等于"+str(self.__result))
    print("计算结果是："+str(self.__result))
  
  @property
  def result(self):
    return self.__result
    
p = Caculator(2)
p.jia(1).jian(5).cheng(4).chu(5)
p.show()
print(p.result)
