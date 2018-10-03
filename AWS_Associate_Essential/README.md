# Section 2: AWS Certified Associate Essentials 

## EC2 and ECS:

1. E22 cloud offers many variations such as general purpose, memory optimised, storage optimised, compute optimised etc.
2. EC2 offers windows and linux AMIs.
3. ECS is a container service for dockers containers. User can create an independent pipeline as: push code to git -> create a docker container -> push to Elastic container registry -> ECS then set ups container registries.

#### Exercise 10:
1. Setup a linux instance and allow traffic on port 80.
2. Connect to the instance using SSH.
3. Set up a nodeJs app on it.
4. Start the server.

## Elastic Block Storage:

1. EBS can be attached to a single EC2 instance as a block of storage which can be a magnetic storage or SSD.
2. User needs to select the size of the block storage to be attached to the EC2 machine.
3. EBS can be selected to terminate on EC2 termination or can be selected to persist on EC2 termination.
4. EBS can be snapshotted but cannot be moved from one region to another.
5. EBS snapshots can be used to attach volume to EC2.

## Elastic File Storage:

1. EFS is a network attached storage which can be accessed by multiple EC2 machines within multiple availability zones in the same region.
2. EFS is an auto scaled storage and user can use as much he wants to use.
3. To access EFS, a mount point has to be created in the subnet in the availability zone. i.e. The subnet in which EC2 machine exists should have a mount point associated with it to connect to EFS.
4. The mount points are created in the EFS panel.
5. After this, EFS has to be mounted to the file system on the EC2 machine using mount command. After this, the EFS is available to be accessed on the EC2 machine.

## Simple Storage Service (S3):

1. It is a web store/object store not a file system. Stores objects not files.
2. The object(file/folder) name prefix are used for partitioning. So, the way names are structured does affect the performance. So, it is advised to have unique name prefixes. 
3. 4 types:
    1. Standard: replication in multi AZs, support lifecycle methods. Unlimited storage. Data availability is 99.99999999%
    2. Standard IA: Same as Standard but low per GB storage cost, has per GB access cost. Data availability is 99.99999999%
    3. Standard IA - One Zone: same as Standard IA but only in one zone so lower per GB storage cost than Standard IA. Data availability is 99.5%
    4. Reduced Redundancy: Being depreciated by AWS Data availability is 99.9%
4. Access Control lists can be used to control access to files. 
5. Bucket policies can be used to control how data is accessed in the buckets.
6. AWS Policy creator can be used to create policies.

## CloudFront:

1. AWS cloudFront caches the content to over 100+ edge location around the world for faster content delivery.
2. Requires an origin server from which the content is to be cached.
3. Origin server can be a S3 bucket or a HTTP server.
4. CloudFront needs to have access to the origin server to perform the caching.
5. It has a default TTL to perform recaching. User can manually change TTL or create cache invalidation to perform manual recaching.
6. CloudFront checks the cache to server the requested file. If the file is not found in the cache at edge locations then it is fetched from origin server and cached at the edge locations.
7. So, when a new file is uploaded, then we do not need to run invalidation. That file will be auto cached even before TTL.
8. Based on the deployment requirements, we can set manual low TTL or run manual invalidations.


## RDS:
1. AWS provides relational database service which supports a number of SQL engines such as mysql, AWS aurora, postgre SQL, Microsoft SQL etc
2. RDS offers manual DB backups.
3. Automated backups are also there. User can setup the frequency.
4. Backups can be encrypted.
5. Multi AZs can be used for master-slave architecture. 
6. It also offers failure in which if master goes down then slave becomes the master and a new instance is launched as a slave in a different AZ.
7. It also offers multiple read replicas for Aurora, PostgreSql, MySql, MariaDB. Max 15 read replicas for Aurora. 
8. Multiple read replicas cannot be put behind AWS ELB. Need to use Route 53 for each read replicas and use a routing policy or third party ELB such as HaProxy.


