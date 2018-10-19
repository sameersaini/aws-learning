# Section 4: AWS Certified Architect  Essentials

#### Exercise 23: NodeJs Development on EC2

1. Create a IAM role with administrative access
2. Create a Security group for HTTP, HTTPS, SSH inward traffic.
3. Launch an EC2 instance using the custom nodeJs AMI.
4. Connect to the instance using SSH.
5. Run the nodeJs app on the instance.


## Backup and Recovery 

1. <b>RPO</b> and <b>RTO</b>: 
    1. RPO: Recovery point objective is max age of files that are restored from a backup.
    2. High backup frequency means low rpo
    3. RTO: Recovery time objective: Maximum length of time a system can be down
    4. Glacier takes quite a time to fetch/restore data.
2. Two types of backup are there: Full backup and incremental backup which captures only changes
3. <b>RAID</b>: Redundant array of inexpensive disk
    1. RAID 0: striping of bits, high disk utilisation, and high read performance but no recovery process
    2. RAID 1: mirroring: data is copied, low disk utilisation, and standard disk read performance. Can handle disk failures
4. <b>EC2 backup and recovery</b>: 
    1. AMIs can be snapshotted and saved to S3.
    2. EBS snapshots are incremental and saved to s3. Snapshots can be move to different regions.
    3. Multiple EBS vols are RAID 1.
5. <b>RDS backups</b>: 
    1. Automatic daily backups can be configured.
    2. Retention for auto backup range from 1 to 5 days
    3. Automatic backups are deleted on DB deletion. Can create a final db backup on deletion
    4. Manual db snapshots can also be taken and these are not deleted on db deletion.
    5. Snapshots can be taken via GUI/API/CLI.
6. <b>Dynamo DB</b>: 
    1. No automated backup
    2. Table import/export can be done and log files are saved to S3.
    3. Export can be set up as a daily export.
    4. Table can be imported easily.
7.  <b>S3 and glacier</b>: Lifecycle rules can be set
    1. S3 object deletion after expiry time
    2. S3 object Archiving to glacier after expiry time
    3. Cab be restored from glacier back to S3

## AWS Auto Scaling: 

1. Creates EC2 instances which can scale up or down depending upon the condition set by the user.
2. Enables horizontal scaling, fault tolerance and multi AZ capability.
3. Requires:
    1. Minimum size. example: 1
    2. Maximum size. example: 4
    3. Desired capacity. example: 2
4. Launch configurations can be created to specify the AMI, instance type, security groups and other configurations etc
5. Scaling plans/policy can be used to specify the scaling methods to follow. Schedules can be set up for scaling up/down
6. Uses CloudWatch alarms to determine the scaling.
7. Scaling can be setup to be <b>Change in capacity by x number</b>, <b>Exact change in capacity by x numbers</b> or <b>percentage change in the capacity</b>.
8. Scaling can be :
    1. <b>Simple</b>: single scaling adjustment
        1. Disadvantage: Can be slow on large spikes and can be fast on small spikes. 
    2. <b>Step Scaling</b>: 
        1. Different scaling conditions can be set up for different bands of conditions.
        2. Example: increase capacity by 25 % over desired capacity for cpu utilisation between 25-50% and increase capacity by 100% over desired capacity for cpu utilisation between 50-75% 
        
        
#### Exercise 24: High Availability and Fault Tolerant Architecture

<b>Part One:</b> Setup a VPC containing public and private subnets along with a NAT instance in public subnet
1. Create a new VPC with a public and private subnet in availability zone us-east-1a
2. Select a NAT instance in the Public subnet.
3. Go through and analyse the subnets and their associations with the route tables.
4. NAT instance is a EC2 instance which uses an open security group, so we need to modify its security group.

<b>Part Two:</b> Create a new security group with required rules only.
1. Change the ENI(elastic network interface) settings so that it don’t gets deleted on Instance termination.
2. Terminate the EC2 NAT instance.
3. ENI is not available to be attached to a new instance.
4. Create anew security group with tighter rules.
5. Attach the newly create SG to the ENI.
6. Launch a new EC2 NAT instance using the current ENI and the newly created SG.
7. Now, the newly created VPC will be using a NAT instance with tighter security.

<b>Part Three:</b> Creating Public and Private subnets in a different AZ:
1. Create a public and private subnet in a different AZ us-east-1b
2. By default, the subnets are private. Therefore, associate them with proper route table so that one is public and the other is private.
3. Create two new NACL. One for private subnets and other for public subnets.
4. Add proper inbound and outbound rules for the NACLs.
5. Associate the 2 public subnets with the Public NACL and 2 private subnets with the Private NACL.

<b>Part Four:</b> Creating an ELB and Auto Scaling Group
1. Create a WebServer SG with inbound rules allowing HTPP, HTTPS, SSH from anywhere and all traffic from with the SG. This SG will be used to launch ELB, ASG, and EC2 instances.
2. Go to EC2 dashboard and create a load balancer in the newly created VPC. Add 2 public subnets to the load balancer
3. Select the WebServer SG for the load balancer.
4. Put the health check to TCP: port 80 and create the load balancer.
5. After create, enable sticky sessions to preserve the temp session data with the instance.
6. Go to Launch configuration in the EC2 instance and create a launch configuration of a Wordpress AMI in the newly create WebServer SG.
7. The go to Auto Scaling Group and use the launch configuration to launch minimum of 2 instances in the 2 public subnets created in part one and two.
8. Select the load balancer created in the previous steps for health checks.
9. Use the auto scaling policies of increase and decrease according to you need.
10. Two instances will be launch in 2 different AZ. And if you terminate any one of then, one more will be launched after the cool down period to maintain a min of 2 instances.


<b>Part Five:</b> Adding a Multi AZ RDS instance and Read replica
1. Create a security group for RDS DB.
2. Add a inbound rule for web server security group so that instances in that group can connect to database
3. Add outbound rule to web server security group so that that requests can be made from within web server SG to the db SG.
4. Create a RED DB subnet to accept traffic from with the subnets
5. Launch a production grade RDS instance into the new VPC that we are working with. Do not create public end-points.
6. Create a read replica replica in a different AZ.

#### Exercise 25: Application Load Balancers

1. Launch a Magento AMI app instance.
2. Launch a Wordpress AMI app instance.
3. Launch a target group for each of the instances and add these instances to the target group.
4. Got to Load balancers page and create a new load balancer. Select application load balancer.
5. Select the by default target group to be Wordpress and create the load balancer.
6. After create. Edit the target rules to include magento target group on /store and /store/*.
7. Save the rules.
8. Now, by default the load balancer will direct traffic to Wordpress app in Wordpress target group and to magento app in magento target group when /store or /store/* hit is received.

#### Exercise 26: Network Load Balancers

1. Create a Target group for TCP on port 80.
2. Create a launch configuration of Wordpress app.
3. Use the launch configuration to create an auto scaling group and set the traffic to ELB and use the target group just created.
4. Create a Network load balancer and attach the target group to it.
5. Clean the Environment.