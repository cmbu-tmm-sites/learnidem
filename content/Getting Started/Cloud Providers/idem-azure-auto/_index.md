---
title: "Idem Azure Auto Provider"
weight: 10
---

<b>Supported Resources</b> provides a list of Azure Resources supported by the latest Idem Azure Provider<br>
<b>Install the Provider</b> section provides instructions for installing the Idem Azure Provider

{{< tabs "Operations" >}}
{{< tab "Supported Resources" >}}

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
<li><p><b>policy:</b></p>
    policy_assignments</li>    
<li><p><b>virtual_networks:</b></p>
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
{{< tab "Install the Provider" >}}
For Installing the latest "idem-azure-auto" Cloud Provider

```shell
pip install idem-azure-auto
```

or you can install / upgrade to an specific release

```shell
pip install idem-azure-auto==0.0.3
```
Please note that the provider may have version dependencies, such as "idem-aiohttp" but [pip](https://pypi.org/project/pip/) install will update them most of the times.
There are also requirements applying to [idem](Getting-Started/Install-Idem/) and Python, e.g. idem version 16.0+ requires [Python 3.7+](https://www.python.org/downloads/) however idem-azure-auto==0.0.3 is only certified up to idem version 15.0.1.

You can verify installation with [pip](https://pypi.org/project/pip/)

```shell
pip list | grep idem-azure-auto
```

And obtain more details, including version and required dependencies

```shell
pip show idem-azure-auto
```
<p><b>Idem Azure Provider Install </b></p>
<script id="asciicast-nVpeQTcSDh36o4UwfFp1tHrnM" src="https://asciinema.org/a/nVpeQTcSDh36o4UwfFp1tHrnM.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>


{{< /tab >}}
{{< /tabs >}}

After Installing the provider you can now set up the credentials needed for the provider to [authenticate](/Getting-Started/Authenticate/)<br>
Then you could follow a few [use case examples ](/Use-Cases/)
