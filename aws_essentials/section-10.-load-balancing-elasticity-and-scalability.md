# Section 10. Load Balancing, Elasticity, and Scalability

## 1. ELB \(Elastic Load Balancing\) Basics

### 1.1. Definition of ELB

**An ELB** **evenly distributes traffic between EC2 Instances that are associated with it.**

AWS Definition: A load balancer distributes incoming application traffic across multiple EC2 Instances in multiple Availability Zones. This increases the fault tolerance of your applications. Elastic Load Balancing detects unhealthy instances and routes traffic only to healthy instances.

**ELB的作用就是平衡各个与之相关联的EC2 Instances之间的network traffic，且能够检测宕机或不工作的EC2 Instances，将network traffic导向到能正常工作的EC2 Instances上。**

![](../.gitbook/assets/image%20%28314%29.png)

### 1.2. How ELB works?

When we set up an ELB, the address assigned to ELB is what we give to our end users so that when they try to connect to the servers \(Web or EC2 Instance\), they're actually connecting through the ELB. ELB then evenly distributes network traffic to the EC2 Instances.

当我们设置一个ELB时，分配给ELB的地址就是我们给最终用户的地址，这样当他们试图连接到服务器\(Web或EC2实例\)时，他们实际上是通过ELB连接的。然后，ELB将网络流量平均分配给EC2实例。

![](../.gitbook/assets/image%20%2894%29.png)

你可能会问NACL去哪儿了。我们可以看下一个图：

实际上ELB位于Internet Gateway和Route Table之间。由于ELB通过平衡各个EC2 Instances之间的Traffic，所以ELB利用Route Table决定了traffic的去向。Route Table控制着数据在Subnets的进出。接着，数据进入Subnet，被Security Group进一步过滤：

![](../.gitbook/assets/image%20%28164%29.png)

再来看一张图：假设现在我们有一组用户，他们想要访问我们的Website（Web server 1 and Web server 2）。那么他们的访问请求就会进入ELB，由ELB来决定各个用户的访问请求的去向。**ELB要保证分流的平均性**。

![](../.gitbook/assets/image%20%28351%29.png)

所以就有了下面这张图：

![](../.gitbook/assets/image%20%28112%29.png)

### 1.3. Pricing/Cost Overview:

ELB并没有提供免费的服务。那么ELB是怎么收费的：

1. 每小时或不足一小时，ELB在运行，就会收费
2. ELB每传输1 GB数据，就会收费

![](../.gitbook/assets/image%20%28344%29.png)

## 2. Creating an ELB \(Elastic Load Balancer\)

### 2.1. Creating an ELB:

![](../.gitbook/assets/image%20%28490%29.png)

#### 2.1.1. 

Type and search "EC2" in AWS navigation bar and enter EC2 Dashboard --&gt; Click "Load Balancers" --&gt; Click "Create Load Balancer" --&gt; Click "Create" HTTP/HTTPS Application Load Balancer:

![](../.gitbook/assets/image%20%28420%29.png)

![](../.gitbook/assets/image%20%28433%29.png)

Type "OmegaELB" in "Name" --&gt; Select default VPC in "VPC" dropdown --&gt; Select Available Zones \(I selected 2 Availability Zones\) and make sure the Availability Zones you select have "Public Subnet" --&gt; Click "Next: Configure Security Settings":

![](../.gitbook/assets/image%20%2818%29.png)

You may get this warning. But don't worry. Actually, we can get rid of this warning message by creating an HTTPS Listeners in previous step.  --&gt; Click "Next: Configure Security Groups":

![](../.gitbook/assets/image%20%28254%29.png)

Only Check "EssentialSG" --&gt; Click "Next: Configure Routing":

![](../.gitbook/assets/image%20%28435%29.png)

Type "EssentialTG" in "Name" --&gt; Expand "Advanced health check settings" to see more settings --&gt; Click "Next: Register Targets":

![](../.gitbook/assets/image%20%28450%29.png)

接着就能看到Environment中含有的EC2 Instances。现在我们要注册target。记住，ELB会将traffic送往targets（也就是EC2 Instances）。所以EC2 Instance就是target group的一部分。还记得我们创建了一个叫"EssentialTG"的target group，所以现在就要讲EC2 Instances添加到"EssentialTG"的target group中。

Check EC2 Instances you want to add --&gt; Click "Add Register" --&gt; You'll EC2 Instances was added --&gt; Click "Next: Review" --&gt; Click "Create":

![](../.gitbook/assets/image%20%28288%29.png)

![](../.gitbook/assets/image%20%28205%29.png)

So we finished:

![](../.gitbook/assets/image%20%28227%29.png)

## 3. Exam

![](../.gitbook/assets/image%20%2877%29.png)

![](../.gitbook/assets/image%20%283%29.png)

![](../.gitbook/assets/image%20%28363%29.png)

![](../.gitbook/assets/image%20%28426%29.png)

![](../.gitbook/assets/image%20%28618%29.png)

![](../.gitbook/assets/image%20%28113%29.png)

![](../.gitbook/assets/image%20%28478%29.png)

![](../.gitbook/assets/image%20%28418%29.png)

![](../.gitbook/assets/image%20%28151%29.png)













