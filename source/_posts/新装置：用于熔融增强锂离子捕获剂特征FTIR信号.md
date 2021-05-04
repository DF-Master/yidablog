---
title: 新装置：用于熔融增强锂离子捕获剂特征FTIR信号
date: 2021-03-10
tags:
- 学术
categories:
- 学术
mathjax: true

---


---

# 新装置：用于熔融增强锂离子捕获剂特征FTIR信号

## 引言

今天，因Li电池的大量应用、核废料的回收问题，Li配合物受到了人们的广泛关注。<sup><a href="#ref1">1,2</a></sup> 分析Li金属有机配合物结构的常用方法有理论计算、FTIR、质谱等，二维红外光谱更是可以通过Stokes-Einstein公式$D=kT/8\pi\eta r^3$z直接判断Li<sup>+</sup>的配位数。<sup><a href="#ref3">3,4</a></sup> 但是，Li<sup>+</sup>盐在有机溶剂中的溶解度一般不会高于0.1 M，<sup><a href="#ref5">5</a></sup> 其部分金属有机配合物在有机溶剂中的溶解度更加有限。因此，直接熔融有机配体以提高配合物溶解度并进一步增强其光谱信号成为了一种可行的办法。

已知，潜在的Li捕获剂**A1、B1**所形成的的金属有机配合物在有机溶剂中FTIR信号较弱。为分析**A1**形成的Li<sup>+</sup>金属有机配合物结构特征，我结合工学设计、通信、编程、云服务、仪器分析的知识与技术，独立尝试了：

- 设计绝缘隔热模具
- 模拟判断实验室所需的PID参数
- 设计PID网络温控器，实现远程控制、网页管理
- 在特定温度熔融**A1**,增强配合物FTIR信号，为二维红外实验做准备<sup><a href="#ref6">6</a></sup> 

![image-20210304232934783](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310203347.png)

<center><font color="gray">图1 A1、B1外观与其结构示意图
    </p></font></center>

    
## 模具设计

玻璃树脂纤维绝缘隔热模具的CAD设计图如图**2**所示。因FTIR装置可放置模具的空间较小，我设计了一套全新的模具。上方留孔是为了通线且保持空气流通。

![image-20210310210159688](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310210159.png)

<center><font color="gray">图2 玻璃树脂纤维绝缘隔热样品池设计图
    </p></font></center>

## PID温度控制技术模拟

为实现测量模具内样品特定温度下的转动特性，我需要对实验时PID参数设置有准确期望，为此我从PID原理入手，进行了信号模拟分析。

**PID**（**P**roportional **I**ntegral **D**erivative）最早源自于船舶的自动操作系统，是迄今为止最简单有效的控制技术。<sup><a href="#ref7">7</a></sup> 约翰·美斯菲尔德说过：“我只要一艘船，和一颗为她掌舵的星。”但人眼是有极限的，俄裔美国工程师尼古拉斯·米诺尔斯基（Minorsky 1922）已用PID技术超越了当时最好的舵手，实现了$\pm1/6$°的船舶角度控制。<sup><a href="#ref8">8,9</a></sup> 模拟效果如图**3**所示。

![image-20210310221544889](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310221544.png)

<center><font color="gray">图3 PID系统对扰动体系的稳定作用的模拟曲线</font></center>

其原理如下：
$$
{\mathrm  {u}}(t)={\mathrm  {MV}}(t)=K_{p}{e(t)}+K_{i}\int _{0}^{t}{e(\tau )}\,{d\tau }+K_{d}{\frac  {d}{dt}}e(t)
$$
符号及其对应的物理意义如表**1**所示：

<center><font color="gray">表1 公式符号及其物理意义对照表 </font></center>

| 符号                    | 物理意义                        |
| ----------------------- | ------------------------------- |
| ${\displaystyle K_{p}}$ | 比例控件，是可调参数            |
| ${\displaystyle K_{i}}$ | 积分控件，也是可调参数          |
| ${\displaystyle K_{d}}$ | 微分控件，也是可调参数          |
| ${\displaystyle e}$     | 误差=设定值（SP）- 回授值（PV） |
| ${\displaystyle t}$     | 目前时间                        |
| ${\displaystyle \tau }$ | 积分变数，数值从0到目前时间     |

PID本质上是拉普拉斯变换后使信号振荡衰减毕竟设定值的滤波器，每个控件参数的作用及设置分析如下：

