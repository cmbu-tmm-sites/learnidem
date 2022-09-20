---
title: "aws.config.rule"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified Config rule and all of its evaluation results. Config sets the state of a rule to DELETING
until the deletion is complete. You cannot update a rule while it is in this state. If you make a PutConfigRule or
DeleteConfigRule request for the rule, you will receive a ResourceInUseException.

Args:
    name(Text): An Idem name of the rule.
    resource_id(Text, optional): AWS Config Rule Name. Idem automatically considers this resource being absent
     if this field is not specified.

Returns:
      Dict[str, Any]

Examples:
      .. code-block:: sls

        ec2-instance-no-public-ip:
          aws.config.rule.absent:
          - name: ec2-instance-no-public-ip
          - resource_id: ec2-instance-no-public-ip
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Return details about your Config rules.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.config.rule
```
{{< /tab >}}

{{< tab "present" >}}

```
Adds or updates Config rule for evaluating whether your Amazon Web Services resources comply with your desired
configurations. For more information about rules, please see AWS Config services
Args:
    name(Text): An Idem name of the rule.
    resource_id(Text, Optional): AWS Config Rule Name.
    scope(Dict[str, Any], optional): Defines which resources can trigger an evaluation for the rule. The scope can include one or
        more resource types, a combination of one resource type and one resource ID, or a combination of
        a tag key and value. Specify a scope to constrain the resources that can trigger an evaluation
        for the rule. If you do not specify a scope, evaluations are triggered when any resource in the
        recording group changes.  The scope can be empty.
            * ComplianceResourceTypes (List[str], optional): The resource types of only those Amazon Web Services resources that you want to trigger an
                evaluation for the rule. You can only specify one type if you also specify a resource ID for
                ComplianceResourceId.
            * TagKey (str, optional): The tag key that is applied to only those Amazon Web Services resources that you want to trigger
                an evaluation for the rule.
            * TagValue (str, optional): The tag value applied to only those Amazon Web Services resources that you want to trigger an
                evaluation for the rule. If you specify a value for TagValue, you must also specify a value for
                TagKey.
            * ComplianceResourceId (str, optional): The ID of the only Amazon Web Services resource that you want to trigger an evaluation for the
                rule. If you specify a resource ID, you must specify one resource type for
                ComplianceResourceTypes.
    source (Dict[str, Any]): Provides the rule owner (Amazon Web Services or customer), the rule identifier, and the
        notifications that cause the function to evaluate your Amazon Web Services resources.
        * Owner (str): Indicates whether Amazon Web Services or the customer owns and manages the Config rule. Config
            Managed Rules are predefined rules owned by Amazon Web Services. For more information, see
            Config Managed Rules in the Config developer guide. Config Custom Rules are rules that you can
            develop either with Guard (CUSTOM_POLICY) or Lambda (CUSTOM_LAMBDA). For more information, see
            Config Custom Rules  in the Config developer guide.
        * SourceIdentifier (str, optional): For Config Managed rules, a predefined identifier from a list. For example, IAM_PASSWORD_POLICY
            is a managed rule. To reference a managed rule, see List of Config Managed Rules. For Config
            Custom Lambda rules, the identifier is the Amazon Resource Name (ARN) of the rule's Lambda
            function, such as arn:aws:lambda:us-east-2:123456789012:function:custom_rule_name. For Config
            Custom Policy rules, this field will be ignored.
        * SourceDetails (List[Dict[str, Any]], optional): Provides the source and the message types that cause Config to evaluate your Amazon Web Services
            resources against a rule. It also provides the frequency with which you want Config to run
            evaluations for the rule if the trigger type is periodic. If the owner is set to CUSTOM_POLICY,
            the only acceptable values for the Config rule trigger message type are
            ConfigurationItemChangeNotification and OversizedConfigurationItemChangeNotification.
            * EventSource (str, optional): The source of the event, such as an Amazon Web Services service, that triggers Config to
                evaluate your Amazon Web Services resources.
            * MessageType (str, optional): The type of notification that triggers Config to run an evaluation for a rule. You can specify
                the following notification types:
                    ConfigurationItemChangeNotification - Triggers an evaluation when Config delivers a configuration item as a result of a resource change.
                    OversizedConfigurationItemChangeNotification - Triggers an evaluation when Config delivers an
                        oversized configuration item. Config may generate this notification type when a resource changes
                        and the notification exceeds the maximum size allowed by Amazon SNS.
                    ScheduledNotification - Triggers a periodic evaluation at the frequency specified for MaximumExecutionFrequency.
                    ConfigurationSnapshotDeliveryCompleted - Triggers a periodic evaluation when Config delivers a
                        configuration snapshot.
                If you want your custom rule to be triggered by configuration changes,
                specify two SourceDetail objects, one for ConfigurationItemChangeNotification and one for
                OversizedConfigurationItemChangeNotification.
            * MaximumExecutionFrequency (str, optional): The frequency at which you want Config to run evaluations for a custom rule with a periodic
                trigger. If you specify a value for MaximumExecutionFrequency, then MessageType must use the
                ScheduledNotification value.  By default, rules with a periodic trigger are evaluated every 24
                hours. To change the frequency, specify a valid value for the MaximumExecutionFrequency
                parameter. Based on the valid value you choose, Config runs evaluations once for each valid
                value. For example, if you choose Three_Hours, Config runs evaluations once every three hours.
                In this case, Three_Hours is the frequency of this rule.
        * CustomPolicyDetails (Dict[str, Any], optional): Provides the runtime system, policy definition, and whether debug logging is enabled. Required
            when owner is set to CUSTOM_POLICY.
            * PolicyRuntime (str): The runtime system for your Config Custom Policy rule. Guard is a policy-as-code language that
                allows you to write policies that are enforced by Config Custom Policy rules. For more
                information about Guard, see the Guard GitHub Repository.
            * PolicyText (str): The policy definition containing the logic for your Config Custom Policy rule.
            * EnableDebugLogDelivery (bool, optional): The boolean expression for enabling debug logging for your Config Custom Policy rule. The
                default value is false.
    max_execution_frequency(Text, Optional): The maximum frequency with which Config runs evaluations for a rule. Default
     is 24 hours
    input_parameters(Text, Optional): A string, in JSON format, that is passed to the Config rule.
    tags (Dict or List, Optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the Config rule.
        * (Key, optional): One part of a key-value pair that make up a tag. A key is a general label that acts like a
            category for more specific tag values.
        * (Value, optional): The optional part of a key-value pair that make up a tag. A value acts as a descriptor within a
            tag category (key).

    tags(List or Dict, Optional): list of tags in the format of [{"Key": tag-key, "Value": tag-value}] or dict in the format of
     {tag-key: tag-value}. The tags for the resource. The metadata that you apply to a resource to help you categorize and
     organize them. Defaults to None

Request syntax:
    [aws-config-rule]:
      aws.config.rule.present:
      - name: 'string'
      - resource_id: 'string'
      - scope: dict
        ComplianceResourceTypes: list
      - source: dict
        Owner: 'string'
        SourceIdentifier: 'string'

Returns:
     None

Examples:
    .. code-block:: sls

        ec2-instance-no-public-ip:
          aws.config.rule.present:
          - name: ec2-instance-no-public-ip
          - resource_id: ec2-instance-no-public-ip
          - tags:
            - Key: ENV
              Value: Test
            - Key: Service
              Value: TestService
          - config_rule_name: ec2-instance-no-public-ip
          - scope:
              ComplianceResourceTypes:
              - AWS::EC2::Instance
              - AWS::EC2::Host
          - source:
              Owner: AWS
              SourceIdentifier: EC2_INSTANCE_NO_PUBLIC_IP
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.config.rule](https://docs.idemproject.io/idem-aws/en/latest/ref/states/config/rule.html).
