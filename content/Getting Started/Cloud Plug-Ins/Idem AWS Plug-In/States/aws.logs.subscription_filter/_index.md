---
title: "aws.logs.subscription_filter"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified subscription filter.

Args:
    name(Text): An Idem name of the resource.
    log_group_name(Text): The name of the log group.
    resource_id(Text, optional): AWS logs Subscription filter name. Defaults to None.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.logs.subscription_filter.absent:
            - name: value
            - resource_id: value
            - log_group_name: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists the subscription filters for all the log groups.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.logs.subscription_filter
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates or updates a subscription filter and associates it with the specified log group. Subscription filters
allow you to subscribe to a real-time stream of log events ingested through PutLogEvents and have them delivered
to a specific destination. When log events are sent to the receiving service, they are Base64 encoded and
compressed with the gzip format. The following destinations are supported for subscription filters:   An Amazon
Kinesis stream belonging to the same account as the subscription filter, for same-account delivery.   A logical
destination that belongs to a different account, for cross-account delivery.   An Amazon Kinesis Firehose
delivery stream that belongs to the same account as the subscription filter, for same-account delivery.   An
Lambda function that belongs to the same account as the subscription filter, for same-account delivery.   Each
log group can have up to two subscription filters associated with it. If you are updating an existing filter,
you must specify the correct name in filterName.  To perform a PutSubscriptionFilter operation, you must also
have the iam:PassRole permission.

Args:
    name(Text): An Idem name of the resource.
    log_group_name(Text): The name of the log group.
    filter_pattern(Text): A filter pattern for subscribing to a filtered stream of log events.
    destination_arn(Text): The ARN of the destination to deliver matching log events to. Currently, the supported
        destinations are:   An Amazon Kinesis stream belonging to the same account as the subscription
        filter, for same-account delivery.   A logical destination (specified using an ARN) belonging to
        a different account, for cross-account delivery. If you are setting up a cross-account
        subscription, the destination must have an IAM policy associated with it that allows the sender
        to send logs to the destination. For more information, see PutDestinationPolicy.   An Amazon
        Kinesis Firehose delivery stream belonging to the same account as the subscription filter, for
        same-account delivery.   A Lambda function belonging to the same account as the subscription
        filter, for same-account delivery.
    resource_id(Text, optional): AWS logs Subscription filter name. Defaults to None.
    role_arn(Text, optional): The ARN of an IAM role that grants CloudWatch Logs permissions to deliver ingested log events to
        the destination stream. You don't need to provide the ARN when you are working with a logical
        destination for cross-account delivery. Defaults to None.
    distribution(Text, optional): The method used to distribute log data to the destination. By default, log data is grouped by
        log stream, but the grouping can be set to random for a more even distribution. This property is
        only applicable when the destination is an Amazon Kinesis stream. Defaults to None.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.logs.subscription_filter.present:
            - name: value
            - log_group_name: value
            - filter_name: value
            - filter_pattern: value
            - role_arn: value
            - destination_arn: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.logs.subscription_filter](https://docs.idemproject.io/idem-aws/en/latest/ref/states/logs/subscription_filter.html).
