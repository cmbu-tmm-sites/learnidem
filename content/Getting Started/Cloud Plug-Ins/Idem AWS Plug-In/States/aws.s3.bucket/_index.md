---
title: "aws.s3.bucket"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified s3 bucket.

Args:
    name(Text): The Idem name of the s3 bucket.
    resource_id(Text, Optional): AWS S3 Bucket name

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        bucket-5435423646-456464:
          aws.s3.bucket.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Obtain S3 buckets under the given context for any user.
:param hub:
:param ctx:
:return:
```
{{< /tab >}}

{{< tab "present" >}}

```
    name (Text) -- An Idem name of the resource.
    create_bucket_configuration(Dict[str, Any], optional): The configuration information for the bucket. Defaults to None.
        LocationConstraint (str, optional): Specifies the Region where the bucket will be created. If you don't specify a Region, the bucket
            is created in the US East (N. Virginia) Region (us-east-1).
    resource_id(Text, optional): AWS S3 Bucket name
    acl (Text, optional) -- The canned ACL to apply to the bucket.
    grant_full_control (Text, optional) --
        Allows grantee the read, write, read ACP, and write ACP permissions on the bucket.
    grant_read (Text, optional) --
        Allows grantee to list the objects in the bucket.
    grant_read_acp (Text, optional) --
        Allows grantee to read the bucket ACL.
    grant_write (Text, optional) --
        Allows grantee to create new objects in the bucket.
        For the bucket and object owners of existing objects, also allows deletions and overwrites of those objects.
    grant_write_acp (Text, optional) --
        Allows grantee to write the ACL for the applicable bucket.
    object_lock_enabled_for_bucket (boolean, optional) --
        Specifies whether you want S3 Object Lock to be enabled for the new bucket.
        ObjectLockConfiguration (dict) --
    The Object Lock configuration that you want to apply to the specified bucket.
        ObjectLockEnabled (string) -- Indicates whether this bucket has an Object Lock configuration enabled. Enable ObjectLockEnabled
                                    when you apply ObjectLockConfiguration to a bucket.
        Rule (dict) -- Specifies the Object Lock rule for the specified object. Enable the this rule when you apply ObjectLockConfiguration
                        to a bucket. Bucket settings require both a mode and a period. The period can be either Days or Years but you must select one.
                        You cannot specify Days and Years at the same time.
            DefaultRetention (dict) -- The default Object Lock retention mode and period that you want to apply to new objects placed
                                in the specified bucket. Bucket settings require both a mode and a period. The period can be either Days or Years
                                but you must select one. You cannot specify Days and Years at the same time.
                Mode (string) -- The default Object Lock retention mode you want to apply to new objects placed in the specified bucket.
                                Must be used with either Days or Years .
                Days (integer) -- The number of days that you want to specify for the default retention period. Must be used with Mode .
                Years (integer) -- The number of years that you want to specify for the default retention period. Must be used with Mode .
    object_ownership (Text, optional) --
        The container element for object ownership for a bucket's ownership controls.
        BucketOwnerPreferred -
            Objects uploaded to the bucket change ownership to the bucket owner if
            the objects are uploaded with the bucket-owner-full-control canned ACL.
        ObjectWriter -
            The uploading account will own the object if the object is uploaded
            with the bucket-owner-full-control canned ACL.
        BucketOwnerEnforced -
            Access control lists (ACLs) are disabled and no longer affect permissions.
            The bucket owner automatically owns and has full control over every object
            in the bucket. The bucket only accepts PUT requests that don't specify an
            ACL or bucket owner full control ACLs, such as the bucket-owner-full-control
            canned ACL or an equivalent form of this ACL expressed in the XML format.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the bucket.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value(str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.

Request Syntax:
    [s3-resource-id]::
      aws.s3.bucket.present:
        - acl: 'private'|'public-read'|'public-read-write'|'authenticated-read'
        - bucket: string
        - create_bucket_configuration:
            LocationConstraint: string
        - grant_full_control: string
        - grant_read: string
        - grant_read_acp: string
        - grant_write: string
        - grant_write_acp: string
        - object_lock_enabled_for_bucket: True|False
        - object_lock_configuration: 'dict'
            ObjectLockEnabled: 'string'
              Rule:
                DefaultRetention: 'dict'
                  Mode: 'string'
                  Days: 'integer'
        - object_ownership: BucketOwnerPreferred'|'ObjectWriter'|'BucketOwnerEnforced'
        - tags:
            - Key: 'string'
              Value: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        test_bucket-bb7bb32e9533:
          aws.s3.bucket.present:
            - name: test_bucket-bb7bb32e9533
            - acl: 'private'
            - create_bucket_configuration:
                LocationConstraint: 'sa-east-1'
            - object_lock_enabled_for_bucket: True
            - object_lock_configuration:
                ObjectLockEnabled: 'Enabled'
                Rule:
                  DefaultRetention:
                    Mode: GOVERNANCE
                    Days: 1
            - object_ownership: 'BucketOwnerEnforced'
            - tags:
                - Key: Name1
                  Value: s3-test1
                - Key: Name2
                  Value: s3-test2
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.s3.bucket](https://docs.idemproject.io/idem-aws/en/latest/ref/states/s3/bucket.html).
