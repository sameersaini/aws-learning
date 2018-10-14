# Section 4: AWS Certified Architect  Essentials

## Exercise 23: NodeJs Development on EC2

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