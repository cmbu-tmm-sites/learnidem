---
title: "aws.cloudwatch.metric_alarm"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified alarms. You can delete up to 100 alarms in one operation. However, this total can include no
more than one composite alarm. For example, you could delete 99 metric alarms and one composite alarms with one
operation, but you can't delete two composite alarms with one operation.

Args:
    name(Text): The AWS name of the metric alarm.
    resource_id(Text, optional): The AWS name of the metric alarm. Idem automatically considers this resource
     being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        [alarm name]:
           aws.cloudwatch.metric_alarm.absent:
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Retrieves the specified alarms. You can filter the results by specifying a prefix for the alarm name, the alarm
state, or a prefix for any action. To use this operation and return information about composite alarms, you must
be signed on with the cloudwatch:DescribeAlarms permission that is scoped to * . You can't return information
about composite alarms if your cloudwatch:DescribeAlarms permission has a narrower scope.

Returns:
    Dict[str, Any]

Examples:
    .. code-block:: bash

        $ idem describe aws.cloudwatch.metric_alarm
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates or updates an alarm and associates it with the specified metric, metric math expression, or anomaly
detection model.Alarms based on anomaly detection models cannot have Auto Scaling actions. When this operation
creates an alarm, the alarm state is immediately set to INSUFFICIENT_DATA . The alarm is then evaluated and its
state is set appropriately. Any actions associated with the new state are then executed. When you update an
existing alarm, its state is left unchanged, but the update completely overwrites the previous configuration
of the alarm. If you are an IAM user,
you must have Amazon EC2 permissions for some alarm operations:
    * The iam:CreateServiceLinkedRole for all alarms with EC2 actions
    * The iam:CreateServiceLinkedRole to create an alarm with Systems Manager OpsItem actions.
The first time you create an alarm in the Amazon Web Services Management Console, the CLI, or by using the
PutMetricAlarm API, CloudWatch creates the necessary service-linked role for you. The service-linked roles are
called AWSServiceRoleForCloudWatchEvents and AWSServiceRoleForCloudWatchAlarms_ActionSSM.

