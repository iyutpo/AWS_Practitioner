# Section 5. Elastic Cloud Compute \(EC2\)

## 1. EC2 Basics

### 1.1. Definition of EC2

EC2 is like a computer. It provides scalable computing capacity in the AWS cloud. Using AWS EC2 eliminates your need to invest in hardware up front, so you can develop and deploy applications faster. You can use AWS EC2 to launch **as many or as few virtual servers** as you need, configure security and networking, and manage storage. AWS EC2 enables you to scale up or down to handle changes in requirements or spikes in popularity, reducing your need to forecast traffic.

我们很好理解我们需要as many virtual servers as possible，但什么时候需要as few virtual servers as we need？例子就是，一个电商平台，当购物淡季时通常不需要很多的server，这时，降低server的数量就能降低维护成本。

![](../.gitbook/assets/image%20%2862%29.png)

一个EC2就类似于一个计算机，可能有操作系统，CPU，RAM，硬盘，网卡，防火墙等

![](../.gitbook/assets/image%20%28258%29.png)

![](../.gitbook/assets/image%20%28104%29.png)

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

![](../.gitbook/assets/image%20%28261%29.png)

### 1.3. Pricing/Cost Overview

![](../.gitbook/assets/image%20%28373%29.png)

## 2. Amazon Machine Image \(AMI\):

### 2.1. Definition of AMI:

**AMI is a preconfigured package required to launch an EC2 instance that includes an operating system, software packages and other required settings**.

**AWS definition**: **An AMI provides the information required to launch an instance**, which is virtual server in the cloud. You specify an AMI when you launch an instance, and you can launch as many instances from the AMI as you need. You can also launch instances from as many different AMIs as you need.

![](../.gitbook/assets/image%20%28340%29.png)

### 2.2. Understanding AMIs:

**AMI包含：**

1. Root Volume Template. Root volume template又包含：
   1. Operating System。如果我们购买了一个Linux EC2 Instance，那么该EC2的操作系统就是Linux
   2. Application Software。如果我们购买的EC2 Instance中有Apache web server，那么其中一个application software就是Apache web server
2. Launch Permissions
3. Block Device Mapping。又包含：
   1. EBS \(hard drive mapping\)

![](../.gitbook/assets/image%20%28365%29.png)

当我们购买了一个Linux EC2 Instance之后，就会有一个与该Linux EC2 Instance相关的AMI被创建（名为"My Linux EC2 Instance \#1"）。之后我们可以用这个被创建的AMI来部署多个具有相同配置的Linux EC2 Instance：（好处就是我们不需要花很多时间安装操作系统和软件）

![](../.gitbook/assets/image%20%28175%29.png)

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

![](../.gitbook/assets/image%20%28317%29.png)

### 2.3. 创建AMI步骤：

#### 2.3.1

Enter "EC2 Dashboard" --&gt; Click "Launch Instance"，你会看到Amazon提供的AMI

![](../.gitbook/assets/image%20%28325%29.png)

![](../.gitbook/assets/image%20%2871%29.png)

例如，上面一幅图中的第二个AMI（Amazon Linux AMI 2018.03.0 \(HVM\), SSD Volume Type - ami-00eb20669e0990cb4）不仅说明了操作系统，硬件配置，而且说明了该AMI上的预装软件（Python, Java, Ruby, PostgreSQL, MySQL, etc）。

我们还可以Click "Community AMIs"：你会发现这里提供的AMI都没有预装软件，只有操作系统。它们是免费的。

![](../.gitbook/assets/image%20%28324%29.png)

我们再Click "AWS Marketplace"：就会看到正在AWS上提供software的厂商。如果我们需要自己创建AMI的话，通常需要在这里购买相关软件，并付费。购买了软件后，在"My AMIs"中就会出现已经购买的软件的列表。（我暂时没买，所以列表为空）

![](../.gitbook/assets/image%20%28400%29.png)

![](../.gitbook/assets/image%20%28165%29.png)

## 3. Instance Type

### 3.1 Definition of Instance Type:

The Instance Type is the CPU of your instance.

