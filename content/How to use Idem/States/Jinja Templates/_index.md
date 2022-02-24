---
title: "Jinja Templates"
weight: 55
---

Idem allows you to use [Jinja Templating](https://jinja.palletsprojects.com/en/3.0.x/) in your [state SLS files](/How-to-use-Idem/States/)

Create an Azure Virtual Networks : <i>my_virtual_networkstate.sls</i>

```shell
{% set address_Prefixes = "10.0.0.0/24" %}
{% set vn_name = "TMM-VirtualNetwork-vRA" %}
{% set rg_name = "Moff-RG01-CAS" %}
{% set local_tags = {"createdWith":"idem", "owner":"tmm" } %}

{{ vn_name }}:
  azure.virtual_networks.virtual_networks.absent:
  - force_update: True
  - resource_group_name: {{ rg_name }}
  - virtual_network_name: {{ vn_name }}
  - parameters:
      location: centralus
      name: {{ vn_name }}
      properties:
        addressSpace:
          addressPrefixes:
          - {{ address_Prefixes }}
        enableDdosProtection: false
      tags: {{ local_tags }}
```
The <b>State SLS</b> file can be executed with:

```shell
idem state my_virtual_networkstate.sls
```

idem state with [Jinja Templating](https://jinja.palletsprojects.com/en/3.0.x/) can significantly boost the scalability and performance of the run. 

Let’s use this new state which verifies that 100 vpcs are absent : <i>vpc_verify_absent.sls</i>

```shell
{% for i in range(100) %}
idem_aws_test_vpc_{{i}}:
  aws.ec2.vpc.absent:
    - name: "idem_aws_test_vpc_{{i}}"
{% endfor -%}
```

The <b>State SLS</b> file can be executed with <b>–runtime parallel</b> to make full use of idem’s async execution calls:

```shell
idem state --runtime parallel vpc_verify_absent.sls
```