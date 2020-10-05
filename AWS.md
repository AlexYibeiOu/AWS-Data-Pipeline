#AWS

##Introduction & Overview

####Summary

Difference between a region, an Availability Zone (AZ) and an

Edge Location.

- A region is a physical location in the world which consists of two of more

  Availability Zones (AZ’s).

- An AZ is one or more discrete data centers, each with redundant power,

  networking and connectivity, housed in separate facilities.

- Edge Locations are endpoints for AWS which are used for cashing content.

  Typically this consists of CloudFront, Amazon’s Content Delivery Network (CDN)

##IAM

### Overview

#### Key Features

Identity Access Management (IAM) offers the following features

- Centralized control of your AWS account
- Share Access to your AWS account
- Granular Permissions
- Identity Federation (including Active Directory, Facebook, Linkedin etc)
- Multifactor Authentication
- Provide temporary access for users/devices and services where necessary
- Allows you to set up your own password rotation policy
- Integrates with many different AWS services
- Supports PCI DSS Compliance

#### Key Terminology

#####Users
End Users such as people, employees of an organization etc.

#####Groups
A collection of users. Each user in the group will inherit the permissions of the group

#####Policies

Policies are made up of documents, called Policy documents. These documents are in a format called JSON (Java Script Object Notation) and they give permissions as to what a User/Group/Role is able to do.

#####Roles
You create roles and then assign them to AWS Resources.

### IAM operations

#### Root account & creata admin account

1. Activate MFA

2. Create an admin account

   Programatic access

   ​	Access Key Id & Secret Access Key

   ​	Create/Activate/Inactivate access key

   Console access

3. Use groups to assign permissions
4. Apply an IAM password policy
5. Rotate you access keys
6. Account settings : Activate / Inactivate Endpoints
7. Create a Role
   1. Choose the service that will use this role
   2. Attach permissions policies

####Lab2 Create a billing alarm

1. Root user, My account: IAM User and Role Access to Billing Information, set active
2. CloudWatch
   1. Change Region to N. Virginia
   2. Create alarm

###Summary

- IAM is universal. It does not apply to regions at this time.

- The “root account” is simply the account created when first setup your AWS

  account. It has complete Admin access.

- New Users have NO permissions when first created.

- New Users are assigned Access Key ID & Secret Access Keys when first created.

- These are not the same as a password. You cannot use the Access key ID & Secret Access Key to Login in to the console. You can use this to access AWS via the APIs and Command Line, however.

- You only get to view these once. If you lose them, you have to regenerate them. So, save them in a secure location.

- Always setup Multifactor Authentication on your root account.

- You can create and customize your own password rotation policies.

##S3

###Overview

#### The Basics

- S3 is Object-based – i.e. allows you to upload files.
- Filescanbefrom0Bytesto5TB
- There is unlimited storage.
- Files are stored in Buckets.
- S3 is a universal namespace. That is, names must be unique globally.
- https://s3-ap-southeast-2.amazonaws.com/chao-mu-personal- bucket
- When you upload a file to S3, you will receive a HTTP 200 code if the upload was successful.

#### Data Consistency Model

* Read after Write consistency for PUTS of new Objects

* Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)

#### Storage Tiers/Classes

* S3 Standard

* S3 Intelligent-Tiering

* S3 – IA : (Infrequently Accessed)
* S3 One Zone –IA
* Glacier
* Glacier Deep Archive

#### S3 - Charges

* Storage
* Requests
* Storage Management Pricing
* Tags
* Data Transfer Pricing

#### Summary

- S3 is Object-based – i.e. allows you to upload files.

- Filescanbefrom0Bytesto5TB

- There is unlimited storage.

- Files are stored in Buckets.

- S3 is a universal namespace. That is, names must be unique globally.

- When you upload a file to S3, you will receive a HTTP 200 code if the upload was

  successful.

- Read after Write consistency for PUTS of new Objects

