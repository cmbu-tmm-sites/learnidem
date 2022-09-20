---
title: "aws.caller_identity"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "search" >}}

```
Details about the IAM user or role whose credentials are used to call the operation.

Args:
    name(string): An Idem name of the resource.

Request Syntax:
    [Idem-resource-state-name]:
      aws.caller_identity.search:
      - name: 'string'

Examples:

        my-caller-account:
          aws.caller_identity.search:
            - name: value

Response Syntax:
      {
        name: 'string',
        user_id: 'string',
        account_id: 'string',
        arn: 'string'
      }

Response Structure:
    name(string): An Idem name of the resource.
    user_id(string): The unique identifier of the calling entity.
    account_id(string): AWS account ID number of the account that owns or contains the calling entity.
    arn(string): AWS ARN associated with the calling entity.
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.caller_identity](https://docs.idemproject.io/idem-aws/en/latest/ref/states/caller_identity.html).
