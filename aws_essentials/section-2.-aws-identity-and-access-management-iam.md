# Section 2. AWS Identity and Access Management \(IAM\)

## What is IAM?

**AWS IAM stands for Identity and Access Management. IAM is used to securely control access to AWS resources.** 

For example, we can create user accounts for people on our team and allow those users to access an AWS service or feature.

## How does IAM work?

First, we can go to Service Navigation Bar and type "IAM". I'll get:

![](../.gitbook/assets/image%20%28138%29.png)

* **An important thing to know is, when you created your AWS account, a root user account was automatically created as well. The root user account is created automatically when you sign up for AWS. Of course, by default, the root user account can access all AWS resources including billing and all services. 也就是说，root account有最高的权限并且能访问所有AWS提供的service**。
* **另外很重要的一点就是，任何新用户都被默认为不能享用任何AWS服务，因此，我们必须为新用户授权 可以享用的服务**。

You'll see 5 Security Status which is also known as "**AWS Best Practices**". It's a guideline and architecture for maintaining a high level of security, accessibility and efficiency.

1. **Delete your root access keys**: We currently don't need to do anything to our root account.
2. **Activate MFA on your root account**: 
   1. MFA, i.e. **Multi-Factor Authentication provides an additional layer of security on your root account and that security is provided by a third-party.** It provides a continually changing, random 6-digit code along with your password when you want to login your root account.
   2. Expand "Activate MFA on your root account" and click "Manage MFA". 

![](../.gitbook/assets/image%20%28193%29.png)

            3. If this pops up, click "Continue to Security Credentials":

![](../.gitbook/assets/image%20%2822%29.png)

            4. Then click "Activate MFA" button, and select "Virtual MFA device" and "Continue".

![](../.gitbook/assets/image%20%28150%29.png)

![](../.gitbook/assets/image%20%28163%29.png)

            5. Then, take out your smartphone our tablet and install an application called "Google Authenticator":

![](../.gitbook/assets/image%20%28135%29.png)

            6. In "Google Authenticator", click "Scan a barcode". Then return to your AWS "Set up virtual MFA device" page and click "show QR code". Scan it.

![](../.gitbook/assets/image%20%28145%29.png)

            7. Then, input your MFA code 1 and MFA code 2. Click "Assign MFA". Then your MFA will be assigned successfully.

![](../.gitbook/assets/image%20%2894%29.png)

![](../.gitbook/assets/image%20%28223%29.png)

            8. Back to "Dashboard" page and you'll see the second box was checked:

![](../.gitbook/assets/image%20%28157%29.png)

    3. **Create individual IAM users**:

           1. Here, you'll want to create an IAM user. Click "Access management" --&gt; Click "Users" --&gt; "Add user":

![](../.gitbook/assets/image%20%28252%29.png)

            2. Next, you can do the same configuration below or customize your own configuration. Click "Next Permissions"

![](../.gitbook/assets/image%20%28130%29.png)

            3. Then you'll be allowed to "Add new users to group" or "Copy permissions from existing user" or "Attach existing policies directly". Click "Attach existing policies directly" and you'll see "AdministratorAccess" in the window below. "AdministratorAccess" user can access all AWS services. We then check the box for "AdministratorAccess" and click on "Next Tags":

![](../.gitbook/assets/image%20%28195%29.png)

            4. I will leave it blank in "Add tags" page and click on "Next: Review"

![](../.gitbook/assets/image%20%28270%29.png)

             5. Take a look at on your information and click "Create user" if everything is good:

![](../.gitbook/assets/image%20%2823%29.png)

            6. Click "Close" if you succeed:

![](../.gitbook/assets/image%20%2828%29.png)

            7. You'll see a new user "jeff" was created. Then go back to "dashboard", you'll find the third box was checked:

![](../.gitbook/assets/image%20%28190%29.png)

![](../.gitbook/assets/image%20%2870%29.png)

    ****4. **Use groups to assign permissions**:

            1. Click on "Manage Groups" --&gt; Click on "Create New Group"

![](../.gitbook/assets/image%20%28139%29.png)

![](../.gitbook/assets/image%20%2846%29.png)

            2. Create a group named "omegaAdmins" and Click on "Next Step"

![](../.gitbook/assets/image%20%28140%29.png)

            3. Then we'll need to attach policy to "omegaAdmins" group which is similar to attaching policy to "jeff" user. Click and check "AdministratorAccess" box --&gt; Click on "Next Step" --&gt; Click on "Create Group". You'll see a new group "omegaAdmins" was created and the fourth box was also checked automatically:

