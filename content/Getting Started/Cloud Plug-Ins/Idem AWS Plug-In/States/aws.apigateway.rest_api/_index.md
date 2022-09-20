---
title: "aws.apigateway.rest_api"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified rest_api resource.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text): AWS rest_api id. Idem automatically considers this resource as absent if this field is not specified.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.apigateway.rest_api.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Returns a list of apigateway.rest_api descriptions

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.apigateway.rest_api
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates a new rest_api resource or modifies an existing one.

Args:
    name(Text): An idem name of the resource.
    resource_id(Text, optional): AWS rest_api id. Defaults to None.
    description (Text, optional): The description of the RestApi .
    version (Text, optional): A version identifier for the API.
    binary_media_types (List[str], optional):  The list of binary media types supported by the RestApi . By default, the RestApi supports only UTF-8-encoded text payloads.
    minimum_compression_size (integer, optional):  A nullable integer that is used to enable compression (with non-negative between 0 and 10485760 (10M) bytes, inclusive) or disable compression (with a null value) on an API. When compression is enabled, compression or decompression is not applied on the payload if the payload size is smaller than this value. Setting it to zero allows compression for any payload size.
    api_key_source (Text, optional):  The source of the API key for metering requests according to a usage plan.
    endpoint_configuration(Dict[str, Any], optional): The endpoint configuration of this RestApi showing the endpoint types of the API. Defaults to None.
        * types (List[str], optional): A list of endpoint types of an API (RestApi) or its custom domain name (DomainName). For an
            edge-optimized API and its custom domain name, the endpoint type is "EDGE". For a regional API
            and its custom domain name, the endpoint type is REGIONAL. For a private API, the endpoint type
            is PRIVATE.
        * vpcEndpointIds (List[str], optional): A list of VpcEndpointIds of an API (RestApi) against which to create Route53 ALIASes. It is only
            supported for PRIVATE endpoint type.
    policy (Text, optional):  A stringified JSON policy document that applies to this RestApi regardless of the caller and Method configuration.
    tags(Dict, optional): The key-value map of strings. The valid character set is [a-zA-Z+-=._:/]. The tag key can be up
        to 128 characters and must not start with aws:. The tag value can be up to 256 characters. Defaults to None.
    disable_execute_api_endpoint (boolean, optional):  Specifies whether clients can invoke your API by using the default execute-api endpoint. By default, clients can invoke your API with the default https://{api_id}.execute-api.{region}.amazonaws.com endpoint. To require that clients use a custom domain name to invoke your API, disable the default endpoint.

Request Syntax:
    [idem_test_aws_apigateway_rest_api]:
      aws.apigateway.rest_api.present:
        - name: 'string'
        - resource_id: 'string'
        - api_key_source: 'string'
        - binary_media_types:
          - 'string'
        - endpoint_configuration:
            types:
            - REGIONAL | EDGE | PRIVATE
            vpcEndpointIds:
            - 'string'
        - tags:
            'string': 'string'
        - disable_execute_api_endpoint: True | False
        - minimum_compression_size: int(0 to 10485760)
        - policy: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_present:
          aws.apigateway.rest_api.present:
            -name: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigateway.rest_api](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigateway/rest_api.html).