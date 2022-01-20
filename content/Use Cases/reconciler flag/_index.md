---
title: "Reconcilier Flag"
weight: 25
---
Suppose you have an SLS file with both virtual-network and subnet. 
Because a subnet depends on a virtual-network, if you just run Idem state once, requesting a subnet will fail.
However whenever you include the <b>reconciler=basic</b> flag, this instruct idem to run a <b>reconciliation loop</b> that will automatically re-run [Idem state](/Use-Cases/SLS-States/), until the subnet gets created successfully.

The following examples showcase how to use the the <b>reconciler=basic</b> flag to create an Azure Resource Group and a Virtual-Network which depends on the same Resource Group we will create.<br>
Make sure to export the encryption key and path to the fernet file as an environment variable as described in the [authentication section](/Getting-Started/Authenticate/) before trying the commands below


Create an Azure Resource Group : <i>my_resource_group_and_virtual_networkstate.sls:</i>

```yaml
tmm-idem-01:
  azure.resource_management.resource_groups.present:
  - resource_group_name: tmm-idem-01
  - parameters:
      location: centralus
      tags: {}

vNet1-Idem:
  azure.virtual_networks.virtual_networks.present:
  - resource_group_name: tmm-idem-01
  - virtual_network_name: vNet1-Idem
  - parameters:
      location: centralus
      name: vNet1-Idem
      properties:
        addressSpace:
          addressPrefixes:
          - 10.0.0.0/24
        enableDdosProtection: false
```
The <b>State SLS</b> file can be executed with:

```shell
idem state my_resource_group_state.sls --reconciler=basic
```
You will see a similar output indicating how idem will create the dependency (the resource group) then use it as an attribute for the virtual network.

```shell
Sleeping 3 seconds for cli
Retry 1 for cli
Sleeping 3 seconds for cli
Retry 2 for cli
--------
      ID: tmm-idem-01
Function: azure.resource_management.resource_groups.present
  Result: True
 Comment: 'tmm-idem-01' has no property need to be updated.
 Changes: 
--------
      ID: vNet1-Idem
Function: azure.virtual_networks.virtual_networks.present
  Result: True
 Comment: 'vNet1-Idem' has no property need to be updated.
 Changes: 
```

<script id="asciicast-6QzLF42ABz0BA6V9YCJhBRSXn" src="https://asciinema.org/a/6QzLF42ABz0BA6V9YCJhBRSXn.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>
