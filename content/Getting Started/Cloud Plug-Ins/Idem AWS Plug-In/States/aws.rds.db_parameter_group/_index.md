---
title: "aws.rds.db_parameter_group"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes a specified DB parameter group. The DB parameter group to be deleted can't be associated with any DB
instances.

Args:
    resource_id(Text): An identifier of the resource in the provider.
    name(Text): The name of the DB parameter group. Constraints:   Must be the name of an existing DB parameter
        group   You can't delete a default DB parameter group   Can't be associated with any DB
        instances.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.rds.db_parameter_group.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Returns a list of DBParameterGroup descriptions.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.rds.db_parameter_group
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a new DB parameter group. A DB parameter group is initially created with the default parameters for the
database engine used by the DB instance. To provide custom values for any of the parameters, you can specify parameters.
Once you've created a DB parameter group, you can associate it with your DB instance. When you associate a new DB parameter group with a
running DB instance, you need to reboot the DB instance without failover for the new DB parameter group and
associated settings to take effect. After you create a DB parameter
group, you should wait at least 5 minutes before creating your first DB instance that uses that DB parameter
group as the default parameter group. This allows Amazon RDS to fully complete the create action before the
parameter group is used as the default for a new DB instance. This is especially important for parameters that
are critical when creating the default database for a DB instance, such as the character set for the default
database defined by the character_set_database parameter. You can use the Parameter Groups option of the Amazon
RDS console to verify that your DB parameter group has been created or modified.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text, optional): An identifier of the resource in the provider. Defaults to None.
    db_parameter_group_family(Text): The DB parameter group family name. A DB parameter group can be associated with one and only one
        DB parameter group family, and can be applied only to a DB instance running a database engine
        and engine version compatible with that DB parameter group family. To list all of the available
        parameter group families for a DB engine, use the following command:  aws rds describe-db-
        engine-versions --query "DBEngineVersions[].DBParameterGroupFamily" --engine <engine>  For
        example, to list all of the available parameter group families for the MySQL DB engine, use the
        following command:  aws rds describe-db-engine-versions --query
        "DBEngineVersions[].DBParameterGroupFamily" --engine mysql   The output contains duplicates.
        The following are the valid DB engine values:    aurora (for MySQL 5.6-compatible Aurora)
        aurora-mysql (for MySQL 5.7-compatible and MySQL 8.0-compatible Aurora)    aurora-postgresql
        mariadb     mysql     oracle-ee     oracle-ee-cdb     oracle-se2     oracle-se2-cdb     postgres
        sqlserver-ee     sqlserver-se     sqlserver-ex     sqlserver-web.
    description(Text): The description for the DB parameter group.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the DB parameter group.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value(str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.
    parameters(List, optional): parameters in the DB parameter group. Defaults to None.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.rds.db_parameter_group.present:
          - name: 'test'
          - resource_id: 'test'
          - db_parameter_group_family: 'aurora-mysql5.7'
          - description: 'test'
          - tags:
             - Key: 'test'
               Value: 'test1'
             - Key: 'test2'
               Value: 'test2'
          - parameters:
             - name: 'aurora_disable_hash_join'
               value: '1'
               apply_method: 'immediate'
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.rds.db_parameter_group](https://docs.idemproject.io/idem-aws/en/latest/ref/states/rds/db_parameter_group.html).