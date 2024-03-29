---
title: "aws.elasticache.replication_group"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes an existing replication group. By default, this operation deletes the entire replication group,
including the primary/primaries and all of the read replicas. If the replication group has only one primary, you
can optionally delete only the read replicas, while retaining the primary by setting RetainPrimaryCluster=true.
When you receive a successful response from this operation, Amazon ElastiCache immediately begins deleting the
selected resources; you cannot cancel or revert this operation.  This operation is valid for Redis only.

Args:
    name(Text): An Idem name of the resource. It is used as ReplicationGroupID during resource creation
    resource_id(Text): The replication group identifier.
    retain_primary_cluster(bool, optional): If set to true, all of the read replicas are deleted, but the primary node is retained. Defaults to None.
    final_snapshot_identifier(Text, optional): The name of a final node group (shard) snapshot. ElastiCache creates the snapshot from the
        primary node in the cluster, rather than one of the replicas; this is to ensure that it captures
        the freshest data. After the final snapshot is taken, the replication group is immediately
        deleted. Defaults to None.
    timeout(Dict, optional): Timeout configuration for deletion of AWS DB Instance.
        * delete (Dict) -- Timeout configuration for deletion of a DB Instance
            * delay(int) -- The amount of time in seconds to wait between attempts.Defaults to 30
            * max_attempts(int) -- Customized timeout configuration containing delay and max attempts.Defaults to 60

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.elasticache.replication_group.absent:
            - name: value
            - resource_id: value
            - replication_group_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.elasticache.replication_group
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a Redis (cluster mode disabled) or a Redis (cluster mode enabled) replication group. This API can be
used to create a standalone regional replication group or a secondary replication group associated with a Global
datastore. A Redis (cluster mode disabled) replication group is a collection of clusters, where one of the
clusters is a read/write primary and the others are read-only replicas. Writes to the primary are asynchronously
propagated to the replicas. A Redis cluster-mode enabled cluster is comprised of from 1 to 90 shards (API/CLI:
node groups). Each shard has a primary node and up to 5 read-only replica nodes. The configuration can range
from 90 shards and 0 replicas to 15 shards and 5 replicas, which is the maximum number or replicas allowed.  The
node or shard limit can be increased to a maximum of 500 per cluster if the Redis engine version is 5.0.6 or
higher. For example, you can choose to configure a 500 node cluster that ranges between 83 shards (one primary
and 5 replicas per shard) and 500 shards (single primary and no replicas). Make sure there are enough available
IP addresses to accommodate the increase. Common pitfalls include the subnets in the subnet group have too small
a CIDR range or the subnets are shared and heavily used by other clusters. For more information, see Creating a
Subnet Group. For versions below 5.0.6, the limit is 250 per cluster. To request a limit increase, see Amazon
Service Limits and choose the limit type Nodes per cluster per instance type.  When a Redis (cluster mode
disabled) replication group has been successfully created, you can add one or more read replicas to it, up to a
total of 5 read replicas. If you need to increase or decrease the number of node groups (console: shards), you
can avail yourself of ElastiCache for Redis' scaling. For more information, see Scaling ElastiCache for Redis
Clusters in the ElastiCache User Guide.  This operation is valid for Redis only.

