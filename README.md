# OpenObserve on ec2

This repository contains things you can use for running OpenObserve on AWS ec2 instances without a Kubernetes cluster.

## bucket.sh

This script does following:

1. Creates an s3 bucket
2. Creates an IAM policy
3. Creates an IAM role and associates this role with the policy created in step 2. This role has a trust relation for ec2.

You can attach the IAM role created above to your ec2 instance. This will allow OpenObserve running on the ec2 instance to access s3 for read/write.

## Attaching IAM role to ec2 instance

You can either use GUI or CLI.

You can attach the IAM role to an EC2 instance using the AWS CLI with this command:

```shell
aws ec2 associate-iam-instance-profile --instance-id YOUR_INSTANCE_ID --iam-instance-profile Name=OpenObserveRole
```


You can get your instance ID using:

```shell
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId]' --output text
```



## How to run OpenObserve

Once you have the IAM role attached to your EC2 instance run the below command to start OpenObserve:

```shell
ZO_ROOT_USER_EMAIL="root@example.com" ZO_ROOT_USER_PASSWORD="Complexpass#123" ZO_S3_BUCKET_NAME=$bucket_name ./openobserve
```
