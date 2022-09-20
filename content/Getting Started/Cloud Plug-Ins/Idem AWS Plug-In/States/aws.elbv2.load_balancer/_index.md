---
title: "aws.elbv2.load_balancer"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
1. Deletes the specified Application Load Balancer, Network Load Balancer, or Gateway Load Balancer. Deleting a
   load balancer also deletes its listeners.
2. You can't delete a load balancer if deletion protection is enabled. If the load balancer does not exist or has
   already been deleted, the call succeeds.
3. Deleting a load balancer does not affect its registered targets. For example, your EC2 instances continue to run
   and are still registered to their target groups. If you no longer need these EC2 instances, you can stop or
   terminate them.

Args:
    name(Text): Idem name of the load balancer.
    resource_id(Text, optional): The Amazon Resource Name (ARN) of the load balancer.

Request Syntax:
    [load_balancer-name]:
      aws.elbv2.load_balancer.absent:
      - name: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        test_load-balancer_name:
            aws.elbv2.load_balancer.absent:
              - name: my-load-balancer
              - resource_id: arn:aws:elasticloadbalancing:us-west-2:123456789012:loadbalancer/app/my-load-balancer/50dc6c495c0c9188
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function
Lists out all load balancers.

Returns:
    Dict[str, Any]

Examples:

.. code-block:: bash

    $ idem describe aws.elbv2.load_balancer
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an Application Load Balancer, Network Load Balancer, or Gateway Load Balancer.

This operation is idempotent, which means that it completes at most one time. If you attempt to create multiple
load balancers with the same settings, each call succeeds.

