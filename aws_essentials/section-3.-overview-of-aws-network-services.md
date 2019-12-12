# Section 3. Overview of AWS Network Services

**The network services: VPC \(Virtual Private Cloud\) allows us to control access to AWS services that we want to deploy.**

## AWS Global Infrastructure:

When we think about AWS, we have to think of it as a global system. This is because AWS has a worldwide infrastructure. AWS connects data and consumers of that data by using its global infrastructure. **The AWS infrastructure is divided into different regions.** So if you take a look at this map, each of the circles on this map represents an existing AWS region and the regions with the green circles are pending regions that will be in service in the near future. **Regions are geographical areas where a group of AWS resources are located. Regions are designed to service AWS customers that are located closest to that region.** **By using the customers that are closest to your location, you can reduce latency when data is transferred between your location and the AWS servers. Latency is  measured based on the amount of time it takes to transfer data from one location to another.** So the higher the latency, the longer it's going to take for data to transfer from one location to another. Another example of how to might use regions, is i**f you were located in the Eastern United States, but you had customers that were located in Australia. By provisioning AWS resources in Australia, you reduce latency for your customers so that they can access your server as quickly as possible.** If you server was located in the US East region and your customers are located in Australia, your customers would experience significant latency due to the distance that data would have to travel. 

![](../.gitbook/assets/image%20%288%29.png)

So AWS has regions in various locations around the world and within each region you'll find availability zones. **Availability zones are geographically isolated zones within a region that house AWS services**. **Availability zones are where physical data centers are located and multiple availability zones provide redundancy for AWS resources within that region.** What this means, as an example, is if we are in the US East northern Virginia region that there are multiple availability zones within that region. 每一个Availability Zone都有一个AWS data center，而每一个AWS data center就是AWS resources的物理地址。**每一个Availability Zone在地理上是相互隔离的。例如，如果我们将一个S3 Bucket存入一个Availability Zone \#1，那么，如果Availability Zone \#1宕机了，我们仍然能够访问我们的S3 Bucket，因为S3 Bucket中的数据已经被同步到了该region的其他两个Availability Zone \#2 和Availability Zone \#3了。这就体现了AWS的"high availability", "fault tolerant"的架构**。

![](../.gitbook/assets/image%20%2842%29.png)

![](../.gitbook/assets/image%20%28113%29.png)



