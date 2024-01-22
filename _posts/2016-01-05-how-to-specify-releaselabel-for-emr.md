---
layout: post
title: How to specify ReleaseLabel for EMR cluster with Boto2
---

Boto is the AWS SDK for Python. You can create clusters, instances or anything using Boto. But sometimes Boto imposes limitations. I wanted to create an EMR cluster with `RelaseLabel=4.2.0`. But we were using Boto2. `ReleaseLabel` is an option in Boto3. For Boto2 there was no documented option for `RelaseLabel`.

So I found out a way to create EMR (Elastic Map Reduce) clusters using Boto 2 with a specific `ReleaseLabel`.

```python
import boto.emr
import boto.exception
from boto.emr.instance_group import InstanceGroup

__author__ = 'dedunu'

connection = boto.emr.connect_to_region(
    region_name='us-east-1',
    aws_access_key_id='<Your AWS Access Key>',
    aws_secret_access_key='<You AWS Secred Key>',
)

api_params = {
    'ReleaseLabel': 'emr-4.2.0'
}

instance_groups = list()

instance_groups.append(InstanceGroup(
    num_instances=1,
    role="MASTER",
    type='m1.large',
    market="ON_DEMAND",
    name="Master nodes"))

instance_groups.append(InstanceGroup(
    num_instances=1,
    role="CORE",
    type='m1.large',
    market="ON_DEMAND",
    name="Slave nodes"))

cluster_id = connection.run_jobflow(
    name='test_emr_job_with_release_label',
    availability_zone='us-east-1a',
    instance_groups=instance_groups,
    # ami_version='3.0.0',
    enable_debugging=False,
    visible_to_all_users=True,
    keep_alive=True,
    job_flow_role="EMR_EC2_DefaultRole",
    service_role="EMR_DefaultRole",
    api_params=api_params,
)

print (cluster_id)
```

I have commented `AMI Version` because `ReleaseLabel` will pick `AMI version` correctly. The above program will print the `cluster ID` in the terminal. 

Sometimes you might get an issue saying "`No Default VPC found.`". This is a network related issue. In that case, you might need to specify `subnet ID` for EMR cluster. Then you don't need to specify an availability zone.

```python
import boto.emr
import boto.exception
from boto.emr.instance_group import InstanceGroup

__author__ = 'dedunu'

connection = boto.emr.connect_to_region(
    region_name='us-east-1',
    aws_access_key_id='<Your AWS Access Key>',
    aws_secret_access_key='<You AWS Secred Key>',
)

api_params = {
    'Instances.Ec2SubnetId': '<Your Subnet ID>',
    'ReleaseLabel': 'emr-4.2.0',
}

instance_groups = list()

instance_groups.append(InstanceGroup(
    num_instances=1,
    role="MASTER",
    type='m1.large',
    market="ON_DEMAND",
    name="Master nodes"))

instance_groups.append(InstanceGroup(
    num_instances=1,
    role="CORE",
    type='m1.large',
    market="ON_DEMAND",
    name="Slave nodes"))

cluster_id = connection.run_jobflow(
    name='test_emr_job_with_release_label',
    # availability_zone='us-east-1a',
    instance_groups=instance_groups,
    # ami_version='3.0.0',
    enable_debugging=False,
    visible_to_all_users=True,
    keep_alive=True,
    job_flow_role="EMR_EC2_DefaultRole",
    service_role="EMR_DefaultRole",
    api_params=api_params,
)

print (cluster_id)
```

#### Gistss

- <https://gist.github.com/dedunumax/f362c3a17a9027ebed2b>
- <https://gist.github.com/dedunumax/b7a0f54d2535f74e7542>

### Tags

- emr
- ReleaseLabel
- python
- boto3
- boto
- boto2
- aws
- amazon
