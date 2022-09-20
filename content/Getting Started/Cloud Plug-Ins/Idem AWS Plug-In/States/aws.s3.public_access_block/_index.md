---
title: "aws.s3.public_access_block"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Removes the PublicAccessBlock configuration for an Amazon S3 bucket.
To use this operation, you must have the s3:PutBucketPublicAccessBlock permission.

Args:
    name(Text): The name of public block configuration
    resource_id (Text): Bucket name to identify the resource
    expected_bucket_owner (Text, optional): The account ID of the expected bucket owner. If the bucket is owned by a different account, the request will fail with an HTTP 403 (Access Denied) error.

Returns:
    Dict[str, Any]

Request Syntax:
    resource_name:
      aws.s3.public_access_block.absent:
        - name: string
        - resource_id: string
        - expected_bucket_owner: string

Examples:

    .. code-block:: sls

        test-bucket-1232323-public-access-block:
          aws.s3.public_access_block.absent:
          - name: test-bucket-1232323-public-access-block
          - resource_id: test-bucket-1232323
          - expected_bucket_owner: 1234567890
```
{{< /tab >}}

{{< tab "describe" >}}

```
Obtain S3 public access block configuration for each bucket under the given context for any user.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.s3.public_access_block
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates or modifies the PublicAccessBlock configuration for an Amazon S3 bucket.
To use this operation, the calling entity must have the s3:PutBucketPublicAccessBlock permission.

Args:
  hub:
  ctx:
  name(Text): The name of the bucket public access block configuration.
  bucket(Text): Bucket name to identify the resource
    public_access_block_configuration(Dict[str, Any]): The PublicAccessBlock configuration that you want to apply to this Amazon S3 bucket. You can
        enable the configuration options in any combination. For more information about when Amazon S3
        considers a bucket or object public, see The Meaning of "Public" in the Amazon S3 User Guide.
        * BlockPublicAcls (bool, optional): Specifies whether Amazon S3 should block public access control lists (ACLs) for this bucket and
            objects in this bucket. Setting this element to TRUE causes the following behavior:   PUT Bucket
            ACL and PUT Object ACL calls fail if the specified ACL is public.   PUT Object calls fail if the
            request includes a public ACL.   PUT Bucket calls fail if the request includes a public ACL.
            Enabling this setting doesn't affect existing policies or ACLs.
        * IgnorePublicAcls (bool, optional): Specifies whether Amazon S3 should ignore public ACLs for this bucket and objects in this
            bucket. Setting this element to TRUE causes Amazon S3 to ignore all public ACLs on this bucket
            and objects in this bucket. Enabling this setting doesn't affect the persistence of any existing
            ACLs and doesn't prevent new public ACLs from being set.
        * BlockPublicPolicy (bool, optional): Specifies whether Amazon S3 should block public bucket policies for this bucket. Setting this
            element to TRUE causes Amazon S3 to reject calls to PUT Bucket policy if the specified bucket
            policy allows public access.  Enabling this setting doesn't affect existing bucket policies.
        * RestrictPublicBuckets (bool, optional): Specifies whether Amazon S3 should restrict public bucket policies for this bucket. Setting this
            element to TRUE restricts access to this bucket to only Amazon Web Service principals and
            authorized users within this account if the bucket has a public policy. Enabling this setting
            doesn't affect previously stored bucket policies, except that public and cross-account access
            within any public bucket policy, including non-public delegation to specific accounts, is
            blocked.
  expected_bucket_owner (Text, optional): The account ID of the expected bucket owner. If the bucket is owned by a different account, the request will fail with an HTTP 403 (Access Denied) error.
  resource_id (Text, Optional): Bucket name to identify the resource

Request Syntax:
  resource_name:
    aws.s3.public_access_block.present:
      - name: string
      - bucket: string
      - public_access_block_configuration: Dict
      - expected_bucket_owner: string
      - resource_id: string

Returns:
  Dict[str, Any]

Examples:

  .. code-block:: sls

  test-bucket-1232323-public-access-block:
    aws.s3.public_access_block.present:
      - name: test-bucket-1232323-public-access-block
      - bucket: test-bucket-1232323
      - public_access_block_configuration: {"BlockPublicAcls": true, "IgnorePublicAcls": true, "BlockPublicPolicy": true, "RestrictPublicBuckets": true }
      - expected_bucket_owner: 1234567890
      - resource_id: test-bucket-1232323
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.s3.public_access_block](https://docs.idemproject.io/idem-aws/en/latest/ref/states/s3/public_access_block.html).
