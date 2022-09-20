---
title: "aws.config.delivery_channel"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified delivery channel Before you can delete the delivery channel, you must stop the configuration recorder
by using the StopConfigurationRecorder action.

Args:
    name(Text): An Idem name of the rule.
    resource_id(Text, optional): AWS Config delivery channel Name. Idem automatically considers this resource being absent
     if this field is not specified.

Returns:
      Dict[str, Any]

Examples:
      .. code-block:: sls

        ec2-instance-no-public-ip:
          aws.config.delivery_channel.absent:
          - name: ec2-instance-no-public-ip
          - resource_id: ec2-instance-no-public-ip
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Return details about your delivery channel.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.config.delivery_channel
```
{{< /tab >}}

{{< tab "present" >}}

```
Add or update the configuration delivery channel object that delivers the configuration information to an Amazon S3 bucket
and to an Amazon SNS topic. For more information about delivery channel, please see AWS Config services
Args:
    name(Text): An Idem name of the delivery channel.
    s3_bucket_name (Text): The name of the Amazon S3 bucket to which Config delivers configuration snapshots and configuration history files
    resource_id (Text, Optional): The resource Id of the delivery channel.
    s3_key_prefix (Text, Optional): The prefix for the specified Amazon S3 bucket.
    s3_kms_key_arn (Text, Optional): The Amazon Resource Name (ARN) of the Key Management Service (KMS ) KMS key (KMS key) used to encrypt objects delivered by Config.
    sns_topic_arn (Text, Optional): The Amazon Resource Name (ARN) of the Amazon SNS topic to which Config sends notifications about configuration changes.
    config_snapshot_delivery_properties (Dict[str, Any], Optional):
        * delivery_frequency (str, optional): The frequency with which Config delivers configuration snapshots.

Request syntax:
    [aws-config-delivery_channel]:
      aws.config.delivery_channel.present:
      - name: 'string'
      - resource_id: 'string'
      - s3_bucket_name 'string'
      - s3_key_prefix: 'string'
      - s3_kms_key_arn: 'string'
      - sns_topic_arn: 'string'
      - config_snapshot_delivery_properties: dict
        delivery_frequency: 'string'

Returns:
     Dict[str, Any]

Examples:
    .. code-block:: sls
        aws-config-delivery_channel:
          aws.config.delivery_channel.present:
            - name: 'delivery-channel'
            - resource_id: 'delivery-channel'
            - s3_bucket_name 'Test-S3'
            - s3_key_prefix: 'S3-prefix'
            - s3_kms_key_arn: 'Test-Kms-Key'
            - sns_topic_arn: 'Test-Topic'
            - config_snapshot_delivery_properties:
              delivery_frequency: 'One_Hour'
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.config.delivery_channel](https://docs.idemproject.io/idem-aws/en/latest/ref/states/config/delivery_channel.html).
