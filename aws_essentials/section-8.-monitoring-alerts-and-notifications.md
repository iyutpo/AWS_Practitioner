# Section 8. Monitoring, Alerts, and Notifications

## 1. SNS \(Simple Notification Service\) Basics

### 1.1. Definition of Simple Notification Service \(SNS\)

An AWS service that allows you to automate the sending of email or text message notifications, based on events that happen in your AWS account.

AWS Definition:

**Simple Notification Service is a web service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients.** In Amazon SNS, there are two types of clients, publishers and subscribers, also referred to as producers and consumers. 

* Publishers communicate asynchronously with subscribers by producing and sending a message to a topic, which is logical access point and communication channel. 
* Subscribers \(i.e., web servers, email address, Amazon SQS queues, AWS Lambda functions\) consume or receive the message or notification over one of the supported protocols \(i.e., **Amazon SQS, HTTP/S, email, SMS,  Lambda**\) when they're subscribed to the topic.

![](../.gitbook/assets/image%20%2826%29.png)

**SNS使用流程（见下图）：**

假设现在最左边的EC2 Instance正常工作，我们创建了一个Amazon CloudWatch来监视第二个EC2 Instance的工作状况。如果第二个EC2 Instance宕机，那么Amazon CloudWatch就会触发 C.W. Alarm，并且通过Email（Simple Notification）等形式提醒 System Admin，等System Admin排除故障之后，EC2 Instance就能重新工作了：

![](../.gitbook/assets/image%20%28278%29.png)

### 1.2. SNS

SNS有几个部分构成：

1. Topic：也就是你如何将终端（endpoint）进行分类的
2. Subscription：是你要将信息送往的终端（endpoint）
3. Publisher：给SNS所需信息的  人/警告/事件

![](../.gitbook/assets/image%20%28407%29.png)

### 1.3. SNS是怎么收费的

1. Publishes：根据SNS请求的数量收费
2. Notification Deliveries：根据Subscriber的数量进行收费
3. Data Transfer in/out of SNS：根据进出SNS的数据量收费

![](../.gitbook/assets/image%20%28646%29.png)

![](../.gitbook/assets/image%20%28276%29.png)

### 1.4. 操作：

这是我们将要做的：

![](../.gitbook/assets/image%20%284%29.png)

#### 1.4.1. Create Topic

