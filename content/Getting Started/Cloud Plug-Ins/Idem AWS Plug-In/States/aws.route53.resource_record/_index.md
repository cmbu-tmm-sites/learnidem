---
title: "aws.route53.resource_record"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified resource record

Args:
    name(Text): Name of the resource record. Needed because of the Idem contract but not used
    resource_id(Text, optional): Composite ID for a resource record in a hosted zone. String formatted as
        <hosted_zone_id>_<record_name>_<record_type>

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        MX_record_is_absent:
          aws.route53.resource_record.absent:
            - name: www.example.com.
            - resource_id: HSHMRK8IGWBU3PU_www.example.com_MX
```
{{< /tab >}}

{{< tab "describe" >}}

```

```
{{< /tab >}}

{{< tab "present" >}}

```
Creates or changes a resource record set, which contains authoritative DNS information for a specified domain name
or subdomain name.

Args:
    name(Text): The name of the record. A '.' will be appended if not already present.
    hosted_zone_id(Text): The ID of the hosted zone that contains the resource record sets
    record_type(Text): The DNS record type. For information about different record types and how data is encoded for
        them, see `Supported DNS Resource Record Types https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html`__
        in the Amazon Route 53 Developer Guide.
    resource_records(List, optional): Information about the resource records to act upon.
    alias_target(Dict, optional): Alias resource record sets only: Information about the Amazon Web Services resource,
        such as a CloudFront distribution or an Amazon S3 bucket, that you want to route traffic to.
    resource_id(Text, optional): Composite ID for a resource record in a hosted zone. String formatted as
        <hosted_zone_id>_<record_name>_<record_type>
    ttl(int, optional): The resource record cache time to live (TTL), in seconds.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

    KL1PX9DBMUY9WHB_www.example.com_AAAA:
      aws.route53.resource_record.present:
      - hosted_zone_id: /hostedzone/KL1PX9DBMUY9WHB
        name: www.example.com.
        record_type: AAAA
        resource_records:
        - 2001:0db8:85a3:0:0:8a2e:0370:7335
        - 2001:0db8:85a3:0:0:8a2e:0370:7334
        ttl: 300

    ZY51FUS5VYB_www.example.net_A:
      aws.route53.resource_record.present:
      - alias_target:
          dns_name: lb1.us-east-1.elb.amazonaws.com.
          evaluate_target_health: false
          hosted_zone_id: Z35SXDOTRQ7X7Z
        hosted_zone_id: /hostedzone/ZY51FUS5VYB
        name: www.example.net.
        record_type: A
        resource_id: ZY51FUS5VYB_www.example.net_A
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.route53.resource_record](https://docs.idemproject.io/idem-aws/en/latest/ref/states/route53/resource_record.html).
