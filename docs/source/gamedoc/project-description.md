# 项目描述

## 一、项目名称

&emsp;&emsp;中文：灵数奇缘  
&emsp;&emsp;意为：灵魂 + 数据 + 游戏人物之间的感情连接

&emsp;&emsp;英文：L·S·D （Luv Sense Digital / Ling Shu Domain）   
&emsp;&emsp;意为：爱意数据化 / 灵数之域

## 二、一句话简介

&emsp;&emsp;一句话简介：一个教AI玩游戏的游戏  
&emsp;&emsp;核心玩法：2D动作 + 养成 + 策略  
&emsp;&emsp;世界观：虚拟游戏 + 未来世界 + 反乌托邦  
&emsp;&emsp;美术风格：民族风 + 潮牌时尚  
&emsp;&emsp;开发引擎：自研开源跨平台2D游戏引擎 [Dorothy-SSR](technical-description/index.md)  
&emsp;&emsp;发布平台：Windows、MacOS、Android、iOS、Linux  
&emsp;&emsp;商业化模式：开源

## 三、故事设定

```{admonition} 故事梗概（by：嗲）
&emsp;&emsp;在末日后，地面上一片焦土，幸存者人类苟延残喘活在地下。游戏公司为了解决冲突，开发了一款没有人能拒绝的沉浸式游戏。
但这个游戏却是阴谋的起点，玩家进入游戏后很多年都不会回到现实社会。  
&emsp;&emsp;面对真正的苦难，游戏商喜闻乐见，他们的年轻人沉浸在虚拟的数字世界。而有一人看透了游戏公司的本质，他希望能改变这一切。
```
&emsp;&emsp;一张图看完所有设定 - <a href="../_static/L·S·D.pdf">在这里</a>。

## 四、玩法介绍

&emsp;&emsp;《灵数奇缘》项目初始策划的游戏玩法是：2D 横版动作 + AI 训练/养成 + 即时战术  
&emsp;&emsp;通过玩家亲手操作教会游戏 NPC 如何进行战斗，生成 NPC 自己的战斗思维。然后由玩家组建自己的战斗小队，通过小队成员共同合作完成任务和挑战。

* **2D 横版动作**  
&emsp;&emsp;LSD的游戏基础形式为传统的2D横版，并使用近现代+科幻的军事武器进行战斗。战斗操作以考验玩家反应力为主，要求应对不同的敌人属性以及敌人技能，找到时机即时使用相应克制的武器发动攻击。

```{eval-rst}
.. figure:: /img/intro/gameplay-platformer.jpg
   :align: center
   :alt: 玩法-2D横版动作

   玩法-2D横版动作
```

* **AI 训练**  
&emsp;&emsp;LSD的游戏提供让玩家自行创作 AI 代码的功能，通过人工智能算法（包括但不限于：分类决策树、Q Learning）采集玩家进行游戏的操作数据，生成决策树形式的AI逻辑代码，并以适合的方式展示给玩家。

```{eval-rst}
.. figure:: /img/intro/gameplay-AI-training.jpg
   :align: center
   :alt: 玩法-AI训练

   玩法-AI训练
```

* **剧情养成**  
&emsp;&emsp;玩家可以通过推进游戏故事、完成游戏任务，或是和游戏角色进行通讯交流，触发养成条件解锁人物能力（克服缺点）。并通过经营军事学园，招募更多的学员加入。

```{eval-rst}
.. figure:: /img/intro/gameplay-making.jpg
   :align: center
   :alt: 玩法-剧情养成

   玩法-剧情养成
```

* **即时战术**  
&emsp;&emsp;玩家训练完成配备强力战斗AI的学员角色可以编队投入战场参与实际的战斗，在战场模式下，玩家只能操作导师的角色替身，其余队员将以训练的战斗AI自动参与战斗，并在行动指令系统下由玩家进行战术调遣。

```{eval-rst}
.. figure:: /img/intro/gameplay-RTT.jpg
   :align: center
   :alt: 玩法-即时战术

   玩法-即时战术
```