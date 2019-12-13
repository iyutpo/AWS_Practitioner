# Section 6. Simple Storage Service \(S3\)

### 1.1. Definition of S3

S3 is an online, bulk storage service that you can access from almost any device.

AWS Definition: AWS S3 has a simple web services interface that you can use to store and retrieve any amount of data, at any time, from anywhere on the web. It gives any user access to the same highly scalable, reliable, fast, inexpensive data storage infrastructure that Amazon uses to run its own global network of web sites. The service aims to maximize benefits of scale and to pass those benefits on to users.

![](../.gitbook/assets/image%20%28369%29.png)

### 1.2. S3 Basics

#### 1.2.1. .Components and Structure

**Basics:** 

1. S3是AWS主要的存储服务
2. 任何形式的文件都可以存放到S3中

**Buckets:**

1. 用户能够创建的根层“文件夹”（Folder）就是“**Bucket**”
2. 任何用户在Bucket中创建的子文件夹都叫做“**Folder**”

**Objects:**

1. 被存入Bucket中的文件都是**Objects**。

**Regions:**

1. 当你创建bucket时，**必须选择bucket将被存入的Region**（如North Virginia）。也就是说，**任何被上传到S3 Bucket的数据，都会被存储到某个Region的data center**。
2. 推荐的存储方式是，选择离你较近的Region，从而减少数据传输所用的时间
3. 如果你要为世界上某个区域的顾客提供服务，那你可以在离他们最近的Region创建S3 Bucket，同样也是为了减低数据传输时间

![](../.gitbook/assets/image%20%28214%29.png)

注意，AWS的一些服务只能允许  在同一个Region内的设备  相互交流

### 1.3. 操作

#### 1.3.1. 创建一个S3 Bucket：

Enter Amazon S3 --&gt; Click "Create bucket":

![](../.gitbook/assets/image%20%28254%29.png)

Type "projectyinghai" as your Bucket name \(Bucket name only contains lower case letters\) --&gt; Click "Next" --&gt; Click "Next":

![](../.gitbook/assets/image%20%28312%29.png)

![](../.gitbook/assets/image%20%28239%29.png)

默认上，你创建的Bucket是屏蔽所有public access的，需要你指定能够进行访问的public access，这里我们先不指定,  Click "Next" --&gt; Click "Create bucket":

![](../.gitbook/assets/image%20%289%29.png)

![](../.gitbook/assets/image%20%28248%29.png)

#### 1.3.2.

Click "projectyinghai" and enter S3 Bucket:

![](../.gitbook/assets/image%20%28140%29.png)

#### 1.3.3.

然后你会看到"Create Folder"按钮。这个是用来创建subfolder的。我们创建一个：Click "Create Folder" --&gt; Type "Projectyinghai" as Folder name --&gt; Click "Save":

![](../.gitbook/assets/image%20%28125%29.png)

![](../.gitbook/assets/image%20%2894%29.png)

#### 1.3.4. Upload files to your folder

Click "Projectyinghai" to enter this folder --&gt; Click "Upload" --&gt; Click "Add files" --&gt; Select any file you want to upload --&gt;

![](../.gitbook/assets/image%20%28129%29.png)

![](../.gitbook/assets/image%20%28318%29.png)

![](../.gitbook/assets/image%20%2834%29.png)

![](../.gitbook/assets/image%20%2812%29.png)

![](../.gitbook/assets/image%20%28108%29.png)

然后用同样的方式在Bucket（Root Folder）中upload一个文件：Click "projectyinghai" --&gt; Click "Upload" --&gt; Click "Add files" --&gt; Select a file you want to upload --&gt; Click "Upload":

![](../.gitbook/assets/image%20%2820%29.png)

![](../.gitbook/assets/image%20%28289%29.png)

![](../.gitbook/assets/image%20%28316%29.png)

![](../.gitbook/assets/image%20%28307%29.png)

### 1.4. Review

现在我们创建了一个Bucket。在Bucket下创建了一个Folder，上传了一个文件。在创建的Folder下，上传了一个文件：

![](../.gitbook/assets/image%20%28131%29.png)

### 1.5. Cost and Pricing

![](../.gitbook/assets/image%20%28274%29.png)

AWS提供5GB的S3 免费存储空间：

![](../.gitbook/assets/image%20%28114%29.png)

且不同地区的S3的价格也有所不同。

## 2. S3 Buckets and Objects

### 2.1. Creating an S3 Bucket:

![](../.gitbook/assets/image%20%28309%29.png)

