---
title: "aws.events.rule"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified rule. Before you can delete the rule, you must remove all targets, using RemoveTargets.
When you delete a rule, incoming events might continue to match to the deleted rule. Allow a short period of
time for changes to take effect. If you call delete rule multiple times for the same rule, all calls will
succeed. When you call delete rule for a non-existent custom eventbus, ResourceNotFoundException is returned.
Managed rules are rules created and managed by another Amazon Web Services service on your behalf. These rules
are created by those other Amazon Web Services to support functionality in those services. You can
delete these rules using the Force option, but you should do so only if you are sure the other service is not
still using that rule.

Args:
    ctx:
    hub:
    resource_id(Text): The name of the AWS CloudWatch Events Rule.
    name(Text): A name, ID to identify the resource.
    event_bus_name (Text, Optional) : The name or ARN of the event bus to associate with this rule.
        If you omit this, the default event bus is used.

Request Syntax:
[rule-id]:
  aws.events.rule.absent:
  - name: 'string'
  - resource_id: 'string'
  - event_bus_name: 'string'
  - qualifier: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.events.rule.absent:
            - name: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists your Amazon EventBridge rules. You can either list all the rules or you can provide a prefix to match to
the rule names. ListRules does not list the targets of a rule. To see the targets associated with a rule, use
ListTargetsByRule.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.events.rule
```
{{< /tab >}}

{{< tab "present" >}}

```
Enables the specified rule. If the rule does not exist, the operation fails. When you enable a rule, incoming
events might not immediately start matching to a newly enabled rule. Allow a short period of time for changes to
take effect.

