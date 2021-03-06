## 练习44-继承 vs 合成
在英雄类的神话故事中,总有一个类似黑暗森林的存在.他可能是个洞穴,一片森林或者另一个行星,总之得有一个屌丝们认为英雄不应该去的地方.当然了,接着立刻会介绍大反派,你懂的,英雄肯定得去那个倒霉地方干掉大反派.似乎只要是英雄就必须进入一个危险境地.  
你很少读到神话故事中,有哪个英雄超级聪明,能避免自己处于危险境地.这个黑暗森林就像一个黑洞,不论英雄做什么,都会把他拽进来.  

在面向对象的编程中,_继承_ 就是邪恶森林.有经验的程序员知道如何避开它,因为他们知道在这邪恶的森林深处有一个邪恶皇后,_多重继承_ ,她用繁多的复杂的牙齿咀嚼软件和程序员.但这个森林有着极强的吸引力,几乎每个程序员都会忍不住深入这个森林希望取下邪恶女皇的首级以证明自己是真正的程序员. 你也无法抵抗_继承森林_的引力,所以你会进入.但冒险一番之后,你才学会远离这个该死的森林,并用武器武装自己,如果再进一次你一定会全副武装.  

我用这个有趣的方式来教你避免犯某些错误.比如:"继承". 哪些正在"坑"里的程序员们会让你跳进坑里,他们这样做是因为他们需要你帮忙,千万不要忘坑里跳.请**永远记住**:  

**绝大部分情况下使用 _继承_ 时,保持简单,尽量用 _组成_ 来代替.任何情况下都不要使用 _多重继承_.**

### 什么是继承?
**继承** 用来表示一个子类从父类继承大部分甚至是全部的属性. 它表现的非常隐秘,当你写下`class Foo(Bar)`,意思是:创建一个类 `Foo`继承自` Bar`,当你写出这行代码后,你所作的任何影响`Foo`的行为,也会影响` Bar`,这等于你将一个通用的函数放进了` Bar class`,对` Foo`添加专用函数.   

这有三种方法让父类和子类相互影响:
1. 子类的动作中隐含父类的动作
2. 子类的动作覆盖父类的动作
3. 子类的动作在父类的动作之后

接下来,我会按顺序论证每个方法.

#### 隐含继承
首先,我会为你展示隐含动作发生在,当你为_父类_ 中定义了一个函数,但是没有在子类中定义时.

```py
class Parent(object):

    def implicit(self):
        print "PARENT implicit()"

class Child(Parent):
    pass

dad = Parent()
son = Child()

dad.implicit()
son.implicit()
```
Child 下面的 pass 作用是:告诉 Python,这是一空白代码块.虽然创造了一个类名叫` Child`,但是并没有为它定义任何东西,他的全部东西都继承自 `Parent`,当你运行代码的时候,你会得到如下结果.
```py
$ python ex44.py
PARENT implicit()
PARENT implicit()
```
#### 覆盖继承
当子类继承的某个函数需要父类有不同表现时,_隐含继承_ 就有问题. 这时你只需要在子类中设置一个相同名字的函数,就可以覆盖掉父类的继承函数.请看下面这段代码:
```py
class Parent(object):
  def override(self):
    print "PARENT override()"

class Child(Parent):
  def override(self):
    print "CHILD override()"

dad = Parent()
son = Child()

dad.override()
son.override()

```
可以看到如下结果:
```py
$ python ex44.py
PARENT override()
CHILD override()

```
就想你看到的,当`dad.override()`运行时,得到了` Parent.override`函数,因为变量` dad`是 Parent, 但是当`son.override()`运行时,输出了` Child.override`的信息,因为` Son`是 Child的实例,而 Child 用自己的函数覆盖了 Parent 的函数.
### 改变之前或之后
第三种方式使用_继承_ 的方式有点特殊,它可以让你决定子类的函数在父类函数的之前或者之后运行.这需要借助一个 Python 内置的函数--` super`,来调取父类的函数. 代码如下:
```py
1  class Parent(object):
2
3     def altered(self):
4         print "PARENT altered()"
5
6 class Child(Parent):
7
8     def altered(self):
9       print "CHILD, BEFORE PARENT altered()"
10      super(Child, self).altered()
11      print "CHILD,AFTER PARENT altered()"
12
13  dad = Parent()
14  son = Child()
15
16 dad.altered()
17 son.altered()
```
关键点在9-11行代码,定义了` son.altered()`的工作原理:
1. 因为子类设置了跟父类相同的函数名,所以父类函数被覆盖,第9行代码得以运行.
2. 在此例中,我需要做一个`之前`和`之后`的对照,于是我使用` super`调用了` Parent.altered`的函数版本
3. 在第10行代码,我使用` super(Child, self).altered()`,它可以提高父类函数的继承权限,屏蔽子类的覆盖.
4. 于是,`Parent.altered`得以运行,可以从控制台中看到输出信息.
5. 当` Parent.altered()`运行过之后,`继续执行 Child.altered`函数最后一行代码.