![](../.gitbook/assets/image%20%28279%29.png)

## 3. Storage Classes

### 3.1. Definition of Storage Classes

**A Storage Class represents the classification assigned to each object in S3**. Available storage classes include:

1. Standard
2. Intelligent-Tiering
3. Standard Infrequent Access
4. One Zone-Infrequent Access \(One Zone-IA\)
5. Glacier
6. Glacier Deep Archive
7. Reduced Redundancy \(not recommended\)

Each storage class has varying attributes that dictate things like:

1. Storage cost
2. Object Availability
3. Object durability
4. Frequency of access \(to the object\)

Each object must be assigned a storage class \(Standard is the default class\)

You can change the storage class of an object at any time for the most part.

![](../.gitbook/assets/image%20%28276%29.png)

### 3.2. 操作

#### 3.2.1. 

Check the file you uploaded --&gt; In the popup window, Click "Storage class":

![](../.gitbook/assets/image%20%2876%29.png)

Then you can change any other storage class in the new popup window:

![](../.gitbook/assets/image%20%28396%29.png)

### 3.3. S3 Storage Classes:

Standard:

1. 是通用型存储类型，面向所有使用目的
2. 是默认的存储类型
3. 有99.9999999999%的耐用性
4. 99.99%的object availability
5. 是最贵的storage class

Intelligent-Tiering:

1. 使用变化的或未知的规律来设计Object。S3监视器能访问这些Object的设计规律，且能移动那些未被Infrequent Access Tier访问过的Object
2. 有99.9999999999%的耐用性
3. 99.90%的object availability
4. 比Standard便宜点

Standard-Infrequent Access \(S3 Standard-IA\)

1. 是为那些  不经常被访问的Object设计的，且这些Object被访问后需要被立即删除
2. 有99.9999999999%的耐用性
3. 99.90%的object availability
4. 比Standard便宜点

One Zone-Infrequent Access \(S3 One Zone-IA\)

1. 是为那些不是很重要的、重复的Object而设计
2. 有99.9999999999%的耐用性
3. 99.5%的object availability
4. 比Standard便宜，且S3 Standard-IA的Storage Class也能访问该类型

Glacier

1. 是为了长期存储而设计
2. 从该Storage Class中提取Object时，可能要几小时
3. 有99.9999999999%的耐用性
4. 花费很低

Glacier Deep Archive:

1. 为了长期存储Object而设计
2. 从该Storage Class中提取Object时，可能要几小时
3. 有99.9999999999%的耐用性
4. 花费最低

![](../.gitbook/assets/image%20%28296%29.png)

### 3.4. What is Object Durability and Availability?

**Object Durability is the percent \(%\) over a one-year time period that a file stored in S3 will not be lost**.

For object durability of 99.9999999999%\(11 nines\), that means that only 0.0000000001% chance of a file in S3 will be lost in a year.

**Object Availability is the percent \(%\) over a one-year time period that a file stored in S3 will be accessible**.

With an object availability of 99.99%, there's a 0.01% chance you won't be able to access a file stored in S3 in a year.

### 3.5. Setting/Changing Storage Class:

![Select Storage Class During Upload Object](../.gitbook/assets/image%20%2865%29.png)

1. 默认上，所有被上传到S3的Object都是Standard的storage class
2. 如果你想将文件（Object）设置为其他类型（storage class），那你要在上传该文件之前对该文件的storage class进行设置。有两种方式：
   1. 一种是在上传过程中，选择storage class（见上图）
   2. 另一种是使用**Object Lifecycle Policies**（之后会讲到）
3. 对于下面的几个storage class：

   1. Standard
   2. Intelligent-Tiering
   3. Standard-Infrequent Access \(S3 Standard-IA\)
   4. One Zone-Infrequent Access \(S3 One Zone-IA\)

   你可以在“Object Properties”下面，随时手动更换Object的storage class（另一个操作方法是：**Check the file you want to change --&gt; Click "Actions" --&gt; Click "Change storage class"**）

4. 如果想将Object变成Glacier或Glacier Deep Archive的storage class：
   1. 你需要使用Object Lifecycle
   2. 如果要变成Glacier类型，可能要花上一两天

![](../.gitbook/assets/image%20%28292%29.png)

## 4. Object Lifecycles

### 4.1. Object Lifecycle Definition

**An object lifecycle is a set of rules that automate the migration of an object's storage class to a different storage class, or its deletion, based on specified time intervals**.



![](../.gitbook/assets/image%20%28153%29.png)