![](../.gitbook/assets/image%20%28109%29.png)

![](../.gitbook/assets/image%20%289%29.png)

![](../.gitbook/assets/image%20%28226%29.png)

![](../.gitbook/assets/image%20%28247%29.png)

    5. **Apply an IAM password policy**:

            1. Go to "Manage Password Policy"

![](../.gitbook/assets/image%20%28180%29.png)

            2. Click on "Set password policy". Then Check "Prevent password reuses" --&gt; Remember 3 password\(s\) --&gt; Click on "Save Changes":

![](../.gitbook/assets/image%20%28255%29.png)

![](../.gitbook/assets/image%20%28124%29.png)

![](../.gitbook/assets/image%20%2887%29.png)

            3. Then all five boxes are checked.

![](../.gitbook/assets/image%20%28202%29.png)

## Add IAM Users and Set Policies

Since we've created our root user "jeff", now we want to add some new users and assign certain policies to each of them. For example, a new user we want to add is called "Mark" and we want "Mark" to be able to access an S3 Bucket:

![](../.gitbook/assets/image%20%28232%29.png)

As you can see, now we don't have any users except "jeff", the root user:

![](../.gitbook/assets/image%20%2812%29.png)

So, we click on "Add user" --&gt; Type "Mark" in User name bar --&gt; Select "Console password" \(we're not going to use "Programmatic access" because it's a more advanced and usually for those developers\) --&gt; Slick on "Custom password" --&gt; input your password --&gt; Uncheck the box for Require password reset" --&gt; "Next permissions":

![](../.gitbook/assets/image%20%2865%29.png)

![](../.gitbook/assets/image%20%2825%29.png)

Once in the following page, "Mark" user was already created. In the following page, we'll make S3 Bucket to user "Mark". Click "Attach existing policies directly" --&gt; In navigation bar, type "s3" --&gt; Check "AmazonS3Full Access" --&gt; Click on "Next: Tags":

![](../.gitbook/assets/image%20%28142%29.png)

The next step is optional, but I would add Tagging for new created user "Mark". Do as below:

![](../.gitbook/assets/image%20%28264%29.png)

Make sure everything looks all right and then create user:

![](../.gitbook/assets/image%20%2854%29.png)

![](../.gitbook/assets/image%20%2877%29.png)

![](../.gitbook/assets/image%20%28199%29.png)

Quiz: Can you create another users "Andrian" and "James"?

Answer:

![](../.gitbook/assets/image%20%2840%29.png)

![](../.gitbook/assets/image%20%28263%29.png)

![](../.gitbook/assets/image%20%28269%29.png)

![](../.gitbook/assets/image%20%2886%29.png)

![](../.gitbook/assets/image%20%28112%29.png)

![](../.gitbook/assets/image%20%28160%29.png)

![](../.gitbook/assets/image%20%2814%29.png)

Now, all three users "Mark", "Andrian", and "Jame" have access to S3 Bucket.

## IAM Groups and Policies

We've created root user "jeff", and 3 new users that only have policies to access S3 Bucket. I may find that creating and assigning policies to each new users is very tedious and time-consuming. This part, I'll introduce a method to create a group which will give a bunch of users the same policies. 例如，如果我们创建了一个Group1，里面有"Andrian", "Mark", "James"，然后将该Group1的权限设置为“能够访问S3 Bucket"，那么该Group1内的用户就都能访问S3 Bucket了。

我们先将之前创建的"Andrian", "Mark", "James"用户对S3 Bucket的访问权限解除：

![](../.gitbook/assets/image%20%28152%29.png)

![](../.gitbook/assets/image%20%2880%29.png)

![](../.gitbook/assets/image%20%28265%29.png)

![](../.gitbook/assets/image%20%2879%29.png)

![](../.gitbook/assets/image%20%28115%29.png)

![](../.gitbook/assets/image%20%28165%29.png)

到此，"Andrian", "Mark", "James"用户对S3 Bucket的访问权限被解除。Click on "Groups" --&gt; Click on "Create New Group"

![](../.gitbook/assets/image%20%28198%29.png)

Input the name of your group \("Dev"\) and Click on "Next":

![](../.gitbook/assets/image%20%2899%29.png)

Next, we don't need to attach any IAM policies. So, click "Next Step" and click "Create Group":

