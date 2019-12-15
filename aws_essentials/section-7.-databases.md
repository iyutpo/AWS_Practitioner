# Section 7. Databases

## 1. RDS \(SQL\) and DynamoDB \(NoSQL\) Basics

### 1.1. Databases

![](../.gitbook/assets/image%20%28535%29.png)

### 1.2. RDS \(Relational Database Service\)

RDS is an SQL database service that provides a wide range of SQL database options to select from.

_**SQL Options include:**_

1. Amazon Aurora
2. MySQL
3. MariaDB
4. PostgreSQL
5. Oracle \(several Oracle options are available\)
6. Microsoft SQL Server \(several Microsoft options are available\)

**AWS Definition:**

**AWS RDS is a web service that makes it easier to set up, operate, and scale a relational database in the cloud. It provides cost-efficient resizeable capacity for an industry-standard relational database and manages common database administration tasks.**

![](../.gitbook/assets/image%20%28529%29.png)

### 1.3. 操作

#### 1.3.1. Create a RDS:

Search "RDS" in AWS navigation bar --&gt; Enter RDS Dashboard --&gt; Click "Create database": 

![](../.gitbook/assets/image%20%28601%29.png)

Then you can select any SQL Engine you want:

![](../.gitbook/assets/image%20%28131%29.png)

### 1.4. DynamoDB \(NoSQL\):

但是AWS并没有提供NoSQL的Engine（没有MongoDB可用）。但是DynamoDB可以用来代替MongoDB/CassandraDB/Oracle NoSQL

AWS DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.

![](../.gitbook/assets/image%20%28555%29.png)

### 1.5. Difference between SQL and NoSQL?

* Relational database stores data and tables using columns and rows and typically you'll see SQL databases used for very structured data, for example, like a contact list. 
* But DynamoDB or NoSQL database stores related data in JSON-like name value document, and JSON stands for JavaScript object notation and JSON is an open standard format that uses human readable text and you'll see this used for nonstructured data, such as cataloguing documents.

![](../.gitbook/assets/image%20%28591%29.png)

### 1.6. RDS Pricing/Cost Overview

除了AWS Aurora之外，其他所有的RDS 都有免费的服务提供

#### 1.6.1. RDS如何收费？

1. 能使用的RDS Engine：
   1. Amazon Aurora
   2. MySQL
   3. MariaDB
   4. PostgreSQL
   5. Oracle \(several Oracle options are available\)
   6. Microsoft SQL Server \(several Microsoft options are available\)
2. RDS Instance Classes:
   1. 很像EC2 Instance的种类
3. Purchasing Terms：
   1. On Demand
   2. Reserved
4. Database Storage
5. Data Transfer in/out of RDS

![](../.gitbook/assets/image%20%28234%29.png)

#### 1.6.2. DynamoDB Pricing/Cost Overview:

DynamoDB也提供了免费的服务

有如下几种针对DynamoDB的收费方式：

1. Provisioned Throughput Capacity
2. Indexed Data Storage
3. DynamoDB Streams
4. Reserved Capacity
5. Data Transfer in/out of DynamoDB

![](../.gitbook/assets/image%20%2845%29.png)

## 2. Provisioning a RDS \(MySQL\)

### 2.1. 

一般情况下，当你创建了database后，这个database通常不能是Internet Accessible的，不能被别人看到你的数据库。所以database一般是作为Private Subnet而存在的（如下）。RDS会与一个Route Table相连，从而实现和其他Public Subnet之间的交流，但是这个Route Table不能与Internet Gateway相连。如果其他的Public Subnet想连接到Internet的话，就需要连接另外一个Route Table，这个Route Table与Internet Gateway相连。

![](../.gitbook/assets/image%20%28638%29.png)

另外如果"Dev" group想要访问RDS的话，就需要管理员"jeff"设置一个”SSH Tunneling"："Tunneling” 是能够让其他用户依次穿过Internet --&gt; Internet gateway --&gt; Route Table --&gt; NACL --&gt; Security Group --&gt; EC2 Instance --&gt; Route Table --&gt; RDS

![](../.gitbook/assets/image%20%2889%29.png)

我们将介绍几种连接RDS的方式。另外注意，**AWS Console也不能让我们直接访问RDS database，所以我们必须利用EC2 Instance和SSH Tunnel来对我们的RDS database进行访问**。要想成功访问数据库，所有这些组件都必须正常工作才行。

![](../.gitbook/assets/image%20%2854%29.png)

### 2.2. 操作

有了RDS，我们需要创建一个subnet  group，该subnet  group中包含两个private subnet。这就是将RDS database变成private subnet的方法：

![](../.gitbook/assets/image%20%28551%29.png)

#### 2.2.1.

Navigate Bar 中搜索"RDS" --&gt; Click " Subnet Groups" in side bar --&gt; Click "Create DB Subnet Group" --&gt; Type "EssentialsSubnetGroup" as "Name" as "Description" --&gt; Select default VPC as VPC --&gt; Add "us-east-1a" and "us-east-1b" as two Availability Zones --&gt; Click "Create":

![](../.gitbook/assets/image%20%28210%29.png)

![](../.gitbook/assets/image%20%28495%29.png)

![](../.gitbook/assets/image%20%2887%29.png)