#### Exercise 11:

1. Create a MySql instance as a source and a PostgreSql instance as a target in RDS.
2. Create database, tables and data in source instance.
3. Create DB endpoints in database migration service.
4. Create Replication instance in database migration service and register DB endpoints created in the 3rd step.
5. Create a migration task in database migration service and specify the source database and tables to migrate.


## Amazon Dynamo DB:

1. Managed NoSql service which stores data in JSON-like format. Consists of Tables, Items & Attributes. Optimised for Speed.
2. Supports primary and secondary indexes.
3. Supports cross-region replication. 
4. Primary key can be a partition(hash) or partition and sort (hash and range).
5. There can be max of 5 global secondary indexes and 5 local secondary indexes.
6. Global Secondary index: Partition and Sort key are different than the primary key.
7. Local Secondary index: Partition key is same as primary key, but Sort key is different from the primary key.
8. 2 ways to search: 
    1. Query: on a index. Fast
    2. Scan is a full table/key scan. Slower. ConsistentRead set to true return results at the time of scan start.
9. Updates:
    1. Atomic Counter: every update increments or decrements the value of an attribute. Good for non-critical counter apps like site counter. Counter increments each time whether or not the call was successful.
    2. Conditional Update: used for critical application. User can request the value of attribute after or before the update.
10. Read Capacity: one read capacity unit represents one strongly consistent read per second or two eventually consistent read per second for 4KB of Item.
11. Write capacity: one write capacity unit represents one write per second for 1 KB of item.
12. Streams: Ordered flow of information about changes to Dynamo DB. 
    1. Created when items are created, updated or deleted in the table
    2. Assigned a sequence number
    3. Stream Records are organised in groups called shards.
    4. Stream records with in a shard are deleted every 24 hours.
    5. Can be used to trigger a AWS Lambda function which can the be used to send mail, save data in S3 etc etc.

## AWS Virtual Private Cloud:

1. When a new account is created AWS creates a default VPC which spans each availability zone. 
2. By default a VPC contains a subnet per availability zone, one internet gateway and one route table entry for the internet gateway.
3. Following is the by default operation:
    1. Each subnet needs to be connected to the internet gateway to be publicly visible on the internet. A entry of the internet gateway is required in route table and then the route is associated to the individual subnet in the subnet settings.
4. Inside a subnet, Security groups provides level 1 security and define which ports of the instances are open and which IPs can connect to the EC2 instances. Security  groups are stateful i.e. they remember that return traffic is automatically allowed.
5. Network ACL/NACL inside a VPC provide level 2 security of data going in/out of the subnet. They are stateless. So, both inbound and outbound rules are required to be specified.
6. Default VPC is assigned a CIDR of 172.16.0.0/16. VPC can be between /28 and /16. Min is /28 i.e. 14 usable addresses.
7. To change the size of a VPC, it must be terminated and recreated.
8. 2 ways of connecting to a VPC:
    1. Internet Gateway: Entry is required in routing table for a default internet gateway. Provides NAT for public IP addresses.
    2. Virtual Private Gateway: VPG is at AWS end. User/client needs a physical device or a VPN software to connect. Each vpn connection has 2 vpn tunnels ie.e 2 public IP addresses to connect.
9. Route Table: Automatically created at creation of a vpn and is associated to all the subnets unless another route table is explicitly connected to a subnet.
    1. Has an entry of internet gate that allows the instances inside a subnet to connect to the internet/publicly via internet gateway.
    2. Custom route table is also automatically created when a vpn is create using the vpn wizard.
    3. A subnet is public if the associated route table has a entry of the internet gateway, else its private. Ex: RDS DB may have only private subnet and instances in the vpn can only connect privately to it.
    4. Private subnet can connect to internet using a NAT gateway or a NAT instance. For ex: a RDS in private subnet may need to connect to internet for downloading updates.
