---
title: "aws.config.config_recorder"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the configuration recorder. After the configuration recorder is deleted,
Config will not record resource configuration changes until you create a new configuration recorder.

Args:
    name(Text): The name of the recorder.
    resource_id(Text, optional): AWS Config configuration recorder Name. Idem automatically considers this resource being absent
     if this field is not specified.

Returns:
      Dict[str, Any]

Examples:
      .. code-block:: sls

        aws-config-recorder:
          aws.config.config_recorder.present:
            - name: 'config_recorder'
            - resource_id: 'config_recorder'
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Return details about your config recorder.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.config.config_recorder
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a new configuration recorder to record the selected resource configurations, please see AWS Config services
Args:
    name(Text): The name of the recorder.
    role_arn (Text): Amazon Resource Name (ARN) of the IAM role used to describe the Amazon Web Services resources associated with the account.
    recording_group (Dict[str, Any], optional): Specifies the types of Amazon Web Services resources for which Config records configuration
        changes.
        * allSupported (bool, optional): Specifies whether Config records configuration changes for every supported type of regional
            resource. If you set this option to true, when Config adds support for a new type of regional
            resource, it starts recording resources of that type automatically. If you set this option to
            true, you cannot enumerate a list of resourceTypes.
        * includeGlobalResourceTypes (bool, optional): Specifies whether Config includes all supported types of global resources (for example, IAM
            resources) with the resources that it records. Before you can set this option to true, you must
            set the allSupported option to true. If you set this option to true, when Config adds support
            for a new type of global resource, it starts recording resources of that type automatically. The
            configuration details for any global resource are the same in all regions. To prevent duplicate
            configuration items, you should consider customizing Config in only one region to record global
            resources.
         * resourceTypes (List[str], optional): A comma-separated list that specifies the types of Amazon Web Services resources for which
            Config records configuration changes (for example, AWS::EC2::Instance or
            AWS::CloudTrail::Trail). To record all configuration changes, you must set the allSupported
            option to true. If you set this option to false, when Config adds support for a new type of
            resource, it will not record resources of that type unless you manually add that type to your
            recording group. For a list of valid resourceTypes values, see the resourceType Value column in
            Supported Amazon Web Services resource Types.
    recording (Bool, Optional): Specifies recording status of the configuration recorder. Default is False.
    resource_id (Text, Optional): The name of the recorder.

Request syntax:
    [aws-config-recorder]:
      aws.config.config_recorder.present:
      - name: 'string'
      - resource_id: 'string'
      - role_arn 'string'
      - recording: 'string'
      - recording_group: 'dict'

Returns:
     Dict[str, Any]

Examples:
    .. code-block:: sls
        aws-config-recorder:
          aws.config.config_recorder.present:
            - name: 'config_recorder'
            - resource_id: 'config_recorder'
            - role_arn 'arn:aws:iam::012345678912:role/aws-service-role/config.amazonaws.com/AWSServiceRoleForConfig'
            - recording: true
            - recording_group:
                allSupported: false
                includeGlobalResourceTypes: false
                resourceTypes:
                - "AWS::ApiGateway::Stage"
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.config.config_recorder](https://docs.idemproject.io/idem-aws/en/latest/ref/states/config/config_recorder.html).