![](../.gitbook/assets/image%20%28116%29.png)

![](../.gitbook/assets/image%20%2830%29.png)

Now, you'll "Dev" group was created:

![](../.gitbook/assets/image%20%2817%29.png)

Next, we're going to put "Andrian", "Mark" and "James" into "Dev" group, click on "Add Users to group":

![](../.gitbook/assets/image%20%2816%29.png)

Then Check the users you want to add and click on "Add Users":

![](../.gitbook/assets/image%20%28118%29.png)

![](../.gitbook/assets/image%20%28242%29.png)

但是现在，这三个用户并没有权力访问S3 Bucket，所以：Click "Permission" tag --&gt; "Attach Policy":

![](../.gitbook/assets/image%20%28166%29.png)

search "s3" --&gt; check "AmazonS3FullAccess" --&gt; "Attach Policy"

![](../.gitbook/assets/image%20%2860%29.png)

![](../.gitbook/assets/image%20%28234%29.png)

如果Andrian需要访问多个S3的权限怎么办？一般来说，一个用户最多可以有十几个S3的访问权限。这时，我们可以将Andrian添加到另一个Group中（操作方法与之前的相同\)。

如果我们将Mark从Dev Group中移除会发生什么呢？

![](../.gitbook/assets/image%20%28219%29.png)

我们看到，从Dev Group移除Mark后，Mark就不再有访问Dev Group的权限，从而也就不能访问S3了。同理，如果我们将Mark再添加回Dev Group，那么Mark又重新获得了访问S3 Bucket的权限：

![](../.gitbook/assets/image%20%28234%29.png)



## IAM Roles

之前我们介绍了：

1. 如何创建IAM Group（"Dev" Goup）
2. 如何向IAM Group中添加一个或多个用户
3. 增加或删除IAM Group中的用户

那么如果现在有一个EC2，而且我们想让这个EC2能够访问S3 Bucket中的文件该怎么做呢？实际上，EC2对于S3的访问并不像用户对于S3的访问那样  是通过添加IAM Policy来实现的。**EC2对于S3的访问需要通过建立IAM Role来实现**。

![](../.gitbook/assets/image%20%28267%29.png)

![](../.gitbook/assets/image%20%2863%29.png)



所以，我们需要创建这个role：

![](../.gitbook/assets/image%20%2861%29.png)

![](../.gitbook/assets/image%20%28129%29.png)

然后我们attach policy to the Role we created：Search "S3" --&gt; Check "AmazonS3FullAccess" --&gt; Click on "Next Tags" --&gt; Click on "Review"

![](../.gitbook/assets/image%20%28256%29.png)

Type "EC2Role" in "Role name" bar --&gt; Click on "Create role":

![](../.gitbook/assets/image%20%28250%29.png)

这时，EC2Role就被创建，且能够让EC2访问S3 Bucket:

![](../.gitbook/assets/image%20%28200%29.png)

到此，我们只是给了EC2访问S3 Bucket的权限，但是并没有给EC2访问Dev Group的权限。所以，我们回到IAM设置处，给予EC2访问RDS的权限。Click "Groups" --&gt; Click "Dev":

![](../.gitbook/assets/image%20%28201%29.png)

Click on "Permission" --&gt; Click "Attach Policy":

![](../.gitbook/assets/image%20%2878%29.png)

Search "EC2" in navigation bar --&gt; Check "AmazonEC2FullAccess" --&gt; Click "Attach Policy":

![](../.gitbook/assets/image%20%28216%29.png)

Then, we also want to attach RDS Policy. Click "Attach Policy":

![](../.gitbook/assets/image%20%28155%29.png)

Search "RDS" in navigation bar --&gt; Check "AmazonRDSFullAccess" --&gt; Click "Attach Policy":

![](../.gitbook/assets/image%20%28238%29.png)

此时，EC2就有了访问所有S3 Bucket内部文件（RDS）的权限了：

![](../.gitbook/assets/image%20%2832%29.png)



What is the default permission assigned for AWS IAM users to all AWS resources?

![](../.gitbook/assets/image%20%28110%29.png)

![](../.gitbook/assets/image%20%28111%29.png)

![](../.gitbook/assets/image%20%2881%29.png)

![](../.gitbook/assets/image%20%28212%29.png)

![](../.gitbook/assets/image%20%2837%29.png)

![](../.gitbook/assets/image%20%28176%29.png)















