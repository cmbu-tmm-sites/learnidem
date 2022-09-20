---
title: "aws.rds.db_cluster_parameter_group"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes a specified DB cluster parameter group. The DB cluster parameter group to be deleted can't be associated
with any DB clusters. For more information on Amazon Aurora, see  What is Amazon Aurora? in the Amazon Aurora
User Guide.  For more information on Multi-AZ DB clusters, see  Multi-AZ deployments with two readable standby
DB instances in the Amazon RDS User Guide.

Args:
    name(Text): An Idem name of the resource
    resource_id(Text, Optional): AWS DB Cluster Parameter Group name. Constraints: Must be the name of an existing
    DB cluster parameter group. You can't delete a default DB cluster parameter group. Can't be associated with
    any DB clusters.

Request Syntax:
    [resource-id]:
      aws.rds.db_cluster_parameter_group.absent:
        - name: 'string'
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.rds.db_cluster_parameter_group.absent:
            - name: db-cluster-parameter-group-test-name
            - resource_id: db-cluster-parameter-group-test-name
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Returns a list of DBClusterParameterGroup descriptions. If a DBClusterParameterGroupName parameter is
specified, the list will contain only the description of the specified DB cluster parameter group.  For more
information on Amazon Aurora, see  What is Amazon Aurora? in the Amazon Aurora User Guide.  For more information
on Multi-AZ DB clusters, see  Multi-AZ deployments with two readable standby DB instances in the Amazon RDS User
Guide.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.rds.db_cluster_parameter_group
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a new DB cluster parameter group.

Parameters in a DB cluster parameter group apply to all of the instances in a DB cluster.

A DB cluster parameter group is initially created with the default parameters for the database engine used by
instances in the DB cluster. To provide custom values for any of the parameters, you must modify the group after
creating it using ModifyDBClusterParameterGroup . Once you've created a DB cluster parameter group, you need to
associate it with your DB cluster using ModifyDBCluster .

When you associate a new DB cluster parameter group with a running Aurora DB cluster, reboot the DB instances in the
DB cluster without failover for the new DB cluster parameter group and associated settings to take effect.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text, optional): AWS DB Cluster Parameter Group name.

    db_parameter_group_family(Text): The DB cluster parameter group family name. A DB cluster
    parameter group can be associated with one and only one DB cluster parameter group family, and can be applied
    only to a DB cluster running a database engine and engine version compatible with that DB cluster parameter
    group family.
    Example: aurora5.6, aurora-postgresql9.6, mysql8.0 etc.

    description(Text): The description for the DB cluster parameter group.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the DB cluster parameter group.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value(str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.

    parameters(List, optional): parameters in the DB parameter group. Defaults to None.
        Parameter support the following:
        * ParameterName (str): Specifies the name of the parameter.
        * ParameterValue (str): Specifies the value of the parameter.
        * Description (str, optional): provides a description of the parameter.
        * Source (str, optional): Indicates the source of the parameter value.
        * ApplyType (str, optional): Specifies the engine specific parameters type.
        * DataType (str, optional): Specifies the valid data type for the parameter.
        * AllowedValues (str, optional): Specifies the valid range of values for the parameter.
        * MinimumEngineVersion (str, optional): The earliest engine version to which the parameter can apply.
        * ApplyMethod (str, optional): Indicates when to apply parameter updates.
        * SupportedEngineModes (list, optional): The valid DB engine modes.

Request Syntax:
    [db-cluster-parameter-group-name]:
      aws.rds.db_cluster_parameter_group.present:
        - name: 'string'
        - resource_id: 'string'
        - db_parameter_group_family: 'string'
        - description: 'string'
        - tags:
            - Key: 'string'
              Value: 'string'
        - parameters:
            - ParameterName: 'aurora_disable_hash_join'
              ParameterValue: '1'
              ApplyMethod: 'immediate'
Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.rds.db_cluster_parameter_group.present:
            - name: db-cluster-parameter-group-1
            - resource_id: db-cluster-parameter-group-1
            - db_parameter_group_family: aurora-5.6
            - description: Test description
            - tags:
                - Key: Name
                  Value: db-cluster-parameter-group-1
            - parameters:
                - ParameterName: 'aurora_disable_hash_join'
                  ParameterValue: '1'
                  ApplyMethod: 'immediate'
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.rds.db_cluster_parameter_group](https://docs.idemproject.io/idem-aws/en/latest/ref/states/rds/db_cluster_parameter_group.html).
