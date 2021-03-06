- 意识
  - 模型是一系列关于数据分布的假设集合
  - 数据与模型同等重要
  - 使用一个模型之前，需要验证该模型各个模块的假设是否与数据分布一致
  
- 机器学习
  - [谷歌机器学习速成课程](https://developers.google.com/machine-learning/crash-course/?hl=zh-CN)
  - [CS229](http://cs229.stanford.edu/)
  
- 计算机视觉
  - [CS231n](http://cs231n.stanford.edu/)
  
- 深度学习
  - [Deep Learning](http://www.deeplearningbook.org/)
  
- conv
  - 假设
    - 空间平稳
    - 局部相关
  - padding
    - 常用的zero padding会带来什么问题（从假设考虑）
    - 如何解决
      - [partial conv](https://arxiv.org/abs/1811.11718)
    - valid padding和same padding区别
  - 超参
    - kernel size为何一般为奇数
    - kernel size如何设置，3一定是最优的吗
  - 增加conv表达能力
    - [attentive normalization](https://arxiv.org/abs/1908.01259)
    - conditional computation
      - [soft conditional computation](https://arxiv.org/abs/1904.04971)
    - attention
      - [channel](https://arxiv.org/abs/1709.01507)
      - [spatial](https://arxiv.org/abs/1807.06521)
  - 增大感受野
    - dilated conv
      - 会带来什么问题（从采样角度考虑）
  - [feature alignment](https://arxiv.org/abs/1703.06211)
    - kernel size、stride、padding共同影响
    - 对dense prediction任务会有较大影响
  - over-parameterized
    - [ACNet](https://arxiv.org/abs/1908.03930)
  - position awared
    - [coordconv](https://arxiv.org/abs/1807.03247)
  - [bagnet](https://arxiv.org/abs/1904.00760)
  - [cnns are biased towards texture](https://arxiv.org/abs/1811.12231)
  - [cnn vs gcn](https://zhuanlan.zhihu.com/p/147654689)

- 特征融合
  - basic
    - concat
    - add
      - sum
      - average
    - 上述三者区别
  - [FPN](https://arxiv.org/abs/1612.03144)
  - [BiFPN](https://arxiv.org/abs/1911.09070)
  - [PANet](https://arxiv.org/abs/1803.01534)

- 感受野
  - [理论感受野](https://github.com/vdumoulin/conv_arithmetic)
    - [各种模块感受野的计算](https://github.com/vdumoulin/conv_arithmetic)
      - [conv](https://fomoro.com/research/article/receptive-field-calculator)、pooling、deconv、dilated conv、residual结构等等
  - [有效感受野](https://arxiv.org/abs/1701.04128)
    - 什么会影响有效感受野大小
  - 在保证感受野不变的情况下提高特征图分辨率，可以去掉降采样的layer，增加降采样layer之后所有conv的dilation rate
    
- 激活函数
  - 永久失活
  - ReLU带来非线性的同时也丢失了信息
    - [CReLU](https://arxiv.org/abs/1603.05201)
    - [swish](https://arxiv.org/abs/1710.05941)
    
- 采样
  - [align corners](https://github.com/pytorch/pytorch/blob/master/torch/nn/modules/upsampling.py)两种情况的区别
    - [对点的定义不同](https://www.dropbox.com/s/o83efjejx1kfrsy/ICCV19_Detectron2.pdf?dl=0)
  - 降采样
    - 方式
      - pooling（max、avg）、conv、[reorg](https://github.com/pjreddie/darknet/blob/master/src/rnn_layer.c)
        - 区别与联系
        - 面对具体任务场景，如何选择使用哪种降采样方法
    - [anti alias](https://arxiv.org/abs/1904.11486)
      - 使采样过程符合采样定理
  - 升采样
    - 方式
      - 不可学习
        - nearest、bilinear、bicubic等
        - 各自异同
      - 可学习
        - deconv
          - deconv可以认为是先升采样（插0的升采样）、再接普通conv的过程
      - 各种方式的区别与联系
      - 面对具体任务场景，如何选择使用哪种升采样方法
    - 可学习一定比不可学习方法好吗
    
- normalization
  - vector normalizaion
    - softmax
    - [fast normalized](https://arxiv.org/abs/1911.09070)
  - feature normalization
    - BN、GN、LN、IN
      - 各自的假设和使用场景
      - BN与SENet区别与联系
      - BN的momentum超参有何含义
      - BN的gamma有何物理含义
    - [FRN](https://arxiv.org/abs/1911.09737)
  - loss normalization
    - [batch wise, sample wise](https://gluon-cv.mxnet.io/build/examples_detection/train_ssd_advanced.html)
    
- translation equivariance与translation invariance
  - 全卷积网络什么情况下具备[translation equivariance](https://arxiv.org/abs/1805.01217)特性
  - pooling真的能带来translation invariance吗
  
- imbalance
  - [Imbalance Problems in Object Detection: A Review](https://arxiv.org/abs/1909.00169)
  - 什么情况才算imbalance
    - 数量不同一定就有imbalance问题吗
  - [样本采样](https://mp.weixin.qq.com/s?__biz=MzAxMzc2NDAxOQ==&mid=2650376125&idx=2&sn=6ca8ae3a0a7714a18062d0d2eb182f84&chksm=8390b361b4e73a7776ef92763f6ea77962a116d04f97dcab2be1dcf63d831cb566ad24002de1&mpshare=1&scene=1&srcid=1121yInn8hMp0IYmK5wQYveS&sharer_sharetime=1574330244918&sharer_shareid=b4f4feb59d190ad2de2d18b933a2a0d5&rd2werd=1#wechat_redirect)
  - 解决方法
    - OHEM
    - Focal Loss
    - GHM
  
- 难样本
  - 什么是难样本
  - 难样本跟outlier的区别与联系
  
- 网络结构设计
  - [stem对网络前向速度的影响较大](https://arxiv.org/abs/1708.05234)
  - 计算量与前向时间不成正比
  - 网络结构本身就是先验，不同任务对应不同网络结构
    - 比如速度最快的人脸检测器和行人检测器网络结构大相径庭
      - 人脸检测器在stem部分可以快速将分辨率降下来
      - 行人检测器在stem部分快速降低分辨率mAP会急剧下降
  - [网络前向速度与硬件强相关](https://arxiv.org/abs/1812.00332)
    - 在某些硬件里，depth wise会很快，另一些则不然
    - 小kernel堆叠不一定比大kernel快
  - scalable
    - [resolution、width、depth](https://arxiv.org/abs/1905.11946)
    - [CBNet](https://arxiv.org/abs/1909.03625)
  - neck
    - FPN
    - [BiFPN](https://arxiv.org/abs/1911.09070)
    - [PAFPN](https://arxiv.org/abs/1803.01534)
    
- 网格效应
  - [deconv](https://distill.pub/2016/deconv-checkerboard/)
    - 全图都会出现
    - 插0的过程会导致空间平稳性丢失
    - 解决方法
      - kernel size是stride整数倍
      - 将deconv转换为升采样（升采样过程采取nearest或者bilinear）和conv
  - dilated conv
    - rate太大会导致局部相关性丢失
    - 高频部分会出现
    - 解决方法
      - [减少高频信息](https://arxiv.org/abs/1705.09914)
        - 去掉max pooling
        - 网络最后接dilated rate小的conv
        - 去掉最后层的residual结构，防止高频信号传播到后面
      - [改变dilated rate配置](https://arxiv.org/abs/1702.08502)
        - 例如原本是2、2、2的dilated conv变为1、2、3的dilated conv
  - 区别与联系
    - deconv和dilated conv本身很像，一个是在特征图上插0，一个是在kernel上插0
    - 广义的deconv是将特征图升采样（可以插0，可以插nearest，可以插bilinear），再接普通conv
    - 广义的dilated conv是将kernel升采样（一般插0，如果不插0，dilated conv的优势就没了），再接普通conv
    - 二者都跟采样有关，都要遵循采样定理
    - 都会因为违背conv的假设（局部相关性、空间平稳性）而出现问题
    
- 数据
  - 划分
    - train、val、test划分
    - k fold cross validation
  - 增强
    - [有哪些增强方法](https://github.com/albumentations-team/albumentations)
    - 面对具体任务，应该如何选择增强方法

- loss
  - 有哪些loss
  - 面对具体任务，应该如何选择loss
  - 分类loss能用来回归吗
  - 回归loss能用来分类吗

- optimization
  - relationship between batch size and learning rate
  - relationship between batch size and convergence rate
  - why mini-batch SGD works
  - why not second order optimization method
  - [double descent](https://arxiv.org/abs/1912.02292)

- 评价指标
    - 有哪些评价指标
    - 面对具体任务，应该如何选择评价指标
