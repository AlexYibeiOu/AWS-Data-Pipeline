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

1. Launch Instance

2. Choose an Amazon Machine Image

   **Free tier eligible**

   **Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type** - ami-00826d10bbe80c195

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

**Now, we can ssh to EC2 in our command line.**

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

###Lambda