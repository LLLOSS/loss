# 五管OTA的输入等效失调电压优化

<center> <div style="height:2mm"><div style="fong-family:华文楷体;font-size:12pt;">
2024.11.04
</center>

## 一、实验目标

- 深入理解并学会计算运算放大器的随机性失调和系统性失调
- 学会通过对电路参数的设计来满足系统性设计失调的设计要求
- 学会使用蒙特卡罗仿真工具仿真电路中随机失调的情况

## 二、实验要求
一个五管OTA如图1所示，共模电压为0.9V，设计晶体管的尺寸，使得电路的跨导$g_m$大于1$mA/V$，通过优化晶体管尺寸使等效输入失调电压尽可能接近N（0，$(0.25mV)^2$）的正态分布。

<div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefined%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241104205302.jpg" width="50%"></div>


<p align="center">
图1：五管OTA电路
</p>


## 三、理论求解

### (1)晶体管面积尺寸设计

$$
\begin{align}
V_{OS}&=V_{OS1,2}+\frac{I_{OS3,4}}{g_{mP}}
\\&=\Delta V_{TH1,2}+\frac{\left(V_{GS}-V_{TH}\right)_{1,2}}{2}\left(\frac{\Delta\frac{W}{L}}{\frac{W}{L}}\right)_{1,2}+\frac{g_{m3,4}}{g_{m1,2}}\Delta V_{TH3,4}+\frac{\left(V_{GS}-V_{TH}\right)_{1,2}}{2}\left(\frac{\Delta\frac{W}{L}}{\frac{W}{L}}\right)_{3,4}
\end{align}
$$

- 根据上式,在做初步设计时可以假设**忽略尺寸失调**带来的影响，从而专注对**阈值电压失调**的分析。
- 假设差分对跨导是电流镜跨导的两倍，即 $g_{\mathrm{mP}}=2g_{\mathrm{mN}}$。由于两个元件随机失调值均符合正态分布，则简化后的随机性等效输入失调公式为

$$
\sigma_{V_{\mathrm{OS}}}^2=\sigma_{V_{\mathrm{THP}}}^2+\left(\frac{g_{\mathrm{mN}}}{g_{\mathrm{mP}}}\right)^2\times\sigma_{V_{\mathrm{THN}}}^2
$$

- 根据设计要求 $\sigma_{V_{\mathrm{OS}}} < 0.25$ mV, 即 $\sigma_{V_{\mathrm{OS}}}^2 < 0.0625$ (mV)$^2$。已知 PMOS 晶体管和 NMOS 晶体管的阈值电压失调均满足同样的分布，不妨假设 $\sigma_{V_{\mathrm{THP}}}^2 = \sigma_{V_{\mathrm{THN}}}^2$。结合上式可知应有：

$$
  \frac{5}{4}·{\sigma^2_{V_{THP}}} ·2\leq 0.0625(mV)^2
  \\解得{\sigma_{V_{THP}}}\leq 0.1581mV
$$

$$
\sigma_{\Delta V_{\mathrm{T}}} = \frac{A_{\mathrm{VT}}}{\sqrt{WL}}, \quad A_{\mathrm{VT}} \approx 3.6~\mathrm{mV \cdot \mu m}
$$

- 考虑设计冗余取${\sigma_{V_{THP}}}=0.15mV$,带入上式得到：

$$
WL = 576~\mathrm{\mu m}^2
$$

### (2)晶体管宽长尺寸设计

- 题目要求$g_{m2}>1m$,则：

$$
  g_{m2}=\frac{2I_{D}}{{{(V_{SG}-V_{TH})_2}}}=\frac{200\mu}{{{(V_{SG}-V_{TH})_2}}}>1m
  \\{{(V_{SG}-V_{TH})_2}}<0.2V
$$

- 不妨令

$$
  \frac{g_{m2}}{g_{m4}}=\frac{{(V_{GS}-V_{TH})_4}}{{(V_{SG}-V_{TH})_2}}=2
$$

- 取${{(V_{GS}-V_{TH})_4}}$=240mV,求解$M_4$与$M_3$尺寸过程如下：

$$
\begin{gather}
I_{D} = \frac{1}{2}\mu_{n}C_{ox}(W/L)_{3}(V_{GS}-V_{TH})^{2} = 100 \mu A \\[10pt]
\mu_n C_{ox} \approx 300 \, \mu A/V^2 \\[10pt]
(V_{GS} - V_{TH})_4 = 0.24 \, V \\[10pt]
WL = 576 \, \mathrm{\mu m}^2
\end{gather}
$$




- 解得
  
$$ 
\begin{align}
  \frac{W}{L}=16.66  \\[10pt]
  L_{3,4}=5.9\mu  \\[10pt]
  W_{3,4}=98u  \\[10pt]
