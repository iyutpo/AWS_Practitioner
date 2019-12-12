# Section 5. Elastic Cloud Compute \(EC2\)

## 1. EC2 Basics

### 1.1. Definition of EC2

EC2 is like a computer. It provides scalable computing capacity in the AWS cloud. Using AWS EC2 eliminates your need to invest in hardware up front, so you can develop and deploy applications faster. You can use AWS EC2 to launch **as many or as few virtual servers** as you need, configure security and networking, and manage storage. AWS EC2 enables you to scale up or down to handle changes in requirements or spikes in popularity, reducing your need to forecast traffic.

我们很好理解我们需要as many virtual servers as possible，但什么时候需要as few virtual servers as we need？例子就是，一个电商平台，当购物淡季时通常不需要很多的server，这时，降低server的数量就能降低维护成本。

![](../.gitbook/assets/image%20%2850%29.png)

一个EC2就类似于一个计算机，可能有操作系统，CPU，RAM，硬盘，网卡，防火墙等

![](../.gitbook/assets/image%20%28167%29.png)

![](../.gitbook/assets/image%20%2872%29.png)

### 1.2. EC2 Instance Purchasing Options:

如此方便的EC2是需要付费的。一般最常见的几种购买方式有：

1. On-Demand: On-Demand purchasing 可以让你选择任何你喜欢的EC2 Instance，并且你有权限随时监控或停止该EC2 Instance
   1. 这是最贵的购买方式
   2. 也是灵活度最高的方式
   3. 只有在你的EC2 Instance运行的时候，才需要付费
   4. 该EC2 Instance可以随时终止
2. Reserved: 这种方式下，你可以购买EC2 Instance一段时间（如1年或3年）
   1. 相比于On-demand，Reversed方式的价格会有明显的折扣
   2. 你可以选择预付、部分预付、不预付
   3. 一旦购买Reserved Instance，在一定时间段内，你拥有该EC2的使用权，且**无论你如何使用该EC2 Instance，你都要支付由该EC2所产生的所有费用**。
3. Spot：这种方式下，你需要对一个EC2进行投标（或拍卖、竞价），然后当Spot价格小于等于投标价格时，你才能支付和使用该EC2 Instance。**如Spot价格是0.5美元/小时（注意，Spot价格是实时变动的），你的竞标价格是0.51美元/小时（显然接下来的时间里，你的竞标价很可能被Spot价格超过），假设你的竞标价在上午8：00被Spot价格超过，你就不能使用这个EC2 Instance了，且上午8：00之后的EC2 Instance的费用不需要你来支付**。
   1. 这种方式一般是Amazon用来出售那些不常被使用的EC2，在EC2使用的淡季，它们的价格会很低，通常适合学生们。例如，我是一个美国东部的大三学生，我可以在凌晨3点所有人都睡着的时候进行竞价，你会发现此时的EC2 Spot价格非常低，经济上对学生来说是比较能接受的。
   2. Spot价格随着供需量进行实时变化
   3. 这种EC2是**按分钟**计价
   4. 只有在你的竞价高于Spot价格时，你才能使用该EC2
   5. 当你的竞价被Spot价格超过，你使用该EC2的权限会自动被终止

![](../.gitbook/assets/image%20%28168%29.png)

### 1.3. Pricing/Cost Overview

![](../.gitbook/assets/image%20%28236%29.png)

















































