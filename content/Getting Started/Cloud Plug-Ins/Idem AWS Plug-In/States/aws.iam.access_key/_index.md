---
title: "aws.iam.access_key"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Ensure the specified access key does not exist.
Either resource_id or both user_name and access_key_id must be passed in.

Args:
    name(Text): An Idem name describing the resource.
    user_name(Text): AWS IAM user name that the key belongs to.
    resource_id(Text, optional): AWS IAM access key ID.
Returns:
    Dict[str, Any]
Examples:
    .. code-block:: sls
        name_describing_key:
          aws.iam.access_key.absent:
            - user_name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe access keys and their current status in a way that can be managed via the "present" function.

We describe all access keys for all users the logged in user can list.

Returns:
    Dict[str, Any]
Examples:
    .. code-block:: bash
        $ idem describe aws.iam.access_key
```
{{< /tab >}}

{{< tab "present" >}}

```
Ensures an AWS key has the assigned status.

This will create a new access key for a user if no access_key_id is passed for this state, either via
access_key_id or resource_id.

If a new access key is created, the secret access key will also be returned. This can optionally be encrypted
with a base 64 encoded PGP public key.

Args:
    name(Text): An Idem name describing the resource.
    user_name(Text): AWS IAM user name that the key belongs to.
    resource_id(Text, optional): AWS IAM access key ID.
    status(Text, optional): "Active" or "Inactive"; Active keys are valid for API calls. Defaults to "Active".
    pgp_key(Text, optional): A base 64 encode PGP public key, used to encrypt the secret access key if a new key is created.

Returns:
    Dict[str, Any]

Examples:
    .. code-block:: sls
        name_describing_key:
          aws.iam.access_key.present:
            - user_name: aws_user
            - status: Active
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.iam.access_key](https://docs.idemproject.io/idem-aws/en/latest/ref/states/iam/access_key.html).
