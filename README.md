# AWS_ccp

## AWS Global Infrastructure
- AZ (Availability Zones): One or more discrete data centers
- GR(Geographic Regions): Physical location in the world with multiple AZs
- EL (Edge Location): A datacenter owned by a trusted AWS partner and has a **direct connection** to the AWS network
    - Used for getting or uploading data fast to AWS
    - These locations serve requests for `CloudFront` and `Route53`
        - Requests going to either of these services will be routed to the nearest EL automatically
    - `S3 Transfer Acceleration` traffic and `API Gateway` endpoint traffic also use the AWS Edge Network
    - Allow for low latency, no matter where the end user is geographically located
- GCR (GovCloud Regions): Allow customers to host sensitive Controlled Unclassified Information and other types of regulated workloads
    - Only accessible to US entities and root account holders who pass a screening process
    - For government, classified data

## Pricing
- On-Demand
> - low cost and flexible
> - pay per hour
> - Ideal for workload that cannot be interrupted
> - **short-term, unpredictable workload, first time development**
> - no upfront payment and no long-term contract
- Reserved Instances
> - ** Steady state or predictable usage **
> - Can resell unused reserved instances
> -  Class
>> - Standard: 75% reduced, cannot change RI attributes
>> - Convertible: 54% reduced, can change RI attributes
>> - Scheduled: reserve instances for specific time periods, e.g. once a week for a few hours
- Spot Instances (BIGGEST SAVINGS)
> - Designed for applications that have flexible start and end times or applications that are only feasible at very low compute costs
> - For those can handle interruptions, and those non-critical background jobs.
> - might be terminated by AWS
- Dedicated Host Instances (MOST EXPENSIVE)
> - dedicated server
> - For those who need a guarantee of isolate hardware

## AWS Support Plans
- Basic
> - Email support for Billing and Account
> - 7 trusted advisor checks
- Developer
>> - Tech support via email
>> - General Guidance
>> - System Impaired < 12 hrs
- Business
>>> - Tech Support via Chat, Phone
>>> - Production System Impaired < 4 hrs
>>> - Production System Down < 1 hr
>>> - All Trusted Advisor checks
>>> - Third party support
- Enterprise
>>>> - Business-Critical System Down < 15 min
>>>> - Personal Concierge, TAM

## Network
- [AWS account[Region[VPC[AZ[Subnet.public[EC2],Subnet.privat[RDS DB]]]]]]
- `VPC (Virtual Private Cloud)`: A logically isolated section of the AWS Cloud where you can launch AWS resources
- `NACLs (Network Access Control List)`: Firewalls at the subnet level
- `Subnets`: A logical partition of an IP network into multiple, smaller network segments
## DB
- Dynamo DB: NoSQL k-v DB
- RDS: MySQL,Postgres... SQL
- Aurora: MySQL and PSQL DB fully managed, also provide serverless (lambda)
    - serverless: Good for development or infrequently used apps
    - Aurora is highly available and durable, and when you have a cluster, it will run 6 copies of the DB across 3 AZs (more expensive than RDS)
- Redshift: Columnar DB, petabyte data warehouse
- ElastiCache: Redis
### Buzz Words
- `Amazon Machine Image (AMI)`
    - Snapshot or copy of the entire server
    - In EC2 > Instances, do Actions > Image > Create Image
    - Once we have an AMI, we can launch another copy of this server/instance

- `CloudFront`
    - Used as a CDN (content distribution network)
    - Can share static files across the globe by copying them to multiple edge locations across the world and will be accessible from those ELs
    - Traffic will hit the domain name, and then it will route the traffic to the nearest EL


- `AWS Marketplace`
    - A curated digital catalog with thousands of software listings from independent software vendors
    - Easy to find, buy, test, and deploy software that already runs on AWS
- `AWS Cost Explorer`
    -  lets you visualize, understand, and manage your AWS costs and usage over time
    - If you have multiple AWS accounts within an AWS Organization, costs will be consolidated in the master account
    - Default Reports give insight into cost drivers and usage trends
    - Use forecasting to get an idea of future costs
    - You can view data at a monthly or daily level of granularity
    - Use filter and grouping functionalities to dig even deeper into your data
- `AWS Budgets`
    - Plan your service usage, service costs, and Instance reservations, and give the user the ability to setup alerts if you exceed or about to exceed the defined budget
    - Create budgets for
        - Cost - dollar amount
        - Usage - e.g. EC2 running hours
        - Reservation - for Reserved Instances
    - Tracked monthly, quarterly, or yearly, with customizable start and end dates
    - Support `EC2`, `RDS`, `Redshift`, and `ElastiCache` reservations
- `AWS Cost and Usage Report`
    - Generates a detailed spreadsheet that enables you to better analyze and understand your AWS costs
    - Use `Athena` to turn the report into a queryable database
    - Use `QuickSight` to visualize your billing data as **graphs**

- `TCO(Total Cost of Ownership) Calculator`
    -  to estimate how much you would save when moving from on-premise to AWS
- `AWS Landing Zone`
    - Helps enterprises quickly set up a secure, AWS multi-account
    - Provides a baseline environment to get started with a multi-account architecture
- `AWS Quick Starts`
    - Prebuilt templates by AWS and AWS Partners that help to deploy popular stacks on AWS
>> 1. A reference architecture for the deployment
>> 2. `AWS CloudFormation` templates that automate and configure the deployment
>> 3. A deployment guide that explains the architecture and implementation in detail

## Provisioning Services
- `AWS Elastic Beanstalk`: Service for deploying and scaling web apps and services developed with Java, .NET, PHP, Node, Python, Ruby, Go, Docker. Similar to Heroku, Netlify

- `AWS OpsWorks`: Configuration management service that provides managed instances of Chef and Puppet(Chef and Puppet programmatically set up a server).
    -  has layers for infrastructure
