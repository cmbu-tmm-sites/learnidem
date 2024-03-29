---
title: "aws.organizations.policy"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified policy from your organization. Before you perform this operation, you must first detach
the policy from all organizational units (OUs), roots, and accounts. This operation can be called only from the
organization's management account.

Args:
    name(Text): Name of the resource.
    resource_id(Text): WS Organization policy ID to identify the resource.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls
        p-iauqv2gg:
            aws.organizations.policy.absent:
            - name: policy_name_1
            - resource_id: p-iauqv2gg
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Retrieves information about a policy.

This operation can be called only from the organization's management account
or by a member account that is a delegated administrator for an AWS service.

Currently, IDEM AWS supports only SERVICE_CONTROL_POLICY.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.organizations.policy
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a policy of a specified type that you can attach to a root, an organizational unit (OU), or an
individual AWS account. For more information about policies and their use, see Managing Organization Policies.
If the request includes tags, then the requester must have the organizations:TagResource permission. This
operation can be called only from the organization's management account.

Args:
    name(Text): Name of the resource.
    resource_id(Text, Optional): AWS Organization policy ID to identify the resource.
    description: An optional description to assign to the policy.
    policy_type : The type of policy to create. Only supported type currently is SERVICE_CONTROL_POLICY
    content : The policy text content to add to the new policy. The text that you supply must adhere to
                the rules of the policy type you specify in the Type parameter
    tags(List or Dict, optional): list of tags in the format of [{"Key": tag-key, "Value": tag-value}] or dict in the format of
                                  {tag-key: tag-value}

Request Syntax:
    [policy-name]:
      aws.organizations.policy.present:
      - resource_id: 'string'
      - name: 'string'
      - description: 'string'
      - policy_type: 'string'
      - content: 'string'
      - tags:
        - Key: 'string'
          Value: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        p-name:
          aws.organizations.policy.present:
            - resource_id: p_id
            - name: AllowAllS3Actions
            - description: Enables admins of attached accounts to delegate all S3 permissions
            - policy_type : SERVICE_CONTROL_POLICY
            - content : '{\"Version\":\"2012-10-17\",\"Statement\":{\"Effect\":\"Allow\",\"Action\":\"s3:*\"}}'
            - tags:
              - Key: org
                Value: idem-aws
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.organizations.policy](https://docs.idemproject.io/idem-aws/en/latest/ref/states/organizations/policy.html).
