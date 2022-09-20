---
title: "aws.neptune.db_instance"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

The DeleteDBInstance action deletes a previously provisioned DB instance. When you delete a DB instance, all
automated backups for that instance are deleted and can't be recovered. Manual DB snapshots of the DB instance
to be deleted by DeleteDBInstance are not deleted.  If you request a final DB snapshot the status of the Amazon
Neptune DB instance is deleting until the DB snapshot is created. The API action DescribeDBInstance is used to
monitor the status of this operation. The action can't be canceled or reverted once submitted. Note that when a
DB instance is in a failure state and has a status of failed, incompatible-restore, or incompatible-network, you
can only delete it when the SkipFinalSnapshot parameter is set to true. You can't delete a DB instance if it is
the only instance in the DB cluster, or if it has deletion protection enabled.

Args:
    name(str): An Idem name of the resource.
    resource_id(str): AWS Neptune DBInstanceIdentifier to identify the resource. This parameter isn't case-
        sensitive. Idem automatically considers the resource being absent if resource_id is not specified.
        Constraints:   Must match the name of an existing DB instance.
    skip_final_snapshot(bool, optional):  Determines whether a final DB snapshot is created before the DB instance is deleted. If true is
        specified, no DBSnapshot is created. If false is specified, a DB snapshot is created before the
        DB instance is deleted. Note that when a DB instance is in a failure state and has a status of
        'failed', 'incompatible-restore', or 'incompatible-network', it can only be deleted when the
        SkipFinalSnapshot parameter is set to "true". Specify true when deleting a Read Replica.  The
        FinalDBSnapshotIdentifier parameter must be specified if SkipFinalSnapshot is false.  Default:
        false. Defaults to None.
    final_db_snapshot_identifier(str, optional):  The DBSnapshotIdentifier of the new DBSnapshot created when SkipFinalSnapshot is set to false.
        Specifying this parameter and also setting the SkipFinalShapshot parameter to true results in an
        error.  Constraints:   Must be 1 to 255 letters or numbers.   First character must be a letter
        Cannot end with a hyphen or contain two consecutive hyphens   Cannot be specified when deleting
        a Read Replica. Defaults to None.
    timeout(Dict, optional): Timeout configuration for deleting of AWS DB Instance.
        * delete (Dict) -- Timeout configuration for deleting DB Instance
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- Customized timeout configuration containing delay and max attempts.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.neptune.db_instance.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Returns information about provisioned instances, and supports pagination.  This operation can also return
information for Amazon RDS instances and Amazon DocDB instances.

Following sensitive parameters are part of present but are not available as part of describe:
- master_user_password
- tde_credential_password
Following parameter is not part of present and is ignored from describe,
idem ensures that the status is in ready state before declaring the resource present:
- db_instance_status

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.neptune.db_instance
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a new DB instance.

