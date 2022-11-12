# aws-solutions-architect-associate-notes
My notes when preparing AWS solutions architect associate cert

# Notes
## S3 storage class
- S3 Standard
    - Designed for durability of 99.999999999% of objects across multiple Availability Zones
    - Designed for 99.99% availability over a given year
- S3 Intelligent-Tiering
    -  delivers automatic cost savings by moving objects between four access tiers when access patterns change
- S3 Standard-IA
    - Infrequent Access
    - Designed for 99.9% availability over a given year
- S3 One Zone-IA
    - One zone, more cheaper, Designed for 99.5% availability over a given year
- S3 Glacier
    - Configurable retrieval times, from minutes to hours
- S3 Glacier Deep Archive
    - Retrieval time within 12 hours
- S3 Outposts
    - Outpost is a fully managed service that offers the same AWS infrastructure, AWS services, APIs, and tools to virtually any datacenter, co-location space, or on-premises facility for a truly consistent hybrid experience.
    - Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment to meet local data processing and data residency needs

## S3 Encryption
- Encryption In Transit
- Encryption At Rest
    - Server side
        - S3 Managed Keys / SSE - S3 (server side encryption S3 ) - when Amazon manages the encryption and decryption keys for you automatically. In this scenario, you concede a little control to Amazon in exchange for ease of use.
        - AWS Key Management Service / SSE - KMS - when Amazon and you both manage the encryption and decryption keys together.
        - Server Side Encryption w/ customer provided keys / SSE - C - when I give Amazon my own keys that I manage. In this scenario, you concede ease of use in exchange for more control.
    - Client side

## S3 Select
S3 Select is an Amazon S3 feature that is designed to pull out only the data you need from an object

## IAM
- You cannot nest IAM Groups. Individual IAM users can belong to multiple groups, but creating subgroups so that one IAM Group is embedded inside of another IAM Group is not possible.
- you let an IAM role be assumed by one of the Active Directories. This is because the IAM ID Federation feature allows an external service to have the ability to assume an IAM role.
### Priority Levels in IAM:
- Explicit Deny: Denies access to a particular resource and this ruling cannot be overruled.
- Explicit Allow: Allows access to a particular resource so long as there is not an associated Explicit Deny.
- Default Deny (or Implicit Deny): IAM identities start off with no resource access. Access instead must be granted.
## Cloud front
- Edge locations are not just read only. They can be written to which will then return the write value back to the origin.
- An Origin Access Identity (OAI) is used for sharing private content via CloudFront. The OAI is a virtual user that will be used to give your CloudFront distribution permission to fetch a private object from your origin (e.g. S3 bucket).
- Use signed URLs for the following cases:
    - You want to use an RTMP distribution. Signed cookies aren't supported for RTMP distributions.
    - You want to restrict access to individual files, for example, an installation download for your application.
    - Your users are using a client (for example, a custom HTTP client) that doesn't support cookies.
- Use signed cookies for the following cases:
    - You want to provide access to multiple restricted files. For example, all of the files for a video in HLS format or all of the files in the paid users' area of a website.
    - You don't want to change your current URLs.
## Snowball
- AWS send the device to your home and you upload the data, then they transport the device to AWS
- As a rule of thumb, if it takes more than one week to upload your data to AWS using the spare capacity of your existing internet connection, then you should consider using Snowball.
## Storage gateway
- Application on-premise can connect to files in cloud through Storage gateway using standard storage protocols, such as NFS, SMB, and iSCSI. But the files are stored in the cloud
- The Storage Gateway service can either be a physical device or a VM image downloaded onto a host in an on-prem data center. It acts as a bridge to send or receive data from AWS.
- File Gateway - Operates via NFS or SMB and is used to store files in S3 over a network filesystem mount point in the supplied virtual machine. Simply put, you can think of a File Gateway as a file system mount on S3.
- Volume Gateway - Operates via iSCSI and is used to store copies of hard disk drives or virtual hard disk drives in S3. These can be achieved via Stored Volumes or Cached Volumes. Simply put, you can think of Volume Gateway as a way of storing virtual hard disk drives in the cloud.
    - Volume Gateway's Stored Volumes let you store data locally on-prem and backs the data up to AWS as a secondary data source.
    - Volume Gateway's Cached Volumes differ as they do not store the entire dataset locally like Stored Volumes. Instead, AWS is used as the primary data source and the local hardware is used as a caching layer.
- Tape Gateway - Operates as a Virtual Tape Library


