---
title: "Idem AWS Plug-In"
weight: 20
---

<b>Supported Resources</b> provides a list of AWS Resources supported by the latest Idem AWS Plug-Ins<br>
<b>Install the Plug-Ins</b> section provides instructions for installing the Idem AWS Plug-Ins

{{< tabs "Operations" >}}
{{< tab "Supported Resources" >}}

<SPAN STYLE="font-size:18.0pt">Current Supported Resources states in "idem-aws"</SPAN>
 <ul>
 <li><p><b>ec2:</b></p>
     elastic_ip</br>
     flow_log<br>
     instance<br>
     internet_gateway<br>
     nat_gateway<br>
     route_table<br>
     spot_instance<br>
     subnet<br>
     transit_gateway<br>
     transit_gateway_vpc_attachment<br>
     vpc</li>
<li><p><b>iam:</b></p>
    instance_profile<br>
    policy<br>
    role<br>
    role_policy<br>
    role_policy_attachment<br>
    user</li>
<li><p><b>kms:</b></p>
    key</li>
<li><p><b>organizations:</b></p>
    organization<br>
    organization_unit</li>
<li><p><b>s3:</b></p>
    bucket</li>
 </ul>

{{< /tab >}}
{{< tab "Install the Plug-Ins" >}}
For Installing the latest "idem-AWS" Cloud Plug-Ins

```shell
pip install idem-aws
```

or you can install / upgrade to an specific release

```shell
pip install idem-aws==0.17.0
```
Please note this plug-in requires [Python 3.7+](https://www.python.org/downloads/) and [idem](Getting-Started/Install-Idem/) 17.0.1

You can verify installation with [pip](https://pypi.org/project/pip/)

```shell
pip list | grep idem-aws
```

And obtain more details, including version and required dependencies

```shell
pip show idem-aws
```

{{< /tab >}}

{{< tab "Container Bundle" >}}
You can pull the container image bundle that includes the idem + idem-aws plug-in

```shell
# GitHub Container Repository
docker pull ghcr.io/vmwarecmbutmm/idem-container:aws-latest

```

You can also learn how to launch it and gain access to the Dockerfile at [VMwareCMBUTMM/idem-container-aws](https://github.com/VMwareCMBUTMM/idem-container/tree/main/idem-aws)


{{< /tabs >}}

After Installing the Plug-Ins you can now set up the credentials needed for the Plug-Ins to [authenticate](/Getting-Started/Authenticate/)<br>
Then you could follow a few [use case examples ](/How-to-use-Idem/Use-Cases/)
