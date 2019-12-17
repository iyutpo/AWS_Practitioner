# Section 6. Simple Storage Service \(S3\)

### 1.1. Definition of S3

S3 is an online, bulk storage service that you can access from almost any device.

AWS Definition: AWS S3 has a simple web services interface that you can use to store and retrieve any amount of data, at any time, from anywhere on the web. It gives any user access to the same highly scalable, reliable, fast, inexpensive data storage infrastructure that Amazon uses to run its own global network of web sites. The service aims to maximize benefits of scale and to pass those benefits on to users.

![](../.gitbook/assets/image%20%28659%29.png)

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

![](../.gitbook/assets/image%20%28404%29.png)

注意，AWS的一些服务只能允许  在同一个Region内的设备  相互交流

### 1.3. 操作

#### 1.3.1. 创建一个S3 Bucket：

Enter Amazon S3 --&gt; Click "Create bucket":

![](../.gitbook/assets/image%20%28475%29.png)

Type "projectyinghai" as your Bucket name \(Bucket name only contains lower case letters\) --&gt; Click "Next" --&gt; Click "Next":

![](../.gitbook/assets/image%20%28561%29.png)

![](../.gitbook/assets/image%20%28451%29.png)

默认上，你创建的Bucket是屏蔽所有public access的，需要你指定能够进行访问的public access，这里我们先不指定,  Click "Next" --&gt; Click "Create bucket":

![](../.gitbook/assets/image%20%2824%29.png)

![](../.gitbook/assets/image%20%28464%29.png)

#### 1.3.2.

Click "projectyinghai" and enter S3 Bucket:

![](../.gitbook/assets/image%20%28269%29.png)

#### 1.3.3.

然后你会看到"Create Folder"按钮。这个是用来创建subfolder的。我们创建一个：Click "Create Folder" --&gt; Type "Projectyinghai" as Folder name --&gt; Click "Save":

![](../.gitbook/assets/image%20%28249%29.png)

![](../.gitbook/assets/image%20%28195%29.png)

#### 1.3.4. Upload files to your folder

Click "Projectyinghai" to enter this folder --&gt; Click "Upload" --&gt; Click "Add files" --&gt; Select any file you want to upload --&gt;

![](../.gitbook/assets/image%20%28253%29.png)

![](../.gitbook/assets/image%20%28570%29.png)

![](../.gitbook/assets/image%20%2874%29.png)

![](../.gitbook/assets/image%20%2827%29.png)

![](../.gitbook/assets/image%20%28219%29.png)

然后用同样的方式在Bucket（Root Folder）中upload一个文件：Click "projectyinghai" --&gt; Click "Upload" --&gt; Click "Add files" --&gt; Select a file you want to upload --&gt; Click "Upload":

![](../.gitbook/assets/image%20%2840%29.png)

![](../.gitbook/assets/image%20%28526%29.png)

![](../.gitbook/assets/image%20%28567%29.png)

![](../.gitbook/assets/image%20%28555%29.png)

### 1.4. Review

现在我们创建了一个Bucket。在Bucket下创建了一个Folder，上传了一个文件。在创建的Folder下，上传了一个文件：

![](../.gitbook/assets/image%20%28258%29.png)

### 1.5. Cost and Pricing

![](../.gitbook/assets/image%20%28507%29.png)

AWS提供5GB的S3 免费存储空间：

![](../.gitbook/assets/image%20%28230%29.png)

且不同地区的S3的价格也有所不同。

## 2. S3 Buckets and Objects

### 2.1. Creating an S3 Bucket:

![](../.gitbook/assets/image%20%28557%29.png)

![](../.gitbook/assets/image%20%28512%29.png)

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

![](../.gitbook/assets/image%20%28509%29.png)

### 3.2. 操作

#### 3.2.1. 

Check the file you uploaded --&gt; In the popup window, Click "Storage class":

![](../.gitbook/assets/image%20%28160%29.png)

Then you can change any other storage class in the new popup window:

![](../.gitbook/assets/image%20%28700%29.png)

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

![](../.gitbook/assets/image%20%28540%29.png)

### 3.4. What is Object Durability and Availability?

**Object Durability is the percent \(%\) over a one-year time period that a file stored in S3 will not be lost**.

For object durability of 99.9999999999%\(11 nines\), that means that only 0.0000000001% chance of a file in S3 will be lost in a year.

**Object Availability is the percent \(%\) over a one-year time period that a file stored in S3 will be accessible**.

With an object availability of 99.99%, there's a 0.01% chance you won't be able to access a file stored in S3 in a year.