- `AWS CloudFormation`: infrastructure as code, JSON or YAML
    - Create a JSON or YAML file that defines all AWS Resources and how you want to configure them, and will set up everything that you want in one go
    - For flexibility
- `AWS QuickStart`: Pre-made packages that can launch and configure your AWS compute, network, storage, and other services required to deploy a workload on AWS

## Computing Services
- `EC2 (Elastic Compute Cloud)`:Highly configurable server in terms of CPU, Memory, Network, OS
- `ECS (Elastic Container Service)`: Docker as a Service - highly scalable, high-performance container orchestration service that supports Docker containers, pay for EC2 instances
- `AWS Fargate` : Microservices with which you don't have to think about infrastructure
    - Pay per task (runtime and CPU utilized when running)
    - You don’t choose EC2 instances, just define containers within a task or service, and AWS will run it
- `EKS`: Kubernetes as a Service - easy to deploy, manage, and scale containerized applications using Kubernetes
- `Lambda `:Serverless functions run code without provisioning or managing servers
- `Elastic Beanstalk`:Orchestrates various AWS services, including EC2, S3, Simple Notification Service (SNS), CloudWatch, autoscaling, and Elastic Load Balancers (ELBs)

## Storage Services
- `S3 (Simple Storage Service)`: Object storage
- `S3 Glacier`: For archiving and long-term backup
- `Storage Gateway`:Hybrid cloud storage with local caching, as an extension of on-premise storage in the cloud
- `EBS (Elastic Block Storage)` :Hard drive in the cloud you attach to EC2 instances
- `Snowball`:Physically migrate lots of data via a computer suitcase 50-80 TB

## Business Centric Services
- `AWS WorkSpaces`: Virtual, remote desktop
- `SES (Simple Email Service)`:
    - Cloud-based email for developers
    - For when you are building an app and want to send out emails FROM that application
    - Supports HTML emails
    - SNS can also send emails, but only plain text
- `QuickSight` : Connect data from S3, Aurora, RDS to create graph from this data.
- `Direct Connect` : Low latenycy, dedicated connection to AWS.

## Logging Services
- `CloudTrail`: Log all API calls between AWS Services 
- `CloudWatch Logs`: performance data
- `CloudWatch metrics`: time-ordered set of data points. A variable to monitor.
- `CloudWatch Events`: trigger an event based on a condition
- `CloudWatch Dashboard`: create visualization based on metrics

## Web
- `AWS WAF (Web Application Firewalls)`: Protect your web application from common web exploits. Has to be attached to either `CLOUDFRONT`  -> `S3 Static Website Hosting`or `APPLICATION LOAD BALANCER (ALB)` -> `EC2 Instances`
- `AWS Shield`: A managed DDoS protection services.
    - When you route your traffic through `Route53` or `CloudFront` you are using `AWS Shield Standard`
- `Amazon Route 53`: an AWS managed Domain Name System (DNS) web service
## Security
- `AWS Security - Guard Duty`: a **threat detection service** that uses machine learning to analyze: `CloudTrail` logs, `VPC` Flow logs, `DNS` logs

- `Key Management Service (KMS)`: To create and control encryption keys to encrypt your data ( Envelope Encryption)
    -  Envelope Encryption: when you encrypt your data, your data is protected, but you have to protect your data/encryption key. When you encrypt your data key with a master key, you have an additional layer of security

- `Amazon Macie` : a fully managed service that continuously monitors S3 data access activity for anomalies, and generates detailed alerts when it detects risk of unauthorized access or inadvertent data leaks. 
- `NACLs (Network Access Control List)`: Firewalls at the subnet level
- `Security Groups` : Firewalls at the instance level

## Cloud Service Variation Study Cloud* Service
- `CloudFormation` - infrastructure as code, sets up services via templating script via JSON
and YML
- `CloudTrail` - who you can blame - logs all API calls between AWS Services
- `CloudFront` - Content Distribution Network (CDN) creates a cached copy of your website and copies to servers located near people trying to download the website
- `CloudWatch` - a collection of services
    - `CloudWatch logs`:Any custom log data, Memory Usage, Rails Logs, Nginx Logs
    - `CloudWatch Metrics`:Metrics based off of logs, i.e. Memory Usage
    - `CloudWatch Events`:Trigger an event based on a condition, i.e. every hour take a snapshot of the server
    - `CloudWatch Alarms`:Triggers notifications based on metrics
    - `CloudWatch Dashboard`:Create visualizations based on metrics 
    - `CloudSearch`:Search engine for when you have an ecommerce website and you want a search bar

## Connect Service Variation Study
- ` Direct Connect`: Connections from DataCenter to AWS
- `Amazon Connect`: Call center service
- `Media Connect`: New version of Elastic Transcoder, Converts Videos to different Video Types

## connect apps via Messages
- SNS (Simple Notification Service)
    - Passes along messages using PubSub (Publisher - Subscriber)
    - Send notifications to subscribers on topics via HTTP, email, SQS, SMS
    - Used for plain text emails (cannot do HTML emails), ex. Billing alarms
    - **TOPICS** and **SUBSCRIPTIONS** REGARDING SNS!!!
- SQS (Simple Queue Service)
    - Queue up messages, guaranteed delivery
    - Places messages into a queue - applications pull queue using the AWS SDK (Software Development Kit)
    - Retains message up to 14 days
    - Sends messages in sequential order
    - Ensure only one message is sent
    - Ensure messages are delivered at least ONCE
    - Good for delayed tasks, i.e. queueing up emails

## security tools to perform audits
- Amazon Inspector : Audits a SINGLE EC2 instance
- Trusted Advisor : Gives a holistic view of recommendations across multiple services and best
practices