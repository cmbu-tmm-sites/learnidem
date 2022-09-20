---
title: "aws.elbv2.target_group"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
1. Deletes the specified target group.
2. You can delete a target group if it is not referenced by any actions. Deleting a target group also deletes any
   associated health checks. Deleting a target group does not affect its registered targets. For example, any EC2
   instances continue to run until you stop or terminate them.

Args:
    name(Text): Idem name of the load balancer.
    resource_id(Text, optional): The Amazon Resource Name (ARN) of ElasticLoadBalancingv2 Target Group.

Request Syntax:
    [target_group-name]:
      aws.elbv2.target_group.absent:
      - name: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

    Examples:

    .. code-block:: sls

        test_load-balancer_name:
            aws.elbv2.target_group.absent:
              - name: my-load-balancer
              - resource_id: arn:aws:elasticloadbalancing:us-west-2:123456789012:targetgroup/my-targets/73e2d6bc24d8a067
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describes the resource in a way that can be recreated/managed with the corresponding "present" function
By default, all target groups are described.

Returns:
    Dict[str, Any]

Examples:

.. code-block:: bash

    $ idem describe aws.elbv2.target_group
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a target group. This operation is idempotent, which means that it completes at most one time. If you
attempt to create multiple target groups with the same settings, each call succeeds.