### 比例（P）控件

比例控件的输出为：
$$
P_{\mathrm  {out}}=K_{p}\,{e(t)}
$$
比例控件决定了输出的速度。由于其与误差大小直接线性相关，所以误差越大，输出越大。当系统达到设定值时，比例控件输出为0。但是，比例控件参数过大会导致控制精度下降，如图**4**所示。

调节P参数时，应调节P参数至出现震荡，再适当减小振幅。

![image-20210310215640876](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310215640.png)

<center><font color="gray">图4 比例控件对系统的影响的模拟曲线
   </font></center>


### 积分控件

积分控件的输出为：
$$
I_{\mathrm  {out}}=K_{i}\int _{0}^{t}{e(\tau )}\,{d\tau }
$$
积分控件可以积分消除过程中的平均误差，并能压制比例控件所不能解决的、多余的调整值。如图**5**所示，在引入线性干扰信号，如实验室中的热源干扰或散热干扰后，积分控件的稳定作用显著。

实验时为开放环境，应适当增大I参数。

![image-20210310215853612](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310215853.png)

<center><font color="gray">(5a) 误差无线性增长下的模拟曲线</font></center>

![image-20210310215857377](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310215857.png)

<center><font color="gray">(5b) 误差含线性增长项的模拟曲线</font></center>

<center><font color="gray">图5 积分控件对系统的影响的模拟曲线</font></center>

### 微分控件

微分控制的输出为：
$$
{\displaystyle D_{\mathrm {out} }=K_{d}{\frac {d}{dt}}e(t)}D_{\mathrm  {out}}=K_{d}{\frac  {d}{dt}}e(t)
$$
微分控件通过对误差求导，减小偶然误差，使系统能更快地对突然产生的改变做反应。如图**6**所示，微分控件能消除系统快速变化造成的影响。

实验室可能存在人员走动、移动仪器等干扰，需每次适当增减D参数。<sup><a href="#ref10">10</a></sup>

![image-20210310220243148](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310220243.png)

<center><font color="gray">图6 微分控件对系统的影响的模拟曲线</font></center>

## 温控装置的搭建

在现有模具与PID参数期望的基础上，需要组装整套温控装置来精确控温。温控装置所需功能如表**2**所示。

<center><font color="gray">表2 FTIR光谱仪温控装置的所需功能</font></center>

| 目标                 | 说明                                                                                                                         |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 具有相当宽的工作范围 | 潜在的Li离子捕获剂的熔点可能存在较大差异；  例如，我们实验室关心的两种分子中，A1的熔点是131-133 °C，而B1的熔点是72-74 °C。   |
| 控温稳定             | 根据Stokes-Einstein方程$D=kT/8\pi\eta r^3$ ,分子的扩散常数与温度线性相关。  为精确分析其转动特性，应尽可能减小温度震荡范围。 |
| 价格合适             | 不应当超出本科生科研的预算。                                                                                                 |
| 高度模块化           | 适合未来的改造，能用于一维与二维红外光谱实验。                                                                               |
| 便于操作             | 希望能从计算机而非仪器上操作，更进一步地提供数据监测、报警等功能。                                                           |

经过三次迭代，最终实现上述功能的温控装置如图**7**所示。仪器与办公室主机远程通信，通过服务器发布结果于网页，相比传统仪器，其优点有：

- 可视化：有多种界面供调试，使用，速览；
- 远程管理：延迟低，占用小，美观性高，免费；
- 参数可调：随时可查询记录、调参优化；
- 模块化：小型一体化，接口简单，高度模块化、集成化；
- 廉价：主结构不超过千元。

![image-20210310220803379](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310220803.png)

<center><font color="gray">图7 控温装置整体结构示意图</font></center>

主机可视化操作界面如图**8 - 9**所示。装置外观及其内部结构如图**10**所示。网页可以通过图**7**中二维码扫码查看。

![QQ图片20210305113848](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310223152.jpeg)

<center><font color="gray">图8 面向调试的监控程序界面</font></center>

![image-20210305114305041](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310223234.png)

<center><font color="gray">图9 面向使用的监控程序界面</font></center>

![image-20210310223534546](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310223534.png)

![image-20210310223458640](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310223458.png)

<center><font color="gray">图10 装置外观及其内部结构</font></center>

## 温控装置实验

