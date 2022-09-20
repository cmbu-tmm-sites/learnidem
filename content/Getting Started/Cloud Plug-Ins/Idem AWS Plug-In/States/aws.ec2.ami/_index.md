---
title: "aws.ec2.ami"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deregisters the specified AMI.

    After you deregister an AMI, it can't be used to launch new instances.

    If you deregister an AMI that matches a Recycle Bin retention rule,
    the AMI is retained in the Recycle Bin for the specified retention period.
    For more information, see Recycle Bin in the Amazon Elastic Compute Cloud User Guide.

    When you deregister an AMI, it doesn't affect any instances that you've already launched from the AMI.
    You'll continue to incur usage costs for those instances until you terminate them.

    When you deregister an Amazon EBS-backed AMI,
    it doesn't affect the snapshot that was created for the root volume of the instance during the AMI creation process.
    When you deregister an instance store-backed AMI,
    it doesn't affect the files that you uploaded to Amazon S3 when you created the AMI.

    Args:
        name(str): The Idem name of the AMI.
        resource_id(str, optional): The AWS image_id.

    Request Syntax:
        .. code-block:: sls

            [ami-resource-id]:
              aws.ec2.ami.absent:
                - name: "string"
                - resource_id: "string"

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            idem-test-ami:
              aws.ec2.ami.absent:
                - name: idem-test-ami
                - resource_id: ami-000c540e28953ace2
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function.

Gets information about the AWS AMI

Returns:
    Dict[str, Dict[str, Any]]

Examples:
    .. code-block:: bash

        $ idem describe aws.ec2.ami
