# Section 2. AWS Identity and Access Management \(IAM\)

## What is IAM?

**AWS IAM stands for Identity and Access Management. IAM is used to securely control access to AWS resources.** 

For example, we can create user accounts for people on our team and allow those users to access an AWS service or feature.

## How does IAM work?

First, we can go to Service Navigation Bar and type "IAM". I'll get:

![](../.gitbook/assets/image%20%2830%29.png)

* **An important thing to know is, when you created your AWS account, a root user account was automatically created as well. The root user account is created automatically when you sign up for AWS. Of course, by default, the root user account can access all AWS resources including billing and all services. 也就是说，root account有最高的权限并且能访问所有AWS提供的service**。
* **另外很重要的一点就是，任何新用户都被默认为不能享用任何AWS服务，因此，我们必须为新用户授权 可以享用的服务**。

You'll see 5 Security Status which is also known as "**AWS Best Practices**". It's a guideline and architecture for maintaining a high level of security, accessibility and efficiency.

1. **Delete your root access keys**: We currently don't need to do anything to our root account.
2. **Activate MFA on your root account**: 
   1. MFA, i.e. **Multi-Factor Authentication provides an additional layer of security on your root account and that security is provided by a third-party.** It provides a continually changing, random 6-digit code along with your password when you want to login your root account.
   2. 
3. **Create individual IAM users**:
4. **Use groups to assign permissions**:
5. **Apply an IAM password policy**:







