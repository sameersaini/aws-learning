## Intro to Storage Services

1. <b>Simple Storage Service</b> : known as S3. To Store any type of data over the internet. User creates a bucket and upload content to that bucket. Its a flat storage. So, bucket names needs to be unique over the entires AWS accounts. 
2. <b>AWS Glacier</b>: Used for long term archiving of data and is much cheaper than S3. Also a server less service. Should only be used for archival. Rule can be set in S3 for auto moving data to Glacier
3. <b>Elastic Block Storage</b>: Used as a block of storage attached to the amazon EC2 server.
4. <b>Elastic File System</b>: It is a network attached storage for EC2 servers. It allows multiple servers to access the same storage.
5. <b>Storage Gateway</b>: Allows to connect on premise storage to AWS cloud. Ex: AWS Storage gateway can be used to transfer in-house data to AWS S3.
6. <b>AWS Snowball</b>: Physical device used to transfer large TB to PB of data from your own data source to AWS cloud. 

##### Exercise 1: working with S3
1. Create a bucket.
2. Create a folder inside a bucket.
3. Upload files to a folder inside a bucket.
4. Download files from a bucket.
5. Delete files from a bucket.
6. Delete a bucket.

## Intro to Database Services

1. <b>Relational Database Service/RDS</b>: Provides fully managed mySql database servers that can be scaled according to the need. Can launch mySql servers or the variations of mysql with mariaDB or amazon’s own mysql service. Microsoft SQL and poster SQL are also available.
2. <b>Dynamo DB</b>: Is is amazon’s own noSQL DB service. Its a serveless service and you don’t have to worry about the underlying infra.
3. <b>Redshift</b>: Fully managed petaByte level data warehouse. Based on postgre Sql engine. It is perfect big data storage solution.
4. <b>ElastiCache</b>: In memory cache service.
5. <b>Database Migration Service</b>: to migrate from one DB engine to another. Ex: oracle -> mysql 
6. <b>Neptune</b>: fast and fully managed graph database service. Very effective graph storage.

##### Exercise 2: 
1. Create a mySql RDS instance.
2. Connect to tha instance using mysql workbench.
3. Create a database in the instance.
4. Connect to same instance using mysql shell.


## Intro to Compute and Networking Services:

1. <b>AWS EC2</b>: elastic compute cloud provides virtual servers in the AWS cloud and it provides a large number of options to choose from and configure servers.
2. <b>AWS EC2 auto scale</b>: allows to dynamically scale EC2 machines. User can Setup load cutoff for when to upgrade and when to downgrade the ec2 machines automatically.
3. <b>AWS lightsail</b>: easiest way to launch virtual servers in the AWS cloud. AWS manages the entire infra
4. <b>Amazon Elastic Container Service</b>: container service for docker containers
5. <b>AWS lambda</b>: It is a server less service that allows you to deploy your code without worrying about the infra. AWS takes care of everything underneath.
6. <b>Amazon Cloud Front</b>: It is a global CDN. Located at around 100 service locations across the world. Caches the most commonly used data for faster delivery.
7. <b>AWS VPC</b>: provides isolated section of AWS cloud which no one else can enter unless the one with the access.
8. <b>Amazon direct connect</b>: high speed dedicated network to AWS cloud.
9. <b>AWS Elastic Load Balancing</b>: automatically distributes the traffic across multiple EC2 machines across multiple availability zones. Auto scale + ELB is very popular.
10. <b>AWS Route 53</b>: highly available and highly scalable domain name system. Can route traffic from domain name to web backend server.
11. <b>AWS API gateway</b>: Its a server less service that lets you manage and deploy secure APIs and lets you control a number of aspects of the APIs. Users can set rules on those APIs like max per min hit limit. 

    NOTE: using amazon Cloud Front in front of (Auto scale + ELB) helps fast access of static content and makes sure dynamic content is also delivered via ELB.
    
##### Exercise 3:
1. Launch a EC2 server using Wordpress AMI by bitnami.
2. Set a public IP
3. Launch the wordpress application.
4. Login as admin console.
5. Terminate the server.

