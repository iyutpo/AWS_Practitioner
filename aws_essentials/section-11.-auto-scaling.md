# Section 11. Auto Scaling

## 1. Auto Scaling

### 1.0. Quick Review

1. **Load Balancing** **is the ability to evenly distribute traffic between our EC2 Instances to ensure that none of these EC2 instances are overloaded by the traffic that they're receiving.**
2. **Scalability is the ability to increase our EC2 Instances. We could increase them by changing the instance type and having a larger processor, more memory, more network throughput, or we could scale by adding multiple EC2 Instances to handle the workload.** 
3. But, we do we do if the traffic that we're receiving varies throughout different parts of the day or even different parts of the year? That's where Elasticity comes into play because, **with Elasticity, you're able to scale up and add additional EC2 Instances as necessary to handle the additional load, but you can also scale down, which allows you to reduce the number of EC2 Instances to match our current demand**.

## 2. Auto Scaling Basics

### 2.1. Definition of Auto Scaling:

Definition of Auto Scaling:

Auto Scaling automates the process of adding \(scaling up\) or removing \(scaling down\) EC2 instances based on traffic demand for your application.

AWS Definition: Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application. You create collections of EC2 instances, called Auto Scaling groups. You can specify the minimum number of instances in each Auto Scaling group,  and Auto Scaling ensures that your group never goes above this size. If you specify the desired capacity, either when you create the group or at any time thereafter, Auto Scaling ensures that your group has this many instances. If you specify scaling policies, then Auto Scaling can launch or terminate instances as demand on your application increases or decreases.

![](../.gitbook/assets/image%20%28176%29.png)

### 2.2. How Auto Scaling works?

![](../.gitbook/assets/image%20%28192%29.png)

### 2.3. Auto Scaling Scenario

我们看例子，假设现在有6个用户，他们想要访问我们的Web Server。我们有两个Web Server，每个只能承受3个用户的访问量

![](../.gitbook/assets/image%20%28615%29.png)

通过ELB，我们就可以将用户平均的分配给两个Web Server：

![](../.gitbook/assets/image%20%28440%29.png)

但是如果现在又有更多的用户想要访问Web Server怎么办？

![](../.gitbook/assets/image%20%28394%29.png)

这时候我们就只能添加新的EC2 Instance来满足用户的访问需求，此时，Auto Scaling就能自动添加一个新的EC2 Instance来供新用户进行访问：

![](../.gitbook/assets/image%20%28536%29.png)

当Web Server的使用高峰过去，用户数量减少，这时，Auto Scaling就会减少EC2的数量：

![](../.gitbook/assets/image%20%28634%29.png)

### 2.4. Pricing of Auto Scaling

1. Launch Configuration: 当Auto Scaling需要添加额外的服务器到Auto Scaling Group中时，被调用的EC2
2. Auto Scaling Group: 在EC2 Server自动被添加或删除时，所有用于管理EC2的Rules和Settings

![](../.gitbook/assets/image%20%28165%29.png)

Auto Scaling是免费的，但是Auto Scaling提供的资源是要收费的（任何Auto Scaling提供的EC2 instance，一旦超过了免费分配的范围，就要收费）。例如，上面我们通过Auto Scaling新增了一个EC2 instance来承载新用户。如果在使用这个EC2 Instance的过程中产生了费用，那就需要付费。**所以，Auto Scaling是免费的，但在使用Auto Scaling的过程中对于其他AWS 资源（如EC2等）的额外使用会产生费用**。

![](../.gitbook/assets/image%20%2836%29.png)

## 3. Using Auto Scaling

### 3.1. Launch Configuration

![](../.gitbook/assets/image%20%2899%29.png)

#### 3.1.1.

Enter EC2 dashboard by searching "EC2" in AWS navigation bar --&gt; Scroll down and Click "Launch Configuration" --&gt; Click "Create launch configuration" --&gt; Select "Amazon Linux AMI 2018.03.0 \(HVM\), SSD Volume Type - ami-00eb20669e0990cb4" --&gt; Click "Next: Configure details":

![](../.gitbook/assets/image%20%28630%29.png)

![](../.gitbook/assets/image%20%28185%29.png)

![](../.gitbook/assets/image%20%2887%29.png)

#### 3.1.2.

Type "EssentialLaunchConfig" as "Name" --&gt; Click to expand "Advanced Details" --&gt; Copy and Paste the code below to "User data" --&gt; In "IP Address Type", Select "Assign a public IP address to any instances" --&gt; Click "Next: Add Storage":

![](../.gitbook/assets/image%20%28285%29.png)

```text
#!/bin/bash
yum update -y
yum install -y httpd
service httpd start
```

#### 3.1.3. 

Click "Next: Configure Security Group" --&gt; Click "Select an existing security group" --&gt; Check "EssentialSG" security group --&gt; Make sure that you've allowed "All TCP" from "Port Range" 0 - 65535 --&gt; Click "Review":

![](../.gitbook/assets/image%20%28411%29.png)

![](../.gitbook/assets/image%20%28355%29.png)

Make sure everything looks all right --&gt; Click "Create launch configuration":

![](../.gitbook/assets/image%20%28322%29.png)

If you don't have a key pair, create a new one. If you've already had your key pair, select it in "Select a key pair" dropdown list --&gt; Check "I acknowledge......" box --&gt; Click "Create launch configuration":

![](../.gitbook/assets/image%20%28130%29.png)

#### 3.1.4. Create Auto Scaling group using launch configuration

If you get the page below, Click"Create an Auto Scaling group using this launch configuration":

![](../.gitbook/assets/image%20%28346%29.png)

Type "EssentialSG" in "Group name" --&gt; Select default VPC in "Network" --&gt; Select "Public Subnet 1 and 2" in "Subnet" --&gt; Check "Receive traffic from one or more load balancers" --&gt; Select "EssentialTG" in "Target Groups" --&gt; Click "Next: Configure scaling policies":

![](../.gitbook/assets/image%20%28736%29.png)

Click "Use scaling policies to adjust the capacity of this group" --&gt; Type "1" and "3" as your minimum and maximum number of EC2 instances to scale --&gt; Type "EssentialSAGSizing" as Scale Group Size "Name" --&gt; Type "80" as "Target Value" --&gt; Click "Next: Configure Notifications"  --&gt; Click "Add notification":

![](../.gitbook/assets/image%20%28457%29.png)

![](../.gitbook/assets/image%20%28674%29.png)

Select "EssentialsAutoScaling..." in "Send to a notification to:" dropdown list --&gt; Click "Next: Configure Tags" --&gt; Click "Review":

![](../.gitbook/assets/image%20%2835%29.png)

![](../.gitbook/assets/image%20%28565%29.png)

Click "Create Auto Scaling group" --&gt; If you get an "Error" shown below, just Click "Retry" --&gt; Click "Close":

![](../.gitbook/assets/image%20%28564%29.png)

![](../.gitbook/assets/image%20%2855%29.png)

![](../.gitbook/assets/image%20%2815%29.png)

Finally, you'll see you Auto Scaling in AWS console \(You'll also get emails from AWS SNS notification saying that you've created Auto Scaling\):

![](../.gitbook/assets/image%20%2850%29.png)

## 4. Exam

![](../.gitbook/assets/image%20%2885%29.png)

![](../.gitbook/assets/image%20%2843%29.png)

![](../.gitbook/assets/image%20%28635%29.png)

![](../.gitbook/assets/image%20%28486%29.png)

![](../.gitbook/assets/image%20%28705%29.png)

![](../.gitbook/assets/image%20%28569%29.png)













