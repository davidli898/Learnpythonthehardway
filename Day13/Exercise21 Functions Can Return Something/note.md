## 练习21 函数可以返回东西
你已经会用 `=`为变量赋予数字或字符串了.现在我又要搞乱你的认知了.我将会演示用` = `和一个新的 python 命令`return`,将变量设置为一个`函数的值`,这里有一点你需要特别注意:  
```
def add(a, b):
    print "ADDING %d + %d" % (a, b)
    return a + b
```
最后一行,`return  a + b `的意思是:  
1. `add` 函数调用两个参数: a 和 b .
2.  在运行函数时,打印函数的运算过程 就是代码中的` ADDING` .
3. 然后我们告诉 python 做一个逆向的动作,也就是先做右边的` a + b `运算,然后再`return`.
4. Python 把两个参数相加,函数运行结束,只要下面任意一行代码运行这个函数,就会将` a + b `的结果赋予到变量中.  

你慢慢地消化这部分内容,因为今后还有很多课程涉及到它.为了帮助你理解,让你解决一个小谜题,学点更酷的东西.  

### 课程训练
1. 如果你还是不太明白,请试着自己写下几个函数,返回一些值,只要是能放到`=`右边的东西,你都可以`return`
2. 脚本的最后是一个谜题,我把一个函数的`return`值当做另一个函数的参数,一个套一个,成了链条.有点像个方程,看起来挺奇怪的.但其实是可行的.你应该自己试着做一些方程.
3. 一旦你用方程解决谜题,沉浸其中看看会发生什么,当你更改一个函数的一部分,故意改变一些获得一个特定的结果.
4. 最后,反过来做一些事. 列一个简单的方程,试着用函数模拟计算.