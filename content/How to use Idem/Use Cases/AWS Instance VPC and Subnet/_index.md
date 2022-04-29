---
title: "AWS Instance VPC and Subnet Resources"
weight: 70
---

This example uses  [Jinja Templating](https://jinja.palletsprojects.com/en/3.0.x/) to set user input, and showcases how AWS VPC, Subnet and EC2 Instance can be created with Idem.

```shell
{% set requiredLocation = "us-east-1b" %}
{% set requiredState = "present" %}
{% set vmName = "i-00bbf5834a8395949" %}
{% set vmSubnet = "subnet-2c47c006" %}
{% set securityGroup = "sg-0e044e76" %}

my_idem_vpc:
  aws.ec2.vpc.{{ requiredState }}:
    - force_update: True
    - cidr_block_association_set:
      - CidrBlock: 10.0.0.1/24
    - tags:
      - Key: idem_demo
        Value: idem_vpc

my_idem_subnet:
  aws.ec2.subnet.{{ requiredState }}:
    - force_update: True
    - vpc_id: vpc-c96a60ad
    - cidr_block: 172.31.80.0/20
    - tags:
      - Key: idem_demo
        Value: idem_subnet

{{ vmName }}:
  aws.ec2.instance.{{ requiredState }}:
  - force_update: True
  - image_id: ami-07d0cf3af28718ef8
  - instance_type: t2.medium
  - placement:
      AvailabilityZone: {{ requiredLocation }}
      GroupName: ''
      Tenancy: default
  - subnet: {{ vmSubnet }}
  - ebs_optimized: false
  - security_group_ids:
    - {{ securityGroup }}
     {% endraw %}'
```

The <b>State SLS</b> file can be executed with:

```shell
idem state states/aws-test/instance_vpc_subnet.sls
```

You will see similar output to: 

```yaml
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
        vpc-02dd1b3d1b133ee74
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
              vpc-cidr-assoc-054174259def940c9
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
      ID: my_idem_subnet
Function: aws.ec2.subnet.present
  Result: True
 Comment: ("Created aws.ec2.subnet 'my_idem_subnet'",)
 Changes: new:
    ----------
    name:
        my_idem_subnet
    resource_id:
        subnet-01dbac229f2b5b1d3
    vpc_id:
        vpc-c96a60ad
    cidr_block:
        172.31.80.0/20
    availability_zone:
        us-east-1a
    map_public_ip_on_launch:
        False
    tags:
        |_
          ----------
          Key:
              idem_demo
          Value:
              idem_subnet
--------
      ID: i-00bbf5834a8395949
Function: aws.ec2.instance.present
  Result: True
 Comment: Created 'i-099f45dc4e9f5c972'
 Changes: 
```
