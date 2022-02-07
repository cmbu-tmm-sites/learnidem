---
title: "Present Update"
weight: 25
---

We can also use the state directive [present](Getting-Started/Basic-Commands/), for instructing Idem to <b>update</b> an existing resource's properties or behavior, e.g. updating specific resource parameters such as : location, tags, addressprefix, etc. 

Please note that due to the nature of some resources, the only way to update parameters or behaviors is by re-creating them, in those scenarios you can include the [force_update: True](/Use-Cases/SLS-States/Present-Update/Force-Update/) flag for enforcing the new present goal state.

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
idem state states/update_my_resource_group_state.sls
```
After that you will see Idem appending our tag information to meet our new intentention and state.
```shell
--------
      ID: moff-idem-01
Function: azure.resource_management.resource_groups.present
  Result: True
 Comment: OK
 Changes: old:
    ----------
    tags:
        ----------
new:
    ----------
    tags:
        ----------
        createdWith:
            idem

```
You can further verify by the [idem describe](/Use-Cases/Describe/) and [filter](/Use-Cases/Filter-flag/) by the resource group name.
 
```shell
idem describe azure.resource_management.resource_groups  --filter="[?resource[?resource_group_name=='moff-idem-01']]"
```

State Present - Update (tags):
<script id="asciicast-U0TBeuu6e5w8oWVoIhXe6q1cx" src="https://asciinema.org/a/U0TBeuu6e5w8oWVoIhXe6q1cx.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>