Args:
    hub:
    ctx:
    name(Text): An Idem name of the resource.
        This name must be unique per region per account, can have a maximum of 32 characters, must contain only
        alphanumeric characters or hyphens, and must not begin or end with a hyphen.
    protocol(Text, optional): The protocol to use for routing traffic to the targets.
        1. For Application Load Balancers, the supported protocols are HTTP and HTTPS.
        2. For Network Load Balancers, the supported protocols are TCP, TLS, UDP, or TCP_UDP.
        3. For Gateway Load Balancers, the supported protocol is GENEVE.
        4. A TCP_UDP listener must be associated with a TCP_UDP target group. If the target is a Lambda function,
           this parameter does not apply.
    protocol_version(Text, optional):  [HTTP/HTTPS protocol] The protocol version. Specify GRPC to send requests to
        targets using gRPC. Specify HTTP2 to send requests to targets using HTTP/2. The default is HTTP1 , which
        sends requests to targets using HTTP/1.1.
    port(Integer, optional): The port on which the targets receive traffic. This port is used unless you specify a
        port override when registering the target. If the target is a Lambda function, this parameter does not
        apply. If the protocol is GENEVE, the supported port is 6081.
    vpc_id(Text, optional): The identifier of the virtual private cloud (VPC). If the target is a Lambda function,
        this parameter does not apply. Otherwise, this parameter is required.
    health_check_protocol(Text, optional): The protocol the load balancer uses when performing health checks on
        targets. For Application Load Balancers, the default is HTTP. For Network Load Balancers and Gateway
        Load Balancers, the default is TCP. The TCP protocol is not supported for health checks if the protocol of
        the target group is HTTP/HTTPS. GENEVE, TLS, UDP, and TCP_UDP protocols are not supported for health checks.
    health_check_port(Text, optional): The port the load balancer uses when performing health checks on targets.
        If the protocol is HTTP, HTTPS, TCP, TLS, UDP, or TCP_UDP, the default is traffic-port , which is the port
        on which each target receives traffic from the load balancer. If the protocol is GENEVE, default is port 80.
    health_check_enabled(Boolean, optional): Indicates whether health checks are enabled. If the target type is
        lambda , health checks are disabled by default but can be enabled. If the target type is instance , ip ,
        or alb , health checks are always enabled and cannot be disabled.
    health_check_path(Text, optional): [HTTP/HTTPS health checks] The destination for health checks on the targets.
        [HTTP1 or HTTP2 protocol version] The ping path. The default is /.
        [GRPC protocol version] The path of a custom health check method with the format /package.service/method.
        The default is /Amazon Web Services.ALB/healthcheck.
    health_check_interval_seconds(Integer, optional): The approximate amount of time, in seconds, between health
        checks of an individual target. If the target group protocol is HTTP or HTTPS, the default is 30 seconds.
        If the target group protocol is TCP, TLS, UDP, or TCP_UDP, the supported values are 10 and 30 seconds and
        the default is 30 seconds. If the target group protocol is GENEVE, the default is 10 seconds. If the target
        type is lambda , the default is 35 seconds.
    health_check_timeout_seconds(Integer, optional): The amount of time, in seconds, during which no response from a
        target means a failed health check. For target groups with a protocol of HTTP/HTTPS/GENEVE, the default is
        5 seconds. For target groups with a protocol of TCP or TLS, this value must be 6 seconds for HTTP health
        checks and 10 seconds for TCP & HTTPS health checks. If the target type is lambda, default is 30 seconds.
    healthy_threshold_count(Integer, optional): The number of consecutive health checks successes required before
        considering an unhealthy target healthy. For target groups with a protocol of HTTP/HTTPS, the default is 5.
        For target groups with a protocol of TCP/TLS/GENEVE, default is 3. If the target type is lambda, default = 5.
    unhealthy_threshold_count(Integer, optional): The number of consecutive health check failures required before
        considering a target unhealthy. If the target group protocol is HTTP or HTTPS, the default is 2. If the
        target group protocol is TCP or TLS, this value must be the same as the healthy threshold count. If the
        target group protocol is GENEVE, the default is 3. If the target type is lambda , the default is 2.
    matcher(Dict[str, str]), optional): [HTTP/HTTPS health checks] The HTTP or gRPC codes to use when checking for a
        successful response from a target.
        ** HttpCode(Text) - For Application Load Balancers, you can specify values between 200 and 499, and the
            default value is 200. You can specify multiple values (for example, "200,202") or a range of values
            (for example, "200-299").
            For Network Load Balancers and Gateway Load Balancers, this must be "200–399".
            Note that when using shorthand syntax, some values such as commas need to be escaped.

        ** GrpcCode(Text) - You can specify values between 0 and 99. You can specify multiple values (for example,
            "0,1") or a range of values (for example, "0-5"). The default value is 12.
    target_type(Text, optional): The type of target that you must specify when registering targets with this
        target group. You can't specify targets for a target group using more than one target type.
        ** instance - Register targets by instance ID. This is the default value.
        ** ip - Register targets by IP address. You can specify IP addresses from the subnets of the virtual private
            cloud (VPC) for the target group, the RFC 1918 range (10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16),
            and the RFC 6598 range (100.64.0.0/10). You can't specify publicly routable IP addresses.
        ** lambda - Register a single Lambda function as a target.
        ** alb - Register a single Application Load Balancer as a target.
    tags([Dict[str, str]], optional): A list of tags to assign to the load balancer. For more information about
        tagging your load balancer, see Tag Your Classic Load Balancer in the Classic Load Balancers Guide.
        Defaults to None.
        * Key (Text): The key of the tag.
        * Value (Text, optional): The value of the tag.
    ip_address_type(Text, optional): The type of IP address used for this target group. The possible values are ipv4
        and ipv6 . This is an optional parameter. If not specified, the IP address type defaults to ipv4 .
    attributes(Dict[str, str], optional): The load balancer attributes.
        Key (Text): The name of the attribute.

        The following attribute is supported by all load balancers:
            1. 'deregistration_delay.timeout_seconds' - The amount of time, in seconds, for Elastic Load Balancing
                to wait before changing the state of a deregistering target from draining to unused . The range is
                0-3600 seconds. The default value is 300 seconds. If the target is a Lambda function, this
                attribute is not supported.

        The following attributes are supported by both Application LoadBalancers and Network Load Balancers:
            1. 'stickiness.enabled' - Indicates whether sticky sessions are enabled.
                The value is true or false. The default is false .
            2. 'stickiness.type' - The type of sticky sessions. The possible values are lb_cookie and app_cookie for
                Application Load Balancers or source_ip for Network Load Balancers.

        The following attributes are supported only if the load balancer is an Application Load Balancer and the
            target is an instance or an IP address:
            1. 'load_balancing.algorithm.type' - The load balancing algorithm determines how the load balancer
                selects targets when routing requests. The value is round_robin or least_outstanding_requests.
                The default is round_robin .
            2. 'slow_start.duration_seconds' - The time period, in seconds, during which a newly registered target
                receives an increasing share of the traffic to the target group. After this time period ends, the
                target receives its full share of traffic. The range is 30-900 seconds (15 minutes).
                The default is 0 seconds (disabled).
            3. 'stickiness.app_cookie.cookie_name' - Indicates the name of the application-based cookie. Names that
                start with the following prefixes are not allowed: AWSALB , AWSALBAPP , and AWSALBTG ; they're
                reserved for use by the load balancer.
            4. 'stickiness.app_cookie.duration_seconds' - The time period, in seconds, during which requests from a
                client should be routed to the same target. After this time period expires, the application-based
                cookie is considered stale. The range is 1 second to 1 week (604800 seconds).
                The default value is 1 day (86400 seconds).
            5. 'stickiness.lb_cookie.duration_seconds' - The time period, in seconds, during which requests from a
                client should be routed to the same target. After this time period expires, the load
                balancer-generated cookie is considered stale. The range is 1 second to 1 week (604800 seconds).
                The default value is 1 day (86400 seconds).

        The following attribute is supported only if the load balancer is an Application Load Balancer and the
            target is a Lambda function:
            1. 'lambda.multi_value_headers.enabled' - Indicates whether the request and response headers that are
                exchanged between the load balancer and the Lambda function include arrays of values or strings.
                The value is true or false. The default is false. If the value is false and the request contains
                a duplicate header field name or query parameter key, the load balancer uses the last value sent by
                the client.

        The following attributes are supported only by Network Load Balancers:
            1. 'deregistration_delay.connection_termination.enabled' - Indicates whether the load balancer
                terminates connections at the end of the deregistration timeout. The value is true or false .
                The default is false .
            2. 'preserve_client_ip.enabled' - Indicates whether client IP preservation is enabled. The value is
                true or false . The default is disabled if the target group type is IP address and the target group
                protocol is TCP or TLS. Otherwise, the default is enabled. Client IP preservation cannot be
                disabled for UDP and TCP_UDP target groups.
            3. 'proxy_protocol_v2.enabled' - Indicates whether Proxy Protocol version 2 is enabled. The value is
                true or false . The default is false .

    targets(List[Dict[str, Any]], optional): The targets. If you specified a port override when you registered a
        target, you must specify both the target ID and the port when you de-register it.

        Information about a target.
        Id(Text): The ID of the target. If the target type of the target group is instance, specify an instance
            ID. If the target type is ip , specify an IP address. If the target type is lambda , specify the ARN of
            the Lambda function. If the target type is alb , specify the ARN of the Application Load Balancer target.
        Port(Integer): The port on which the target is listening. If the target group protocol is GENEVE, the
            supported port is 6081. If the target type is alb , the targeted Application Load Balancer must have at
            least one listener whose port matches the target group port. Not used if the target is a Lambda function.
        AvailabilityZone(Text): An Availability Zone or all . This determines whether the target receives traffic
            from the load balancer nodes in the specified Availability Zone or from all enabled Availability Zones
            for the load balancer.
            1. This parameter is not supported if the target type of the target group is instance or alb .
            2. If the target type is ip and the IP address is in a subnet of the VPC for the target group, the
               Availability Zone is automatically detected and this parameter is optional. If the IP address is
               outside the VPC, this parameter is required.
            3. With an Application Load Balancer, if the target type is ip and the IP address is outside the VPC for
               the target group, the only supported value is all .
            4. If the target type is lambda , this parameter is optional and the only supported value is all .
    resource_id:(Text, optional): The Amazon Resource Name (ARN) of the ElasticLoadBalancingv2 target group.

