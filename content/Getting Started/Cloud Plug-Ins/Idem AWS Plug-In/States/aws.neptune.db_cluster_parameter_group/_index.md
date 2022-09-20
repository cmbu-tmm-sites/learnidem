---
title: "aws.neptune.db_cluster_parameter_group"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes a specified DB cluster parameter group.

    The DB cluster parameter group to be deleted can't be associated
    with any DB clusters.

    Args:
        hub:
            The redistributed pop central hub

        ctx:
            idem context

        name(str):
            DBClusterParameterGroupName parameter on the resource.
            This is also used as idem name.

        resource_id(str, Optional):
            DBClusterParameterGroupName of the resource. Defaults to None.
            Idem automatically considers the resource being absent if resource_id is not specified.
            Constraints:   Must match the name of an existing DBClusterParameterGroupName.

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            resource_is_absent:
              aws.neptune.db_cluster_parameter_group.absent:
                - name: value
                - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function.

    Returns a list of DBClusterParameterGroup descriptions.

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: bash

            $ idem describe aws.neptune.db_cluster_parameter_group
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a new DB cluster parameter group.

    Parameters in a DB cluster parameter group apply to all of the
    instances in a DB cluster.  A DB cluster parameter group is initially created with the default parameters for
    the database engine used by instances in the DB cluster if parameters is not specified. When you associate a new

    Warning:
    DB cluster parameter group with a running DB cluster, you need to reboot the DB instances in the DB cluster
    without failover for the new DB cluster parameter group and associated settings to take effect.  After you
    create a DB cluster parameter group, you should wait at least 5 minutes before creating your first DB cluster
    that uses that DB cluster parameter group as the default parameter group. This allows Amazon Neptune to fully
    complete the create action before the DB cluster parameter group is used as the default for a new DB cluster.
    This is especially important for parameters that are critical when creating the default database for a DB
    cluster, such as the character set for the default database defined by the character_set_database parameter. You
    can use the Parameter Groups option of the Amazon Neptune console or the DescribeDBClusterParameters command to
    verify that your DB cluster parameter group has been created or modified.

    Args:
        hub:
            The redistributed pop central hub

        ctx:
            idem context

        name(str):
            DBClusterParameterGroupName parameter on the resource. This value is stored as a lowercase string.
            This is also used as idem name.

        resource_id(str, Optional):
            DBClusterParameterGroupName of the resource. Defaults to None.

        db_parameter_group_family(str):
            The DB cluster parameter group family name. A DB cluster parameter group can be
            associated with one and only one DB cluster parameter group family, and can be applied only to a DB cluster
            running a database engine and engine version compatible with that DB cluster parameter group
            family.

        description(str):
            The description for the DB cluster parameter group. This is required field.

        parameters(list, Optional): parameters in the DB cluster parameter group. Defaults to None.
            These parameters can only be modified.
            To modify more than one parameter, submit a list of the following: ParameterName , ParameterValue , and
            ApplyMethod . A maximum of 20 parameters can be modified in a single request.
            Note:
                Changes to dynamic parameters are applied immediately. Changes to static parameters require a reboot
                without failover to the DB cluster associated with the parameter group before the change can take
                effect.
            Below are the attributes available for parameters:

            Type: object dict(Describes a parameter)

            * ParameterName (str):
                Specifies the name of the parameter.
            * ParameterValue (str):
                Specifies the value of the parameter.
            * Description (str, Optional):
                provides a description of the parameter.
            * Source (str, Optional):
                Indicates the source of the parameter value.
            * ApplyType (str, Optional):
                Specifies the engine specific parameters type.
            * DataType (str, Optional):
                Specifies the valid data type for the parameter.
            * AllowedValues (str, Optional):
                Specifies the valid range of values for the parameter.
            * MinimumEngineVersion (str, Optional):
                The earliest engine version to which the parameter can apply.
            * ApplyMethod (str, Optional):
                Indicates when to apply parameter updates.
            * SupportedEngineModes (list, Optional):
                The valid DB engine modes.

        tags(dict, Optional):
            The tags to be assigned to the new DB cluster parameter group. Defaults to None.

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            resource_is_present:
              aws.neptune.db_cluster_parameter_group.present:
                - name: value
                - db_parameter_group_family: value
                - description: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.neptune.db_cluster_parameter_group](https://docs.idemproject.io/idem-aws/en/latest/ref/states/neptune/db_cluster_parameter_group.html).