10. VPC Security:
    1. Security groups: These are at instance level and is applied only to an instance is attached to. Level 1 of security. These are stateful. If there are more than one rule for a port number then the most permissive rule is applied.
    2. NACL: :level 2 security of data going in/out of the subnet and thus are auto applied to all the instances in the subnet.. They are stateless. So, both inbound and outbound rules are required to be specified. Rules are processed in order and then most restrictive rule is applied. 

#### Exercise 12:
1. Create a custom VPC with a public and a private subnet.
2. Launch a EC2 instance in the public subnet.
3. Connect to the EC2 instance.
4. Remove the default gateway from the route table associated to the public IP.
5. Try to connect to the EC2 instance. Connection won’t succeed.

## AWS Simple Queue Service SQS:

1. Used for queing messages.
2. Act as a buffer of data for processing servers and helps to decouple applications from demand and smooths out the peak demand.
3. Upto 10 attributes can be added in addition to message body.
4. Message size can be from 1KB to 256 KB.
5. A cloud watch alarm can be set to monitor the size of the queue and the alarm can be used to send message to auto scaling group to increase/decrease the number of processing servers when the demand is high or when the demand is low.
6. 2 types:
    1. Standard: Default queue type. Unlimited transactions per second and guarantees that message will be delivered but there can be duplicate messages.
    2. FIFO: 300 transactions per second. No duplicates and proper FIFO ordering. Not available in all regions.
7. Message LifeCycle: 
    1. Message received by SQS.
    2. Message delivered to processing server. Visibility timeout period starts.
    3. Message processed by processing server. Visibility timeout period ends and the message is deleted from the queue.
8. Visibility timeout period is the time duration for which the message is invisible in the queue and therefore, is not delivered to the processing server again or to other processing servers for processing.
9. If the message is not deleted by the time visibility timeout period ends, the message again becomes visible and can be received again by the processing server.
10. Dead Letter queues: To store messaged which were not processed successfully for analysing them later. Must be in the same region and same AWS account.
11. Delay queue: Message delivery is delayed by a pre defined time period, which is configurable. 120,000 message is the max message per queue.
12. Message Timers: Invisibility time period for the messages in the queue and cab be changed manually.
13. Short Polling: SQS sends response to processing server even if no messages are in the queue. These are empty responses.
14. Long Polling: SQS sends waits to send response to processing server until a message is there in the queue. This helps in saving empty responses.
15. Response wait time can be configured to be between 1 to 20 secs.
 
## Simple Notification Service:

1. Used for sending notifications for mobile/web clients. Notifications can be push notifications or emails.
2. Clients can be HTTP/HTTPs web client, Email client, SQS queue(only standard queue), Lambda functions, SMS or mobile push notifications.
3. Messages can be 256 KB in size. 
4. Topic names are unique and subscribers/clients listen to those topic names.
5. Transport protocols can be HTTP, HTTPS, Email-JSON, SQS


## Simple Workflow Service:

1. Helps implement complex business processes by coordinating work across distributed application components. 
2. Processes can be long running processes.
3. Tasks are executed with no duplicates.
4. It provides routing and queuing of tasks.
5. Workflows can have child workflows.
6. <b>Components</b>:
    1. Workflow - It is the control flow logic i.e. the business process
    2. Domain - It contains a single workflow or more than one workflow.
    3. Tasks - The actual work to be performed in the workflow. This can be done by code, a web service etc. Tasks make up the workflow.
    4. Actors - Interact directly with SWF to coordinate with Tasks.
        1. Starters - Initiate the execution of workflow.
        2. Decider - Implement workflow logic using activity workers.
        3. Activity workers - Perform actual tasks of workflow.
7. <b>Tasks</b>:
    1. Must be registered using console or using SDK API
    2. There can be a queue of task. Decision and activity tasks have a separate list.
    3. Task routing can be used to assign a task to a particular activity worker.