## EC2
- A golden image is simply an AMI that you have fully customized to your liking with all necessary software/data/configuration details set and ready to go once. This personal AMI can then be the source from which you launch new instances.
- On-Demand instances are based on a fixed rate by the hour or second. As the name implies, you can start an On-Demand instance whenever you need one and can stop it when you no longer need it. There is no requirement for a long-term commitment.
- Reserved instances ensure that you keep exclusive use of an instance on 1 or 3 year contract terms. The long-term commitment provides significantly reduced discounts at the hourly rate.
    - Standard Reserved Instances have inflexible reservations that are discounted at 75% off of On-Demand instances. Standard Reserved Instances cannot be moved between regions. You can choose if a Reserved Instance applies to either a specific Availability Zone, or an Entire Region, but you cannot change the region.
    - Convertible Reserved Instances are instances that are discounted at 54% off of On-Demand instances, but you can also modify the instance type at any point. For example, you suspect that after a few months your VM might need to change from general purpose to memory optimized, but you aren't sure just yet. So if you think that in the future you might need to change your VM type or upgrade your VMs capacity, choose Convertible Reserved Instances. There is no downgrading instance type with this option though.
    - Scheduled Reserved Instances are reserved according to a specified timeline that you set. For example, you might use Scheduled Reserved Instances if you run education software that only needs to be available during school hours. This option allows you to better match your needed capacity with a recurring schedule so that you can save money.
- AWS Spot Instances are unused Elastic Compute Cloud (EC2) instances, with a variable price that depends on supply and demand in the Amazon spot market, and is lower than the on demand price for the same instance type.
- Reserved Instances that are terminated are billed until the end of their term.
- With EC2, termination protection of the instance is disabled by default
- Placement group
    - Clustered Placement Grouping is when you put all of your EC2 instances in a single availability zone. This is recommended for applications that need the lowest latency possible and require the highest network throughput.
    - Spread Placement Grouping is when you put each individual EC2 instance on top of its own distinct hardware so that failure is isolated.
    - Partitioned Placement Grouping is similar to Spread placement grouping, but differs because you can have multiple EC2 instances within a single partition. Failure instead is isolated to a partition (say 3 or 4 instances instead of 1), yet you enjoy the benefits of close proximity for improved network performance.

## EBS
- There are five different types of EBS Storage:
    - General Purpose (SSD)
    - Provisioned IOPS (SSD, built for speed)
    - Throughput Optimized Hard Disk Drive (magnetic, built for larger data loads)
    - Cold Hard Disk Drive (magnetic, built for less frequently accessed workloads)
    - Magnetic

## ENI
- Enhanced Networking ENI uses single root I/O virtualization to provide high-performance networking capabilities on supported instance types
- For instances that work with Machine Learning and High Performance Computing, use EFA (Elastic Fabric Adaptor)

## Security group
-  while NACLs control inbound and outbound traffic for your subnets (they act as a Firewall for Subnets)
## WAF
- WAF operates as a Layer 7 firewall
## CloudTrail
- CloudTrail Events stores the last 90 days of events in its Event History. This is enabled by default and is no additional cost.
FSx for Windows
- With FSx for Windows, you can easily move your Windows-based applications that require file storage in AWS.
- FSx for Windows removes duplicated content and compresses common content
- By default, all data is encrypted at rest.
RDS
- SQS queues can be used to store pending database writes if your application is struggling under a high write load
- Multi-AZ is supported for all DB flavors except aurora. This is because Aurora is completely fault-tolerant on its own.
- DB snapshots are done manually by the administrator. A key different from automated backups is that they are retained even after the original RDS instance is terminated. With automated backups, the backed up data in S3 is wiped clean along with the RDS engine. 
- Aurora is the AWS flagship DB known to combine the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases. It is a MySQL/PostgreSQL-compatible RDBMS that provides the security, availability, and reliability of commercial databases at 1/10th the cost of competitors. It is far more effective as an AWS database due to the 5x and 3x performance multipliers for MySQL and PostgreSQL respectively.
- A common tactic for migrating RDS DBs into Aurora RDs is to create a read replica of a RDS MariaDB/MySQL DB as an Aurora DB. Then simply promote the Aurora DB into a production instance and delete the old MariaDB/MySQL DB.
- Aurora Serverless is a simple, on-demand, autoscaling configuration for the MySQL/PostgreSQl-compatible editions of Aurora. With Aurora Serverless, your instance automatically scales up or down and starts on or off based on your application usage. The use cases for this service are infrequent, intermittent, and unpredictable workloads.

