# Section 1. AWS Basic Navigation

## Section 1. AWS Basic Navigation

**This article assumes that you've created your own AWS account. \(You can Google "AWS free tier" and Create/Login your AWS account on top right of the web page.**

![](../.gitbook/assets/image%20%28113%29.png)

**Then, you can type "billing" in the navigation bar:**

![](../.gitbook/assets/image%20%2873%29.png)

**​You'll get this page. Or, you can check your Billing Preferences also:**

![](../.gitbook/assets/image%20%2839%29.png)

In "Billing preferences" you can set up email alert.

**Now, let's go back to AWS Homepage by clicking AWS logo on the top left of the page. Scroll down a little bit and expand "All Services". Click "EC2"**

![](../.gitbook/assets/image%20%2820%29.png)

**You may also find all services in the navigation bar under "Services":**

![](../.gitbook/assets/image%20%28111%29.png)

**Besides, "Resource Groups" can create a group. The "pushpin" logo allows you to create a service shortcut by simply dragging the service logo:**

![](../.gitbook/assets/image%20%2897%29.png)

For example, you can create an "EC2" shortcut like this:

![](../.gitbook/assets/image%20%28107%29.png)

**Next, we'll create a Billing Alert to help us ensure we do not exceed our billing threshold per month. Similarly, we can navigate to "Billing" page, and select "Billing preferences". Then, check the box of "Receive Billing Alerts".**

![](../.gitbook/assets/image%20%2856%29.png)

Then, you'll be able to get an alert via email when you're close or exceeded your billing threshold.

Then, in the navigation bar, we search "cloudwatch".

![](../.gitbook/assets/image%20%2868%29.png)

In next page, select "billing" under "Alarms". Then click "Create Alarm":

![](../.gitbook/assets/image%20%2887%29.png)

"Select Metric":

![](../.gitbook/assets/image%20%28102%29.png)

Select "Usage" --&gt; "By AWS Resource" --&gt; Check "EC2" box --&gt; "Select metric"

![](../.gitbook/assets/image%20%2825%29.png)

![](../.gitbook/assets/image%20%2840%29.png)

![](../.gitbook/assets/image%20%281%29.png)

In the next page, you can scroll down a little bit and select "Greater/Equal to". Type in the particular amount in "Define the threshold value" bar. Click "Next".

![](../.gitbook/assets/image%20%2859%29.png)

![](../.gitbook/assets/image%20%2886%29.png)

Then, you'll see "in Alarm" which means if your billing exceeds $1, you'll get an alarm. You'll also see "SNS" \(i.e. AWS's Simple Notification Service\). You can add an email address to be alarmed when your billing exceeds $1.

![](../.gitbook/assets/image%20%28115%29.png)

Click "Create Topic" and then click "Next".

![](../.gitbook/assets/image%20%2862%29.png)

Define and add description. Select "Next":

![](../.gitbook/assets/image%20%2855%29.png)

In Preview and create page, make sure everything looks okay and then click "Create alarm".

![](../.gitbook/assets/image%20%283%29.png)

Then we select the billing alarm just created:

![](../.gitbook/assets/image%20%28103%29.png)

**AWS Documentations. Always remember, AWS Documentations are very helpful even for those professional AWS users.**

![](../.gitbook/assets/image%20%2813%29.png)

