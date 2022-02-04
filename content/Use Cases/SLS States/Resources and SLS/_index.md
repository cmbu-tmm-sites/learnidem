---
title: "Resources and SLS"
weight: 55
---

This example showcases how to combine multiple resources in one single SLS State file, for creating a basic Azure Virtual Machine, we will create the Resource Group, Re-Use an existing NIC and then create the Azure Virtual Machine resource, then we will update the metadata:

We will use [describe](/Getting-Started/Basic-Commands/) command to verify we don't have an existing Azure VM

```shell
idem describe azure.compute.virtual_machines
```
You should get empty brackets

```shell
{}
```

Let's first create an Azure Resource Group named "moff-idem-01"

We can do it by writing the following state <b>"rg_moff_present.sls"</b>
that includes the idem [present](/Getting-Started/Basic-Commands/) directive for <b>azure.resource_management.resource_groups</b>

```shell
moff-idem-01:
  azure.resource_management.resource_groups.present:
  - resource_group_name: moff-idem-01
  - parameters:
      location: eastus
      tags: {}
```

Then we can simply execute it by calling the command "state"

```shell
idem state rg_moff_present.sls
```

This will return the following output (please note the provisioningState):

```shell
--------
      ID: moff-idem-01
Function: azure.resource_management.resource_groups.present
  Result: True
 Comment: Created
 Changes: new:
    ----------
    id:
        /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-01
    name:
        moff-idem-01
    type:
        Microsoft.Resources/resourceGroups
    location:
        eastus
    tags:
        ----------
    properties:
        ----------
        provisioningState:
            Succeeded
```

If we re-run the same "state" command, it will indicate that indeed the resource is present, and that nothing changed since we didn't introduce any modifications to the state file. 

```shell
--------
      ID: moff-idem-01
Function: azure.resource_management.resource_groups.present
  Result: True
 Comment: 'moff-idem-01' has no property need to be updated.
 Changes: 
```

Now, in order to create a Azure VM, we will need to indicate the "networkInterfaces id"

We can create it also with "idem virtual_networks" or we could re-use an existing one by discovering with the "idem describe" command for "virtual_networks" resources:

```shell
idem describe azure.virtual_networks.network_interfaces
```

In this case, the output of the command shows this network interface available

```shell
--------
? /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default
: azure.virtual_networks.network_interfaces.present:
  - network_interface_name: default
  - resource_group_name: group8a87dd00ea7183a729588634c88e5123
  - parameters:
      etag: W/6f33dd08-64fa-4d11-8c17-2d9fdea97671
      "id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default"
      location: centralus
      name: default
      properties:
        dnsSettings:
          appliedDnsServers: []
          dnsServers: []
        enableAcceleratedNetworking: false
        enableIPForwarding: false
        hostedWorkloads: []
        ipConfigurations:
        - etag: W/6f33dd08-64fa-4d11-8c17-2d9fdea97671
          id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default/ipConfigurations/nicconfig8a87dd00ea7183a729588634c88e5123
          name: nicconfig8a87dd00ea7183a729588634c88e5123
          properties:
            primary: true
            privateIPAddress: 10.0.0.8
            privateIPAddressVersion: IPv4
            privateIPAllocationMethod: Dynamic
            provisioningState: Succeeded
            publicIPAddress:
              id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/publicIPAddresses/VNF-Primary-CSCF-1-002668-pip
            subnet:
              id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/Moff-RG01-CAS/providers/Microsoft.Network/virtualNetworks/vNet1-MoffCAS01/subnets/default
          type: Microsoft.Network/networkInterfaces/ipConfigurations
        macAddress: 00-0D-3A-A5-4A-E9
        networkSecurityGroup:
          id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/Moff-RG01-CAS/providers/Microsoft.Network/networkSecurityGroups/Moff-CAS-Default
        nicType: Standard
        provisioningState: Succeeded
        resourceGuid: 33b57d86-1cfd-4c05-9772-92cfcc1e0f6c
        tapConfigurations: []
        vnetEncryptionSupported: false
```

Now, let's write a new state <b>"vm_moff_present.sls"</b> defining our Azure VM
that includes the idem [present](/Getting-Started/Basic-Commands/) directive for <b>azure.compute.virtual_machines</b>

Also note that included properties needed for creating the Azure VM, such as VM Name, Hardware Profile (Flavor), ImageReference, etc.

