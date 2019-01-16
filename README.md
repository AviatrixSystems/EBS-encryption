# EBS-encryption
This repo shows how to encrypt an AWS EBS root volume. You can use the script to apply to Aviatrix Controller and gateways. 

Requirements
------------
-       Install AWS Python SDK [Boto3](https://github.com/boto/boto3#quick-start) 
-       Install AWS CLI [AWSCLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
-       AWS CLI Configuration [Configure your client](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

-       IAM Permissions
        These IAM policy actions are required in order to run this script. This is an example policy you can attach to a user to give them the proper IAM authorization.
	    {
                "Version": "2010-10-10",
		"Statement": [
		    {
		        "Effect": "Allow",
	                "Action": [
		            "ec2:DescribeInstances",
			    "ec2:DescribeVolumes",
			    "ec2:DescribeSnapshots",
			    "ec2:StopInstances",
			    "ec2:StartInstances",
			    "ec2:CopySnapshot",
			    "ec2:CreateSnapshot",
			    "ec2:CreateVolume",
			    "ec2:DeleteVolume",
			    "ec2:DeleteSnapshot",
			    "ec2:AttachVolume",
			    "ec2:DetachVolume"
		        ],
		        "Resource": "*"
		    }
		]
	    } 


Execute the script to encrypt root volume
-----------------------------------------
syntax: enc_volume.py [-h] -i INSTANCE_ID [-key CUSTOMER_MASTER_KEY]
                     [-region REGION] [-p PROFILE] [-key_id AWS_ACCESS_KEY_ID]
                     [-secret_key AWS_SECRET_ACCESS_KEY]

Example 1:
To encrypt root volume for instance i-04b8deaeb555fbee8 with default AWS CLI created profile userx and AWS default key management system:
```sh
sudo ./enc_volume.py -i i-04b8deaeb555fbee8 -p userx
```

Example 2:
To encrypt root volume for instance i-04b8deaeb555fbee8 with default AWS CLI created profile userx and customer master key:

```sh
sudo ./enc_volume.py -i i-04b8deaeb555fbee8 -p userx -key xxx
```

Example 3:
To encrypt root volume for instance i-04b8deaeb555fbee8 in region us-east-1 with AWS Access Key ID yyy and Secret Access Key zzz and customer master key xxx:

```sh
sudo ./enc_volume.py -i i-04b8deaeb555fbee8 --key xxx --region us-east-1 --aws_access_key_id yyy --aws_secret_access_key zzz
```
