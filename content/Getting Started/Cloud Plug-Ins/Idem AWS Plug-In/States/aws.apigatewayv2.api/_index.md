---
title: "aws.apigatewayv2.api"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway v2 api resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): The API resource identifier in Amazon Web Services.
        Idem automatically considers this resource being absent if this field is not specified.

Request syntax:
    [idem_test_aws_apigatewayv2_api]:
      aws.apigatewayv2.api.absent:
        - name: 'string'
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_api:
          aws.apigatewayv2.api.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the API Gateway v2 api resources for an AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.apigatewayv2.api
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an API Gateway v2 api resource.

Args:
    name(string): An Idem name of the resource. This is also used as the name of the API during resource creation.
    protocol_type(string): The API protocol.
    resource_id(string, optional): The API resource identifier in Amazon Web Services.
    api_key_selection_expression(string, optional): An API key selection expression. Supported only for WebSocket APIs.
    cors_configuration(Dict[str, Any], optional): A CORS configuration. Supported only for HTTP APIs. See Configuring CORS for more information. Defaults to None.
        * AllowCredentials (bool, optional): Specifies whether credentials are included in the CORS request. Supported only for HTTP APIs.
        * AllowHeaders (List[str], optional): Represents a collection of allowed headers. Supported only for HTTP APIs.
        * AllowMethods (List[str], optional): Represents a collection of allowed HTTP methods. Supported only for HTTP APIs.
        * AllowOrigins (List[str], optional): Represents a collection of allowed origins. Supported only for HTTP APIs.
        * ExposeHeaders (List[str], optional): Represents a collection of exposed headers. Supported only for HTTP APIs.
        * MaxAge (int, optional): The number of seconds that the browser should cache preflight request results. Supported only
            for HTTP APIs.
    credentials_arn(string, optional): This property is part of quick create. It specifies the credentials required for the integration, if any.
        For a Lambda integration, three options are available. To specify an IAM Role for API Gateway to assume, use the role's Amazon Resource Name (ARN).
        To require that the caller's identity be passed through from the request, specify arn:aws:iam:::user/.
        To use resource-based permissions on supported AWS services, specify null.
        Currently, this property is not used for HTTP integrations. Supported only for HTTP APIs.
    description(string, optional): The description of the API.
    disable_execute_api_endpoint(bool, optional): Specifies whether clients can invoke your API by using the default execute-api endpoint.
        By default, clients can invoke your API with the default https://{api_id}.execute-api.{region}.amazonaws.com endpoint.
        To require that clients use a custom domain name to invoke your API, disable the default endpoint.
    disable_schema_validation(bool, optional): Avoid validating models when creating a deployment. Supported only for WebSocket APIs.
    route_key(string, optional): This property is part of quick create. If you don't specify a routeKey, a default route of $default is created.
        The $default route acts as a catch-all for any request made to your API, for a particular stage.
        The $default route key can't be modified. You can add routes after creating the API, and you can update the route keys of additional routes.
        Supported only for HTTP APIs.
    route_selection_expression(string, optional): The route selection expression for the API. For HTTP APIs, the routeSelectionExpression must
        be ${request.method} ${request.path}. If not provided, this will be the default for HTTP APIs. This property is required for WebSocket APIs.
    tags(Dict, optional): The collection of tags. Each tag element is associated with a given resource.
    target(string, optional): This property is part of quick create. Quick create produces an API with an integration, a default catch-all route,
        and a default stage which is configured to automatically deploy changes. For HTTP integrations, specify a fully qualified URL.
        For Lambda integrations, specify a function ARN. The type of the integration will be HTTP_PROXY or AWS_PROXY, respectively.
        Supported only for HTTP APIs.
    version(string, optional): A version identifier for the API.

Request Syntax:
    [idem_test_aws_apigatewayv2_api]:
      aws.apigatewayv2.api.present:
        - name: 'string'
        - protocol_type: 'WEBSOCKET'|'HTTP'
        - api_key_selection_expression: 'string'
        - cors_configuration: Dict
        - credentials_arn: 'string'
        - description: 'string'
        - disable_execute_api_endpoint: True|False
        - disable_schema_validation: True|False
        - route_key: 'string'
        - route_selection_expression: 'string'
        - tags:
          - 'string': 'string'
        - target: 'string'
        - version: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_api:
          aws.apigatewayv2.api.present:
            - name: value
            - protocol_type: value
            - api_key_selection_expression: value
            - cors_configuration: { "AllowCredentials": True }
            - credentials_arn: value
            - description: value
            - disable_execute_api_endpoint: True
            - disable_schema_validation: True
            - route_key: value
            - route_selection_expression: value
            - tags: { "key": "value" }
            - target: value
            - version: value
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed API Gateway v2 api resource as a data-source.

Args:
    name(string): An Idem name of the resource.
    resource_id(string): The API resource identifier in Amazon Web Services.

Request syntax:
    [idem_test_aws_apigatewayv2_api]:
      aws.apigatewayv2.api.search:
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_api:
          aws.apigatewayv2.api.search:
            - resource_id: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigatewayv2.api](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigatewayv2/api.html).
