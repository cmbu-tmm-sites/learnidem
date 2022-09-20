---
title: "aws.ec2.flow_log"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes a flow log.

Args:
    name(Text): Name of the resource.
    resource_id(Text, optional): AWS Flow log ID.

Request Syntax:
    [flow-log-name]:
      aws.ec2.flow_log.present:
      - name: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:
    .. code-block:: sls
        resource_is_absent:
          aws.ec2.flow_log.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Describes one or more flow logs. To view the information in your flow logs (the log streams for the network
interfaces), you must use the CloudWatch Logs console or the CloudWatch Logs API.
Returns:
    Dict[str, Any]
Examples:
    .. code-block:: bash
        $ idem describe aws_auto.ec2.flow_log
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a flow log to capture information about IP traffic for a specific network interface, subnet,
or VPC.  Flow log data for a monitored network interface is recorded as flow log records, which are log events
consisting of fields that describe the traffic flow. For more information, see Flow log records in the Amazon
Virtual Private Cloud User Guide. When publishing to CloudWatch Logs, flow log records are published to a log
group, and each network interface has a unique log stream in the log group. When publishing to Amazon S3, flow
log records for all of the monitored network interfaces are published to a single log file object that is stored
in the specified bucket. For more information, see VPC Flow Logs in the Amazon Virtual Private Cloud User Guide.
Args:
    name(str): Name of the resource.
    log_group_name(str, Optional): log_group_name if the log_destination_type is cloudwatch
    resource_type(str): Type of resource flow-log is attached to (Subnet, VPC, NetworkInterface)
    traffic_type(str): Type of traffic to be recorded (REJECT, ALL, ACCEPT)
    log_destination_type(str, Optional): S3 bucket or Default: cloud-watch-logs
    log_destination(str, Optional): S3 bucket ARN
    log_format(str, Optional): Syntax to be used to print log statements
    max_aggregation_interval(int, Optional): Max interval during which packets are aggregated and then stored in log record
    resource_id(str, Optional): AWS Flow log ID.
    iam_role(str, Optional): ARN of IAM role to be used to post in cloud-watch-logs
    destination_options(Dict[str, Any], optional): The destination options. Defaults to None.
        * FileFormat (str, optional): The format for the flow log. The default is plain-text.
        * HiveCompatiblePartitions (bool, optional): Indicates whether to use Hive-compatible prefixes for flow logs stored in Amazon S3. The default
            is false.
        * PerHourPartition (bool, optional): Indicates whether to partition the flow log per hour. This reduces the cost and response time
            for queries. The default is false.
    resource_ids([str]): list of resource_ids flow-log is attached to
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the flow log resource. Defaults to None.
        * (Key, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * (Value, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.

Request Syntax:
    [flow-log-id]:
      aws.ec2.flow_log.present:
      - name: 'string'
      - log_group_name: 'string'
      - resource_type: 'integer'
      - traffic_type: 'string'
      - tags:
        - Key: 'string'
          Value: 'string'

Returns:
    Dict[str, Any]

Examples:
    .. code-block:: sls
        fl-09c0787e693332a0a:
            aws.ec2.flow_log.present:
            - traffic_type: REJECT
            - log_destination_type: s3
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.flow_log](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/flow_log.html).