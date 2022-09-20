---
title: "aws.apigatewayv2.authorizer"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway v2 authorizer resource.

Args:
    name(string): An Idem name of the resource.
    api_id(string): The API resource identifier in Amazon Web Services.
    resource_id(string, optional): The Authorizer resource identifier in Amazon Web Services.
        Idem automatically considers this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_authorizer:
          aws.apigatewayv2.authorizer.absent:
            - name: value
            - api_id: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the API Gateway v2 authorized resources for an AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.apigatewayv2.authorizer
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an API Gateway v2 authorized resource.

Args:
    name(string): An Idem name of the resource. This is also used as the name of the Authorizer during resource creation.
    api_id(string): The API resource identifier in Amazon Web Services.
    authorizer_type(string): The authorizer type. Specify REQUEST for a Lambda function using incoming request parameters.
        Specify JWT to use JSON Web Tokens (supported only for HTTP APIs).
    resource_id(string, optional): The authorizer resource identifier in Amazon Web Services.
    authorizer_credentials_arn(str, optional): Specifies the required credentials as an IAM role for API Gateway to invoke the authorizer. To
        specify an IAM role for API Gateway to assume, use the role's Amazon Resource Name (ARN). To use
        resource-based permissions on the Lambda function, don't specify this parameter. Supported only
        for REQUEST authorizers.
    authorizer_payload_format_version(str, optional): Specifies the format of the payload sent to an HTTP API Lambda authorizer. Required for HTTP API
        Lambda authorizers. Supported values are 1.0 and 2.0. To learn more, see Working with AWS Lambda
        authorizers for HTTP APIs.
    authorizer_result_ttl_in_seconds(int, optional): The time to live (TTL) for cached authorizer results, in seconds. If it equals 0, authorization
        caching is disabled. If it is greater than 0, API Gateway caches authorizer responses. The
        maximum value is 3600, or 1 hour. Supported only for HTTP API Lambda authorizers.
    authorizer_type(str): The authorizer type. Specify REQUEST for a Lambda function using incoming request parameters.
        Specify JWT to use JSON Web Tokens (supported only for HTTP APIs).
    authorizer_uri(str, optional): The authorizer's Uniform Resource Identifier (URI). For REQUEST authorizers, this must be a
        well-formed Lambda function URI, for example, arn:aws:apigateway:us-
        west-2:lambda:path/2015-03-31/functions/arn:aws:lambda:us-
        west-2:{account_id}:function:{lambda_function_name}/invocations. In general, the URI has this
        form: arn:aws:apigateway:{region}:lambda:path/{service_api}                , where {region} is
        the same as the region hosting the Lambda function, path indicates that the remaining substring
        in the URI should be treated as the path to the resource, including the initial /. For Lambda
        functions, this is usually of the form /2015-03-31/functions/[FunctionARN]/invocations.
        Supported only for REQUEST authorizers.
    enable_simple_responses(bool, optional): Specifies whether a Lambda authorizer returns a response in a simple format. By default, a
        Lambda authorizer must return an IAM policy. If enabled, the Lambda authorizer can return a
        boolean value instead of an IAM policy. Supported only for HTTP APIs. To learn more, see Working
        with AWS Lambda authorizers for HTTP APIs.
    identity_source(List): The identity source for which authorization is requested. For a REQUEST authorizer, this is
        optional. The value is a set of one or more mapping expressions of the specified request
        parameters. The identity source can be headers, query string parameters, stage variables, and
        context parameters. For example, if an Auth header and a Name query string parameter are defined
        as identity sources, this value is route.request.header.Auth, route.request.querystring.Name for
        WebSocket APIs. For HTTP APIs, use selection expressions prefixed with $, for example,
        $request.header.Auth, $request.querystring.Name. These parameters are used to perform runtime
        validation for Lambda-based authorizers by verifying all of the identity-related request
        parameters are present in the request, not null, and non-empty. Only when this is true does the
        authorizer invoke the authorizer Lambda function. Otherwise, it returns a 401 Unauthorized
        response without calling the Lambda function. For HTTP APIs, identity sources are also used as
        the cache key when caching is enabled. To learn more, see Working with AWS Lambda authorizers
        for HTTP APIs. For JWT, a single entry that specifies where to extract the JSON Web Token (JWT)
        from inbound requests. Currently only header-based and query parameter-based selections are
        supported, for example $request.header.Authorization.
    jwt_configuration(Dict[str, Any], optional): Represents the configuration of a JWT authorizer. Required for the JWT authorizer type.
        Supported only for HTTP APIs. Defaults to None.
        * Audience (List[str], optional): A list of the intended recipients of the JWT. A valid JWT must provide an aud that matches at
            least one entry in this list. See RFC 7519. Supported only for HTTP APIs.
        * Issuer (str, optional): The base domain of the identity provider that issues JSON Web Tokens. For example, an Amazon
            Cognito user pool has the following format: https://cognito-idp.{region}.amazonaws.com/{userPoolId}.
            Required for the JWT authorizer type. Supported only for HTTP APIs.

Request Syntax:
    [idem_test_aws_apigatewayv2_authorizer]:
      aws.apigatewayv2.authorizer.present:
        - name: 'string'
        - api_id: 'string'
        - authorizer_type: 'REQUEST'|'JWT'
        - identity_source: ['string']
        - authorizer_credentials_arn: 'string'
        - authorizer_payload_format_version: 'string'
        - authorizer_result_ttl_in_seconds: 123
        - authorizer_uri: 'string'
        - enable_simple_responses: True|False
        - jwt_configuration: {
            'Audience': ['string'],
            'Issuer': 'string'
          }

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_authorizer:
          aws.apigatewayv2.authorizer.present:
            - name: value
            - api_id: value
            - authorizer_type: value
            - identity_source: [value]
            - authorizer_credentials_arn: value
            - authorizer_payload_format_version: value
            - authorizer_result_ttl_in_seconds: value
            - authorizer_uri: value
            - enable_simple_responses: True|False
            - jwt_configuration: {
                'Audience': [value],
                'Issuer': value
              }
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed API Gateway v2 authorizer resource as a data-source.

Args:
    name(string): An Idem name of the resource.
    api_id(string): The API resource identifier in Amazon Web Services.
    resource_id(string): The Authorizer resource identifier in Amazon Web Services.

Request syntax:
    [idem_test_aws_apigatewayv2_authorizer]:
      aws.apigatewayv2.authorizer.search:
        - api_id: 'string'
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_authorizer:
          aws.apigatewayv2.authorizer.search:
            - api_id: value
            - resource_id: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigatewayv2.authorizer](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigatewayv2/authorizer.html).
