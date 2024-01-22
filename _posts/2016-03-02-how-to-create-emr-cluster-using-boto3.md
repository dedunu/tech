---
layout: post
title: How to create an EMR cluster using Boto3?
---

I wrote a blog post about [Boto2 and EMR clusters a few months ago](2016-01-05-how-to-specify-releaselabel-for-emr.md). Today I'm going to show how to create EMR clusters using Boto3. Boto3 documentation is available at [here](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html).

```python
import boto3

__author__ = 'dedunu'

connection = boto3.client(
    'emr',
    region_name='us-west-1',
    aws_access_key_id='<Your AWS Access Key>',
    aws_secret_access_key='<You AWS Secred Key>',
)

cluster_id = connection.run_job_flow(
    Name='test_emr_job_with_boto3',
    LogUri='s3://<your s3 location>',
    ReleaseLabel='emr-4.2.0',
    Instances={
        'InstanceGroups': [
            {
                'Name': "Master nodes",
                'Market': 'ON_DEMAND',
                'InstanceRole': 'MASTER',
                'InstanceType': 'm1.large',
                'InstanceCount': 1,
            },
            {
                'Name': "Slave nodes",
                'Market': 'ON_DEMAND',
                'InstanceRole': 'CORE',
                'InstanceType': 'm1.large',
                'InstanceCount': 2,
            }
        ],
        'Ec2KeyName': '<Ec2 Keyname>',
        'KeepJobFlowAliveWhenNoSteps': True,
        'TerminationProtected': False,
        'Ec2SubnetId': '<Your Subnet ID>',
    },
    Steps=[],
    VisibleToAllUsers=True,
    JobFlowRole='EMR_EC2_DefaultRole',
    ServiceRole='EMR_DefaultRole',
    Tags=[
        {
            'Key': 'tag_name_1',
            'Value': 'tab_value_1',
        },
        {
            'Key': 'tag_name_2',
            'Value': 'tag_value_2',
        },
    ],
)

print (cluster_id['JobFlowId'])
```

#### Gistss

- <https://gist.github.com/dedunumax/5491fa5430427626ef47>

### Tags

- emr
- amazon
- boto3
- boto
- aws