你看到如下输出:
```py
$ python ex44.py
PARENT altered()
CHILD, BEFORE PARENT altered()
PARENT altered()
CHILD, AFTER PARENT altered()
```
### 3种混合
为了集中展示这三种，我这有一个最终版本的代码，一次展示这三种继承方式。
```py
1 class Parent(object):
2
3       def override(self):
4         print "PARENT override()"
5
6       def implicit(self):
7         print "PARENT implicit()"
8
9       def altered(self):
10         print "PARENT altered()"
11
12  class Child(Parent):
13     
14      def override(self):
15         print "CHILD override（）"
16       
17      def altered(self):
18        print "CHILD,BEFORE PARENT altered()"
19        super(Child, self).altered()
20        print "CHILD, AFTER PARENT altered()"
21
22  dad = Parent()
23  son = Child()
24
25 dad.implicit()  # this line will  print ""PARENT implicit()""
26 son.implicit() # this line will print "PARENT implicit()"
27
28 dad.override() # this line will print "PARENT override()"
29 son.override() # this line will print "PARENT override()"
30
31 dad.altered() # this line will print PARENT altered()"
32 son.altered() # this line will "CHILD,BEFORE PARENT altered()" ,"PARENT altered()","CHILD, AFTER PARENT altered()"
```
### 使用super() 的原因
这差不多是个常识,但是我们有个问题在于"多重继承",多重继承就是一个子类继承自多个父类.比如这个:
```py
 class SuperFun(Child, BadStuff):
   pass
```
上述代码的意思是:设置一个类名叫` SuperFun`同时继承父类 Child 和 BadStuff.  

在这个例子中,每当你在任意一个` SuperFun`的实例中使用隐含继承时, Python 会开始在` BadStuff`和` Child`中搜寻任何可能相似的类,但在执行这个动作的时候,有一个一致的顺序.叫做"Method resolution order(MRO)",还有一个叫"C3"的算法来实现.   
因为MRO是一个复杂的,定义明确的用法. Python 不可能将操作权限交给你.所以 Python 给了一个` super()`函数,在你需要改变继承属性的时候使用.  

### 搭配 super() 使用 __init__
super() 的最常见的用法就是在`__init__`函数中.这通常是你在 Child 这种类里边需要做的唯一的事.然后完成 Parent 的初始化. 这有一个简洁的例子:
```py
class Child(Parent):

  def __init__(self, stuff):
     self.stuff = stuff
     super(Child, self).__init__()
```

## 合成
继承是很有用,但还有另一种途径可以实现同样的操作,使用类和模块,而不是依赖隐含继承.这个方式可以简单地复制另一个类,这有一个例子:  
```py
class  Other(object):

  def override(self):
    print "OTHER override()"

  def implicit(self):
    print "OTHER implicit()"

  def altered(self):
    print "OTHER altered()"

class Child(object):

  def __init__(self):
    self.other = Other()

  def implicit(self):
    self.other.implicit()

  def override(self):
    print "CHILD override()"

  def altered(self):
    print "CHILD, BEFORE OTHER altered()"
    self.other.altered()
    print "CHILD, AFTER OTHER altered()"

son = CHILD()

son.implicit()
son.override()
son.altered()
```
## 什么时候用继承,什么时候用合成?
不论使用_继承_ 还是_合成_,都是期望通过可复用的代码了解决问题.你不会希望在用复杂的代码开发软件,因为目前为止,证明那是低效的._继承_ 的作用是通过建立一个机制来解决问题,这个机制由一些基本的类组成,并内置一些功能. _合成_ 的方法是给你一些模块,并能够调用其他类中的函数.  
如果碰到一个问题,用两种方法都可以解决,那到底用哪种合适?答案是非常主观的.你可以借鉴我的3条规则:
1. 任何情况下,避免多重继承,如果你被卡住了,那就停下来去了解类的层级并花一些时间研究这些概念的来龙去脉.
2. 使用_合成_ 将代码打包进一个模块,然后使用到非常多的非相关的场景和地方
3. 当这里有很多关联性强的概念时,可以使用_继承_.

### 课程训练
前往阅读 http://www.python.org/dev/peps/pep-0008 开始试着用自己的代码来实现.你会注意到,网站上的说法跟本书不太相同,现在你应该自己试着去理解官方文档了.
