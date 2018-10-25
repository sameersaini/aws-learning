# Section 5: AWS Certified SysOps Administrator Associate

## Troubleshooting EC2

1. EC2 Fails to Launch:
    1. Service limit reached. Check limits
    2. EBS volume limit reached
    3. Corrupt EBS snapshots
    4. Insufficient instance capacity i.e. capacity mismatch
    5. Account issues like non payment of bills.
    6. Can be troubleshooted using State Transition Reason in instance description.
2. Failed Status Checks:
    1. Due to memory issues, problem with I/O device, kernel issues etc.
    2. Wait for it to resolve itself.
    3. View the system log for the instance.
    4. Can create instance recovery alarm in CloudWatch
3. Fails to terminate/stop
    1. Problem with the underlying computer.
    2. In autoscaling, min number of instances are maintained. So, if u terminate one, a new is launched.
    3. To stop, use force stop command from CLI.
    4. Contact AWS Support and they will stop it.
4. Fails to Connect:
    1. Instance may be overloaded
    2. VPC setup may be wrong.
    3. Key may be wrong.
    4. ICMP should be on for ping to work
    5. For Windows, check for firewall settings.

#### Exercise 29: Perform various actions for troubleshooting EC2 instances

1. Check limits on the EC2 instances
2. Launch an instance.
3. Check Logs on the instance
4. Check Security check statuses
5. Set a CloudWatch alarm to restart the instance whenever any status check fails for 2 consecutive times.


## Troubleshooting RDS

1. <b>Failing to Connect</b>
    1. Wrong security group settings.
    2. Wrong password used.
    3. Local firewall restrictions.
    4. Test connection using netCat or telnet command.
2. <b>Causes of Service outage</b>
    1. Instance may have rebooted
    2. Setting changed that requires a reboot immediately.
    3. Storage may be full.
    4. SET apply immediately to false.
    5. Set a cloud watch alarm using FreeStorageSpace metric.
3. <b>Causes of Read Replica Outage</b>
    1. Storage Class may be lower than he master DB.
    2. High write rate causes cache refresh.
    3. Monitor ReplicaLag in CloudWatch.
    4. Use same instance/storage for master and slave.
    5. Disable query cache for write intensive task.

#### Exercise 30: Perform various actions for troubleshooting RDS instances

1. Create a RDS instance
2. Check recent events of the instance
3. View error_log for any errors
4. Connect to the instance using Telnet
5. Create a Read Replica of the instance and check the replication lag. It should be 0
6. Create a read/write parameter group and attach it to replica and schedule to apply this in next maintenance window.
7. This will help us to bulk write the replica in case of a high replica lag.
8. When lag has been reduced to a satisfying number, then again change the parameter group to default parameter group.


## Monitoring EC2 & ELB

1. <b>Standard CloudWatch Metrics</b>:
    1. T2 CPU Credit such as CPUCreditUsage and CPUCreditBalance
    2. Metrics can be on cpu utilisation, disk IO and network IO.
    3. Detailed monitoring can be enabled.
2. <b>Custom Metrics</b>:
    1. Can be created and published to cloud watch.
    2. Resolution can be 1 min or 1 sec.
    3. Perl Monitoring script can be used to collect memory, disk and cpu utilisation data.
    4. Aggregation can be used such as min, max, sum, average, and percentile.
3. <b>EC2 CloudWatch Alarm Actions</b>:
    1. Can be used to reboot, stop or terminate instances based on the alarms
    2. Can be created using EC2 or CloudWatch console.
    3. Use case can be stopping an idle instance.
    4. Reboot an instance having a lot of memory leaks.
    5. Terminate when a batch job has finished.
4. <b>ELB monitoring</b>:
    1. ELB sends the CloudWatch metric data every 60 secs.
    2. ELB publishes a log file to S3 every 5 to 60 secs which has the access logs.
    3. Application ELB provides a tracking feature to track HTTP reqs from clients to targets or other services.
    4. Adds/updates a header to the HTTP req.
    5. AWS CloudTrail can be used to monitor the api calls. 



#### Exercise 31: Implement EC2 monitoring scripts.

1. Create a IAM policy that to allow put, get list on CloudWatch metrics.
2. Attach that policy to a EC2 IAM role.
3. Create an EC2 instance and attach the newly created role to it and add run scripts to install perl.
4. SSH the EC2 instance and run the required perl scripts to send the metrics data to CloudWatch.
5. Add a cron job to send metrics data to CloudWatch every 60 secs.
6. Check the monitoring data in CloudWatch.

## Monitoring RDS:
1. Monitoring Options:
    1. CloudWatch Alarms, Logs or Events.
    2. Enhanced Monitoring - provide OS metrics. Only present in RDS service.
    3. RDS Events 
    4. Database log files.
    5. Amazon performance insights.
    6. Monitor CloudTrail logs 
2. Enhanced Monitoring
    1. Provides real time OS metrics.
    2. Can be views in the console or CloudWatch Logs.
    3. Not available for t1.micro or m1.small
    4. Cost varies on the instance size.
3. RDS Events:
    1. Can be used to trigger SNS notification service.
    2. Multiple event types such as backup, creation, deletion, low storage, high load etc.
    3. Can be viewed using CLI, SDK/API, RDS Console.
4. DB Log files: 
    1. Type of log files available depends on the type of DB engine used.
    2. Transaction logs not supported. Only general logs.

#### Exercise 32: Monitoring RDS.
1. Launch a RDS instance.
2. Monitor CloudWatch metrics.
3. Monitor Enhanced metrics.
4. Monitor OS events.
5. Monitor DB logs.





