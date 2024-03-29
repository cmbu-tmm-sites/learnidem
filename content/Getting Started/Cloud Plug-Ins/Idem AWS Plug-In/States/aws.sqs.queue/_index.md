---
title: "aws.sqs.queue"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the queue specified by the QueueUrl, regardless of the queue's contents.  Be careful with the
DeleteQueue action: When you delete a queue, any messages in the queue are no longer available. When you
delete a queue, the deletion process takes up to 60 seconds. Requests you send involving that queue during the
60 seconds might succeed. For example, a  SendMessage  request might succeed, but after 60 seconds the queue and
the message you sent no longer exist. When you delete a queue, you must wait at least 60 seconds before creating
a queue with the same name. Cross-account permissions don't apply to this action. For more information, see
Grant cross-account permissions to a role and a user name in the Amazon SQS Developer Guide.

Args:
    name(Text): The name of the SQS queue to delete.
    resource_id(Text, optional): The URL of the Amazon SQS queue to delete. Case-sensitive.
        Idem automatically considers this resource being absent if this field is not specified.

Request Syntax:
    [idem_resource_name]:
      aws.sqs.queue.absent:
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.sqs.queue.absent:
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**


Returns a list of your queues in the current region.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.sqs.queue
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a new standard or FIFO queue. You can pass one or more attributes in the request. Keep the following in
mind:
    If you don't specify the fifo_queue attribute, Amazon SQS creates a standard queue. You can't change the
    queue type after you create it, and you can't convert an existing standard queue into a FIFO queue. You must
    either create a new FIFO queue for your application or delete your existing standard queue and recreate it as a
    FIFO queue. For more information, see Moving From a Standard Queue to a FIFO Queue in the Amazon SQS Developer
    Guide. If you don't provide a value for an attribute, the queue is created with the default value for the
    attribute. If you delete a queue, you must wait at least 60 seconds before creating a queue with the same
    name. To successfully create a new queue, you must provide a queue name that adheres to the limits related to
    queues and is unique within the scope of your queues. After you create a queue, you must wait at least one
    second after the queue is created to be able to use the queue. Cross-account permissions
    don't apply to this action. For more information, see Grant cross-account permissions to a role and a user name
    in the Amazon SQS Developer Guide.

