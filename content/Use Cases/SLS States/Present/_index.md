---
title: "Present"
weight: 15
---

In order to create a new Azure Resource Group, we craft the <b>my_resource_group_state.sls:</b> file with the following contents:

```yaml
<Your Azure Resource Group Name>:
  azure.resource_management.resource_groups.present:
  - resource_group_name: <Your Azure Resource Group Name>
  - parameters:
    location: <Azure Region>
    tags: {}
```
We refer first to the Azure Idem Provider's Resource Group - "[azure.resource_management.resource_groups](/Getting-Started/Cloud-Providers/)" and we append the state directive [present](Getting-Started/Basic-Commands/), for instructing idem to <b>create</b> a new resource group in Azure.

Please note that you can map Azure REST API's  URI and Body Parameters to the state parameters, e.g. for the [Azure Resource Group](https://docs.microsoft.com/en-us/rest/api/resources/resource-groups/create-or-update) 

Then <b>State SLS</b> file can be executed with:

```shell
idem state <file_path>/my_resource_group_state.sls
```
In this example:

```shell
idem state states/my_resource_group_state.sls
```
After that you will see Idem appending our tag information to meet our new intentention and state.

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
You can further verify by the [idem describe](/Use-Cases/Describe/) and [filter](/Use-Cases/Filter-flag/) by the resource group name.

```shell
idem describe azure.resource_management.resource_groups  --filter="[?resource[?resource_group_name=='moff-idem-01']]"
```
State Present:
<script id="asciicast-kZUpVCaDPqkaXUIPP1z4XrG5J" src="https://asciinema.org/a/kZUpVCaDPqkaXUIPP1z4XrG5J.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>

The resource parameters in an SLS yaml file follow the exact structure as what’s in the [Azure REST API doc](https://docs.microsoft.com/en-us/rest/api/azure/).
<b>URI Parameters</b> should be specified in each case with “-” in front. All parameters of the API <b>request body</b> should be specified in exactly the same way as what’s in the [Azure REST API doc](https://docs.microsoft.com/en-us/rest/api/azure/). Please note that we can use the [state describe](Getting-Started/Basic-Commands/) for creating SLS files with most parameters.

 You can include multiple resources in a single SLS yaml file.
 Some resources may have dependencies among them, for that you include [ reconciler=basic flag ](/Use-Cases/reconciler-flag/), This allows Idem-azure-auto to run Idem state
with Idem's reconciliation loop.