AWS definition: When you launch an instance, the instance type that you specify determines the hardware of the host computer used for your instance. Each instance type offers different compute, memory, and storage capabilities and are grouped in instance families based on these capabilities. Select an instance type based on the requirements of the application or software that you plan to run on your instance.

![](../.gitbook/assets/image%20%28397%29.png)

### 3.2. Instance Types Components:

![](../.gitbook/assets/image%20%28256%29.png)

#### 3.2.1.

Click "Quick Start" --&gt; Click "Select" button of "Amazon Linux AMI 2018.03.0 \(HVM\), SSD Volume Type - ami-00eb20669e0990cb4"：

![](../.gitbook/assets/image%20%28101%29.png)

进来之后你会发现有若干列：

* “Family”是描述当前Instance在哪个方面被优化过。如果你scroll down，就会发现有"Compute optimized", "Storage optimized"等。
* “Type”是“Family”的子类
* vCPU，Memory，Instance Storage很容易理解，不赘述
* EBS-Optimized Available：描述当前的Instance是否可以进行EBS优化选项
* Network Performance：网络性能。是根据数据传输速度（也就是带宽）来评价的。

![](../.gitbook/assets/image%20%28381%29.png)

（上图只是帮助你了解各种Instance Type和各个列的意义，并没有创建或启动任何Instance）

## 4. EBS \(Elastic Block Store\)

### 4.1. Definition of EBS:

EBS is a storage volume for an EC2 Instance \(You can think EBS as a hard drive\).

AWS Definition: AWS EBS provides block level storage volumes for use with EC2 Instances. **EBS volumes are highly available and reliable storage volumes that can be attached to any running instance that is in the same Availability Zone.** **EBS volumes that are attached to an EC2 Instance are exposed  as storage volumes that persist independently from the life of the instance**.

![](../.gitbook/assets/image%20%28359%29.png)

#### 4.1.1. 在我们进一步讲解EBS之前，先来看一下什么是IOPS：