## Identity and Access Management: 
Full documentation at [click here](http://cdn.backspace.academy/courses/aws-certification/02/100/distilled-02-10.pdf)

#### IAM best practices:
1. Enable MFA and reduce root access.
2. Create an admin group and add IAM users with full privileges to that group, put those users on MFA and look the root account away.
3. Grant least privileges.
4. Create individual users and manage permissions with groups
5. IAM roles for share access and for EC2 instances.
6. Strong password policy, set a password expiration time and rotate the credentials regularly.
7. More conditions can be used for added security.


## Big Data Solutions Core Knowledge:
1. <b>Redshift</b>: 
    1. PetaByte Scale data warehousing Service based on Postgre SQL and can be accessed with standard BI tools.
    2. Data is replicated between nodes on a cluster and is backed to S3 with snapshots.
    3. User initiated snapshots are preserved even on cluster deletion.
    4. Migration: AWS SnowBall is sent to AWS. AWS uploads the data to S3. AWS Data Pipeline then transfers data from S3 to RDS/Redshift/other destination.
2. <b>Elastic Map Reduce</b>:
    1. Fully managed Hadoop service
    2. Provides clusters of Ec2 instances for the EMR jobs which are then deleted on job completion.
    3. Supports Hadoop MapReduce and ApacheSpark.
    4. Storage options: HDFS, EMRFS can access files on S3 
3. <b>Elastic Search</b>:
    1. Fully managed elastic search service.
    2. Suitable for queuing and searching large volumes of data.
    3. Can gather data from S3, Kenesis Streams, dynamoDb, cloud watch, cloud trail etc etc
    4. Not suitable for OTLP and petabyte storages.
4. <b>QuickSight</b>:
    1. BI reporting service uses in memory engine
    2. Cost is 1/10th of the traditional analytical s/w such as tableau.
5. <b>Kinesis</b>:
    1. Used for real time streaming data analytics.
    2. Data can be put into streams using API calls, SDKs, Kinesis Agents etc etc.
    3. Kinesis Client Library can be used to process data which is already in the stream.
    4. Kinesis firehose can capture, load, transform the streaming data into kinesis analytics, AWS S3, AWS Redshift etc etc.
    5. Not suitable for long term data storage.


## AWS API Gateway:

1. A simple, flexible, fully managed pay as u go service that handles all aspects of creating and operating robust APIs for application backends which may be running on AWS EC2/Lambda.
2. Adds a son/swagger type definition to create APIs in the the API Gateway, then deploy the APIs.
3. User can configure the throttling to define the number of hits allowed per second.
4. A simple way to structure is: Route53 -> cloudFront -> API Gateway -> backend/AWS Lambda
5. If it is a simple GET req without query params, then the req is handled by cloudFront, else it is passed to API gateway for further processing.

#### Exercise 13:
1. Create a rest API and host it using API Gateway.
2. Connect the API using a client.

## AWS Cognito:

1. Used to create user pools by providing sign up and sign up capabilities to the apps.
2. Can authenticate uses with third party providers such as FB, google, etc and SAML 2.0 authentication to create federated Identity pools.
3. After authenticating users, it can provide temp crews to the users and provide them with IAM roles which allow the users to access AWS services such as S3.
4. Can handle hundred of millions of users.
5. Can be used in modern server less apps.
6. Sync key store: used as a temporary key value store to sync data between apps and aws.


## AWS CodePipeline:
1. Helps to create a CI/CD pipeline to build->test->deploy apps.
2. Can look for changes in S3, GitHub, and AWS cloudFront.
3. It links to GitHub using a web-hook.
4. User can set up which branch look for.
5. Then it can build, test and deploy apps.


#### Exercise 14:
1. Create a sample node app in AWS beanstalk.
2. Upload the sample code in GitHub.
3. Create a AWS codePipeline and link the GitHub code to the pipeline.
4. Then make changes in the code and push it to GitHub.
5. Code pipeline will auto detect the changes and deploy it to the beanstalk app.