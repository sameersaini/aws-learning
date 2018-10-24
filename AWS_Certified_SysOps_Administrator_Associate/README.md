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