\end{align}
$$
  
- ${{(V_{SG}-V_{TH})_2}}$=120mV,求解$M_1$与$M_2$尺寸过程如下：
  
$$
\begin{gather}
  I_{D}=\frac{1}{2}\mu_{p}C_{ox}(W/L)_{2}(V_{SG}-V_{TH})^{2}=100\mu A \\[10pt]
  \mu_pC_{ox}\approx50 μA/V^2 \\[10pt]
  {{(V_{GS}-V_{TH})_2}}=0.12V \\[10pt]
  WL = 576~\mathrm{\mu m}^2   
\end{gather} 
$$

- 解得

$$
\begin{gather}
  \frac{W}{L}=278  \\[10pt]
  L_{3,4}=1.44\mu \\[10pt]
  W_{3,4}=400u
\end{gather}
$$
  

## 三、仿真验证

- 按照设计参数搭建电路图如下

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_21-58-44.jpg" width="75%"></div>

  
<p align="center">
图2：五管OTA仿真电路
</p>


- op仿真结果如下，$g_m$达到要求，管子工作在饱和区。

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_22-03-21.jpg" width=75%></div>

  
<p align="center">
图3：op仿真
</p>


- 加载蒙特卡罗仿真，并对0.9V时的共模电压进行处理，结果如下：

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_22-09-44.jpg" width="75%"></div>

  
<p align="center">
图4:400次蒙特卡罗仿真结果的直方图分布
</p>


  可以看出，未达到0.25m的实验要求，需要进一步迭代参数

## 四、迭代电路

- 实验值是理论的大约2倍，考虑到WL与$\sigma_{V_{\mathrm{OS}}}^2$的反比关系，WL将变成原来的4倍，为保证静态工作点稳定现将PMOS管W和L同等扩大到原来的2倍，设计电路图如下：

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_22-18-01.jpg" width="75%"></div>

  
<p align="center">
图5:调整后的电路
</p>


- 蒙特卡洛仿真结果如下：

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_22-21-15.jpg" width="75%"></div>

  
<p align="center">
图6:400次蒙特卡罗仿真结果的直方图分布
</p>


- 可以看到，指标改善$\frac{500}{360}$=1.38倍，而$\frac{360}{250}$=1.44，照此趋势，还需将PMOS管子的宽长同比扩大2倍多一些，在这里选择将POMS宽长比再同时扩大2.5倍，设计电路如下

  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_22-27-13.jpg" width="75%"></div>

  
<p align="center">
图7:第二版迭代电路
</p>


- 蒙特卡洛仿真结果如下，可以看出${\sigma_{V_{THP}}}$=0.245m<0.25m，满足要求：
  
  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_22-30-48.jpg" width="75%"></div>
  
  
<p align="center">
图8:400次蒙特卡罗仿真结果的直方图分布
</p>


- op仿真检查静态工作点，结果如下,所有管子正常工作，$g_m$=1.53m>1m，满足要求：
  
  <div align="center"><img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-11-04_22-35-25.jpg" width="75%"></div>
  
  
<p align="center">
图9:终版电路的静态工作点检查
</p>


## 五、实验总结

- **理论计算与初步设计**：基于五管OTA的结构特点，首先分析了影响失调电压的主要因素，并通过调整晶体管的尺寸，使得跨导满足设计需求。初步设计忽略了**尺寸失调**的影响，集中于**阈值电压失调**的计算，以满足失调电压接近正态分布的要求。
- **仿真验证**：在初步设计参数的基础上，进行电路仿真验证，确认电路在饱和区内工作。通过蒙特卡罗仿真模拟随机失调的分布情况，发现初始设计未达到失调电压小于0.25 mV的指标，需进一步优化参数。
- **参数迭代优化**：通过多次调整晶体管的宽长比，**特别是增加PMOS管的宽长尺寸**，逐步降低了失调电压。最终设计通过再次迭代将PMOS管的宽长比扩大2.5倍，仿真结果达到0.245 mV，符合实验指标。
- **失调电压的本质与其影响**：运算放大器的失调电压直接影响其性能，尤其在高精度应用中，如信号处理、模数转换等领域。五管OTA的失调电压源于两类因素：一是**随机性失调**，包括器件匹配偏差、制造工艺波动等；二是**系统性失调**，主要因电路布局和器件尺寸的设计不当引起。本次实验从这些失调的本质出发，优化电路设计参数，使其接近理想状态，对高精度电路设计具有重要的借鉴意义。
- **精密电路设计中的迭代优化方法**：在电路设计中，特别是高精度电路设计中，往往需要多次迭代优化。这一实验中，我们采取了两次主要的器件尺寸迭代调整，通过**增大PMOS的宽长尺寸**来降低失调电压。
