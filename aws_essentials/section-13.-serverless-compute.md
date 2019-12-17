# Section 13. Serverless Compute

## 1. Lambda Basics

### 1.1. Definition of Lambda

**Lambda is serverless computing. It's the next generation of cloud computing that will replace EC2 instances \(for the most part\).**

AWS Definition: AWS Lambda is a compute service that lets you run code without provisioning or managing servers. AWS Lambda executes your code only when needed and scales automatically, from a few requests per day to thousands per second. You pay only for the compute time you consume - there is not charge when your code is not running. 使用AWS Lambda，你可以为你任何的应用或后台服务 运行代码。**AWS Lambda runs your code on a high-availability compute infrastructure and performs all of the administration of the compute resources, including server and operating system maintenance, capacity provisioning and automatic scaling, code monitoring and logging**. 你唯一要做的就是将你的代码提供到AWS上即可（目前支持Node.js,  Java, Go, C\#, Python\)

![](../.gitbook/assets/image%20%28445%29.png)

### 1.2. Diagram

还记得我们之前讲到过的AWS架构（如下图）：

![](../.gitbook/assets/image%20%28546%29.png)

这个架构实际上是比较复杂的，而我们的Lambda就相当于AWS内部的所有部分：

![](../.gitbook/assets/image%20%28399%29.png)

但是除了EC2 Instance等部分是不需要的之外，Route 53和DNS server仍然是必须的，因为我们需要这两个部分为我们访问网站进行导向。

假如我们电脑上只有一个应用，那么电脑是能正常运行该应用的，但如果应用增多，变为30个，那么这个电脑的配置就无法运行如此多的应用。此时我们很可能想要买一台更高配置的电脑。在AWS上，我们就需要购买一个更好配置的EC2 Instance。然而如果使用Lambda，Lambda就能Scale up来满足 运行30个应用所需的计算资源，从而使得我们的Code可以运行，而不需要我们对Server做任何的Management。你只需要对Lambda的使用程度进行付费。（也就是说，你不用设置Auto Scaling）

### 1.3. Pricing/Cost Overview:

Lambda提供免费的服务，以下是几种收费方式：

1. 按照Requests \(也就是运行code的量）
2. 按照运行code的时长
3. 按照从其他AWS服务/资源 所获得的数据的量

![](../.gitbook/assets/image%20%2892%29.png)

## 2. Lambda Test

### 2.1. Create and Execute a Lambda Function:

![](../.gitbook/assets/image%20%28328%29.png)

#### 2.1.1. Creating a Lambda Function:

Type and search "Lambda" in AWS navigation bar --&gt; Click "Create Function" --&gt; Select "Author from scratch" --&gt; Type "EssentialFunction" in "Function name" --&gt; Select "Python 3.7" under "Runtime" dropdown list --&gt; Click to expand "Choose or create an execution role" --&gt; Click "Create function":

![](../.gitbook/assets/image%20%28474%29.png)

![](../.gitbook/assets/image%20%28432%29.png)

![](../.gitbook/assets/image%20%28335%29.png)

You can also add a trigger and select "CloudWatch" to get notification. But we're not going to add triggers here:

![](../.gitbook/assets/image%20%28684%29.png)

#### 2.1.2. 

Click "Lambda" \(Blue word\) to go back --&gt; Click "Functions" --&gt; Click "EssentialFunction":

![](../.gitbook/assets/image%20%28428%29.png)

Then you'll be able to see a "lambda\_function.py" file down below --&gt; Click "Test" on top of the page:

![](../.gitbook/assets/image%20%28643%29.png)

Type 'Test" as "Event name" --&gt; Click "Create": 

![](../.gitbook/assets/image%20%28655%29.png)

Click "Test" again and you'll see the Execution succeeded. And you can also check the runtime of your code in "Details":

![](../.gitbook/assets/image%20%28391%29.png)

![](../.gitbook/assets/image%20%28503%29.png)

![](../.gitbook/assets/image%20%2845%29.png)







