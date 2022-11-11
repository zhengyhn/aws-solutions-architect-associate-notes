# aws-solutions-architect-associate-notes
My notes when preparing AWS solutions architect associate cert

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
