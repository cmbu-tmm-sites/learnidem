---
title: "aws.sns.subscription"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified subscription. This action is idempotent, so deleting a topic that does not exist
does not result in an error.

Args:
    name(Text): The name of the state.
    resource_id(Text): The AWS resource identifier i.e. resource arn

Request Syntax:
    [subscription-name]:
      aws.sns.subscription.absent:
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        test-subscription:
          aws.sns.subscription.absent:
          - resource_id: arn:aws:sns:eu-west-3:537227425989:test-topic:9c0fd640-7fc6-4888-bc08-f0a497a6237f
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function
Describes list of all the subscriptions present in all topics


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.sns.subscription
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a new endpoint subscription to a topic.If the endpoint type is HTTP/S or email, or if the endpoint and
the topic are not in the same Amazon Web Services account,For http and email protocols the endpoint owner must
run the ConfirmSubscription action to confirm the subscription.

Args:
    hub:
    ctx:
    name(Text): The idem name for the resource
    topic_arn(Text): The ARN of the topic to which the subscription should be added
    protocol(Text): The protocol that you want to use.Supported protocols are:http,https,email,email-json,
                              sms,sqs,application,lambda,firehose
    endpoint(Text): The endpoint that you want to receive notifications.Endpoints vary by protocol
    resource_id(Text, optional): The AWS resource identifier, here it is resource arn
    attributes(Dict, optional): Attributes of the subscription
    return_subscription_arn(bool, optional): A bool value to specify if the subscription_arn should be return after
                                            creation.By default,it is false i.e. subscription_arn is not returned.


Request Syntax:
    [subscription-name]:
      aws.sns.subscription.present:
      - topic_arn: 'string'
      - protocol: 'string'
      - endpoint: 'string'
      - resource_id: 'string'
      - attributes: 'dict'
      - return_subscription_arn: 'bool'


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        subscription-name:
          aws.sns.subscription.present:
            - topic_arn: arn:aws:sns:eu-west-3:537227425989:test-topic
            - protocol: sms
            - endpoint: "+911234567890"
            - attributes:
                DeliveryPolicy: '{"healthyRetryPolicy": {"minDelayTarget": 10,"maxDelayTarget": 30,"numRetries": 10,"numMaxDelayRetries": 7,"numNoDelayRetries": 0,"numMinDelayRetries": 3,"backoffFunction": "linear"},"sicklyRetryPolicy": null,"throttlePolicy": null,"guaranteed": false}'
                FilterPolicy: '{"pets": ["dog", "cat"]}'
            - return_subscription_arn: True
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.sns.subscription](https://docs.idemproject.io/idem-aws/en/latest/ref/states/sns/subscription.html).
