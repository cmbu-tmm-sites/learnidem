---
title: "aws.apigatewayv2.stage"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway v2 stage resource.

Args:
    name(string): An Idem name of the resource.
    api_id(string): The API resource identifier in Amazon Web Services.
    resource_id(string, optional): The stage resource name in Amazon Web Services.
        Idem automatically considers this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_stage:
          aws.apigatewayv2.stage.absent:
            - name: value
            - api_id: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the API Gateway v2 stage resources for an AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.apigatewayv2.stage
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an API Gateway v2 stage resource.

Args:
    name(string): An Idem name of the resource. This is also used as the name of the Stage during resource creation.
    api_id(string): The API resource identifier in Amazon Web Services.
    resource_id(string, optional): The stage resource name in Amazon Web Services.
    access_log_settings(Dict[str, Any], optional): Settings for logging access in this stage. Defaults to None.
        * DestinationArn (str, optional): The ARN of the CloudWatch Logs log group to receive access logs.
        * Format (str, optional): A single line format of the access logs of data, as specified by selected $context variables.
            The format must include at least $context.requestId.
    auto_deploy(bool, optional): Specifies whether updates to an API automatically trigger a new deployment.
    client_certificate_id(string, optional): The identifier of a client certificate for a Stage. Supported only for WebSocket APIs.
    default_route_settings(Dict[str, Any], optional): The default route settings for the stage. Defaults to None.
        * DataTraceEnabled (bool, optional): Specifies whether (true) or not (false) data trace logging is enabled for this route. This
            property affects the log entries pushed to Amazon CloudWatch Logs. Supported only for WebSocket
            APIs.
        * DetailedMetricsEnabled (bool, optional): Specifies whether detailed metrics are enabled.
        * LoggingLevel (str, optional): Specifies the logging level for this route: INFO, ERROR, or OFF. This property affects the log
            entries pushed to Amazon CloudWatch Logs. Supported only for WebSocket APIs.
        * ThrottlingBurstLimit (int, optional): Specifies the throttling burst limit.
        * ThrottlingRateLimit (float, optional): Specifies the throttling rate limit.
    deployment_id(string, optional): The deployment identifier of the API stage.
    description(string, optional): The description for the API stage.
    route_settings(Dict[str, Dict[str, Any]], optional): Route settings for the stage, by routeKey. Defaults to None.
        * DataTraceEnabled (bool, optional): Specifies whether (true) or not (false) data trace logging is enabled for this route. This
            property affects the log entries pushed to Amazon CloudWatch Logs. Supported only for WebSocket
            APIs.
        * DetailedMetricsEnabled (bool, optional): Specifies whether detailed metrics are enabled.
        * LoggingLevel (str, optional): Specifies the logging level for this route: INFO, ERROR, or OFF. This property affects the log
            entries pushed to Amazon CloudWatch Logs. Supported only for WebSocket APIs.
        * ThrottlingBurstLimit (int, optional): Specifies the throttling burst limit.
        * ThrottlingRateLimit (float, optional): Specifies the throttling rate limit.
    stage_variables(Dict, optional): A map that defines the stage variables for a Stage. Variable names can have alphanumeric and
        underscore characters, and the values must match [A-Za-z0-9-._~:/?#&=,]+.
    tags(Dict, optional): The collection of tags. Each tag element is associated with a given resource.

Request Syntax:
    [idem_test_aws_apigatewayv2_stage]:
      aws.apigatewayv2.stage.present:
        - name: 'string'
        - api_id: 'string'
        - access_log_settings: {
            'DestinationArn': 'string',
            'Format': 'string'
          }
        - auto_deploy: True|False
        - client_certificate_id: 'string'
        - default_route_settings:{
            'DataTraceEnabled': True|False,
            'DetailedMetricsEnabled': True|False,
            'LoggingLevel': 'ERROR'|'INFO'|'OFF',
            'ThrottlingBurstLimit': int,
            'ThrottlingRateLimit': int
        }
        - deployment_id: 'string'
        - description: 'string'
        - route_settings: {
            'string': {
                'DataTraceEnabled': True|False,
                'DetailedMetricsEnabled': True|False,
                'LoggingLevel': 'ERROR'|'INFO'|'OFF',
                'ThrottlingBurstLimit': int,
                'ThrottlingRateLimit': int
            }
          }
        - stage_variables: {'string': 'string'}
        - tags: {'string': 'string'}

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_stage:
          aws.apigatewayv2.stage.present:
            - name: value
            - api_id: value
            - access_log_settings: {}
            - auto_deploy: True|False
            - client_certificate_id: value
            - default_route_settings: {}
            - deployment_id: value
            - description: value
            - route_settings: {}
            - stage_variables: {}
            - tags: {}
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed API Gateway v2 stage resource as a data-source.

Args:
    name(string): An Idem name of the resource.
    api_id(string): The API resource identifier in Amazon Web Services.
    resource_id(string): The Stage resource name in Amazon Web Services.

Request syntax:
    [idem_test_aws_apigatewayv2_stage]:
      aws.apigatewayv2.stage.search:
        - api_id: 'string'
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_stage:
          aws.apigatewayv2.stage.search:
            - api_id: value
            - resource_id: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigatewayv2.stage](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigatewayv2/stage.html).
