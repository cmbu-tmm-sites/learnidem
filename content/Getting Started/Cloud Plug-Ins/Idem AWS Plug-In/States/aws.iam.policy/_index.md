---
title: "aws.iam.policy"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified managed policy. Before you can delete a managed policy, you must first detach the policy
from all users, groups, and roles that it is attached to. In addition, you must delete all the policy's
versions. The following steps describe the process for deleting a managed policy:   Detach the policy from all
users, groups, and roles that the policy is attached to, using DetachUserPolicy, DetachGroupPolicy, or
DetachRolePolicy. To list all the users, groups, and roles that a policy is attached to, use
ListEntitiesForPolicy.   Delete all versions of the policy using DeletePolicyVersion. To list the policy's
versions, use ListPolicyVersions. You cannot use DeletePolicyVersion to delete the version that is marked as the
default version. You delete the policy's default version in the next step of the process.   Delete the policy
(this automatically deletes the policy's default version) using this operation.   For information about managed
policies, see Managed policies and inline policies in the IAM User Guide.

Args:
    name(Text): IAM policy name.
    resource_id(Text, optional): Amazon Resource Name (ARN) to identify IAM policy. If not specified, Idem will use "name"
     parameter to identify the IAM policy on AWS.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.iam.policy.absent:
            - name: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists all of your own customer-defined managed policies.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.iam.policy
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Create or update a managed policy for your Amazon Web Services account. When creating a policy, this operation
 creates a policy version with a version identifier of v1 and sets v1 as the policy's default version. When updating
  a policy, this operation creates a new policy version, sets the new policy to the default version, and
   deletes the old policy. As a best practice, you can validate your IAM policies. To learn more, see Validating
    IAM policies in AWS's IAM User Guide. For more information about managed policies in general,
     see Managed policies and inline policies in AWS's IAM User Guide.

Args:
    name(Text): IAM policy name.
    policy_document(Dict or Text): The JSON policy document that you want to use as the content for the new policy.
     You must provide policies in JSON format in IAM. However, for CloudFormation templates formatted in YAML,
      you can provide the policy in JSON or YAML format. CloudFormation always converts a YAML policy to JSON format
       before submitting it to IAM.
    resource_id(Text, optional): Amazon Resource Name (ARN) to identify IAM policy.
     This is a required field for Idem to manage a brown-field resource.
    path(Text, optional): The path for the policy. Defaults to a slash (/)
    description(Text, optional): A friendly description of the policy.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the IAM customer managed policy.
        Each tag consists of a key name and an associated value. Defaults to None.
        * (Key): The key name that can be used to look up or retrieve the associated value. For example,
            Department or Cost Center are common choices.
        * (Value): The value associated with this tag. For example, tags with a key name of Department could have
            values such as Human Resources, Accounting, and Support. Tags with a key name of Cost Center
            might have values that consist of the number associated with the different cost centers in your
            company. Typically, many resources have tags with the same key name but with different values.
            Amazon Web Services always interprets the tag Value as a single string. If you need to store an
            array, you can store comma-separated values in the string. However, you must interpret the value
            in your code.
    timeout(Dict, optional): Timeout configuration for create/update/deletion of AWS IAM Policy.
        * create (Dict): Timeout configuration for creating AWS IAM Policy
            * delay (int, Optional): The amount of time in seconds to wait between attempts.
            * max_attempts (int, Optional): Customized timeout configuration containing delay and max attempts.
        * update(Dict, optional): Timeout configuration for updating AWS IAM Policy
            * delay (int, Optional): The amount of time in seconds to wait between attempts.
            * max_attempts: (int, Optional) Customized timeout configuration containing delay and max attempts.

Request Syntax:
    [policy-idem-state]:
      aws.iam.policy.present:
      - name: 'string'
      - resource_id: 'string'
      - path: 'string'
      - policy_document: 'dict' or 'string'
      - description: 'string'
      - tags:
        - Key: 'string'
          Value: 'string'
      - timeout:
          create:
            delay: 'int'
            max_attempts: 'int'
          update:
            delay: 'int'
            max_attempts: 'int'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        my-iam-policy:
          aws.iam.policy.present:
            - name: idem-policy-automation
            - resource_id: arn:aws:iam::53721234567:policy/idem-policy-automation
            - path: /
            - policy_document: '{"Statement": [{"Action": ["ec2:CreateSubnet"], "Effect": "Allow", "Resource": "*"}], "Version": "2012-10-17"}'
            - description: "Idem IAM policy description example"
            - tags:
              - Key: Name
                Value: Idem-test-policy
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.iam.policy](https://docs.idemproject.io/idem-aws/en/latest/ref/states/iam/policy.html).
