---
### 2018-09-05 ~ 2018-09-11

###  **实验** 

**实验意图与方向**：甲状腺结节分割模型的优化

**实验来源**：
- 论文[The One Hundred Layers Tiramisu: Fully Convolutional DenseNets for Semantic Segmentation](https://arxiv.org/abs/1611.09326)（简称Tiramisu）的方法
- 基于[ERFNet: Efficient Residual Factorized ConvNet for Real-Time Semantic Segmentation](https://ieeexplore.ieee.org/document/8063438/?reload=true)（简称ERFNet）的方法改进[Tiramisu](https://arxiv.org/abs/1611.09326)；
	
- [点击这里获取Tiramisu源代码](https://github.com/HasnainRaz/FC-DenseNet-TensorFlow)

**实验基础**：

- 已有结果

| 网络        | Tiramisu   |  ERFNet |
| ---------   | :-------:  | :----:  |
| 交并比      | 83%        |   82%   |
| 模型大小    |   35.4M    |   31.5M |
| 最小运行显存|    471M    |   305M  |
|   运行时间  |    1.4s    |   1.0s  |
| cpu运行内存|    <400M   |   未测  |
| cpu运行时间|    3.65  s    |   未测  |
- 已有数据 

甲状腺结节图像，掩码各3917张

**改进概述**：
- 分割模型一般对图像下采样5次，图像缩小到原图的32倍（Tiramisu，FCN，Unet等），当下采样次数较少时，卷积核的感受野变小，导致分割效果变差；为了减少下采样次数，同时扩大感受野，在最后一次下采样后分别使用了空洞率为2,4,8,16的空洞卷积来提取特征，这时的分割效果不会变差。下采样次数变少的同时，相对应的上采样次数也变少，这样可以有效减小模型大小和模型运行时间。
- 用双线性插值带替上采样
- 卷积分解：用3×1和1×3的两个卷积核带替一个3×3的卷积核


### **结果**
![此处输入图片的描述](./picture.png)