Type and search "SNS" in AWS navigation bar --&gt; \(If you didn't get the first picture below, you can then ignore current operation\) Click "Amazon SNS" \(Blue words\) --&gt; Enter the page shown in the second picture below --&gt; Type "EssentialTopic" in "Topic Name" --&gt; Click "Next Step":

![](../.gitbook/assets/image%20%28135%29.png)

![](../.gitbook/assets/image%20%2897%29.png)

Then do the configurations shown in following pictures：

![](../.gitbook/assets/image%20%28460%29.png)

![](../.gitbook/assets/image%20%2881%29.png)

![](../.gitbook/assets/image%20%28587%29.png)

![](../.gitbook/assets/image%20%2855%29.png)

![](../.gitbook/assets/image%20%28194%29.png)

点击"Create topic"之后，你会看到ARN（Amazon Resource Name）。ARN就是由"Topic Name" "EssentialTopic"产生的。

#### 1.4.2. Create Subscription:

Click "Subscription" --&gt; Click "Create subscription"：

![](../.gitbook/assets/image%20%28125%29.png)

Click the navigation bar under "Topic ARN" so that you can select "arn:.......:EssentialTopic" --&gt; Select "Email" as Protocol --&gt; Type your email address in "Endpoint" bar --&gt; Click "Create subscription":

![](../.gitbook/assets/image%20%28521%29.png)

If you go and check your email, you'll find an email "EssentialTopic" which is an AWS Notification:

![](../.gitbook/assets/image%20%28567%29.png)

Click "Confirm subscription" to confirm:

![](../.gitbook/assets/image%20%28427%29.png)

![](../.gitbook/assets/image%20%28170%29.png)

If you go back to AWS SNS console, you'll find "Subscription status" turned to "Confirmed":

![](../.gitbook/assets/image%20%2885%29.png)

#### 1.4.3.

Click "Topics" --&gt; Click "EssentialTopic":

![](../.gitbook/assets/image%20%2846%29.png)

Click "Publish message":

![](../.gitbook/assets/image%20%28420%29.png)

Type "Test Essential Topic" as "Subject" --&gt; Input "Test for SNS topic" in "Message body to be send to the endpoint" --&gt; Click "Publish message":  You'll get an email:

![](../.gitbook/assets/image%20%28629%29.png)

![](../.gitbook/assets/image%20%285%29.png)

![](../.gitbook/assets/image%20%28517%29.png)

#### 1.4.4. Create another New topic:

Click "Topic" --&gt; Click "Create topic":

![](../.gitbook/assets/image%20%28140%29.png)

Input "EssentialBillingAlarm" in "Name" and "Display name" bar --&gt; Click "Create topic":

![](../.gitbook/assets/image%20%28566%29.png)

![](../.gitbook/assets/image%20%28359%29.png)

#### 1.4.5. 

Click "Topics" --&gt; Click "EssentialBillingAlarm" --&gt; Click "Create subscription":

![](../.gitbook/assets/image%20%28341%29.png)

![](../.gitbook/assets/image%20%28442%29.png)

Also, Click to Select "arn:......EssentialBillingAlarm" in "Topic ARN" bar --&gt; Select "Email" as "Protocol" --&gt; Input your email address in "Endpoint" --&gt; Click "Create subscriptions":

![](../.gitbook/assets/image%20%28252%29.png)

#### 1.4.6. Create Autoscaling Topic:

Click "Topics" --&gt; Click "Create Topic":

![](../.gitbook/assets/image%20%28639%29.png)

Input "EssentialAutoScaling" as Name and "Display name" --&gt; Click "Create topic":

![](../.gitbook/assets/image%20%28245%29.png)

![](../.gitbook/assets/image%20%28277%29.png)

#### 1.4.7. Create another subscription

Click "Subscription" --&gt; Click "Create subscription":

![](../.gitbook/assets/image%20%28603%29.png)

Select "arn:......EssentialAutoScaling" as "Topic ARN" --&gt; Select "Email" as "Protocol" --&gt; Input your email address as "Endpoint" --&gt; Click "Create subscription":

![](../.gitbook/assets/image%20%28175%29.png)

Then, we go back and Click "Topics" --&gt; Click "EssentialAutoScaling" --&gt; Click "Create subscription":

![](../.gitbook/assets/image%20%286%29.png)

![](../.gitbook/assets/image%20%2874%29.png)

We select "arn:......:EssentialAutoScaling" as "Topic ARN" --&gt; Select "SMS" as "Protocol" --&gt; Input your phone number in "Endpoint" --&gt; Click "Create subscription":

![](../.gitbook/assets/image%20%28117%29.png)

#### 1.4.8. Check you email

I you go back to your email. You'll find there're two new emails, one for EssentialAutoScaling and one for EssentialBilling Alarm:

![](../.gitbook/assets/image%20%28324%29.png)

We open "EssentialBillingAlarm" email and Click the URL to confirm the subscription:

![](../.gitbook/assets/image%20%2848%29.png)

![](../.gitbook/assets/image%20%28313%29.png)

Do the same thing for EssentialAutoScaling:

![](../.gitbook/assets/image%20%28124%29.png)

![](../.gitbook/assets/image%20%28235%29.png)

You'll see all subscriptions are confirmed including the SMS one:

![](../.gitbook/assets/image%20%28204%29.png)

## 2. Exam

**默认上，每个Topic的最大SNS Subscription数量为12500000个。**

**默认上，每个账号最多有100000个SNS Notification**

![](../.gitbook/assets/image%20%2857%29.png)

![](../.gitbook/assets/image%20%2870%29.png)

![](../.gitbook/assets/image%20%28226%29.png)

![](../.gitbook/assets/image%20%28209%29.png)

![](../.gitbook/assets/image%20%28241%29.png)











