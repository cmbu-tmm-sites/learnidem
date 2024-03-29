---
title: "aws.ec2.elastic_ip"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Releases the specified Elastic IP address. [EC2-Classic, default VPC] Releasing an Elastic IP address
automatically disassociates it from any instance that it's associated with. To disassociate an Elastic IP address
without releasing it, use DisassociateAddress . [Nondefault VPC] You must use DisassociateAddress to disassociate
the Elastic IP address before you can release it. After releasing an Elastic IP address, it is released to the IP
address pool. Be sure to update your DNS records and any servers or devices that communicate with the address. If
you attempt to release an Elastic IP address that you already released, you'll get an AuthFailure error if the
address is already allocated to another Amazon Web Services account. [EC2-VPC] After you release an Elastic IP
address for use in a VPC, you might be able to recover it. For more information, see AllocateAddress.

Args:
    name(Text): An Idem name of the elastic IP resource.
    resource_id(Text, optional): The public ip address. Idem automatically considers this resource being absent
     if this field is not specified.
Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        127.15.17.187:
          aws.ec2.elastic_ip.absent:
          - resource_id: 127.15.17.187
          - domain: vpc
          - tags:
            - Key: name
              Value: ONE
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function
Describes the specified Elastic IP addresses or all of your Elastic IP addresses.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.elastic_ip
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Allocates an Elastic IP address to your Amazon Web Services account. After you allocate the Elastic IP address
you can associate it with an instance or network interface. After you release an Elastic IP address,
it is released to the IP address pool and can be allocated to a different Amazon Web Services account. [EC2-VPC]
If you release an Elastic IP address, you might be able to recover it. You cannot recover an Elastic IP address
that you released after it is allocated to another Amazon Web Services account. You cannot recover an Elastic IP
address for EC2-Classic. To attempt to recover an Elastic IP address that you released, specify it in this
operation. An Elastic IP address is for use either in the EC2-Classic platform or in a VPC. By default,
you can allocate 5 Elastic IP addresses for EC2-Classic per Region and 5 Elastic IP addresses for EC2-VPC per
Region. For more information, see Elastic IP Addresses in the Amazon Elastic Compute Cloud User Guide.

Args:
    name(Text): An Idem name of the elastic IP resource.
    domain(Text): Indicates whether the Elastic IP address is for use with instances in a VPC or instances in EC2-Classic.
    resource_id(Text, optional): The public ip address.
    network_border_group(Text, optional): A unique set of Availability Zones, Local Zones, or Wavelength Zones from which Amazon Web Services advertises IP addresses
    public_ipv4_pool(Text, optional): The ID of an address pool that you own.
    customer_owned_ipv4_pool(Text, optional): The ID of a customer-owned address pool.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the elastic IP resource. Defaults to None.
        * Key (string) --  The key of the tag. Tag keys are case-sensitive and accept a maximum of 127 Unicode characters. May not begin with aws: .
        * Value (string) -- The value of the tag. Tag values are case-sensitive and accept a maximum of 255 Unicode characters.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        127.15.17.187:
          aws.ec2.elastic_ip.present:
          - resource_id: 127.15.17.187
          - domain: vpc
          - tags:
            - Key: name
              Value: ONE
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.elastic_ip](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/elastic_ip.html).