```shell
  azure.compute.virtual_machines.present:
  - resource_group_name: moff-idem-01
  - vm_name: Development-idem-015042
  - parameters:
      location: centralus
      name: Development-idem-015042
      properties:
        hardwareProfile:
          vmSize: Standard_A5
        networkProfile:
          networkInterfaces:
          - id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default
            properties:
              primary: true
        storageProfile:
          dataDisks: []
          imageReference:
            exactVersion: 18.04.201804262
            offer: UbuntuServer
            publisher: Canonical
            sku: 18.04-LTS
            version: 18.04.201804262
        osProfile:
          adminUsername: azureuser
          allowExtensionOperations: true
          computerName: Development-idem-015042
          adminPassword: "C@n0n1c@lVMware"
          linuxConfiguration:
            disablePasswordAuthentication: false
            patchSettings:
              assessmentMode: ImageDefault
              patchMode: ImageDefault
            provisionVMAgent: true
          secrets: []
```

and just as before when we created our Azure Resource Group, we can simply execute it by calling the command "state"

```shell
idem state vm_moff_present.sls
```

This will return the following output (please note the provisioningState):

```shell
--------
      ID: Development-idem-015042
Function: azure.compute.virtual_machines.present
  Result: True
 Comment: Created
 Changes: new:
    ----------
    name:
        Development-idem-015042
    id:
        /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-01/providers/Microsoft.Compute/virtualMachines/Development-idem-015042
    type:
        Microsoft.Compute/virtualMachines
    location:
        centralus
    properties:
        ----------
        vmId:
            1ae9935c-3699-4837-a59d-a2938b24644d
        hardwareProfile:
            ----------
            vmSize:
                Standard_A5
        storageProfile:
            ----------
            imageReference:
                ----------
                publisher:
                    Canonical
                offer:
                    UbuntuServer
                sku:
                    18.04-LTS
                version:
                    18.04.201804262
                exactVersion:
                    18.04.201804262
            osDisk:
                ----------
                osType:
                    Linux
                createOption:
                    FromImage
                caching:
                    ReadWrite
                managedDisk:
                    ----------
                    storageAccountType:
                        Standard_LRS
                deleteOption:
                    Detach
                diskSizeGB:
                    30
            dataDisks:
        osProfile:
            ----------
            computerName:
                Development-idem-015042
            adminUsername:
                azureuser
            linuxConfiguration:
                ----------
                disablePasswordAuthentication:
                    False
                provisionVMAgent:
                    True
                patchSettings:
                    ----------
                    patchMode:
                        ImageDefault
                    assessmentMode:
                        ImageDefault
            secrets:
            allowExtensionOperations:
                True
            requireGuestProvisionSignal:
                True
        networkProfile:
            ----------
            networkInterfaces:
                |_
                  ----------
                  id:
                      /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default
                  properties:
                      ----------
                      primary:
                          True
        "provisioningState:
            Creating"
```

If we re-run the same "state" command, it will indicate that indeed the resource is present, and that nothing changed since we didn't introduce any modifications to the state file. 

```shell
--------
      ID: Development-idem-015042
Function: azure.compute.virtual_machines.present
  Result: True
 Comment: OK
 Changes: old:
    ----------
    properties:
        ----------
        provisioningState:
            Creating
new:
    ----------
    properties:
        ----------
        "provisioningState:
            Updating"
```

At this point if we re-run [describe](/Getting-Started/Basic-Commands/) command for <b>azure.compute.virtual_machines</b>

```shell
idem describe azure.compute.virtual_machines
```
We get a description for the newly added Azure VM

```shell
? /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/MOFF-IDEM-01/providers/Microsoft.Compute/virtualMachines/Development-idem-015042
: azure.compute.virtual_machines.present:
  - resource_group_name: MOFF-IDEM-01
  - vm_name: Development-idem-015042
  - parameters:
      id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/MOFF-IDEM-01/providers/Microsoft.Compute/virtualMachines/Development-idem-015042
      location: centralus
      name: Development-idem-015042
      properties:
        hardwareProfile:
          vmSize: Standard_A5
        networkProfile:
          networkInterfaces:
          - id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default
            properties:
              primary: true
        osProfile:
          adminUsername: azureuser
          allowExtensionOperations: true
          computerName: Development-idem-015042
          linuxConfiguration:
            disablePasswordAuthentication: false
            patchSettings:
              assessmentMode: ImageDefault
              patchMode: ImageDefault
            provisionVMAgent: true
          requireGuestProvisionSignal: true
          secrets: []
        provisioningState: Succeeded
        storageProfile:
          dataDisks: []
          imageReference:
            exactVersion: 18.04.201804262
            offer: UbuntuServer
            publisher: Canonical
            sku: 18.04-LTS
            version: 18.04.201804262
          osDisk:
            caching: ReadWrite
            createOption: FromImage
            deleteOption: Detach
            diskSizeGB: 30
            managedDisk:
              id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-01/providers/Microsoft.Compute/disks/Development-idem-015042_OsDisk_1_e6d0942b1250478f86e21be7ed48629b
              storageAccountType: Standard_LRS
            name: Development-idem-015042_OsDisk_1_e6d0942b1250478f86e21be7ed48629b
            osType: Linux
        vmId: 1ae9935c-3699-4837-a59d-a2938b24644d
      type: Microsoft.Compute/virtualMachines
```

