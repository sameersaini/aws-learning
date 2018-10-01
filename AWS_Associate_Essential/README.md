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


### Exercise 11:

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