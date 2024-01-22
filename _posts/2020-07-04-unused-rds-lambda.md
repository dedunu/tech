---
layout: post
title: "Stopping unused RDS instances using AWS Lambda"
---

If you stop unused RDS instances, it will start in 7 days. It is easy, if you have one instance, you can manage manually. When you have 100s of database instances, it is a bit difficult to stop them manually. If you create a lambda function with a weekly EventBrigde (CloudWatch Events) trigger, it will keep the instances stopped.

```python
"""RDS-Unused AWS Lambda Function
It will go through the REGION's RDS instances and check on CloudWatch for the unused
instances and will stop them.
"""
import json
from datetime import datetime, timedelta
from multiprocessing import Process, Pipe

import boto3

REGION = 'us-west-1'
"""str: Region to scan
"""


def lambda_handler(event, context):
    """Entry point for the Lambda function
    :param event: Parameters sent to the function
    :param context: Runtime information
    :return: number of databases scanned
    """

    print("Event:" + str(event))
    print("Context:" + str(event))

    # Connecting to AWS and getting all the instances
    client = boto3.client('rds', region_name=REGION)
    paginator = client.get_paginator('describe_db_instances')
    pages = paginator.paginate()

    processes = []
    parents = []

    # Creating threads using process for each database instance
    for db_instance in [db_instances
                        for page in pages
                        for db_instances in page['DBInstances']]:
        create_process(db_instance['DBInstanceIdentifier'], processes, parents)

    # Starting all the processes
    for process in processes:
        process.start()

    # Waiting for all the process to end
    for process in processes:
        process.join()

    # Counting the number of instances scanned
    db_instances_scanned = sum(parent.recv()[0] for parent in parents)

    print('Ununsed instance scan finished successfully. Scanned ' +
          str(db_instances_scanned) + ' instances.')

    return {
        'scanned': json.dumps(db_instances_scanned)
    }


def create_process(db_instance, processes, parent_connections):
    """Create a process and add to processes
    :param db_instance: Instance object returned from boto3
    :param processes: Process array with all the processes
    :param parent_connections: Parent connections to collect results
    """

    parent_conn, child_conn = Pipe()
    parent_connections.append(parent_conn)

    process = Process(
        target=check_for_unused,
        args=(db_instance, child_conn)
    )

    processes.append(process)


def check_for_unused(db_instance, conn):
    """Checking for instances with no connections and stop them.
    :param db_instance: Database instance information returned fromm boto3
    :param conn: child connection
    """
    client = boto3.client('cloudwatch', region_name=REGION)

    end_date = datetime.utcnow()
    start_date = end_date - timedelta(days=14)

    # Getting DatabaseConnections metrics for the last 14 days
    connection_statistics = client.get_metric_statistics(
        Namespace='AWS/RDS',
        MetricName='DatabaseConnections',
        Dimensions=[
            {
                'Name': 'DBInstanceIdentifier',
                'Value': db_instance
            },
        ],
        StartTime=start_date,
        EndTime=end_date,
        Period=86400,
        Statistics=["Maximum"]
    )

    total_connection_count = sum(data_point['Maximum']
                                 for data_point in connection_statistics['Datapoints'])

    if total_connection_count == 0:
        rds_client = boto3.client('rds', region_name=REGION)
        try:
            rds_client.stop_db_instance(DBInstanceIdentifier=db_instance)
            print(db_instance + " database was stopped.")
        except rds_client.exceptions.InvalidDBInstanceStateFault:
            print('Failed to stop ' + db_instance)

    conn.send([1])
    conn.close()
```

## Gist

- <https://gist.github.com/dedunumax/cc66e901e29e139247690d54be77d026>

### Tags

- aws
- rds
- python
- lambda