Now let's update this Azure VM metadata by adding new tags, all we need to do is to update our existing state <b>"vm_moff_present.sls"</b> by append the property "tag" at the bottom

```shell
Development-idem-015042:
  azure.compute.virtual_machines.present:
  - resource_group_name: moff-idem-01
  - vm_name: Development-idem-015042
  - parameters:
      location: centralus
      name: Development-idem-015042
      properties:
        hardwareProfile:
          vmSize: Standard_A5
        networkProfile:
          networkInterfaces:
          - id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default
            properties:
              primary: true
        storageProfile:
          dataDisks: []
          imageReference:
            exactVersion: 18.04.201804262
            offer: UbuntuServer
            publisher: Canonical
            sku: 18.04-LTS
            version: 18.04.201804262
        osProfile:
          adminUsername: azureuser
          allowExtensionOperations: true
          computerName: Development-idem-015042
          adminPassword: "C@n0n1c@lVMware"
          linuxConfiguration:
            disablePasswordAuthentication: false
            patchSettings:
              assessmentMode: ImageDefault
              patchMode: ImageDefault
            provisionVMAgent: true
          secrets: []
      tags:
        blueprintname: goapp-terraform
        deployment: IDEM-Test-Azure
        project: development
```

 we can, once again, call the command "state"

```shell
idem state vm_moff_present.sls
```

This will return the following output (please note the provisioningState):

```shell
--------
      ID: Development-idem-015042
Function: azure.compute.virtual_machines.present
  Result: True
 Comment: OK
 Changes: old:
    ----------
    properties:
        ----------
        provisioningState:
            Succeeded
new:
    ----------
    tags:
        ----------
        blueprintname:
            goapp-terraform
        deployment:
            IDEM-Test-Azure
        project:
            development
    properties:
        ----------
        "provisioningState:
            Updating"
```

And consequently if we re-run [describe](/Getting-Started/Basic-Commands/) command for <b>azure.compute.virtual_machines</b>

```shell
idem describe azure.compute.virtual_machines
```
We get a description for the newly added Azure VM but this time at the bottom we can see the "tag" information.

```shell
? /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/MOFF-IDEM-01/providers/Microsoft.Compute/virtualMachines/Development-idem-015042
: azure.compute.virtual_machines.present:
  - resource_group_name: MOFF-IDEM-01
  - vm_name: Development-idem-015042
  - parameters:
      id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/MOFF-IDEM-01/providers/Microsoft.Compute/virtualMachines/Development-idem-015042
      location: centralus
      name: Development-idem-015042
      properties:
        hardwareProfile:
          vmSize: Standard_A5
        networkProfile:
          networkInterfaces:
          - id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default
            properties:
              primary: true
        osProfile:
          adminUsername: azureuser
          allowExtensionOperations: true
          computerName: Development-idem-015042
          linuxConfiguration:
            disablePasswordAuthentication: false
            patchSettings:
              assessmentMode: ImageDefault
              patchMode: ImageDefault
            provisionVMAgent: true
          requireGuestProvisionSignal: true
          secrets: []
        provisioningState: Succeeded
        storageProfile:
          dataDisks: []
          imageReference:
            exactVersion: 18.04.201804262
            offer: UbuntuServer
            publisher: Canonical
            sku: 18.04-LTS
            version: 18.04.201804262
          osDisk:
            caching: ReadWrite
            createOption: FromImage
            deleteOption: Detach
            diskSizeGB: 30
            managedDisk:
              id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-01/providers/Microsoft.Compute/disks/Development-idem-015042_OsDisk_1_e6d0942b1250478f86e21be7ed48629b
              storageAccountType: Standard_LRS
            name: Development-idem-015042_OsDisk_1_e6d0942b1250478f86e21be7ed48629b
            osType: Linux
        vmId: 1ae9935c-3699-4837-a59d-a2938b24644d
      "tags:
        blueprintname: goapp-terraform
        deployment: IDEM-Test-Azure
        project: development"
      type: Microsoft.Compute/virtualMachines
```

And once we don't need this Azure VM and Resource Group

We can do it by writing the following state <b>"vm_rg_moff_absent.sls"</b>
that includes the idem [absent](/Getting-Started/Basic-Commands/) directive for <b>azure.resource_management.resource_groups</b> & <b>azure.compute.virtual_machines</b>

