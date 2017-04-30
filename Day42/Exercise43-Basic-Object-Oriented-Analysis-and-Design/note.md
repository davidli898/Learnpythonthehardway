## 练习43 基础面向对象分析和设计
我将描述一个流程,当你用 Python 创造东西的流程,尤其是使用面向对象编程的时候.我所说的流程意味着我将会给你一系列步骤,你可以按顺序去做,但你不要成为规则的奴隶或生搬硬套.它们只是许多编程问题的良好开端,但不是解决所有问题的灵丹妙药,你不要把它当做所有问题的唯一解,而是多个可能性的一种.  
流程如下:
1. 写出或画出这个问题
2. 从#1抽象出问题的关键概念,并研究它们
3. 为概念创建一个 class的分级表和object地图
4. 将 class写成代码 并运行 测试
5. 重复以上环节并改善

上述解决问题的视角被称为"自上而下式",意思是从抽象的松散的想法开始,慢慢改善,知道想法成型并能用代码实现.  

首先我从写下问题开始,并试着思考关于这个问题的任何方面,或许我还会画出一两个流程图,地图,甚至我还会给我自己写一系列描述发这个问题的邮件.我用这种方式来解析问题中的关键概念,同时也能查明那些我原本已经知道的东西.

接着我会仔细检查这些笔记,图表,和描述信息,我会把这些关键概念抽出来.这有个简单的小技巧来做这件事:简要地制作一个全部名词和动词列表,写和画都行,然后写出他们的关系.我能得到一些很不错的类名,对象名和函数名的列表以便接下来使用,然后列表中任何不懂的概念我都会查清楚,并改进这个列表.  

一旦我有了概念的列表,我会做一个简单的概念关系框架来描述每个概念和类的关系.你应该常常拿出名词表来问自己:"这个名词像不像另一个概念名? 那意味着那有一个通用的父级类,那应该叫它什么?" 请持续做这件事情直到你拥有一个类的体系,接下来是动词,你看下它们是否某个类的函数名字,是的话,就把它添加到框架里.  

借助这个类的体系来梳理思路,我得以坐下写下基本的代码骨架,比如:类,函数等,仅此而已,然后我接下来,我会做个测试,确保我设置的类能够正常运转,有些时候,我写一小段代码,就测试一下,然后再写一小段,再测试,直到完成整个程序.

最后,我会反复执行这个流程,直到非常清晰并可以完成代码部署.如果我因为某个概念或者问题在某个特别的部分被卡住了,那么我会继续上面这个流程,直到我把问题解决.  

### 关于一个简单的游戏引擎分析
这个游戏我打算命名为:" Gothons from Planet Percal #25" ,是一个小的空间冒险游戏.除了这些想法没有更多的细节了,但我可以发散思维,将这个游戏做出来.

#### 写下来或画出来这个问题
下面是游戏介绍:  

"外星人入侵了一艘太空船,我们英雄需要穿过一个迷宫,去反击他们,然后他可以进入逃生舱回到地球.这个游戏类似于** Zork**之类的冒险类型游戏通过文字输出以及各类有趣的死亡方式.这个游戏拥有一个引擎来运行包含很多房间和场景的地图,玩家进入每个房间时都会输出描述信息然后指示引擎调出相关下一个房间."  

此刻,我有一个关于如何运行游戏的好想法.那么我先将每个场景描述一下:  
* **Death** 这是玩家死亡状态,应该以有趣的方式呈现
* **Central Corridor** 中央走廊,这是起始点,有一个Gothon已经在这等待玩家,玩家需要答对一个笑话,才能继续游戏
* **Laser Weapon Armory** 激光武器库,英雄从这获得中子弹,在踏上逃生舱之前引爆太空船,这需要一个小键盘来猜测数字密码.  
* **The Bridge** 桥,当英雄固定好炸弹后,一个与 Gothon战斗的场景.
* **Escape Pod** 英雄逃离的地方,但需要猜出正确的逃生舱

#### 解析并研究这些关键概念
当我有了足够的信息来抽取一些名词,并分析它们的类体系时,我会先做一个关于所有名词的列表.
* Alien  外星人
* Player 玩家
* Ship 太空船
* Maze 迷宫
* Room 房间
* Scene 场景
* Escape Pod 逃生舱
* Planet 地球
* Map 地图
* Engine 引擎
* Death 死亡
* Central Corridor 中央走廊
* Laser Weapon Armory  激光武器库
* The Bridge 桥

同样地,我也会将所有的动词过一遍,看下有没有适合的函数名字,但我暂时先跳过这一步.  

此时此刻,你可能也逐个研究了这堆概念,但目前你还什么都不清楚.比如,我可能玩过几次这种类型游戏,并确保我知道它们是怎样运行的.我可能会研究飞船的设计原理或者炸弹的工作原理,也可能去研究技术问题比如将游戏状态存储进数据库.当我完成这个研究,我估计会基于最新的信息重新开始#1的步骤,并且可能会重写我的描述,并提取新的概念.  

#### 为概念们创建一个类的体系和对象地图
一旦我有了这个,我借助提问进入类的体系:"它和另一个事物的相似性是什么?","它是不是另外一个事物的另外一种说法?"  

我立刻发现,我所说的`Room`和` Scene`基本上是一回事,取决于我想做什么.我决定用` Scene`,接着我发现,所有像` Central Corridor`的特定房间基本上都是`Scene`,同时发现`Death`也是一个` Scene`. `Maze`和` Map`基本上也是一回事.所以我打算用`Map`. 自从频繁使用它之后,我也不想做一个战斗系统了,所以我决定忽略` Alien`和` Player`, 留着以后再用. 其实` planet`也不应该单独存在,它也是个` Scene`而已.  
通过这个流程,我开始做了一个类体系,是这样:
```py
* Map
* Engine
* Scene
  * Death
  * Central Corridor
  * Laser Weapon Armory
  * The Bridge
  * Escape Pod
```
接下来我会把每个事物对应的动作加进去,比如上述描述可知,我需要一个方法来`运行`引擎, 在地图中`切换场景`等等,所以我添加了下面这些.  
```py
* Map
 - next_scene
 - opening_scene
* Engine
  - play
* Scene
  - enter
  * Death
  * Central Corridor
  * Laser Weapon Armory
  * The Bridge
  * Escape Pod
```
注意我将`-enter`放在了` Scene`下面,因为其他的子场景会继承并复写.  

#### 写代码然后测试
我有时会将上面的树形结构,直接复制进编辑器,再修改.

在这个文件中,你可以看到我简单地把类层级拷贝进来,文件最底部的几行代码,是为了测试这个基础结构是否能运行,在接下来的部分,你需要填充剩余部分,使游戏符合描述.  
#### 反复做并改善
我的流程的最后一步,并不那么像一个步骤,有点像` while 循环`.你从没实现过"一次过关"的操作,所以你应该再把整个流程回顾一遍,并最后一步学到的信息重新改进它.有时候我走到了第3步,但是发现我需要回到步骤1或2再进行巩固,那么我就停下来,返回继续巩固.有时候我灵光一现,跳到代码尾部将我脑中的解决方案写出来,然后回到之前步骤继续做,确保能覆盖所有的可能性.  

关于这个流程的另一个想法是,你不仅可以应用到某个大问题上,也可以用到大问题中的各个小问题中去,譬如说,你不知道` Engine.play`如何写,可以停下,然后将这个流程应用到如何写出这个函数.

### 由上到下 VS 自下而上 设计
我的这个流程就是典型的"由上到下"式设计.它大多从抽象的概念开始