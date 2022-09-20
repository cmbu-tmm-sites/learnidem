---
title: "aws.s3.bucket_versioning"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Suspends a versioning configuration for an S3 bucket resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): The name of the S3 bucket in Amazon Web Services.
        Idem automatically considers this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_s3_bucket_versioning:
          aws.s3.bucket_versioning.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the versioning configuration for each S3 bucket under the given AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.s3.bucket_versioning
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a versioning configuration for an S3 bucket resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): The name of the S3 bucket in Amazon Web Services. It must be equal to the bucket parameter.
    bucket(string): The name of the S3 bucket in Amazon Web Services.
    mfa_delete(string, optional): The versioning state of the bucket. Defaults to "Disabled"
    status(string, optional): Specifies whether MFA delete is enabled in the bucket versioning configuration. Defaults to "Enabled".

Request Syntax:
    [idem_test_aws_s3_bucket_versioning]:
      aws.s3.bucket_versioning.present:
        - name: 'string'
        - bucket: 'string'
        - mfa_delete: 'string'
        - status: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_s3_bucket_versioning:
          aws.s3.bucket_versioning.present:
            - name: value
            - bucket: value
            - mfa_delete: 'Enabled'|'Disabled'
            - status: 'Enabled'|'Suspended'
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.s3.bucket_versioning](https://docs.idemproject.io/idem-aws/en/latest/ref/states/s3/bucket_versioning.html).
