## 练习33-While 循环
现在一个新的循环要完全颠覆你的认知了,那就是 while 循环.它同样会在布尔表达式为真的情况下,执行它下面的代码块.  

等等,你能跟上这些术语吧? 就是我们写一行代码,用`:`结尾,告诉 python 我要开始一段代码块,然后换行并缩进,开始写代码块.只有通过这种格式, Python 从知道你要干嘛.如果你不明白这段话是什么意思,你要回去复习了.  

接下来,我们会做些练习,让你大脑接受这些格式.   

言归正传,来说 while 循环.它的原理有点类似`if 语句`,不同的是,`if 语句`只运行一次,而` while 循环`回重复执行代码块,直到布尔表达式的值为`False`.  

所以 `while 循环` 存在一个问题,那就是某些时候,它根本不会停止,一直循环运行到宇宙终结. 为了避免这个问题,这里有三个规则需要注意:  
1. 尽量减少使用` while 循环`,多用` for 循环`
2. 检查你的` while循环`代码,确保布尔表达式会出现`False`的情况
3. 如出现不确定的情况,在代码头部和尾部 输出变量的值来帮助判断.  


### 课程训练
1. 将本节的` while循环`改成一个函数,把`(i < 6)`改成一个参数
```py
def while_f(i):
    numbers = []
    while i < 6:  # keep loop if i < 6
        numbers.append(i) # put the value of  i into the list numbers
        i = i + 1  # every time  increase 1 for i
        print "Numbers now:", numbers
    print numbers
while_f(0)
```
2. 使用这个函数,重写这个脚本,并带入新的数字来尝试
3. 为这个函数新增一个参数,用来代替第8行的 `+ 1`, 这样你就可以随意增加数值了.
4. 使用这个函数重写脚本,试试效果有什么不同

如果` while 循环`无法停止,你可以使用 `Ctrl + C` 来终止它.