## DynamoDB
- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache that can reduce Amazon DynamoDB response times from milliseconds to microseconds, even at millions of requests per second.
- A DynamoDB stream is an ordered flow of information about changes to items in an Amazon DynamoDB table. When you enable a stream on a table, DynamoDB captures information about every modification to data items in the table.

## Redshift
- Amazon Redshift is a fully managed, petabyte-scale data warehouse service in the cloud
- Amazon Redshift Spectrum is used to run queries against exabytes of unstructured data in Amazon S3, with no loading or ETL
## Route53
- When you buy a domain name, every DNS address starts with an SOA (Start of Authority) record. The SOA record stores information about the name of the server that kicked off the transfer of ownership, the administrator who will now use the domain, the current metadata available, and the default number of seconds or TTL.
- NS records, or Name Server records, are used by the Top Level Domain hosts (.org, .com, .uk, etc.) to direct traffic to the Content servers. The Content DNS servers contain the authoritative DNS records.
- A records: These are the fundamental type of DNS record. The “A” in A records stands for “address”. These records are used by a computer to directly pair a domain name to an IP address. IPv4 and IPv6 are both supported with "AAAA" referring to the IPv6 version. A: URL -> IPv4 and AAAA: URL -> IPv6.
- CName records: Also referred to as the Canonical Name. These records are used to resolve one domain name to another domain name. For example, the domain of the mobile version of a website may be a CName from the domain of the browser version of that same website rather than a separate IP address. This would allow mobile users who visit the site and to receive the mobile version. CNAME: URL -> URL.
- Alias records: These records are used to map your domains to AWS resources such as load balancers, CDN endpoints, and S3 buckets. Alias records function similarly to CNames in the sense that you map one domain to another. The key difference though is that by pointing your Alias record at a service rather than a domain name, you have the ability to freely change your domain names if needed and not have to worry about what records might be mapped to it. Alias records give you dynamic functionality. Alias: URL -> AWS Resource.
- PTR records: These records are the opposite of an A record. PTR records map an IP to a domain and they are used in reverse DNS lookups as a way to obtain the domain name of an IP address. PTR: IPv4 -> URL.
- routing
    - Simple Routing is used when you just need a single record in your DNS with either one or more IP addresses behind the record in case you want to balance load. If you specify multiple values in a Simple Routing policy, Route53 returns a random IP from the options available.
    - Weighted Routing is used when you want to split your traffic based on assigned weights. For example, if you want 80% of your traffic to go to one AZ and the rest to go to another, use Weighted Routing. This policy is very useful for testing feature changes and due to the traffic splitting characteristics, it can double as a means to perform blue-green deployments. When creating Weighted Routing, you need to specify a new record for each IP address. You cannot group the various IPs under one record like with Simple Routing.
    - Latency-based Routing, as the name implies, is based on setting up routing based on what would be the lowest latency for a given user. To use latency-based routing, you must create a latency resource record set in the same region as the corresponding EC2 or ELB resource receiving the traffic. When Route53 receives a query for your site, it selects the record set that gives the user the quickest speed. When creating Latency-based Routing, you need to specify a new record for each IP.
    - Failover Routing is used when you want to configure an active-passive failover set up. Route53 will monitor the health of your primary so that it can failover when needed. You can also manually set up health checks to monitor all endpoints if you want more detailed rules.
    - Geolocation Routing lets you choose where traffic will be sent based on the geographic location of your users.
    - Geo-proximity Routing lets you choose where traffic will be sent based on the geographic location of your users and your resources. You can choose to route more or less traffic based on a specified weight which is referred to as a bias. This bias either expands or shrinks the availability of a geographic region which makes it easy to shift traffic from resources in one location to resources in another. To use this routing method, you must enable Route53 traffic flow. If you want to control global traffic, use Geo-proximity routing. If you want traffic to stay in a local region, use Geolocation routing.
    - Multivalue Routing is pretty much the same as Simple Routing, but Multivalue Routing allows you to put health checks on each record set. This ensures then that only a healthy IP will be randomly returned rather than any IP.

