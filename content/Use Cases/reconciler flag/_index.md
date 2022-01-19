---
title: "Reconcilier Flag"
weight: 25
---
You can lists all the current Azure resources of the same resource type under the subscription id specified in the credential profile.<br>
Make sure to export the encryption key and path to the fernet file as an environment variable as described in the [authentication section](/Getting-Started/Authenticate/) before trying the commands below

{{< tabs "usecases" >}}
{{< tab "Describe Azure Resources" >}}

We will use [describe](/Getting-Started/Basic-Commands/) directive and the specific Azure Resource 

```shell
idem describe azure.[ supported Azure State].[Azure Resource] 
```

Example, if we want to list existing VMs

```shell
idem describe azure.compute.virtual_machines
```

or

if we want to list existing Virtual Networks

```shell
idem describe azure.virtual_networks.virtual_networks
```

{{< /tab >}}
 {{< /tabs >}}
