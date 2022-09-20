---
title: "aws.s3.bucket_lifecycle"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes a lifecycle configuration from an S3 bucket resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): The name of the S3 bucket in Amazon Web Services.
        Idem automatically considers this resource being absent if this field is not specified.
    timeout(Dict, optional): Timeout configuration for S3 bucket lifecycle configuration.
        * delete (string): Timeout configuration for deleting the S3 bucket lifecycle configuration.
            * delay (int, optional): The amount of time in seconds to wait between attempts. Defaults to 4 seconds.
            * max_attempts (int, optional): Maximum attempts of waiting for the deletion. Defaults to 30 attempts.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_s3_bucket_lifecycle:
          aws.s3.bucket_lifecycle.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the lifecycle configuration for each S3 bucket under the given AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.s3.bucket_lifecycle
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a lifecycle configuration for an S3 bucket resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): The name of the S3 bucket in Amazon Web Services. It must be equal to the bucket parameter.
    bucket(string): The name of the S3 bucket in Amazon Web Services.
    lifecycle_configuration(Dict[str, Any], optional): The lifecycle configuration for the S3 bucket. Defaults to None.
        * Rules (List[Dict[str, Any]]): Specifies lifecycle configuration rules for an Amazon S3 bucket.
            * ID (str): Unique identifier for the rule. The value can't be longer than 255 characters.
            * Status (str): If Enabled, the rule is currently being applied. If Disabled, the rule is not currently being
                applied.
            * Filter (Dict[str, Any]): The Filter is used to identify objects that a Lifecycle Rule applies to. A Filter must have exactly one of Prefix , Tag , or And specified.
                * Prefix (str, optional): Prefix identifying one or more objects to which the rule applies.
                * Tag (Dict[str, Any], optional): his tag must exist in the object's tag set in order for the rule to apply.
                    * Key (str): Name of the object key.
                    * Value (str): Value of the tag.
                * ObjectSizeGreaterThan (int, optional): Minimum object size to which the rule applies.
                * ObjectSizeLessThan (int, optional): Maximum object size to which the rule applies.
                * And (Dict[str, Any], optional): This is used in a Lifecycle Rule Filter to apply a logical AND to two or more predicates. The Lifecycle Rule will apply to any object matching all of the predicates configured inside the And operator.
                    * Prefix (str, optional): Prefix identifying one or more objects to which the rule applies.
                    * Tag (Dict[str, Any], optional): his tag must exist in the object's tag set in order for the rule to apply.
                        * Key (str): Name of the object key.
                        * Value (str): Value of the tag.
                    * ObjectSizeGreaterThan (int, optional): Minimum object size to which the rule applies.
                    * ObjectSizeLessThan (int, optional): Maximum object size to which the rule applies.
            * Expiration (Dict[str, Any], optional): Specifies the expiration for the lifecycle of the object.
                * Date (Text, optional): Indicates at what date the object is to be moved or deleted. Should be in GMT ISO 8601 Format.
                * Days (int, optional): Indicates the lifetime, in days, of the objects that are subject to the rule. The value must be
                    a non-zero positive integer.
                * ExpiredObjectDeleteMarker (bool, optional): Indicates whether Amazon S3 will remove a delete marker with no noncurrent versions. If set to
                    true, the delete marker will be expired; if set to false the policy takes no action. This cannot
                    be specified with Days or Date in a Lifecycle Expiration Policy.
            * Transition (Dict[str, Any], optional): Specifies when an object transitions to a specified storage class. For more information about
                Amazon S3 lifecycle configuration rules, see Transitioning Objects Using Amazon S3 Lifecycle in
                the Amazon S3 User Guide.
                * Date (Text, optional): Indicates when objects are transitioned to the specified storage class. The date value must be
                    in ISO 8601 format. The time is always midnight UTC.
                * Days (int, optional): Indicates the number of days after creation when objects are transitioned to the specified
                    storage class. The value must be a positive integer.
                * StorageClass (str, optional): The storage class to which you want the object to transition.
            * NoncurrentVersionTransition (Dict[str, Any], optional): Container for the transition rule that describes when noncurrent objects transition to the
                STANDARD_IA, ONEZONE_IA, INTELLIGENT_TIERING, GLACIER_IR, GLACIER, or DEEP_ARCHIVE storage
                class. If your bucket is versioning-enabled (or versioning is suspended), you can set this
                action to request that Amazon S3 transition noncurrent object versions to the STANDARD_IA,
                ONEZONE_IA, INTELLIGENT_TIERING, GLACIER_IR, GLACIER, or DEEP_ARCHIVE storage class at a
                specific period in the object's lifetime.
                * NoncurrentDays (int, optional): Specifies the number of days an object is noncurrent before Amazon S3 can perform the associated
                    action. For information about the noncurrent days calculations, see How Amazon S3 Calculates How
                    Long an Object Has Been Noncurrent in the Amazon S3 User Guide.
                * StorageClass (str, optional): The class of storage used to store the object.
                * NewerNoncurrentVersions (int, optional): Specifies how many noncurrent versions Amazon S3 will retain. If there are this many more recent
                    noncurrent versions, Amazon S3 will take the associated action. For more information about
                    noncurrent versions, see Lifecycle configuration elements in the Amazon S3 User Guide.
            * NoncurrentVersionExpiration (Dict[str, Any], optional): Specifies when noncurrent object versions expire. Upon expiration, Amazon S3 permanently deletes
                the noncurrent object versions. You set this lifecycle configuration action on a bucket that has
                versioning enabled (or suspended) to request that Amazon S3 delete noncurrent object versions at
                a specific period in the object's lifetime.
                * NoncurrentDays (int, optional): Specifies the number of days an object is noncurrent before Amazon S3 can perform the associated
                    action. The value must be a non-zero positive integer. For information about the noncurrent days
                    calculations, see How Amazon S3 Calculates When an Object Became Noncurrent in the Amazon S3
                    User Guide.
                * NewerNoncurrentVersions (int, optional): Specifies how many noncurrent versions Amazon S3 will retain. If there are this many more recent
                    noncurrent versions, Amazon S3 will take the associated action. For more information about
                    noncurrent versions, see Lifecycle configuration elements in the Amazon S3 User Guide.
            * AbortIncompleteMultipartUpload (Dict[str, Any], optional): Specifies the days since the initiation of an incomplete multipart upload that Amazon S3 will
                wait before permanently removing all parts of the upload. For more information, see  Aborting
                Incomplete Multipart Uploads Using a Bucket Lifecycle Policy in the Amazon S3 User Guide.
                * DaysAfterInitiation (int, optional): Specifies the number of days after which Amazon S3 aborts an incomplete multipart upload.
    timeout(Dict, optional): Timeout configuration for S3 bucket lifecycle configuration.
        * update (string): Timeout configuration for updating the S3 bucket lifecycle configuration.
            * delay (int, optional): The amount of time in seconds to wait between attempts. Defaults to 4 seconds.
            * max_attempts (int, optional): Maximum attempts of waiting for the update. Defaults to 30 attempts.

