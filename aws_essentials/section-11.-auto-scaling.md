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

![](../.gitbook/assets/image%20%28153%29.png)

### 2.2. How Auto Scaling works?

![](../.gitbook/assets/image%20%28166%29.png)

### 2.3. Auto Scaling Scenario

![](../.gitbook/assets/image%20%28541%29.png)





























