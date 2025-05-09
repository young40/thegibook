---
title: 4.1 概率论基础
---

自然界中的很多现象或事件，在一定的范围之内是随机发生的，称为随机事件（random events）。然而经过人们的观察，在这些事件的大量重复的过程中，它们的分布却呈现出某种规律性，例如股票的波动，人口统计中的一些特性，骰子分布等等。因此，统计学就是一门通过对大量采样样本进行统计以计算出其分布规律的学科。而既然随机事件在大量重复试验下服从一定的分布，那么如果我们已知某随机事件服从某一分布，就可以通过大量重复试验来计算该随机事件的某些特征，例如统计平均值。这样就可以使用随机的方法来解决确定性的问题。



### 随机变量
为了利用随机性来解决数学问题，首先需要使用数学语言来描述随机事件。在数学中，随机事件用随机变量（random variables）来表示，随机变量用大写字母表示，例如$X$。随机变量是一个函数，它将某一集合内的随机事件（或者另一个随机变量）映射到一个数值的集合，或者通俗地说，随机变量$X$用一个数值来表述一个随机事件，例如用1，2，3，4，5和6这六个数值来表述骰子的六个可能的随机事件，这样就可以用数学方法来描述随机事件。随机变量的值用小写字母表示，例如$x$，称为随机数（random numbers）。随机变量的输入集合也可以是另一个随机变量，这时我们将服从一种分布的随机变量转换为服从另一种分布的随机变量（注意：一个随机变量的值是某个随机事件的数学表示，当我们看到一个随机变量时，它不是一个普通的数字，我们应该要联系到它背后的随机事件，例如对于骰子，随机变量的值6表示的是某一次骰子记录的结果为数字为6的那一面朝上。所以我们说随机变量始终是一个“映射”或“函数”，但是仅有将一个基本的随机变量（如$X$）转换为了一个分布的随机变量（如$Y$）时，才能写成函数的形式，对于基本随机变量$X$，它仅表示一种映射。），例如：$Y=f(X)$。

随机变量$X$的每个值$x$都关联着一个概率，即每次采样时该值（或对应随机事件）出现的概率，随机变量所有可能值组成的概率分布函数称为概率密度函数（probability density function，PDF），用$p$表示，如图（1）(a)所示。

<div>
    <div align="center" id="f:mc-cdf">
        <img src="/img/figures/mc/cdf.svg" width="550" />
    </div>
    <p align="left"><b>图（1）：</b>概率密度函数p(x)表示随机采样结果处于$[x,x+dx]$区间的概率，相应地，累积分布函数则是采样的结果处于$(-\infty,x]$区间内的概率</p>
</div>

随机变量可以是离散或连续的，例如骰子游戏，每次扔骰子的结果被映射为一个离散的随机变量的值$x_i$，所有值的集合为$X=\{1,2,3,4,5,6\}$，第$i$个随机数值出现的概率为$p_i=1/6$。对于离散随机变量，每个随机数对应的概率满足：$0\leq p_i \leq 1$，所有离散变量的概率之和满足：$\sum_i p_i=1$。

对于连续随机变量$X$，其概率密度函数$p(x)$是通过落于$x$附近的区间$[x,x+dx]$内的随机数的概率$p(x)dx$来定义的，然而这种定义方式并不直观，所以连续随机变量的概率分布一般通过更直观的称为累积分布函数（cumulative distribution function，CDF）来定义，连续随机变量$X$的累积分布函数用大写字母$P$表示，其定义为：

$$
	P(y)=Pr\{x\leq y\}={\rm \int}_{-\infty}^{y}p(x){\rm d}x
$$
<Eq num="1"/>

累积分布函数$P(y)$定义的是所有随机数的值中小于或等于$y$的随机变量的概率的积分（注意这里我们使用两种形式来表示累积分布函数，$P(y)$所代表的变量形式，以及$Pr\{x\leq y \}$所代表的范围的形式。}，所以累积分布函数是一个递增函数，如图（1）(b)所示。连续随机变量的概率密度函数$p(x)$具有以下属性：

