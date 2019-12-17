# Section 12. Route 53

## 1. Route 53 Basics

### 1.1. Route 53 Definition

**Route 53 is where you can configure and manage web domains for websites or application you host on AWS**.

AWS Definition: Amazon Route 53 performs 3 main functions:

1. **Domain registration:** Amazon Route 53 lets you register domain names such as example.com
2. **Domain Name System \(DNS\) service**: Amazon Route 53 translates friendly domain names like www.example.com into IP address like 192.0.2.1. Amazon Route 53 responds to DNS queries using a global network of authoritative DNS servers, which reduces latency.
3. Health checking: Amazon Route 53 sends automated requests over the Internet to your applications, to verify that it's reachable, and functional.

你可以使用上述功能中的任意几个。例如，你可以用Route 53注册DNS，或者用Route 53作为你已注册的域名的DNS服务。

![](../.gitbook/assets/image%20%28222%29.png)

我们来看一下domain和DNS是如何相互匹配，从而让用户能访问网站的：

#### 1.1.1. 假设一个用户想要访问linuxacademy.com

![](../.gitbook/assets/image%20%28713%29.png)

#### 1.1.2. 将linuxacademy.com这个网址输入浏览器之后，电脑就知道，用户想要访问这个网站。但是，电脑并不知道linuxacademy.com这个网址的host server在哪，所以电脑就需要IP address

![](../.gitbook/assets/image%20%2812%29.png)

#### 1.1.3. 此时，如果用户将linuxacademy.com输入到浏览器，那让然无法访问。这就像是你的朋友给你寄了一封信，他知道你的名字，但不知道你的住址，那么这封信就送不到你手上。

![](../.gitbook/assets/image%20%28661%29.png)

#### 1.1.4. 那么怎么知道linuxacademy.com的IP address呢？这时就需要DNS server了。DNS server就像是一个电话簿，当你想给某个人打电话，但你只知道这个人的名字，你通过查电话簿就能知道他的电话了。DNS server内就是一个database，里面存放着网站域名 \(Website domain, e.g. linuxacademy.com\)和它们相对应的IP address \(e.g. 192.0.2.1\)，这样一来，浏览器就可以将website domain \(linuxacademy.com\)发给DNS server，然后DNS server将查找到的IP address连同website domain一并送往Internet。这样就完成了一次用户对linuxacademy.com的访问。

![](../.gitbook/assets/image%20%28339%29.png)

### 1.2. Diagram

想必你对Route 53和DNS server有了一定的了解了。我们看下图：

1. Route 53注册了linuxacademy.com网址，并将该网址在DNS server中注册了一个IP address
2. 然后customers在浏览器输入linuxacademy.com --&gt; 进入DNS server查找到该网址的IP address --&gt; DNS server给customer这个IP address
3. 从而customer就通过Internet  --&gt; 进入Route 53 --&gt; 进入Internet Gateway --&gt; 进入ELB --&gt; .........

![](../.gitbook/assets/image%20%28370%29.png)

### 1.3. Pricing/Cost of Route 53

Route 53不提供免费服务。收费方式如下：

1. 根据host zone的数量
2. 根据network traffic flow
3. 根据standard queries的数量
4. 根据latency
5. 根据Geo DNS访问请求
6. 根据Health check的数量
7. 根据Register/transfer domain的数量

![](../.gitbook/assets/image%20%28572%29.png)

## 2. Using Route 53

### 2.1. Registering a Domain:

![](../.gitbook/assets/image%20%28501%29.png)

#### 2.1.1.

Type and search "Route 53" in AWS navigation bar --&gt; Select "Domain registration" --&gt; Click "Register domain":

![](../.gitbook/assets/image%20%28283%29.png)

![](../.gitbook/assets/image%20%28235%29.png)

Type "projectyinghai" as my "Domain name" --&gt; Click "Check" --&gt; Click "Add to cart" --&gt; Click "Continue":

![](../.gitbook/assets/image%20%2821%29.png)

![](../.gitbook/assets/image%20%28182%29.png)

Then you should input your personal information for this domain --&gt; Click "Continue" if you finished --&gt; Then you'll get an email from AWS saying that you need to verify the email address --&gt; Click the URL the email you received --&gt; After finishing verification, you'll get another email saying that you verified successfully.

![](../.gitbook/assets/image%20%28553%29.png)

![](../.gitbook/assets/image%20%28600%29.png)

![](../.gitbook/assets/image%20%28116%29.png)

