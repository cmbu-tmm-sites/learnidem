---
title: "SLS States"
weight: 15
---

States are yaml file definitions with extension <b>SLS</b> <br>
States can be accessed by their relative location in idem-azure-auto/idem_azure_auto/states.<br>
For example, in the <b>State SLS</b> yaml file below, Azure resource group state can be created and subsequently updated with the [Present](/Getting-Started/Basic-Commands/) state function. 

The following examples showcase how to use the available [idem states](/Getting-Started/Basic-Commands/) to work with Azure Resources.
Make sure to export the encryption key and path to the <i>fernet file</i> as an environment variable as described in the [authentication section](/Getting-Started/Authenticate/) before trying the commands below

{{< tabs "usecases" >}}

{{< tab "Present" >}}

In order to create a new Azure Resource Group, we craft the <b>my_resource_group_state.sls:</b> file with the following contents:

```yaml
<Your Azure Resource Group Name>:
  azure.resource_management.resource_groups.present:
  - resource_group_name: <Your Azure Resource Group Name>
  - parameters:
    location: <Azure Region>
```
We refer first to the Azure Idem Provider's Resource Group - "[azure.resource_management.resource_groups](/Getting-Started/Cloud-Providers/)" and we append the state directive [present](Getting-Started/Basic-Commands/), for instructing idem to <b>create</b> a new resource group in Azure.

Then <b>State SLS</b> file can be executed with:

```shell
idem state <file_path>/my_resource_group_state.sls
```
In this example:

```shell
idem state my_resource_group_state.sls
```

Now, for creating an Azure virtual network, the process would be the same, we only need to change the resource pointer:

```yaml
<Your Virtual Network>:
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
<b>URI Parameters</b> should be specified in each case with “-” in front. All parameters of the API <b>request body</b> should be specified in exactly the same way as what’s in the [Azure REST API doc](https://docs.microsoft.com/en-us/rest/api/azure/). Please note that we can use the [state describe](Getting-Started/Basic-Commands/) for creating SLS files with most parameters.

 You can include multiple resources in a single SLS yaml file.
 Some resources may have dependencies among them, for that you include [ reconciler=basic flag ](/Use-Cases/reconciler-flag/), This allows Idem-azure-auto to run Idem state
with Idem's reconciliation loop.

 {{< /tab >}}

  {{< tab "Present (Update)" >}}
We can also use the state directive [present](Getting-Started/Basic-Commands/), for instructing Idem to <b>update</b> an existing resource's properties or behavior, e.g. updating specific resource parameters such as : location, tags, addressprefix, etc. 

Please note that due to the nature of some resources, the only way to update parameters or behaviors is by re-creating them, in those scenarios you can include the [force_update: True](/Use-Cases/Force-Update/) flag for enforcing the new present goal state.

Let's update the <b>tags</b> information for an existing Azure Resource Group, in order to do that, we craft the <b>update_my_resource_group_state.sls:</b> file with the following contents:

 ```yaml
<Your Azure Resource Group Name>:
  azure.resource_management.resource_groups.present:
  - resource_group_name: <Your Azure Resource Group Name>
  - parameters:
    location: <Azure Region>
    tags: {"createdWith": "idem"}
```
We added just the code line: <b>tags: {"createdWith": "idem"}</b> 
Then <b>State SLS</b> file can be executed with:

```shell
idem state <file_path>/update_my_resource_group_state.sls
```
In this example:

```shell
idem state update_my_resource_group_state.sls
```
After that you will see Idem appending our tag information to meet our new intentention and state.


 {{< /tab >}}

  {{< tab "Absent" >}}

Once you don't need a resource, you can completely delete it by using the state directive [absent](Getting-Started/Basic-Commands/), which instructs Idem to <b>remove</b> an existing resource.

Let's delete an existing Azure Resource Group, in order to do that, we craft the <b>delete_my_resource_group_state.sls:</b> file with the following contents:

```yaml
<Your Azure Resource Group Name>:
  azure.resource_management.resource_groups.absent:
  - resource_group_name: <Your Azure Resource Group Name>
  - parameters:
    location: <Azure Region>
```

Then <b>State SLS</b> file can be executed with:

```shell
idem state <file_path>/delete_my_resource_group_state.sls
```
In this example:

```shell
idem state delete_my_resource_group_state.sls
```
After that you will see Idem removing the resource group to meet our new intentention and state.


 {{< /tab >}}

{{< tab "Describe 2 State" >}}
 
You probably noticed that when you execute a [describe](/Use-Cases/Describe/) operation fron CLI, the output resembles the same  kind of data we have defined in SLS states examples, that is because it is exactly the same, meaning, you don't need to start from scratch to create, modify or even delete resources, you can simply issue the [describe](/Use-Cases/Describe/) operation and save the output into an SLS file then "tweak" accordingly to meet your intention.

Let's say we want to add a new Azure resource group, for that I could simply describe an existing "Azure Resource Group Name" and save the output into a SLS file.

```shell
 idem describe azure.resource_management.resource_groups --filter="[?resource[?vm_name=='<Existing Azure Resource Group Name>']]" >> my_other resource_group_state.sls
```

Then we can edit the file, removing any property we don't need and updating the relevant ones, such as the name or the region, etc.<br>
Please note, that when editing, you always need to include the minimum parameters to create any given resource (Azure Provider Documentation and even Azure Cloud API documentation provides details in this regard).

 ```yaml
<New Azure Resource Group Name>:
  azure.resource_management.resource_groups.present:
  - resource_group_name: <New Azure Resource Group Name>
  - parameters:
    location: <Azure Region>
    tags: {"createdWith": "idem"}
```

Please make sure to indicate the state directive [present](Getting-Started/Basic-Commands/), for instructing idem to <b>create</b> a new resource group in Azure.

Then <b>State SLS</b> file can be executed with:

```shell
idem state <file_path>/my_other resource_group_state.sls
```
In this example:

```shell
idem state my_other resource_group_state.sls
```
After that you will see Idem creating a new resource to meet our new intentention and state.

{{< /tab >}}

{{< tab "Basic End to End Azure Virtual Machine " >}}
This example showcases how to create a basic Azure Virtual Machine, we will create the Resource Group, Re-Use an existing NIC and create the Azure Virtual Machine resource then we could update the metadata:

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

{{< /tab >}}


 {{< /tabs >}}
