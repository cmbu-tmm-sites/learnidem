---
title: "aws.ec2.placement_group"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified placement group. You must terminate all instances in the placement group before you can
delete the placement group. For more information, see Placement groups in the Amazon EC2 User Guide.

Args:
    name(Text): An Idem name of the resource and the GroupName of the placement group
    resource_id(Text): The GroupName of the placement group. Idem automatically considers this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.ec2.placement_group.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Args:

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.ec2.placement_group
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a placement group in which to launch instances. The strategy of the placement group determines how the
instances are organized within the group.  A cluster placement group is a logical grouping of instances within a
single Availability Zone that benefit from low network latency, high network throughput. A spread placement
group places instances on distinct hardware. A partition placement group places groups of instances in different
partitions, where instances in one partition do not share the same hardware with instances in another partition.
For more information, see Placement groups in the Amazon EC2 User Guide.

Args:
    name(Text): An Idem name of the resource and the GroupName of the placement group.
    resource_id(Text, optional): The GroupId of the placement group
    strategy(Text, optional): The placement strategy. Defaults to None.
    partition_count(int, optional): The number of partitions. Valid only when Strategy is set to partition. Defaults to None.
    tags(Dict[str, str], optional): The tags to apply to the resource. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
        characters. May not begin with aws:.
        * Value (str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
        Unicode characters.
    spread_level(str, optional): Determines how placement groups spread instances.    Host – You can use host only with Outpost
        placement groups.   Rack – No usage restrictions. Defaults to None.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.ec2.placement_group.present:
            - name: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.placement_group](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/placement_group.html).
