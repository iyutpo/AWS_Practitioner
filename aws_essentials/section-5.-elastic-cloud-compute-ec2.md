# Section 5. Elastic Cloud Compute \(EC2\)

## 1. EC2 Basics

### 1.1. Definition of EC2

EC2 is like a computer. It provides scalable computing capacity in the AWS cloud. Using AWS EC2 eliminates your need to invest in hardware up front, so you can develop and deploy applications faster. You can use AWS EC2 to launch **as many or as few virtual servers** as you need, configure security and networking, and manage storage. AWS EC2 enables you to scale up or down to handle changes in requirements or spikes in popularity, reducing your need to forecast traffic.

我们很好理解我们需要as many virtual servers as possible，但什么时候需要as few virtual servers as we need？例子就是，一个电商平台，当购物淡季时通常不需要很多的server，这时，降低server的数量就能降低维护成本。

![](../.gitbook/assets/image%20%2850%29.png)

一个EC2就类似于一个计算机，可能有操作系统，CPU，RAM，硬盘，网卡，防火墙等

![](../.gitbook/assets/image%20%28172%29.png)

![](../.gitbook/assets/image%20%2874%29.png)

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

![](../.gitbook/assets/image%20%28173%29.png)

### 1.3. Pricing/Cost Overview

![](../.gitbook/assets/image%20%28246%29.png)

## 2. Amazon Machine Image \(AMI\):

### 2.1. Definition of AMI:

**AMI is a preconfigured package required to launch an EC2 instance that includes an operating system, software packages and other required settings**.

**AWS definition**: **An AMI provides the information required to launch an instance**, which is virtual server in the cloud. You specify an AMI when you launch an instance, and you can launch as many instances from the AMI as you need. You can also launch instances from as many different AMIs as you need.

![](../.gitbook/assets/image%20%28221%29.png)

### 2.2. Understanding AMIs:

**AMI包含：**

1. Root Volume Template. Root volume template又包含：
   1. Operating System。如果我们购买了一个Linux EC2 Instance，那么该EC2的操作系统就是Linux
   2. Application Software。如果我们购买的EC2 Instance中有Apache web server，那么其中一个application software就是Apache web server
2. Launch Permissions
3. Block Device Mapping。又包含：
   1. EBS \(hard drive mapping\)

![](../.gitbook/assets/image%20%28241%29.png)

当我们购买了一个Linux EC2 Instance之后，就会有一个与该Linux EC2 Instance相关的AMI被创建（名为"My Linux EC2 Instance \#1"）。之后我们可以用这个被创建的AMI来部署多个具有相同配置的Linux EC2 Instance：（好处就是我们不需要花很多时间安装操作系统和软件）

![](../.gitbook/assets/image%20%28115%29.png)

#### 2.2.1. 当启动EC2 Instance之前，我们要先选一个AMI。如何选择AMI呢？

AMI一共有三类：

1. Community AMI：
   1. 免费
   2. 使用这类AMI时，你只能选择你需要的操作系统
2. AWS Marketplace AMI：
   1. 付费
   2. 通常会有一些package和带有证书的software
3. My AMI：
   1. 这种是我们自己创建的AMI

![](../.gitbook/assets/image%20%28204%29.png)

### 2.3. 创建AMI步骤：

#### 2.3.1

Enter "EC2 Dashboard" --&gt; Click "Launch Instance"，你会看到Amazon提供的AMI

![](../.gitbook/assets/image%20%28209%29.png)

![](../.gitbook/assets/image%20%2855%29.png)

例如，上面一幅图中的第二个AMI（Amazon Linux AMI 2018.03.0 \(HVM\), SSD Volume Type - ami-00eb20669e0990cb4）不仅说明了操作系统，硬件配置，而且说明了该AMI上的预装软件（Python, Java, Ruby, PostgreSQL, MySQL, etc）。

我们还可以Click "Community AMIs"：你会发现这里提供的AMI都没有预装软件，只有操作系统。它们是免费的。

![](../.gitbook/assets/image%20%28208%29.png)

我们再Click "AWS Marketplace"：就会看到正在AWS上提供software的厂商。如果我们需要自己创建AMI的话，通常需要在这里购买相关软件，并付费。购买了软件后，在"My AMIs"中就会出现已经购买的软件的列表。（我暂时没买，所以列表为空）

![](../.gitbook/assets/image%20%28263%29.png)

![](../.gitbook/assets/image%20%28108%29.png)

## 3. Instance Type

### 3.1 Definition of Instance Type:

The Instance Type is the CPU of your instance.

AWS definition: When you launch an instance, the instance type that you specify determines the hardware of the host computer used for your instance. Each instance type offers different compute, memory, and storage capabilities and are grouped in instance families based on these capabilities. Select an instance type based on the requirements of the application or software that you plan to run on your instance.

![](../.gitbook/assets/image%20%28261%29.png)

### 3.2. Instance Types Components:

![](../.gitbook/assets/image%20%28170%29.png)

#### 3.2.1.

Click "Quick Start" --&gt; Click "Select" button of "Amazon Linux AMI 2018.03.0 \(HVM\), SSD Volume Type - ami-00eb20669e0990cb4"：

![](../.gitbook/assets/image%20%2871%29.png)

进来之后你会发现有若干列：

* “Family”是描述当前Instance在哪个方面被优化过。如果你scroll down，就会发现有"Compute optimized", "Storage optimized"等。
* “Type”是“am

![](../.gitbook/assets/image%20%28252%29.png)

























