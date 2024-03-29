---
title: "aws.ec2.transit_gateway_vpc_attachment"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified VPC attachment.

Args:
    name(Text): Name of the resource.
    resource_id(Text, optional): AWS Transit gateway VPC attachment id. Idem automatically considers this resource being absent
     if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        aws.ec2.transit_gateway_vpc_attachment.absent:
            - name: tgw-attach-0871e9c72becf0710
            - resource_id: tgw-attach-0871e9c72becf0710
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Describes one or more VPC attachments. By default, all VPC attachments are described. Alternatively, you can
filter the results.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.transit_gateway_vpc_attachment
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Attaches the specified VPC to the specified transit gateway. If you attach a VPC with a CIDR range that overlaps
the CIDR range of a VPC that is already attached, the new VPC CIDR range is not propagated to the default
propagation route table. To send VPC traffic to an attached transit gateway, add a route to the VPC route table
using CreateRoute.

Args:
    name(Text): Name of the resource.
    transit_gateway(Text): The ID of the transit gateway.
    vpc_id(Text): The ID of the VPC.
    subnet_ids(List): The IDs of one or more subnets. You can specify only one subnet per Availability Zone.
                   You must specify at least one subnet, but we recommend that you specify two subnets for better availability.
                   The transit gateway uses one IP address from each specified subnet.
         * (Text)
    resource_id(Text, optional): AWS Transit gateway VPC attachment id.
    options(Dict[str, Any], optional): The VPC attachment options. Defaults to None.
        * DnsSupport (str, optional): Enable or disable DNS support. The default is enable.
        * Ipv6Support (str, optional): Enable or disable IPv6 support. The default is disable.
        * ApplianceModeSupport (str, optional): Enable or disable support for appliance mode. If enabled, a traffic flow between a source and
            destination uses the same Availability Zone for the VPC attachment for the lifetime of that
            flow. The default is disable.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the transit gateway VPC attachment.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value (str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.

Request Syntax:
    [transit-gateway-resource-id]:
      aws.ec2.transit_gateway_vpc_attachment.present:
        - name: 'string'
        - resource_id: 'string'
        - transit_gateway: 'string'
        - vpc_id: 'string'
        - subnet_ids:
           - 'string'
        - options:
            ApplianceModeSupport: 'string'
            DnsSupport: 'string'
            Ipv6Support: 'string'
        - tags:
            - Key: 'string'
              Value: 'string'
Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        tgw-attach-0871e9c72becf0710:
            aws.ec2.transit_gateway_vpc_attachment.present:
            - name: tgw-attach-0871e9c72becf0710
            - resource_id: tgw-attach-0871e9c72becf0710
            - transit_gateway: tgw-02994a8dda824c337
            - vpc_id: vpc-0afa0d5fe3fc2785c
            - subnet_ids:
               - subnet-07f91b9ebd252be49
            - options:
                ApplianceModeSupport: disable
                DnsSupport: enable
                Ipv6Support: disable
            - tags:
                - Key: Name
                  Value: test-transit-gateway-attachment
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.transit_gateway_vpc_attachment](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/transit_gateway_vpc_attachment.html).