为验证该装置控温效果，对新装置进行干烧控温测试，热电偶直接放于陶瓷加热片上，实验结果如图**11**所示。可以看出，P = 2，I = 5000，D = 100时控温效果最佳，温度控制精度为 $\pm$0.5 °C。实验时高频微扰不显著，增大D的效果不够明显；增大P会显著导致振荡范围加大，控制精度下降；增大I对控温能力的辅助最为明显，表明系统的主要误差是平均误差。

![image-20210310223844766](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310223844.png)

<center><font color="gray">图11 干烧加热片温度控制曲线图</font></center>

将加热片置于绝缘隔热样品池中，加热装有待测样品**B1**(4,4,4-trifluoro-1-(naphthalen-2-yl)butane-1,3-dione)及其Li配合物的CaF<sub>2</sub>片，实验结果如图**13**所示。考虑到样品在71-73 °C附近熔融可能会造成偶然误差，适当调大了最佳参数设置的微分控件参数。

![image-20210310223957089](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310223957.png)

<center><font color="gray">图12 对CaF2片中B1样品加热温度控制图</font></center>

在P = 2，I = 5000， D = 1000的参数设置下，对样品实现了对样品$\pm$ 0.5 °C的精确控温。该结果与干烧结果比较相近，这和样品池的结构有关。虽然样品池自身具有绝缘隔热功能，但通光孔完全暴露在空气中，且样品较少，整体比热容较低，与干烧状态环境相似。

由此可见，最佳PID参数的大致特性与**PID温度控制技术模拟**所得结论一致。

综上所述，我独立设计、制造了可在FTIR光谱仪中使用的绝缘隔热模具与可以实现手机一码管理的自动化温控装置，最终实现了最高 $\pm$0.5 °C的可优化精度的、可视化的温控系统。

## FTIR光谱实验

是在完成了上述装置后，我将装置应用于Li金属有机配合物的信号增强上。

首先，为预测2**A1 –** Li金属有机配合物可能的结构，用Gaussian16以M062x对其进行计算分析。**A1**及其配合物可能的结构如图**13**所示，其红外光谱特征峰计算结果如图**14**所示。二者均已乘校正系数。计算表明，若**A1**与Li形成了2**A1 –** Li金属有机配合物，应在1650 cm<sup>-1</sup>与1311 cm<sup>-1</sup>处表现出特征峰，并在1700 cm<sup>-1</sup>表现出显著的信号衰减。

 ![image-20210310225136003](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310225136.png)![image-20210310225203781](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310225203.png)

<center><font color="gray">图13 A1及A1-Li配合物可能的结构</font></center>

   ![image-20210310230042401](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310230042.png)

![image-20210310230110025](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310230110.png)

<center><font color="gray">图14 A1及A1-Li配合物红外光谱计算结果图</font></center>

随后，为了进一步确认实际形成的2**A1**-Li的结构与计算结果一致，需要分析其FTIR光谱以寻找其特征峰。在实际实验中，经过反复筛选，最终确定了HCCl<sub>3</sub>是溶解**A1**及其金属有机配合物效果最好、背景干扰最少的溶剂，结果如图**15**所示。在1560  cm<sup>-1</sup>与1335 cm<sup>-1</sup>处，可以看到2**A1** – Li的特征峰，但信号较弱，不利于用二维红外进一步分析其转动特征。1620 cm<sup>-1</sup>无明显信号减弱，表明体系中仍主要以**A1**为主，形成配合物的**A1**较少。

![image-20210310230344962](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310230345.png)

<center><font color="gray">图15 A1及2A1-Li配合物溶液FTIR光谱图</font></center>

为进一步增强信号，采用新装置对样品池恒温加热。在加热至160 °C熔融**A1**后，如图**16**所示，2**A1**-Li金属有机配合物的信号显著增强。可以看出，1362 cm<sup>-1</sup>处有显著的新峰，1620 cm<sup>-1</sup>处的峰降低明显，1560 cm<sup>-1</sup>处的绝对信号增强虽不明显，但相对强度增强极其明显，证明了熔融能显著增强2**A1**-Li金属有机配合物的溶解度及其FTIR信号，验证了新装置的有效性。