### 3.5. Setting/Changing Storage Class:

![Select Storage Class During Upload Object](../.gitbook/assets/image%20%28138%29.png)

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

![](../.gitbook/assets/image%20%28530%29.png)

## 4. Object Lifecycles

### 4.1. Object Lifecycle Definition

**An object lifecycle is a set of rules that automate the migration of an object's storage class to a different storage class, or its deletion, based on specified time intervals**.

例如，如果我现在有一个文件，在将来的0-29天内，我每天都要访问这个文件。从第30天到第90天，我可能只需要每周访问该文件。从第90天开始，我可能不再访问该文件，但我并不想删除它，而是保留它，以防万一。

使用Lifecycle policy，你就能自动将文件转换为不同的storage class来满足你访问该文件（object）的需求，从而降低S3的使用费用。

![](../.gitbook/assets/image%20%28297%29.png)

### 4.2. 例子

还是上面的例子，在0-29天内，我们可以用“Standard”的class storage，因为我们每天都要使用该文件；在30-89天内，我们不常使用，所以可以用"Standard Infrequent Access"的storage class；在90天之后我们几乎不会用到它，所以可以用“Glacier”的storage class

![](../.gitbook/assets/image%20%28243%29.png)

### 4.3. Lifecycle Management:

1. Lifecycle的功能作用在Bucket（Root Folder）上
2. 然而，lifecycle policy可以用在：
   1. 整个Bucket（包括Bucket内部的所有Object）上
   2. Bucket下面的某个特定的Folder上
   3. Bucket下面的某个特定的Object上
3. 你可以随时手动删除一个lifecycle policy或将storage class更改为任意形式

![](../.gitbook/assets/image%20%28352%29.png)

#### 4.3.1. Manage Bucket Lifecycle:

Enter Bucket "projectyinghai" --&gt; Click "Management" --&gt; Click "Add lifecycle rule" --&gt; Type "EssentialLifecycle" in "Enter a rule name" tag --&gt; Click "Next" :

![](../.gitbook/assets/image%20%28579%29.png)

![](../.gitbook/assets/image%20%28471%29.png)

Then we'll need to set Lifecycle rule: Check "Current version" --&gt; Click "Add transition" --&gt; Select "Transition to Standard-IA after" --&gt; Type "30" in "Days after creation:（因为前30天是Standard-IA，所以我们设置30天）：

![](../.gitbook/assets/image%20%28580%29.png)

在30天后，我们要设置Glacier：Click "Add transition" --&gt;  Select "Transition to Glacier after" --&gt; Type "90" in "Days after creation" --&gt; Check "I acknowledge..." --&gt; Click "Next"：

![](../.gitbook/assets/image%20%28244%29.png)

Then Click "Next" and Click "Save":

![](../.gitbook/assets/image%20%28730%29.png)

![](../.gitbook/assets/image%20%28517%29.png)

![](../.gitbook/assets/image%20%28592%29.png)

## 5. Permissions

### 5.1. Definition of Permission

S3 Permissions are what allow you to have granular control over who can view, access and use specific buckets and options.

1. Permission的功能通常作用在Bucket或Object上
2. 在Bucket层上，你可以通过Permission控制：

   1. List：谁能看到Bucket的名字
   2. Upload/Delete：上传Object 或 删除已经在Bucket中的Object
   3. Permissions：添加/删除/查看 permissions

   注意，Bucket层的Permissions通常用于内部控制

3. 在Object层，你可以通过Permission控制：

   1. 打开/下载
   2. 查看 Permissions
   3. 编辑 Permissions

   注意，你可以将特定的Object通过链接的方式进行分享，分享的对象可以是世界上任何人

![](../.gitbook/assets/image%20%2846%29.png)

### 5.2. 操作

#### 5.2.1. 

Enter Bucket "projectyinghai" --&gt; Click "Permissions" --&gt; Click "Access Control List" （是用来赋予基本的“写”权限的）：

![](../.gitbook/assets/image%20%28304%29.png)

我们在之前的IAM章节添加了"Mark", "Adrian", "James"作为"Dev" Group，但是他们并没有权限访问S3 Bucket（因为S3 Bucket默认上不允许Public访问。所以现在如果我们想给"Dev" Group访问S3 Bucket的权限，我们可以将这个S3 Bucket设置为Public。但一般不推荐让所有人都有权限访问。不过如果你是在做网页，那无可厚非。



![](../.gitbook/assets/image%20%28203%29.png)