Args:
    name(str): The name of the new queue. The following limits apply to this name:
        A queue name can have up to 80 characters. Valid values: alphanumeric characters, hyphens (-), and
        underscores (_). A FIFO queue name must end with the .fifo suffix. Case-sensitive.
    resource_id(str, optional): The URL of the Amazon SQS queue. Case-sensitive. Defaults to None.
    delay_seconds(int, optional): The length of time, in seconds, for which the delivery of all messages in the
        queue is delayed. Valid values: An integer from 0 to 900 seconds (15 minutes). Default: 0.
    maximum_message_size(int, optional): The limit of how many bytes a message can contain before
        Amazon SQS rejects it. Valid values: An integer from 1,024 bytes (1 KiB) to 262,144 bytes (256 KiB).
        Default: 262,144 (256 KiB).
    message_retention_period(int, optional): The length of time, in seconds, for which Amazon SQS retains a message.
        Valid values: An integer from 60 seconds (1 minute) to 1,209,600 seconds (14 days).
        Default: 345,600 (4 days).
    policy(Dict, optional): The queue's policy. A valid Amazon Web Services policy. For more information
        about policy structure, see Overview of Amazon Web Services IAM Policies in the Amazon IAM User Guide.
    receive_message_wait_time_seconds(int, optional): The length of time, in seconds, for which a ReceiveMessage
        action waits for a message to arrive. Valid values: An integer from 0 to 20 (seconds). Default: 0.
    redrive_policy(Dict, optional): The dictionary that includes the parameters for the dead-letter queue
        functionality of the source queue. For more information about the redrive policy and dead-letter queues,
        see Using Amazon SQS Dead-Letter Queues in the Amazon SQS Developer Guide.
        * deadLetterTargetArn (str): The Amazon Resource Name (ARN) of the dead-letter queue to which Amazon SQS
            moves messages after the value of maxReceiveCount is exceeded.
        * maxReceiveCount (int): The number of times a message is delivered to the source queue before being moved to
            the dead-letter queue. When the ReceiveCount for a message exceeds the maxReceiveCount for a queue,
            Amazon SQS moves the message to the dead-letter-queue. The dead-letter queue of a FIFO queue must also
            be a FIFO queue. Similarly, the dead-letter queue of a standard queue must also be a standard queue.
    visibility_timeout(int, optional): The visibility timeout for the queue, in seconds. Valid values: An integer
        from 0 to 43,200 (12 hours). Default: 30. For more information about the visibility timeout,
        see Visibility Timeout in the Amazon SQS Developer Guide.
    The following attributes apply only to server-side-encryption:
    kms_master_key_id(str, optional): The ID of an Amazon Web Services managed customer master key (CMK) for
        Amazon SQS or a custom CMK. For more information, see Key Terms. While the alias of the Amazon Web Services
        managed CMK for Amazon SQS is always alias/aws/sqs, the alias of a custom CMK can, for example, be
        alias/MyAlias . For more examples, see KeyId in the Key Management Service API Reference.
    kms_data_key_reuse_period_seconds(int, optional): The length of time, in seconds, for which Amazon SQS can
        reuse a data key to encrypt or decrypt messages before calling KMS again. An integer representing seconds,
        between 60 seconds (1 minute) and 86,400 seconds (24 hours). Default: 300 (5 minutes). A shorter time period
        provides better security but results in more calls to KMS which might incur charges after Free Tier.
        For more information, see How Does the Data Key Reuse Period Work?
    sqs_managed_sse_enabled(bool, optional): enables server-side queue encryption using SQS owned encryption keys.
        Only one server-side encryption option is supported per queue.

    The following attributes apply only to FIFO (first-in-first-out) queues:
    fifo_queue(bool, optional): Designates a queue as FIFO. Valid values are true and false. If you don't specify
        the FifoQueue attribute, Amazon SQS creates a standard queue. You can provide this attribute only during
        queue creation. You can't change it for an existing queue. When you set this attribute, you must also
        provide the MessageGroupId for your messages explicitly. For more information, see FIFO queue logic in
        the Amazon SQS Developer Guide.
    content_based_deduplication(bool, optional): Enables content-based deduplication. Valid values are true and
        false. For more information, see Exactly-once processing in the Amazon SQS Developer Guide. Note
        the following:
            Every message must have a unique MessageDeduplicationId.
                You may provide a MessageDeduplicationId explicitly.
                If you aren't able to provide a MessageDeduplicationId and you enable ContentBasedDeduplication
                    for your queue, Amazon SQS uses a SHA-256 hash to generate the MessageDeduplicationId using
                    the body of the message (but not the attributes of themessage).
                If you don't provide a MessageDeduplicationId and the queue doesn't have
                    ContentBasedDeduplication set, the action fails with an error.
                If the queue has ContentBasedDeduplication set, your MessageDeduplicationId overrides
                    the generated one.
            When ContentBasedDeduplication is in effect, messages with identical content sent within
                the deduplication interval are treated as duplicates
                and only one copy of the message is delivered.
            If you send one message with ContentBasedDeduplication enabled and then another message with a
                MessageDeduplicationId that is the same as the one generated for the first
                MessageDeduplicationId, the two messages are treated as duplicates and only one copy of the
                message is delivered.

    The following attributes apply only to high throughput for FIFO queues:
    deduplication_scope(str, optional): Specifies whether message deduplication occurs at the message group
        or queue level. Valid values are messageGroup and queue.
    fifo_throughput_limit(str, optional): Specifies whether the FIFO queue throughput quota applies to the entire
        queue or per message group. Valid values are perQueue and perMessageGroupId. The perMessageGroupId value is
        allowed only when the value for DeduplicationScope is messageGroup.
        To enable high throughput for FIFO queues, do the following:
            Set DeduplicationScope to messageGroup.
            Set FifoThroughputLimit to perMessageGroupId.
        If you set these attributes to anything other than the values shown for
            enabling high throughput, normal throughput is in effect and deduplication occurs as specified.
        For information on throughput quotas, see Quotas related to messages in the Amazon SQS Developer
            Guide. Defaults to None.
    tags(Dict, optional): Add cost allocation tags to the specified Amazon SQS queue. For an overview, see Tagging
        Your Amazon SQS Queues in the Amazon SQS Developer Guide. When you use queue tags, keep the following
        guidelines in mind:
            Adding more than 50 tags to a queue isn't recommended.
            Tags don't have any semantic meaning. Amazon SQS interprets tags as character strings.
            Tags are case-sensitive.
            A new tag with a key identical to that of an existing tag overwrites the existing tag.
        For a full list of tag restrictions, see Quotas related to queues in the Amazon SQS Developer Guide.
        To be able to tag a queue on creation, you must have the sqs:CreateQueue and sqs:TagQueue permissions.
        Cross-account permissions don't apply to this action. For more information, see Grant cross-account
        permissions to a role and a user name in the Amazon SQS Developer Guide. Defaults to None.

Request Syntax:
    [queue_name]:
      aws.sqs.queue.present:
        - delay_seconds: 'int'
        - maximum_message_size: 'int'
        - message_retention_period: 'int'
        - policy: 'dict'
        - receive_message_wait_time_seconds: 'int'
        - redrive_policy: 'dict'
        - visibility_timeout: 'int'
        - kms_master_key_id: 'string'
        - kms_data_key_reuse_period_seconds: 'int'
        - sqs_managed_sse_enabled: 'bool'
        - fifo_queue: 'bool'
        - content_based_deduplication: 'bool'
        - deduplication_scope: 'string'
        - fifo_throughput_limit: 'string'
        - tags:
            'string': 'string'

Returns:
    Dict[str, Any]

Examples:
    .. code-block:: sls

        example_fifo_queue.fifo:
          aws.sqs.queue.present:
            - delay_seconds: 35
            - maximum_message_size: 12345
            - message_retention_period: 1759
            - policy:
                Version: 2022-03-30
                Id: Example_Queue_Policy
                Statement:
                  Effect: Deny
                  Principal:
                    AWS:
                     - "000000000000"
                  Action: sqs:SendMessage
                  Resource: arn:aws:sqs:us-west-1:000000000000:example_sqs_queue.fifo
            - receive_message_wait_time_seconds: 3
            - redrive_policy:
                deadLetterTargetArn: arn:aws:sqs:us-west-1:000000000000:dead_letter_sqs_queue.fifo
                maxReceiveCount: 5
            - visibility_timeout: 75
            - kms_master_key_id: alias/sample/key
            - kms_data_key_reuse_period_seconds: 735
            - fifo_queue: true
            - content_based_deduplication: true
            - deduplication_scope: message_group
            - fifo_throughput_limit: perMessageGroupId
            - tags:
                something: this-is-just-some-text
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.sqs.queue](https://docs.idemproject.io/idem-aws/en/latest/ref/states/sqs/queue.html).