$$
	\begin{aligned}
		\forall x: p(x)&\geq 0\\
		{\rm \int}_{-\infty}^{+\infty}p(x){\rm d}x&=1\\
		p(x)&= \cfrac{{\rm d}P(x)}{{\rm d}x}
	\end{aligned}
$$
<Eq num="2" id="eq:mc-continuous-pdf"/>

相应地，随机变量的值$x$落于区间$[a,b]$的概率为：

$$
	\begin{aligned}
		Pr\{a\leq x\leq b\}&=Pr\{x\leq b\}-Pr\{x\leq a\}\\
		&=P(b)-P(a)={\rm \int}_{a}^{b}p(z){\rm d}z
	\end{aligned}
$$
<Eq num="3"/> 

例如对于如图（1）(b)所示的累积分布函数$P(x)=1-\mathrm{e}^{-x},x\in[0,\infty)$，它对应的概率密度函数为$p(x)=P(x)^{'}=\mathrm{e}^{-x},x\in[0,\infty)$，如图（1）(a)所示。

特别地，对于$[a,b]$区间上的均匀分布，其概率密度函数为常数$ \cfrac{1}{b-a}$，它表示随机采样结果落于区间$[x,x+dx]$的概率在每个$x$处都相同，如图（2）所示。均匀分布的随机变量是整个蒙特卡洛方法的基础，在计算机模拟中，通常都是由系统提供的${\rm random}()$函数生成某个区间内的均匀分布，然后使用后面讲述的方法将均匀分布的随机变量转换为具有任意概率密度分布的随机变量。

<div>
    <div align="center" id="f:mc-uniform-cdf">
        <img src="/img/figures/mc/uniform-cdf.svg" width="600" />
    </div>
    <p align="left"><b>图(2)：</b>均匀分布是最基础的随机变量，它的概率密度函数$p(x)$是一个常数</p>
</div>



### 期望与方差
随机变量的概率密度函数和累积分布函数能够完整地描述一个随机变量的特征，但单个随机变量具有随机性，它对于实际的数学分析并没有什么意义，我们对多个随机变量采样的统计结果更感兴趣，本节介绍对随机函数进行多次采样结果（而不是单个随机变量）的一些数字特征，例如期望，方差及相关系数。

对于离散随机变量$X$，假设其值$x_i$对应的采样概率为$p_i$，则该随机变量$X$的数学期望（expected value），又称为均值（mean），为：

$$
	E[X]=\sum_{i=1}^{n}p_i x_i
$$
<Eq num="4" id="eq:mc-expected-value"/> 

期望代表的是对一个随机变量$X$进行采样的平均结果。例如对于骰子的例子，它的数学期望为：

$$
	\begin{aligned}
		E[X_{\rm die}]&=\sum_{i=1}^{6}p_i x_i\\
		&=\sum_{i=1}^{6} \cfrac{1}{6}x_i = \cfrac{1}{6}(1+2+3+4+5+6)\\
		&=3.5
	\end{aligned}
$$
<Eq num="5"/>

对应地，对于连续随机变量$x$，其期望为随机变量值$x$与其概率密度函数$p(x)$的乘积在全定义域上的积分（如果该积分绝对收敛）：

$$\label{eq:mc-continuous-e}
	E[X]={\rm \int}_{-\infty}^{+\infty}xp(x){\rm d}x
$$
<Eq num="6"/>

上述的关于随机变量的期望的定义在概念上很好理解，但是通常我们对随机变量的函数更感兴趣，考虑随机变量$Y=g(X)$，并且只知道随机变量$X$的概率分布，怎样求出随机变量$Y$的期望呢？

随机变量函数的数学期望可以通过下面的定理来求，即无意识的统计规律
（law of the unconscious statistician）: 设$Y$是随机变量$X$的函数：$Y=g(X)$，这里$g$是连续函数，如果$X$是离散型随机变量，它的概率分布为$P\{X=x_i\}=p_i,i=1,2,\cdots$，若$\sum^{\infty}_{i=1}g(x_i)p_i$绝对收敛， 则有：

$$
	E[Y]=E[g(X)]=\sum^{\infty}_{i=1}g(x_i)p_i
$$
<Eq num="7"/>

如果$X$是连续型随机变量，它的概率密度为$p(x)$，若${\rm \int}^{\infty}_{-\infty}g(x)p(x){\rm d}x$绝对收敛，则有：

$$
	E[Y]=E[g(X)]={\rm \int}^{\infty}_{-\infty}g(x)p(x){\rm d}x
$$
<Eq num="8"/>

该定理的重要意义在于，当求$E[Y]$时，我们不必算出$Y$的分布律或概率密度，而只需要利用$X$的分布律或概率密度就可以了。

除了均值，我们需要知道这些随机变量的采样结果相对其期望的偏离程度，这可以用每个随机变量与期望值差的期望的绝对值来表示，即：$|E[x-E[X]]|$，由于涉及绝对值不便于计算，所以使用该期望的平方来表征该量，即方差（variance）
$\sigma^2$, 表示为$V\{X\}$，方差的平方根$\sigma$称为标准差（standard deviation）。对于离散随机变量，其方差为：

$$
	\sigma^2=E[(x-E[X])^2]=\sum_i (x_i-E[x])^2p_i
$$
<Eq num="9"/>

\noindent 对于连续随机变量，其方差为：

$$\label{}
	\sigma^2=E[(x-E[x])^2]={\rm \int} (x-E[x])^2 p(x){\rm d}x
$$
<Eq num="10" id="e:discrete-variance"/>

方差具有以下性质：
1. 若$C$是常数，则：$V\{C\}=0$
2. 若$C$是常数，$X$为随机变量，则：$V\{CX\}=C^2V\{X\}$
3. 若$X$和$Y$是两个独立的随机变量，则：$V\{X+Y\}=V\{X\}+V\{Y\}$



### 大数定律
在统计学中，很多问题涉及对大量独立的随机变量采样$x_i$的和进行处理，这些随机变量拥有相同的概率密度函数$p$，这样的随机变量称为独立同分布（independent identically distributed，IID）的随机变量，例如在实验条件保持不变的情况下，一系列抛硬币的正反面结果就是独立同分布的。当这些随机变量采样的和被除以这些随机变量采样的数量$N$时，我们得到该随机变量的期望的一个估计（estimator），即：

$$
	E[X]\approx\overline{X}=  \cfrac{1}{N}\sum_{i=1}^{N}x_i
$$
<Eq num="11"/>

:::tip[估计]
	所谓估计的概念，可以理解为是对应数学模型的一种具体的（往往是近似的）求解方法，比如在这里随机变量的数学期望模型为$E[X]=\sum^{n}_{i=1}p_ix_i$（对于离散随机变量），或者$E[X]=\int xp(x){\rm d}x$（对于连续随机变量），上述的随机变量的期望应该怎么求解呢？我们可以对该随机变量重复$N$次采样，这形成一些独立同分布的随机数，然后通过对这些随机数进行统计计数来近似上述的期望模型，即使用估计$\overline{X}=  \cfrac{1}{N}\sum_{i=1}^{N}x_i$来近似$E[X]$。
:::

随着随机采样数量$N$的增大，该估计的方差逐渐减小。我们希望$N$值足够大，以至于该估计的值能够充分接近期望的值，这样我们能够将统计方法用于解决确定性问题。大数定律（law of large numbers）告诉我们，当$N\rightarrow\infty$时，我们可以确定随机变量的统计平均值趋近于期望的值，即：

$$
	P\Bigg\{ E[X]=\lim_{N \to \infty} \cfrac{1}{N}\sum_{i=1}^{N}x_i \Bigg\}=1
$$
<Eq num="12" id="eq:mc-large-numbers"/> 

大数定律告诉我们，随机变量的期望描述的加和（如式（4））或积分（如式（6））计算，可以通过对随机变量执行大量的重复采样，这得到一些独立同分布的随机数，然后使用这些采样结果的统计平均来近似。

大数定律是蒙特卡洛方法的重要基础，关于大数定律的证明过程可以参见切比雪夫不等式以及中心极限定理，这里不再对其进行详述，我们只需要理解通过对某个分布函数执行大量重复采样来近似随机数期望这种思路即可。