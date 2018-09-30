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