Args:
    name(str): An Idem name of the resource. This is also DB instance identifier during resource creation. This
        parameter is stored as a lowercase string.
        Constraints:   Must contain from 1 to 63 letters, numbers, or hyphens.   First character must be a letter.
        Cannot end with a hyphen or contain two consecutive hyphens.   Example: mydbinstance.
    resource_id(str, optional): AWS Neptune DBInstanceIdentifier to identify the resource. Defaults to None.
    db_name(str, optional): Not supported. Defaults to None.
    allocated_storage(int, optional): Not supported by Neptune. Defaults to None.
    db_instance_class(str): The compute and memory capacity of the DB instance, for example, db.m4.large. Not all DB
        instance classes are available in all Amazon Regions.
    engine(str): The name of the database engine to be used for this instance. Valid Values: neptune.
    master_username(str, optional): Not supported by Neptune. Defaults to None.
    master_user_password(str, optional): Not supported by Neptune. Defaults to None.
    db_security_groups(List[str], optional): A list of DB security groups to associate with this DB instance. Default: The default DB
        security group for the database engine. Defaults to None.
    vpc_security_group_ids(List[str], optional): A list of EC2 VPC security groups to associate with this DB instance. Not applicable. The
        associated list of EC2 VPC security groups is managed by the DB cluster. For more information,
        see CreateDBCluster. Default: The default EC2 VPC security group for the DB subnet group's VPC. Defaults to None.
    availability_zone(str, optional):  The EC2 Availability Zone that the DB instance is created in Default: A random, system-chosen
        Availability Zone in the endpoint's Amazon Region.  Example: us-east-1d   Constraint: The
        AvailabilityZone parameter can't be specified if the MultiAZ parameter is set to true. The
        specified Availability Zone must be in the same Amazon Region as the current endpoint. Defaults to None.
    db_subnet_group_name(str, optional): A DB subnet group to associate with this DB instance. If there is no DB subnet group, then it is
        a non-VPC DB instance. Defaults to None.
    preferred_maintenance_window(str, optional): The time range each week during which system maintenance can occur, in Universal Coordinated
        Time (UTC).  Format: ddd:hh24:mi-ddd:hh24:mi  The default is a 30-minute window selected at
        random from an 8-hour block of time for each Amazon Region, occurring on a random day of the
        week. Valid Days: Mon, Tue, Wed, Thu, Fri, Sat, Sun. Constraints: Minimum 30-minute window. Defaults to None.
    db_parameter_group_name(str, optional): The name of the DB parameter group to associate with this DB instance. If this argument is
        omitted, the default DBParameterGroup for the specified engine is used. Constraints:   Must be 1
        to 255 letters, numbers, or hyphens.   First character must be a letter   Cannot end with a
        hyphen or contain two consecutive hyphens. Defaults to None.
    backup_retention_period(int, optional): The number of days for which automated backups are retained. Not applicable. The retention
        period for automated backups is managed by the DB cluster. For more information, see
        CreateDBCluster. Default: 1 Constraints:   Must be a value from 0 to 35   Cannot be set to 0 if
        the DB instance is a source to Read Replicas. Defaults to None.
    preferred_backup_window(str, optional):  The daily time range during which automated backups are created. Not applicable. The daily time
        range for creating automated backups is managed by the DB cluster. For more information, see
        CreateDBCluster. Defaults to None.
    port(int, optional): The port number on which the database accepts connections. Not applicable. The port is managed
        by the DB cluster. For more information, see CreateDBCluster.  Default: 8182  Type: Integer. Defaults to None.
    multi_az(bool, optional): Specifies if the DB instance is a Multi-AZ deployment. You can't set the AvailabilityZone
        parameter if the MultiAZ parameter is set to true. Defaults to None.
    engine_version(str, optional): The version number of the database engine to use. Currently, setting this parameter has no
        effect. Defaults to None.
    auto_minor_version_upgrade(bool, optional): Indicates that minor engine upgrades are applied automatically to the DB instance during the
        maintenance window. Default: true. Defaults to None.
    license_model(str, optional): License model information for this DB instance.  Valid values: license-included | bring-your-
        own-license | general-public-license. Defaults to None.
    iops(int, optional): The amount of Provisioned IOPS (input/output operations per second) to be initially allocated
        for the DB instance. Defaults to None.
    option_group_name(str, optional):  (Not supported by Neptune). Defaults to None.
    character_set_name(str, optional):  (Not supported by Neptune). Defaults to None.
    publicly_accessible(bool, optional): This flag should no longer be used. Defaults to None.
    tags(Dict, optional): Dict in the format of {tag-key: tag-value} to associate with the VPC.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value(str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.
    db_cluster_identifier(str, optional): The identifier of the DB cluster that the instance will belong to. For information on creating a
        DB cluster, see CreateDBCluster. Type: String. Defaults to None.
    storage_type(str, optional): Specifies the storage type to be associated with the DB instance. Not applicable. Storage is
        managed by the DB Cluster. Defaults to None.
    tde_credential_arn(str, optional): The ARN from the key store with which to associate the instance for TDE encryption. Defaults to None.
    tde_credential_password(str, optional): The password for the given ARN from the key store in order to access the device. Defaults to None.
    storage_encrypted(bool, optional): Specifies whether the DB instance is encrypted. Not applicable. The encryption for DB instances
        is managed by the DB cluster. For more information, see CreateDBCluster. Default: false. Defaults to None.
    kms_key_id(str, optional): The Amazon KMS key identifier for an encrypted DB instance. The KMS key identifier is the Amazon
        Resource Name (ARN) for the KMS encryption key. If you are creating a DB instance with the same
        Amazon account that owns the KMS encryption key used to encrypt the new DB instance, then you
        can use the KMS key alias instead of the ARN for the KM encryption key. Not applicable. The KMS
        key identifier is managed by the DB cluster. For more information, see CreateDBCluster. If the
        StorageEncrypted parameter is true, and you do not specify a value for the KmsKeyId parameter,
        then Amazon Neptune will use your default encryption key. Amazon KMS creates the default
        encryption key for your Amazon account. Your Amazon account has a different default encryption
        key for each Amazon Region. Defaults to None.
    domain(str, optional): Specify the Active Directory Domain to create the instance in. Defaults to None.
    copy_tags_to_snapshot(bool, optional): True to copy all tags from the DB instance to snapshots of the DB instance, and otherwise false.
        The default is false. Defaults to None.
    monitoring_interval(int, optional): The interval, in seconds, between points when Enhanced Monitoring metrics are collected for the
        DB instance. To disable collecting Enhanced Monitoring metrics, specify 0. The default is 0. If
        MonitoringRoleArn is specified, then you must also set MonitoringInterval to a value other than
        0. Valid Values: 0, 1, 5, 10, 15, 30, 60. Defaults to None.
    monitoring_role_arn(str, optional): The ARN for the IAM role that permits Neptune to send enhanced monitoring metrics to Amazon
        CloudWatch Logs. For example, arn:aws:iam:123456789012:role/emaccess. If MonitoringInterval is
        set to a value other than 0, then you must supply a MonitoringRoleArn value. Defaults to None.
    domain_iam_role_name(str, optional): Specify the name of the IAM role to be used when making API calls to the Directory Service. Defaults to None.
    promotion_tier(int, optional): A value that specifies the order in which an Read Replica is promoted to the primary instance
        after a failure of the existing primary instance.  Default: 1 Valid Values: 0 - 15. Defaults to None.
    timezone(str, optional): The time zone of the DB instance. Defaults to None.
    enable_iam_database_authentication(bool, optional): Not supported by Neptune (ignored). Defaults to None.
    enable_performance_insights(bool, optional):  (Not supported by Neptune). Defaults to None.
    performance_insights_kms_key_id(str, optional):  (Not supported by Neptune). Defaults to None.
    enable_cloudwatch_logs_exports(List[str], optional): The list of log types that need to be enabled for exporting to CloudWatch Logs. Defaults to None.
    deletion_protection(bool, optional): A value that indicates whether the DB instance has deletion protection enabled. The database
        can't be deleted when deletion protection is enabled. By default, deletion protection is
        disabled. See Deleting a DB Instance. DB instances in a DB cluster can be deleted even when
        deletion protection is enabled in their parent DB cluster. Defaults to None.
    apply_immediately(bool, optional): Specifies whether the modifications in this request and any pending modifications are asynchronously applied as soon as possible, regardless of the PreferredMaintenanceWindow setting for the DB instance.
        If this parameter is set to false , changes to the DB instance are applied during the next maintenance window. Some parameter changes can cause an outage and are applied on the next call to RebootDBInstance , or the next failure reboot.
        Default: false
    allow_major_version_upgrade(bool, optional): Indicates that major version upgrades are allowed. Changing this parameter doesn't result in an outage and the change is asynchronously applied as soon as possible.
    ca_certificate_identifier(str, optional): Indicates the certificate that needs to be associated with the instance.
    cloudwatch_logs_export_configuration(dict, optional): The configuration setting for the log types to be enabled for export to CloudWatch Logs for a specific DB instance or DB cluster.
        EnableLogTypes (list) -- The list of log types to enable. (string)
        DisableLogTypes (list) -- The list of log types to disable. (string)
        eg: {
            'EnableLogTypes': [
                'string',
            ],
            'DisableLogTypes': [
                'string',
            ]
        }
        This parameter is most useful while modifying the resource as during create, we may just want to use 'enable_cloudwatch_logs_export' parameter to just enable some log types.
        However, if this parameter is specified during creation of resource, idem will create and update the resource.
    timeout(Dict, optional): Timeout configuration for create/update of AWS DB Instance.
        * create (Dict) -- Timeout configuration for creating DB Instance
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- Customized timeout configuration containing delay and max attempts.
        * update (Dict) -- Timeout configuration for updating DB Instance
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- Customized timeout configuration containing delay and max attempts.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
            aws.neptune.db_instance.present:
                - name: string
                - db_instance_identifier: string
                - db_instance_class: string
                - engine: string
                - db_cluster_identifier: string
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.neptune.db_instance](https://docs.idemproject.io/idem-aws/en/latest/ref/states/neptune/db_instance.html).