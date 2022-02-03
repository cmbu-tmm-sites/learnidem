---
title: "End to End Azure VM"
weight: 65
---

This example showcases how to create, combine and reference multiple [Idem Azure Provider Resources](/Getting-Started/Cloud-Providers/):<br>
<ul>
 <li><p><b>Resource Group</b></p></li>
 <li><p><b>Virtual Network</b></p></li>
 <li><p><b>Subnet</b></p></li>
 <li><p><b>Public IP</b></p></li>
 <li><p><b>Security Groups</b></p></li>
 <li><p><b>Network Interface</b></p></li>
 <li><p><b>Virtual Machine</b></p></li>
 </ul>
<br>
At the end we will have created an Azure Virtual Machine ( which includes attributes such as SSH Key authentication and Cloud-Init ).

Let's create a new SLS file named "goapp.sls"<br>

First let's add a <b>Resource Group</b>
```yaml
# Resource Group
moff-idem-rg-01:
  azure.resource_management.resource_groups.present:
  - resource_group_name: moff-idem-rg-01
  - parameters:
      location: centralus
      tags: {}
```
Then a <b>Virtual Network</b>, please note that we can reference our <b>Resource Group</b> by providing only its name

# Virtual Network
```yaml
vNet1-Idem:
  azure.virtual_networks.virtual_networks.present:
  - resource_group_name: moff-idem-rg-01
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

Now we can define a <b>Subnet</b>, just as before we can reference our <b>Resource Group</b> & <b>Virtual Network</b> by providing only their name

# Subnet
```yaml
moff-idem-subnet-1:
  azure.virtual_networks.subnets.present:
  - resource_group_name: moff-idem-rg-01
  - virtual_network_name: vNet1-Idem
  - subnet_name: moff-idem-subnet-1
  - parameters:
      properties:
        "addressPrefix": "10.12.13.0/27"
      location: centralus
```

Something similar happens for a <b>Public IP</b>, we reference our <b>Resource Group</b> by providing only its name

# Public IP
```yaml
moff-idem-pub-ip:
  azure.virtual_networks.public_ip_addresses.present:
  - resource_group_name: moff-idem-rg-01
  - public_ip_address_name: moff-idem-pub-ip
  - parameters:
      location: centralus
      properties:
        publicIPAllocationMethod: Dynamic
        idleTimeoutInMinutes: 10
        publicIPAddressVersion: IPv4
```

Same story for a <b>Security Groups</b>, we reference our <b>Resource Group</b> by providing only its name, however notice that we include a [force_update](/Use-Cases/Force-Update/) option, so we could update <b>Security Groups</b> as needed

# Security Groups
```yaml
moff-idem-sg-1:
  azure.virtual_networks.network_security_groups.present:
  - force_update: True
  - resource_group_name: moff-idem-rg-01
  - network_security_group_name: moff-idem-sg-1
  - parameters:
      location: centralus
      properties:
        securityRules:
        - name: moff-idem-sg-rule-1
          properties:
            protocol: "*"
            sourceAddressPrefix: "*"
            destinationAddressPrefix: "*"
            access: "Allow"
            destinationPortRange: "22"
            sourcePortRange: "*"
            priority: 130
            direction: "Inbound"
        - name: moff-idem-sg-rule-2
          properties:
            protocol: "*"
            sourceAddressPrefix: "*"
            destinationAddressPrefix: "*"
            access: "Allow"
            destinationPortRange: "80"
            sourcePortRange: "*"
            priority: 150
            direction: "Inbound"
```

Now, in the case of <b>Network Interfaces</b>, we need to reference our <b>Resource Group</b> but for the <b>Security Groups</b>, <b>Public IP</b> & <b>Subnet</b>, the "ID" and Azure Resource URL is needed, however you can see the Azure Resource URL follows a very well defined structure:

```shell
 /subscriptions/<your Azure Subscription ID>/<resource group>/<name of the resource group>/providers/<Microsoft Provider Type>/<name of the resource>
