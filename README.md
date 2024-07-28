# Notice
由于 [原版pyOnmyoji](https://github.com/luoy2/pyOnmyoji) 不再更新、~~[阴阳师官方不再提供游戏的 exe 可执行程序](https://github.com/luoy2/pyOnmyoji/issues/20)，而且我不再玩这游戏了，本 fork 切换为只读模式。~~ 本项目基本不会得到什么维护。

大部分代码需要找游戏运行的窗口，实验表明只要把`constants.init_constants` 初始化窗口参数改成 `u'MuMu模拟器12'` 有些代码仍然能复用，毕竟是基于机器视觉的自动化测试工具。

## TODO （如果有人想要学习的话）
* 更换底层的自动化测试框架。现在使用的 [Serpent.AI](https://github.com/SerpentAI/SerpentAI) 并不是经常维护。~~而且我感觉咱这也没 AI 啊。~~
* 更新场景判别和目标定位方法：
  - 场景判别也许可以训练专用神经网络模型（比如 darknet？）实现
    - 我在百鬼夜行模块中的做法是找到场景的关键对象，用 ORB 求描述子，然后对当前场景也求描述子，通过描述子之间汉宁距离的远近判别当前场景。这法子太古老了不够智能。
  - 如果自动化测试框架中能提供这样的服务最好。
* 设计更加现代化的脚本检测回避系统：
  - 现在的代码的回避机制相当原始，我发现的只有给点击坐标加随机参数，以及定时休息这两个。
  - 所谓脚本检测回避系统应该让游戏行为更像真实的游戏玩家
    - 比如打御魂副本的时候，没几个人会只刷本不看聊天区吧？
      * OCR 识别聊天区裙友吹水的内容，喂给 [ollama](https://github.com/ollama/ollama) 等 LLM 工具生成合理的回复，并在聊天区与大家互动。
* 记得 [搜索 Github](https://github.com/search?q=%E9%98%B4%E9%98%B3%E5%B8%88&type=repositories) 学习其他人的代码。

以下是原 README。

----
# pyOnmyoji
python play onmyoji(网易-阴阳师), folked win32 controller from SerpentAI

The initial purpose of this project is trying to train a RNN to play Onmyoji as a data science project. (Special thanks to [SerpentAI](https://github.com/SerpentAI/SerpentAI) providing the framework)

While working on the model constructing, I will try to move some features from my [Lua Bot](https://github.com/luoy2/yys_lua_script) to this python project.

#### python env:

| python version        | availability |
| --------------------- |:-------------:|
| python 3.8            | untested    |
| python 3.7            | possible    |
| python 3.6            | available   |
| < python 3.5          | untested    |
| python 2.x            | unavailable |


#### install
```
pip install -r requirements.txt
```



#### a few notes：
1. all the color cords were taken on a **4k monitor(win ui zoom 150%)**, so if you are on a different resolution and zoom percentage, you probably need to re take all the color cords. I will upload a tutorial and a PyQt tool about taking the color cords sometime later. Basically, all the colors were in `colors/util.py` and the structure would be:

```
LiaoAttack = ColorToMatch([537, 169, 1459, 963], [[(0, 0), (243, 178, 94)], [(33, -37), (150, 59, 46)], [(-331, -3), (243, 178, 94)]], 1)
```

  - first list `[537, 169, 1459, 963]` is the region of the color tuples you want to find
  - second list were the color tuples. the first cords will always be `[0, 0]`, which means you need to find a RGB color (e.g. (243, 178, 94), and the (33, -37) offset color should be (150, 59, 46), going forward.
  - third value is the tolerence value for find colors
 
 
 
 #### Tansuo
1. 进入方法：进入探索界面， 运行`tansuo.py`. 若不需要寮突破， 请将`liao_status` 设为0. 否则会优先去打寮突破-> 个人突破 -> 探索。
  ```
  if __name__ == '__main__':
    liao_status = 1
  ```
2. 探索目前的机制是狗粮大队长默认处于左1号位， 然后会在寮突破， 探索， 个人突破中循环。 探索会自动打最后一章的经验怪以及boss。
  
  
 #### 结界突破
 1. 锁定突破阵容后， 进入结界突破寮突破界面， 运行`jiejietupo.py`
 
 #### 御魂队长模式
 1. 选好阵容， 找好基友， 锁定出战阵容
 2. 在小队等待界面运行`party.py`
 
 #### 御魂队员模式
 1. 同上
 2. 在任意界面运行`party_member.py`

 #### 业原火
 1. 锁定出战阵容
 2. 在开始之前的界面运行`yeyuanhuo.py`. 目前只支持痴
 
 #### 百鬼夜行
 1. 进入百鬼夜行准备界面，也就是有跳跳弟弟和跳跳妹妹的那个画面
 2. 运行`baiguiyexing.py`
 
