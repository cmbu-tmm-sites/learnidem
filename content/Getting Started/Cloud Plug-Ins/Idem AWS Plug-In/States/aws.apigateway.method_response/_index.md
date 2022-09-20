---
title: "aws.apigateway.method_response"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway Method Response.

Args:
    hub:

    ctx:

    name(string):
        An Idem name of the resource.

    resource_id(string, optional):
        Idem Resource id, formatted as: rest_api_id-parent_resource_id-http_method-status_code. Defaults to None.
            Idem automatically considers this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

    idem_test_aws_apigateway_method_response:
      aws.apigateway.method_response.absent:
        - name: value
        - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the API Gateway Method Responses associated with a specific Method.

Returns a list of apigateway.method_response descriptions

Returns:
    Dict[str, Any]


Examples:

    .. code-block:: bash

        $ idem describe aws.apigateway.method_response
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a new API Gateway Method Response or modifies an existing one.

Args:
    name(string):
        An idem name of the resource.

    rest_api_id(string):
        AWS rest_api id of the associated RestApi.

    parent_resource_id(string):
        The parent resource's id.

    http_method(string):
        String that specifies the method request's HTTP method type.

    status_code(string):
        The method response's status code.

    resource_id(string, optional):
        Defaults to None. Idem Resource id, formatted as: rest_api_id-parent_resource_id-http_method-status_code.

    response_models(dict, optional):
        Specifies the Model resources used for the response's content-type.
            Response models are represented as a key/value map, with a content-type as the key and a Model name
            as the value.

    response_parameters(dict, optional):
        A key-value map specifying required or optional response parameters
            that API Gateway can send back to the caller. A key defines a method response header and the value
            specifies whether the associated method response header is required or not. The expression of the key
            must match the pattern method.response.header.{name} , where name is a valid and unique header name.
            API Gateway passes certain integration response data to the method response headers specified here
            according to the mapping you prescribe in the API's IntegrationResponse. The integration response data
            that can be mapped include an integration response header expressed in integration.response.header.{name},
            a static value enclosed within a pair of single quotes (e.g., 'application/json' ), or a JSON expression
            from the back-end response payload in the form of integration.response.body.{JSON-expression},
            where JSON-expression is a valid JSON expression without the $ prefix.)

Request Syntax:
    [idem_test_aws_apigateway_method_response]:
      aws.apigateway.method_response.present:
        - name: 'string'
        - rest_api_id: 'string'
        - parent_resource_id: 'string'
        - http_method: 'string'
        - status_code: 'string'

Returns:
    Dict[str, Any]
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigateway.method_response](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigateway/method_response.html).
