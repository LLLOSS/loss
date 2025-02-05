# 单极NMOS共源极放大器的设计

<center> <div style="height:2mm"><div style="fong-family:华文楷体;font-size:12pt;">
2024.9.17
</center>

## 一、实验目标

- 了解在AC仿真中进行其他参数扫描的方法
- 掌握共源晶体管放大电路的幅频特性，以及快速近似估计的方法
- 掌握高速共源放大器的设计方法并通过仿真进行验证
- 了解$\frac{g_{m}}{I_{D}}$工程设计思想,并初步掌握设计流程

## 二、实验要求

有一NMOS单级共源放大器,需设计偏置电流和晶体管尺寸,以满足15 GHz的特征频率和50倍的自增益,并尽可能优化功耗。

## 三、基础理论

 $\frac{g_m}{I_D}$(跨导效率，Transconductance Efficiency)是模拟电路设计中的一个关键参数，表示晶体管跨导$g_m$与偏置电流$I_D$之间的比值。它反映了晶体管在特定偏置电流下的放大能力以及功耗效率，是权衡增益和功耗的一个重要指标。

 定义

  - 跨导$g_m$: 跨导表示晶体管在输入电压变化时产生的输出电流增量，定义为：

    $$
    g_m=\frac{\partial I_D}{\partial V_{GS}}
    $$

    它表示输入电压$V_{GS}$的微小变化如何影响漏极电流$I_D$的变化。
  
  - 偏置电流$I_D$:偏置电流是通过晶体管的直流工作电流，也称为漏极电流。
  
  - $\frac{g_m}{I_D}$: 跨导效率表示**每单位电流所能产生的增益能力**。它的单位是$\mathcal{V}^{-1}$,反映了放大器在给定功耗下的增益能力。

 物理意义

  - 功率效率：$\frac{g_m}{I_D}$的值越大，表示在相同的偏置电流$I_D$下，晶体管能够提供更高的跨导$g_m$,即更
  高的增益。因此，**较高**的$\frac{g_m}{I_D}$表示放大器具有较高的功率效率，能以**较低**的功耗实现较高的增
  益。
  - 设计权衡：在低功耗设计中，通常希望$\frac{g_m}{I_D}$高一些，以降低电路功耗。但**较高**的$\frac{g_m}{I_D}$通常意味着
  晶体管工作在**较弱**的反转区域，增益**较高**但速度**较慢**；反之，较低的$\frac{g_m}{I_D}$,意味着晶体管工作在强
  反转区域，速度较快但功耗增加。
  
- 设计中的应用

  在设计模拟放大器时，$\frac{g_m}{I_D}$是一个非常重要的优化工具，可以帮助设计师在增益、速度、线性度和功耗之间进行权衡。设计时，通常会通过电路仿真来找到最合适的$\frac{g_m}{I_D}$ 值，以达到所需的性能指标。

  - 低功耗电路设计：在需要低功耗的电路中，设计师会希望选择高$\frac{g_m}{I_D}$ 的工作点(弱反转区或亚阈值区),以实现高能效。
  - 高速电路设计：在高速电路(如高频放大器)中，设计师会选择低$\frac{g_m}{I_D}$的工作点 (强反转区),以实现更高的速度和带宽。
 

<div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-17_16-29-23.png" width="80%"></div>


<p align="center">
图1：g<sub>m</sub>/I<sub>DS</sub>与I<sub>DS</sub>/I<sub>DSt</sub>的关系
</p>


- 

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-17_16-40-54.png" width="85%"></div>
  
<p align="center">
图2：不同区域下的特征频率及跨导
</p>


## 四、实验步骤

- 综合特征频率和自增益的要求，并尽可能降低功耗，选取$\frac{g_m}{I_D}$ = 10作为本次设计的跨导效率。查阅教材附录，为保证15GHz的特征频率和50倍的自增益，选取L=250nm的沟道长度，为方便后续调试不妨将$\frac{W}{L}$设为1。设计电路图如下
  
  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-17_17-23-40.png" width="75%"></div>

