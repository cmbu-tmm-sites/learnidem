---
title: "Idem Azure Plug-In"
weight: 20
---

The various states available for use in the Idem-Azure plugin are documented briefly on the [Idem Azure Plug-In States](states) page.<br />

{{< tabs "Installing" >}}
{{< tab "Installing the Idem Azure Plug-In" >}}
To install the latest "idem-azure" Plug-In

```shell
pip install idem-azure-auto
```

or you can install / upgrade to an specific release

```shell
pip install idem-azure-auto==0.0.3
```
Please note that the Plug-Ins may have version dependencies, such as "idem-aiohttp" but [pip](https://pypi.org/project/pip/) install will update them most of the times.
There are also requirements applying to [idem](Getting-Started/Install-Idem/) and Python, e.g. idem version 16.0+ requires [Python 3.7+](https://www.python.org/downloads/) however idem-azure-auto==0.0.3 is only certified up to idem version 15.0.1.

You can verify installation with [pip](https://pypi.org/project/pip/)

```shell
pip list | grep idem-azure-auto
```

And obtain more details, including version and required dependencies

```shell
pip show idem-azure-auto
```
<p><b>Idem Azure Plug-Ins Install </b></p>
<script id="asciicast-nVpeQTcSDh36o4UwfFp1tHrnM" src="https://asciinema.org/a/nVpeQTcSDh36o4UwfFp1tHrnM.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>


{{< /tab >}}
{{< tab "Container Bundle" >}}
You can pull the container image bundle that includes the idem + idem-azure-auto plug-in

```shell
# GitHub Container Repository
docker pull ghcr.io/vmwarecmbutmm/idem-container:azure-latest

```

You can also learn how to launch it and gain access to the Dockerfile at [VMwareCMBUTMM/idem-container](https://github.com/VMwareCMBUTMM/idem-container)


{{< /tab >}}
{{< /tabs >}}

After Installing the Plug-In you can now set up the credentials needed for the Plug-In to [authenticate](/Getting-Started/Authenticate/) to Azure.<br />
Then you could follow a few [use case examples](/How-to-use-Idem/Use-Cases/).