Args:
    name(Text): The name for the alarm. This name must be unique within the Region.
    resource_id(Text): The AWS name of the metric alarm.
    alarm_description(Text, Optional): The description for the alarm.
    actions_enabled(Boolean, Optional): Indicates whether actions should be executed during any changes to the alarm
        state. The default is TRUE .
    ok_actions(List, Optional): The actions to execute when this alarm transitions to an OK state from any other state.
        Each action is specified as an Amazon Resource Name (ARN).
        Valid Values:
            arn:aws:automate:*region* :ec2:stop | arn:aws:automate:*region* :ec2:terminate |
            arn:aws:automate:*region* :ec2:recover | arn:aws:automate:*region* :ec2:reboot |
            ``arn:aws:sns:region :account-id :sns-topic-name `` |
            ``arn:aws:autoscaling:region :account-id :scalingPolicy:policy-id
            :autoScalingGroupName/group-friendly-name :policyName/policy-friendly-name ``
        Valid Values (for use with IAM roles):
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Stop/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Terminate/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Reboot/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Recover/1.0
    alarm_actions(List, Optional):The actions to execute when this alarm transitions to the ALARM state from any
        other state.
        Each action is specified as an Amazon Resource Name (ARN).
        Valid Values:
            arn:aws:automate:*region* :ec2:stop |
            arn:aws:automate:*region* :ec2:terminate |
            arn:aws:automate:*region* :ec2:recover |
            arn:aws:automate:*region* :ec2:reboot |
            ``arn:aws:sns:region :account-id :sns-topic-name `` |
             ``arn:aws:autoscaling:region :account-id :scalingPolicy:policy-id
             :autoScalingGroupName/group-friendly-name :policyName/policy-friendly-name `` |
            ``arn:aws:ssm:region :account-id :opsitem:severity `` |
            ``arn:aws:ssm-incidents::account-id :response-plan:response-plan-name ``
       Valid Values (for use with IAM roles):
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Stop/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Terminate/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Reboot/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Recover/1.0

    insufficient_data_actions(List, Optional):The actions to execute when this alarm transitions to the
    INSUFFICIENT_DATA state from any other state. Each action is specified as an Amazon Resource Name (ARN).
        Valid Values:
            arn:aws:automate:*region* :ec2:stop |
            arn:aws:automate:*region* :ec2:terminate |
            arn:aws:automate:*region* :ec2:recover |
            arn:aws:automate:*region* :ec2:reboot |
            ``arn:aws:sns:region :account-id :sns-topic-name `` |
            ``arn:aws:autoscaling:region :account-id :scalingPolicy:policy-id
            :autoScalingGroupName/group-friendly-name :policyName/policy-friendly-name ``
        Valid Values (for use with IAM roles):
            >arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Stop/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Terminate/1.0 |
            arn:aws:swf:*region* :*account-id* :action/actions/AWS_EC2.InstanceId.Reboot/1.0
    metric_name(Text, Optional): The name for the metric associated with the alarm. For each PutMetricAlarm operation,
        you must specify either MetricName or a Metrics array.
    namespace(Text, Optional): The namespace for the metric associated specified in MetricName .
    statistic(Text, Optional): The statistic for the metric specified in MetricName , other than percentile. For
        percentile statistics, use ExtendedStatistic . When you call PutMetricAlarm and specify a MetricName ,
        you must specify either Statistic or ExtendedStatistic, but not both.
    extended_statistic(Text, Optional): The percentile statistic for the metric specified in MetricName . Specify a value
        between p0.0 and p100. When you call PutMetricAlarm and specify a MetricName , you must specify either
        Statistic or ExtendedStatistic, but not both.
    dimensions(List[Dict[str, Any]], optional): The dimensions for the metric specified in MetricName. Defaults to None.
        * Name (str): The name of the dimension. Dimension names must contain only ASCII characters, must include at
            least one non-whitespace character, and cannot start with a colon (:).
        * Value (str): The value of the dimension. Dimension values must contain only ASCII characters and must include
            at least one non-whitespace character.
    period(Integer): The length, in seconds, used each time the metric specified in MetricName is evaluated.
        Valid values are 10, 30, and any multiple of 60.
    unit(Text, Optional): The unit of measure for the statistic. For example, the units for the Amazon EC2 NetworkIn metric are
        Bytes because NetworkIn tracks the number of bytes that an instance receives on all network interfaces.
        You can also specify a unit when you create a custom metric. Units help provide conceptual meaning to your
        data. Metric data points that specify a unit of measure, such as Percent, are aggregated separately.
    evaluation_periods(Integer): The number of periods over which data is compared to the specified threshold.
        If you are setting an alarm that requires that a number of consecutive data points be breaching to trigger
        the alarm, this value specifies that number. If you are setting an "M out of N" alarm, this value is the N.
        An alarm's total current evaluation period can be no longer than one day, so this number multiplied by
        Period cannot be more than 86,400 seconds.

    datapoints_to_alarm(Integer, Optional): The number of data points that must be breaching to trigger the alarm.
        This is used only if you are setting an "M out of N" alarm. In that case, this value is the M.
    threshold(float, optional): The value against which the specified statistic is compared.  This parameter is required for
        alarms based on static thresholds, but should not be used for alarms based on anomaly detection models.
    comparison_operator(Text): The arithmetic operation to use when comparing the specified statistic and
        threshold. The specified statistic value is used as the first operand.
        The values LessThanLowerOrGreaterThanUpperThreshold , LessThanLowerThreshold , and
        GreaterThanUpperThreshold are used only for alarms based on anomaly detection models.
    treat_missing_data(Text, Optional): Sets how this alarm is to handle missing data points. If TreatMissingData is
        omitted, the default behavior of missing is used.
        Valid Values: breaching | notBreaching | ignore | missing
    evaluate_low_sample_count_percentile(Text, Optional): Used only for alarms based on percentiles. If you specify ignore ,
        the alarm state does not change during periods with too few data points to be statistically significant.
        If you specify evaluate or omit this parameter, the alarm is always evaluated and possibly changes state
        no matter how many data points are available.
    metrics(List[Dict[str, Any]], optional): An array of MetricDataQuery structures that enable you to create an alarm based on the result of
        a metric math expression. For each PutMetricAlarm operation, you must specify either MetricName
        or a Metrics array. Each item in the Metrics array either retrieves a metric or performs a math
        expression. One item in the Metrics array is the expression that the alarm watches. You
        designate this expression by setting ReturnData to true for this object in the array. For more
        information, see MetricDataQuery. If you use the Metrics parameter, you cannot include the
        MetricName, Dimensions, Period, Namespace, Statistic, or ExtendedStatistic parameters of
        PutMetricAlarm in the same operation. Instead, you retrieve the metrics you are using in your
        math expression as part of the Metrics array. Defaults to None.
        * Id (str): A short name used to tie this object to the results in the response. This name must be unique
            within a single call to GetMetricData. If you are performing math expressions on this set of
            data, this name represents that data and can serve as a variable in the mathematical expression.
            The valid characters are letters, numbers, and underscore. The first character must be a
            lowercase letter.
        * MetricStat (Dict[str, Any], optional): The metric to be returned, along with statistics, period, and units. Use this parameter only if
            this object is retrieving a metric and not performing a math expression on returned data. Within
            one MetricDataQuery object, you must specify either Expression or MetricStat but not both.
            * Metric (Dict[str, Any]): The metric to return, including the metric name, namespace, and dimensions.
                * Namespace (str, optional): The namespace of the metric.
                * MetricName (str, optional): The name of the metric. This is a required field.
                * Dimensions (List[Dict[str, Any]], optional): The dimensions for the metric.
                    * Name (str): The name of the dimension. Dimension names must contain only ASCII characters, must include at
                        least one non-whitespace character, and cannot start with a colon (:).
                    * Value (str): The value of the dimension. Dimension values must contain only ASCII characters and must include
                        at least one non-whitespace character.
            * Period (int): The granularity, in seconds, of the returned data points. For metrics with regular resolution, a
                period can be as short as one minute (60 seconds) and must be a multiple of 60. For high-
                resolution metrics that are collected at intervals of less than one minute, the period can be 1,
                5, 10, 30, 60, or any multiple of 60. High-resolution metrics are those metrics stored by a
                PutMetricData call that includes a StorageResolution of 1 second. If the StartTime parameter
                specifies a time stamp that is greater than 3 hours ago, you must specify the period as follows
                or no data points in that time range is returned:   Start time between 3 hours and 15 days ago -
                Use a multiple of 60 seconds (1 minute).   Start time between 15 and 63 days ago - Use a
                multiple of 300 seconds (5 minutes).   Start time greater than 63 days ago - Use a multiple of
                3600 seconds (1 hour).
            * Stat (str): The statistic to return. It can include any CloudWatch statistic or extended statistic.
            * Unit (str, optional): When you are using a Put operation, this defines what unit you want to use when storing the
                metric. In a Get operation, if you omit Unit then all data that was collected with any unit is
                returned, along with the corresponding units that were specified when the data was reported to
                CloudWatch. If you specify a unit, the operation returns only data that was collected with that
                unit specified. If you specify a unit that does not match the data collected, the results of the
                operation are null. CloudWatch does not perform unit conversions.
        * Expression (str, optional): This field can contain either a Metrics Insights query, or a metric math expression to be
            performed on the returned data. For more information about Metrics Insights queries, see Metrics
            Insights query components and syntax in the Amazon CloudWatch User Guide. A math expression can
            use the Id of the other metrics or queries to refer to those metrics, and can also use the Id of
            other expressions to use the result of those expressions. For more information about metric math
            expressions, see Metric Math Syntax and Functions in the Amazon CloudWatch User Guide. Within
            each MetricDataQuery object, you must specify either Expression or MetricStat but not both.
        * Label (str, optional): A human-readable label for this metric or expression. This is especially useful if this is an
            expression, so that you know what the value represents. If the metric or expression is shown in
            a CloudWatch dashboard widget, the label is shown. If Label is omitted, CloudWatch generates a
            default. You can put dynamic expressions into a label, so that it is more descriptive. For more
            information, see Using Dynamic Labels.
        * ReturnData (bool, optional): When used in GetMetricData, this option indicates whether to return the timestamps and raw data
            values of this metric. If you are performing this call just to do math expressions and do not
            also need the raw data returned, you can specify False. If you omit this, the default of True is
            used. When used in PutMetricAlarm, specify True for the one expression result to use as the
            alarm. For all other metrics and expressions in the same PutMetricAlarm operation, specify
            ReturnData as False.
        * Period (int, optional): The granularity, in seconds, of the returned data points. For metrics with regular resolution, a
            period can be as short as one minute (60 seconds) and must be a multiple of 60. For high-
            resolution metrics that are collected at intervals of less than one minute, the period can be 1,
            5, 10, 30, 60, or any multiple of 60. High-resolution metrics are those metrics stored by a
            PutMetricData operation that includes a StorageResolution of 1 second.
        * AccountId (str, optional): The ID of the account where the metrics are located, if this is a cross-account alarm. Use this
            field only for PutMetricAlarm operations. It is not used in GetMetricData operations.
    tags(List or Dict, Optional): A List of tags in the format of [{"Key": tag-key, "Value": tag-value}] or dict in the format of
        {tag-key: tag-value} to associate with the alarm. You can associate as many as 50 tags with
        an alarm. Tags can help you organize and categorize your resources. You can also use them to
        scope user permissions by granting a user permission to access or change only resources with
        certain tag values. If you are using this operation to update an existing alarm, any tags you
        specify in this parameter are ignored. To change the tags of an existing alarm, use TagResource
        or UntagResource. Defaults to None.
        * (Key): A string that you can use to assign a value. The combination of tag keys and values can help you
            organize and categorize your resources.
        * (Value): The value for the specified tag key.

