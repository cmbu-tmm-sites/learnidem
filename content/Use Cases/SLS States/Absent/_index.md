---
title: "Absent"
weight: 35
---

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
idem state states/delete_my_resource_group_state.sls
```
After that you will see Idem removing the resource group to meet our new intentention and state.
```shell
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
        createdWith:
            idem
    properties:
        ----------
        provisioningState:
            Succeeded
```
You can further verify by the [idem describe](/Use-Cases/Describe/) and [filter](/Use-Cases/Filter-flag/) by the resource group name.
 
```shell
idem describe azure.resource_management.resource_groups  --filter="[?resource[?resource_group_name=='moff-idem-01']]"
```

State Absent - Delete:
<script id="asciicast-obpjtrBTOr3A4cDo5kNEdQLXt" src="https://asciinema.org/a/obpjtrBTOr3A4cDo5kNEdQLXt.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>

 