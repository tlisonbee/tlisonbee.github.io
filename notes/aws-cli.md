
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

# Find all EBS Snapshots with a particular tag and add another tag
``` bash
for snapshot in `aws ec2 describe-snapshots  --filters "Name=tag:MyExistingTagName,Values=MyExistingTagValue" --query 'Snapshots[*].SnapshotId' --output text  | xargs`; 
do 
  echo $snapshot; 
  aws ec2 create-tags --resources $snapshot --tags 'Key=AdditionalTagName,Value=AdditionalTagValue' ; 
done
```

# Elastic Search Research

``` bash
for name in `aws es list-domain-names  --query 'DomainNames[*].DomainName' --output text | xargs`
do 
    echo "======== $name ===========" ; 
    aws es  describe-elasticsearch-domains  --domain-names $name 
    aws es list-tags --arn "arn:aws:es:us-east-1:1234567890:domain/$name"
done > my-report.txt
```
