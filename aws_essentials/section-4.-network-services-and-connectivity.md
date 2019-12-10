# Section 4. Network Services and Connectivity

## 1. VPC Basics

#### 1.1 VPC \(Virtual Private Cloud\)

![](../.gitbook/assets/image%20%28104%29.png)

类似于Facebook用户的Homepage，我有自己的homepage，我的朋友有他们自己的homepage，每个人只有权力更改自己的homepage。

再举一个家庭网络的例子：如果你家里有网络，那么这个网络就叫做Private network。常见的家庭网络的组成有：

1. Wire: 从街道拉到家内的电线
2. Modem: 是你链接网络的”门“
3. Wire: 这个电线是链接Modem和路由器（Router）的
4. Router/Switch: 是帮助你链接到网络的设备。它能将网络信号导向到网络中的其他设备上，或者通过Modem将网络信号导向到/导回 Internet Service Provider \(ISP\)
5. Local Devices: 例如个人电脑，手机等能连接到网络的设备都是Local Devices。

![](../.gitbook/assets/image%20%28121%29.png)

所以说，如果Modem坏掉，Local Devices和Router就无法连接到ISP。但是Local Devices之间仍然可以通信，因为Router还在工作。

如果Router不工作，那么Local Devices之间失去联系，且无法连接到ISP

![](../.gitbook/assets/image%20%28155%29.png)

在Local Devices和Router之间添加了一个Firewall，Firewall的作用就是识别电脑病毒等有害信息，并将其过滤掉，使得只有安全的信息能被传输到Local Devices上。

![](../.gitbook/assets/image%20%2895%29.png)

#### 1.2 现在我们再来看一下AWS VPC的架构：

1. 首先，我们有若干个**EC2 instance**，它们就相当于上一个案例中的Local Devices（如个人电脑，手机等）。
2. 如果这些EC2 Instance想要访问某个网站，这些访问请求就会进入**Network Access Control List \(NACL\)**，它的功能就相当于一个Firewall，它能让特定的network traffic通过。
3. 一旦通过了，这些请求就进入**Route Table**（相当于上个案例的Router），从而进入**Internet Gateway**（相当于Modem），再进入**Internet** \(or Internet Service Provider, ISP\)。
4. 然后**Internet**会将访问到的信息  通过I**nternet Gateway**和**Route Table**返回给**Network Access Control List \(NACL\)**。过滤之后再传送到每个**EC2 Instance**上。

![](../.gitbook/assets/image%20%28148%29.png)

## 2. Internet Gateways \(IGW\)

IGW是软件和硬件的组合，它为private network提供了访问Internet Service Provider \(ISP\)的路径和通道。**因此，我们必须保证IGW的high availability和redundancy**。

![](../.gitbook/assets/image%20%28113%29.png)

另外，**当你创建了自己的AWS account后，一个VPC就自动生成了。VPC生成后就会有一个IGW被attach到VPC上**：

![](../.gitbook/assets/image%20%2852%29.png)

来到"Your VPCs"下面，你会发现VPC ID与Internet Gateway被Attach到的VPC的ID是一样的。

![](../.gitbook/assets/image%20%2843%29.png)

如果我们将VPC与Internet Gateway之间的连接断开，那么就无法连接到Internet Service Provider了：

![](../.gitbook/assets/image%20%2838%29.png)

![](../.gitbook/assets/image%20%2822%29.png)

注意：**一个VPC一次只能attach一个Internet Gateway（A VPC can only attach one Internet Gateway at a time）**。

#### 2.1 Create an Internet Gateway \(IGW\)

![](../.gitbook/assets/image%20%28131%29.png)

![](../.gitbook/assets/image%20%28114%29.png)

## 3. Route Tables \(RTs\)

#### 3.1 Route Table Definition:

A Route Table contains **a set of rules**, called **routes**, that are used to **determine where network traffic is directed**.

![](../.gitbook/assets/image%20%28135%29.png)

还记得AWS VPC的架构：

![](../.gitbook/assets/image%20%28148%29.png)

我们进入AWS来查看一下Route Table：Click on "Route Tables" --&gt; take a look at VPC ID --&gt; Click on "Routes" tag down below:

![](../.gitbook/assets/image%20%2833%29.png)

在"Routes"这一栏，我们有两个Routes，第一个是ip address CIDR notation for our default VPC. So when the VPC was created, it assigned this IP range to the VPC and if we take a look at the Target, the Target is "local". This indicates that if the destination IP address falls within this IP CIDR range, then the communication should be kept locally within our VPC.

第二个Route Destination是0.0.0.0/0。它意味着，if any communications that's not destinated specifically for our local subnet should be directed to this default destination, which is our internet gateway. 如果有任何通信不以当地子网为终点，那么该通信就要被定向到该默认终点，也就是172.31.0.0/16这里。那就是说，随着通信信息通过VPC，一旦它再次通过route table，route table判断  如果该信息要去往"local" \(i.e. 172.31.0.0/16\)，那就放行；如果要去往其他终点，那就会被定向到我们的Internet Gateway之外，然后回到Internet Service Provider。

思考：如果我们将Internet Gateway从VPC上detach下来会怎样？（如下图）

![](../.gitbook/assets/image%20%2893%29.png)

我们来实际操作一下：

























