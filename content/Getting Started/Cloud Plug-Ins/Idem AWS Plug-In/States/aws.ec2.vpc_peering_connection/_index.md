---
title: "aws.ec2.vpc_peering_connection"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes a VPC peering connection. Either the owner of the requester VPC or the owner of the accepter VPC can
delete the VPC peering connection if it's in the active state. The owner of the requester VPC can delete a VPC
peering connection in the pending-acceptance state. You cannot delete a VPC peering connection that's in the
failed state.

Args:
    name(str): An Idem name of the resource.
    resource_id(str, optional): An identifier of the resource in the provider.

Request Syntax:
    [vpc-peering-connection-id]:
      aws.ec2.vpc_peering_connection.absent:
      - resource_id: 'string'
      - name: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.ec2.vpc_peering_connection.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Describes one or more of your VPC peering connections.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.vpc_peering_connection
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Requests a VPC peering connection between two VPCs: a requester VPC that you own and an accepter VPC with which
to create the connection. The accepter VPC can belong to another Amazon Web Services account and can be in a
different Region to the requester VPC. The requester VPC and accepter VPC cannot have overlapping CIDR blocks.
Limitations and rules apply to a VPC peering connection. For more information, see the limitations section in
the VPC Peering Guide.  The owner of the accepter VPC must accept the peering request to activate the peering
connection. The VPC peering connection request expires after 7 days, after which it cannot be accepted or
rejected. If you create a VPC peering connection request between VPCs with overlapping CIDR blocks, the VPC
peering connection has a status of failed.

NOTE: These five parameters - peer_owner_id, peer_vpc_id, vpc_id, peer_region and status
    can't be updated for a given VPC peering connection.
    The only thing that could be updated is the tags,
    and when status is set to active when a new resource is created in real,
    an attempt will be made to set the vpc peering connection status to active.
    In case of an update attempt of the previously mentioned five parameters,
    where resource_id is passed for an existing connection, they will be ignored.

Args:
    name(str): An Idem name of the resource.
    resource_id(str, optional): An identifier of the resource in the provider. Defaults to None.
    peer_owner_id(str, optional): The Amazon Web Services account ID of the owner of the accepter VPC.
        Default: Your Amazon Web Services account ID. Defaults to None.
    peer_vpc_id(str, optional): The ID of the VPC with which you are creating the VPC peering connection.
        You must specify this parameter in the request. Defaults to None.
    vpc_id(str, optional): The ID of the requester VPC. You must specify this parameter in the request.
        Defaults to None.
    peer_region(str, optional): The Region code for the accepter VPC, if the accepter VPC is located in a Region
        other than the Region in which you make the request.
        Default: The Region in which you make the request. Defaults to None.
    tags(Dict, optional): list of tags in the format of [{"Key": tag-key, "Value": tag-value}]
        or dict in the format of {tag-key: tag-value} The tags to assign to the peering connection.
        Defaults to None.
    status: (str, optional) The current status of the vpc peering connection.

Request Syntax:
    [vpc-peering-connection-id]:
      aws.ec2.vpc_peering_connection.present:
      - resource_id: 'string'
      - name: 'string'
      - peer_owner_id: 'string'
      - peer_region: 'string'
      - peer_vpc_id: 'string'
      - vpc_id: 'string'
      - tags: 'Dict'
      - status: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.ec2.vpc_peering_connection.present:
            - resource_id: pcx-ae89ce9b
            - name: pcx-ae89ce9b
            - peer_owner_id: '000000000000'
            - peer_region: us-west-2
            - peer_vpc_id: vpc-98c058ae
            - vpc_id: vpc-2c90d746
            - status: active
            - tags:
                first_key: first_value
                second_key: second_value
                third_key: third_value
                fourth_key: fourth_value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.vpc_peering_connection](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/vpc_peering_connection.html).
