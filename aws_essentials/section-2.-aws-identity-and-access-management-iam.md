# Section 2. AWS Identity and Access Management \(IAM\)

## What is IAM?

**AWS IAM stands for Identity and Access Management. IAM is used to securely control access to AWS resources.** 

For example, we can create user accounts for people on our team and allow those users to access an AWS service or feature.

## How does IAM work?

First, we can go to Service Navigation Bar and type "IAM". I'll get:

![](../.gitbook/assets/image%20%2843%29.png)

* **An important thing to know is, when you created your AWS account, a root user account was automatically created as well. The root user account is created automatically when you sign up for AWS. Of course, by default, the root user account can access all AWS resources including billing and all services. 也就是说，root account有最高的权限并且能访问所有AWS提供的service**。
* **另外很重要的一点就是，任何新用户都被默认为不能享用任何AWS服务，因此，我们必须为新用户授权 可以享用的服务**。

You'll see 5 Security Status which is also known as "**AWS Best Practices**". It's a guideline and architecture for maintaining a high level of security, accessibility and efficiency.

1. **Delete your root access keys**: We currently don't need to do anything to our root account.
2. **Activate MFA on your root account**: 
   1. MFA, i.e. **Multi-Factor Authentication provides an additional layer of security on your root account and that security is provided by a third-party.** It provides a continually changing, random 6-digit code along with your password when you want to login your root account.
   2. Expand "Activate MFA on your root account" and click "Manage MFA". 

![](../.gitbook/assets/image%20%2863%29.png)

            3. If this pops up, click "Continue to Security Credentials":

![](../.gitbook/assets/image%20%289%29.png)

            4. Then click "Activate MFA" button, and select "Virtual MFA device" and "Continue".

![](../.gitbook/assets/image%20%2849%29.png)

![](../.gitbook/assets/image%20%2853%29.png)

            5. Then, take out your smartphone our tablet and install an application called "Google Authenticator":

![](../.gitbook/assets/image%20%2841%29.png)

            6. In "Google Authenticator", click "Scan a barcode". Then return to your AWS "Set up virtual MFA device" page and click "show QR code". Scan it.

![](../.gitbook/assets/image%20%2847%29.png)

            7. Then, input your MFA code 1 and MFA code 2. Click "Assign MFA". Then your MFA will be assigned successfully.

![](../.gitbook/assets/image%20%2827%29.png)

![](../.gitbook/assets/image%20%2871%29.png)

            8. Back to "Dashboard" page and you'll see the second box was checked:

![](../.gitbook/assets/image%20%2851%29.png)

    3. **Create individual IAM users**:

           1. Here, you'll want to create an IAM user. Click "Access management" --&gt; Click "Users" --&gt; "Add user":

![](../.gitbook/assets/image%20%2882%29.png)

            2. Next, you can do the same configuration below or customize your own configuration. Click "Next Permissions"

![](../.gitbook/assets/image%20%2838%29.png)

            3. Then you'll be allowed to "Add new users to group" or "Copy permissions from existing user" or "Attach existing policies directly". Click "Attach existing policies directly" and you'll see "AdministratorAccess" in the window below. "AdministratorAccess" user can access all AWS services. We then check the box for "AdministratorAccess" and click on "Next Tags":

![](../.gitbook/assets/image%20%2864%29.png)

            4. I will leave it blank in "Add tags" page and click on "Next: Review"

![](../.gitbook/assets/image%20%2889%29.png)

             5. Take a look at on your information and click "Create user" if everything is good:

![](../.gitbook/assets/image%20%2810%29.png)

            6. Click "Close" if you succeed:

![](../.gitbook/assets/image%20%2812%29.png)

            7. You'll see a new user "jeff" was created. Then go back to "dashboard", you'll find the third box was checked:

![](../.gitbook/assets/image%20%2862%29.png)

![](../.gitbook/assets/image%20%2819%29.png)

    ****4. **Use groups to assign permissions**:

            1. Click on "Manage Groups" --&gt; Click on "Create New Group"

![](../.gitbook/assets/image%20%2844%29.png)

![](../.gitbook/assets/image%20%2816%29.png)

            2. Create a group named "omegaAdmins" and Click on "Next Step"

![](../.gitbook/assets/image%20%2845%29.png)

            3. Then we'll need to attach policy to "omegaAdmins" group which is similar to attaching policy to "jeff" user. Click and check "AdministratorAccess" box --&gt; Click on "Next Step" --&gt; Click on "Create Group". You'll see a new group "omegaAdmins" was created and the fourth box was also checked automatically:

![](../.gitbook/assets/image%20%2833%29.png)

![](../.gitbook/assets/image%20%285%29.png)

![](../.gitbook/assets/image%20%2873%29.png)

![](../.gitbook/assets/image%20%2880%29.png)

    5. **Apply an IAM password policy**:

            1. Go to "Manage Password Policy"

![](../.gitbook/assets/image%20%2858%29.png)

            2. Click on "Set password policy". Then Check "Prevent password reuses" --&gt; Remember 3 password\(s\) --&gt; Click on "Save Changes":

![](../.gitbook/assets/image%20%2884%29.png)

![](../.gitbook/assets/image%20%2837%29.png)

![](../.gitbook/assets/image%20%2823%29.png)

            3. Then all five boxes are checked.

![](../.gitbook/assets/image%20%2866%29.png)













