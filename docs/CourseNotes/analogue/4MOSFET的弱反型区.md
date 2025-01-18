# MOSFET的弱反型区

<center> <div style="height:2mm"><div style="fong-family:华文楷体;font-size:12pt;">
2024.9.11
</center>

## 一、实验要求

分别估算本书所使用工艺NMOS和PMOS晶体管亚阈值系数的值；通过对仿真结果的分析，大致寻找弱反型区与强反型区之间的过渡区域。

## 二、实验原理及过程

- 偏置在弱反型区MOSFET的跨导为

$$g_{m,w_{i}}=\frac{I_{D}}{\eta{V_{T}}}$$

- 首先对NMOS进行分析，设计如题目所示的电路如下

<img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-10_23-26-11.png" width="80%">

​	进行题目要求的DC仿真，结果如下

<img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-10_23-27-44.png" width="100%">

- 分析发现，NMOS的阈值电压$V_{TH}$在0.4V左右，取$V_{GS}$= 0.38V的弱反型区进行分析

  <img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-10_23-40-10.png" width="50%">

$$
\eta= \frac{I_{D}}{g_{m,w_{i}}V_{T}}= \frac{1.8253u}{26.5655u*26m}=2.64 
$$

- 将NMOS换成同等尺寸的PMOS，将Vin调整为1.4V，使得Vs-Vd略小于Vth，进行op仿真结果如下

  <img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-09-11_00-19-53.png" width="50%">

$$
\eta= \frac{I_{D}}{g_{m,w_{i}}V_{T}}= \frac{42.7474n}{994.3032n*26m}=1.65 
$$

- 通常情况下，1<$\eta<3$。当$V_{\mathrm{GS}}$满足$V_{\mathrm{GS}}<V_{\mathrm{TH}}-\eta kT/q$ 时，一般认为MOSFET 进入弱反型区域；而当$V_{\mathrm{GS}}>V_{\mathrm{TH}}+\eta kT/q$时，可认为 MOSFET 工作在强反型区。
