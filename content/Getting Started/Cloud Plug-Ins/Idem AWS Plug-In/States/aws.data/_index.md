---
title: "aws.data"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "lookup" >}}

```
A state to look up a resource that is not managed.
It's data will be available to other states via the arg_bind requisite interface.

:param hub:
:param ctx:
:param name: The name of the state
:param service: The name of the service under the boto3 client to use
:param resource: The name of the collection under the service to search
:param filter: A JMESPath

.. code-block:: sls

    my_unmanaged_resource:
        aws.data.lookup:
            service: ec2
            resource: vpc
            filter: *[]
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.data](https://docs.idemproject.io/idem-aws/en/latest/ref/states/data.html).
