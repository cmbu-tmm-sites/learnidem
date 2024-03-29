---
title: "aws.ec2.route_table_association"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Disassociates a subnet or gateway from a route table. After you perform this action, the subnet no longer uses
the routes in the route table. Instead, it uses the routes in the VPC's main route table.

Args:
    name(Text): An Idem name to identify the route table resource.
    route_table_id(Text): The ID of the route table.
    resource_id(Text, optional): AWS Route Table ID. Idem automatically considers this resource being absent
     if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.ec2.route_table_association.absent:
            - name: value
            - route_table: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Describes one or more of your route table associations. Each subnet in your VPC must be associated with a route
table. If a subnet is not explicitly associated with any route table, it is implicitly associated with the main
route table. This command does not return the subnet ID for implicit associations. For more information,
see Route tables in the Amazon Virtual Private Cloud User Guide.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.route_table_association
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Associates a subnet in your VPC or an internet gateway or virtual private gateway attached to your VPC with a
route table in your VPC. This association causes traffic from the subnet or gateway to be routed according to the
routes in the route table. The action returns an association ID, which you need in order to disassociate the
route table later. A route table can be associated with multiple subnets.

Args:
    name(Text): An Idem name to identify the route table resource.
    resource_id(Text, optional): AWS Route Table ID.
    route_table_id(Text): The ID of the route table.
    subnet_id(Text, optional): The ID of the subnet. A subnet ID is not returned for an implicit association.
    gateway_id(Text, optional): The ID of the internet gateway or virtual private gateway.

Request Syntax:
    [route_table-resource-name]:
      aws.ec2.route_table_association.present:
      - route_table_id: 'string'
      - resource_id: 'string'
      - subnet_id: 'string'
      - gateway_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        test_route-table_association:
          aws.ec2.route_table_association.present:
          - route_table_id: vpc-02850adfa9f6fc916
          - resource_id: route_table-3485hydfe5f6tb998
          - gateway_id: vgw-0334141b528f99316
          - subnet_id: subnet-0610f7c1a12a1af6a
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.route_table_association](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/route_table_association.html).
