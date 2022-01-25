---
title: "Basic Commands"
weight: 40
---

Idem provides the [idem cli](/Getting-Started/Install-Idem/) which allows to describe resources but also invoke states.<br>
[Idem states](/Use-Cases/SLS-States/) are used to make sure resources are in a desired state. The desired state of a resource can be specified in SLS file.

{{< tabs "commands" >}}

{{< tab "CLI Commands" >}}

<b>encrypt</b><br>
     Use the acct subsystem to encrypt data, e.g. [Encrypt the credentials file](/Getting-Started/Authenticate/)

```shell
idem encrypt /path/to/credentials.yaml
```

<b>decrypt</b><br>
     Use the acct subsystem to decrypt data, e.g. an existing encrypted credentials file (*.fernet)

```shell
idem decrypt /path/to/credentials_test.yaml.fernet
```

<b>describe</b><br>
    Commands to run description routines, e.g. [Listing and obtaining existing VMs details](/Use-Cases/Describe/)

```shell
idem describe azure.compute.virtual_machines
```

<b>state</b><br>
    Commands to run idempotent states, e.g. [create, update, and in general manage your resources](/Use-Cases/SLS-States/) 

```shell
idem state vm_moff_present.sls
```

You will use mostly a combination of <b>describe</b> (Discover status and helper for crafting a state file to update resource) and <b>state</b> commands (for managing the resources states), <br> let's take a closer look to <b>state</b> operations.

<b>exec</b><br>
    Commands to run execution routines, normally used internally in idem code
{{< /tab >}}

{{< tab "States" >}}
 
 <ul>
<li><p><b>Present State</b></p> 
    makes sure a resource exists in a desired state. If a resource does not exist, running present will create the resource on the provider. If a resource exists, running present will update the resource on the provider. (Only the values that the Cloud Provider REST API supports can be updated.)</li>
<li><p><b>Absent State</b></p>
    makes sure a resource does not exist. If a resource exits, running absent will delete the resource. If a resource does not exist, running absent is a no-operation.</li>
<li><p><b>Describe State</b></p>
    lists all the current resources of the same resource type under the <b>subscription id</b> specified in the credential profile.</li>
 </ul>

You can learn and learn more about each state at the <b>[use cases](/Use-Cases/)</b>


{{< /tab >}}


 {{< /tabs >}}