Request Syntax:
    [idem_test_aws_s3_bucket_lifecycle]:
      aws.s3.bucket_lifecycle.present:
        - name: 'string'
        - bucket: 'string'
        - lifecycle_configuration: {'string': []}

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_s3_bucket_lifecycle:
          aws.s3.bucket_lifecycle.present:
            - name: value
            - bucket: value
            - lifecycle_configuration:
                Rules:
                - ID: 'string'
                  Status: 'Enabled'|'Disabled'
                  Filter:
                    Prefix: ''
                  Expiration:
                    Date: datetime(2015, 1, 1)
                    Days: 123
                    ExpiredObjectDeleteMarker: True|False
                  Transition:
                    Date: datetime(2015, 1, 1)
                    Days: 123
                    StorageClass: 'GLACIER'|'STANDARD_IA'|'ONEZONE_IA'|'INTELLIGENT_TIERING'|'DEEP_ARCHIVE'|'GLACIER_IR'
                  NoncurrentVersionTransitions:
                    - NoncurrentDays: 123
                      StorageClass: 'GLACIER'|'STANDARD_IA'|'ONEZONE_IA'|'INTELLIGENT_TIERING'|'DEEP_ARCHIVE'|'GLACIER_IR'
                      NewerNoncurrentVersions: 123
                  NoncurrentVersionExpiration:
                    NoncurrentDays: 123
                    NewerNoncurrentVersions: 123
                  AbortIncompleteMultipartUpload:
                    DaysAfterInitiation: 123
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.s3.bucket_lifecycle](https://docs.idemproject.io/idem-aws/en/latest/ref/states/s3/bucket_lifecycle.html).