## Intro to management services
1. <b>CloudFormation</b>: Allows user to create a text file to define the infra and use this text file to deploy resources to the AWS cloud.
2. <b>AWS Service catalog</b>: allows companies to catalog resources that can be deployed on the AWS cloud and in turn allow them to comply with the common governance metrics
3. <b>AWS cloud watch</b>: monitoring service for AWS resources and applications and can be used to set alarms for a number of events such as billing alarms.
4. <b>AWS Systems Manager</b>: helps to view operational data from AWS resources and helps user to understand which tasks can be automated.
5. <b>AWS cloudTrail</b>: monitors and logs the AWS account activity which includes CLI operations or the actions taken from the AWS management console.
6. <b>AWS config</b>: allows user to evaluate and set up configuration for the AWS resources which helps to simplify change management, troubleshooting etc.
7. <b>AWS trusted advisor</b>: online expert system to analyse your current AWS resources and set up and give expert advise on how to maximise the potential and throughput of your AWS resources.

##### Exercise 4:
1. Add a billing alarm using cloud watch.

## Intro to Application Services
1. <b>Step Function</b>: define the steps to be followed for application development
2. <b>AWS SWF</b>: Simple Workflow Service: Similar to Step Function. User can define the workflow of the app development
3. <b>SNS</b>: simple pub/sub messaging service. Create a topic-> publish it ->  subscribe-> subscribers receive the notification. Also, used for the sending push messages to mobile devices.
4. <b>SQS</b>: Simple Queue Service. Message Queue service helps to decouple application form demand. Queue holds the request while some other req is currently under processing. Used when demand fluctuations cannot be handle by auto scale + ELB. When the Queue is full/too large, SQS + cloudWatch can be used to send and trigger actions in AWS autoscale to increase the AWS EC2
5. <b>Amazon pinpoint</b>: Allows to send sms, email of push messages for marketing campaigns.
6. <b>Amazon SES</b>: Simple email service is used to send emails/bulk emails to users. To send bulk emails, user needs to request limit increase.


##### Exercise 5:
1. Use SES to send email to a user.

## Intro to Analytics and Machine Learning:
1. <b>Amazon EMR</b>: Elastic Map Reduce is amazon’s Hadoop framework as a service. Also provide other frameworks to work with such as Hbase, Spark.
2. <b>Amazon Athena</b>: allows to analyse data stored in S3 bucket using standard SQL statements.
3. <b>Amazon Elastic Search</b>: fully managed service for elastic.co’s elastic search service, that allows high speed querying and analysis of data stored on AWS.  
4. <b>Amazon Kinesis</b>: allows to collect, process and analyse real time streaming data.
5. <b>Amazon Sagemaker</b>: AWS flagship product that allows to build train and deploy machine learning models. 
6. <b>Amazon Rekognition</b>: can be used for analysis of images and videos.
7. <b>Amazon Lex</b>: can be used for making chatbots for customer interactions.
8. <b>Amazon Poly</b>: text to speech conversion.
9. <b>Amazon Comprehend</b>: use deep learning for text analysis. Can be used to determine customer patterns.
10. <b>Amazon Translate</b>: translates text to other languages.
11. <b>Amazon Transcribe</b>: speech recognition service used for speech to text conversion 

##### Exercise 6:
1. Use Amazon Recognition to analyse images and videos.

## Intro to Security, Identity & Compliance:

1. <b>Artifact</b>: Provides access to AWS security and compliance documentation.
2. <b>Certificate Manager</b>: provides free SSL certs for HTTPS. 
3. <b>AWS cloud directory</b>: multi dimensional hierarchy of data.
4. <b>AWS directory services</b>: fully managed Microsoft active directory service
5. <b>Cloud HSM</b>: dedicated Hardware security module in the AWS cloud. Helps to meet corporate and regulatory compliance at a very low cost.
6. <b>Cognito</b>: provides sign in and sign out capabilities to web apps and also provides integration with google, Facebook and other 3rd party auth providers.
7. <b>IAM</b>: allows to create sub users inside a root account and provide them limited access. Policies can be attached to the users which defines the access the user is having.
8. <b>Amazon Inspector</b>: automated security assessment service that provides the vulnerabilities in the the was account.
9. <b>KMS</b>: key management service: allows to create and manage encryption keys for encryption.
10. <b>AWS shield</b>: provides protection against DDos attack. Standard version is auto applied on all accounts.
11. <b>Amazon WAF</b>: web application fireball: sits in front of web site. Provides protection against common attacks such as SQL injection, cross site scripting. Rules can be set in fireball for different applications.


##### Exercise 7:
1. Create a IAM user
2. Set policies on IAM ser
3. Login with IAM user.


## Intro to Developer Tools:
1. <b>Cloud 9</b>: IDE running in the AWS cloud. Allows to deploy code to AWS directly from IDE.
2. <b>CodeStart</b>: allows to develop and deploy to AWS and can manage the entire CI/CD pipeline. Issue tracking integrated via JIRA.
3. <b>X-Ray</b>: makes it easy to debug the app and provides insights to the app performance.
4. <b>CodeCommit</b>: GIT repository just like GITHUB.
5. <b>CodePipeline</b>: CI/CD service that can test and deploy apps every time a change occurs.
6. <b>CodeBuild</b>: builds, compiles, and tests apps that are ready for deployment. 
7. <b>AWS CodeDeploy</b>: helps in automatic code deployment to AWS EC2 or AWS Lambda.


## Intro to mobile services:

1. <b>AWS mobile hub</b>: creates configuration file for mobile devices regarding the AWS services to be used
2. <b>AWS Device Farm</b>: app testing service. Allows to test apps on large number of mobile devices.
3. <b>AWS AppSync</b>: graphQL backEnd for mobile and web applications.

## Intro to Migration Services:

1. <b>AWS Application Discovery Service</b>: gathers information about enterprises on-premises data centre to help plan migration to AWS
2. <b>AWS Database Migration Service</b>: helps migration of on-premise database to AWS even to a different database engine.
3. <b>AWS Server Migration Service</b>: helps automate migration of thousands of on-premise servers to AWS cloud.
4. <b>AWS SnowBall</b>: refer above in Storage Services.

## Business Productivity and App Streaming:
1. <b>Amazon Workdocs</b>: file management service. View and edit files
2. <b>Amazon WorkMail</b>: fully managed business mail and calendar serve.
3. <b>Amazon Chime</b>: Video conferencing service
4. <b>Amazon WorkSpaces</b>: fully managed desktop as a service for windows desktop.
5. <b>Amazon AppStream</b>: application streaming services. Stream apps from AWS to web browser

## Intro to IOT Services:
1. <b>AWS IOT</b>: managed platform that allows IOT devices to communicate with cloud applications and other devices.
2. <b>AWS FreeRTOS</b>: OS that allows low power and low cost devices to connect to AWS IOT
3. <b>AWS GreenGrass</b>: allows AWS IOT connected devices to run AWS lambda, message caching and machine learning locally.

#### Non lab Exercise:
1. Setup a AWS windows workstation and connect to it.

## Intro To Elastic Beanstalk


1. With Elastic Beanstalk, user can deploy, monitor, and scale an application quickly and easily. 
2. It Let us do the heavy lifting so you can focus on your business.
3. User can specify the number of machines, type of load balancing and auto scaling.
4. User can select the technology to be used for the app.
5. It makes the infra deployment and management very easy.

##### Exercise 8:
1. Create a high availability nodeJs app using Elastic Beanstalk, which uses auto scaling and load balancing.
2. Open it in the Browser.
3. Terminate the app.


## Working with IAM: 
IAM is a web service that enables Amazon Web Services (AWS) customers to manage users and user permissions in AWS.

#### Best Practices for IAM:

1. Lock away your AWS Account  <b>Root User Access Keys</b>.
2. Create Individual   <b>IAM Users</b>
3. Use <b>Groups</b> to Assign permission to IAM Users.
4. Use <b>AWS defined policies</b> whenever possible.
5. Use <b>Access Levels</b> to review permissions.
6. Configure a Strong  <b>Password Policy</b>.
7. Enable  <b>Multi Factor Authentication</b>.
8. Use <b>Roles</b> For Application that run EC2 instances.
9. <b>Rotate Credentials</b> regularly.
10. Remove <b>Obsolete</b> credentials.
11. <b>Monitor</b> activity of your account using AWS CloudTrail.

##### Exercise 9: Working with IAM

1. Create a IAM User.
2. Attach a policy.
3. Create a Role.
4. Attach a Role to the IAM User.
5. Enforce a strong password policy.
7. Create a Role and attach it to EC2 service.
6. Create an alias for the AWS Account.
7. Generate a credentials report.


## Working with EC2: 
EC2 is a service which allows the user to launch virtual servers with a lot of configurable options. Instances can be general purpose, computing optimised, memory optimised, dedicated instances or dedicated h/w instances. To try out EC2, launch an instance, create a per file and login to the server using ssh.
AWS also provides elastic container service where the user first creates docker containers, upload them to amazon elastic registry and then deploy them Elastic container service to EC2 server.

## Working with S3: 
S3 or simple storage service allows users to create buckets and store any kind of data files in those buckets. The bucket names should be unique universally. Files in the buckets can be versioned which helps in retrieving old versions and getting deleted data back. Also, lifecycle method can be set which migrates the data files to archive storage such as amazon glacier after a user defined number of days and can also delete filed permanently after a user defined number of days.

## Working with Databases:  
1. <b>RDS</b>: AWS provides relational database service which supports a number of SQL engines such as mysql, AWS aurora, postgre SQL, Microsoft SQL etc. Make sure to replicate the database across multiple availability zones in order to make sure the database is always available. If Db in one zone goes down then the DB in other zone is used as a backup.
2. <b>Dynamo DB</b>: It is a NoSql database which stores data in form of JSON type documents. It provides user low latency at any scale. User can set primary keys. Secondary key and sort keys.
3. <b>Neptune</b>: It is a graph DB service and is used for applications where relationships are required. Such type of data is difficult to handle in a RDS or a NoSQL service.
4. <b>RedShift</b>: This services provides big data capabilities based on a postgre database and can handle petabyte scales of data. There is a leader node and multiple compute nodes.
5. <b>AWS Elastic Cache</b>: It provides a in memory Storage service based on redis or memcached engine and can be used as a fast access point for most frequently used data in an application.


##Working with VPC: Virtual private Cloud

When a new account is created AWS creates a default VPC for each availability zone. 
By default a VPC contains a subnet per availability zone, one internet gateway and one route table entry for the internet gateway.

<b><i>Following is the by default operation</i></b>:

Each subnet needs to be connected to the internet gateway to be publicly visible on the internet. A entry of the internet gateway is required in route table and then the route is associated to the individual subnet in the subnet settings.

Inside a subnet, <b>Security groups</b> provides <b>level 1</b> security and define which ports of the instances are open and which IPs can connect to the EC2 instances.

<b>Network ACL/NACL</b> inside a VPC provide <b>level 2</b> security of data going in/out of the subnet. They are stateless. So, both inbound and outbound rules are required to be specified.

## Section 2: AWS Certified Associate Essentials 

Elastic cloud compute (EC2) and Elastic Container service: (ECS):

1. E22 cloud offers many variations such as general purpose, memory optimised, storage optimised, compute optimised etc.
2. EC2 offers windows and linux AMIs.
3. ECS is a container service for dockers containers. User can create an independent pipeline as: push code to git -> create a docker container -> push to Elastic container registry -> ECS then set ups container registries.

Exercise 10:
1. Setup a linux instance and allow traffic on port 80.
2. Connect to the instance using SSH.
3. Set up a nodeJs app on it.
4. Start the server.