# Section 1. AWS Basic Navigation

## Section 1. AWS Basic Navigation

**This article assumes that you've created your own AWS account. \(You can Google "AWS free tier" and Create/Login your AWS account on top right of the web page.**

![](../.gitbook/assets/image%20%28695%29.png)

**Then, you can type "billing" in the navigation bar:**

![](../.gitbook/assets/image%20%28441%29.png)

**​You'll get this page. Or, you can check your Billing Preferences also:**

![](../.gitbook/assets/image%20%28266%29.png)

In "Billing preferences" you can set up email alert.

**Now, let's go back to AWS Homepage by clicking AWS logo on the top left of the page. Scroll down a little bit and expand "All Services". Click "EC2"**

![](../.gitbook/assets/image%20%28103%29.png)

**You may also find all services in the navigation bar under "Services":**

![](../.gitbook/assets/image%20%28685%29.png)

**Besides, "Resource Groups" can create a group. The "pushpin" logo allows you to create a service shortcut by simply dragging the service logo:**

![](../.gitbook/assets/image%20%28593%29.png)

For example, you can create an "EC2" shortcut like this:

![](../.gitbook/assets/image%20%28657%29.png)

**Next, we'll create a Billing Alert to help us ensure we do not exceed our billing threshold per month. Similarly, we can navigate to "Billing" page, and select "Billing preferences". Then, check the box of "Receive Billing Alerts".**

![](../.gitbook/assets/image%20%28361%29.png)

Then, you'll be able to get an alert via email when you're close or exceeded your billing threshold.

Then, in the navigation bar, we search "cloudwatch".

![](../.gitbook/assets/image%20%28408%29.png)

In next page, select "billing" under "Alarms". Then click "Create Alarm":

![](../.gitbook/assets/image%20%28524%29.png)

"Select Metric":

![](../.gitbook/assets/image%20%28636%29.png)

Select "Usage" --&gt; "By AWS Resource" --&gt; Check "EC2" box --&gt; "Select metric"

![](../.gitbook/assets/image%20%28128%29.png)

![](../.gitbook/assets/image%20%28276%29.png)

![](../.gitbook/assets/image%20%2810%29.png)

In the next page, you can scroll down a little bit and select "Greater/Equal to". Type in the particular amount in "Define the threshold value" bar. Click "Next".

![](../.gitbook/assets/image%20%28376%29.png)

![](../.gitbook/assets/image%20%28523%29.png)

Then, you'll see "in Alarm" which means if your billing exceeds $1, you'll get an alarm. You'll also see "SNS" \(i.e. AWS's Simple Notification Service\). You can add an email address to be alarmed when your billing exceeds $1.

![](../.gitbook/assets/image%20%28698%29.png)

Click "Create Topic" and then click "Next".

![](../.gitbook/assets/image%20%28385%29.png)

Define and add description. Select "Next":

![](../.gitbook/assets/image%20%28357%29.png)

In Preview and create page, make sure everything looks okay and then click "Create alarm".

![](../.gitbook/assets/image%20%2813%29.png)

Then we select the billing alarm just created:

![](../.gitbook/assets/image%20%28637%29.png)

**AWS Documentations. Always remember, AWS Documentations are very helpful even for those professional AWS users.**

![](../.gitbook/assets/image%20%2849%29.png)

