
# RDS Cluster Backup Setup

```bash
aws rds describe-db-clusters \
--query 'DBClusters[*].[DBClusterIdentifier,EarliestRestorableTime,LatestRestorableTime,BackupRetentionPeriod,PreferredBackupWindow]' \
--output text
```

# Recent RDS Cluster Snapshots

```bash
aws rds describe-db-cluster-snapshots \
   --snapshot-type automated \
   --query 'DBClusterSnapshots[*].[SnapshotCreateTime,DBClusterIdentifier]' \
   --output text | sort -r | head
```

# ASGs with only 1 AZ but have more than one instance
``` bash
aws autoscaling describe-auto-scaling-groups --query 'AutoScalingGroups[?AvailabilityZones.length(@) < `3` && Instances.length(@) > `1`].{ASG:AutoScalingGroupName,DesiredCapacity:DesiredCapacity,CurrentNumInstances:Instances.length(@),NumberOfAZs:AvailabilityZones.length(@),AZs:AvailabilityZones}' > asgs-with-two-or-more-instances-but-only-one-az.json 
```

# ASGs with zero instances
``` bash
aws autoscaling describe-auto-scaling-groups \
--query 'AutoScalingGroups[?Instances.length(@) == `0`].[AutoScalingGroupName]' \
--output text
```

# ASGs by date created
``` bash
aws autoscaling describe-auto-scaling-groups \
--query 'AutoScalingGroups[*].[CreatedTime,AutoScalingGroupName,Instances.length(@)]' \
--output text | sort
```
