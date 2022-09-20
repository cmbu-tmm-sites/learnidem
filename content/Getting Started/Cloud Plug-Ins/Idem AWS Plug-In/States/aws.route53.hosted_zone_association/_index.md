---
title: "aws.route53.hosted_zone_association"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Removes the specified managed policy from the specified role.

Args:
    name(Text): An Idem name of the AWS hosted zone vpc association.
    resource_id(Text, optional): The id of the hosted zone and vpc association. Idem automatically considers this resource being absent
     if this field is not specified.
    comment(Text, optional): A comment about the disassociation request.
    timeout(Dict, optional): Timeout configuration for hosted zone and vpc association.
        * delete (Dict) -- Timeout configuration for creating nat gateway
                * delay (int) -- The amount of time in seconds to wait between attempts. Defaults to 15.
                * max_attempts(int) -- Customized timeout configuration containing delay and max attempts. Defaults to 40.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        Z09756241DYDBTZK8J11E:vpc-9aacf0f2:eu-central-1:
          aws.route53.hosted_zone_association.absent:
            - name: Z09756241DYDBTZK8J11E:vpc-9aacf0f2:eu-central-1
            - resource_id: Z09756241DYDBTZK8J11E:vpc-9aacf0f2:eu-central-1
            - timeout:
                delete:
                    delay: 15
                    max_attempts: 40
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists the associated vpc's with respective hosted zones. If there are no vpc associated with the specified hosted
zone, the operation returns an empty dict.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.route53.hosted_zone_association
```
{{< /tab >}}

{{< tab "present" >}}

```
Associates the specified vpc to the specified hosted zone.

Args:
    hub:
    ctx:
    name(Text): An Idem name of the AWS hosted zone vpc association.
    zone_id(Text): The id of hosted zone to associate to a vpc
    vpc_id(Text): The id of the vpc to associate to a hosted zone.
    vpc_region(Text, optional): The AWS region where the vpc belongs to.
                                If the vpc_region is not specified, AWS region from credentials file will be used.
    resource_id(Text, optional): The identifier for this object, combination of hosted_zone id, vpc id and vpc region separated by a separator ':'
    comment(Text, optional): A comment about the association request.
    timeout(Dict, optional): Timeout configuration for create/update of AWS DB Cluster.
        * create (Dict) -- Timeout configuration for creating DB Cluster
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- Customized timeout configuration containing delay and max attempts.
    timeout(Dict, optional): Timeout configuration for hosted zone and vpc association.
        * create (Dict) -- Timeout configuration for creating nat gateway
             * delay (int) -- The amount of time in seconds to wait between attempts. Defaults to 15.
            * max_attempts(int) -- Customized timeout configuration containing delay and max attempts. Defaults to 40.

Request Syntax:
    [zone_id:vpc_id:vpc_region]:
      aws.route53.hosted_zone_association.present:
      - resource_id: 'string'
      - zone_id: 'string'
      - vpc_id: 'string'
      - vpc_region: 'string'
      - comment: 'string'
      - timeout:
          create
            delay: 'integer'
            max_attempts: 'integer'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        Z09756241DYDBTZK8J11E:vpc-9aacf0f2:eu-central-1:
          aws.route53.hosted_zone_association.present:
            - zone_id: Z09756241DYDBTZK8J11E
            - vpc_id: vpc-9aacf0f2
            - vpc_region: eu-central-1
            - resource_id: Z09756241DYDBTZK8J11E:vpc-9aacf0f2:eu-central-1
            - timeout:
                create:
                    delay: 15
                    max_attempts: 40
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.route53.hosted_zone_association](https://docs.idemproject.io/idem-aws/en/latest/ref/states/route53/hosted_zone_association.html).
