---
title: "aws.ec2.route_table"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified route table. You must disassociate the route table from any subnets before you can delete
it. You can't delete the main route table.

Args:
    name(Text): An Idem name to identify the route table resource.
    resource_id(Text, optional): AWS Route Table ID. Idem automatically considers this resource being absent
     if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.ec2.route_table.absent:
            - name: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Describes one or more of your route tables. Each subnet in your VPC must be associated with a route table. If a
subnet is not explicitly associated with any route table, it is implicitly associated with the main route table.
This command does not return the subnet ID for implicit associations. For more information, see Route tables in
the Amazon Virtual Private Cloud User Guide.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.route_table
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a route table for the specified VPC. For more information, see Route tables in the Amazon Virtual Private Cloud User Guide.

Args:
    name(Text): An Idem name to identify the route table resource.
    resource_id(Text, optional): AWS Route Table ID.
    vpc_id(Text): AWS VPC ID.
    routes(List[Dict[Text, Any]], optional): The network interfaces to associate with the instance. If you specify a network interface, you
        must specify any security groups and subnets as part of the network interface. Defaults to None.
        * DestinationCidrBlock (str, optional): The IPv4 CIDR address block used for the destination match. Routing decisions are based on the
            most specific match. We modify the specified CIDR block to its canonical form; for example, if
            you specify 100.68.0.18/18, we modify it to 100.68.0.0/18. Defaults to None.
        * DestinationIpv6CidrBlock (str, optional): The IPv6 CIDR block used for the destination match.
            Routing decisions are based on the most specific match. Defaults to None.
        * EgressOnlyInternetGatewayId (str, optional): [IPv6 traffic only] The ID of an egress-only internet gateway. Defaults to None.
        * GatewayId (str, optional): The ID of an internet gateway or virtual private gateway attached to your VPC. Defaults to None.
        * InstanceId (str, optional): The ID of a NAT instance in your VPC. The operation fails if you specify an instance ID unless
            exactly one network interface is attached. Defaults to None.
        * InstanceOwnerId (str, optional): The ID of Amazon Web Services account that owns the instance. Defaults to None.
        * NatGatewayId (str, optional): [IPv4 traffic only] The ID of a NAT gateway. Defaults to None.
        * (TransitGatewayId, str, optional): The ID of a transit gateway. Defaults to None.
        * LocalGatewayId (str, optional): The ID of the local gateway. Defaults to None.
        * CarrierGatewayId (str, optional): The ID of the carrier gateway. You can only use this option when the VPC contains a subnet which
            is associated with a Wavelength Zone. Defaults to None.
        * NetworkInterfaceId (str, optional): The ID of a network interface. Defaults to None.
        * VpcPeeringConnectionId (str, optional): The ID of a VPC peering connection. Defaults to None.
        * CoreNetworkArn (str, optional): The Amazon Resource Name (ARN) of the core network. Defaults to None.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the route table.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value (str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.

Request Syntax:
    [route_table-resource-name]:
      aws.ec2.route_table.present:
      - vpc_id: 'string'
      - resource_id: 'string'
      - routes:
        - DestinationCidrBlock: 'string'
          GatewayId: 'string'
      - tags:
        - Key: 'string'
          Value: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        test_route-table:
          aws.ec2.route_table.present:
          - vpc_id: vpc-02850adfa9f6fc916
          - resource_id: route_table-3485hydfe5f6tb998
          - routes:
            - DestinationCidrBlock: 198.31.0.0/16
              GatewayId: local
          - tags:
            - Key: Name
              Value: route-table-association-test
```
{{< /tab >}}

{{< tab "search" >}}

```
Provides details about a specific route table as a data-source. Supply one of the inputs as the filter.

Args:
    name(Text): An Idem name of the AWS route table resource.
    resource_id(Text, optional): AWS route table ID to identify the resource.
    filters(list, optional): One or more filters: for example, tag :<key>, tag-key. A complete list of filters can be found at
     https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ec2.html#EC2.Client.describe_route_tables

Request Syntax:
    [Idem-state-name]:
      aws.ec2.route_table.search:
          - name: 'string'
          - resource_id: 'string'
          - filters:
            - name: 'string'
              values: list
            - name: 'string'
              values: list

Response Syntax:
    The following fields will be returned in the `new_state` of the response.

    - name: 'string'
    - resource_id: 'string'
    - vpc_id: 'string'
    - propagating_vgws: list
    - tags: list
    - routes: list
    - associations: list

Examples:

    Input state file:

    .. code-block:: sls

        idem-test-route-table-search:
            aws.ec2.route_table.search:
              - name: idem-test-route-table-search
              - filters:
                - name: 'vpc-id'
                  values: ["vpc-0ba2072e7101375ee"]
                - name: 'tag:Name'
                  values: ["cluster01-eks-private-0"]

    Sample response:

        - name: 'idem-test-route-table-search'
        - resource_id: 'rtb-05d27d2c959185162'
        - vpc_id: 'vpc-0ba2072e7101375ee'
        - propagating_vgws: []
        - tags:
            - Key: 'Name'
              Value: 'cluster01-eks-private-0'
        - routes:
            - DestinationCidrBlock: '10.170.0.0/16'
              GatewayId: 'local'
              Origin: 'CreateRouteTable'
              State: 'active'
        - associations:
            - Main: False
              RouteTableAssociationId: 'rtbassoc-009e17e6d53ddf889'
              RouteTableId: 'rtb-05d27d2c959185162'
              SubnetId: 'subnet-023a9ac1f67decab0'
              AssociationState:
                State: 'associated'
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.route_table](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/route_table.html).