![image-20210310230605889](https://gitee.com/DF-Master/yidapicbed/raw/master/20210310230606.png)

<center><font color="gray">图16 A1及2A1-Li配合物熔融FTIR光谱图</font></center>

综上所述，通过设计绝缘隔热模具与新型基于PID的网络控温装置，我熔融了**A1**，大大提高了2**A1**-Li金属有机配合物的溶解度并增强了它的FTIR信号，并进一步为分析研究**B1**及其配合物的FTIR光谱、进行二维红外光谱实验以分析其转动特征提供了可能性。

## 总结与展望

为增强有机溶剂中溶解度较小的2**A1**-Li金属有机配合物的FTIR信号，本文通过数据模拟方式分析了制造PID温控装置的可行性与可能的参数设置，通过独立制造的可一码远程管理、具有网页可视化界面、能程序化调参的网络温控装置，将**A1**升至160 °C熔融以提高2**A1**-Li金属有机配合物溶解度，大大增强了2**A1**-Li金属有机配合物的FTIR信号，为后续二维红外实验分析其转动光谱特征提供了可能。此外，质谱分析、热力学分析等手段验证其结构也是可行的方案。

未来，该装置还可通过更换加热负载、样品池等模块，进一步用于二维红外光谱仪、荧光光谱仪、紫外光谱仪等仪器，并增加温度报警、自动预实验、稳定区可视化提示、数据库数据互动分析等功能。相比商用仪器，该仪器操作友好，可视化程度高，价格低廉，改装容易，具有极大的发展潜力。

## 致谢

感谢北京大学化学与分子工程学院图书馆提供文献查阅服务。

感谢郑俊荣、于志浩老师给予我指导与鼓励，让我敢于磨砺自身的知识与技能。

感谢实验室师兄师姐牺牲科研时间给予我指导，回答我愚蠢至极的问题。

感谢张奇涵老师和其他化学与分子工程学院的老师，在我们本科生科研与教育上付出如此多的心血。

感谢我的父亲、母亲，为离家千里的我操碎了心。谁言寸草心，报得三春晖，这番恩情我一辈子都难以报还。

感谢我最好的朋友沈杨翊、莫文韬、徐逸飞，在我心情最低落的时候给予我鼓励，耐心地教会我知识和技术，让我能一直坚持到最后，没有你们就没有我的这篇报告。

感谢叶昕波、魏旭炎、程祥松等一系列在过程中帮助过我的人。你们的热心让我感到幸福。

## 引用文献

1     <span name = "ref1">严宣申.   (北京大学出版社, 北京, 1999).</span>

2     <span name = "ref2">Engineering, N. S. a. *Documents Related to Liquid-Halide (Fluoride and Chloride) Reactor Research and Development*, <[https://web.archive.org/web/20140903095137/http://www.energyfromthorium.com/pdf/](https://web.archive.org/web/20140903095137/http:/www.energyfromthorium.com/pdf/)> (1957).</span>

3     <span name = "ref3">Jiang, B. *et al.* The Anion Effect on Li(+) Ion Coordination Structure in Ethylene Carbonate Solutions. *J Phys Chem Lett* **7**, 3554-3559, doi:10.1021/acs.jpclett.6b01664 (2016).</span>

4      <span name = "ref4">Yuan, K. *et al.* Coordination number of Li+ in nonaqueous electrolyte solutions determined by molecular rotational measurements. *J Phys Chem B* **118**, 3689-3695, doi:10.1021/jp500877u (2014).</span>

5     <span name = "ref5"> Xin, N., Sun, Y., He, M., Radke, C. J. & Prausnitz, J. M. Solubilities of six lithium salts in five non-aqueous solvents and in a few of their binary mixtures. *Fluid Phase Equilibria* **461**, 1-7, doi:10.1016/j.fluid.2017.12.034 (2018).</span>

6      <span name = "ref6">Wescott., T. PID without a PhD. *EE Times-India.* (2000).</span>

7     <span name = "ref7"> Bennett, S. A brief history of automatic control. *IEEE Control Systems Magazine (IEEE).* **16**, 17–25 (1996).</span>

8     <span name = "ref8"> Bennett, S. A history of control engineering, . 48 (1993).</span>

9     <span name = "ref9"> Li, Y. a. A., K.H. and Chong, G.C.Y. . PID control system analysis and design - Problems, remedies, and future directions. . *IEEE Control Systems Magazine,* **26**, 32-41 (2006).</span>

10  <span name = "ref10">Kiam Heong, A., Chong, G. & Yun, L. PID control system analysis, design, and technology. *IEEE Transactions on Control Systems Technology* **13**, 559-576, doi:10.1109/tcst.2005.847331 (2005)</span>


