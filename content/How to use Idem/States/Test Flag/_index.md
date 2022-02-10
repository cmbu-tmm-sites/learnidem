---
title: "Test Flag"
weight: 40
---

Sometimes, specially with a [present](/How-to-use-Idem/States/Present/) , a [present update](/How-to-use-Idem/States/Present-Update/) or [absent](/How-to-use-Idem/States/Absent/) states, you would like to verify the changes that may happen before actually applying them

For that you can use the state flag <b>"test"</b>
```shell
  --test, -t            Set the idem run to execute in test mode. No changes
                        will be made, idem will only detect if changes will be
                        made in a real run.
```

As an example,  

```shell
idem state states/my_resource_group_state.sls -t
```

After that Idem will provide similar output, indicating that the resource "would" and the actual operation<br>
in this case, our state <b>would update</b> our Azure Resource Group named "moff-idem-01" with new meta-data if we decide to [enforce it](/) :

```shell
--------
      ID: moff-idem-01
Function: azure.resource_management.resource_groups.present
  Result: True
 Comment: Would update azure.resource_management.resource_groups with parameters: {'tags': {'createdWith': 'idem'}}
 Changes: None

```


 