Args:
    name(Text): An Idem name to identify load balancer. This name must be unique per region per account, can have a
        maximum of 32 characters, must contain only alphanumeric characters or hyphens, must not begin or end with
        a hyphen, and must not begin with "internal-"
    subnets(List, Optional): The IDs of the public subnets. You can specify only one subnet per Availability Zone.
        You must specify either subnets or subnet mappings, but not both. To specify an Elastic IP address, specify
        subnet mappings instead of subnets.

        [Application Load Balancers] You must specify subnets from at least two Availability Zones.
        [Application Load Balancers on Outposts] You must specify one Outpost subnet.
        [Application Load Balancers on Local Zones] You can specify subnets from one or more Local Zones.
        [Network Load Balancers] You can specify subnets from one or more Availability Zones.
        [Gateway Load Balancers] You can specify subnets from one or more Availability Zones.
    subnet_mappings([List[Dict[str, Any]]): The IDs of the public subnets. You can specify only one subnet per
        Availability Zone. You must specify either subnets or subnet mappings, but not both.

        [Application Load Balancers] You must specify subnets from at least two Availability Zones. You cannot
            specify Elastic IP addresses for your subnets.
        [Application Load Balancers on Outposts] You must specify one Outpost subnet.
        [Application Load Balancers on Local Zones] You can specify subnets from one or more Local Zones.
        [Network Load Balancers] You can specify subnets from one or more Availability Zones. You can specify one
            Elastic IP address per subnet if you need static IP addresses for your internet-facing load balancer.
            For internal load balancers, you can specify one private IP address per subnet from the IPv4 range of
            the subnet. For internet-facing load balancer, you can specify one IPv6 address per subnet.
        [Gateway Load Balancers] You can specify subnets from one or more Availability Zones. You cannot specify
            Elastic IP addresses for your subnets.

            * SubnetId (Text, Optional): The ID of the subnet.
            * AllocationId (Text, Optional): [Network Load Balancers] The allocation ID of the Elastic IP address
                for an internet-facing load balancer.
            * PrivateIPv4Address (Text, Optional): [Network Load Balancers] The private IPv4 address for an internal
                load balancer.
            * IPv6Address (Text, Optional): [Network Load Balancers] The IPv6 address.
    security_groups(List): [Application Load Balancers] The IDs of the security groups for the load balancer.
    scheme(Text, Optional): The nodes of an Internet-facing load balancer have public IP addresses. The DNS name of
        an Internet-facing load balancer is publicly resolvable to the public IP addresses of the nodes. Therefore,
        Internet-facing load balancers can route requests from clients over the internet.

        The nodes of an internal load balancer have only private IP addresses. The DNS name of an internal load
        balancer is publicly resolvable to the private IP addresses of the nodes. Therefore, internal load balancers
         can route requests only from clients with access to the VPC for the load balancer.

        The default is an Internet-facing load balancer. You cannot specify a scheme for a Gateway Load Balancer.
    tags([Dict[str, str], optional): The tags to assign to the load balancer. Defaults to None.
        * Key (Text): The key of the tag.
        * Value (Text, optional): The value of the tag.
    lb_type(Text, Optional): The type of load balancer. The default is application.
    ip_address_type(Text, Optional): The type of IP addresses used by the subnets for your load balancer. The
        possible values are ipv4 (for IPv4 addresses) and dualstack (for IPv4 and IPv6 addresses).
    customer_owned_ipv4_pool(Text, Optional): [Application Load Balancers on Outposts] The ID of the customer-owned
        address pool (CoIP pool).
    attributes: The load balancer attributes.
        (Dict): Information about a tag.
            Key (Text): The name of the attribute.

        Attributes supported by all load balancers.
            1. 'deletion_protection.enabled' - Indicates whether deletion protection is enabled. The value is true
                or false. The default is false.

        The following attributes are supported by both Application Load Balancers and Network Load Balancers:
            1. 'access_logs.s3.enabled' - Indicates whether access logs are enabled. The value is true or false.
               The default is false .
            2. 'access_logs.s3.bucket' - The name of the S3 bucket for the access logs. This attribute is required
               if access logs are enabled. The bucket must exist in the same region as the load balancer and have a
               bucket policy that grants Elastic Load Balancing permissions to write to the bucket.
            3. 'access_logs.s3.prefix' - The prefix for the location in the S3 bucket for the access logs.
            4. 'ipv6.deny_all_igw_traffic' - Blocks internet gateway (IGW) access to the load balancer. It is set
               to false for internet-facing load balancers and true for internal load balancers, preventing
               unintended access to your internal load balancer through an internet gateway.

        The following attributes are supported by only Application Load Balancers:
            1. 'idle_timeout.timeout_seconds' - The idle timeout value, in seconds. The valid range is 1-4000
               seconds. The default is 60 seconds.
            2. 'routing.http.desync_mitigation_mode' - Determines how the load balancer handles requests that might
               pose a security risk to your application. The possible values are monitor, defensive, and strictest.
               The default is defensive .
            3. 'routing.http.drop_invalid_header_fields.enabled' - Indicates whether HTTP headers with invalid
               header fields are removed by load balancer(true) or routed to target(s) (false). Default is false.
            4. 'routing.http.preserve_host_header.enabled' - Indicates whether the Application Load Balancer should
               preserve the Host header in the HTTP request and send it to the target without any change. The
               possible values are true and false. The default is false.
            5. 'routing.http.x_amzn_tls_version_and_cipher_suite.enabled' - Indicates whether the two headers
               (x-amzn-tls-version and x-amzn-tls-cipher-suite ), which contain information about the negotiated TLS
               version and cipher suite, are added to the client request before sending it to the target. The
               x-amzn-tls-version header has information about the TLS protocol version negotiated with the client,
               and the x-amzn-tls-cipher-suite header has information about the cipher suite negotiated with the
               client. Both headers are in OpenSSL format. The possible values for the attribute are true and false.
               The default is false.
            6. 'routing.http.xff_client_port.enabled' - Indicates whether the X-Forwarded-For header should preserve
               the source port that the client used to connect to the load balancer. The possible values are true
               and false . The default is false .
            7. 'routing.http.xff_header_processing.mode' - Enables you to modify, preserve, or remove the
               X-Forwarded-For header in the HTTP request before the Application Load Balancer sends the request to
               the target. The possible values: append, preserve, and remove. The default is 'append'.

               If the value is 'append', the Application Load Balancer adds the client IP address (of the last hop)
                  to the X-Forwarded-For header in the HTTP request before it sends it to targets.
               If the value is 'preserve' the Application Load Balancer preserves the X-Forwarded-For header in the
                  HTTP request, and sends it to targets without any change.
               If the value is 'remove', Application Load Balancer removes the X-Forwarded-For header in the HTTP
                  request before it sends it to targets.
            8. 'routing.http2.enabled' - Indicates whether HTTP/2 is enabled. The possible values are true & false.
               The default is true . Elastic Load Balancing requires that message header names contain only
               alphanumeric characters and hyphens.
            9. 'waf.fail_open.enabled' - Indicates whether to allow a WAF-enabled load balancer to route requests to
               target(s) if it is unable to forward the request to Amazon Web Services WAF. The possible values are
               true and false . The default is false .

        The following attribute is supported by Network Load Balancers and Gateway Load Balancers:
            1. 'load_balancing.cross_zone.enabled' - Indicates whether cross-zone load balancing is enabled. The
               possible values are true and false . The default is false .
        Value (Text): The value of the attribute.
    resource_id:(Text, optional): The Amazon Resource Name (ARN) of the load balancer.

Request Syntax:
    [load_balancer-name]:
      aws.elbv2.load_balancer.present:
      - name: 'string'
      - subnets: 'list'
      - subnet_mappings: 'list'
      - security_groups: 'list'
      - scheme: 'string'
      - lb_type: 'string',
      - ip_address_type: 'string',
      - customer_owned_ipv4_pool: 'string',
      - attributes: 'list'
      - tags:
          'string': 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

. code-block:: sls

    test_load-balancer_name:
      aws.elbv2.load_balancer.present:
        - name: my-load-balancer
        - resource_id: arn:aws:elasticloadbalancing:us-west-2:123456789012:loadbalancer/app/my-load-balancer/50dc6c495c0c9188
        - tags:
            name: load-balancer-name
        - availability_zones
          - us-west-2a
        - subnets
          - subnet-15aaab61
        - security_groups
          - sg-a61988c3
        - scheme: internal
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.elbv2.load_balancer](https://docs.idemproject.io/idem-aws/en/latest/ref/states/elbv2/load_balancer.html).
