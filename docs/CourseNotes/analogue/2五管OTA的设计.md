# 五管OTA的设计

<center> <div style="height:2mm"><div style="fong-family:华文楷体;font-size:12pt;">
2024.6.1
</center>

## 实验目标

- 掌握五管OTA和电流镜的原理
- 理解输入共模范围的含义
- 体会放大电路各指标之间的折中

## 实验要求

设计如图所示的五管OTA电路，通过调整PMOS和NMOS的尺寸，使得达到如下的设计指标

<img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_09-42-27.png" >

设计指标如下：

<img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_09-44-47.png" width=30%>

##实验原理及内容
###设计$M_{3,4}$的尺寸

- 按最坏情况，输入共模尺寸最大时，$M_{1}$和$M_{2}$最容易进入线性区。只需保证在$V_{in}$ = 1.4V时，$M_{1}$和$M_{2}$没有进入线性区即可。

- 需要保证

$$
V_{in} - V_{F} < V_{TH1,2}
$$

  * $$V_{F} = V_{DD} - V_{SG3} \quad \Rightarrow \quad V_{in} - V_{DD} + V_{SG3} < V_{TH1,2}$$
  
    $$\Rightarrow \quad V_{SG3} - V_{TH3} < V_{DD} - V_{in} + V_{TH1,2} - V_{TH3}$$
    
    $$\Rightarrow \quad \sqrt{\frac{2I_{D}}{u_{P} C_{ox} \left( \frac{W}{L} \right)_{3}}} < V_{DD} - V_{in} + V_{TH1,2} - V_{TH3}$$
    
    $\Rightarrow \quad$电流值可以自己设定，不妨设 $I_{D} = 40\mu A,$ 由不等式的原理，右边整体要取最小值，则 $\ V_{in} \取最大1.4V $。考虑阈值电压的漂移，$V_{TH1,2}$取比0.4V较小一点，取0.3V。$V_{TH3}$取较大一些，取0.5V
    
    $$\Rightarrow \quad \sqrt{\frac{2I_{D}}{u_{P} C_{ox} \left( \frac{W}{L} \right)_{3}}} < 0.2V$$
    
    解得$\left( \frac{W}{L} \right)_{3} < 40$。由于阈值电压的取值留了充分的余地，因此$\left( \frac{W}{L} \right)_{3}$取边缘值40可行。

- $$\left( \frac{W}{L} \right)_{3} = 40$$

### 设计$M_{1,2}$的尺寸

- 记$M_{1}$和$M_{2}$的源极和$M_{5}$的漏极的公共点为P。

- 为使$M_{5}$一直在饱和区，需满足

$$
V_{p} > V_{GS5} - V_{TH5}
$$

  - 不妨设
  
$$
V_{GS5} - V_{TH5} = 0.2V，即V_{P} > 0.2V
$$

$$V_{P} = V_{in} - V_{GS5} > 0.2V$$

$$V_{GS5} - V_{TH1} + V_{TH1} < V_{in} - 0.2V$$

$$\sqrt{\frac{2I_{D}}{u_{n}C_{ox}({\frac{W}{L}})_{1}}} < V_{in} - 0.2V - V_{TH1}$$

  - 考虑阈值电压的飘移，$V_{TH1}$取0.5V，

    $$\Rightarrow \sqrt{\frac{2I_{D}}{u_{n}C_{ox}({\frac{W}{L}})_{1}}} < 0.2V$$

    $$\Rightarrow \text{取} \sqrt{\frac{2I_{D}}{u_{n}C_{ox}({\frac{W}{L}})_{1}}} = 0.15V$$

    解得
    
    $$\left(\frac{W}{L}\right)_{1} = 11.85$$


### 设计$M_{5,6}$的尺寸以及电流镜的值

- 对于$M_{5}$，它的电流$I_{D}$ = 80uA。$V_{GS5}$ - $V_{TH5}$ = 0.2V

$$\sqrt{\frac{2I_{D}}{u_{n}C_{ox}({\frac{W}{L}})_{5}}} = 0.2V$$

$$(\frac{W}{L})_{5} = 13.33$$

- 对于$M_{6}$ 不妨设置一个1:1电流镜，让$(\frac{W}{L})_{6}$ =$(\frac{W}{L})_{5}$ = 13.33

###设计电路图如下

<img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_11-59-31.png">

- 将直流共模电平设置为vcm，将vcm从0.9V到1.4V每0.1V设置一个点，就会有6次$V_{in}$的输入，对应6条$V_{out}$ 的输出。

  如下图所示

  <img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_15-46-14.png">

<img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_15-47-35.png">

  - 发现$V_{in}$至少在大于1.3V之后增益就掉到200以下。

### 对参数的改进

- $|A| = g_{m1,2}(r_{o2} \parallel r_{o4})$
- $g_{m1,2}$= $\frac{2I_{1,2}}{V_{GS1,2}-{V_{TH1,2}}}$ 
- $r_{o2,4}$≈ $\frac{1}{λI_{2,4}}$ 

- 若增益不满足条件：

  - 通过适当减小$V_{GS1,2}$来增大跨导，但仍需满足之前的不等式
  - 通过增大沟道长度来增大输出电阻，但需保持宽长比不变
  - 通过减小电流来增大输出电阻

- 选择减小电流$I_{D}$ ，将电流源80uA减小为60uA。重复之前的仿真操作，得到的电路和数据如下：<img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_16-04-29.png">

  <img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_16-05-59.png">

  <img src="https://picgo-loss.oss-cn-beijing.aliyuncs.com/undefinedSnipaste_2024-06-01_16-07-36.png">

- 可以看到，这次增益均达到了200，在Vcm=0.9V和1.4V时进行op仿真，发现所有MOS管均在饱和区。至此，所有要求均已完成。

  