**IOPS \(Input/Output Operations Per Second）is the amount of data that can be written to or retrieved from EBS per second.**

AWS IOPS definition: IOPS are unit of measure representing input/output operations per second. The operations are measured in KiB, and the underlying drive technology determines the maximum amount of data that a volume type counts as a single I/O. I/O size is capped at 256 KiB for SSD volumes and 1024 KiB for HDD volumes because SSD volumes handle small or random I/O much more efficiently than HDD volumes.

所以你用的IOPS越多，读写速度越快。

**IOPS的数量是由EBS volume的大小决定的。EBS volume越大，IOPS数量越多，读写速度越快**

![](../.gitbook/assets/image%20%28387%29.png)

### 4.2. EBS

Root vs. Additional EBS Volumes: 

1. 每个EC2 instance必须有一个根目录（root volume），root volume可以是也可以不是EBS
2. 默认地，当instance终止后，EBS root volume会被删除。但是instance终止后，你仍可以选择保有若干个EBS volume。
3. 在创建EC2 Instance的过程中，你可以将其他的EBS volume添加到当前的EC2 instance上
4. 任何其他的volume都可以随时被attach或detach，并且这些volume在EC2 Instance被终止后不会被删除：

![](../.gitbook/assets/image%20%28228%29.png)

### 4.3. 我们来操作一下：

#### 4.3.1.

Click "Next: Configure Instance Details" --&gt; Click "Add Storage" --&gt; Click "Next: Add Tags" --&gt; Click "Cancel" \(We're not going to create\)

![](../.gitbook/assets/image%20%28390%29.png)

![](../.gitbook/assets/image%20%28138%29.png)

![](../.gitbook/assets/image%20%2864%29.png)

#### 4.3.2. Create Volume

Enter "EC2 Dashboard" --&gt; Click "Volumes" --&gt; Click "Create Volume" --&gt; You'll see the second picture below \(We'll talk about **snapshot** in the following section\) --&gt; Click "Cancel"

![](../.gitbook/assets/image%20%28107%29.png)

![](../.gitbook/assets/image%20%28383%29.png)

#### 4.3.3. Additional EBS Volume和Root Volume的区别：

Additional EBS Volume可以被随时attach或detach到任意的EC2 Instance上。这就有点类似于U盘，你可以随时插入任意一台电脑（EC2 Instance）。

![](../.gitbook/assets/image%20%28111%29.png)

#### 4.3.4. Snapshot : 

1. is an image of an EBS volume that can be **stored as a backup of the volume or used to create a duplicate**. （Snapshot是用来作为EBS磁盘卷\(EBS volume\)的备份  的）
2. **Snapshot is not an active EBS volume**. You cannot attach or detach a snapshot to an EC2 instance.
3. **To restore a snapshot, you need to create a new EBS volume using the snapshot as its template**.

![](../.gitbook/assets/image%20%28240%29.png)

## 5. Security Groups

### 5.1 Definition of Security Groups:

Security Groups are very similar to NACLs. They allow or deny network traffic. However, security groups are found on the instance level \(as opposed to the subnet level\). In addition, the way allow/deny rules work are different from NACLs.

AWS definition: **A security group acts as a virtual firewall that controls the network traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance.** You add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time. The new rules are automatically applied to all instances that are associated with the security group. When we decide whether to allow traffic to reach an instance, we evaluate all the rules from all the security groups that are associated with the instance.

**Security Groups很像NACL，都是用来限制network traffic进出EC2 Instance的。但是NACL是从subnet层面对traffic进行限制，而Security Groups是从EC2 Instance层面上对traffic进行限制的。另外一点不同是，我们可以对NACL创建DENY Rules，但是不能对Security Groups创建DENY Rules**。

![](../.gitbook/assets/image%20%28374%29.png)

### 5.2. Understanding How Security Groups Work

ELB \(Elastic Load Balancer\)：作用是接受从Internet Gateway传入的信号，并在各个EC2 Instance之间，对该信号进行负载均衡（load balance）。所以ELB就决定着一个信号会被传向哪个EC2 Instance。

![](../.gitbook/assets/image%20%28183%29.png)

所以，我们通常需要保证左右两个EC2 Instance的Security Group有相同的Rule（i.e. 他们的Rule要允许/阻挡的信号是相同的）。否则，可能会出现：对于一个相同的信号，EC2 Instance 1收到了，但EC2 Instance 2没收到的现象。

对于Security Groups，默认上，所有的inbound traffic都被DENY，所有outbound traffic都被ALLOW：（见下图，中间蓝框就是EC2 Instance 1的Security Group）

![](../.gitbook/assets/image%20%28211%29.png)

### 5.3. 如何使用 \(How to use and set Security Groups\)

#### 5.3.1.

Enter "EC2 Dashboard" --&gt; Click "Security Groups" --&gt; Check Security Group named as "default" --&gt; Click "Inbound" and "Outbound" respectively. 你会发现所有inbound和outbound traffic都是ALLOW的：default security group是在你创建了EC2 Instance之后自动被创建的（如果你没有其他4个Security Group没关系，我们只看default Security Group）。

![](../.gitbook/assets/image%20%28179%29.png)

![](../.gitbook/assets/image%20%28362%29.png)

#### 5.3.2. Create a new Security Group:

Click "Create Security Group" --&gt; You'll see the second picture below \(All inbound traffic is not allowed \(denied\) by default\) --&gt; You'll also see the third picture below \(All outbound traffic is allowed by default\) 

![](../.gitbook/assets/image%20%28112%29.png)

![](../.gitbook/assets/image%20%28351%29.png)

![](../.gitbook/assets/image%20%28306%29.png)

#### 5.3.3. Add Traffic Rules for Security Group:

Click "Add Rule" --&gt; Select "HTTP" under "Type" tag.你会发现你没有权利对当前的Security Group Inbound Rule进行DENY的设置（不需要点"Create"）

![](../.gitbook/assets/image%20%2845%29.png)

如果点击"Create"按钮之后，我们的VPC结构就如下图所示：此时，右边的Subnet2中有我们默认（default）的Security Group \(SG\)，它不允许任何traffic进入EC2 Instance 2。左边的Subnet1是自定义的Security Group，允许HTTP traffic进入EC2 Instance 1。

![](../.gitbook/assets/image%20%28164%29.png)

所以上面的例子能看出，NACLs是stateless的，而Security Group是stateful的。

**Stateful是指，即使该Security Group中没有匹配的Outbound Rules，任何被允许进入Security Group的traffic都将自动被允许返回其源\(e.g. EC2 Instance, etc\)。这与NACL不同，在NACL中，如果没有创建允许该traffic的Outbound Rules，它将在NACL中被拒绝。**（Stateful means that any network traffic that is allowed to enter into a security group is automatically allowed to return its source, even if there's not a matching outbound rule in that security group. This is different from NACLs, which means that without an outbound rule created to allow that traffic , it would be denied at the NACL.）

## 6. IP Addressing

### 6.1 Definition of IP Addressing:

IP Addressing provides an EC2 Instance with **public IP address**.

Quick Example: 我们将network traffic想象成实体邮件，将IP address想象成每个收件人的家庭住址。在邮差寄送邮件的时候就需要找到你的住址。如果没有住址，邮差就无法寄送邮件

![](../.gitbook/assets/image%20%28172%29.png)

## 6.2 Public and Private IP Addresses:

我们说了，IP Addressing是为EC2 Instance创建Public IP address的。那么Public 和 Private Address的区别是什么呢？

#### 6.2.1. Private IP Address:

1. By default all EC2 instances have a private IP address.
2. Private IP Addressed allow for instances to communicate with each other, as long as they are located in the same VPC \(or broader private network\). 只要两个private IP address在同一个VPC下，他们之间就能进行信息交流

#### 6.2.2. Public IP Address:

1. EC2 Instances can be launched with or without a public IP address \(by default\), depending on VPC/subnet settings. EC2 instance无论有没有public IP address都能正常启动。
2. Public IP addresses are **required** for the instance to communicate with the Internet. 当EC2 Instance之间想通过Internet进行交流时，**必须**要有Public IP address

**另外要注意，default VPC和subnet都已经被预先配置好了，这样一来任何新建的EC2 instance都会有一个public IP address**

![](../.gitbook/assets/image%20%28342%29.png)

### 6.3. 操作

#### 6.3.1. Create a VPC

Enter "VPC Dashboard" --&gt; Click "Your VPCs" --&gt; Click "Create VPC":

![](../.gitbook/assets/image%20%28186%29.png)

Type "testvpc" in "Name tag" --&gt; Type "10.20.0.0/24" in "IPv4 VIDR block" --&gt; Click "Create":

![](../.gitbook/assets/image%20%28158%29.png)

#### 6.3.2. Create a Subnet:

Click "Subnets" --&gt; Click "Create subnet":

![](../.gitbook/assets/image%20%28270%29.png)

Type "testsubnet" in "Name tag" --&gt; Select "testvpc" in "VPC" --&gt; Type "10.20.0.0/24" in "IPv4 CIDR block" --&gt; Click "Create":

![](../.gitbook/assets/image%20%28295%29.png)

Check "testsubnet" you just created --&gt; In "description" tag below, you'll see that "Auto-assign public IPv4 address" is "No"

![](../.gitbook/assets/image%20%28267%29.png)

#### 6.3.3. Then we'll go back to EC2 and launch an EC2:

Enter "EC2 Dashboard" --&gt; Click "Launch Instances":

![](../.gitbook/assets/image%20%28384%29.png)

Select "Amazon Linux AMI 2018.03.0 \(HVM\), SSD Volume Type - ami-00eb20669e0990cb4":

![](../.gitbook/assets/image%20%2881%29.png)

Select "Next: Configure instance details":

![](../.gitbook/assets/image%20%28155%29.png)

In the following page, if you Switch "Network" to "testvpc", you'll find that "Auto-assign Public IP" is "Disable".  However, in "default" VPC, "Auto-assign Public IP" is "Enable".

![](../.gitbook/assets/image%20%28156%29.png)

![](../.gitbook/assets/image%20%2839%29.png)

### 6.4. How EC2 is connected to Internet:

![](../.gitbook/assets/image%20%2874%29.png)

所以，如果你的EC2 Instance连不上网Internet，你就要逐个检查这几个部分。

## 7. Launching and using an EC2 Instance

之前说了很多概念性的东西，这里我们来实际操作一下：

### 7.1 Launching an EC2 Instance:

Basic Steps:

1. Select an AMI
2. Select an Instance Type
3. Configure Instance Details:

   1. We're going to run a Bach script that install Apache: （下面代码中我们要运行的是第2，3行。先update，然后 install，最后确认Apache service成功启动）

   `# !/bin/bach`

   `yum update -y`

   `yum install -y httpd`

   `service httpd start`

4. Add Storage
5. Add a Tag \(give the instance a name\)
6. Configure/assign a Security Group
7. Review and launch
8. Create and download a Key Pair 

![](../.gitbook/assets/image%20%28124%29.png)

下面是Lanuch EC2 Instance的完整步骤（这里将省略文字描述）：

![](../.gitbook/assets/image%20%28334%29.png)

![](../.gitbook/assets/image%20%28415%29.png)

![](../.gitbook/assets/image%20%2879%29.png)

![](../.gitbook/assets/image%20%28319%29.png)

然后将之前给的4行Bash Script复制到下图中：

![](../.gitbook/assets/image%20%28105%29.png)

![](../.gitbook/assets/image%20%28266%29.png)

![](../.gitbook/assets/image%20%28259%29.png)

![](../.gitbook/assets/image%20%28281%29.png)

![](../.gitbook/assets/image%20%28250%29.png)

![](../.gitbook/assets/image%20%28260%29.png)

![](../.gitbook/assets/image%20%28226%29.png)

![](../.gitbook/assets/image%20%2889%29.png)

===============================  我是分界线 ===============================

{% tabs %}
{% tab title="Windows" %}
如果你的Windows上没有PuTTY，我们在新窗口中打开"Connect using PuTTY"：

![](../.gitbook/assets/image%20%28178%29.png)

然后点击PuTTY download page：

![](../.gitbook/assets/image%20%2895%29.png)

点击Download Here：

![](../.gitbook/assets/image%20%2885%29.png)

我的是64bit的Windows，所以：

![](../.gitbook/assets/image%20%2878%29.png)

然后打开下载的.msi文件并安装：

![](../.gitbook/assets/image%20%28336%29.png)

然后打开PuTTYgen：

![](../.gitbook/assets/image%20%28213%29.png)

![](../.gitbook/assets/image%20%2853%29.png)

![](../.gitbook/assets/image%20%28132%29.png)

你会在PuTTYgen中看到.pem文件的相关信息，然后Click "Save private key"： 

![](../.gitbook/assets/image%20%28225%29.png)

Click "Yes":

![](../.gitbook/assets/image%20%28339%29.png)

Select the directory you want to save. Type the file name as "essentialputty":

![](../.gitbook/assets/image%20%2855%29.png)

Close PuTTYgen. Open PuTTY:

![](../.gitbook/assets/image%20%28268%29.png)

打开PuTTY之后，我们回到AWS页面，将"Public DNS \(IPv4\)"后边的地址复制到PuTTY的"Host Name \(or IP address\)"这一栏：

![](../.gitbook/assets/image%20%28416%29.png)

![](../.gitbook/assets/image%20%28194%29.png)

然后再回到AWS界面，点击"Connect":

![](../.gitbook/assets/image%20%2870%29.png)

在弹出的窗口中，赋值复制用户名"ec2-user"，粘贴到PuTTY --&gt; Connection --&gt; Data --&gt; "Auto-login username"这一栏下：

![](../.gitbook/assets/image%20%28412%29.png)

![](../.gitbook/assets/image%20%28314%29.png)

然后在PuTTY --&gt; SSH --&gt; Auth --&gt;Click "Browse" --&gt; Select "essentialputty.ppk" file --&gt; Click "Open": \(**But, Don't Click "Open" in PuTTY!!!**\)

![](../.gitbook/assets/image%20%28417%29.png)

在 PuTTY中，Click "Session" --&gt; Type "Webserver" in "Saved Sessions" --&gt; Click "Save" --&gt; Click "Open" --&gt; In the popup window, Click "Yes". Then You will enter:

![](../.gitbook/assets/image%20%28208%29.png)

![](../.gitbook/assets/image%20%28372%29.png)

![](../.gitbook/assets/image%20%2891%29.png)

到此我们就完成了EC2在Windows上的启动。
{% endtab %}

{% tab title="Linux/Mac" %}
![](../.gitbook/assets/image%20%2888%29.png)

然后在Linux/Mac系统中， 进入Terminal：输入上图中的第一行代码`chmod 400 essentialskp.pem`

![](../.gitbook/assets/image%20%28227%29.png)

然后，将刚刚的第3行代码粘贴：

![](../.gitbook/assets/image%20%28206%29.png)

输入"Yes"并回车：

![](../.gitbook/assets/image%20%28133%29.png)

然后输入"ifconfig"并回车：你会看到我的Internet address是172.31.23.69（你的可能不同）

![](../.gitbook/assets/image%20%2868%29.png)

然后我们回到AWS页面：发现“Private IPs”也是172.31.23.69。同时我们还能看到Public IP是18.234.255.212

![](../.gitbook/assets/image%20%28100%29.png)

我们来检查一下public IP：（先复制Public IP）：

![](../.gitbook/assets/image%20%28385%29.png)

![](../.gitbook/assets/image%20%28389%29.png)

如果你出现了上图的情况（一直在加载，但没有页面），我们就需要做一些trouble-shooting：我们先回到刚刚的Terminal，输入`yum update -y`

![](../.gitbook/assets/image%20%2810%29.png)

如果你没有权限，可以执行`sudo yum update -y`：

![](../.gitbook/assets/image%20%28170%29.png)

如果是出现如下结果：

![](../.gitbook/assets/image%20%28277%29.png)

说明可能我们的NACL是有问题的，此时我们回到这里：我们发现"EssentialsNACL"这个NACL正在使用private subnet 4，而我们当时创建的EC2 Instance用的是Public Subnet 1（**见7.1的第5张图**）

![](../.gitbook/assets/image%20%2816%29.png)

然后我们进入default NACL然后Click "Edit"（因为我们发现这个NACL的Outbound Rule只允许端口1024-65535之间的TCP traffic传出EC2。所以我们要开放所有端口）：Click the default NACL --&gt; Click "Edit" --&gt; Replace "1024" with "1" --&gt; Click "Save"：

![](../.gitbook/assets/image%20%28188%29.png)

![](../.gitbook/assets/image%20%28212%29.png)

同样，我们还需要对Inbound进行修改：Click "Inbound Rules" --&gt; "Click "Edit" --&gt; Select "TCP" under "Type" column --&gt; Type "1-65535" Under "Port range" column --&gt; Click "Save": 

![](../.gitbook/assets/image%20%28134%29.png)

![](../.gitbook/assets/image%20%28139%29.png)

然后再回到Terminal：并输入"`sudo yum update -y`"：

![](../.gitbook/assets/image%20%2896%29.png)

等一下所有的package都安装完成后：输入"`sudo yum install -y httpd`"

![](../.gitbook/assets/image%20%28144%29.png)

同样，安装完成后，我们输入`service httpd start`

![](../.gitbook/assets/image%20%2831%29.png)

再回到浏览器，刷新，发现能加载Apache了：

![](../.gitbook/assets/image%20%28167%29.png)

到此我们就完成了EC2在Linux和Mac上的启动。
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/image%20%28366%29.png)





## 8. Exam

![](../.gitbook/assets/image%20%28297%29.png)

![](../.gitbook/assets/image%20%28344%29.png)

![](../.gitbook/assets/image%20%28280%29.png)

![](../.gitbook/assets/image%20%28288%29.png)

![](../.gitbook/assets/image%20%28127%29.png)

![](../.gitbook/assets/image%20%28109%29.png)







