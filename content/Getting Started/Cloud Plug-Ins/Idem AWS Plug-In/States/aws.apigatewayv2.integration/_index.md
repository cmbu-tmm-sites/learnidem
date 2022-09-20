---
title: "aws.apigatewayv2.integration"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway v2 integration resource.

Args:
    name(string): An Idem name of the resource.
    api_id(string): The API resource identifier in Amazon Web Services.
    resource_id(string, optional): The Integration resource identifier in Amazon Web Services.
        Idem automatically considers this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_integration:
          aws.apigatewayv2.integration.absent:
            - name: value
            - api_id: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the API Gateway v2 integration resources for an AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.apigatewayv2.integration
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an API Gateway v2 integration resource.

Args:
    name(string): An Idem name of the resource.
    api_id(string): The API resource identifier in Amazon Web Services.
    integration_type(string): The integration type of an integration. One of the following: AWS: for integrating the route or
        method request with an AWS service action, including the Lambda function-invoking action. With
        the Lambda function-invoking action, this is referred to as the Lambda custom integration. With
        any other AWS service action, this is known as AWS integration. Supported only for WebSocket
        APIs. AWS_PROXY: for integrating the route or method request with a Lambda function or other AWS
        service action. This integration is also referred to as a Lambda proxy integration. HTTP: for
        integrating the route or method request with an HTTP endpoint. This integration is also referred
        to as the HTTP custom integration. Supported only for WebSocket APIs. HTTP_PROXY: for
        integrating the route or method request with an HTTP endpoint, with the client request passed
        through as-is. This is also referred to as HTTP proxy integration. For HTTP API private
        integrations, use an HTTP_PROXY integration. MOCK: for integrating the route or method request
        with API Gateway as a "loopback" endpoint without invoking any backend. Supported only for
        WebSocket APIs.
    resource_id(string, optional): The integration resource identifier in Amazon Web Services.
    connection_id(string, optional): The ID of the VPC link for a private integration. Supported only for HTTP APIs. Defaults to None.
    connection_type(string, optional): The type of the network connection to the integration endpoint. Specify INTERNET for connections
        through the public routable internet or VPC_LINK for private connections between API Gateway and
        resources in a VPC. The default value is INTERNET.
    content_handling_strategy(string, optional): Supported only for WebSocket APIs. Specifies how to handle response payload content type
        conversions. Supported values are CONVERT_TO_BINARY and CONVERT_TO_TEXT, with the following
        behaviors: CONVERT_TO_BINARY: Converts a response payload from a Base64-encoded string to the
        corresponding binary blob. CONVERT_TO_TEXT: Converts a response payload from a binary blob to a
        Base64-encoded string. If this property is not defined, the response payload will be passed
        through from the integration response to the route response or method response without
        modification.
    credentials_arn(string, optional): Specifies the credentials required for the integration, if any. For AWS integrations, three
        options are available. To specify an IAM Role for API Gateway to assume, use the role's Amazon
        Resource Name (ARN). To require that the caller's identity be passed through from the request,
        specify the string arn:aws:iam::*:user/*. To use resource-based permissions on supported AWS
        services, specify null.
    description(string, optional): The description of the integration.
    integration_method(string, optional): Specifies the integration's HTTP method type. Defaults to None.
    integration_subtype(string, optional): Supported only for HTTP API AWS_PROXY integrations. Specifies the AWS service action to invoke.
        To learn more, see Integration subtype reference.
    integration_uri(string, optional): For a Lambda integration, specify the URI of a Lambda function. For an HTTP integration, specify
        a fully-qualified URL. For an HTTP API private integration, specify the ARN of an Application
        Load Balancer listener, Network Load Balancer listener, or AWS Cloud Map service. If you specify
        the ARN of an AWS Cloud Map service, API Gateway uses DiscoverInstances to identify resources.
        You can use query parameters to target specific resources. To learn more, see DiscoverInstances.
        For private integrations, all resources must be owned by the same AWS account.
    passthrough_behavior(string, optional): Specifies the pass-through behavior for incoming requests based on the Content-Type header in
        the request, and the available mapping templates specified as the requestTemplates property on
        the Integration resource. There are three valid values: WHEN_NO_MATCH, WHEN_NO_TEMPLATES, and
        NEVER. Supported only for WebSocket APIs. WHEN_NO_MATCH passes the request body for unmapped
        content types through to the integration backend without transformation. NEVER rejects unmapped
        content types with an HTTP 415 Unsupported Media Type response. WHEN_NO_TEMPLATES allows pass-
        through when the integration has no content types mapped to templates. However, if there is at
        least one content type defined, unmapped content types will be rejected with the same HTTP 415
        Unsupported Media Type response.
    payload_format_version(string, optional): Specifies the format of the payload sent to an integration. Required for HTTP APIs. Defaults to None.
    request_parameters(Dict, optional): For WebSocket APIs, a key-value map specifying request parameters that are passed from the
        method request to the backend. The key is an integration request parameter name and the
        associated value is a method request parameter value or static value that must be enclosed
        within single quotes and pre-encoded as required by the backend. The method request parameter
        value must match the pattern of method.request.{location}.{name}, where
        {location} is querystring, path, or header; and {name}
        must be a valid and unique method request parameter name. For HTTP API integrations with a
        specified integrationSubtype, request parameters are a key-value map specifying parameters that
        are passed to AWS_PROXY integrations. You can provide static values, or map request data, stage
        variables, or context variables that are evaluated at runtime. To learn more, see Working with
        AWS service integrations for HTTP APIs. For HTTP API integrations without a specified
        integrationSubtype request parameters are a key-value map specifying how to transform HTTP
        requests before sending them to the backend. The key should follow the pattern
        <action>:<header|querystring|path>.<location> where action can be append, overwrite or remove.
        For values, you can provide static values, or map request data, stage variables, or context
        variables that are evaluated at runtime. To learn more, see Transforming API requests and
        responses.
    request_templates(Dict, optional): Represents a map of Velocity templates that are applied on the request payload based on the
        value of the Content-Type header sent by the client. The content type value is the key in this
        map, and the template (as a String) is the value. Supported only for WebSocket APIs.
    response_parameters(Dict, optional): Supported only for HTTP APIs. You use response parameters to transform the HTTP response from a
        backend integration before returning the response to clients. Specify a key-value map from a
        selection key to response parameters. The selection key must be a valid HTTP status code within
        the range of 200-599. Response parameters are a key-value map. The key must match pattern
        <action>:<header>.<location> or overwrite.statuscode. The action can be append, overwrite or
        remove. The value can be a static value, or map to response data, stage variables, or context
        variables that are evaluated at runtime. To learn more, see Transforming API requests and
        responses.
    template_selection_expression(string, optional): The template selection expression for the integration.
    timeout_in_millis(int, optional): Custom timeout between 50 and 29,000 milliseconds for WebSocket APIs and between 50 and 30,000
        milliseconds for HTTP APIs. The default timeout is 29 seconds for WebSocket APIs and 30 seconds
        for HTTP APIs.
    tls_config(Dict[str, Any], optional): The TLS configuration for a private integration. If you specify a TLS configuration, private
        integration traffic uses the HTTPS protocol. Supported only for HTTP APIs. Defaults to None.
        * ServerNameToVerify (str, optional): If you specify a server name, API Gateway uses it to verify the hostname on the integration's
            certificate. The server name is also included in the TLS handshake to support Server Name
            Indication (SNI) or virtual hosting.

Request Syntax:
    [idem_test_aws_apigatewayv2_route]:
      aws.apigatewayv2.route.present:
        - name: 'string'
        - api_id: 'string'
        - integration_type: 'AWS'|'HTTP'|'MOCK'|'HTTP_PROXY'|'AWS_PROXY'
        - connection_id: 'string'
        - connection_type: 'INTERNET'|'VPC_LINK'
        - content_handling_strategy: 'AWS'|'HTTP'|'MOCK'|'HTTP_PROXY'|'AWS_PROXY'
        - credentials_arn: 'string'
        - description: 'string'
        - integration_method: 'string'
        - integration_subtype: 'string'
        - integration_uri: 'string'
        - passthrough_behavior: 'WHEN_NO_MATCH'|'NEVER'|'WHEN_NO_TEMPLATES'
        - payload_format_version: 'string'
        - request_parameters: {'string': 'string'}
        - request_templates: {'string': 'string'}
        - response_parameters: {string': {'string': 'string'}}
        - template_selection_expression: 'string'
        - timeout_in_millis: int
        - tls_config: {'ServerNameToVerify': 'string'}

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_route:
          aws.apigatewayv2.route.present:
            - name: value
            - api_id: value
            - integration_type: value
            - connection_id: value
            - connection_type: value
            - content_handling_strategy: value
            - credentials_arn: value
            - description: value
            - integration_method: value
            - integration_subtype: value
            - integration_uri: value
            - passthrough_behavior: value
            - payload_format_version: value
            - request_parameters: {}
            - request_templates: {}
            - response_parameters: {}
            - template_selection_expression: value
            - timeout_in_millis: value
            - tls_config: {}
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed API Gateway v2 integration resource as a data-source.

Args:
    name(string): An Idem name of the resource.
    api_id(string): The API resource identifier in Amazon Web Services.
    resource_id(string): The Integration resource identifier in Amazon Web Services.

Request syntax:
    [idem_test_aws_apigatewayv2_integration]:
      aws.apigatewayv2.integration.search:
        - api_id: 'string'
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_integration:
          aws.apigatewayv2.integration.search:
            - api_id: value
            - resource_id: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigatewayv2.integration](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigatewayv2/integration.html).
