---
title:   粮不产则我产之：基于AI绘图的私人表情包生产
date: 2023-12-15
categories:
- 生活
tags:
- 生活
- 杂记
- 服务器

---

> NAI呦NAI，于轮回荆棘之道，听吾此刻之召唤！予吾强大之力量，摧彼错误之现实！
以千千兆兆赛博之主为名，吾呼唤孤独之战斗者 ——缠流子！
以汝之血色衣冠，配汝之珠绿之瞳；邪魅妄语勿近，虚空魂魄勿来！
饕餮之享，浪漫之光，破除矩阵，凝眸彼方！化身残影，魑魅魍魉，或视或闻，哐哐哐哐！
一生二，二生四，四生八，八生一零二四矩阵，吾之表情包呦，速来！
> 

![召唤出来了！](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS00.png)

---

<!--more-->

遥想NAI初告破，千军万马齐炼丹；

调教TAG深似海，4090热如山。

经载LORA何深深，技术论坛难瞻瞻；

不如挥袖整活去，搞怪表情乐且憨！

遥想从疫情期间接触SDwebui和最早期的破解版Novelai模型，转眼间已是一年。期间加了学校的QQ群、关注了各色AI绘图的博主，转眼间便梓泽丘墟，过往经验已成废品，新生技术眼花缭乱，逐渐放弃了追逐最新AI绘图工具的欲望。况且随着AI绘图的逐渐铺开——大家也习惯了辨识AI的风格，逐渐思考和分析AI绘图的不足，用AI绘图来创作，也成了一件普通且无新鲜感的事。

但是事情在这个月出现了变化——一位跑团群偶尔聊天的朋友，她突然开始大量地使用一位小众角色的表情包。从画风和细节可以看出，这些图应当是源于AI的，但过往的经验告诉我过去的AI模型难以如此精准地把握角色的人设细节和绘制动图。最重要的是，它的手画的很好！

看来事到如今，我落后的版本实在太多了。况且，先前还被人诟病”你怎么聊天打几百字也不用表情包“，但打开表情栏又觉得捉襟见肘——是时候，做一套自己单推角色的表情包了！

![开工！](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS01.png)

---

## 1 追往事：基于AI的跑团CG

从四年前开始跑团开始，我和群友就时常感慨——如此精彩的遭遇，要是有CG就好了！纵使文字绘声绘色，少了CG和特效，终究是令人想象时抱残守缺、多有遗憾。回想和伙伴们共同的冒险之时，记忆也变得模糊了起来。

随着跑团工具的更新，慢慢地有了智能特效、官方CG，但对一些独特的角色和能力，终究是难以表现——比如半身是章鱼半身是龙的变身野蛮人，我真的好想看一看她会长成什么样呱！一年前的GM（主持人）特意在结束前在贴吧上为我们的角色绘制了定制的人设图，虽然细节终究无法完全呈现，但也了却了大部分的心愿——至少，我们终于能看看我们在异世界，是如何冒险的了！

![偏好火球术的小鬼龙脉术士（我的形象）](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS02.jpg)


![可靠的野蛮人大姐姐（队伍里的主c，实际狂喜！PRPRPR~）](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS03.jpg)


![最后将大反派祷死的神裔牧师（虚假的善良人）](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS05.jpg)



![主敏的剑士（唯一的技能手，为数不多的真·善良人）](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS04.png)


但是，即便如此，能做出完全还原设定的角色已是极难，更何况不能有绘画错误（比如手），所以几乎不可能用现成的AI作品去衍生一系列的动作。不能看到自己喜欢的角色动起来，终究是一大遗憾。

---

## 2 昨日谈：从MID开始的动作派生

相比开源版本的社区版SD-AI绘图，midjourney以其官方服务中国市场、渠道易得（网上有售）、动作自然丰富在年中算是小火了一把。而且，使用discord的工作环境，比起浏览器操作让我更喜欢——至少它给了我一种对话般的体验和相对私密的氛围。

