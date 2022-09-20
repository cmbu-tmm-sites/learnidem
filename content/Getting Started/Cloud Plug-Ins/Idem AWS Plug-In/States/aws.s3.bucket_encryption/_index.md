---
title: "aws.s3.bucket_encryption"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an encryption configuration from an S3 bucket resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): The name of the S3 bucket in Amazon Web Services.
        Idem automatically considers this resource being absent if this field is not specified.
    timeout(Dict, optional): Timeout configuration for S3 bucket encryption configuration.
        * delete (string): Timeout configuration for deleting the S3 bucket encryption configuration.
            * delay (int, optional): The amount of time in seconds to wait between attempts. Defaults to 4 seconds.
            * max_attempts (int, optional): Maximum attempts of waiting for the deletion. Defaults to 30 attempts.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_s3_bucket_encryption:
          aws.s3.bucket_encryption.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the encryption configuration for each S3 bucket under the given AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.s3.bucket_encryption
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an encryption configuration for an S3 bucket resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): The name of the S3 bucket in Amazon Web Services. It must be equal to the bucket parameter.
    bucket(string): The name of the S3 bucket in Amazon Web Services.
    server_side_encryption_configuration(Dict): The server-side-encryption configuration for the S3 bucket.
    timeout(Dict, optional): Timeout configuration for S3 bucket encryption configuration.
        * update (string): Timeout configuration for updating the S3 bucket encryption configuration.
            * delay (int, optional): The amount of time in seconds to wait between attempts. Defaults to 4 seconds.
            * max_attempts (int, optional): Maximum attempts of waiting for the update. Defaults to 30 attempts.

Request Syntax:
    [idem_test_aws_s3_bucket_encryption]:
      aws.s3.bucket_encryption.present:
        - name: 'string'
        - bucket: 'string'
        - server_side_encryption_configuration: {'string': []}

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_s3_bucket_encryption:
          aws.s3.bucket_encryption.present:
            - name: value
            - bucket: value
            - server_side_encryption_configuration:
                Rules:
                - ApplyServerSideEncryptionByDefault:
                    SSEAlgorithm: 'AES256'|'aws:kms'
                    KMSMasterKeyID: 'string'
                  BucketKeyEnabled: True|False
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.s3.bucket_encryption](https://docs.idemproject.io/idem-aws/en/latest/ref/states/s3/bucket_encryption.html).
