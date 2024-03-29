---
title: "aws.efs.file_system"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes a file system, permanently severing access to its contents. Upon return, the file system no longer
exists and you can't access any contents of the deleted file system.  You can't delete a file system that is in
use. That is, if the file system has any mount targets, you must first delete them. For more information, see
DescribeMountTargets and DeleteMountTarget.   The DeleteFileSystem call returns while the file system state is
still deleting. You can check the file system deletion status by calling the DescribeFileSystems operation,
which returns a list of file systems in your account. If you pass file system ID or creation token for the
deleted file system, the DescribeFileSystems returns a 404 FileSystemNotFound error.  This operation requires
permissions for the elasticfilesystem:DeleteFileSystem action.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text, optional): EFS file system ID.

Request Syntax:
   [file-system-resource-id]:
        aws.efs.file_system.absent:
        - name: 'string'
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        fs-xxxxxxxxx:
          aws.efs.file_system.absent:
          - name: efs-name
          - resource_id: fs-xxxxxxxxx
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Returns the description of a specific Amazon EFS file system if either the file system CreationToken or the
FileSystemId is provided. Otherwise, it returns descriptions of all file systems owned by the caller's Amazon
Web Services account in the Amazon Web Services Region of the endpoint that you're calling. When retrieving all
file system descriptions, you can optionally specify the MaxItems parameter to limit the number of descriptions
in a response. Currently, this number is automatically set to 10. If more file system descriptions remain,
Amazon EFS returns a NextMarker, an opaque token, in the response. In this case, you should send a subsequent
request with the Marker request parameter set to the value of NextMarker.  To retrieve a list of your file
system descriptions, this operation is used in an iterative process, where DescribeFileSystems is called first
without the Marker and then the operation continues to call it with the Marker parameter set to the value of the
NextMarker from the previous response until the response has no NextMarker.   The order of file systems returned
in the response of one DescribeFileSystems call and the order of file systems returned across the responses of a
multi-call iteration is unspecified.   This operation requires permissions for the
elasticfilesystem:DescribeFileSystems action.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.efs.file_system
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a new, empty file system. The operation requires a creation token in the request that Amazon EFS uses to
ensure idempotent creation (calling the operation with same creation token has no effect). If a file system does
not currently exist that is owned by the caller's Amazon Web Services account with the specified creation token,
this operation does the following:   Creates a new, empty file system. The file system will have an Amazon EFS
assigned ID, and an initial lifecycle state creating.   Returns with the description of the created file system.
Otherwise, this operation returns a FileSystemAlreadyExists error with the ID of the existing file system.  For
basic use cases, you can use a randomly generated UUID for the creation token.   The idempotent operation allows
you to retry a CreateFileSystem call without risk of creating an extra file system. This can happen when an
initial call fails in a way that leaves it uncertain whether or not a file system was actually created. An
example might be that a transport level timeout occurred or your connection was reset. As long as you use the
same creation token, if the initial call had succeeded in creating a file system, the client can learn of its
existence from the FileSystemAlreadyExists error. For more information, see Creating a file system in the Amazon
EFS User Guide.  The CreateFileSystem call returns while the file system's lifecycle state is still creating.
You can check the file system creation status by calling the DescribeFileSystems operation, which among other
things returns the file system state.  This operation accepts an optional PerformanceMode parameter that you
choose for your file system. We recommend generalPurpose performance mode for most file systems. File systems
using the maxIO performance mode can scale to higher levels of aggregate throughput and operations per second
with a tradeoff of slightly higher latencies for most file operations. The performance mode can't be changed
after the file system has been created. For more information, see Amazon EFS performance modes. You can set the
throughput mode for the file system using the ThroughputMode parameter. After the file system is fully created,
Amazon EFS sets its lifecycle state to available, at which point you can create one or more mount targets for
the file system in your VPC. For more information, see CreateMountTarget. You mount your Amazon EFS file system
on an EC2 instances in your VPC by using the mount target. For more information, see Amazon EFS: How it Works.
This operation requires permissions for the elasticfilesystem:CreateFileSystem action.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text, optional): EFS file system ID.
    creation_token(Text): A string of up to 64 ASCII characters. Amazon EFS uses this to ensure idempotent creation.
    performance_mode(Text, optional): The performance mode of the file system. We recommend generalPurpose performance mode for most
        file systems. File systems using the maxIO performance mode can scale to higher levels of
        aggregate throughput and operations per second with a tradeoff of slightly higher latencies for
        most file operations. The performance mode can't be changed after the file system has been
        created.  The maxIO mode is not supported on file systems using One Zone storage classes. Defaults to None.
    encrypted(bool, optional): A Boolean value that, if true, creates an encrypted file system. When creating an encrypted file
        system, you have the option of specifying an existing Key Management Service key (KMS key). If
        you don't specify a KMS key, then the default KMS key for Amazon EFS, /aws/elasticfilesystem, is
        used to protect the encrypted file system. Defaults to None.
    kms_key_id(Text, optional): The ID of the KMS key that you want to use to protect the encrypted file system. This parameter
        is only required if you want to use a non-default KMS key. If this parameter is not specified,
        the default KMS key for Amazon EFS is used. You can specify a KMS key ID using the following
        formats:   Key ID - A unique identifier of the key, for example
        1234abcd-12ab-34cd-56ef-1234567890ab.   ARN - An Amazon Resource Name (ARN) for the key, for
        example arn:aws:kms:us-west-2:111122223333:key/1234abcd-12ab-34cd-56ef-1234567890ab.   Key alias
        - A previously created display name for a key, for example alias/projectKey1.   Key alias ARN -
        An ARN for a key alias, for example arn:aws:kms:us-west-2:444455556666:alias/projectKey1.   If
        you use KmsKeyId, you must set the CreateFileSystemRequest$Encrypted parameter to true.  EFS
        accepts only symmetric KMS keys. You cannot use asymmetric KMS keys with Amazon EFS file
        systems. Defaults to None.
    throughput_mode(Text, optional): Specifies the throughput mode for the file system, either bursting or provisioned. If you set
        ThroughputMode to provisioned, you must also set a value for ProvisionedThroughputInMibps. After
        you create the file system, you can decrease your file system's throughput in Provisioned
        Throughput mode or change between the throughput modes, as long as it’s been more than 24 hours
        since the last decrease or throughput mode change. For more information, see Specifying
        throughput with provisioned mode in the Amazon EFS User Guide.  Default is bursting. Defaults to None.
    provisioned_throughput_in_mibps(float, optional): The throughput, measured in MiB/s, that you want to provision for a file system that you're
        creating. Valid values are 1-1024. Required if ThroughputMode is set to provisioned. The upper
        limit for throughput is 1024 MiB/s. To increase this limit, contact Amazon Web Services Support.
        For more information, see Amazon EFS quotas that you can increase in the Amazon EFS User Guide. Defaults to None.
    availability_zone_name(Text, optional): Used to create a file system that uses One Zone storage classes. It specifies the Amazon Web
        Services Availability Zone in which to create the file system. Use the format us-east-1a to
        specify the Availability Zone. For more information about One Zone storage classes, see Using
        EFS storage classes in the Amazon EFS User Guide.  One Zone storage classes are not available in
        all Availability Zones in Amazon Web Services Regions where Amazon EFS is available. Defaults to None.
    backup(bool, optional): Specifies whether automatic backups are enabled on the file system that you are creating. Set
        the value to true to enable automatic backups. If you are creating a file system that uses One
        Zone storage classes, automatic backups are enabled by default. For more information, see
        Automatic backups in the Amazon EFS User Guide. Default is false. However, if you specify an
        AvailabilityZoneName, the default is true.  Backup is not available in all Amazon Web Services
        Regions where Amazon EFS is available. Defaults to None.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the file system.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value(str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.

Request Syntax:
   [file-system-resource-id]:
        aws.efs.file_system.present:
        - name: 'string'
        - resource_id: 'string'
        - performance_mode: generalPurpose
        - encrypted: 'boolean'
        - kms_key_id: 'string'
        - creation_token: 'string'
        - throughput_mode: bursting/provisioned
        - provisioned_throughput_in_mibps: 'float'
        - availability_zone_name: 'string'
        - backup: 'boolean'
        - tags: List

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        fs-xxxxxxxxx:
          aws.efs.file_system.present:
          - name: efs-name
          - resource_id: fs-xxxxxxxxx
          - performance_mode: generalPurpose
          - encrypted: true
          - kms_key_id: arn:aws:kms:us-west-1:5xxxxxx:key/597f1c02-94dc-4c88-9088-f9aca5e39cf7
          - creation_token: xxx
          - throughput_mode: bursting
          - provisioned_throughput_in_mibps: 500.0
          - availability_zone_name: us-west-1b
          - backup: true
          - tags:
            - key: Name
              value: efs-name
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.efs.file_system](https://docs.idemproject.io/idem-aws/en/latest/ref/states/efs/file_system.html).