```
{{< /tab >}}

{{< tab "present" >}}

```
Register an AWS AMI.

    Args:
        name(str):
            A region-unique name for the AMI.
            Constraints: 3-128 alphanumeric characters, parentheses (``()``), square brackets (``[]``), spaces, periods (``.``),
            slashes (``/``), dashes (``-``), single quotes (``'``), at-signs (``@``), or underscores(``_``)

        resource_id(str, optional):
            AWS AMI image_id

        image_location(str, optional):
            The full path to your AMI manifest in Amazon S3 storage.
            The specified bucket must have the aws-exec-read canned access control list (ACL) to ensure that it can be accessed by Amazon EC2.
            For more information, see Canned ACLs in the Amazon S3 Service Developer Guide .

        architecture(str, optional):
            The architecture of the AMI. Default: For Amazon EBS-backed AMIs, i386.
            For instance store-backed AMIs, the architecture specified in the manifest file.

        block_device_mappings(list, optional):
            The block device mapping entries.
            If you specify an Amazon EBS volume using the ID of an Amazon EBS snapshot, you can't specify the encryption state of the volume.
            If you create an AMI on an Outpost, then all backing snapshots must be on the same Outpost or in the Region of that Outpost.
            AMIs on an Outpost that include local snapshots can be used to launch instances on the same Outpost only.
            For more information, Amazon EBS local snapshots on Outposts in the Amazon Elastic Compute Cloud User Guide.

            Below are the attributes available for block device mapping entries:

            Type: object dict(Describes a block device mapping, which defines the EBS volumes and instance store volumes to attach to an instance at launch.)

            * DeviceName (str):
                The device name (for example, ``/dev/sdh`` or ``xvdh``).

            * VirtualName (str, Optional):
                The virtual device name (ephemeral N). Instance store volumes are numbered starting from 0.
                An instance type with 2 available instance store volumes can specify mappings for ephemeral0 and ephemeral1 .
                The number of available instance store volumes depends on the instance type. After you connect to the instance, you must mount the volume.
                NVMe instance store volumes are automatically enumerated and assigned a device name. Including them in your block device mapping has no effect.
                Constraints: For M3 instances, you must specify instance store volumes in the block device mapping for the instance.
                When you launch an M3 instance, we ignore any instance store volumes specified in the block device mapping for the AMI.

            * Ebs (dict):
                Parameters used to automatically set up EBS volumes when the instance is launched.

            * DeleteOnTermination (bool, optional):
                Indicates whether the EBS volume is deleted on instance termination. For more information,
                see Preserving Amazon EBS volumes on instance termination in the Amazon EC2 User Guide .

            * Iops (int, optional):
                The number of I/O operations per second (IOPS). For gp3 , io1 , and io2 volumes,
                this represents the number of IOPS that are provisioned for the volume. For gp2 volumes,
                this represents the baseline performance of the volume and the rate at which the volume accumulates I/O credits for bursting.

                The following are the supported values for each volume type:

                gp3 : 3,000-16,000 IOPS
                io1 : 100-64,000 IOPS
                io2 : 100-64,000 IOPS
                For io1 and io2 volumes, we guarantee 64,000 IOPS only for Instances built on the Nitro System.
                Other instance families guarantee performance up to 32,000 IOPS.

                This parameter is required for io1 and io2 volumes. The default for gp3 volumes is 3,000 IOPS.
                This parameter is not supported for gp2 , st1 , sc1 , or standard volumes.

            * SnapshotId (str):
                The ID of the snapshot.

            * VolumeSize (int):
                The size of the volume, in GiBs. You must specify either a snapshot ID or a volume size.
                If you specify a snapshot, the default is the snapshot size.
                You can specify a volume size that is equal to or larger than the snapshot size.

                The following are the supported volumes sizes for each volume type:

                gp2 and gp3 :1-16,384
                io1 and io2 : 4-16,384
                st1 and sc1 : 125-16,384
                standard : 1-1,024

            * VolumeType (str):
                The volume type. For more information, see Amazon EBS volume types in the Amazon EC2 User Guide .
                If the volume type is io1 or io2 , you must specify the IOPS that the volume supports.

            * KmsKeyId (str, optional):
                Identifier (key ID, key alias, ID ARN, or alias ARN) for a customer managed CMK under which the EBS volume is encrypted.
                This parameter is only supported on BlockDeviceMapping objects called by RunInstances, RequestSpotFleet, and RequestSpotInstances .

            * Throughput (int, optional):
                The throughput that the volume supports, in MiB/s.
                This parameter is valid only for gp3 volumes.
                Valid Range: Minimum value of 125. Maximum value of 1000.

            * OutpostArn (str, optional):
                The ARN of the Outpost on which the snapshot is stored.

            * Encrypted (bool, optional):
                Indicates whether the encryption state of an EBS volume is changed while being restored from a backing snapshot.
                The effect of setting the encryption state to true depends on the volume origin (new or from a snapshot),
                starting encryption state, ownership, and whether encryption by default is enabled. For more information,
                see Amazon EBS encryption in the Amazon EC2 User Guide .
                In no case can you remove encryption from an encrypted volume.
                Encrypted volumes can only be attached to instances that support Amazon EBS encryption.
                For more information, see Supported instance types .
                This parameter is not returned by DescribeImageAttribute .

            * NoDevice (str, optional):
                To omit the device from the block device mapping, specify an empty string.
                When this property is specified, the device is removed from the block device mapping regardless of the assigned value.

        description(str, optional):
            A description for your AMI.

        ena_support(bool, optional):
            Set to true to enable enhanced networking with ENA for the AMI and any instances that you launch from the AMI.
            This option is supported only for HVM AMIs.
            Specifying this option with a PV AMI can make instances launched from the AMI unreachable.

        kernel_id (str, optional):
            The ID of the kernel.

        billing_products (list, optional):
            The billing product codes. Your account must be authorized to specify billing product codes.
            Otherwise, you can use the Amazon Web Services Marketplace to bill for the use of an AMI.

        ramdisk_id(str, optional):
            The ID of the RAM disk.

        root_device_name(str, optional):
            The device name of the root device volume (for example, /dev/sda1 ).

        sriov_net_support(str, optional):
            Set to simple to enable enhanced networking with the Intel 82599 Virtual Function interface for the AMI and any instances that you launch from the AMI.
            There is no way to disable sriovNetSupport at this time.
            This option is supported only for HVM AMIs. Specifying this option with a PV AMI can make instances launched from the AMI unreachable.

        virtualization_type(str, optional):
            The type of virtualization (hvm | paravirtual).
            Default: paravirtual

        boot_mode(str, optional):
            The boot mode of the AMI. For more information, see Boot modes in the Amazon Elastic Compute Cloud User Guide.

        tags(dict or list, optional):
            Dict in the format of ``{tag-key: tag-value}`` or List of tags in the format of
            ``[{"Key": tag-key, "Value": tag-value}]`` to associate with the AMI.

            * Key (str):
                The key name that can be used to look up or retrieve the associated value. For example,
                Department or Cost Center are common choices.

            * Value (str):
                The value associated with this tag. For example, tags with a key name of Department could have
                values such as Human Resources, Accounting, and Support. Tags with a key name of Cost Center
                might have values that consist of the number associated with the different cost centers in your
                company. Typically, many resources have tags with the same key name but with different values.
                Amazon Web Services always interprets the tag Value as a single string. If you need to store an
                array, you can store comma-separated values in the string. However, you must interpret the value
                in your code.

    Request Syntax:
       .. code-block:: sls

          [ami-resource-id]:
            aws.ec2.ami.present:
              - name: "string"
              - image_location: "string"
              - architecture: i386|x86_64|arm64|x86_64_mac
              - block_device_mappings:
                  - DeviceName: "string"
                    VirtualName: "string"
                    Ebs:
                      DeleteOnTermination: True|False
                      Iops: 123
                      SnapshotId: "string"
                      VolumeSize: integer
                      VolumeType: standard|io1|io2|gp2|sc1|st1|gp3
                      KmsKeyId: "string"
                      Throughput: integer
                      OutpostArn: "string"
                      Encrypted: True|False
                      NoDevice: "string"
              - description: "string"
              - ena_support: True|False
              - kernel_id: "string"
              - billing_products:
                  - string
                  - string
              - ramdisk_id: "string"
              - root_device_name: "string"
              - sriov_net_support: "string"
              - virtualization_type: "string"
              - boot_mode: legacy-bios|uefi
              - tags:
                  - Key: "string"
                    Value: "string"
              - resource_id: "string"

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            idem-test-ami:
              aws.ec2.ami.present:
                - name: amzn-ami-vpc-nat-2018.03.0.20210721.0-x86_64-ebs
                - resource_id: ami-00a36856283d67c39
                - image_location: amazon/amzn-ami-vpc-nat-2018.03.0.20210721.0-x86_64-ebs
                - architecture: x86_64
                - kernel_id: None
                - block_device_mappings:
                    - DeviceName: /dev/xvda
                      Ebs:
                        DeleteOnTermination: false
                        SnapshotId: snap-1833745e
                        VolumeSize: 15
                        VolumeType: standard
                - description: Amazon Linux AMI 2018.03.0.20210721.0 x86_64 VPC HVM ebs
                - ramdisk_id: ari-1a2b3c4d
                - root_device_name: /dev/xvda
                - virtualization_type: hvm
                - tags:
                    - Key: Name
                      Value: ami-name
                    - Key: ami-tag-key-2
                      Value: ami-tag-value-2
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed AMI as a data-source. Supply one of the inputs as the filter.

Args:
    name(str):
        The name of the Idem state.

    resource_id(str, optional):
        AWS image id to identify the resource.

    executable_users(list, optional):
        Scopes the images by users with explicit launch permissions.
        Specify an Amazon Web Services account ID, self (the sender of the request), or all (public AMIs).

    owners(list, optional):
        Scopes the results to images with the specified owners.
        You can specify a combination of Amazon Web Services account IDs, self , amazon , and aws-marketplace.
        If you omit this parameter, the results include all images for which you have launch permissions, regardless of ownership.

    include_deprecated(bool, optional):
        If true , all deprecated AMIs are included in the response.
        If false , no deprecated AMIs are included in the response. If no value is specified, the default value is false .

    most_recent(bool, optional):
        If more than one result is returned, use the most recent AMI.

    filters(list, optional):
        One or more filters: for example, tag :<key>, tag-key. A complete list of filters can be found at
        `boto3: EC2.Client.describe_images <https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ec2.html#EC2.Client.describe_images>`__


Request Syntax:
    .. code-block:: sls

        [Idem-state-name]:
          aws.ec2.ami.search:
            - resource_id: "string"
            - executable_users
              - user1
            - owners
              - amazon
            - include_deprecated: True|False
            - most_recent: True|False
            - filters:
                - name: "string"
                  values: "list"
                - name: "string"
                  values: "list"

Examples:
    .. code-block:: sls

        my-unmanaged-ami:
          aws.ec2.ami.search:
            - resource_id: value
            - most_recent: False
            - filters:
                - name: "name"
                  values: ["amzn-ami-minimal-hvm-2018.03.0.20181129-x86_64-ebs_2"]
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.ami](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/ami.html).
