---
title: "aws.iam.user_policy_attachment"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Removes the specified managed policy from the specified user.
A user can also have inline policies embedded with it. To delete an inline policy, use DeleteUserPolicy

Args:
    name(Text): The name (friendly name, not ARN) of the IAM user to attach the policy to.
    user_name(Text): The name (friendly name, not ARN) of the IAM user to detach the policy from.
    This parameter allows (through its regex pattern ) a string of characters consisting of upper and lowercase alphanumeric characters with no spaces. You can also include any of the following characters: _+=,.@-
    policy_arn(Text): The Amazon Resource Name (ARN) of the IAM policy you want to attach.

Request Syntax:
    [iam-user-policy-name]:
      aws.iam.user_policy.absent:
      - user_name: 'string'
      - policy_arn: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

    serverless-arn:aws:iam::aws:policy/AdministratorAccess:
      aws.iam.user_policy_attachment.absent:
      - user_name: serverless
      - policy_arn: arn:aws:iam::aws:policy/AdministratorAccess
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists all managed policies that are attached to the specified IAM user. Lists all managed policies that are attached to the specified IAM user.



Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws_auto.iam.user_policy_attachment
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Attaches the specified managed policy to the specified user.
You use this operation to attach a managed policy to a user. To embed an inline policy in a user, use PutUserPolicy .

Args:
    hub:
    ctx:
    name(Text): The name (friendly name, not ARN) of the IAM user to attach the policy to.
    user_name(Text): The name (friendly name, not ARN) of the IAM user to detach the policy from.
    This parameter allows (through its regex pattern ) a string of characters consisting of upper and lowercase alphanumeric characters with no spaces. You can also include any of the following characters: _+=,.@-
    policy_arn(Text): The Amazon Resource Name (ARN) of the IAM policy you want to attach.

Request Syntax:
    [iam-attach-user-policy-name]:
      aws.iam.user_policy_attachment.present:
      - user_name: 'string'
      - policy_arn: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls
    serverless-arn:aws:iam::aws:policy/AdministratorAccess:
      aws.iam.user_policy_attachment.present:
      - user_name: serverless
      - policy_arn: arn:aws:iam::aws:policy/AdministratorAccess
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.iam.user_policy_attachment](https://docs.idemproject.io/idem-aws/en/latest/ref/states/iam/user_policy_attachment.html).