## ELB
- Application LBs are best suited for HTTP(S) traffic and they balance load on layer 7. 
- Network LBs are best suited for TCP traffic where performance is required and they balance load on layer 4. They are capable of managing millions of requests per second while maintaining extremely low latency
- Classic LBs are the legacy ELB produce and they balance either on HTTP(S) or TCP, but not both. Even though they are the oldest LBs, they still support features like sticky sessions and X-Forwarded-For headers.
VPC
- VPCs are region specific and you can have up to five VPCs per region.
- Amazon always reserves five IP addresses within a subnet. The first four IP addresses and the last IP address of each subnet CIDR block will always be unavailable for use.
## VPN
- Naturally, your instances that you launch in your VPC can't communicate with your own on-premise servers. You can allow the access by first:
    - attaching a virtual private gateway to the VPC
    - creating a custom route table for the connection
    - updating your security group rules to allow traffic from the connection
    - creating the managed VPN connection itself.
- To bring up VPN connection, you must also define a customer gateway resource in AWS, which provides AWS information about your customer gateway device. And you have to set up an Internet-routable IP address of the customer gateway's external interface.
- 

## SQS
- FIFO SQS queues guarantee exactly-once processing and is limited to 300 transactions per second.
- Messages in the queue can be kept there from one minute to 14 days and the default retention period is 4 days.
- Visibility timeouts in SQS are the mechanism in which messages marked for delivery from the queue are given a time frame to be fully received by a reader. This is done by temporarily making them invisible to other readers. If the message is not fully processed within the time limit, the message becomes visible again. This is another way in which messages can be duplicated. If you want to reduce the chance of duplication, increase the visibility timeout.
- The visibility timeout maximum is 12 hours.
- Always remember that the messages in the SQS queue will continue to exist even after the EC2 instance has processed it, until you delete that message. You have to ensure that you delete the message after processing to prevent the message from being received and processed again once the visibility timeout expires.
- SQS long-polling: This polling technique will only return from the queue once a message is there, regardless if the queue is currently full or empty. This way, the reader needs to wait either for the timeout set or for a message to finally arrive. SQS long polling doesn't return a response until a message arrives in the queue, reducing your overall cost over time.
- SQS short-polling: This polling technique will return immediately with either a message that’s already stored in the queue or empty-handed.
## SWF:  Simple workflow service
- Actor: worker that trigger a workflow
- Decider: worker that control the flow
- Activity Worker: actually carry out the task to completion
## Lambda
- X-Ray: use to debug
## CloudFormation
- similar to terraform
## Elastic Beantalk
- Lambda runs your code, Beantalk runs your application
## Cignito
- Web Identity Federation, like Facebook/Google login
## Resource Access Manager
- share AWS resource with any AWS account or within AWS organization
## Athena
- Query S3 content using SQL
## Macie
- Detect sensitive data,  ML-powered
## Others:
- AWS Security Token Service (AWS STS) is the service that you can use to create and provide trusted users with temporary security credentials that can control access to your AWS resources.
- AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet. Chef and Puppet are automation platforms that allow you to use code to automate the configurations of your servers.
- A media transcoder in the cloud. Basically, it is a service that converts media files from their original format to the media format specified whether for phones, tablets, PCs, etc.
- AWS Directory Service provides multiple ways to use Amazon Cloud Directory and Microsoft Active Directory (AD) with other AWS services.
- AWS IoT Core is a managed cloud service that lets connected devices easily and securely interact with cloud applications and other devices.
- Amazon WorkSpaces is a managed, secure Desktop-as-a-Service (DaaS) solution. You can use Amazon WorkSpaces to provision either Windows or Linux desktops in just a few minutes and quickly scale to provide thousands of desktops to workers across the globe
- The term pilot light is often used to describe a disaster recovery scenario in which a minimal version of an environment is always running in the cloud.
- You can use Amazon Data Lifecycle Manager (Amazon DLM) to automate the creation, retention, and deletion of snapshots taken to back up your Amazon EBS volumes.
- You can bring part or all of your public IPv4 address range from your on-premises network to your AWS account. You continue to own the address range, but AWS advertises it on the Internet. After you bring the address range to AWS, it appears in your account as an address pool