Args:
    hub:
    ctx:
    name(Text): A name, ID to identify the resource.
    resource_id(Text, Optional): The name of the AWS CloudWatch Events Rule.
    targets(List[Dict[str, Any]]): The targets to update or add to the rule.
        * Id (str): The ID of the target within the specified rule. Use this ID to reference the target when
            updating the rule. We recommend using a memorable and unique string.
        * Arn (str): The Amazon Resource Name (ARN) of the target.
        * RoleArn (str, optional): The Amazon Resource Name (ARN) of the IAM role to be used for this target when the rule is
            triggered. If one rule triggers multiple targets, you can use a different IAM role for each
            target.
        * Input (str, optional): Valid JSON text passed to the target. In this case, nothing from the event itself is passed to
            the target. For more information, see The JavaScript Object Notation (JSON) Data Interchange
            Format.
        * InputPath (str, optional): The value of the JSONPath that is used for extracting part of the matched event when passing it
            to the target. You must use JSON dot notation, not bracket notation. For more information about
            JSON paths, see JSONPath.
        * InputTransformer (Dict[str, Any], optional): Settings to enable you to provide custom input to a target based on certain event data. You can
            extract one or more key-value pairs from the event and then use that data to send customized
            input to the target.
            * InputPathsMap (Dict[str, str], optional): Map of JSON paths to be extracted from the event. You can then insert these in the template in
        InputTemplate to produce the output you want to be sent to the target.  InputPathsMap is an
        array key-value pairs, where each value is a valid JSON path. You can have as many as 100 key-
        value pairs. You must use JSON dot notation, not bracket notation. The keys cannot start with
        "Amazon Web Services."
            * InputTemplate (str): Input template where you specify placeholders that will be filled with the values of the keys
                from InputPathsMap to customize the data sent to the target. Enclose each InputPathsMaps value
                in brackets: <value> The InputTemplate must be valid JSON. If InputTemplate is a JSON object
                (surrounded by curly braces), the following restrictions apply:   The placeholder cannot be used
                as an object key.   The following example shows the syntax for using InputPathsMap and
                InputTemplate.
                   "InputTransformer":
                   {
                        "InputPathsMap": {"instance": "$.detail.instance","status": "$.detail.status"},
                        "InputTemplate": "<instance> is in state <status>"
                   }
                To have the InputTemplate include quote marks within a JSON string, escape each
                quote marks with a slash, as in the following example:
                   "InputTransformer":   {
                        "InputPathsMap": {"instance": "$.detail.instance","status": "$.detail.status"},
                        "InputTemplate": "<instance> is in state \"<status>\""
                        }
                The InputTemplate can also be valid JSON with varibles in quotes or out, as in the following example:
                   "InputTransformer":   {
                        "InputPathsMap": {"instance": "$.detail.instance","status": "$.detail.status"},
                        "InputTemplate": '{"myInstance": <instance>,"myStatus": "<instance> is in state \"<status>\""}'
                    }
        * KinesisParameters (Dict[str, Any], optional): The custom parameter you can use to control the shard assignment, when the target is a Kinesis
            data stream. If you do not include this parameter, the default is to use the eventId as the
            partition key.
            * PartitionKeyPath (str): The JSON path to be extracted from the event and used as the partition key. For more
                information, see Amazon Kinesis Streams Key Concepts in the Amazon Kinesis Streams Developer
                Guide.
        * RunCommandParameters (Dict[str, Any], optional): Parameters used when you are using the rule to invoke Amazon EC2 Run Command.
            * RunCommandTargets (List[Dict[str, Any]]): Currently, we support including only one RunCommandTarget block, which specifies either an array
                of InstanceIds or a tag.
                * Key (str): Can be either tag: tag-key or InstanceIds.
                * Values (List[str]): If Key is tag: tag-key, Values is a list of tag values. If Key is InstanceIds, Values is a list
                    of Amazon EC2 instance IDs.
        * EcsParameters (Dict[str, Any], optional): Contains the Amazon ECS task definition and task count to be used, if the event target is an
            Amazon ECS task. For more information about Amazon ECS tasks, see Task Definitions  in the
            Amazon EC2 Container Service Developer Guide.
            * TaskDefinitionArn (str): The ARN of the task definition to use if the event target is an Amazon ECS task.
            * TaskCount (int, optional): The number of tasks to create based on TaskDefinition. The default is 1.
            * LaunchType (str, optional): Specifies the launch type on which your task is running. The launch type that you specify here
                must match one of the launch type (compatibilities) of the target task. The FARGATE value is
                supported only in the Regions where Fargate with Amazon ECS is supported. For more information,
                see Fargate on Amazon ECS in the Amazon Elastic Container Service Developer Guide.
            * NetworkConfiguration (Dict[str, Any], optional): Use this structure if the Amazon ECS task uses the awsvpc network mode. This structure specifies
                the VPC subnets and security groups associated with the task, and whether a public IP address is
                to be used. This structure is required if LaunchType is FARGATE because the awsvpc mode is
                required for Fargate tasks. If you specify NetworkConfiguration when the target ECS task does
                not use the awsvpc network mode, the task fails.
                * awsvpcConfiguration (Dict[str, Any], optional): Use this structure to specify the VPC subnets and security groups for the task, and whether a
                    public IP address is to be used. This structure is relevant only for ECS tasks that use the
                    awsvpc network mode.
                    * Subnets (List[str]): Specifies the subnets associated with the task. These subnets must all be in the same VPC. You
                        can specify as many as 16 subnets.
                    * SecurityGroups (List[str], optional): Specifies the security groups associated with the task. These security groups must all be in the
                        same VPC. You can specify as many as five security groups. If you do not specify a security
                        group, the default security group for the VPC is used.
                    * AssignPublicIp (str, optional): Specifies whether the task's elastic network interface receives a public IP address. You can
                        specify ENABLED only when LaunchType in EcsParameters is set to FARGATE.
            * PlatformVersion (str, optional): Specifies the platform version for the task. Specify only the numeric portion of the platform
                version, such as 1.1.0. This structure is used only if LaunchType is FARGATE. For more
                information about valid platform versions, see Fargate Platform Versions in the Amazon Elastic
                Container Service Developer Guide.
            * Group (str, optional): Specifies an ECS task group for the task. The maximum length is 255 characters.
            * CapacityProviderStrategy (List[Dict[str, Any]], optional): The capacity provider strategy to use for the task. If a capacityProviderStrategy is specified,
                the launchType parameter must be omitted. If no capacityProviderStrategy or launchType is
                specified, the defaultCapacityProviderStrategy for the cluster is used.
                * capacityProvider (str): The short name of the capacity provider.
                * weight (int, optional): The weight value designates the relative percentage of the total number of tasks launched that
                    should use the specified capacity provider. The weight value is taken into consideration after
                    the base value, if defined, is satisfied.
                * base (int, optional): The base value designates how many tasks, at a minimum, to run on the specified capacity
                    provider. Only one capacity provider in a capacity provider strategy can have a base defined. If
                    no value is specified, the default value of 0 is used.
            * EnableECSManagedTags (bool, optional): Specifies whether to enable Amazon ECS managed tags for the task. For more information, see
                Tagging Your Amazon ECS Resources in the Amazon Elastic Container Service Developer Guide.
            * EnableExecuteCommand (bool, optional): Whether or not to enable the execute command functionality for the containers in this task. If
                true, this enables execute command functionality on all containers in the task.
            * PlacementConstraints (List[Dict[str, Any]], optional): An array of placement constraint objects to use for the task. You can specify up to 10
                constraints per task (including constraints in the task definition and those specified at
                runtime).
                * type (str, optional): The type of constraint. Use distinctInstance to ensure that each task in a particular group is
                    running on a different container instance. Use memberOf to restrict the selection to a group of
                    valid candidates.
                * expression (str, optional): A cluster query language expression to apply to the constraint. You cannot specify an expression
                    if the constraint type is distinctInstance. To learn more, see Cluster Query Language in the
                    Amazon Elastic Container Service Developer Guide.
            * PlacementStrategy (List[Dict[str, Any]], optional): The placement strategy objects to use for the task. You can specify a maximum of five strategy
                rules per task.
                * type (str, optional): The type of placement strategy. The random placement strategy randomly places tasks on available
                    candidates. The spread placement strategy spreads placement across available candidates evenly
                    based on the field parameter. The binpack strategy places tasks on available candidates that
                    have the least available amount of the resource that is specified with the field parameter. For
                    example, if you binpack on memory, a task is placed on the instance with the least amount of
                    remaining memory (but still enough to run the task).
                * field (str, optional): The field to apply the placement strategy against. For the spread placement strategy, valid
                    values are instanceId (or host, which has the same effect), or any platform or custom attribute
                    that is applied to a container instance, such as attribute:ecs.availability-zone. For the
                    binpack placement strategy, valid values are cpu and memory. For the random placement strategy,
                    this field is not used.
            * PropagateTags (str, optional): Specifies whether to propagate the tags from the task definition to the task. If no value is
                specified, the tags are not propagated. Tags can only be propagated to the task during task
                creation. To add tags to a task after task creation, use the TagResource API action.
            * ReferenceId (str, optional): The reference ID to use for the task.
            * Tags (List[Dict[str, Any]], optional): The metadata that you apply to the task to help you categorize and organize them. Each tag
                consists of a key and an optional value, both of which you define. To learn more, see RunTask in
                the Amazon ECS API Reference.
                * Key (str): A string you can use to assign a value. The combination of tag keys and values can help you
        organize and categorize your resources.
                * Value (str): The value for the specified tag key.
        * BatchParameters (Dict[str, Any], optional): If the event target is an Batch job, this contains the job definition, job name, and other
            parameters. For more information, see Jobs in the Batch User Guide.
            * JobDefinition (str): The ARN or name of the job definition to use if the event target is an Batch job. This job
                definition must already exist.
            * JobName (str): The name to use for this execution of the job, if the target is an Batch job.
            * ArrayProperties (Dict[str, Any], optional): The array properties for the submitted job, such as the size of the array. The array size can be
                between 2 and 10,000. If you specify array properties for a job, it becomes an array job. This
                parameter is used only if the target is an Batch job.
                * Size (int, optional): The size of the array, if this is an array batch job. Valid values are integers between 2 and
                    10,000.
            * RetryStrategy (Dict[str, Any], optional): The retry strategy to use for failed jobs, if the target is an Batch job. The retry strategy is
                the number of times to retry the failed job execution. Valid values are 1–10. When you specify a
                retry strategy here, it overrides the retry strategy defined in the job definition.
                * Attempts (int, optional): The number of times to attempt to retry, if the job fails. Valid values are 1–10.
        * SqsParameters (Dict[str, Any], optional): Contains the message group ID to use when the target is a FIFO queue. If you specify an SQS FIFO
            queue as a target, the queue must have content-based deduplication enabled.
            * MessageGroupId (str, optional): The FIFO message group ID to use as the target.
        * HttpParameters (Dict[str, Any], optional): Contains the HTTP parameters to use when the target is a API Gateway REST endpoint or
            EventBridge ApiDestination. If you specify an API Gateway REST API or EventBridge ApiDestination
            as a target, you can use this parameter to specify headers, path parameters, and query string
            keys/values as part of your target invoking request. If you're using ApiDestinations, the
            corresponding Connection can also have these values configured. In case of any conflicting keys,
            values from the Connection take precedence.
            * PathParameterValues (List[str], optional): The path parameter values to be used to populate API Gateway REST API or EventBridge
                ApiDestination path wildcards ("*").
            * HeaderParameters (Dict[str, str], optional): The headers that need to be sent as part of request invoking the API Gateway REST API or
                EventBridge ApiDestination.
            * QueryStringParameters (Dict[str, str], optional): The query string keys/values that need to be sent as part of request invoking the API Gateway
                REST API or EventBridge ApiDestination.
        * RedshiftDataParameters (Dict[str, Any], optional): Contains the Amazon Redshift Data API parameters to use when the target is a Amazon Redshift
            cluster. If you specify a Amazon Redshift Cluster as a Target, you can use this to specify
            parameters to invoke the Amazon Redshift Data API ExecuteStatement based on EventBridge events.
            * SecretManagerArn (str, optional): The name or ARN of the secret that enables access to the database. Required when authenticating
                using Amazon Web Services Secrets Manager.
            * Database (str): The name of the database. Required when authenticating using temporary credentials.
            * DbUser (str, optional): The database user name. Required when authenticating using temporary credentials.
            * Sql (str): The SQL statement text to run.
            * StatementName (str, optional): The name of the SQL statement. You can name the SQL statement when you create it to identify the
                query.
            * WithEvent (bool, optional): Indicates whether to send an event back to EventBridge after the SQL statement runs.
        * SageMakerPipelineParameters (Dict[str, Any], optional): Contains the SageMaker Model Building Pipeline parameters to start execution of a SageMaker
            Model Building Pipeline. If you specify a SageMaker Model Building Pipeline as a target, you can
            use this to specify parameters to start a pipeline execution based on EventBridge events.
            * PipelineParameterList (List[Dict[str, Any]], optional): List of Parameter names and values for SageMaker Model Building Pipeline execution.
                * Name (str): Name of parameter to start execution of a SageMaker Model Building Pipeline.
                * Value (str): Value of parameter to start execution of a SageMaker Model Building Pipeline.
        * DeadLetterConfig (Dict[str, Any], optional): The DeadLetterConfig that defines the target queue to send dead-letter queue events to.
            * Arn (str, optional): The ARN of the SQS queue specified as the target for the dead-letter queue.
        * RetryPolicy (Dict[str, Any], optional): The RetryPolicy object that contains the retry policy configuration to use for the dead-letter
            queue.
            * MaximumRetryAttempts (int, optional): The maximum number of retry attempts to make before the request fails. Retry attempts continue
                until either the maximum number of attempts is made or until the duration of the
                MaximumEventAgeInSeconds is met.
            * MaximumEventAgeInSeconds (int, optional): The maximum amount of time, in seconds, to continue to make retry attempts.
    schedule_expression (Text, Optional): Scheduling expression.
        For example, "cron(0 20 * * ? *)" or "rate(5 minutes)".
    event_pattern (Text, Optional): Rules use event patterns to select events and route them to targets. A pattern
        either matches an event or it doesn't. Event patterns are represented as JSON objects with a structure that
        is similar to that of events.
    rule_status (Text, Optional): Indicates whether the rule is enabled or disabled.
    description (Text, Optional): A description of the rule.
    role_arn (Text, Optional): The Amazon Resource Name (ARN) of the IAM role associated with the rule.
        If you're setting an event bus in another account as the target and that account granted permission to your
        account through an organization instead of directly by the account ID, you must specify a RoleArn with proper
        permissions in the Target structure, instead of here in this parameter.
    event_bus_name (Text, Optional) : The name or ARN of the event bus to associate with this rule.
        If you omit this, the default event bus is used.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the event.
        Each tag consists of a key name and an associated value. Defaults to None.
        * Key (str, optional): The key of the tag. Constraints: Tag keys are case-sensitive and accept a maximum of 127 Unicode
            characters. May not begin with aws:.
        * Value(str, optional): The value of the tag. Constraints: Tag values are case-sensitive and accept a maximum of 256
            Unicode characters.

Request Syntax:
    [cloudwatch-events-rule-id]:
      aws.events.rule.present:
        - name: event_rule
        - arn: arn:aws:events:us-west-1:000000000000:rule/qqqqqqq
        - rule_status: ENABLED | DISABLED
        - schedule_expression: rate(5 minutes)
        - event_bus_name: default
        - tags:
          - Key: 'string'
            Value: 'string'


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        event_rule_id:
            aws.events.rule.present:
              - name: event_rule
              - arn: arn:aws:events:us-west-1:000000000000:rule/test
              - rule_status: ENABLED | DISABLED
              - schedule_expression: rate(5 minutes)
              - event_bus_name: default
              - tags:
                - Key: idem_test_event_rule1
                  Value: test value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.events.rule](https://docs.idemproject.io/idem-aws/en/latest/ref/states/events/rule.html).
