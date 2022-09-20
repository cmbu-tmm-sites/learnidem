---
title: "aws.elb.load_balancer"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified load balancer.

If you are attempting to recreate a load balancer, you must reconfigure all
settings. The DNS name associated with a deleted load balancer are no longer usable. The name and associated DNS
record of the deleted load balancer no longer exist and traffic sent to any of its IP addresses is no longer
delivered to your instances.

If the load balancer does not exist or has already been deleted, the call to DeleteLoadBalancer still succeeds.

Args:
    name(Text): Idem name of the load balancer.
    resource_id:(Text, optional): AWS ELB load balancer name.

Request Syntax:
    [load_balancer-name]:
      aws.elb.load_balancer.absent:
      - name: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        test_load-balancer_name:
            aws.elb.load_balancer.absent:
              - name: my-load-balancer
              - resource_id: my-load-balancer
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function.
This call describes all of your load balancers.

Returns:
    Dict[str, Any]

Examples:

.. code-block:: bash

    $ idem describe aws.elb.load_balancer
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a Classic Load Balancer. You can add listeners, security groups, subnets, and tags when you create your
load balancer, or you can add them later using CreateLoadBalancerListeners , ApplySecurityGroupsToLoadBalancer ,
AttachLoadBalancerToSubnets and AddTags .

To describe your current load balancers, see DescribeLoadBalancers. When you are finished with a load balancer,
you can delete it using DeleteLoadBalancer.

You can create up to 20 load balancers per region per account. You can request an increase for the number of load
balancers for your account. For more information, see Limits for Your Classic Load Balancer in the
Classic Load Balancers Guide.

Args:
    name(Text): The name of the load balancer. This name must be unique within your set of load balancers for the
        region, must have a maximum of 32 characters, must contain only alphanumeric characters or hyphens, and
        cannot begin or end with a hyphen.
    listeners(List): The listeners.
        (Dict) --
            Information about a listener.
            Protocol (Text)
                The load balancer transport protocol to use for routing: HTTP, HTTPS, TCP, or SSL.
            LoadBalancerPort (Integer)
                The port on which the load balancer is listening. On EC2-VPC, you can specify any port from the
                range 1-65535. On EC2-Classic, you can specify any port from the following list: 25, 80, 443, 465,
                587, 1024-65535.
            InstanceProtocol (Text, Optional)
                1. The protocol to use for routing traffic to instance: HTTP, HTTPS, TCP, or SSL. If the front-end
                protocol is TCP or SSL, the back-end protocol must be TCP or SSL. If the front-end protocol is HTTP
                or HTTPS, the back-end protocol must be HTTP or HTTPS.
                2. If there is another listener with the same InstancePort whose InstanceProtocol is secure,
                (HTTPS or SSL), the listener's InstanceProtocol must also be secure.
                3. If there is another listener with the same InstancePort whose InstanceProtocol is HTTP or TCP,
                the listener's InstanceProtocol must be HTTP or TCP.
            InstancePort (Integer)
                The port on which the instance is listening.
            SSLCertificateId (Text, Optional)
                The Amazon Resource Name (ARN) of the server certificate.
    availability_zones(List, Optional):
        One or more Availability Zones from the same region as the load balancer. You must specify at least one
        Availability Zone. You can add more Availability Zones after you create the load balancer using
        EnableAvailabilityZonesForLoadBalancer .
    subnets(List, Optional):
        The IDs of the subnets in your VPC to attach to the load balancer. Specify one subnet per Availability Zone
        specified in AvailabilityZones .
    security_groups(List, Optional):
        The IDs of the security groups to assign to the load balancer.
    scheme(Text, Optional):
        1. Given load balance type. Valid only for load balancers in a VPC. By default, Elastic Load
        Balancing creates an Internet-facing load balancer with a DNS name that resolves to public IP addresses.
        2. Specify internal to create a load balancer with a DNS name that resolves to private IP addresses.
    instances(Dict, optional):
        The IDs of the instances.
            The ID of an EC2 instance (Dict)
                InstanceId (Text): The instance ID.
    load_balancer_attributes(Dict, Optional):
        The attributes for the load balancer.

        CrossZoneLoadBalancing(Dict): If enabled, the load balancer routes the request traffic evenly across all
                    instances regardless of the Availability Zones.
            Enabled (boolean): Specifies whether cross-zone load balancing is enabled for the load balancer.

        AccessLog(Dict, Optional): If enabled, the load balancer captures detailed information of all requests and
                    delivers the information to the Amazon S3 bucket that you specify.
            Enabled(Boolean): Specifies whether access logs are enabled for the load balancer.
            S3BucketName(Text, optional): The name of the Amazon S3 bucket where the access logs are stored.
            EmitInterval(Integer, optional): The interval for publishing the access logs. You can specify an
                interval of either 5 minutes or 60 minutes. Default: 60 minutes
            S3BucketPrefix(Text, optional): The logical hierarchy you created for your Amazon S3 bucket, for example
                my-bucket-prefix/prod . If the prefix is not provided, the log is placed at the root level of the
                bucket.

        ConnectionDraining(Dict, optional): If enabled, the load balancer allows existing requests to complete
                    before the load balancer shifts traffic away from a deregistered or unhealthy instance.
            Enabled(Boolean): Specifies whether connection draining is enabled for the load balancer.
            Timeout(Integer, optional): The maximum time, in seconds, to keep the existing connections open before
                unregistering the instances.
            ConnectionSettings(Dict): If enabled, the load balancer allows the connections to remain idle
                (no data is sent over the connection) for the specified duration.
            IdleTimeout(Integer): The time, in seconds, that the connection is allowed to be idle (no data has been
                sent over the connection) before it is closed by the load balancer.

        AdditionalAttributes (List, optional): Any additional attributes.
            (Dict): Information about additional load balancer attributes.
                Key (Text): The name of the attribute. The following attribute is supported.
                    elb.http.desyncmitigationmode - Determines how the load balancer handles requests that might
                        pose a security risk to your application. The possible values are monitor , defensive ,
                        and strictest . The default is defensive .
                Value (Text, optional): This value of the attribute.
    tags([Dict[str, str], optional): The tags to assign to the load balancer. Defaults to None.
        * Key (Text): The key of the tag.
        * Value (Text, optional): The value of the tag.

    resource_id:(Text, optional): AWS ELB load balancer name.

Request Syntax:
[load_balancer-name]:
  aws.elb.load_balancer.present:
  - name: 'string'
  - listeners: 'list'
  - availability_zones: 'list'
  - subnets: 'string'
  - security_groups: 'list'
  - scheme: 'string'
  - instances: 'list',
  - load_balancer_attributes: 'list',
  - tags:
      'string': 'string'
  - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

.. code-block:: sls

    test_load-balancer_name:
      aws.elb.load_balancer.present:
        - name: my-load-balancer
        - resource_id: my-load-balancer
        - listeners:
          - InstancePort: 80
          - InstanceProtocol: HTTP
          - LoadBalancerPort: 80
          - Protocol: HTTP
        - tags:
            name: my-load-balancer
        - availability_zones
          - us-west-2a
        - subnets
          - subnet-15aaab61
        - security_groups
          - sg-a61988c378fgtyu
        - scheme: internal
        - instances:
          - i-d6f6f34tyu78ae3
          - i-207d9vbty56u717
          - i-afefvbu90ipb49b
        - load_balancer_attributes:
          - CrossZoneLoadBalancing
            Enabled: True
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.elb.load_balancer](https://docs.idemproject.io/idem-aws/en/latest/ref/states/elb/load_balancer.html).