<p align="center">
图3：初始电路
</p>

  
- 为了找到$\frac{g_m}{I_D}$ = 10的偏置电压$V_{dc}$,设计DC仿真，并将$\frac{g_m}{I_D}$ - 10 作为输出函数，这样只需找仿真图像的零点即可。仿真参数和波形图如下：

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-17_17-43-55.png" width="100%"></div>
  
<p align="center">
图4：仿真求解Vdc
</p>


  由图可知，$V_{dc}$ = 570mV比较合适

- 将$$V_{dc}$$设置为570mV后，进行op仿真，结果如下

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-17_17-51-31.png" width="50%"></div>

<p align="center">
图5：op仿真结果(关键数据已圈出)
</p>


$$ 
    \frac{g_m}{I_D}=\frac{50.427u}{5.0601u}=9.97 
$$

$$ 
A_{0}=\frac{g_{m}}{g_{ds}}=\frac{50.4278u}{787.9879n}=64
$$


  可以看出，自增益符合要求

- 接下来检查特征频率，仿真参数和波形图如下：

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefined117710c350deb8b6956f9a19b65e806.png"></div>

<p align="center">
图6：特征频率的仿真参数和波形图
</p>


  特征频率只有10G，不符合要求，接下来需要对参数进行调整

- 考虑到强反型区的特征频率公式：

$$
f_{T,si}\approx\frac{g_{m}}{2\pi C_{GS}}=\frac{\mu_{0}C_{OX}\frac{W}{L}\left(V_{GS}-V_{TH}\right)}{2\pi\frac{2}{3}WLC_{OX}}=\frac{3\mu_{0}\left(V_{GS}-V_{TH}\right)}{4\pi L^{2}}
$$

  可以采取降低沟道长度，来提高特征频率，但是也要考虑到对增益的降低。

- 经过**无数次**的迭代调试，始终没能达到题目要求，增益上来了频率就掉，提高了频率增益就掉。

- 在无数次失败后，发现一个**重要结论**，那就是提高$V_{DS}$可以拉高自增益，在其它参数不变的情况下将**$V_{DS}$**从0.9V提高到1.8V时，自增益可以从64提高到75，虽然不多，但对接下来的调试已经足够。

- 之所以没有发现上述结论，是因为笔者认为增大漏源电压 $V_{DS}$ 会**加剧沟道长度调制效应**，导致漏极电流增大、**输出电阻减小**，最终导致增益降低。所以对于自增益增大这个结果，笔者想不出合理的解释，所以一直也没有考虑对$V_{DS}$进行增大。

- 在$V_{DS}$=1.8V的情况下继续调试，考虑到
  
$$
  f_{T,si}\propto \frac{1}{L^2}
  $$
  
  所以
$$
L_{new}=\sqrt{\frac{10GHz}{15GHz}} * 250nm\approx200nm
$$
  
- 修改沟道长度之后，其余参数不变，再分别进行op仿真和AC仿真，并将结果整合在一张图，如下图所示

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-17_20-17-46.png"></div>
  
<p align="center">
图7：op仿真和AC仿真的结果
</p>


  可以看出：

$$
  f_{T,si} > 16GHz
$$

$$
  A_{0}=\frac{g_{m}}{g_{ds}}=\frac{69.4266u}{1.2976u}=53.5 > 50
$$

$$
  \frac{g_m}{I_D}=\frac{69.4266u}{7.3302u}=9.47
$$

  这三个参数分别保证了特征频率、自增益和功耗。实现了三者的折中。

## 五、实验总结

- 通过实验验证了晶体管的特征频率与信号源电阻无关
- 公式的初步预估结果与实际的仿真结果有一定的差距，这表明在集成电路设计中，最终的设计定型都需要通过仿真实现，而电路理论则可帮助设计者在正确的方向上更好地优化电路。
- $\frac{g_m}{I_D}$工程设计方法可以摆脱工作区间和相应公式在电路设计中造成的困扰，方便了设计者。

