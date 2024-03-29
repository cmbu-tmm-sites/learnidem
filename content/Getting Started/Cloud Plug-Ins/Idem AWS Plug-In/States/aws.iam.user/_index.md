---
title: "aws.iam.user"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified IAM user. Unlike the Amazon Web Services Management Console, when you delete a user
programmatically, you must delete the items attached to the user manually, or the deletion fails. For more
information, see Deleting an IAM user. Before attempting to delete a user, remove the following items:
Password (DeleteLoginProfile)   Access keys (DeleteAccessKey)   Signing certificate (DeleteSigningCertificate)
SSH public key (DeleteSSHPublicKey)   Git credentials (DeleteServiceSpecificCredential)   Multi-factor
authentication (MFA) device (DeactivateMFADevice, DeleteVirtualMFADevice)   Inline policies (DeleteUserPolicy)
Attached managed policies (DetachUserPolicy)   Group memberships (RemoveUserFromGroup)

Args:
    name(Text): A name, ID to identify the resource.
    resource_id(Text, optional): The name of the user to delete. This parameter allows (through its regex pattern) a string of
        characters consisting of upper and lowercase alphanumeric characters with no spaces. You can
        also include any of the following characters: _+=,.@-.

Request syntax:

    user-1:
          aws.iam.user.absent:
            - name: 'string'
            - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        user-1:
          aws.iam.user.absent:
            - name: user-1
            - resource_id: user-1
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists the IAM users that have the specified path prefix. If no path prefix is specified, the operation returns
all users in the Amazon Web Services account. If there are none, the operation returns an empty list.  IAM
resource-listing operations return a subset of the available attributes for the resource. For example, this
operation does not return tags, even though they are an attribute of the returned object. To view all of the
information for a user, see GetUser.  You can paginate the results using the MaxItems and Marker parameters.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.iam.user
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a new IAM user for your Amazon Web Services account.  For information about quotas for the number of IAM
users you can create, see IAM and STS quotas in the IAM User Guide.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text, optional): AWS IAM username
    user_name(Text): The name of the user to create. IAM user, group, role, and policy names must be unique within
        the account. Names are not distinguished by case. For example, you cannot create resources named
        both "MyResource" and "myresource".
    path(Text, optional):  The path for the user name. For more information about paths, see IAM identifiers in the IAM
        User Guide. This parameter is optional. If it is not included, it defaults to a slash (/). This
        parameter allows (through its regex pattern) a string of characters consisting of either a
        forward slash (/) by itself or a string that must begin and end with forward slashes. In
        addition, it can contain any ASCII character from the ! (\u0021) through the DEL character
        (\u007F), including most punctuation characters, digits, and upper and lowercased letters. Defaults to None.
    permissions_boundary(Text, optional): The ARN of the policy that is used to set the permissions boundary for the user. Defaults to None.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the user.
        Each tag consists of a key name and an  associated value. Defaults to None.
        * (Key): The key name that can be used to look up or retrieve the associated value. For example,
            Department or Cost Center are common choices.
        * (Value): The value associated with this tag. For example, tags with a key name of Department could have
            values such as Human Resources, Accounting, and Support. Tags with a key name of Cost Center
            might have values that consist of the number associated with the different cost centers in your
            company. Typically, many resources have tags with the same key name but with different values.
            Amazon Web Services always interprets the tag Value as a single string. If you need to store an
            array, you can store comma-separated values in the string. However, you must interpret the value
            in your code.

Request Syntax:
    user-name:
          aws.iam.user.present:
            - user_name: 'string'
            - resource_id: 'string'
            - path: 'string'
            - permissions_boundary: 'string'
            - tags:
                - Key: 'string'
                  Value: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        user1:
          aws.iam.user.present:
            - user_name: iam-user-1
            - resource_id: iam-user-1
            - path: /
            - permissions_boundary: arn:aew12k3r4kr9efg9
            - tags:
                - Key: test-key
                  Value: test-value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.iam.user](https://docs.idemproject.io/idem-aws/en/latest/ref/states/iam/user.html).