- Eventual Consistency for overwrite PUTS and DELETES (can take some time to

  propagate

###S3 operations

####Create a S3 bucket

1. Name and Region
2. Versioning
3. Default encryption
4. Block public access

####Upload file to S3 bucket

1. Manage users
2. Access for other AWS account
3. Manage public permissions
4. Storage class

####Lifecycle management

1. Add lifecycle rule 
2. rule name : folder based
3. Add filter to prefix/tags
4. Choose Version
5. Choose Object creation and Days after creation
6. Configure expiration

###Summary

- Buckets are a universal name space

- Upload an object to S3 receive a HTTP 200 code

- S3, S3-IA, S3 Reduced Redundancy Storage • Encryption

  Client Side Encryption Server Side Encryption

  Server side encryption with Amazon S3 Managed Key (SSE-S3) Server side encryption with KMS (SSE-KMS)
   Server side encryption with Customer Provided Keys (SSE-C)

  Control access to buckets using either a bucket ACL or using Bucket Polices By default buckets are private and all objects stored inside them are private

##EC2

###Overview

#### EC2 Options

- On Demand – allows you to pay a fixed rate by the hour (or by the second) with no commitment.
- Reserved – provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. 1 Year or 3 Year Terms.
- Spot – enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times.
- Dedicated Hosts – Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses.

#### EBS Types

* SSD
   General Purpose SSD –balances price and performance for a wide variety of workloads.
   Provisioned IOPS SSD – Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads.

* Magnetic
   Throughput Optimized HDD – Low cost HDD volume designed for frequently accessed, throughput-intensive workloads.
   Cold HDD –Lowest cost HDD volume designed for less frequently accessed workloads.
   Magnetic – Previous Generation. Can be a boot volume,

###Lab: launch a EC2 instance

**Step 1: launch an instance**

1. Launch Instance

2. Choose an Amazon Machine Image

   Free tier eligible

   Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type - ami-00826d10bbe80c195

   The Amazon Linux AMI is an EBS-backed, AWS-supported image. The default image includes AWS command line tools, Python, Ruby, Perl, and Java. The repositories include Docker, PHP, MySQL, PostgreSQL, and other packages.

   Root device type: ebs 

   Virtualization type: hvm 

   ENA Enabled: Yes

3. Choose an Instance Type

   t2.micro

4. Configure Instance Details (leave default)

   VPC

   subnet

   Auto-assign Public IP

   IAM role

   User data

5. Add Storage (leave default)

6. Add Tags (leave default)

7. Configure Security Group

   Choose existing or create a new Security group name (MySg)

   Add Rule: 

   SSH 

   HTTP 

   HTTPS

8. Select an existing key pair or create a new key pair 

   If creating an new key pair, you have to download the private key file (*.pem file) .

**Step 2: ssh to EC2 in command line.**

1. Open command line, change direction to where the pem file is stored then run below commands.

```shell
sudo su
chmod 400 *.pem
```

2. Copy the Public IP address (Let's use 3.25.98.238 here )of the EC2 instance. 

```shell
ssh ec2-user@3.25.98.238 -i *.pem
```

3. Update EC2 instance.

```shell
[ec2-user@ip-172-31-39-146 /]$ sudo su
[root@ip-172-31-39-146 /]# yum update
```

4. Install httpd

```shell
[root@ip-172-31-39-146 /]# yum install httpd -y
```

5. Create index.html

```shell
[root@ip-172-31-39-146 /]# cd /var/www/html/
[root@ip-172-31-39-146 html]# vi index.html
```

6. Append below html code.

```html
<html><h1>Hellow World!</h1></html>
```

7. Start webserver service

```shell
[root@ip-172-31-39-146 html]# service httpd start
```

8. Open a browser, input the IP address 3.25.98.238, we can see the Hello World! website.

#### Summary

- Termination Protection is turned off by default, you must turn it on.

- On an EBS-backed instance, the default action is for the root EBS volume

  to be deleted when the instance is terminated.

- EBS Root Volume of your DEFAULT AMI’s cannot be encrypted. You can

  also use a third party tool (such as bit locker etc) to encrypt the root volume, or this can be done when creating AMI’s in the AWS console or using the API.

- Additional volumes can be encrypted.

- A Security Group is a virtual Firewall to control traffic to your instances.

- When you firstly launch an instance, it will be associated with one or

  multiple security groups.

- You add rules to each security group to allow traffic to or from the

  instances.

- It is the first line to defense hackers.

###Security groups basics

1. Inbound rules
2. Outbound rules

#### Summary

- All inbound traffic is blocked by default.

- All outbound traffic is allowed.

- Changes to security groups take effect immediately.

- You can have any number of EC2 instances within a security group.

- You can have multiple security groups attached to EC2 instances.

- Security groups are STATEFUL.

  If you create and inbound rule allowing traffic in, that traffic is

  automatically allowed back out again.

- You cannot block specific IP addresses using Security Groups, instead use

  Network Access Control Lists.

###Load balancer theory

#### Application Load Balancer

Application Load Balancers are best suited for load balancing of HTTP and HTTPS traffic. They operate at Layer 7 and are application-aware. They are intelligent, and you can create advanced request routing, sending specified requests to specific web servers.

#### Network Load Balancer

Network Load Balancers are best suited for load balancing of TCP traffic where extreme performance is required. Operating at the connection level (Layer 4), Network Load Balancers are capable of handling millions of requests per second, while maintaining ultra-low latencies.
 Use for extreme performance!

#### Classic Load Balancer

Classic Load Balancers are the legacy Elastic Load Balancers. You can load balance HTTP/HTTPS applications and use Layer 7- specific features, such as X-Forwarded and sticky sessions. You can also use strict Layer load balancing for applications that rely purely on the TCP protocol.

#### X-Forwarded-For Header

There is user with public IP address – 124.12.12.100
 It is sending request to our classic load balancer – 10.0.0.10
 It takes the request and forwards it to our ec2 instance. And our ec2 instance will only see private IP address - 10.0.0.10 but not 124.12.12.100.
 How could ec2 get the public IP address of the request sender?

X-Forwarded-For – 124.12.12.100

#### Summary

- 3 Types of Load Balancers Application Load Balancers Network Load Balancers Classic Load Balancers

- 504 Error means the gateway has timed out. This means that the application not responding within the idle timeout period.

  Trouble shoot the application. Is it the Web Server or Database Server?

- If you need the IPv4 address of your end user, look for the X-Forwarded-For

  header.

###The AWS command line and EC2

1. Input credential.

```shell
aws configure
```

Access Key ID, Secret Access Key, Region, json

2. Login S3 from EC2

```shell
aws s3 ls --region ap-southeast-2
```

3. This way is not safe. Delete credential.

```shell
cd ~
rm .aws
```

4. Teminate instance.

'Change termination protection' Enabled can protect instance terminated by mistake.

###Using IAM roles with EC2

Launch a new EC2 instance with a role enable EC2 instance access to S3.

Or, we can attached this role to the exist instance.

##IAM,S3,EC2 in one graph

![AWS IAM S3 EC2](https://tva1.sinaimg.cn/large/007S8ZIlgy1gjcci6mx1rj30q10hngne.jpg)

##Lambda

### Summary

- Lambda scales out (not up) automatically

- Lambda functions are independent, 1 event = 1 function

- Lambda is serverless

- Lambda functions can trigger other lambda functions, 1 event can = x functions

  if functions trigger other functions.

- Lambda can do things globally, you can use it to back up S3 buckets to other

  S3 buckets etc.

### Lab: create a lambda funciton

1. Function name.

2. Runtime (Python, Java, Node.js, .NET, Ruby, Go)

3. Permissions, execution role (eg: EC2 Full Access)

4. Edit function code.

   ```python
   import json
   import boto3
   
   def lambda_handler(event, context):
       # TODO implement
       ec2 = boto3.client('ec2', region_name=event['region'])
       instances = [event['instance_id']]
       inst = ec2.describe_instances(InstanceIds=[instances[0]])
       state = inst['Reservations'][0]['Instances'][0]['State']['Name']
       print(state)
       if(state == "stopped"):
           ec2.start_instances(InstanceIds=instances)
           print('Started your instances: ' + instances[0])
       else:
           print(instances[0] + ' is already started')
   ```

   

5. Memory 128MB ~ 3008MB (if necessary)

6. Timeout 1sec ~ 15min (if necessary)

7. VPC (if necessary)

8. Create a test event

   ```json
   {
     "instance_id": "i-0dad5e7aa7d6538db",
     "region": "ap-southeast-2"
   }
   ```

9. Deploy

##Database on AWS

###RDS

#### Lab: create a RDS instance

1. Engine options (MySQL) & Version
2. Templactes (Free tier)
3. DB instance identifier
4. Master username & password
5. Storage type (SSD/Magnetic)
6. Network & Security
   1. Security group (inbound rules: Type MYSQL/Aurora, open to your ip, eg: 59.102.47.112/32)
   2. Public accessibility ( Yes )

Workbench create a database connection:

1. hostname: filled with Endpoint
2. Port 3306
3. User & Password

####RDS - Backups

- There are two different types of Backups for AWS: Automated Backups and Database Snapshots.
- Automated Backups allow you to recover your database to any point in time within a “retention period”. The retention period can be between one and 35 days. Automated Backups will take a full daily snapshot and will also store transaction logs throughout the day. When you do a recovery, AWS will first choose the most recent daily back up, and then apply transaction logs relevant to that. This allows you to do a point in time recovery down to a second, within the retention period.

#### Automated Backups

- Automated Backups are enabled by default. The backup data is stored in S3 and you get free storage space equal to the size of your database. So if you have an RDS instance of 10Gb, you will get 10Gb worth of storage.
- Backups are taken within a defined window. During the backup window, storage I/O may be suspended while your data is being backed up and you may experience elevated latency.

#### Snapshots

DB Snapshots are done manually (ie they are user initiated.) They are stored even after you delete the original RDS instance, unlike automated backups.

#### Restoring Backups

Whenever you restore either an Automatic Backup or a manual Snapshot, the restored version of the database will be a new RDS instance with a new DNS endpoint.

#### Encryption

- Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora. Encryption is done using the AWS Key Management Service (KMS) service. Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.
- At the present time, encrypting an existing DB Instance is not supported. To use Amazon RDS encryption for an existing database, you must first create a snapshot, make a copy of that snapshot and encrypt the copy.

#### Multi-AZ

- Multi-AZ allows you to have an exact copy of your production database in another Availability Zone. AWS handles the replication for you, so when your production database is written to, this write will automatically be synchronized to the stand by database.
- In the event of planned database maintenance, DB Instance failure, or an Availability Zone failure, Amazon RDS will automatically failover to the standby so that database operations can resume quickly without administrative intervention.
- Mutil-AZ is for Disaster Recovery only. It is not primarily used for improving performance. For performance improvement, you need Read Replicas.

#### Read replicas

Read replicas allow you to have a read-only copy of your production database. This is achieved by using Asynchronous replication from the primary RDS instance to the read replica. You use read replicas primarily for very read-heavy database workloads.

- Used for scaling, not for Disaster Recovery.

- Must have automatic backups turned on in order to deploy a read replica.

- You can have up to 5 read replica copies of any database.

- You can have read replicas of read replicas (but watch out for latency.)

- Each read replica will have its own DNS end point.

- You can have read replicas that have Multi-AZ.

- You can create read replicas of Multi-AZ source database.

- Read replicas can be promoted to be their own databases. This breaks the

  replication.

- You can have a read replica in a second region.

###DynamoDB

####Overview

Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, at-tech, IoT, and many other applications.

- Stored on SSD storage
- Spread Across 3 geographically distinct data centers.
- Eventual Consistent Reads (Default)
- Strongly Consistent Reads
- Eventual Consistent Reads
   Consistency across all copies of data is usually reached within a second. Repeating a read after a short time should return the updated data. (Best Read Performance.)
- Strongly Consistent Reads
   A strongly consistent read returns a result that reflects all writes that received a successful response prior to the read.

#### Lab: create a DynamoDB table

1. Tabel name 
2. Primary key
3. Read/write capacity mode (Provisioned / On-demand)
4. Provisioned capacity ( Read / Write capacity )
5. Auto Scaling
6. Encryption at Rest 
   1. Default: key own by AWS 
   2. KMS - Customer managed CMK
   3. KMS - AWS managed CMK

###RedShift

###Elasticache

Elasticache is a web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

Elasticache supports two open-source in-memory caching engines:

 • Memcached
 • Redis

https://aws.amazon.com/elasticache/redis-vs-memcached/

###Aurora

### Sumary

1. RDS – OLTP  ( SQL / MySQL / PostgreSQL / Oracle / Aurora / MariaDB )
2. DynamoDB – No SQL
3. Redshift – OLAP
4. Elasticache – In Memory Caching