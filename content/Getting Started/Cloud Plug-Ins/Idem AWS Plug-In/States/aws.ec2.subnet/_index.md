---
title: "aws.ec2.subnet"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified subnet. You must terminate all running instances in the subnet before you can delete the
subnet.

Args:
    name(Text): The Idem name of the subnet.
    resource_id(Text, optional): AWS Subnet ID. Idem automatically considers this resource being absent if
     this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.ec2.subnet.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```

```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a subnet in a specified VPC. You must specify an IPv4 CIDR block for the subnet. After you create a
subnet, you can't change its CIDR block. The allowed block size is between a /16 netmask (65,536 IP addresses)
and /28 netmask (16 IP addresses). The CIDR block must not overlap with the CIDR block of an existing subnet in
the VPC. If you've associated an IPv6 CIDR block with your VPC, you can create a subnet with an IPv6 CIDR block
that uses a /64 prefix length.   Amazon Web Services reserves both the first four and the last IPv4 address in
each subnet's CIDR block. They're not available for use.  If you add more than one subnet to a VPC, they're set
up in a star topology with a logical router in the middle. When you stop an instance in a subnet, it retains its
private IPv4 address. It's therefore possible to have a subnet with no running instances (they're all stopped),
but no remaining IP addresses available. For more information about subnets, see Your VPC and subnets in the
Amazon Virtual Private Cloud User Guide.

Args:
    name(Text): An Idem name of the resource.
    vpc_id(Text): ID of the VPC.
    cidr_block(Text): The IPv4 network range for the subnet, in CIDR notation. For example, 10.0.0.0/24. We modify the
        specified CIDR block to its canonical form; for example, if you specify 100.68.0.18/18, we
        modify it to 100.68.0.0/18.
    resource_id(Text, optional): AWS Subnet ID
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the subnet.
        Each tag consists of a key name and an associated value. Defaults to None.
        * (Key, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * (Value, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.
    availability_zone(Text, optional): The Availability Zone or Local Zone for the subnet. Default: Amazon Web Services selects one for
        you. If you create more than one subnet in your VPC, we do not necessarily select a different
        zone for each subnet. To create a subnet in a Local Zone, set this value to the Local Zone ID,
        for example us-west-2-lax-1a. For information about the Regions that support Local Zones, see
        Available Regions in the Amazon Elastic Compute Cloud User Guide. To create a subnet in an
        Outpost, set this value to the Availability Zone for the Outpost and specify the Outpost ARN. Defaults to None.
    availability_zone_id(Text, optional): The AZ ID or the Local Zone ID of the subnet. Defaults to None.
    ipv6_cidr_block(Text, optional): The IPv6 network range for the subnet, in CIDR notation. The subnet size must use a /64 prefix
        length. Defaults to None.
    outpost_arn(Text, optional): The Amazon Resource Name (ARN) of the Outpost. If you specify an Outpost ARN, you must also
        specify the Availability Zone of the Outpost subnet. Defaults to None.
    map_public_ip_on_launch (boolean, optional): Indicates whether instances launched in this subnet receive a public IPv4 address.
    assign_ipv6_address_on_creation (boolean, optional): Specify true to indicate that network interfaces created in the specified subnet should be assigned an IPv6 address.
        This includes a network interface that's created when launching an instance into the subnet (the instance therefore receives an IPv6 address).
    map_customer_owned_ip_on_launch (boolean, optional): Specify true to indicate that network interfaces attached to instances created in the specified subnet should be assigned a customer-owned IPv4 address.
    customer_owned_ipv4_pool (Text, optional): The customer-owned IPv4 address pool associated with the subnet. You must set this value when you specify true for MapCustomerOwnedIpOnLaunch .
    enable_dns_64 (boolean, optional): Indicates whether DNS queries made to the Amazon-provided DNS Resolver in this subnet should return synthetic IPv6 addresses for IPv4-only destinations.
    enable_lni_at_device_index (int, optional): Indicates the device position for local network interfaces in this subnet.
    private_dns_name_options_on_launch (Dict) -- The type of hostnames to assign to instances in the subnet at launch. An instance hostname is based on the IPv4 address or ID of the instance.
        HostnameType (Text) -- The type of hostname for EC2 instances. For IPv4 only subnets, an instance DNS name must be based on the instance IPv4 address.
            For IPv6 only subnets, an instance DNS name must be based on the instance ID. For dual-stack subnets, you can specify whether DNS names use the instance IPv4 address or the instance ID.
        EnableResourceNameDnsARecord (boolean) -- Indicates whether to respond to DNS queries for instance hostnames with DNS A records.
        EnableResourceNameDnsAAAARecord (boolean) -- Indicates whether to respond to DNS queries for instance hostname with DNS AAAA records.
    disable_lni_at_device_index (boolean): Specify true to indicate that local network interfaces at the current position should be disabled.

Request Syntax:
    [subnet-resource-name]:
      aws.ec2.subnet.present:
      - resource_id: 'string'
      - cidr_block: 'string'
      - ipv6_cidr_block: 'string'
      - vpc_id: 'string'
      - availability_zone: 'string'
      - availability_zone_id: 'string'
      - outpost_arn: 'string'
      - map_public_ip_on_launch: bool
      - assign_ipv6_address_on_creation: bool
      - map_customer_owned_ip_on_launch: bool
      - enable_dns_64: bool
      - private_dns_name_options_on_launch:
          EnableResourceNameDnsAAAARecord: bool
          EnableResourceNameDnsARecord: bool
          HostnameType: 'string'
      - tags:
        - Key: 'string'
          Value: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        my-subnet:
          aws.ec2.subnet.present:
            - vpc_id: vpc-07123af5a5zwqcc0
            - cidr_block: 10.10.10.0/28
            - availability_zone: eu-west-2c
            - tags:
              - Key: Name
                Value: Idem-test-subnet
            - ipv6_cidr_block: 2a05:d01c:74f:7200::/64
            - map_public_ip_on_launch: true
            - assign_ipv6_address_on_creation: false
            - map_customer_owned_ip_on_launch: false
            - enable_dns_64: false
            - private_dns_name_options_on_launch:
                EnableResourceNameDnsAAAARecord: false
                EnableResourceNameDnsARecord: false
                HostnameType: ip-name
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed subnet as a data-source. Supply one of the inputs as the filter.

Args:
    name(string): The name of the Idem state.
    resource_id(string, optional): AWS subnet id to identify the resource.
    availability_zone(string, optional): The Availability Zone for the subnet.
    availability_zone_id(string, optional): The ID of the Availability Zone for the subnet.
    cidr_block(string, optional): The IPv4 CIDR block of the subnet. The CIDR block you specify must exactly match
     the subnet's CIDR block for information to be returned for the subnet.
    default_for_az(string, optional): Indicate whether the subnet is the default subnet in the Availability Zone.
    filters(List, optional): One or more filters: for example, tag :<key>, tag-key. A complete list of filters can be found at
     https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ec2.html#EC2.Client.describe_subnets
    ipv6_cidr_block(string, optional): An IPv6 CIDR block associated with the subnet.
    status(string, optional): The state of the subnet (pending | available ).
    vpc_id(string, optional): The ID of the VPC for the subnet.
    tags(List or Dict, optional): The list or dict of tags to filter by.
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.subnet](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/subnet.html).