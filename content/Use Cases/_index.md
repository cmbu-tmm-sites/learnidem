---
title: "Use Cases"
weight: 40
---

{{< tabs "usecases" >}}
{{< tab "Describe Azure Resources" >}}
Content to walk through describing Azure resources and auto create state files for resource
{{< /tab >}}
{{< tab "Create Azure Resources" >}}
States can be accessed by their relative location in idem-azure-auto/idem_azure_auto/states.
For example, in the <b>State SLS</b> yaml file below, Azure resource group state can be created with the [Present](/Getting-Started/Basic-Commands/) function :

<i>my_resource_group_state.sls:</i>

```yaml
my-azure-resource-group:
  azure.resource_management.resource_groups.present:
  - resource_group_name: <Your Azure Resource Group Name>
  - parameters:
    location: <Azure Region>
```
The <b>State SLS</b> file can be executed with:

```shell
idem state my_resource_group_state.sls
```

Example of creating an Azure virtual network:
```yaml
my-virtual-network:
  azure.virtual_networks.virtual_networks.present:
  - resource_group_name: <Your Azure Resource Group Name>
  - virtual_network_name: <Your Virtual Network>
  - parameters:
    location: <Azure Region>
    properties:
      addressSpace:
        addressPrefixes:
        - 10.12.13.0/25
      flowTimeoutInMinutes: 10
```
The resource parameters in an SLS yaml file follow the exact structure as what’s in the [Azure REST API doc](https://docs.microsoft.com/en-us/rest/api/azure/).
<b>URI Parameters</b> should be specified in snake case with “-” in front. All parameters of the API <b>request body</b> should be specified in exactly the same way as what’s in the [Azure REST API doc](https://docs.microsoft.com/en-us/rest/api/azure/).

 You can include multiple resources in a single SLS yaml file.
 {{< /tab >}}
 {{< tab "Describe AWS Resources" >}}
 Content to walk through describing AWS resources and auto create state files for resource
 {{< /tab >}}
 {{< tab "Create AWS Resources" >}}
 Create AWS resources from state files and modify created resource
 {{< /tab >}}

 {{< /tabs >}}
