---
title: "aws.apigateway.method"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway Method resource

Args:
    name(string): An Idem name of the resource.
    parent_resource_id(string): AWS Parent Resource ID.
    rest_api_id(string): The string identifier of the associated RestApi.
    http_method(string): The HTTP verb of the Method resource.
    resource_id(string, optional): The resource identifier for the Method resource. Idem automatically considers
        this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigateway_method:
          aws.apigateway.method.absent:
            - name: value
            - parent_resource_id: value
            - rest_api_id: value
            - resource_id: value
            - http_method: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the API Gateway Methods associated with a specific Rest API.

Returns a list of apigateway.method descriptions

Returns:
    Dict[str, Any]


Examples:

    .. code-block:: bash

        $ idem describe aws.apigateway.method
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an API Gateway Method resource

Args:
    name(string): Idem name of the resource.
    rest_api_id(string): The string identifier of the associated Rest API.
    http_method(string): String that specifies the method request's HTTP method type.
    parent_resource_id(string): AWS Parent Resource ID.
    authorization_type(string, optional): The method's authorization type. Valid values are NONE for open access,
        AWS_IAM for using AWS IAM permissions, CUSTOM for using a custom authorizer, or
        COGNITO_USER_POOLS for using a Cognito user pool. Necessary for creation but not for updating.
    resource_id(string, optional): Idem Resource ID that is generated once the resource is created.
    api_key_required(bool, optional): A boolean flag specifying whether a valid ApiKey is required to invoke this method.

    Parameters not yet supported by Idem:
    authorization_scopes(list, optional): A list of authorization scopes configured on the method. The scopes are
        used with a COGNITO_USER_POOLS authorizer to authorize the method invocation. The authorization works by
        matching the method scopes against the scopes parsed from the access token in the incoming request.
        The method invocation is authorized if any method scopes matches a claimed scope in the access token.
        Otherwise, the invocation is not authorized. When the method scope is configured, the client must provide
        an access token instead of an identity token for authorization purposes.
    authorizer_id(string, optional): The identifier of an Authorizer to use on this method. The authorizationType must be CUSTOM .
    operation_name(string, optional): A human-friendly operation identifier for the method.
    request_parameters(dict, optional): A key-value map defining required or optional method request parameters that
        can be accepted by API Gateway. A key is a method request parameter name matching the pattern of
        method.request.{location}.{name} , where location is querystring , path , or header and name is a valid and
        unique parameter name. The value associated with the key is a Boolean flag indicating whether the parameter
        is required (true ) or optional (false ). The method request parameter names defined here are available in
        Integration to be mapped to integration request parameters or templates.
    request_models(dict, optional): A key-value map specifying data schemas, represented by Model resources,
        (as the mapped value) of the request payloads of given content types (as the mapping key).
    request_validator_id(string, optional): The identifier of a RequestValidator for request validation.



Request Syntax:
    [idem_test_aws_apigateway_method]:
      aws.apigateway.method.present:
        - name: 'string'
        - rest_api_id: 'string'
        - parent_resource_id: 'string'
        - http_method: 'string'
        - authorization_type: 'string'

Returns:
    Dict[str, Any]
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigateway.method](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigateway/method.html).
