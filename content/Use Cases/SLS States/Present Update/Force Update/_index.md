---
title: "Force Update"
weight: 30
---
New Idem state feature:
<b>force_update</b> are supported on most resources. This flag is default to "False".<br>
If the flag is set to "True" in an SLS file, the resource will be updated via "PUT"
operation. This will allow parameters that aren't supported in the "PATCH" operation to be updated.<br>
<b style="color:black;">Use
with caution;</b> <b style="color:red;">"PUT" operation can  wipe out some existing data or replace the whole resource</b>, e.g. it could destroy and recreate a Virtual Machine.

Let's say I have already the Azure Virtual Network : vNet1-Idem 

```shell
(my_idem_env) demouser@idem:~/environments$ idem describe azure.virtual_networks.virtual_networks  --filter="[?resource[?virtual_network_name=='vNet1-Idem']]" 
? /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/Moff-RG01-CAS/providers/Microsoft.Network/virtualNetworks/vNet1-Idem
: azure.virtual_networks.virtual_networks.present:
  - resource_group_name: Moff-RG01-CAS
  - virtual_network_name: vNet1-Idem
  - parameters:
      etag: W/"4b58c957-49a6-49d5-b607-258bf9275080"
      id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/Moff-RG01-CAS/providers/Microsoft.Network/virtualNetworks/vNet1-Idem
      location: centralus
      name: vNet1-Idem
      properties:
        addressSpace:
          addressPrefixes:
          - 10.0.0.0/24
        enableDdosProtection: false
        provisioningState: Succeeded
        resourceGuid: 5416c5e5-72e8-4f02-9276-8b028d045a4f
        subnets: []
        virtualNetworkPeerings: []
      type: Microsoft.Network/virtualNetworks
```
and we need to update the Address Prefix from 10.0.0.0/24 to 10.12.13.0/25, we could do it by updating an SLS file and executing [idem state](/Use-Cases/SLS-States/), however due to the nature of the virtual network resource, it needs to be recreated, so we could only do it by running the same SLS file but this time explicitly including the <b>force_update</b> set to "True"

```yaml
vNet1-Idem:
  azure.virtual_networks.virtual_networks.present:
  - force_update: True
  - resource_group_name: Moff-RG01-CAS
  - virtual_network_name: vNet1-Idem
  - parameters:
      location: centralus
      name: vNet1-Idem
      properties:
        addressSpace:
          addressPrefixes:
          - 10.12.13.0/25
        enableDdosProtection: false

```
We apply our changes:

```shell
idem state update_virtual_network_addPrefix.sls
```

Then we verify that the Address Prefix was indeed updated

```shell
(my_idem_env) demouser@idem:~/environments$ idem describe azure.virtual_networks.virtual_networks  --filter="[?resource[?virtual_network_name=='vNet1-Idem']]" 
? /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/Moff-RG01-CAS/providers/Microsoft.Network/virtualNetworks/vNet1-Idem
: azure.virtual_networks.virtual_networks.present:
  - resource_group_name: Moff-RG01-CAS
  - virtual_network_name: vNet1-Idem
  - parameters:
      etag: W/"f36439b9-78db-48b1-96aa-92a4a950397d"
      id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/Moff-RG01-CAS/providers/Microsoft.Network/virtualNetworks/vNet1-Idem
      location: centralus
      name: vNet1-Idem
      properties:
        addressSpace:
          addressPrefixes:
          - 10.12.13.0/25
        enableDdosProtection: false
        provisioningState: Succeeded
        resourceGuid: 636fd30a-b0d8-471d-9868-c684ad602597
        subnets: []
        virtualNetworkPeerings: []
      type: Microsoft.Network/virtualNetworks
```
<script id="asciicast-2Ae7Ar7RECBy8Io3124LEh3Wk" src="https://asciinema.org/a/2Ae7Ar7RECBy8Io3124LEh3Wk.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>
