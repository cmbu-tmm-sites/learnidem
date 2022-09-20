---
title: "aws.apigateway.integration"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway Integration.

Args:
    hub:

    ctx:

    name(string):
        An Idem name of the resource.

    resource_id(string, optional):
        Idem Resource id, formatted as: rest_api_id-parent_resource_id-http_method. Defaults to None.
            Idem automatically considers this resource being absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

    idem_test_aws_apigateway_integration:
      aws.apigateway.integration.absent:
        - name: value
        - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the API Gateway Integrations.

Returns a list of apigateway.integration descriptions

Returns:
    Dict[str, Any]


Examples:

    .. code-block:: bash

        $ idem describe aws.apigateway.integration
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a new API Gateway Integration or modifies an existing one.

Args:
    hub:

    ctx:

    name(string):
        An idem name of the resource.

    rest_api_id(string):
        AWS rest_api id of the associated RestApi.

    parent_resource_id(string):
        The parent resource's id.

    http_method(string):
        String that specifies the method request's HTTP method type.

    input_type(string):
        Specifies a put integration input's type.

    resource_id(string, optional):
        Idem Resource id, formatted as: rest_api_id-parent_resource_id-http_method. Defaults to None.

    cache_namespace(string, optional):
        Specifies a group of related cached parameters. By default, API Gateway uses
            the resource ID as the cacheNamespace . You can specify the same cacheNamespace across resources to return
            the same cached data for requests to different resources.

    cache_key_parameters(list, optional):
        A list of request parameters whose values API Gateway caches. To be valid
            values for cacheKeyParameters , these parameters must also be specified for Method requestParameters.

    timeout_in_millis(int, optional):
        Custom timeout between 50 and 29,000 milliseconds. The default value is 29,000 milliseconds or 29 seconds.

    passthrough_behavior:
        Custom timeout between 50 and 29,000 milliseconds. The default value is
            29,000 milliseconds or 29 seconds.

    connection_id(string, optional):
        The ID of the VpcLink used for the integration. Specify this value only if you specify VPC_LINK as the
            connection type.

Request Syntax:
    [idem_test_aws_apigateway_integration]:
      aws.apigateway.integration.present:
        - name: 'string'
        - rest_api_id: 'string'
        - parent_resource_id: 'string'
        - http_method: 'string'
        - input_type: 'string'

Returns:
    Dict[str, Any]
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigateway.integration](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigateway/integration.html).
