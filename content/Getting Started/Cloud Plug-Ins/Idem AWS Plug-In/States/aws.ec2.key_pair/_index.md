---
title: "aws.ec2.key_pair"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified key pair.

Args:
    resource_id(str): An identifier of the resource in the provider.
    name(str, optional): Name of the key_pair. Defaults to None.

Request Syntax:
    [key_pair_name]:
      aws.ec2.key_pair.absent:
      - resource_id: 'string'
      - name: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.ec2.key_pair.absent:
            - resource_id:(str): An identifier of the resource in the provider. Defaults to None.
            - name(str): value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Returns information about all key pairs in the user's account.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.key_pair
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates an ED25519 or 2048-bit RSA key pair with the specified name and
in the specified PEM or PPK format that you can use with an Amazon EC2 instance.
A key pair is used to control login access to EC2 instances. The key pair is available
only in the Amazon Web Services Region in which you create it.
Currently, this resource requires an existing user-supplied key pair.
This key pair's public key will be registered with AWS to allow logging-in to EC2 instances.
When importing an existing key pair the public key material may be in any format supported by AWS.
Supported formats are described in Amazon docs:
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#how-to-generate-your-own-key-and-import-it-to-aws
For more information, see the Amazon ec2 Developer Guide.
Please note that, for security reasons, you cannot download the keypairs themselves.
You'll simply be given their name and fingerprint.

Args:
    name(str): The name for your new key pair.
    public_key(str): The public key material.
    resource_id(str, optional): The key pair id.
    tags(Dict, optional): dict of tags to assign to the key pair in the format of
    {"tag-key": "tag-value"} or dict in the format of {tag-key: tag-value}. Defaults to None.
        * tag-key (str) --  The key of the tag. Tag keys are case-sensitive and accept a maximum of 127 Unicode characters.
        * tag-value (str) -- The value of the tag. Tag values are case-sensitive and accept a maximum of 255 Unicode characters.

Request Syntax:
    [key_pair_name]:
      aws.ec2.key_pair.present:
      - resource_id: 'string'
      - name: 'string'
      - public_key: 'string'
      - tags: Dict[str, str]
          'string': 'string'
          'string': 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.ec2.key_pair.present:
            - name: value
            - public_key: value
            - tags:
                first_key: first_value
                second_key: second_value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.key_pair](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/key_pair.html).