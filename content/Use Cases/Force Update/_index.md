---
title: "Force Update"
weight: 30
---
New Idem state feature:
"force_update" are supported on most resources. This flag is default to False.
If the flag is set to True in an sls file, the resource will be updated via PUT
operation with Azure. This will allow parameters that aren't supported in the
PATCH operation to be updated. However, this is also a riskier operation since
PUT operation can wipe out some existing data of the resource on Azure. So use
with caution.

```shell
my-virtual-network:
  azure.virtual_networks.virtual_networks.present:
  - force_update: True
  - resource_group_name: my-azure-resource-group
  - virtual_network_name: my-virtual-network
  - parameters:
    location: eastus
    properties:
      addressSpace:
        addressPrefixes:
        - 10.12.13.0/25
      flowTimeoutInMinutes: 10

```


