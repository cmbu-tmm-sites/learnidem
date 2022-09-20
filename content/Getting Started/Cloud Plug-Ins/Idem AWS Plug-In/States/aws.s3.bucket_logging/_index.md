---
title: "aws.s3.bucket_logging"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the logging configuration for an S3 bucket.

    This action enables you to delete logging configurations from a bucket using a single HTTP request.
    If you know the object keys that you want to delete, then this action provides a suitable alternative to sending
    individual delete requests, reducing per-request overhead. For each configuration, Amazon S3 performs a delete
    action and returns the result of that delete, success, or failure, in the response.

    Args:
        name(str): Idem name of the bucket.
        resource_id(Text): Name of the bucket on which logging needs to be deleted.

    Request Syntax:
        .. code-block:: sls

            [bucket_name]-logging:
              aws.s3.bucket_logging.absent:
                - name: "string"
                - resource_id: "string"

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            test-bucket-logging:
              aws.s3.bucket_logging.absent:
                - name: test-bucket
                - resource_id: test-bucket
```
{{< /tab >}}

{{< tab "describe" >}}

```
Gets information about the S3 bucket logging parameters.

    Describe the resource in a way that can be recreated/managed with the corresponding "present" function.

    Returns:
        Dict[str, Dict[str, Any]]

    Examples:
        .. code-block:: bash

            $ idem describe aws.s3.bucket_logging
```
{{< /tab >}}

{{< tab "present" >}}

```
Create/Update the logging parameter for S3 bucket.

    Set the logging parameters for a bucket and to specify permissions for who can view and modify the logging
    parameters. All logs are saved to bucket in the same Amazon Web Services Region as the source bucket. To set
    the logging status of a bucket, you must be the bucket owner. The bucket owner is automatically granted
    FULL_CONTROL to all logs. You use the Grantee request element to grant access to other people. The Permissions
    request element specifies the kind of access the grantee has to the logs.

    Args:
        name(str):
            An Idem name of the resource.
            This is also used as the name of the bucket for which to set the logging parameters during resource creation.

        resource_id(str, optional):
            Name of the S3 bucket.

        bucket_logging_status(dict):
            Container for logging status information.

            * LoggingEnabled (dict, optional):
                Describes where logs are stored and the prefix that Amazon S3 assigns to all log object keys for a bucket.

                * TargetBucket (str):
                    Specifies the bucket where you want Amazon S3 to store server access logs.
                    You can have your logs delivered to any bucket that you own, including the same bucket that is being
                    logged. You can also configure multiple buckets to deliver their logs to the same target bucket.
                    In this case, you should choose a different TargetPrefix for each source bucket so that the delivered
                    log files can be distinguished by key.

                * TargetGrants (list, optional):
                    Container for granting information.
                    Buckets that use the bucket owner enforced setting for Object Ownership don't support target grants.

                    * Grantee (dict, optional):
                        Container for the person being granted permissions.

                        * DisplayName (str, optional):
                            Screen name of the grantee.

                        * EmailAddress (str, optional):
                            Email address of the grantee.

                        * ID (str, optional):
                            The canonical user ID of the grantee.

                        * Type (str):
                            Type of grantee.

                        * URI (str, optional):
                            URI of the grantee group.

                    * Permission (str, optional):
                        Logging permissions assigned to the grantee for the bucket.

                * TargetPrefix (str):
                    A prefix for all log object keys. If you store log files from multiple Amazon S3 buckets in a
                    single bucket, you can use a prefix to distinguish which log files came from which bucket.

    Request Syntax:
        .. code-block:: sls

            [bucket_name]-logging:
              aws.s3.bucket_logging.present:
              - name: "string"
              - resource_id: "string"
              - bucket_logging_status:
                  LoggingEnabled:
                    TargetBucket: "string"
                    TargetGrants:
                    - Grantee:
                        DisplayName: [string]
                        EmailAddress: [string]
                        ID: [string]
                        Type: [string]
                        URI: [string]
                      Permission: [string]
                    TargetPrefix: [string]

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            test-bucket-logging:
              aws.s3.bucket_logging.present:
                - name: test-bucket
                - bucket_logging_status:
                    LoggingEnabled:
                        TargetBucket: test-bucket
                        TargetGrants:
                        - Grantee:
                            URI: http://acs.amazonaws.com/groups/s3/LogDelivery
                            Type: Group
                          Permission: WRITE
                        - Grantee:
                            URI: http://acs.amazonaws.com/groups/s3/LogDelivery
                            Type: Group
                          Permission: READ_ACP
                        TargetPrefix: logs
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.s3.bucket_logging](https://docs.idemproject.io/idem-aws/en/latest/ref/states/s3/bucket_logging.html).
