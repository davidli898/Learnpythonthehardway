## 练习47-自动测试
你有没有试过一遍又一遍敲入命令来测试你编写的游戏.那么写一段代码来代替你测试可好?之后你对游戏做一些改动,或增加一些新模块的话,只需要`run your tests`.这些自动化测试并不能帮你找出所以bug, 但是它能大大节约你测试代码的时间.  

今后的每个练习都不会再有` What you should see`部分.取而代之的是` What you should test`部分,你将会为你的每段代码编写自动测试脚本,这会帮助你成为一个更好的程序员.  

我不会跟你解释为什么你需要编写自动化测试脚本.我只会告诉你尝试去做一个程序员,因为程序员会将无聊沉闷的工作自动化.即使测试一小段代码也绝对是无聊沉闷的,所以你最好写另一小段代码来替你测试它.  

### 编写一个测试案例
我们将会用一段非常简单的代码来进行测试.我们将会用这个简单的测试你的新项目框架.  
首先,复制你的项目框架到`ex47`,下面会给出步骤,我只给出英文描述,而不是直接给出代码,所以你得靠自己思考.
1. 复制` skeleton`到 `ex47`
2. 把`ex47`中的每一个`NAME`重新命名
3. 修改`ex47`文件中的每一个 NAME
4. 最后,移除所有的`*. pyc`文件.  

如果有遗忘,就回到练习46,如果你不能轻而易举地完成,你可想需要多做几遍.

### 测试的参考原则
当你设计测试的时候可以遵循下面几个参考原则:
1. 把测试文件放进` test/`文件夹中,命名为** BLAH_tests.py,否则 `nosetests`不会运行他们.这是一种保护机制,防止你的测试文件被其他代码破坏.
2. 给每一个你编写的模块制作测试文件.
3. 尽量使你的测试文件简短,不过不要担心它的凌乱,因为大部分测试文件都很凌乱.
4. 即使你的测试文件很凌乱,也尽量让它干净,把重复的代码去掉,创建辅助功能摆脱复杂的代码,这会很管用.
5. 最后,不要给你的测试文件附加太多东西,有时候重新设计某种东西的最好方法是删了重做.  

### 课程训练
1. 阅读更多关于` nosetests`的资料,以及` alternatives`的资料
2. 学习关于 Python 的` doc tests`内容,比较一下,是否比本章的工具更好.
3. 利用学到的知识,重建你的游戏,使房间更高级.