所以现在我们 回到AWS 页面，Click "Public Access" --&gt; Click "Edit" --&gt; Uncheck the box of "Block all public access" --&gt; Click "Save" --&gt; Type "confirm" in popup window to confirm --&gt; Click "Confirm":

![](../.gitbook/assets/image%20%2881%29.png)

![](../.gitbook/assets/image%20%28652%29.png)

![](../.gitbook/assets/image%20%28302%29.png)

![](../.gitbook/assets/image%20%28706%29.png)

Then Click "Permissions" --&gt; Click "Access Control List" --&gt; Select "Everyone" under "Public access" --&gt; In side window, Check "List objects" --&gt; Click "Save"：

![](../.gitbook/assets/image%20%28573%29.png)

![](../.gitbook/assets/image%20%28364%29.png)

You'll see that your S3 Bucket is now Public \(See orange sign below\):

![](../.gitbook/assets/image%20%28134%29.png)

#### 5.2.2. 为Public授予查看Object的权限

如果我们进入S3 Bucket "projectyinghai" --&gt; Click the file we uploaded --&gt; Right Click the "Object URL" and open it in a new tag --&gt; You'll see that your access was denied:

![](../.gitbook/assets/image%20%28720%29.png)

![](../.gitbook/assets/image%20%28551%29.png)

![](../.gitbook/assets/image%20%2886%29.png)

这是因为我们没有给Public授权访问：

![](../.gitbook/assets/image%20%28663%29.png)

所以我们Select "Everyone" under "Public access" --&gt; In side window, Check "Read object" --&gt; Click 'Save"：

![](../.gitbook/assets/image%20%28738%29.png)

然后我们再回到 "Overview" --&gt; Right Click "URL" and Open in new tab:  \( You'll see you file opened successfully in new tab\)

![](../.gitbook/assets/image%20%28216%29.png)

### 5.3. Sharing an S3 Object with the world:

1. 在Object上，我们可以创建如下Permission：
   1. Grantee ==&gt; 给所有人权限
   2. Check --&gt; 打开/下载的权限
2. 在"Actions"下，我们可以Select "Make Public"（下面第二图）
3. 在"Properties" 下的URL就会被激活， 从而所有人都有权限直接访问并下载它

注意，如果想要去掉Object的Public Access权限，我们可以删除相应的Permission或者直接将为Bucket提供Public Access权限的Policy删除即可

![](../.gitbook/assets/image%20%28470%29.png)

![](../.gitbook/assets/image%20%287%29.png)

![](../.gitbook/assets/image%20%2871%29.png)

## 6. Object Versioning

### 6.1. Definition of Object Versioning

**S3 Versioning is a feature that keeps track of and stores all versions of an object so that you can access and use an older version if you like**.

1. Versioning只有“开”和“关”两个状态
2. 一旦打开，你只能suspend（暂停）versioning。并且你无法再关闭它
3. Suspend（暂停）versioning只能阻止版本的增长，但所有之前的版本仍会被保存在storage中
4. versioning只能在Bucket层上设置，并且应用到该Bucket下面的所有Object上。

![](../.gitbook/assets/image%20%28731%29.png)

### 6.2. 操作

Click and enter your Root Folder "projectyinghai" --&gt; Click "Properties" --&gt; Click "Versioning" --&gt; Click "Enable versioning" --&gt; Click "save" --&gt; You'll see versioning is enabled:

![](../.gitbook/assets/image%20%28386%29.png)

![](../.gitbook/assets/image%20%28442%29.png)

Click the file you uploaded --&gt; Click "Latest version" --&gt; You'll find all previous versions and the time when you uploaded this Object:

![](../.gitbook/assets/image%20%28320%29.png)

Then, we go back to "projectyinghai" --&gt; Upload this .jpg file again \(details omitted\) --&gt; Then Click the file you uploaded --&gt; Click "Latest version" --&gt; You'll find two versions here：

![](../.gitbook/assets/image%20%28119%29.png)

另外一点要注意的是，如果进入"Projectyinghai"这个子文件夹下，打开这个图片文件，点击"Latest version" 你会发现，即使是在不同地址的相同的两个文件，也会有不同的versioning：

![](../.gitbook/assets/image%20%28340%29.png)

![](../.gitbook/assets/image%20%28109%29.png)

## 7. Exam:

![](../.gitbook/assets/image%20%2876%29.png)

![](../.gitbook/assets/image%20%28488%29.png)

![](../.gitbook/assets/image%20%2870%29.png)

![](../.gitbook/assets/image%20%28318%29.png)

![](../.gitbook/assets/image%20%28332%29.png)

![](../.gitbook/assets/image%20%28601%29.png)





















