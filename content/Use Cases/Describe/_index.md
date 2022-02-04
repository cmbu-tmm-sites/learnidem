---
title: "Describe command"
weight: 10
---
[idem describe](/Getting-Started/Basic-Commands/) directive lists all the current cloud provider resources of the same resource type under the subscription id specified in the credential profile.<br>
Make sure to export the encryption key and path to the fernet file as an OS environment variable as described in the [authentication section](/Getting-Started/Authenticate/) before trying the commands below:


You can use [describe](/Getting-Started/Basic-Commands/) directive below to discover and obtain details for an specific Resource (in this case Azure) 

```shell
idem describe [provider].[Resource States Group].[Resource] 
```
The <b>provider</b>, tells [idem](/Getting-Started/Basic-Commands/) which provider to access.<br>
The <b>Resource States Group</b>, organizes resources of the same type or topic, e.g. the Azure Compute or Azure Virtual_Networks.<br>
The <b>Resource</b>, indicates the specific resources type you want to work with, e.g. Virtual Machines or Network Interfaces, etc.<br>

Refer to [Idem Azure Provider](/Getting-Started/Cloud-Providers/idem-azure-auto/) for a list of supported <b>Resource States Group</b> & associated <b>Resources</b>

Example, if we want to list existing VMs, I will 

```shell
idem describe azure.compute.virtual_machines
```

<script id="asciicast-SiXcq1OmVkca57LNf2m6N4wWK" src="https://asciinema.org/a/SiXcq1OmVkca57LNf2m6N4wWK.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>

or, if we want to list existing Virtual Networks

```shell
idem describe azure.virtual_networks.virtual_networks
```

<script id="asciicast-iolx0POfh5rLl4XBOxktnOlzl" src="https://asciinema.org/a/iolx0POfh5rLl4XBOxktnOlzl.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>


 You can describe specific results with the [Filter Flag](/Use-Cases/Filter-flag/)
