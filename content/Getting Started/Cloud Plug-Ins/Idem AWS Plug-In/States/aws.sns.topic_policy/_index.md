---
title: "aws.sns.topic_policy"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the current topic policy and replace with the default value. This action is idempotent, so deleting a topic's policy that does not exist
does not result in an error.

Args:
    name(Text): The idem name of the topic_policy.
    resource_id(Text): Topic arn and 'policy' keyword separated with '-'

Request Syntax:
    [topic-policy-name]:
      aws.sns.topic_policy.absent:
      - name: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        test-topic-policy:
          aws.sns.topic_policy.absent:
          - name: test-topic-policy
          - resource_id: arn:aws:sns:eu-west-3:537227425989:test-topic-policy
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function
Describes list of all the topic policy


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.sns.topic_policy
```
{{< /tab >}}

{{< tab "present" >}}

```
Updates the topic's policy attribute. A topic can have a single policy, checks for changes in policy attribute and
updates it if required.

Args:
    hub:
    ctx:
    name(Text): The idem name for the topic_policy
    topic_arn(Text): The ARN of the topic for which the policy should be updated
    policy(Text): Topic policy, in json string format
    resource_id(Text, optional): Topic arn and 'policy' keyword separated with '-'



Request Syntax:
    [topic-policy-name]:
      aws.sns.topic_policy.present:
      - name: 'string'
      - topic_arn: 'string'
      - policy: 'string'
      - resource_id: 'string'


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        topic-policy-name:
          aws.sns.topic_policy.present:
            - name: topic-policy-name
            - topic_arn: arn:aws:sns:eu-west-3:537227425989:test-topic
            - policy: '{"Version": "2012-10-17", "Id": "id-1", "Statement": [{"Sid":
                       "__default_statement_ID", "Effect": "Allow", "Principal": {"AWS": "*"}, "Action":
                       ["SNS:GetTopicAttributes", "SNS:SetTopicAttributes", "SNS:AddPermission", "SNS:RemovePermission",
                       "SNS:DeleteTopic", "SNS:Subscribe", "SNS:ListSubscriptionsByTopic", "SNS:Publish"],
                       "Resource": "arn:aws:sns:eu-west-3:537227425989:test-topic", "Condition": {"StringEquals":
                       {"AWS:SourceOwner": "537227425989"}}}]}'
            - resource_id: arn:aws:sns:eu-west-3:537227425989:test-topic-policy
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.sns.topic_policy](https://docs.idemproject.io/idem-aws/en/latest/ref/states/sns/topic_policy.html).