# Mock exam notes
- Subnets have a DHCP option set. DHCP stands for dynamic host control protocol, this is how devices automatically receive their IP addresses. Each VPC comes with one DHCP option set, and can only have one applied at a time. It can be changed, but you must create a new one to do so, you can not edit your DHCP option set.
- What does ::/0 mean? it is actually for all IPv6 addresses
- A Bastion Host is an Ec2 instance in a public subnet inside a VPC. And they are a great security feature that can be used to allow incoming management connection and then once connect you can jump/connect into private resources in subnets. It is an inbound management point and you can really tighten up what access is allowed with your route tables
- A gateway endpoint is used for AWS public services, So remember that some AWS services are public services and they sit inside the AWS public zone, and sometimes we want to connect to these public services like s3 or DynamoDB from a private instance or subnet that does not have access to the internet and does not have a NAT Gateway set up
- A NAT gateway must be provisioned into a public subnet (so that it has a route to the internet), and it must part of the private subnet's route table (so that the private instances have a route to the NAT gateway).
- AWS Backup is a fully managed backup service that makes it easy to centralize and automate the back up of data across AWS services in the cloud as well as on premises using the AWS Storage Gateway.
- One Snowball Edged device can hold up to 100TB. You would need 200 devices. For 10PB or more, AWS recommends Snowmobile as a more efficient and cost effective solution. One Snowmobile can hold up to 100PB, so that is all you would need.
- Virtual Tape Library gateway allows us to present a virtual tape library over ISCSI to any compatible backup software, this has a high admin overhead and is also costly, and should be stored off site, Allows us to present a virtual tape drive and it is stored in S3 Can be used to migrate your data into AWS over a period of time
-  Lambda functions are not persistent and you get a new runtime environment each time you invoke the function. You will need to pull data into your runtime environment. Any outputs from your function you can store in DynamoDB or s3. If we need longer, Step Functions is a great choice.
- How can you give your Lambda function more CPU capacity so it completes faster? Allocating more RAM to the function also allocates more CPU.
- Security groups are stateful: This means any changes applied to an incoming rule will be automatically applied to the outgoing rule. e.g. If you allow an incoming port 80, the outgoing port 80 will be automatically opened.
- Network ACLs are stateless: This means any changes applied to an incoming rule will not be applied to the outgoing rule. e.g. If you allow an incoming port 80, you would also need to apply the rule for outgoing traffic.
- Both AWS Managed and Customer Managed keys support key rotation. Rotation is when the physical data used to completed the cryptographic operation is changed. With AWS managed keys, rotation occurs every three years and cannot be disabled.
- We have two types of Customer Master Keys (CMKs): AWS managed CMKs and customer managed CMKs. Customer managed keys are created by customers and are more configurable than AWS managed keys. However, those keys cannot be shared across regions.
-  Instance role key rotation is handled by IAM/STS
- When a storage device has reached the end of its useful life, AWS procedures do include a decommissioning process that is designed to prevent customer data from being exposed to unauthorized individuals. AWS uses the techniques detailed in DoD 5220.22-M (“National Industrial Security Program Operating Manual “) or NIST 800-88 (“Guidelines for Media Sanitization”) to destroy data as part of the decommissioning process
- Security groups cannot be attached to DynamoDB.
- Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL
- A cluster placement group is a logical grouping of instances within a single Availability Zone. A cluster placement group can span peered VPCs in the same Region. Instances in the same cluster placement group enjoy a higher per-flow throughput limit for TCP/IP traffic and are placed in the same high-bisection bandwidth segment of the network.
- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache that can reduce Amazon DynamoDB response times from milliseconds to microseconds, even at millions of requests per second. While DynamoDB offers consistent single-digit millisecond latency, DynamoDB with DAX takes performance to the next level with response times in microseconds for millions of requests per second for read-heavy workloads. With DAX, your applications remain fast and responsive, even when a popular event or news story drives unprecedented request volumes your way. No tuning required.
- Amazon DynamoDB auto scaling uses the AWS Application Auto Scaling service to dynamically adjust provisioned throughput capacity on your behalf, in response to actual traffic patterns. This enables a table or a global secondary index to increase its provisioned read and write capacity to handle sudden increases in traffic, without throttling. When the workload decreases, Application Auto Scaling decreases the throughput so that you don't pay for unused provisioned capacity. Note that if you use the AWS Management Console to create a table or a global secondary index, DynamoDB auto scaling is enabled by default. You can modify your auto scaling settings at any time.
- Your AWS account has default quotas, formerly referred to as limits, for each AWS service. Unless otherwise noted, each quota is Region-specific. You can request increases for some quotas, and other quotas cannot be increased. Service Quotas is an AWS service that helps you manage your quotas for over 100 AWS services from one location. Along with looking up the quota values, you can also request a quota increase from the Service Quotas console.
- Warm standby maintains a scaled-down but fully functional version of your workload always running in the DR Region. Business-critical systems are fully duplicated and are always on, but with a scaled down fleet. When the time comes for recovery, the system is scaled up quickly to handle the production load
- Best practices for configuring network interfaces 
  - You can attach a network interface to an instance when it's running (hot attach), when it's stopped (warm attach), or when the instance is being launched (cold attach).
  - You can detach secondary network interfaces when the instance is running or stopped. However, you can't detach the primary network interface.
  - You can move a network interface from one instance to another, if the instances are in the same Availability Zone and VPC but in different subnets.
  - When launching an instance using the CLI, API, or an SDK, you can specify the primary network interface and additional network interfaces.
  - Launching an Amazon Linux or Windows Server instance with multiple network interfaces automatically configures interfaces, private IPv4 addresses, and route tables on the operating system of the instance.
  - A warm or hot attach of an additional network interface may require you to manually bring up the second interface, configure the private IPv4 address, and modify the route table accordingly.
  - Instances running Amazon Linux or Windows Server automatically recognize the warm or hot attach and configure themselves.
  - Attaching another network interface to an instance (for example, a NIC teaming configuration) cannot be used as a method to increase or double the network bandwidth to or from the dual-homed instance. If you attach two or more network interfaces from the same subnet to an instance, you may encounter networking issues such as asymmetric routing. If possible, use a secondary private IPv4 address on the primary network interface instead.
  - For more information, see Assigning a secondary private IPv4 address. https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html