#### 2.2.2. Then we'll create a RDS database:

Click "Dashboard" --&gt; Click "Create database" --&gt; Select "MySQL" --&gt; Type "essentialsdb" as your "DB instance identifier" --&gt; Set your password --&gt; Then Select "Burstable classes \(includes t classes\)" under "DB instance size":

![](../.gitbook/assets/image%20%2817%29.png)

![](../.gitbook/assets/image%20%28634%29.png)

![](../.gitbook/assets/image%20%28582%29.png)

![](../.gitbook/assets/image%20%28595%29.png)

Click to expand "Additional connectivity configuration" --&gt; Click "Create new" --&gt; Type "EssentialSG" in "New VPC security group name" --&gt; Expand "Additional configuration" --&gt; Type "essentialdb" in "Initial database":

![](../.gitbook/assets/image%20%28191%29.png)

![](../.gitbook/assets/image%20%28168%29.png)

Select "o days" as "Backup retention period" --&gt; 

![](../.gitbook/assets/image%20%28120%29.png)

Uncheck "Deletion protection" --&gt; Click "Create database": \(Your database creation may take 5 - 10 mins\)

![](../.gitbook/assets/image%20%28372%29.png)

#### 2.2.3. After Creation:

You'll see some important information in "Connectivity & security":

![](../.gitbook/assets/image%20%28257%29.png)

Click and enter "essentialdb" --&gt; In your Browser, Open AWS in a new tab and search "VPC" in navigation bar --&gt; Click "Security Group" --&gt; Check "EssentialSG" --&gt; Click "Inbound" tag --&gt;

![](../.gitbook/assets/image%20%2884%29.png)

![](../.gitbook/assets/image%20%28570%29.png)

Set Rules as picture below: --&gt; Click "Save rules":

![](../.gitbook/assets/image%20%28456%29.png)

Then, Click "Network ACLs" --&gt; Check "5 subnets" --&gt; Click "Outbound Rules" --&gt; Edit Outbound Rules as below \(You should allow all outbound traffic"：

![](../.gitbook/assets/image%20%28520%29.png)

### 2.3. Connecting to MySQL  RDS Database:

如果想要连接到RDS Database，我们还需要第三方的应用。如果没有第三方应用就无法在AWS console上连接或使用 RDS Database。

![](../.gitbook/assets/image%20%2860%29.png)

这里推荐使用的第三方应用是MySQL Workbench

你可以在这里下载：[https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/)  （Select appropriate version before download）\( I'll select "Complete" --&gt; then Click "next" --&gt; "Install" \)

![](../.gitbook/assets/image%20%28275%29.png)

In MySQL Workbench, Click "Cross" icon: 

![](../.gitbook/assets/image%20%28584%29.png)

Then we go back to AWS console and Search "EC2" in navigation bar and enter "EC2 Dashboard" --&gt; Click "Instances" --&gt; Check "Webserver" EC2 \(see picture below\) --&gt; Copy "IPv4 Public IP" --&gt; Go back to MySQL Workbench popup window, Select "Standard TCP/IP over SSH" in "Connection Method" --&gt; Paste IPv4 address to "SSH Hostname" bar --&gt; Type "ec2-user" in SSH Username"：

![](../.gitbook/assets/image%20%2841%29.png)

![](../.gitbook/assets/image%20%28112%29.png)

Then, Click on "..." button behind "SSH Key File" --&gt; Find "essentialskp.pem" and Click "Open":

![](../.gitbook/assets/image%20%2813%29.png)

![](../.gitbook/assets/image%20%2898%29.png)

Almost there. We go back to AWS RDS console --&gt; Copy "Endpoint" under "Connectivity & security" --&gt; Go back to MySQL popup window, Paste it to "MySQL Hostname":

![](../.gitbook/assets/image%20%28107%29.png)

Then replace "root" with "admin" in "Username" bar --&gt; Click "Store in Vault" to input your password in the popup window --&gt; Click "OK"：

![](../.gitbook/assets/image%20%28206%29.png)

![](../.gitbook/assets/image%20%28530%29.png)

Then, Click "Test Connection" --&gt; In the popup window below, Click "OK" --&gt; Hopefully, I'll get the second picture \(popup window below\) --&gt; Click "OK" ：

![](../.gitbook/assets/image%20%28369%29.png)

![](../.gitbook/assets/image%20%28228%29.png)

Click "OK" to close MySQL popup window --&gt; You'll see "essentialdb" in your MySQL Workbench:

![](../.gitbook/assets/image%20%28106%29.png)

![](../.gitbook/assets/image%20%28539%29.png)

Double Click "essentialdb" to open it:

![](../.gitbook/assets/image%20%28110%29.png)

### 2.4. Quick Overview

现在SSH Tunneling就设置完成，一定要保证绿线经过的部分都配置正确，才能建立MySQL与AWS RDS之间的联系。

![](../.gitbook/assets/image%20%28244%29.png)

## 3. Exam

![](../.gitbook/assets/image%20%28145%29.png)

![](../.gitbook/assets/image%20%28462%29.png)

![](../.gitbook/assets/image%20%28165%29.png)

![](../.gitbook/assets/image%20%28647%29.png)

![](../.gitbook/assets/image%20%28185%29.png)

















