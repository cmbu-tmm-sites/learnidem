---
title: "aws.apigateway.resource"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified resource.

Args:
    name(string): The Idem name of the resource.
    rest_api_id(string): AWS rest_api id of the associated RestApi.
    resource_id(string, optional): AWS Resource id. Defaults to None.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.apigateway.resource.absent:
            - name: value
            - resource_id: value
            - rest_api_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the API Gateway Resources associated with a specific Rest API.

Returns a list of apigateway.resource descriptions

Returns:
    Dict[str, Any]


Examples:

    .. code-block:: bash

        $ idem describe aws.apigateway.resource
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a new resource or modifies an existing one.

Args:
    name(string): An idem name of the resource.
    rest_api_id(string): AWS rest_api id of the associated RestApi.
    parent_id(string): The parent resource's id.
    path_part(string): The last path segment for this resource.
    resource_id(string, optional): AWS Resource id. Defaults to None.

Request Syntax:
    [idem_test_aws_apigateway_resource]:
      aws.apigateway.resource.present:
        - name: 'string'
        - rest_api_id: 'string'
        - parent_id: 'string'
        - path_part: 'string'

Returns:
    Dict[str, Any]
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigateway.resource](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigateway/resource.html).
