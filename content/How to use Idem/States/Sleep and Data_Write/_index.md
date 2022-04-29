---
title: "Sleep and Data.Write"
weight: 60
---

Idem introduced the <strong>Sleep</strong> function for controlled delays in execution, this is useful whenever you combine multiple resources or need to pause Idem run

Additionally the <strong>Data.Write</strong> function allows you to export directly the output of a state execution with 
 [Jinja Templating](https://jinja.palletsprojects.com/en/3.0.x/) support.

This example uses  [Jinja Templating](https://jinja.palletsprojects.com/en/3.0.x/) to set user input, it waits 5 seconds before creating an AWS VPC Resource then outputs the VPC ID result into the text file "vpc-resources.txt"

```shell
{% set requiredLocation = "us-east-1b" %}
{% set requiredState = "present" %}
{% set output_dir = "/home/demouser/environments" %}
{% set rgsList = ["my_idem_vpc"] %}

sleep_5s:
  time.sleep:
      - duration: 5

{% for i in rgsList %}
{{i}}:        
  aws.ec2.vpc.{{ requiredState }}:
    - cidr_block_association_set:
      - CidrBlock: 10.0.0.1/24
    - tags:
      - Key: idem_demo
        Value: idem_vpc
{% endfor -%}

vpc-resources-to-import:
    data.write:
        - file_name: "{{ output_dir }}/states/aws-test/vpc-resources.txt"
        - template: '{% raw %}
                              My Demo vpc.${aws.ec2.vpc:my_idem_vpc:resource_id}
                     {% endraw %}'
```

The <b>State SLS</b> file can be executed with:

```shell
idem state states/aws-test/instance_vpc.sls 
```

You will see similar output to: 

```yaml
--------
      ID: sleep_5s
Function: time.sleep
  Result: True
 Comment: ('Successfully slept for 5 seconds.',)
 Changes: 
--------
      ID: my_idem_vpc
Function: aws.ec2.vpc.present
  Result: True
 Comment: ("Created aws.ec2.vpc 'my_idem_vpc'",)
 Changes: new:
    ----------
    name:
        my_idem_vpc
    resource_id:
        vpc-015ce7a4bca01de3c
    instance_tenancy:
        default
    tags:
        |_
          ----------
          Key:
              idem_demo
          Value:
              idem_vpc
    cidr_block_association_set:
        |_
          ----------
          AssociationId:
              vpc-cidr-assoc-011a7e466f9fd671d
          CidrBlock:
              10.0.0.0/24
          CidrBlockState:
              ----------
              State:
                  associated
    enable_dns_hostnames:
        False
    enable_dns_support:
        True
--------
      ID: vpc-resources-to-import
Function: data.write
  Result: True
 Comment: Wrote to file '/home/demouser/environments/states/aws-test/vpc-resources.txt'.
 Changes:
```

And the content of the '/home/demouser/environments/states/aws-test/vpc-resources.txt' file:

```shell
My Demo vpc.vpc-015ce7a4bca01de3c
```