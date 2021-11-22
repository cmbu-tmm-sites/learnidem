---
title: "Cloud Providers"
weight: 20
---

For Installing Cloud Providers you can use "pip" tool :

{{< tabs "install" >}}
{{< tab "idem-aws" >}}

For Installing "idem-aws" Cloud Provider:

```shell
pip3 install idem-aws 
```

You can verify installation with "pip"

```shell
pip3 list | grep idem-aws
```

{{< /tab >}}
{{< tab "idem-azure" >}}

For Installing "idem-azure-auto" Cloud Provider:

```shell
pip3 install idem-azure-auto
```

You can verify installation with "pip"

```shell
pip3 list | grep idem-azure-auto
```

<SPAN STYLE="font-size:18.0pt">Current Supported Resources states in "idem-azure-auto"</SPAN>
 <ul>
<li><p><b>Compute Service:</b></p> 
    virtual_machines</li>
<li><p><b>Resource Management:</b></p>
    resource_groups</li>
<li><p><b>Virtual networks Service:</b></p>
    network_interfaces<br>
    network_security_groups<br>
    public_ip_addresses<br> 
    security_rules<br>
    subnets<br>
    virtual_networks<br></li>
 </ul>

{{< /tab >}}
{{< /tabs >}}

Now you need to set up the credentials for your Idem Cloud Providers for [authentication](/Getting-Started/Authenticate/)

[You can find use case examples here](/Use-Cases/)