```shell
Development-idem-015042:
  azure.compute.virtual_machines.absent:
  - resource_group_name: MOFF-IDEM-01
  - vm_name: Development-idem-015042
  - parameters:
      location: centralus
      name: Development-idem-015042

moff-idem-01:
  azure.resource_management.resource_groups.absent:
  - resource_group_name: moff-idem-01
  - parameters:
      location: eastus

```
Then running the command

```shell
idem state vm_rg_moff_absent.sls
```

This will return the following output (please note the provisioningState):

```shell
--------
      ID: Development-idem-015042
Function: azure.compute.virtual_machines.absent
  Result: True
 Comment: Accepted
 Changes: old:
    ----------
    name:
        Development-idem-015042
    id:
        /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/MOFF-IDEM-01/providers/Microsoft.Compute/virtualMachines/Development-idem-015042
    type:
        Microsoft.Compute/virtualMachines
    location:
        centralus
    tags:
        ----------
        blueprintname:
            goapp-terraform
        deployment:
            IDEM-Test-Azure
        project:
            development
    properties:
        ----------
        vmId:
            1ae9935c-3699-4837-a59d-a2938b24644d
        hardwareProfile:
            ----------
            vmSize:
                Standard_A5
        storageProfile:
            ----------
            imageReference:
                ----------
                publisher:
                    Canonical
                offer:
                    UbuntuServer
                sku:
                    18.04-LTS
                version:
                    18.04.201804262
                exactVersion:
                    18.04.201804262
            osDisk:
                ----------
                osType:
                    Linux
                name:
                    Development-idem-015042_OsDisk_1_e6d0942b1250478f86e21be7ed48629b
                createOption:
                    FromImage
                caching:
                    ReadWrite
                managedDisk:
                    ----------
                    storageAccountType:
                        Standard_LRS
                    id:
                        /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-01/providers/Microsoft.Compute/disks/Development-idem-015042_OsDisk_1_e6d0942b1250478f86e21be7ed48629b
                deleteOption:
                    Detach
                diskSizeGB:
                    30
            dataDisks:
        osProfile:
            ----------
            computerName:
                Development-idem-015042
            adminUsername:
                azureuser
            linuxConfiguration:
                ----------
                disablePasswordAuthentication:
                    False
                provisionVMAgent:
                    True
                patchSettings:
                    ----------
                    patchMode:
                        ImageDefault
                    assessmentMode:
                        ImageDefault
            secrets:
            allowExtensionOperations:
                True
            requireGuestProvisionSignal:
                True
        networkProfile:
            ----------
            networkInterfaces:
                |_
                  ----------
                  id:
                      /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/group8a87dd00ea7183a729588634c88e5123/providers/Microsoft.Network/networkInterfaces/default
                  properties:
                      ----------
                      primary:
                          True
        "provisioningState:
            Succeeded"
--------
      ID: moff-idem-01
Function: azure.resource_management.resource_groups.absent
  Result: True
 Comment: Accepted
 Changes: old:
    ----------
    id:
        /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-01
    name:
        moff-idem-01
    type:
        Microsoft.Resources/resourceGroups
    location:
        eastus
    tags:
        ----------
    properties:
        ----------
        "provisioningState:
            Succeeded"
```
If we re-run the same "state" command, 


```shell
idem state vm_rg_moff_absent.sls
```

it will indicate that indeed the resource is already absent or being deleted (some resources take more time to be removed). 

```shell
--------
      ID: Development-idem-015042
Function: azure.compute.virtual_machines.absent
  Result: True
 Comment: 'Development-idem-015042' already absent
 Changes: None
--------
      ID: moff-idem-01
Function: azure.resource_management.resource_groups.absent
  Result: True
 Comment: Accepted
 Changes: old:
    ----------
    id:
        /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-01
    name:
        moff-idem-01
    type:
        Microsoft.Resources/resourceGroups
    location:
        eastus
    tags:
        ----------
    properties:
        ----------
        "provisioningState:
            Deleting"
```

One more time

```shell
idem state vm_rg_moff_absent.sls
```

And both Azure resources are removed or absent

```shell
--------
      ID: Development-idem-015042
Function: azure.compute.virtual_machines.absent
  Result: True
 Comment: 'Development-idem-015042' already absent
 Changes: None
--------
      ID: moff-idem-01
Function: azure.resource_management.resource_groups.absent
  Result: True
 Comment: 'moff-idem-01' already absent
 Changes: None
```
 Some resources may have dependencies among them, for that you include [ reconciler=basic flag ](/Use-Cases/reconciler-flag/), This allows Idem-azure-auto to run Idem state
with Idem's reconciliation loop.
