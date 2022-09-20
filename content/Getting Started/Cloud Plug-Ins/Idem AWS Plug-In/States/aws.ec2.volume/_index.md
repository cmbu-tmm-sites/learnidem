---
title: "aws.ec2.volume"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deregisters the specified Volume

    Deletes the specified EBS volume. The volume must be in the available state (not attached to an instance). The
    volume can remain in the deleting state for several minutes. For more information, see Delete an Amazon EBS
    volume in the Amazon Elastic Compute Cloud User Guide.

    Args:
        name (str): An Idem name of the resource.
        resource_id (str): Volume ID.

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            resource_is_absent:
              aws_auto.ec2.volume.absent:
                - name: idem-test-volume
                - resource_id: volume-123456789
                - volume_id: volume-123456789
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Describes the specified EBS volumes or all of your EBS volumes. If you are describing a long list of volumes, we
recommend that you paginate the output to make the list more manageable. The MaxResults parameter sets the
maximum number of results returned in a single page. If the list of results exceeds your MaxResults value, then
that number of results is returned along with a NextToken value that can be passed to a subsequent
DescribeVolumes request to retrieve the remaining results. For more information about EBS volumes, see Amazon
EBS volumes in the Amazon Elastic Compute Cloud User Guide.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws_auto.ec2.volume
```
{{< /tab >}}

{{< tab "present" >}}

```
Register an AWS Volume

    Creates an EBS volume that can be attached to an instance in the same Availability Zone. You can create a new
    empty volume or restore a volume from an EBS snapshot. Any Amazon Web Services Marketplace product codes from
    the snapshot are propagated to the volume. You can create encrypted volumes. Encrypted volumes must be attached
    to instances that support Amazon EBS encryption. Volumes that are created from encrypted snapshots are also
    automatically encrypted. For more information, see Amazon EBS encryption in the Amazon Elastic Compute Cloud
    User Guide. You can tag your volumes during creation. For more information, see Tag your Amazon EC2 resources in
    the Amazon Elastic Compute Cloud User Guide. For more information, see Create an Amazon EBS volume in the Amazon
    Elastic Compute Cloud User Guide.

    Args:
        name (str):
            An Idem name of the volume resource.

        resource_id (str, optional):
            The AWS volume_id of the Volume. Defaults to None.

        availability_zone (str):
            The Availability Zone in which to create the volume.

        encrypted (bool, optional):
            Indicates whether the volume should be encrypted. The effect of setting the encryption state to
            true depends on the volume origin (new or from a snapshot), starting encryption state,
            ownership, and whether encryption by default is enabled. For more information, see Encryption by
            default in the Amazon Elastic Compute Cloud User Guide. Encrypted Amazon EBS volumes must be
            attached to instances that support Amazon EBS encryption. For more information, see Supported
            instance types. Defaults to None.

        iops (int, optional):
            The number of I/O operations per second (IOPS). For gp3, io1, and io2 volumes, this represents
            the number of IOPS that are provisioned for the volume. For gp2 volumes, this represents the
            baseline performance of the volume and the rate at which the volume accumulates I/O credits for
            bursting. The following are the supported values for each volume type:    gp3: 3,000-16,000 IOPS
            io1: 100-64,000 IOPS    io2: 100-64,000 IOPS    io1 and io2 volumes support up to 64,000 IOPS
            only on Instances built on the Nitro System. Other instance families support performance up to
            32,000 IOPS. This parameter is required for io1 and io2 volumes. The default for gp3 volumes is
            3,000 IOPS. This parameter is not supported for gp2, st1, sc1, or standard volumes. Defaults to None.

        kms_key_id (str, optional):
            The identifier of the Key Management Service (KMS) KMS key to use for Amazon EBS encryption. If
            this parameter is not specified, your KMS key for Amazon EBS is used. If KmsKeyId is specified,
            the encrypted state must be true. You can specify the KMS key using any of the following:   Key
            ID. For example, 1234abcd-12ab-34cd-56ef-1234567890ab.   Key alias. For example,
            alias/ExampleAlias.   Key ARN. For example, arn:aws:kms:us-
            east-1:012345678910:key/1234abcd-12ab-34cd-56ef-1234567890ab.   Alias ARN. For example,
            arn:aws:kms:us-east-1:012345678910:alias/ExampleAlias.   Amazon Web Services authenticates the
            KMS key asynchronously. Therefore, if you specify an ID, alias, or ARN that is not valid, the
            action can appear to complete, but eventually fails. Defaults to None.

        outpost_arn (str, optional):
            The Amazon Resource Name (ARN) of the Outpost. Defaults to None.

        size (int, optional):
            The size of the volume, in GiBs. You must specify either a snapshot ID or a volume size. If you
            specify a snapshot, the default is the snapshot size. You can specify a volume size that is
            equal to or larger than the snapshot size. The following are the supported volumes sizes for
            each volume type:    gp2 and gp3: 1-16,384    io1 and io2: 4-16,384    st1 and sc1: 125-16,384
            standard: 1-1,024. Defaults to None.

        snapshot_id (str, optional):
            The snapshot from which to create the volume. You must specify either a snapshot ID or a volume
            size. Defaults to None.

        volume_type (str, optional): ]
            The volume type. This parameter can be one of the following values:   General Purpose SSD: gp2 |
            gp3    Provisioned IOPS SSD: io1 | io2    Throughput Optimized HDD: st1    Cold HDD: sc1
            Magnetic: standard    For more information, see Amazon EBS volume types in the Amazon Elastic
            Compute Cloud User Guide. Default: gp2. Defaults to None.

        multi_attach_enabled (bool, optional):
            Indicates whether to enable Amazon EBS Multi-Attach. If you enable Multi-Attach, you can attach
            the volume to up to 16 Instances built on the Nitro System in the same Availability Zone. This
            parameter is supported with io1 and io2 volumes only. For more information, see  Amazon EBS
            Multi-Attach in the Amazon Elastic Compute Cloud User Guide. Defaults to None.

        throughput (int, optional):
            The throughput to provision for a volume, with a maximum of 1,000 MiB/s. This parameter is valid
            only for gp3 volumes. Valid Range: Minimum value of 125. Maximum value of 1000. Defaults to None.

        tags (dict, optional):
            dict in the format of ``{tag-key: tag-value}``. Defaults to None.

            * Key (str):
                The key of the tag. Tag keys are case-sensitive and accept a maximum of 127 Unicode characters. May not begin with aws: .

            * Value (str):
                The value of the tag. Tag values are case-sensitive and accept a maximum of 255 Unicode characters.

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            resource_is_present:
              aws_auto.ec2.volume.present:
                - name: some-volume-ARN
                - snapshot_id: some-snapshot-ARN
                - volume_type: standard
                - availability_zone: us-east-1a
                - size: 1
                - encrypted: True
                - tags:
                  - Key: name
                    Value: some-volume-ARN
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.volume](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/volume.html).
