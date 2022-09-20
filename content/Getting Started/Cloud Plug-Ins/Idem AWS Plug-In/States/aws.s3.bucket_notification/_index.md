---
title: "aws.s3.bucket_notification"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
This action enables you to delete multiple notification configurations from a bucket using a single HTTP request.
If you know the object keys that you want to delete, then this action provides a suitable alternative to sending
individual delete requests, reducing per-request overhead. For each configuration, Amazon S3 performs a delete
action and returns the result of that delete, success, or failure, in the response.

Args:
    hub:
    ctx:
    name(Text): Name of the bucket on which notification needs to be configured.
    resource_id(Text, optional): Name of the bucket and 'notifications' keyword with a seperator '-'.

Returns:
    Dict[str, Any]

Request Syntax:
    [bucket_name-notification]:
          aws.s3.bucket_notification.absent:
            - name: [string]
            - resource_id: [string]


Examples:

    .. code-block:: sls

        test-bucket-notification:
          aws.s3.bucket_notification.absent:
            - name: test-bucket
            - resource_id: test-bucket-notifications
```
{{< /tab >}}

{{< tab "describe" >}}

```
Obtain S3 bucket notifications for each bucket under the given context for any user.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.s3.bucket_notification
```
{{< /tab >}}

{{< tab "present" >}}

```
Bucket Notification allows user to receive notifications when certain events happen in the S3 bucket. To enable
notifications, add a notification configuration that identifies the events that you want Amazon S3 to publish.
Make sure that it also identifies the destinations where you want Amazon S3 to send the notifications. You store
this configuration in the notification subresource that's associated with a bucket
Amazon S3 can publish notifications for the following events:

a) New object created events
b) Object removal events
c) Restore object events
d) Reduced Redundancy Storage (RRS) object lost events
e) Replication events
f) S3 Lifecycle expiration events
g) S3 Lifecycle transition events
h) S3 Intelligent-Tiering automatic archival events
i) Object tagging events
j) Object ACL PUT events

Amazon S3 can send event notification messages to the following destinations. User can specify the Amazon Resource
Name (ARN) value of these destinations in the notification configuration.

1) Amazon Simple Notification Service (Amazon SNS) topics
2) Amazon Simple Queue Service (Amazon SQS) queues
3) AWS Lambda function

Args:
    name(Text): Name of the bucket on which notification needs to be configured.
    notifications(List[Dict[str, Any]], optional): Describes the Lambda functions to invoke and the events for which to invoke them.
        * Id (str, optional): An optional unique identifier for configurations in a notification configuration. If you don't
            provide one, Amazon S3 will assign an ID.
        * LambdaFunctionArn (str): The Amazon Resource Name (ARN) of the Lambda function that Amazon S3 invokes when the specified
            event type occurs.
        * Events (List[str]): The Amazon S3 bucket event for which to invoke the Lambda function. For more information, see
            Supported Event Types in the Amazon S3 User Guide.
        * Filter (Dict[str, Any], optional): Specifies object key name filtering rules. For information about key name filtering, see
            Configuring Event Notifications in the Amazon S3 User Guide.
            * Key (Dict[str, Any], optional): A container for object key name prefix and suffix filtering rules.
                * FilterRules (List[Dict[str, Any]], optional): A list of containers for the key-value pair that defines the criteria for the filter rule.
                    * Name (str, optional): The object key name prefix or suffix identifying one or more objects to which the filtering rule
                        applies. The maximum length is 1,024 characters. Overlapping prefixes and suffixes are not
                        supported. For more information, see Configuring Event Notifications in the Amazon S3 User
                        Guide.
                    * Value (str, optional): The value that the filter searches for in object key names.
    resource_id(Text, optional): Name of the bucket and 'notifications' keyword with a seperator '-'.

Returns:
    Dict[str, Any]

Request Syntax:
    [bucket_name]-notifications:
          aws.s3.bucket_notification.present:
            - name: [string]
            - resource_id: [string]
            - notifications
                LambdaFunctionConfigurations:
                    - Events:
                      - [string]
                      Filter:
                        Key:
                          FilterRules:
                          - Name: Prefix
                            Value: ''
                          - Name: Suffix
                            Value: [string]
                      Id: [string]
                      LambdaFunctionArn: [string]
                TopicConfigurations:

Examples:

    .. code-block:: sls

        test-bucket-notifications:
          aws.s3.bucket_notification.present:
            - name: test-bucket
            - resource_id: test-bucket-notifications
            - notifications
                LambdaFunctionConfigurations:
                    - Events:
                      - s3:ObjectCreated:*
                      Filter:
                        Key:
                          FilterRules:
                          - Name: Prefix
                            Value: ''
                          - Name: Suffix
                            Value: .jpeg
                      Id: test
                      LambdaFunctionArn: arn:aws:lambda:us-west-1:000000000000:function:test
                TopicConfigurations:
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.s3.bucket_notification](https://docs.idemproject.io/idem-aws/en/latest/ref/states/s3/bucket_notification.html).
