# Section 9. Management Tools

## 1. CloudWatch Basics

### 1.1. Definition of CloudWatch

CloudWatch is a service that allows you to monitor various elements of your AWS account.

AWS Definition: Amazon CloudWatch monitors your AWS resources and the applications you run on AWS in real time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications. CloudWatch alarms send notifications or automatically make changes to the resources you are monitoring based on rules that you define.

![](../.gitbook/assets/image%20%28383%29.png)

### 1.2. How CloudWatch works?

可以使用CloudWatch来监控你的AWS资源和服务情况，如EC2 CPU的使用情况，S3中的文件（Object）数量，EC2磁盘的读写情况等。

![](../.gitbook/assets/image%20%28534%29.png)

当然，CloudWatch也能帮你监控AWS账单。你可以设置一个Alarm threshold，每当账单超过该threshold，就会有Alarm：

![](../.gitbook/assets/image%20%28186%29.png)

### 1.3. Pricing/Cost of CloudWatch

CloudWatch也提供了一部分的免费服务。当出现如下几种情况的时候，会收费（不同Region的收费金额也有不同）：[https//aws.amazon.com/cloudwatch/pricing/](https://aws.amazon.com/cloudwatch/pricing/) 

1. 每创建一个Dashboard
2. 对于EC2 Instance进行详细的监控时
3. 自定义参数的CloudWatch
4. CloudWatch API请求
5. CloudWatch 日志文件（Logs）
6. CloudWatch事件  或 自定义事件

![](../.gitbook/assets/image%20%282%29.png)

## 2. CloudWatch Metrics and Alarms

### 2.1. What we will do:

![](../.gitbook/assets/image%20%28277%29.png)

### 2.2. How to use CloudWatch:

![](../.gitbook/assets/image%20%28739%29.png)

#### 2.2.1. Create a CloudWatch Dashboard

Search "CloudWatch" in AWS navigation bar --&gt; Click "Dashboards" --&gt; Click "Create dashboard" --&gt; Type "EssentialsDashBoard" in "Dashboarn name" bar --&gt; Select "Line" --&gt; Click "Configure":

![](../.gitbook/assets/image%20%28388%29.png)

![](../.gitbook/assets/image%20%28155%29.png)

![](../.gitbook/assets/image%20%28154%29.png)

You'll see some default metrics here --&gt; Click "EC2" --&gt; Click "Per-Instance Metrics" --&gt;

![](../.gitbook/assets/image%20%28295%29.png)

![](../.gitbook/assets/image%20%28242%29.png)

You can then play with this metric dashboard, but we're going to take a look at "CPUUtilization" --&gt; Click "Create Widget":

![](../.gitbook/assets/image%20%28377%29.png)

If you click "Save dashboard", that means every time you enter CloudWatch Dashboard, you'll see this CPUUtilization dashboard:

![](../.gitbook/assets/image%20%28291%29.png)

#### 2.2.2. Creating a CloudWatch Alarm:

Click "Alarms" --&gt; Click "Create Alarms" --&gt;  Click "Select metric" --&gt; Select "EC2" --&gt; Select "Per-Instance Metrics" --&gt; 

![](../.gitbook/assets/image%20%28531%29.png)

![](../.gitbook/assets/image%20%28306%29.png)

![](../.gitbook/assets/image%20%28647%29.png)

![](../.gitbook/assets/image%20%28226%29.png)

We select "CPUUtilization" again --&gt; Click "Select metric" --&gt; You'll find InstanceID

![](../.gitbook/assets/image%20%28329%29.png)

![](../.gitbook/assets/image%20%28321%29.png)

Also in this page, under "Conditions" --&gt; Click "Greater/Equal" --&gt; Type "0.2" in "Define the threshold value" --&gt; Expand "Additional configuration" and leave everything default --&gt; Click "Next":

![](../.gitbook/assets/image%20%28494%29.png)

In next page, Select "EssentialAutoScaling" in "Send a notification to..." --&gt; Click "next":

![](../.gitbook/assets/image%20%28162%29.png)

Type "EsssentialCPUUtilization" in "Define a unique name"  and "Alarm description - optional" --&gt; Click "Next":

![](../.gitbook/assets/image%20%28272%29.png)

In the next page, Click "Create Alarm":

![](../.gitbook/assets/image%20%28431%29.png)

#### 2.2.3. Check your billing:

Click "Billing" in side window --&gt; Click "Create alarm" --&gt; Click "Select metric" --&gt; 

![](../.gitbook/assets/image%20%28701%29.png)

![](../.gitbook/assets/image%20%28456%29.png)

Click "Billing" --&gt; Click "Total Estimated Charge" --&gt; Check "USD" --&gt; Click "Select metric"

![](../.gitbook/assets/image%20%288%29.png)

![](../.gitbook/assets/image%20%28210%29.png)

![](../.gitbook/assets/image%20%28429%29.png)

Then Click "Greater/Equal" --&gt; Type "10" in "Define the threshold value" --&gt; Click "next"

![](../.gitbook/assets/image%20%28505%29.png)

Type "EssentialBillingAlarm" in "Send a notification to..." bar --&gt; Click "Next":

![](../.gitbook/assets/image%20%28680%29.png)

Then Type "Essentialbillingalarm" in "Define a unique name" bar --&gt; Also copy and paste "Essentialbillingalarm" in "Alarm description - optional" --&gt; Click "Next" --&gt; Click "Create alarm":

![](../.gitbook/assets/image%20%28325%29.png)

![](../.gitbook/assets/image%20%28395%29.png)

## 3. CloudTrail - Basics

### 3.1. Overview

![](../.gitbook/assets/image%20%28317%29.png)

### 3.2. Definition of CloudTrail:

Definition of CloudTrail: **is a service that allows you to track various actions taken while using your AWS account. 是用来查看你使用AWS时，一系列的历史操作的（包括AWS Management Console，命令行，SDK和API等）**

AWS definition: Amazon CloudTrail is an AWS service that helps you enable governance, compliance, operational, and risk auditing of your AWS account. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events include actions taken in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs.

![](../.gitbook/assets/image%20%28360%29.png)

### 3.3. How CloudTrail works?

如下图，例如Matt关闭了一个EC2 Instance，James对S3 Bucket的权限进行了修改并使得Public能够访问该Bucket。那么AWS CloudTrail就会生成日志文件（log files），这些log files通常是.gzip文件，AWS CloudTrail会将它们（log files）存入一个S3 Bucket中

![](../.gitbook/assets/image%20%2823%29.png)

### 3.4. Pricing/Cost of CloudTrail:

CloudTrail不提供免费的服务。然而，你可以建立一个试用的CloudTrail，在每个Region免费提供管理事件的单个副本。S3费用根据AWS的使用情况而定。

如何收费

1. Management Events：例如启动EC2 Instance或创建S3 Bucket
2. Data Events：对resource进行的资源操作，例如S3 Object层的API（如Get, Put, Delete, Lambda function等会唤起API的操作）
3. Usage Charges：如S3, SNS或加密

在使用CloudTrail之前，最好先看一下AWS当前的收费规则，以确保能负担使用费用：[https://aws.amazon.com/cloudtrail/pricing/ ](https://aws.amazon.com/cloudtrail/pricing/)

![](../.gitbook/assets/image%20%28722%29.png)

### 3.5. CloudTrail的使用

#### 3.5.1. Creating a CloudTrail:

![](../.gitbook/assets/image%20%28622%29.png)

In AWS navigation bar, type and search "CloudTrail" and enter dashboard --&gt; Click "Create trail" --&gt; Type "EssentialTrail" as "Trail name" --&gt; Type "essentialbucketyinghai" as "S3 bucket" --&gt; You can configure more settings in "Advanced", but I'm going to leave it as default --&gt; Click "Create":

![](../.gitbook/assets/image%20%28175%29.png)

![](../.gitbook/assets/image%20%28606%29.png)

![](../.gitbook/assets/image%20%28315%29.png)

Click and enter "EssentialTrail" --&gt; Click "Trash can" icon on top right --&gt; Click "Delete" to delete current "EssentialTrail" CloudTrail:

![](../.gitbook/assets/image%20%28280%29.png)

![](../.gitbook/assets/image%20%2820%29.png)

![](../.gitbook/assets/image%20%28330%29.png)

![](../.gitbook/assets/image%20%2879%29.png)

Deletion succeeded.

## 4. Exam

![](../.gitbook/assets/image%20%28174%29.png)

![](../.gitbook/assets/image%20%28703%29.png)

![](../.gitbook/assets/image%20%28198%29.png)

![](../.gitbook/assets/image%20%28293%29.png)

![](../.gitbook/assets/image%20%28537%29.png)