Request Syntax:
    [metric-alarm-name]::
        aws.cloudwatch.metric_alarm.present:
        - name: 'string'
        - alarm_description: 'string'
        - actions_enabled: True|False
        - ok_actions= ['string']
        - alarm_actions: ['string']
        - insufficient_data_actions: ['string']
        - metric_name: 'string'
        - namespace: 'string'
        - statistic: 'SampleCount'|'Average'|'Sum'|'Minimum'|'Maximum'
        - dimensions: 'list'
        - period: 'integer'
        - unit: 'string'
        - evaluation_periods: 'integer'
        - datapoints_to_alarm: 'integer'
        - threshold: 'integer'
        - comparison_operator: 'string'
        - treat_missing_data: 'string',
        - evaluate_low_sample_count_percentile: 'string',
        - metrics: 'list'
        - threshold_metric_id: 'string'
        - tags:
          - Key: 'string'
            Value: 'string'

Returns:
     Dict[str, Any]


Examples:

    .. code-block:: sls

        awsec2-i-0f36e2b10a7463129-LessThanOrEqualToThreshold-CPUUtilization:
          aws.cloudwatch.metric_alarm.present:
            - name: awsec2-i-0f36e2b10a7463129-LessThanOrEqualToThreshold-CPUUtilization
            - alarm_description: "stop EC2 instance if it utilizes CPU less than 5"
            - actions_enabled: True
            - alarm_actions:
              - arn:aws:swf:*region*:*account-id*:action/actions/AWS_EC2.InstanceId.Stop/1.0
            - insufficient_data_actions: []
            - metric_name: CPUUtilization
            - namespace: AWS/EC2
            - statistic: Average
            - dimensions:
              - Name: InstanceId
                Value: i-0f36e2b10a7463129
            - period: 60
            - evaluation_periods: 1
            - datapoints_to_alarm: 1
            - threshold: 20
            - comparison_operator: LessThanThreshold
            - tags:
              - Key: type
                Value: metric_alarm
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.cloudwatch.metric_alarm](https://docs.idemproject.io/idem-aws/en/latest/ref/states/cloudwatch/metric_alarm.html).
