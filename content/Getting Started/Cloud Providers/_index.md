---
title: "Cloud Providers"
weight: 20
---

For Installing Cloud Providers you can use Python Package Installer [pip](https://pypi.org/project/pip/)" tool :

{{< tabs "install" >}}
<!--  tab "idem-aws" 

For Installing "idem-aws" Cloud Provider

```shell
pip3 install idem-aws
```

You can verify installation with "pip"

```shell
pip3 list | grep idem-aws
```

 /tab  -->
{{< tab "idem-azure-auto" >}}


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
<p><b>Idem Azure Provider Install - Ubuntu</b></p>
<script id="asciicast-nVpeQTcSDh36o4UwfFp1tHrnM" src="https://asciinema.org/a/nVpeQTcSDh36o4UwfFp1tHrnM.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>


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
{{< /tabs >}}

Now you need to set up the credentials for your Idem Cloud Providers for [authentication](/Getting-Started/Authenticate/)<br>
Then you could follow a few [use case examples ](/Use-Cases/)