Args:
    name(Text): An Idem name of the resource. It is used as ReplicationGroupID during resource creation
    resource_id(Text, optional): The replication group identifier.
    replication_group_description(Text): A user-created description for the replication group.
    global_replication_group_id(Text, optional): The name of the Global datastore. Defaults to None.
    primary_cluster_id(Text, optional): The identifier of the cluster that serves as the primary for this replication group. This
        cluster must already exist and have a status of available. This parameter is not required if
        NumCacheClusters, NumNodeGroups, or ReplicasPerNodeGroup is specified. Defaults to None.
    automatic_failover_enabled(bool, optional): Specifies whether a read-only replica is automatically promoted to read/write primary if the
        existing primary fails.  AutomaticFailoverEnabled must be enabled for Redis (cluster mode
        enabled) replication groups. Default: false. Defaults to None.
    multi_az_enabled(bool, optional): A flag indicating if you have Multi-AZ enabled to enhance fault tolerance. For more information,
        see Minimizing Downtime: Multi-AZ. Defaults to None.
    num_cache_clusters(int, optional): The number of clusters this replication group initially has. This parameter is not used if there
        is more than one node group (shard). You should use ReplicasPerNodeGroup instead. If
        AutomaticFailoverEnabled is true, the value of this parameter must be at least 2. If
        AutomaticFailoverEnabled is false you can omit this parameter (it will default to 1), or you can
        explicitly set it to a value between 2 and 6. The maximum permitted value for NumCacheClusters
        is 6 (1 primary plus 5 replicas). Defaults to None.
    preferred_cache_cluster_a_zs(List[str], optional): A list of EC2 Availability Zones in which the replication group's clusters are created. The
        order of the Availability Zones in the list is the order in which clusters are allocated. The
        primary cluster is created in the first AZ in the list. This parameter is not used if there is
        more than one node group (shard). You should use NodeGroupConfiguration instead.  If you are
        creating your replication group in an Amazon VPC (recommended), you can only locate clusters in
        Availability Zones associated with the subnets in the selected subnet group. The number of
        Availability Zones listed must equal the value of NumCacheClusters.  Default: system chosen
        Availability Zones. Defaults to None.
    num_node_groups(int, optional): An optional parameter that specifies the number of node groups (shards) for this Redis (cluster
        mode enabled) replication group. For Redis (cluster mode disabled) either omit this parameter or
        set it to 1. Default: 1. Defaults to None.
    replicas_per_node_group(int, optional): An optional parameter that specifies the number of replica nodes in each node group (shard).
        Valid values are 0 to 5. Defaults to None.
    node_group_configuration(List[Dict], optional): A list of node group (shard) configuration options. Each node group (shard) configuration has
        the following members: PrimaryAvailabilityZone, ReplicaAvailabilityZones, ReplicaCount, and
        Slots. If you're creating a Redis (cluster mode disabled) or a Redis (cluster mode enabled)
        replication group, you can use this parameter to individually configure each node group (shard),
        or you can omit this parameter. However, it is required when seeding a Redis (cluster mode
        enabled) cluster from a S3 rdb file. You must configure each node group (shard) using this
        parameter because you must specify the slots for each node group. Defaults to None.
        * NodeGroupId (str, optional): Either the ElastiCache for Redis supplied 4-digit id or a user supplied id for the node group
        these configuration values apply to.
        * Slots (str, optional): A string that specifies the keyspace for a particular node group. Keyspaces range from 0 to
        16,383. The string is in the format startkey-endkey. Example: "0-3999"
        * ReplicaCount (int, optional): The number of read replica nodes in this node group (shard).
        * PrimaryAvailabilityZone (str, optional): The Availability Zone where the primary node of this node group (shard) is launched.
        * ReplicaAvailabilityZones (List[str], optional): A list of Availability Zones to be used for the read replicas. The number of Availability Zones
        in this list must match the value of ReplicaCount or ReplicasPerNodeGroup if not specified.
        * PrimaryOutpostArn (str, optional): The outpost ARN of the primary node.
        * ReplicaOutpostArns (List[str], optional): The outpost ARN of the node replicas.
    cache_node_type(Text, optional): The compute and memory capacity of the nodes in the node group (shard). The following node types
        are supported by ElastiCache. Generally speaking, the current generation types provide more
        memory and computational power at lower cost when compared to their equivalent previous
        generation counterparts.   General purpose:   Current generation:   M6g node types (available
        only for Redis engine version 5.0.6 onward and for Memcached engine version 1.5.16 onward):
        cache.m6g.large, cache.m6g.xlarge, cache.m6g.2xlarge, cache.m6g.4xlarge, cache.m6g.8xlarge,
        cache.m6g.12xlarge, cache.m6g.16xlarge   For region availability, see Supported Node Types    M5
        node types: cache.m5.large, cache.m5.xlarge, cache.m5.2xlarge, cache.m5.4xlarge,
        cache.m5.12xlarge, cache.m5.24xlarge   M4 node types: cache.m4.large, cache.m4.xlarge,
        cache.m4.2xlarge, cache.m4.4xlarge, cache.m4.10xlarge   T4g node types (available only for Redis
        engine version 5.0.6 onward and Memcached engine version 1.5.16 onward): cache.t4g.micro,
        cache.t4g.small, cache.t4g.medium   T3 node types: cache.t3.micro, cache.t3.small,
        cache.t3.medium   T2 node types: cache.t2.micro, cache.t2.small, cache.t2.medium    Previous
        generation: (not recommended)  T1 node types: cache.t1.micro   M1 node types: cache.m1.small,
        cache.m1.medium, cache.m1.large, cache.m1.xlarge   M3 node types: cache.m3.medium,
        cache.m3.large, cache.m3.xlarge, cache.m3.2xlarge      Compute optimized:   Previous generation:
        (not recommended)  C1 node types: cache.c1.xlarge      Memory optimized with data tiering:
        Current generation:   R6gd node types (available only for Redis engine version 6.2 onward).
        cache.r6gd.xlarge, cache.r6gd.2xlarge, cache.r6gd.4xlarge, cache.r6gd.8xlarge,
        cache.r6gd.12xlarge, cache.r6gd.16xlarge      Memory optimized:   Current generation:   R6g node
        types (available only for Redis engine version 5.0.6 onward and for Memcached engine version
        1.5.16 onward).  cache.r6g.large, cache.r6g.xlarge, cache.r6g.2xlarge, cache.r6g.4xlarge,
        cache.r6g.8xlarge, cache.r6g.12xlarge, cache.r6g.16xlarge   For region availability, see
        Supported Node Types    R5 node types: cache.r5.large, cache.r5.xlarge, cache.r5.2xlarge,
        cache.r5.4xlarge, cache.r5.12xlarge, cache.r5.24xlarge   R4 node types: cache.r4.large,
        cache.r4.xlarge, cache.r4.2xlarge, cache.r4.4xlarge, cache.r4.8xlarge, cache.r4.16xlarge
        Previous generation: (not recommended)  M2 node types: cache.m2.xlarge, cache.m2.2xlarge,
        cache.m2.4xlarge   R3 node types: cache.r3.large, cache.r3.xlarge, cache.r3.2xlarge,
        cache.r3.4xlarge, cache.r3.8xlarge       Additional node type info    All current generation
        instance types are created in Amazon VPC by default.   Redis append-only files (AOF) are not
        supported for T1 or T2 instances.   Redis Multi-AZ with automatic failover is not supported on
        T1 instances.   Redis configuration variables appendonly and appendfsync are not supported on
        Redis version 2.8.22 and later. Defaults to None.
    engine(Text, optional): The name of the cache engine to be used for the clusters in this replication group. Must be
        Redis. Defaults to None.
    engine_version(Text, optional): The version number of the cache engine to be used for the clusters in this replication group. To
        view the supported cache engine versions, use the DescribeCacheEngineVersions operation.
        Important: You can upgrade to a newer engine version (see Selecting a Cache Engine and Version)
        in the ElastiCache User Guide, but you cannot downgrade to an earlier engine version. If you
        want to use an earlier engine version, you must delete the existing cluster or replication group
        and create it anew with the earlier engine version. Defaults to None.
    cache_parameter_group_name(Text, optional): The name of the parameter group to associate with this replication group. If this argument is
        omitted, the default cache parameter group for the specified engine is used. If you are running
        Redis version 3.2.4 or later, only one node group (shard), and want to use a default parameter
        group, we recommend that you specify the parameter group by name.    To create a Redis (cluster
        mode disabled) replication group, use CacheParameterGroupName=default.redis3.2.   To create a
        Redis (cluster mode enabled) replication group, use
        CacheParameterGroupName=default.redis3.2.cluster.on. Defaults to None.
    cache_subnet_group_name(Text, optional): The name of the cache subnet group to be used for the replication group.  If you're going to
        launch your cluster in an Amazon VPC, you need to create a subnet group before you start
        creating a cluster. For more information, see Subnets and Subnet Groups. Defaults to None.
    cache_security_group_names(List[str], optional): A list of cache security group names to associate with this replication group. Defaults to None.
    security_group_ids(List[str], optional): One or more Amazon VPC security groups associated with this replication group. Use this
        parameter only when you are creating a replication group in an Amazon Virtual Private Cloud
        (Amazon VPC). Defaults to None.
    tags(Dict[str, str]): A list of tags to be added to this resource. Tags are comma-separated key,value pairs (e.g.
        Key=myKey, Value=myKeyValue. You can include multiple tags as shown following: Key=myKey,
        Value=myKeyValue Key=mySecondKey, Value=mySecondKeyValue. Tags on replication groups will be
        replicated to all nodes. Defaults to None.
        * Key (str, optional): The key for the tag. May not be null.
        * Value (str, optional): The tag's value. May be null.
    snapshot_arns(List[str], optional): A list of Amazon Resource Names (ARN) that uniquely identify the Redis RDB snapshot files stored
        in Amazon S3. The snapshot files are used to populate the new replication group. The Amazon S3
        object name in the ARN cannot contain any commas. The new replication group will have the number
        of node groups (console: shards) specified by the parameter NumNodeGroups or the number of node
        groups configured by NodeGroupConfiguration regardless of the number of ARNs specified here.
        Example of an Amazon S3 ARN: arn:aws:s3:::my_bucket/snapshot1.rdb. Defaults to None.
    snapshot_name(Text, optional): The name of a snapshot from which to restore data into the new replication group. The snapshot
        status changes to restoring while the new replication group is being created. Defaults to None.
    preferred_maintenance_window(Text, optional): Specifies the weekly time range during which maintenance on the cluster is performed. It is
        specified as a range in the format ddd:hh24:mi-ddd:hh24:mi (24H Clock UTC). The minimum
        maintenance window is a 60 minute period. Valid values for ddd are: Specifies the weekly time
        range during which maintenance on the cluster is performed. It is specified as a range in the
        format ddd:hh24:mi-ddd:hh24:mi (24H Clock UTC). The minimum maintenance window is a 60 minute
        period. Valid values for ddd are:    sun     mon     tue     wed     thu     fri     sat
        Example: sun:23:00-mon:01:30. Defaults to None.
    port(int, optional): The port number on which each member of the replication group accepts connections. Defaults to None.
    notification_topic_arn(Text, optional): The Amazon Resource Name (ARN) of the Amazon Simple Notification Service (SNS) topic to which
        notifications are sent.  The Amazon SNS topic owner must be the same as the cluster owner. Defaults to None.
    auto_minor_version_upgrade(bool, optional):  If you are running Redis engine version 6.0 or later, set this parameter to yes if you want to
        opt-in to the next auto minor version upgrade campaign. This parameter is disabled for previous
        versions. . Defaults to None.
    snapshot_retention_limit(int, optional): The number of days for which ElastiCache retains automatic snapshots before deleting them. For
        example, if you set SnapshotRetentionLimit to 5, a snapshot that was taken today is retained for
        5 days before being deleted. Default: 0 (i.e., automatic backups are disabled for this cluster). Defaults to None.
    snapshot_window(Text, optional): The daily time range (in UTC) during which ElastiCache begins taking a daily snapshot of your
        node group (shard). Example: 05:00-09:00  If you do not specify this parameter, ElastiCache
        automatically chooses an appropriate time range. Defaults to None.
    auth_token(Text, optional):  Reserved parameter. The password used to access a password protected server.  AuthToken can be
        specified only on replication groups where TransitEncryptionEnabled is true.  For HIPAA
        compliance, you must specify TransitEncryptionEnabled as true, an AuthToken, and a
        CacheSubnetGroup.  Password constraints:   Must be only printable ASCII characters.   Must be at
        least 16 characters and no more than 128 characters in length.   The only permitted printable
        special characters are !, &, #, $, ^, <, >, and -. Other printable special characters cannot be
        used in the AUTH token.   For more information, see AUTH password at
        http://redis.io/commands/AUTH. Defaults to None.
    transit_encryption_enabled(bool, optional): A flag that enables in-transit encryption when set to true. You cannot modify the value of
        TransitEncryptionEnabled after the cluster is created. To enable in-transit encryption on a
        cluster you must set TransitEncryptionEnabled to true when you create a cluster. This parameter
        is valid only if the Engine parameter is redis, the EngineVersion parameter is 3.2.6, 4.x or
        later, and the cluster is being created in an Amazon VPC. If you enable in-transit encryption,
        you must also specify a value for CacheSubnetGroup.  Required: Only available when creating a
        replication group in an Amazon VPC using redis version 3.2.6, 4.x or later. Default: false   For
        HIPAA compliance, you must specify TransitEncryptionEnabled as true, an AuthToken, and a
        CacheSubnetGroup. Defaults to None.
    at_rest_encryption_enabled(bool, optional): A flag that enables encryption at rest when set to true. You cannot modify the value of
        AtRestEncryptionEnabled after the replication group is created. To enable encryption at rest on
        a replication group you must set AtRestEncryptionEnabled to true when you create the replication
        group.   Required: Only available when creating a replication group in an Amazon VPC using redis
        version 3.2.6, 4.x or later. Default: false. Defaults to None.
    kms_key_id(Text, optional): The ID of the KMS key used to encrypt the disk in the cluster. Defaults to None.
    user_group_ids(List[str], optional): The user group to associate with the replication group. Defaults to None.
    log_delivery_configurations(List[Dict], optional): Specifies the destination, format and type of the logs. Defaults to None.
        * LogType (Text, optional): Refers to slow-log.
        * DestinationType (Text, optional): Specify either cloudwatch-logs or kinesis-firehose as the destination type.
        * DestinationDetails (Text, optional): Configuration details of either a CloudWatch Logs destination or Kinesis Data Firehose
        destination.
            * CloudWatchLogsDetails (Dict, optional): The configuration details of the CloudWatch Logs destination.
                * LogGroup (Text, optional): The name of the CloudWatch Logs log group.
            * KinesisFirehoseDetails (Dict, optional): The configuration details of the Kinesis Data Firehose destination.
                * DeliveryStream (str, optional): The name of the Kinesis Data Firehose delivery stream.
        * LogFormat (Text, optional): Specifies either JSON or TEXT
        * Enabled (bool, optional): Specify if log delivery is enabled. Default true.
    data_tiering_enabled(bool, optional): Enables data tiering. Data tiering is only supported for replication groups using the r6gd node
        type. This parameter must be set to true when using r6gd nodes. For more information, see Data
        tiering. Defaults to None.
    snapshotting_cluster_id (Text, optional): The cluster ID that is used as the daily snapshot source for the replication group. This parameter
                cannot be set for Redis (cluster mode enabled) replication groups.
    node_group_id(Text, optional): Deprecated. This parameter is not used.
    notification_topic_status(bool, optional): The Amazon Resource Name (ARN) of the Amazon SNS topic to which notifications are sent.
    apply_immediately(bool, optional): If true , this parameter causes the modifications in this request and any pending modifications to be applied,
        asynchronously and as soon as possible, regardless of the PreferredMaintenanceWindow setting for the replication group.
        If false , changes to the nodes in the replication group are applied on the next maintenance reboot, or the next failure reboot,
        whichever occurs first.
        Valid values: true | false
        Default: false
    auto_token_update_strategy(Text, optional): Specifies the strategy to use to update the AUTH token. This parameter must be specified with
            the auth-token parameter. Possible values:
            Rotate
            Set
            For more information, see Authenticating Users with Redis AUTH
    user_group_ids_to_add(List[str], optional): The ID of the user group you are associating with the replication group.
    user_group_ids_to_remove(List[str], optional): The ID of the user group to disassociate from the replication group, meaning the users in
            the group no longer can access the replication group.
    remove_user_groups(bool, optional): Removes the user group associated with this replication group.
    timeout(Dict, optional): Timeout configuration for create/update of AWS DB Cluster.
        * create (Dict) -- Timeout configuration for creating DB Instance
            * delay(int) -- The amount of time in seconds to wait between attempts.Defaults to 30
            * max_attempts(int) -- Customized timeout configuration containing delay and max attempts.Defaults to 60
        * update (Dict) -- Timeout configuration for updating DB Instance
            * delay(int) -- The amount of time in seconds to wait between attempts.Defaults to 30
            * max_attempts(int) -- Customized timeout configuration containing delay and max attempts.Defaults to 60

Request Syntax:
    [cache_replication_group_name]:
      aws.elasticache.replication_group.present:
        - replication_group_description: 'string'
        - engine: 'string'
        - cache_node_type: 'string'
        - cache_subnet_group_name: 'string'
        - cache_parameter_group_name: 'string'
        - cache_security_group_names: 'string'
        - primary_cluster_id: 'string'
        - automatic_failover_enabled: 'bool
        - multi_az_enabled: 'bool
        - num_cache_clusters: 'int'
        - num_node_groups: 'int'
        - replicas_per_node_group: 'int'
        - tags:
            - 'string': 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        cache_replication_group_name:
          aws.elasticache.replication_group.present:
            - replication_group_description: Testing idem aws replication group
            - engine: Redis
            - cache_node_type: cache.t2.micro
            - cache_subnet_group_name: idem-test
            - cache_parameter_group_name: idem-test-parameter-group-name
            - cache_security_group_names: idem-test-security_group_names
            - primary_cluster_id: idem-test-primary_cluster_id
            - automatic_failover_enabled: disabled
            - multi_az_enabled: disabled
            - num_cache_clusters: 123
            - num_node_groups: 1
            - replicas_per_node_group: 1
            - tags:
                - Product119: vj-test-elasticache1119
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.elasticache.replication_group](https://docs.idemproject.io/idem-aws/en/latest/ref/states/elasticache/replication_group.html).
