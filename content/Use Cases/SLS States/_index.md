---
title: "SLS States"
weight: 15
---

States can be defined as yaml definitions and captured in files with extension <b>SLS</b> <br>
Example: <b>my_resource_group_state.sls</b>

```yaml
# Resource Group
moff-idem-rg-01:
  azure.resource_management.resource_groups.present:
  - resource_group_name: moff-idem-rg-01
  - parameters:
      location: centralus
      tags: {}
```

SLS State file can exist anywhere in the file system, and they can be accessed by their relative location in the file system.<br>
Example: <b>/home/demouser/states/my_resource_group_state.sls</b>

If we wanted to execute the <b>State SLS</b>:

```shell
idem state <file_path>/<file name>.sls
```
In this example:

```shell
idem state ~/states/my_resource_group_state.sls
```

The following SLS use cases in this section, showcase how to use the available [idem describe](/Getting-Started/Basic-Commands/) states to work with Azure Resources.<br>
Make sure to export the encryption key and path to the fernet file as an environment variable as described in the authentication section before trying the examples in this section, follow the [Authenticate](/Getting-Started/Authenticate/) section for more details.



