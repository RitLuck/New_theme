---
title: "Enable Termination Protection on ec2 instances using bash "
date: 2024-06-24T15:41:16+04:00
draft: false
toc: false
images:
tags:
  - tech
  - aws
  - bash
---

To prevent your instance from being accidentally terminated, you can enable **termination protection** for the instance.

Below is a simple bash script that will 
1. Retrieve Running Instance IDs: Fetches a list of all running instance IDs in your AWS account.
2. Enable Termination Protection: Loops through each retrieved instance ID and enables termination protection.


```
#!/bin/bash

# Get a list of all running instance IDs
INSTANCE_IDS=$(aws ec2 describe-instances --filters "Name=instance-state-name,Values=running" --query "Reservations[*].Instances[*].InstanceId" --output text --profile PROFILE_NAME)

# Loop through each instance ID and enable termination protection
for instance_id in $INSTANCE_IDS
do
  echo "Enabling termination protection for instance: $instance_id"
  aws ec2 modify-instance-attribute --instance-id "$instance_id" --disable-api-termination --profile PROFILE_NAME
done

echo "Termination protection enabled for all running instances."

```

AWS CLI Commands:
   - **aws ec2 describe-instances** : Retrieves information about instances based on specified filters. Here, it fetches running instances.
   - **aws ec2 modify-instance-attribute** : Sets termination protection (--disable-api-termination) for each instance ID obtained.

Instance ID Loop:

The script iterates through each instance ID in $INSTANCE_IDS.
For each instance ID, it disables API termination to enforce termination protection.