Go back to your AWS register page, and Click "Refresh status" button --&gt; You'll get the page below --&gt; Check the box --&gt; Click "Complete Order" --&gt; You'll get a thank-you email from AWS:

![](../.gitbook/assets/image%20%28225%29.png)

![](../.gitbook/assets/image%20%28413%29.png)

Then Click "Go To Domains" --&gt; Wait couple minutes until your domain is registered:

![](../.gitbook/assets/image%20%28528%29.png)

![](../.gitbook/assets/image%20%28532%29.png)

Click "Hosted zones" --&gt; Click "projectyinghai" --&gt; Click "Create Record Set" --&gt; Type "www" in "Name" --&gt; Select "A - IPv4 address" as "Type" --&gt; Select "Yes" for "Alias" --&gt; Select "OmegaELB" ELB we created before --&gt; Click "Create" --&gt; Then our first Record will be created:

![](../.gitbook/assets/image%20%28585%29.png)

![](../.gitbook/assets/image%20%28142%29.png)

![](../.gitbook/assets/image%20%28605%29.png)

We then create another Record --&gt; Click "Create Record Set" --&gt; Leave "Name" blank --&gt; Select "Yes" for "Alias" --&gt; Click "Create":

![](../.gitbook/assets/image%20%2834%29.png)

![](../.gitbook/assets/image%20%28596%29.png)

Then you should wait for 1 - 5 minutes. --&gt; Open your browser and type www.projectyinghai.com --&gt; Then you'll see Apache web page in your browser:

![](../.gitbook/assets/image%20%28127%29.png)

Another way to open www.projectyinghai.com is: Go to your EC2 Dashboard --&gt; Click "Load Balancers" --&gt; Check "OmegaELB" --&gt; Copy DNS name --&gt; Open browser and paste DNS name like the second picture below shows --&gt; You'll access www.projectyinghai.com as well:

![](../.gitbook/assets/image%20%28455%29.png)

![](../.gitbook/assets/image%20%28443%29.png)

## 3. CloudFront Basics

### 3.1. Definition of CloudFront

CloudFront is an AWS service that replicates data, video, and applications around the world to reduce latency, so that access to these resources is fast for the people who will see them.

AWS Definition: Amazon CloudFront is a web service that speeds up distribution of your statics and dynamic web content, such as .html, .css, .js and image files, to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. 当用户 向 由CloudFront服务的 内容发起访问时，用户会被导向到 提供最低latency的 位置边缘，从而被访问的内容可以以最快的速度被该用户访问。如果这个内容已经在 位置边缘（edge location），那么CloudFront就能立刻将该内容传递给用户。反之，如果该内容不在 位置边缘（edge location），那么CloudFront会将该内容 从 源（source）进行提取，然后送往 位置边缘（edge location）。这个 源（source）可以是一个S3 Bucket。

![](../.gitbook/assets/image%20%2848%29.png)

### 3.2. How CloudFront works?

1. 将你想要分发的数据上传到S3 Bucket（为了能使CloudFront URLs能正常工作，我们通常要给Public读取权限）
2. 在CloudFront console，选择“Distribution”
3. 选择传输方式，选择Get Started
4. 在“Create Distribution”页面，“Origin Settings”下面，选择你之前创建的S3 Bucket。
5. 在“Default Cache Behavior Settings”接受默认值：
6. 在“Distribution Settings”进行相应配置
7. 选择“Create Distribution”，之后，等待“InProgress”变为“Deployed”即可
8. 如果你在CloudFront中使用了备用domain，保证备用domain也成功在Route 53中配置好

![](../.gitbook/assets/image%20%28191%29.png)

#### 3.2.1. 

Type and search "CloudFront" to enter dashboard --&gt; Click "Create Distribution" --&gt; Click "Get started" under "Web" --&gt; Select "essentialbucketyinghai.s3......" in "Origin Domain Name" --&gt; If you want to create, then Click "Create Distribution". But, we're not going to create here.

![](../.gitbook/assets/image%20%28607%29.png)

![](../.gitbook/assets/image%20%28704%29.png)

![](../.gitbook/assets/image%20%28714%29.png)

![](../.gitbook/assets/image%20%2860%29.png)

## 4. Exam

![](../.gitbook/assets/image%20%28497%29.png)

![](../.gitbook/assets/image%20%28271%29.png)

![](../.gitbook/assets/image%20%28679%29.png)

![](../.gitbook/assets/image%20%28610%29.png)

![](../.gitbook/assets/image%20%28604%29.png)

![](../.gitbook/assets/image%20%2873%29.png)

















