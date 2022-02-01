---
title: "Filter Flag"
weight: 25
---
You can display specific Azure resources by <b>Filter</b> flag with the [describe](/Getting-Started/Basic-Commands/) command.<br>
Filter criteria is based on [JMESPath](https://jmespath.org/) whichis a query language for JSON. You can extract and transform elements from a JSON document.<br> 
Make sure to export the encryption key and path to the fernet file as an environment variable as described in the [authentication section](/Getting-Started/Authenticate/) before trying the commands below

{{< tabs "usecases" >}}
{{< tab "Filter Azure Resources" >}}

We will use [describe](/Getting-Started/Basic-Commands/) directive and the specific Azure Resource and the <b>Filter</b> flag to display specific resources. 

```shell
idem describe azure.[ supported Azure State].[Azure Resource]  --filter= "<JMESPath Query Language>"
```

Example, if we want to filter and specific existing Azure VM named "cmac-test-idem" under the account profile "tmm"

```shell
 idem describe azure.compute.virtual_machines --filter="[?resource[?vm_name=='cmac-test-idem']]" --acct-profile tmm
```

<script id="asciicast-DP3P74Vx5us1wveqRrKvsSQkd" src="https://asciinema.org/a/DP3P74Vx5us1wveqRrKvsSQkd.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>


or inspect the existing Azure Virtual Network named "vNet1-MoffCAS01" under the default account profile.

```shell
 idem describe azure.virtual_networks.virtual_networks  --filter="[?resource[?virtual_network_name=='vNet1-MoffCAS01']]"
```

<script id="asciicast-rRdpcMxQYbGy5Kc1RJGCYUj3A" src="https://asciinema.org/a/rRdpcMxQYbGy5Kc1RJGCYUj3A.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>


{{< /tab >}}
 {{< /tabs >}}
