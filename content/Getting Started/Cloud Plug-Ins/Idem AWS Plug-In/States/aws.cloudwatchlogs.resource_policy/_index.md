---
title: "aws.cloudwatchlogs.resource_policy"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes a resource policy from this account. This revokes the access of the identities in that policy to put log
events to this account.

Args:
    hub:
    ctx:
    name(Text): The name of the policy to be revoked. An Idem name of the resource
    resource_id(Text, Optional): AWS CloudWatchLogs resource policy name prefix

Request Syntax:
    [log_group_resource_policy_name]:
      aws.cloudwatchlogs.resource_policy.absent:
      - name: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_policy_is_absent:
          aws.cloudwatchlogs.resource_policy.absent:
            - name: policy-tu62879
            - resource_id: policy-tu62879
```
{{< /tab >}}

{{< tab "describe" >}}

```
Lists the resource policies in this account.

Args:
    hub:
    ctx:

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.cloudwatchlogs.resource_policy
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates or updates a resource policy allowing other Amazon Web Services services to put log events to this account,
such as Amazon Route 53. An account can have up to 10 resource policies per Amazon Web Services Region.

Args:
    hub:
    ctx:
    name(Text): Name of the new policy. An Idem name of the resource
    policy_document(Text): Details of the new policy, including the identity of the principal that is enabled to
        put logs to this account. This is formatted as a JSON string. This parameter is required.
    resource_id(Text, Optional): AWS CloudWatchLogs resource policy name prefix

Request Syntax:
    [log_group_resource_policy_name]:
      aws.cloudwatchlogs.resource_policy.present:
      - name: 'string'
      - policy_document: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_policy_is_present:
          aws.cloudwatchlogs.resource_policy.present:
            - name: policy-tu62879
            - policy_document: "{ "Version": "2012-10-17", "Statement": [ { "Sid": "Route53LogsToCloudWatchLogs",
                    "Effect": "Allow", "Principal": { "Service": [ "route53.amazonaws.com" ] }, "Action":
                    "logs:PutLogEvents", "Resource": "logArn", "Condition": { "ArnLike": { "aws:SourceArn":
                    "myRoute53ResourceArn" }, "StringEquals": { "aws:SourceAccount": "myAwsAccountId" } } } ] }"
            - resource_id: policy-tu62879
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.cloudwatchlogs.resource_policy](https://docs.idemproject.io/idem-aws/en/latest/ref/states/cloudwatchlogs/resource_policy.html).
