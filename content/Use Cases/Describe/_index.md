---
title: "Describe command"
weight: 10
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
you can always reference those account profiles with the option `--acct-profile`

```shell
idem describe azure.compute.virtual_machines --acct-profile tmm
```
<script id="asciicast-SiXcq1OmVkca57LNf2m6N4wWK" src="https://asciinema.org/a/SiXcq1OmVkca57LNf2m6N4wWK.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>

or, if we want to list existing Virtual Networks

```shell
idem describe azure.virtual_networks.virtual_networks
```

you can always reference those account profiles with the option `--acct-profile`

```shell
idem describe azure.virtual_networks.virtual_networks --acct-profile tmm
```
<script id="asciicast-iolx0POfh5rLl4XBOxktnOlzl" src="https://asciinema.org/a/iolx0POfh5rLl4XBOxktnOlzl.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>


{{< /tab >}}
 {{< /tabs >}}

 You can describe specific results with the [Filter Flag](/Use-Cases/Filter-flag/)