```

Example for <b>Public IP</b>:

```shell
/subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-rg-01/providers/Microsoft.Network/publicIPAddresses/moff-idem-pub-ip
```
You can learn more of Azure Resource URL in Azure API Doc.

# Network Interfaces
```yaml
moff-idem-nic-01:
  azure.virtual_networks.network_interfaces.present:
  - resource_group_name: moff-idem-rg-01
  - network_interface_name: moff-idem-nic-01
  - parameters:
      location: centralus
      properties:
        enableAcceleratedNetworking: false
        hostedWorkloads: []
        networkSecurityGroup:
          id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-rg-01/providers/Microsoft.Network/networkSecurityGroups/moff-idem-sg-1
        ipConfigurations:
          - name: moff-idem-nic-01-ipconfig1
            properties:
              primary: true
              publicIPAddress:
                id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-rg-01/providers/Microsoft.Network/publicIPAddresses/moff-idem-pub-ip
              subnet:
                id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-rg-01/providers/Microsoft.Network/virtualNetworks/vNet1-Idem/subnets/moff-idem-subnet-1
```

At this point we can add our <b>Virtual Machine</b>, in the case only the <b>Network Interfaces</b> ID is needed, following same logic as before

# Create VM
```yaml
Development-idem-015:
  azure.compute.virtual_machines.present:
  - resource_group_name: moff-idem-rg-01
  - vm_name: Development-idem-015
  - parameters:
      location: centralus
      name: Development-idem-015
      properties:
        hardwareProfile:
          vmSize: Standard_A5
        networkProfile:
          networkInterfaces:
          - id: /subscriptions/23a8cee7-a1e4-4bb3-aff9-6898b4ee6fde/resourceGroups/moff-idem-rg-01/providers/Microsoft.Network/networkInterfaces/moff-idem-nic-01
            properties:
              primary: true
        osProfile:
          adminUsername: demouser
          allowExtensionOperations: true
          computerName: Development-idem-015
          linuxConfiguration:
            ssh: 
              publicKeys:  
                - keyData: "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDFLX/56zSvZawvw3A0hfSVFPMPPeP8ZXeQ91+YdqCSyMUxgexQPpSEZIPbwodM0aAXMg227JuGji+JQlnXxCy1UDcpsGYnGsr3j3qrazrfp7tSBY5vTuHdmE4ZAEyoUFcEGPbDCzn82RI4PlF7508I32OPtr7HiZYeU+uP18snkvdXqEB8OCoSMy36lE806w+e3HVT/bMoj+wSAzjqju5Eqeg96IZOoeqpWQyTeLdaMqVdlQcSKcYnnKCIMaHTehZjtOHRte3EtSnbdiwCPnFno9EzHdCIde4KT+dFG9B2Goy2z10MkxFbR6IDxdbFxg4+siHNnHfbd/ILQuqN ubuntu"
                  path: /home/demouser/.ssh/authorized_keys
            disablePasswordAuthentication: true 
            patchSettings:
              assessmentMode: ImageDefault
              patchMode: ImageDefault
            provisionVMAgent: true
          secrets: []
        userData: "RXhhbXBsZSBVc2VyRGF0YQ==" 
        storageProfile:
          dataDisks: []
          imageReference:
            exactVersion: 18.04.201804262
            offer: UbuntuServer
            publisher: Canonical
            sku: 18.04-LTS
            version: 18.04.201804262
          osDisk:
            caching: None
            createOption: FromImage
            deleteOption: Detach
            diskSizeGB: 30
            managedDisk:
              storageAccountType: Standard_LRS
            name: Development-idem-015-boot-disk
            osType: Linux
      tags:
        blueprintname: goapp-idem
        deployment: Idem-Discover
        project: development
        requestedby: hernandezf@vmware.com
```

Save your file and we are ready for deployment, please note that all the resources have the [Idem Present Directive](/Getting-Started/Basic-Commands/) and that we must include the [reconcilier flag](/Use-Cases/reconciler-flag/), so [Idem](/) can loop for all the dependencies resources to be created.

```shell
idem state my_resource_group_state.sls --reconciler=basic
```

You can then use [Idem describe](/Use-Cases/Describe/) to validate all your resources are created (BTW, it would be a good idea to use your own SSH public Key, this one is fake)