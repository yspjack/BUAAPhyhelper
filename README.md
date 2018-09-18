# BUAAPhyhelper

一个北航实验报告小工具，全是垃圾代码，没什么好看的。

（如果你也写了脚本 欢迎fork和pr~）

## 近期更新

- 添加了1071。

## TODO（咕咕咕咕咕咕咕咕咕咕咕）

- 1021和Matlab兼容
- 重构1021_1。
- 重构1051_1部分，考虑自动舍入。
- **打印和计算分离**
- 模块化，重复代码写个库。

## FAQ

Q：为什么保留位数和书本不同？

A：我大部分数据都多打印了一些位数，请自行按照“四舍六入五取偶”来得到数据（因为我懒）。

Q：如果我用你的脚本报告扣分了怎么办？

A：本人对脚本产生的任何后果概不负责。

## 1051

### 1.自组电位差计（必做）

按照书本P165输入所有数据后就可以按照书本顺序计算出所有值。

### 测试

`python3 main.py < Test.txt`

和课本上的数据对照即可。

### 2.箱式电位差计测电池电动势

我没做XD。

### 3.箱式电位差计测固定电阻

电路图略。

### 测试

`python3 main.py < Test.txt`

（其实没有正确答案

### 4.箱式电位差计测电表内阻

跟第二个一模一样的，不额外写了。

## 1021

垃圾仪器，要气死我了.jpg

### 1.测量冰的熔解热

#### 环境要求

**Octave**（别问我为什么）

如果一定要Matlab，请考虑用适当的积分函数替换cal_area.m中的quadv函数。

#### 实验数据输入

如果要输入你的数据，应该保证以下四个文件和main.m同一目录。

##### const文件

- 环境温度对应的阻值R0（单位千欧）。
- 冰的温度T1，一般为-21℃。
- 水的质量m（单位克）。
- 杯子质量m1（单位克）。
- 搅拌棒质量m2（单位克）。
- 冰的质量M（单位克）。

最终输入应该为一个6x1的矩阵。

##### down、melt、up文件

分别对应降温、溶解、升温曲线的数据，要求两列，第一列为时间t，第二列为对应的阻值R（单位千欧），说白了就是实验原始数据。

#### 可控变量

目前只有两个可控变量

- precision 对应面积相等要求的精度
- step 对应搜索面积相等点时候的区间长度

推荐 precision ≈ 10*step。

#### 最终输出

最终会输出对应的修正图像，L和K以及T2'和T3'。

![](http://a2.qpic.cn/psb?/V10hb9Qz3wPcMq/i2MSZX7D*cdJ2idIgAeub7yEZ0ePx0KLRlp0VFhvgBM!/b/dPkAAAAAAAAA&ek=1&kp=1&pt=0&bo=iASAAogEgAIDACU!&vuin=771644612&tm=1507989600&sce=60-1-1&rf=viewer_311)

### 注意

- 由于采用折线拟合，实际上计算会有很大的误差。
- K采用解微分方程后线性回归求得，可能跟以往处理不同。
- **代码非常非常垃圾**。

### 2.测量热功当量

#### 特别注意

本脚本采用的是《电热法测量热功当量实验的新探究》（蔡 晨，李朝荣，李英姿，王 选）中提到新处理方法，如果你没有测K请不要使用。

#### 环境要求

依旧是Octave。

#### 数据输入

##### const文件

- 室温对应的阻值。（单位千欧）
- 水杯质量。（单位克）
- 水质量。（单位克）
- 电压

最终输入应该是一个4x1的矩阵。

##### down、up文件

分别对应测k的时候数据和加热时的数据，要求两列，第一列为时间t，第二列为温度对应的阻值R。

#### 最终输出

- 系数K
- 热功当量J
- 相关系数r
- J不确定度u(J)

## 1042

emmmm，还算轻松的一个实验。

### 1.双电桥测低电阻

#### 环境要求

octave

#### 输入

##### R

R文件输入为四列，分别为对应的铜丝长度（厘米），正测电阻阻值（欧姆），反测电阻阻值（欧姆）以及使用的R1和R2值（欧姆）。

##### D

D文件输入为一列，为D的测量值和游标卡尺实际零点（毫米）。

**最后一行的数据应该是游标卡尺的实际零点（实验室垃圾卡尺零点经常不在0）。**

##### const

const文件输入只有一行一列，为标准阻值Rn的值（欧姆）。

#### 输出

- 正测反测的平均值Raver
- 每次得到的Rx
- b的值
- 电阻率tho
- b的不确定度
- D的a类、b类不确定度以及合成后的不确定度u_D
- tho的相对不确定度和不确定度

#### 特别注意

其实没什么特别注意的，修约依旧是自己看呗。

### 2.双电桥改单电桥测中电阻

#### 环境要求

python3

#### 使用

`python3 main.py`

然后按照提示输入测得的数据即可。

其中S表示灵敏度。

## 1091

唉，垃圾1091，不多说了。

### 1.迈克尔逊干涉

#### 环境要求

python3

#### 使用

直接

```shell
python3 main.py
```

根据提示完成即可。

#### 说明

- 标准值为632.8nm，但是书上并未要求计算两个误差。
- 相对误差在5%以内都可以接受（大概？）。

### 2.牛顿环干涉

#### 环境要求

octave

#### 输入

##### in

为一个10行2列的矩阵，第一列为第11-20环直径左边的位置，第二列为第11-20环直径右边的位置。

#### 输出

反正做的人也不多，这里从略了。

### 说明

- 没有标准值。

## 1031

还行，赞美于老师。

其他几个实验都没有复杂的数据处理，略了。

### 3.用模拟示波器测量声速

#### 环境要求

Octave.

#### 输入

##### const

应该为一个3x1的矩阵，依次为f1，f2，t。

##### data

应该为一个10x2的矩阵，第一列为第1\~10个读数，第二列为第11\~20个读数。

#### 输出

- 声速
- 不确定度计算
- 相对误差

#### 注意

- 处理的时候默认你是**连续**测得20个数据，和书上有一定区别。
- 这个实验精度比较高，一般相对误差应该是小于1%。

## 1071

啊，徐老师讲的真好。

### 2.测量三棱镜的顶角

#### 环境要求

**octave**

~~（octave对角度变换没有函数支持，懒得自己写）~~

Update: Using `mapping` package via `pkg load mapping`

If you're using Ubuntu, run the following command to install octave package.

```bash
sudo apt-get install octave-mapping
```

#### 输入

##### data

输入为一个nx8的矩阵，分别是a1,b1,a2,b2的度和分值。

#### 输出

- 平均值
- 顶角A
- a类b类不确定度
- 合成不确定度

以上所有输出有度分秒和度两种形式。

### 3.最小偏向角法测棱镜折射率

**octave**

~~（octave对角度变换没有函数支持，懒得自己写）~~

Update: Use `mapping` package

#### 输入

##### data

输入为一个nx8的矩阵，分别是a1,b1,a2,b2的度和分值。

注意这个矩阵是测量最小偏向角的数据。

##### Adata

把第二个实验的数据粘过来改名为Adata即可，这里要用第二个实验的数据的原因见课本。

#### 输出

- 折射率
- 最小偏向角的a类，b类，合成不确定度
- 折射率的合成不确定度**（计算的时候没有取对数）**

### 说明

- convert函数其实还存在一定bug，懒得改了。
- 第三个实验要用到第二个实验的数据。