- Memory utilization is not available as an out of the box metric in CloudWatch. You can, however, collect memory metrics when you configure a custom metric for CloudWatch. Types of custom metrics that you can set up include:
  - Memory utilization
  - Disk swap utilization
  - Disk space utilization
  - Page file utilization
  - Log collection
 
- Q: What happens during Multi-AZ failover and how long does it take? Failover is automatically handled by Amazon RDS so that you can resume database operations as quickly as possible without administrative intervention.
  - When failing over, Amazon RDS simply flips the canonical name record (CNAME) for your DB instance to point at the standby, which is in turn promoted to become the new primary. We encourage you to follow best practices and implement database connection retry at the application layer.
  - Failovers, as defined by the interval between the detection of the failure on the primary and the resumption of transactions on the standby, typically complete within one to two minutes. Failover time can also be affected by whether large uncommitted transactions must be recovered; the use of adequately large instance types is recommended with Multi-AZ for best results. AWS also recommends the use of Provisioned IOPS with Multi-AZ instances for fast, predictable, and consistent throughput performance.
- Cloud watch can monitor Auto Scaling Groups and optimize resource utilization
- The default timeframe for scheduling an AWS KMS key deletion is 30 days. The timeframe selection for scheduling an AWS KMS key deletion is 7-30 days.
- There are 8 permitted services on which you may conduct vulnerability and penetration testing without prior approval from AWS
  - Amazon EC2 instances, NAT Gateways, and Elastic Load Balancers
  - Amazon RDS
  - Amazon CloudFront
  - Amazon Aurora
  - Amazon API Gateways
  - AWS Lambda and Lambda Edge functions
  - Amazon Lightsail resources
  - Amazon Elastic Beanstalk environments
 
