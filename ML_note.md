本文机器学习的知识
## kernel LR
链接 ========> https://shomy.top/2017/03/07/kernel-lr/  

## 优化器总结  
链接 ========> https://blog.csdn.net/u010089444/article/details/76725843
### sgd
#### Batch Gradient Descent
每一轮迭代中，用整个训练集的数据计算梯度，然后更新参数。  
Θ=Θ−α⋅▽Θ​J(Θ)  
#### 优点
cost函数若为凸函数，则可以保证收敛到全局最优点，若为非凸函数，则可以收敛到局部最优点  
#### 缺点
每次计算梯度需要在整个数据集上计算一遍，批量梯度下降速度可能较慢  
训练时占用内存较大  
没办法在线新增实例运算  

#### Stochastic Gradient Descent
每一轮迭代中，用新读入的一个数据进行梯度计算和参数更新。  
Θ=Θ−α⋅▽Θ​J(Θ;x(i),y(i))  
#### 优点
有几率跳出局部最优点  
可以在线新增实例  
#### 缺点
下降速度慢，可能在沟壑处震荡  

#### Mini-batch Gradient Descent
每一轮迭代中选取数据集中的一个子集进行梯度计算和训练。  
Θ=Θ−α⋅▽Θ​J(Θ;x(i:i+n),y(i:i+n))  

梯度下降都有的缺点是学习率难以设置，且所有参数的学习率统一，在鞍点难以训练  

### Momentum
vt​=γ⋅vt−1​+α⋅▽Θ​J(Θ) 
Θ=Θ−vt​  
考虑在原有速度上加上惯性，这样若下降方向与之前一致则速度会越来越快，反之即便下降方向改变，也依然有一个在原方向上的惯性存在  
（避免方向不断改变带来的收敛速度减慢）  

### Nesterov Momentum
vt​=γ⋅vt−1​+α⋅▽Θ​J(Θ−γvt−1​)  
Θ=Θ−vt​  
在动量的基础上略作修改，更新梯度不再考虑原有的参数处，而是在新的参数点处计算，目的是展望新的参数处的下降方向。  

### Adagrad
Θt+1,i​=Θt,i​−α⋅gt,i​  
Θt+1,i​=Θt,i​−α/Gt,ii​+ϵ⋅gt,i  
Gt为一个对角矩阵，其中对角线上的元素为各参数之前迭代的梯度平方和，目的在于在之前迭代速度较快的方向走的慢一些，  
但是求和梯度会使得参数迭代速度下降很快，导致训练提前结束。  

### RMSprop
E[g2]t​=0.9E[g2]t−1​+0.1gt2​
Θt+1​=Θt​−​α​⋅/E[g2]t​+ϵ
gt​
将之前的梯度求和转为求梯度平均（这样既能保留之前的目的，同时学习率又不会大幅下降）  

### Adam
mt​=β1​mt−1​+(1−β1​)gt​  
vt​=β2​vt−1​+(1−β2​)gt2​  
m^t​=mt/(1−β1t)  
v^t​=vt/(1−β2t)  
Θt+1​=Θt​−α​/(v^t​+ϵ)m^t​  
结合了动量和RMSprop的优点，收敛速度快。

