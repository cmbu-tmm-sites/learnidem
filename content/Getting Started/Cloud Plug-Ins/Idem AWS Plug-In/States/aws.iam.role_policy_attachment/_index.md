---
title: "aws.iam.role_policy_attachment"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Removes the specified managed policy from the specified role.

Args:
    name(Text): The name of the AWS IAM role policy.
    role_name(Text): The name (friendly name, not ARN) of the role to attach a policy.
     This parameter allows (through its regex pattern ) a string of characters consisting of upper and lowercase
      alphanumeric characters with no spaces. You can also include any of the following characters: _+=,.@-
    policy_arn(Text): The Amazon Resource Name (ARN) of the IAM policy you want to attach.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.iam.role_policy_attachment.absent:
            - name: value
            - role_name: value
            - policy_arn: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists the names of the attached managed policies of all IAM roles. If there are no managed policies attached
 to the specified role, the operation returns an empty dict.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.iam.role_policy_attachment
```
{{< /tab >}}

{{< tab "present" >}}

```
Attaches the specified managed policy to the specified IAM role. When you attach a managed policy to a role,
 the managed policy becomes part of the role's permission (access) policy.

Args:
    hub:
    ctx:
    name(Text): A name to represent the operation. This name is only for logging purpose. It is not used to
     attach a policy to a role.
    role_name(Text): The name (friendly name, not ARN) of the role to attach a policy.
     This parameter allows (through its regex pattern ) a string of characters consisting of upper and lowercase
      alphanumeric characters with no spaces. You can also include any of the following characters: _+=,.@-
    policy_arn(Text): The Amazon Resource Name (ARN) of the IAM policy you want to attach.
    resource_id(Text, Optional): The identifier for this object

Request Syntax:
    [iam-attach-role-policy-name]:
      aws.iam.role_policy_attachment.present:
      - resource_id: 'string'
      - role_name: 'string'
      - policy_arn: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem-test-policy-temp-name:
          aws.iam.role_policy_attachment.present:
            - role_name: idem-test-role-name
            - policy_arn: arn:aws:iam::aws:policy/ReadOnlyAccess
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.iam.role_policy_attachment](https://docs.idemproject.io/idem-aws/en/latest/ref/states/iam/role_policy_attachment.html).