midjourney的图生图、动作衍生算是做的不错的，专向二次元形象和卡通形象的niji模型更是令人印象深刻——我喂了niji一张相对幼的缠流子同人图，它便可以给我拍生出这个同人的一系列形象、表情和动作，找到满意的结果后，还可以基于seed进行细调。

![还算不错的表情包九宫格](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS06.png)


但不到半天，我就算是玩腻了niji，问题也很明显：

- 人设不稳定，最基础的瞳色、挑染的位置和大小，niji不太能把握
- 老毛病，不太擅长画手
- 画风太固定，一眼AI，而且是一眼niji

而且就算是第一眼很炫酷的大头像，也能被艺术生挑出一大堆毛病。即便是我，也会在惊叹之余感到”有点不自然”。

![一眼炫酷但是毛病一堆](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS07.jpg)



那么，那位群友到底是如何制作出如此小众角色这么精良、这么丰富、这么稳定还会画手的表情包的呢？厚着脸皮，我打开了那位群友的私戳聊天栏：

> 姐，借借你的号行不？
> 

---

## 3 开新章：nai3带来的船新体验

今年11月末发布的novelai最新模型nai3可谓是相当无敌——也可以说是“人至贱则无敌”。它家盗用了大量版权作品，模型效果前所未有的无敌好——缠流子作为一个在同人领域相当冷门的角色，在用其它模型时我都得加大量Tag维持她那飘忽不定的挑染和易变的人设，而在用nai3时，我担心的却是“这也太像原作了直接拿来用会有版权问题的吧”？！

![画风太还原了呀喂！](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS08.png)



为了降低原作画风和加入新的元素，我甚至得调低{matoi ryuuko}的Tag权重才能把握好表情包和人设的平衡。过去AI的诸多痛点诸如画手、吃面在这一模型中得到了史诗级加强，它甚至连ns都能画!(东半球最强律师函警告)

![还好它没把nintendo的logo写的太清晰](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS09.png)

对于一些相对复杂的动作和姿势，nai3也支持局部蒙版细调、整体增强和派生作画，虽然体感上不如mid的垫图方便，但是在操作感上直接拉满，而且tag调校好之后的效果稳定性强的出人意料。

![西服头像](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS10.png)


![西服表情包1](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS11.png)



![西服表情包2](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS12.png)



![赛博朋克风](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS13.png)



![睡衣](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS14.png)



![和服](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS15.png)



![DND](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS16.png)


![夏日风格](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS17.png)


在nai3中生图后，直接进行AI抠图、AI调大小，最后用内置AI辅助的PS修改出图，导入主流通讯软件——QQ、微信、飞书、电报etc，除了微信，都非常方便！电报还可以不用审批上传表情包，分享（虽然私用并不会分享）也更方便了。

现在工具已经完成了，快给你的老板发送你最喜欢的表情包吧！

![乐](https://raw.githubusercontent.com/DF-Master/yidapicbed/main/2023/202312/202312MRSTICKS/202312MRSTICKS18.png)

乐

---

## 尾声

作为一个行业几乎不占AI的人，渐渐也感受到了AI深入生活的每一个毛孔——每天坐上工位，和AI组织公文，然后在AI的辅助下写代码，在AI指导下操作软件，然后在群里水AI表情包；下班后，回寝室享受扫地机器人的AI清洁程序，在AI的大数据推荐下看视频、买东西，和朋友聊聊AI领域的最新进展，最后拿出工资给AI续费……可谓是过云上生活，享赛博人生。虽然故事中的”赛博朋克”离现实很遥远，但换到十年前，我肯定会觉得今天过的是科幻生活了。

努力地跟进AI进展，倒也未必是有什么想法，只是隐约觉得不学就要被时代甩在后面了。虽然表情包只是一个起点，但今后的AI工具，只会一点点替代掉我桌上的扳手和螺丝刀，用一根网线把我死死地拴在云上。

现实的人是如此浅薄和无力，我深入云端，或许却是为了将来的逃避。