Request Syntax:
    [target_group-name]:
      aws.elbv2.target_group.present:
        - name: 'string'
        - protocol: 'string',
        - protocol_version: 'string',
        - port: 'string',
        - vpc_id: 'string',
        - health_check_protocol: 'string',
        - health_check_port: 'string',
        - health_check_enabled: 'boolean',
        - health_check_path: 'string',
        - health_check_interval_seconds: 'integer',
        - health_check_timeout_seconds: 'integer',
        - healthy_threshold_count: 'integer',
        - unhealthy_threshold_count: 'integer',
        - matcher: list,
        - target_type: 'string',
        - tags: dict,
        - ip_address_type: 'string',
        - resource_id: 'string',
        - targets: 'list',

Returns:
    Dict[str, Any]

Examples:

.. code-block:: sls

    test_target-group_name:
      aws.elbv2.target_group.present:
        - name: my-target-group
        - protocol: HTTP,
        - protocol_version: HTTP2,
        - port: 80,
        - vpc_id: vpc-3ac0fb5f,
        - health_check_protocol: HTTP,
        - health_check_port: traffic-port,
        - health_check_enabled: True,
        - health_check_path: /health-check,
        - health_check_interval_seconds: 30,
        - health_check_timeout_seconds: 60,
        - healthy_threshold_count: 5,
        - unhealthy_threshold_count: 2,
        - matcher:
          - HttpCode: 200
        - target_type: instance,
        - tags:
            name: target-group-name
        - ip_address_type: ipv4,
        - targets:
          - Id: i-80c8dd94
            Port: 80
            AvailabilityZone: us-east-1a
        - resource_id: arn:aws:elasticloadbalancing:us-west-2:123456789012:targetgroup/my-targets/73e2d6bc24d8a067
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.elbv2.target_group](https://docs.idemproject.io/idem-aws/en/latest/ref/states/elbv2/target_group.html).
