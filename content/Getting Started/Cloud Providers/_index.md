---
title: "Cloud Providers"
weight: 20
---

For Installing Cloud Providers you can use "pip" tool :

{{< tabs "install" >}}
{{< tab "idem-aws" >}}

For Installing "idem-aws" Cloud Provider

```shell
pip3 install idem-aws
```

You can verify installation with "pip"

```shell
pip3 list | grep idem-aws
```

{{< /tab >}}
{{< tab "idem-azure-auto" >}}

For Installing the latest "idem-azure-auto" Cloud Provider

```shell
pip3 install idem-azure-auto
```

or you can install / upgrade to an specific release

```shell
pip install idem-azure-auto==0.0.2
```
Please note that the provider may have version dependencies, such as "idem-aiohttp" & "idem" itself but the "pip" install will update them as well.

You can verify installation with "pip"

```shell
pip3 list | grep idem-azure-auto
```

<SPAN STYLE="font-size:18.0pt">Current Supported Resources states in "idem-azure-auto"</SPAN>
 <ul>
 <li><p><b>authorization:</b></p>
     role_assignment</br>
     role_definition</li>
<li><p><b>compute:</b></p>
    virtual_machines</li>
<li><p><b>resource_management:</b></p>
    resource_groups</li>
<li><p><b>storage_resource_provider:</b></p>
    storage_accounts</li>    
<li><p><b>virtual_networks_service:</b></p>
    nat_gateways<br>
    network_interfaces<br>
    network_security_groups<br>
    public_ip_addresses<br>
    route_tables<br>
    routes<br>
    security_rules<br>
    subnets<br>
    virtual_networks<br></li>
 </ul>

{{< /tab >}}
{{< /tabs >}}

Now you need to set up the credentials for your Idem Cloud Providers for [authentication](/Getting-Started/Authenticate/)

[You can find use case examples here](/Use-Cases/)