- The root user (root account) is capable of enabling MFA Delete. Versioning must be enabled to enable MFA Delete on an S3 Bucket.
- Personnel Security is an AWS responsibility in the Shared Responsibility Model. AWS must maintain the security of the cloud by protecting facilities using security personnel.
- Low risk of credential exposure, no need for creating IAM Users, and no need for rotating STS keys are all benefits of using STS
- Only Business or Enterprise customers with AWS Trusted Advisor have programmatic access. Only Business or Enterprise customers with AWS Trusted Advisor has access to automated CloudWatch alerting
- AWS Trusted Advisors provides recommendations that help you follow AWS best practices. Trusted Advisor evaluates your account by using checks. These checks identify ways to optimize your AWS infrastructure, improve security and performance, reduce costs, and monitor service quotas. You can then follow the check recommendations to optimize your services and resources.
- In regards to best practices, Any IAM User with AWS Console access should be required to use MFA. The requirement of MFA will decrease risks to the AWS account
- An IAM user with the AWS managed IAM Policy "PowerUserAccess" is capable of most administrative tasks in an AWS account but is limited. The limitations consist of no billing access and the inability to manage IAM users and groups.
- FIPS 140-2 Level 3 is the level of compliance is CloudHSM (Cloud Hardware Security Module)
- Amazon Inspector analyzes AWS Resource behavior, test network security, assesses deviations from best practices, and provides recommendations on how to resolve based on Inspector reports.
- S3 supports two types of replication: cross-region replication (CRR) and same-region replication (SRR). It does not support cross-account replication.
- When you suspend versioning, S3 retains all current and existing past versions. However, all new objects will overwrite the existing current version. No new versions will be created.
- S3 Accelerated Transfer first utilizes the public internet and then uses the closest best performance edge locations to transfer through fewer networks. Once it hits the edge locations, it use the AWS global network, which is much faster with lower consistent latency.
- To use an S3 bucket for Route 53 DNS failover, the bucket name must match the domain name.
- AAAA map to an IPV6 address
- Geo location routing is focused delivering queries to match the location of your customers, the physical geography, so you can create records with the same name and type in a hosted zone but set a location field, so that location can be default, set to a country, or continent
- A use-case of geo location routing policy is data protection/sovereignty issues for example Europe's general data protection regulation - and Geo-routing would be a great reason to use geo-location (as opposed to latency) to ensure the right EC2 instances, and databases, interact with European customers
- Amazon Route 53 alias records provide a Route 53–specific extension to DNS functionality. Alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets. They also let you route traffic from one record in a hosted zone to another record
- All routing policies can have an optional health check, except simple routing policies
- You can not use capital letters in bucket names. S3 Bucket names must be unique in all regions. You can not reuse an S3 Bucket name, nor can you use a bucket name that exists anywhere in any AWS account
- Inline policies are policies that you create and manage and embed directly into a single user, group, or role. Inline policies are useful if you want to maintain a strict one-to-one relationship between a policy and the principal entity that it's applied to.
- If versioning is disabled and the object is deleted, it's gone forever.
- 5 terabytes is the largest individual object you can store in S3
- EC2 instance metadata can be used to configure or manage a running instance, and can also be used to access user data that was specified when the instance was launched
- AMIs are region specific
- There are a number of prerequisites that must be meet to allow for hibernation, including a specific set of supported EC2 instance types. Reference Documentation: Hibernate Your On-Demand or Reserved Linux Instance
- EBS volumes are not encrypted by default.
- DynamoDB supports backup and restore
- IBM Db2 is not a supported database engine
- AWS handles NAT Gateway scaling for you
- What instance will the ELB load balancer send traffic to if no hosts are healthy?  It will send traffic to all the instances, hoping one is online.
- CloudWatch's default metric interval is 5 minutes
- Baking your code into your AMIs will help reduce provisioning time
- Yes! SQS can only handle messages up to 256KB of text in any format
- Redshift focuses on storing data and not on streaming it
- At this time, Redshift does not support multi-AZ deployments.
- Kinesis Data Analytics allows you to transform data using SQL
- You need to wait at least 7 days before you can schedule a KMS key to be deleted
- GuardDuty focuses on monitoring your networking traffic
- What part of a CloudFormation template allows you to pass values into the template? Parameters allow us to pass data into the template before it's created.
- Global Accelerator can help deal with IP caching issues by providing static IPs.
- Trusted Advisor is a free tool that audits for AWS best practices
- Organizations can consolidate your logs into a single S3 bucket
- You need to place the account ID in the role trust policy to allow the other account to assume it
- Config is able to track AWS architecture and check for best practice violations
- Database Migration Service can be used to migrate a databse from on-prem to RDS
- AWS Migration Hub can organize and track your move to the cloud.
- NACL rules are evaluated by rule number from lowest to highest and executed immediately when a matching rule is found
- Using an Application Load Balancer instead of a Classic Load Balancer has the following benefits:
 
  - Support for path-based routing. You can configure rules for your listener that forward requests based on the URL in the request. This enables you to structure your application as smaller services, and route requests to the correct service based on the content of the URL.
  - Support for host-based routing. You can configure rules for your listener that forward requests based on the host field in the HTTP header. This enables you to route requests to multiple domains using a single load balancer.
  - Support for routing based on fields in the request, such as standard and custom HTTP headers and methods, query parameters, and source IP addresses.
  - Support for routing requests to multiple applications on a single EC2 instance. You can register each instance or IP address with the same target group using multiple ports.
  - Support for redirecting requests from one URL to another.
  - Support for returning a custom HTTP response.
  - Support for registering targets by IP address, including targets outside the VPC for the load balancer.
  - Support for registering Lambda functions as targets.
  - Support for the load balancer to authenticate users of your applications through their corporate or social identities before routing requests.
  - Support for containerized applications. Amazon Elastic Container Service (Amazon ECS) can select an unused port when scheduling a task and register the task with a target group using this port. This enables you to make efficient use of your clusters.
  - Support for monitoring the health of each service independently, as health checks are defined at the target group level and many CloudWatch metrics are reported at the target group level. Attaching a target group to an Auto Scaling Group enables you to scale each service dynamically based on demand.
  - Access logs contain additional information and are stored in compressed format.
  - Improved load balancer performance.
