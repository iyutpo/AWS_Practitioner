# Section 2. AWS Identity and Access Management \(IAM\)

## What is IAM?

**AWS IAM stands for Identity and Access Management. IAM is used to securely control access to AWS resources.** 

For example, we can create user accounts for people on our team and allow those users to access an AWS service or feature.

## How does IAM work?

First, we can go to Service Navigation Bar and type "IAM". I'll get:

![](../.gitbook/assets/image%20%2864%29.png)

* **An important thing to know is, when you created your AWS account, a root user account was automatically created as well. The root user account is created automatically when you sign up for AWS. Of course, by default, the root user account can access all AWS resources including billing and all services. 也就是说，root account有最高的权限并且能访问所有AWS提供的service**。
* **另外很重要的一点就是，任何新用户都被默认为不能享用任何AWS服务，因此，我们必须为新用户授权 可以享用的服务**。

You'll see 5 Security Status which is also known as "**AWS Best Practices**". It's a guideline and architecture for maintaining a high level of security, accessibility and efficiency.

1. **Delete your root access keys**: We currently don't need to do anything to our root account.
2. **Activate MFA on your root account**: 
   1. MFA, i.e. **Multi-Factor Authentication provides an additional layer of security on your root account and that security is provided by a third-party.** It provides a continually changing, random 6-digit code along with your password when you want to login your root account.
   2. Expand "Activate MFA on your root account" and click "Manage MFA". 

![](../.gitbook/assets/image%20%2889%29.png)

            3. If this pops up, click "Continue to Security Credentials":

![](../.gitbook/assets/image%20%2814%29.png)

            4. Then click "Activate MFA" button, and select "Virtual MFA device" and "Continue".

![](../.gitbook/assets/image%20%2871%29.png)

![](../.gitbook/assets/image%20%2877%29.png)

            5. Then, take out your smartphone our tablet and install an application called "Google Authenticator":

![](../.gitbook/assets/image%20%2861%29.png)

            6. In "Google Authenticator", click "Scan a barcode". Then return to your AWS "Set up virtual MFA device" page and click "show QR code". Scan it.

![](../.gitbook/assets/image%20%2869%29.png)

            7. Then, input your MFA code 1 and MFA code 2. Click "Assign MFA". Then your MFA will be assigned successfully.

![](../.gitbook/assets/image%20%2842%29.png)

![](../.gitbook/assets/image%20%2899%29.png)

            8. Back to "Dashboard" page and you'll see the second box was checked:

![](../.gitbook/assets/image%20%2874%29.png)

    3. **Create individual IAM users**:

           1. Here, you'll want to create an IAM user. Click "Access management" --&gt; Click "Users" --&gt; "Add user":

![](../.gitbook/assets/image%20%28112%29.png)

            2. Next, you can do the same configuration below or customize your own configuration. Click "Next Permissions"

![](../.gitbook/assets/image%20%2858%29.png)

            3. Then you'll be allowed to "Add new users to group" or "Copy permissions from existing user" or "Attach existing policies directly". Click "Attach existing policies directly" and you'll see "AdministratorAccess" in the window below. "AdministratorAccess" user can access all AWS services. We then check the box for "AdministratorAccess" and click on "Next Tags":

![](../.gitbook/assets/image%20%2890%29.png)

            4. I will leave it blank in "Add tags" page and click on "Next: Review"

![](../.gitbook/assets/image%20%28123%29.png)

             5. Take a look at on your information and click "Create user" if everything is good:

![](../.gitbook/assets/image%20%2815%29.png)

            6. Click "Close" if you succeed:

![](../.gitbook/assets/image%20%2818%29.png)

            7. You'll see a new user "jeff" was created. Then go back to "dashboard", you'll find the third box was checked:

![](../.gitbook/assets/image%20%2888%29.png)

![](../.gitbook/assets/image%20%2830%29.png)

    ****4. **Use groups to assign permissions**:

            1. Click on "Manage Groups" --&gt; Click on "Create New Group"

![](../.gitbook/assets/image%20%2865%29.png)

![](../.gitbook/assets/image%20%2824%29.png)

            2. Create a group named "omegaAdmins" and Click on "Next Step"

![](../.gitbook/assets/image%20%2866%29.png)

            3. Then we'll need to attach policy to "omegaAdmins" group which is similar to attaching policy to "jeff" user. Click and check "AdministratorAccess" box --&gt; Click on "Next Step" --&gt; Click on "Create Group". You'll see a new group "omegaAdmins" was created and the fourth box was also checked automatically:

![](../.gitbook/assets/image%20%2849%29.png)

![](../.gitbook/assets/image%20%285%29.png)

![](../.gitbook/assets/image%20%28101%29.png)

![](../.gitbook/assets/image%20%28110%29.png)

    5. **Apply an IAM password policy**:

            1. Go to "Manage Password Policy"

