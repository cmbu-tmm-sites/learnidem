---
title: "aws.ec2.instance"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Shuts down the specified instance.
Terminated instances remain visible after termination (for approximately one hour).

Args:
    hub:
    ctx:
    name(Text): The name of the state.
    resource_id(Text): An instance id

Returns:
    Dict[Text, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.ec2.instance.absent:
            - name: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Returns:
    Dict[Text, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.instance
```
{{< /tab >}}

{{< tab "present" >}}

```
Launches an instance using an AMI for which you have permissions.
You can specify a number of options, or leave the default options.
The following rules apply:
    - [EC2-VPC] If you don't specify a subnet ID, we choose a default subnet from your default VPC for you.
        If you don't have a default VPC, you must specify a subnet ID in the request.
    - [EC2-Classic] If don't specify an Availability Zone, we choose one for you.
        Some instance types must be launched into a VPC.
        If you do not have a default VPC, or if you do not specify a subnet ID, the request fails.
        For more information, see Instance types available only in a VPC.
    - [EC2-VPC] All instances have a network interface with a primary private IPv4 address.
        If you don't specify this address, we choose one from the IPv4 range of your subnet.
        Not all instance types support IPv6 addresses.
        For more information, see Instance types.
    - If you don't specify a security group ID, we use the default security group.
        For more information, see Security groups.
    - If any of the AMIs have a product code attached for which the user has not subscribed, the request fails.
    - You can create a launch template, which is a resource that contains the parameters to launch an instance.
        You can specify the launch template instead of specifying the launch parameters.
        An instance is ready for you to use when it's in the running state.
    - You can tag instances and EBS volumes during launch, after launch, or both.
    - Linux instances have access to the public key of the key pair at boot.
        You can use this key to provide secure access to the instance.
        Amazon EC2 public images use this feature to provide secure access without passwords.
        For more information, see Key pairs.

Args:
    hub:
    ctx:
    name(Text): An Idem name of the resource.
    resource_id(Text): AWS Ec2 Instance ID
    image_id(Text): The ID of an AMI
    instance_type(Text): The instance type to use for this instance on creation
    volume_attachments(Dict[Text, Text]): The instance device name mapped to a volume id
    ebs_optimized(bool): Indicates whether the instance is optimized ofr Amazon EBS I/O.
    kernel_id(Text): The kernel associated with this instance, if applicable.
    subnet_id(Text): The ID of the subnet in which the instance is running
    network_interfaces(List[Dict[str, Any]], optional): The network interfaces to associate with the instance. If you specify a network interface, you
        must specify any security groups and subnets as part of the network interface. Defaults to None.
        * AssociatePublicIpAddress (bool, optional): Indicates whether to assign a public IPv4 address to an instance you launch in a VPC. The public
            IP address can only be assigned to a network interface for eth0, and can only be assigned to a
            new network interface, not an existing one. You cannot specify more than one network interface
            in the request. If launching into a default subnet, the default value is true.
        * DeleteOnTermination (bool, optional): If set to true, the interface is deleted when the instance is terminated. You can specify true
            only if creating a new network interface when launching an instance.
        * Description (str, optional): The description of the network interface. Applies only if creating a network interface when
            launching an instance.
        * DeviceIndex (int, optional): The position of the network interface in the attachment order. A primary network interface has a
            device index of 0. If you specify a network interface when launching an instance, you must
            specify the device index.
        * Groups (List[str], optional): The IDs of the security groups for the network interface. Applies only if creating a network
            interface when launching an instance.
        * Ipv6AddressCount (int, optional): A number of IPv6 addresses to assign to the network interface. Amazon EC2 chooses the IPv6
            addresses from the range of the subnet. You cannot specify this option and the option to assign
            specific IPv6 addresses in the same request. You can specify this option if you've specified a
            minimum number of instances to launch.
        * Ipv6Addresses (List[Dict[str, Any]], optional): One or more IPv6 addresses to assign to the network interface. You cannot specify this option
            and the option to assign a number of IPv6 addresses in the same request. You cannot specify this
            option if you've specified a minimum number of instances to launch.
            * Ipv6Address (str, optional): The IPv6 address.
        * NetworkInterfaceId (str, optional): The ID of the network interface. If you are creating a Spot Fleet, omit this parameter because
            you can’t specify a network interface ID in a launch specification.
        * PrivateIpAddress (str, optional): The private IPv4 address of the network interface. Applies only if creating a network interface
            when launching an instance. You cannot specify this option if you're launching more than one
            instance in a RunInstances request.
        * PrivateIpAddresses (List[Dict[str, Any]], optional): One or more private IPv4 addresses to assign to the network interface. Only one private IPv4
            address can be designated as primary. You cannot specify this option if you're launching more
            than one instance in a RunInstances request.
            * Primary (bool, optional): Indicates whether the private IPv4 address is the primary private IPv4 address. Only one IPv4
                address can be designated as primary.
            * PrivateIpAddress (str, optional): The private IPv4 addresses.
        * SecondaryPrivateIpAddressCount (int, optional): The number of secondary private IPv4 addresses. You can't specify this option and specify more
            than one private IP address using the private IP addresses option. You cannot specify this
            option if you're launching more than one instance in a RunInstances request.
        * SubnetId (str, optional): The ID of the subnet associated with the network interface. Applies only if creating a network
            interface when launching an instance.
        * AssociateCarrierIpAddress (bool, optional): Indicates whether to assign a carrier IP address to the network interface. You can only assign a
            carrier IP address to a network interface that is in a subnet in a Wavelength Zone. For more
            information about carrier IP addresses, see Carrier IP addresses in the Amazon Web Services
            Wavelength Developer Guide.
        * InterfaceType (str, optional): The type of network interface. Valid values: interface | efa
        * NetworkCardIndex (int, optional): The index of the network card. Some instance types support multiple network cards. The primary
            network interface must be assigned to network card index 0. The default is network card index 0.
            If you are using RequestSpotInstances to create Spot Instances, omit this parameter because you
            can’t specify the network card index when using this API. To specify the network card index, use
            RunInstances.
        * Ipv4Prefixes (List[Dict[str, Any]], optional): One or more IPv4 delegated prefixes to be assigned to the network interface. You cannot use this
            option if you use the Ipv4PrefixCount option.
            * Ipv4Prefix (str, optional): The IPv4 prefix. For information, see  Assigning prefixes to Amazon EC2 network interfaces in
                the Amazon Elastic Compute Cloud User Guide.
        * Ipv4PrefixCount (int, optional): The number of IPv4 delegated prefixes to be automatically assigned to the network interface. You
            cannot use this option if you use the Ipv4Prefix option.
        * Ipv6Prefixes (List[Dict[str, Any]], optional): One or more IPv6 delegated prefixes to be assigned to the network interface. You cannot use this
            option if you use the Ipv6PrefixCount option.
            * Ipv6Prefix (str, optional): The IPv6 prefix.
        * Ipv6PrefixCount (int, optional): The number of IPv6 delegated prefixes to be automatically assigned to the network interface. You
            cannot use this option if you use the Ipv6Prefix option.
    monitoring_enabled(bool): Indicates whether detailed monitoring is enabled.
    source_dest_check(bool): Indicates whether source/destination checking is enabled
    running(bool): Indicates whether the instance should be in the "running" state
    private_ip_address(Text): The Ipv4 address of the network interface within the subnet.
    owner_id(Text): The ID of the AWS account that owns the reservation.
    availability_zone(Text): The Availability Zone of the instance.
    affinity(Text): The affinity setting for the instance on the Dedicated Host.
    group_name(Text): The affinity setting for the instance on the Dedicated Host.
    partition_number(int): The number of the partition that the instance is in.
    host_id(Text): The ID of the Dedicated Host on which the instance resides.
    tenancy(Text): The tenancy of the instance (if the instance is running in a VPC). An instance with a tenancy of dedicated runs on single-tenant hardware.
    spread_domain(str): Not yet documented by AWS
    host_resource_group_arn(Text): The ARN of the host resource group in which to launch the instances.
    user_data(Text): The user data for the instance
    disable_api_termination(bool): Indicates that an instance cannot be terminated using the Amazon Ec2 console, command line tool, or API.
    ram_disk_id(Text): The ID of the RAM disk, if applicable.
    tags(Dict, optional): The tags to apply to the resource. Defaults to None.
    iam_profile_arn(Text): The IAM instance profile ARN
    instance_initiated_shutdown_behavior(Text): Indicates whether an instance stops or terminates when you initiate shutdown from the instance (using the operating system command for system shutdown)
    elastic_inference_accelerators(List[Dict[str, Any]], optional): An elastic inference accelerator to associate with the instance. Elastic inference accelerators
        are a resource you can attach to your Amazon EC2 instances to accelerate your Deep Learning (DL)
        inference workloads. You cannot specify accelerators from different generations in the same
        request. Defaults to None.
        * Type (str):  The type of elastic inference accelerator. The possible values are eia1.medium, eia1.large,
            eia1.xlarge, eia2.medium, eia2.large, and eia2.xlarge.
        * Count (int, optional):  The number of elastic inference accelerators to attach to the instance.  Default: 1
    elastic_gpu_specifications(List[Dict[str, Any]], optional): An elastic GPU to associate with the instance. An Elastic GPU is a GPU resource that you can
        attach to your Windows instance to accelerate the graphics performance of your applications. For
        more information, see Amazon EC2 Elastic GPUs in the Amazon EC2 User Guide. Defaults to None.
        * Type (str): The type of Elastic Graphics accelerator. For more information about the values to specify for
            Type, see Elastic Graphics Basics, specifically the Elastic Graphics accelerator column, in the
            Amazon Elastic Compute Cloud User Guide for Windows Instances.
    auto_recovery_enabled(bool): Disables the automatic recovery behavior of your instance or sets it to default.
    sriov_net_support(Text): Specifies whether enhanced networking with the Intel 82599 Virtual Function interface is enabled
    key_name(Text): The name of the keypair
    nitro_enclave_enabled(bool): Indicates whether the instance is enabled for AWS Nitro Enclaves.
    capacity_reservation_specification(Dict[str, Any], optional): Information about the Capacity Reservation targeting option. If you do not specify this
        parameter, the instance's Capacity Reservation preference defaults to open, which enables it to
        run in any open Capacity Reservation that has matching attributes (instance type, platform,
        Availability Zone). Defaults to None.
        * CapacityReservationPreference (str, optional): Indicates the instance's Capacity Reservation preferences.
            Possible preferences include:
                open - The instance can run in any open Capacity Reservation that has matching attributes (instance
                    type, platform, Availability Zone).
                none - The instance avoids running in a Capacity Reservation even if one is available. The instance runs as an On-Demand Instance.
        * CapacityReservationTarget (Dict[str, Any], optional): Information about the target Capacity Reservation or Capacity Reservation group.
            * CapacityReservationId (str, optional): The ID of the Capacity Reservation in which to run the instance.
            * CapacityReservationResourceGroupArn (str, optional): The ARN of the Capacity Reservation resource group in which to run the instance.
    client_token(Text): The idempotency token for the instance
    root_device_name(Text): The device name of the root device (for example, /dev/sda1).
    product_codes(List[Dict[Text, Text]]: The product codes attached to the instance, if applicable.
    reservation_id(Text): The ID of the reservation
    block_device_mappings(List[Dict[str, Any]], optional): The block device mapping, which defines the EBS volumes and instance store volumes to attach to
        the instance at launch. For more information, see Block device mappings in the Amazon EC2 User
        Guide. Defaults to None.
        * DeviceName (str, optional): The device name (for example, /dev/sdh or xvdh).
        * VirtualName (str, optional): The virtual device name (ephemeralN). Instance store volumes are numbered starting from 0. An
            instance type with 2 available instance store volumes can specify mappings for ephemeral0 and
            ephemeral1. The number of available instance store volumes depends on the instance type. After
            you connect to the instance, you must mount the volume. NVMe instance store volumes are
            automatically enumerated and assigned a device name. Including them in your block device mapping
            has no effect. Constraints: For M3 instances, you must specify instance store volumes in the
            block device mapping for the instance. When you launch an M3 instance, we ignore any instance
            store volumes specified in the block device mapping for the AMI.
        * Ebs (Dict[str, Any], optional): Parameters used to automatically set up EBS volumes when the instance is launched.
            * DeleteOnTermination (bool, optional): Indicates whether the EBS volume is deleted on instance termination. For more information, see
                Preserving Amazon EBS volumes on instance termination in the Amazon EC2 User Guide.
            * Iops (int, optional): The number of I/O operations per second (IOPS). For gp3, io1, and io2 volumes, this represents
                the number of IOPS that are provisioned for the volume. For gp2 volumes, this represents the
                baseline performance of the volume and the rate at which the volume accumulates I/O credits for
                bursting. The following are the supported values for each volume type:    gp3: 3,000-16,000 IOPS
                io1: 100-64,000 IOPS    io2: 100-64,000 IOPS   For io1 and io2 volumes, we guarantee 64,000 IOPS
                only for Instances built on the Nitro System. Other instance families guarantee performance up
                to 32,000 IOPS. This parameter is required for io1 and io2 volumes. The default for gp3 volumes
                is 3,000 IOPS. This parameter is not supported for gp2, st1, sc1, or standard volumes.
            * SnapshotId (str, optional): The ID of the snapshot.
            * VolumeSize (int, optional): The size of the volume, in GiBs. You must specify either a snapshot ID or a volume size. If you
                specify a snapshot, the default is the snapshot size. You can specify a volume size that is
                equal to or larger than the snapshot size. The following are the supported volumes sizes for
                each volume type:    gp2 and gp3:1-16,384    io1 and io2: 4-16,384    st1 and sc1: 125-16,384
                standard: 1-1,024
            * VolumeType (str, optional): The volume type. For more information, see Amazon EBS volume types in the Amazon EC2 User Guide.
                If the volume type is io1 or io2, you must specify the IOPS that the volume supports.
            * KmsKeyId (str, optional): Identifier (key ID, key alias, ID ARN, or alias ARN) for a customer managed CMK under which the
                EBS volume is encrypted. This parameter is only supported on BlockDeviceMapping objects called
                by RunInstances, RequestSpotFleet, and RequestSpotInstances.
            * Throughput (int, optional): The throughput that the volume supports, in MiB/s. This parameter is valid only for gp3 volumes.
                Valid Range: Minimum value of 125. Maximum value of 1000.
            * OutpostArn (str, optional): The ARN of the Outpost on which the snapshot is stored. This parameter is only supported on
                BlockDeviceMapping objects called by  CreateImage.
            * Encrypted (bool, optional): Indicates whether the encryption state of an EBS volume is changed while being restored from a
                backing snapshot. The effect of setting the encryption state to true depends on the volume
                origin (new or from a snapshot), starting encryption state, ownership, and whether encryption by
                default is enabled. For more information, see Amazon EBS encryption in the Amazon EC2 User
                Guide. In no case can you remove encryption from an encrypted volume. Encrypted volumes can only
                be attached to instances that support Amazon EBS encryption. For more information, see Supported
                instance types. This parameter is not returned by DescribeImageAttribute.
        * NoDevice (str, optional): To omit the device from the block device mapping, specify an empty string. When this property is
            specified, the device is removed from the block device mapping regardless of the assigned value.
    license_arns(List[Text]): The license configuration arns
    hibernation_enabled(bool): Indicates whether the instance is configured for hibernation.
    market_type(Text): The market (purchasing) option for the instance
    max_price(Text): The maximum hourly price you're willing to pay for the Spot Instances.
    spot_instance_type(Text): The Spot Instance request type. Persistent Spot Instance requests are only supported when the instance interruption behavior is either hibernate or stop.
    block_duration_minutes(int): Deprecated
    valid_until(Text): The end date of the request, in UTC format (YYYY -MM -DD T*HH* :MM :SS Z). Supported only for persistent requests.
    instance_interruption_behavior(Text): The behavior when a Spot Instance is interrupted. The default is terminate.
    cpu_credits(Text): The credit option for CPU usage of a T2, T3, or T3a instance. Valid values are standard and unlimited.
    cpu_core_count(int): The number of CPU cores for the instance.
    cpu_threads_per_core(int): The number of threads per CPU core. To disable multithreading for the instance, specify a value of1 . Otherwise, specify the default value of 2.
    http_tokens(Text): The state of token usage for your instance metadata requests. If the state is optional, you can
            choose to retrieve instance metadata with or without a signed token header on your request. If
            you retrieve the IAM role credentials without a token, the version 1.0 role credentials are
            returned. If you retrieve the IAM role credentials using a valid signed token, the version 2.0
            role credentials are returned. If the state is required, you must send a signed token header
            with any instance metadata retrieval requests. In this state, retrieving the IAM role
            credentials always returns the version 2.0 credentials; the version 1.0 credentials are not
            available. Default: optional
    http_put_response_hop_limit(int): The desired HTTP PUT response hop limit for instance metadata requests. The larger the number,
            the further instance metadata requests can travel. Default: 1 Possible values: Integers from 1
            to 64
    http_endpoint_enabled(bool): Enables or disables the HTTP metadata endpoint on your instances. If you specify a value of
            disabled, you cannot access your instance metadata. Default: enabled
    http_protocol_ipv6_enabled(Text): Enables or disables the IPv6 endpoint for the instance metadata service.
    metadata_tags_enabled(bool): Set to enabled to allow access to instance tags from the instance metadata. Set to disabled to
            turn off access to instance tags from the instance metadata. For more information, see Work with
            instance tags using the instance metadata. Default: disabled
    hostname_type(Text): The type of hostname for EC2 instances.
        For IPv4 only subnets, an instance DNS name must be based on the instance IPv4 address.
        For IPv6 only subnets, an instance DNS name must be based on the instance ID.
        For dual-stack subnets, you can specify whether DNS names use the instance IPv4 address or the instance ID.
    enable_resource_name_dns_a_record(bool): Indicates whether to respond to DNS queries for instance hostnames with DNS A records.
    enable_resource_name_dns_aaaa_record(bool): Indicates whether to respond to DNS queries for instance hostnames with DNS A records.
    capacity_reservation_preference(Text): Indicates the instance's Capacity Reservation preferences.
    instance_requirements(Dict[Text, Any]): The attributes for the instance type.
        When you specify instance attributes, Amazon EC2 will identify instance types with these attributes.
    bootstrap(List[Dict[Text, Any]]): BootText options for provisioning an instance with "heist"

Returns:
    Dict[Text, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.ec2.instance.present:
            - name: value
            - image_id: my_ami_id-0000000000000000
            - tags:
                my_tag_key_1: my_tag_value_1
                my_tag_key_2: my_tag_value_2
            - bootstrap:
                - heist_manager: salt.minion
                  artifact_version: 1234
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.instance](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/instance.html).