- You can back up the data on your Amazon EBS volumes to Amazon S3 by taking point-in-time snapshots. Snapshots are incremental backups, which means that only the blocks on the device that have changed after your most recent snapshot are saved. This minimizes the time required to create the snapshot and saves on storage costs by not duplicating data. When you delete a snapshot, only the data unique to that snapshot is removed. Each snapshot contains all of the information that is needed to restore your data (from the moment when the snapshot was taken) to a new EBS volume.
-  In a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone
- AWS recommends that you create Auto Scaling groups from launch templates to ensure that you're accessing the latest features and improvements. If you plan to continue to use launch configurations with Amazon EC2 Auto Scaling, be aware that not all Auto Scaling group features are available. When you edit an Auto Scaling group that has an existing launch configuration, you have the option of replacing the launch configuration with a launch template. This lets you use launch templates with any Auto Scaling groups that you currently use. In doing so, you can take advantage of the versioning and other features of launch templates
- If a subnet is associated with a route table that has a route to an internet gateway, it's known as a public subnet. If a subnet is associated with a route table that does not have a route to an internet gateway, it's known as a private subnet.
- Kinesis data streams – Kinesis data streams is highly customizable and best suited for developers building custom applications or streaming data for specialized needs. However, requires manual scaling and provisioning. Data typically is made available in a stream for 24 hours, but for an additional cost, users can gain data availability for up to seven days.
 
- Kinesis Data Firehose – Firehose handles loading data streams directly into AWS products for processing. Scaling is handled automatically, up to gigabytes per second, and allows for batching, encrypting, and compressing. Firehose also allows for streaming to S3, Elasticsearch Service, or Redshift, where data can be copied for processing through additional services.
- Backup and restore (RPO in hours, RTO in 24 hours or less): Back up your data and applications using point-in-time backups into the DR Region. Restore this data when necessary to recover from a disaster.
 
- Pilot light (RPO in minutes, RTO in hours): Replicate your data from one region to another and provision a copy of your core workload infrastructure. Resources required to support data replication and backup such as databases and object storage are always on. Other elements such as application servers are loaded with application code and configurations, but are switched off and are only used during testing or when Disaster Recovery failover is invoked.
 
- Warm standby (RPO in seconds, RTO in minutes): Maintain a scaled-down but fully functional version of your workload always running in the DR Region. Business-critical systems are fully duplicated and are always on, but with a scaled down fleet. When the time comes for recovery, the system is scaled up quickly to handle the production load. The more scaled-up the Warm Standby is, the lower RTO and control plane reliance will be. When scaled up to full scale this is known as a Hot Standby.
 
- Multi-region (multi-site) active-active (RPO near zero, RTO potentially zero): Your workload is deployed to, and actively serving traffic from, multiple AWS Regions. This strategy requires you to synchronize data across Regions. Possible conflicts caused by writes to the same record in two different regional replicas must be avoided or handled. Data replication is useful for data synchronization and will protect you against some types of disaster, but it will not protect you against data corruption or destruction unless your solution also includes options for point-in-time recovery. Use services like Amazon Route 53 or AWS Global Accelerator to route your user traffic to where your workload is healthy. For more details on AWS services you can use for active-active architectures see the AWS Regions section of Use Fault Isolation to Protect Your Workload.
- Distributed Denial of Service (DDoS) attacks risk shutting out legitimate traffic and lowering availability for your users. 
- AWS Shield provides automatic protection against these attacks at no extra cost for AWS service endpoints on your workload.
 
- your VPC includes a default security group. You can't delete this group, however, you can change the group's rules. The procedure is the same as modifying any other security group. For more information, see Adding, removing, and updating rules.
- AWS Personal Health Dashboard provides alerts and remediation guidance when AWS is experiencing events that may impact you. While the Service Health Dashboard displays the general status of AWS services, Personal Health Dashboard gives you a personalized view of the performance and availability of the AWS services underlying your AWS resources. The dashboard displays relevant and timely information to help you manage events in progress, and provides proactive notification to help you plan for scheduled activities. With Personal Health Dashboard, alerts are triggered by changes in the health of AWS resources, giving you event visibility and guidance to help quickly diagnose and resolve issues