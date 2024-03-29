---
title: "aws.kms.key"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Key cannot be immediately deleted but can be scheduled to be deleted.
Once the key is set to be deleted in 'pending_window_in_days' a deletion date is
set on the key and it cannot be modified.
So 'deleting' again with a different 'pending_window_in_days' is ignored.
Also key can be disabled using the present function with key_state = 'Disabled'.

Args:
    hub:
    ctx:
    name(Text): Name of the key.
    resource_id(Text, Optional): AWS KMS Key ID. Idem automatically considers this resource being absent
     if this field is not specified.
    pending_window_in_days(int, Optional, Default: 7 days): How many days before key is deleted.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.kms.key.absent:
            - resource_id: value
            - name: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Gets a list of keys in the caller's Amazon Web Services account and region. For more information about
keys, see Createkey. By default, the Listkeys operation returns all keys in the account and region.
To get only the keys associated with a particular KMS key, use the KeyId parameter. The Listkeys response
can include keys that you created and associated with your customer managed keys, and keys that Amazon Web
Services created and associated with Amazon Web Services managed keys in your account. You can recognize Amazon
Web Services keys because their names have the format aws/<service-name>, such as aws/dynamodb. The response
might also include keys that have no TargetKeyId field. These are predefined keys that Amazon Web Services
has created but has not yet associated with a KMS key. keys that Amazon Web Services creates in your account,
including predefined keys, do not count against your KMS keys quota.  Cross-account use: No. Listkeys
does not return keys in other Amazon Web Services accounts.  Required permissions: kms:Listkeys (IAM
policy) For details, see Controlling access to keys in the Key Management Service Developer Guide.  Related
operations:     CreateKey


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.kms.key
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Create or update AWS kms key.

Update limitations:
Policy can be updated, but cannot be cleared once set.
multi_region, key_usage and key_spec cannot be updated
enable_key_rotation, cannot be enabled on asymmetric KMS keys.

Args:
    hub:
    ctx:
    name(str): A name of the kms key
    resource_id(str, Optional): AWS KMS Key ID.
    description(str, Optional): description of the key
    key_usage(str, Default: 'ENCRYPT_DECRYPT'): optional values: 'SIGN_VERIFY'|'ENCRYPT_DECRYPT'
    key_spec(str, Default: "SYMMETRIC_DEFAULT"): optional values: 'RSA_2048'|'RSA_3072'|
        'RSA_4096'|'ECC_NIST_P256'|'ECC_NIST_P384'|'ECC_NIST_P521'|'ECC_SECG_P256K1'|'SYMMETRIC_DEFAULT'
    key_state(str: Default: Enabled): by default key is enabled. Use 'Disabled' to disable the key.
    origin(str, Default: "AWS_KMS"): optional values: 'AWS_KMS'|'EXTERNAL'|'AWS_CLOUDHSM'
    multi_region(bool, Default: False):
    policy(str, Optional): a default policy is created for each key
    bypass_policy_lockout_safety_check(bool, Default = False): bypass policy safety check, should be true when
        policy is specified or key creation fails with this error:
        "The new key policy will not allow you to update the key policy in the future.
        This field is not returned by 'describe'.
    enable_key_rotation(bool, Default = False): by default new key created with key rotation disabled.
    tags(List or Dict, optional): list of tags in the format of [{"TagKey": tag-key, "TagValue": tag-value}] or dict in the format of
            {tag-key: tag-value} The tags to assign to the key. Defaults to None.
    timeout(Dict, optional): Timeout configuration for update of AWS KMS key.
        * update (string) -- Timeout configuration for update of a KMS key
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- Max attempts of waiting for change.

Request Syntax:
    [key-resource-id]:
      aws.kms.key.present:
      - resource_id: 'string'
      - description: 'string'
      - key_state: 'string'
      - key_usage: 'string'
      - key_spec: 'string'
      - multi_region: 'boolean'
      - bypass_policy_lockout_safety_check: 'boolean'
      - policy: 'string'
      - tags:
        - TagKey: 'string'
          TagValue: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        new-key:
            aws.kms.key.present:
                - key_state: Enabled
                - description: key-with-policy-and-tags
                - key_usage: ENCRYPT_DECRYPT
                - key_spec: SYMMETRIC_DEFAULT
                - multi_region: false
                - bypass_policy_lockout_safety_check: true
                - policy: "{\"Version\":\"2012-10-17\",\"Statement\":[{\"Sid\":\"EnableIAMUserPermissions\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":\"arn:aws:iam::537227425989:root\"},\"Action\":[\"kms:Create*\",\"kms:Describe*\",\"kms:Enable*\"],\"Resource\":\"*\"}]}"
                - tags:
                    - TagKey: test-key
                      TagValue: test-value
                    - TagKey: test-key-1
                      TagValue: test-key-1
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.kms.key](https://docs.idemproject.io/idem-aws/en/latest/ref/states/kms/key.html).