![](../.gitbook/assets/image%20%2884%29.png)

            2. Click on "Set password policy". Then Check "Prevent password reuses" --&gt; Remember 3 password\(s\) --&gt; Click on "Save Changes":

![](../.gitbook/assets/image%20%28114%29.png)

![](../.gitbook/assets/image%20%2857%29.png)

![](../.gitbook/assets/image%20%2838%29.png)

            3. Then all five boxes are checked.

![](../.gitbook/assets/image%20%2894%29.png)

## Add IAM Users and Set Policies

Since we've created our root user "jeff", now we want to add some new users and assign certain policies to each of them. For example, a new user we want to add is called "Mark" and we want "Mark" to be able to access an S3 Bucket:

![](../.gitbook/assets/image%20%28104%29.png)

As you can see, now we don't have any users except "jeff", the root user:

![](../.gitbook/assets/image%20%287%29.png)

So, we click on "Add user" --&gt; Type "Mark" in User name bar --&gt; Select "Console password" \(we're not going to use "Programmatic access" because it's a more advanced and usually for those developers\) --&gt; Slick on "Custom password" --&gt; input your password --&gt; Uncheck the box for Require password reset" --&gt; "Next permissions":

![](../.gitbook/assets/image%20%2828%29.png)

![](../.gitbook/assets/image%20%2816%29.png)

Once in the following page, "Mark" user was already created. In the following page, we'll make S3 Bucket to user "Mark". Click "Attach existing policies directly" --&gt; In navigation bar, type "s3" --&gt; Check "AmazonS3Full Access" --&gt; Click on "Next: Tags":

![](../.gitbook/assets/image%20%2867%29.png)

The next step is optional, but I would add Tagging for new created user "Mark". Do as below:

![](../.gitbook/assets/image%20%28119%29.png)

Make sure everything looks all right and then create user:

![](../.gitbook/assets/image%20%2827%29.png)

![](../.gitbook/assets/image%20%2832%29.png)

![](../.gitbook/assets/image%20%2893%29.png)

Quiz: Can you create another users "Andrian" and "James"?

Answer:

![](../.gitbook/assets/image%20%2821%29.png)

![](../.gitbook/assets/image%20%28118%29.png)

![](../.gitbook/assets/image%20%28122%29.png)

![](../.gitbook/assets/image%20%2837%29.png)

![](../.gitbook/assets/image%20%2850%29.png)

![](../.gitbook/assets/image%20%2876%29.png)

![](../.gitbook/assets/image%20%289%29.png)

Now, all three users "Mark", "Andrian", and "Jame" have access to S3 Bucket.

## IAM Groups and Policies

We've created root user "jeff", and 3 new users that only have policies to access S3 Bucket. I may find that creating and assigning policies to each new users is very tedious and time-consuming. This part, I'll introduce a method to create a group which will give a bunch of users the same policies. 例如，如果我们创建了一个Group1，里面有"Andrian", "Mark", "James"，然后将该Group1的权限设置为“能够访问S3 Bucket"，那么该Group1内的用户就都能访问S3 Bucket了。

我们先将之前创建的"Andrian", "Mark", "James"用户对S3 Bucket的访问权限解除：

![](../.gitbook/assets/image%20%2872%29.png)

![](../.gitbook/assets/image%20%2834%29.png)

![](../.gitbook/assets/image%20%28120%29.png)

![](../.gitbook/assets/image%20%2833%29.png)

![](../.gitbook/assets/image%20%2852%29.png)

![](../.gitbook/assets/image%20%2878%29.png)

到此，"Andrian", "Mark", "James"用户对S3 Bucket的访问权限被解除。Click on "Groups" --&gt; Click on "Create New Group"

![](../.gitbook/assets/image%20%2892%29.png)

Input the name of your group \("Dev"\) and Click on "Next":

![](../.gitbook/assets/image%20%2845%29.png)

Next, we don't need to attach any IAM policies. So, click "Next Step" and click "Create Group":

![](../.gitbook/assets/image%20%2853%29.png)

![](../.gitbook/assets/image%20%2819%29.png)

Now, you'll "Dev" group was created:

![](../.gitbook/assets/image%20%2811%29.png)

Next, we're going to put "Andrian", "Mark" and "James" into "Dev" group, click on "Add Users to group":

![](../.gitbook/assets/image%20%2810%29.png)

Then Check the users you want to add and click on "Add Users":

![](../.gitbook/assets/image%20%2854%29.png)

![](../.gitbook/assets/image%20%28108%29.png)

但是现在，这三个用户并没有权力访问S3 Bucket，所以：Click "Permission" tag --&gt; "Attach Policy":

![](../.gitbook/assets/image%20%2879%29.png)

search "s3" --&gt; check "Amazon3SS3S



















