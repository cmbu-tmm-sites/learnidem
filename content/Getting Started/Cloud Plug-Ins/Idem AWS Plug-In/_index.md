---
title: "Idem AWS Plug-In"
weight: 20
---

The various states available for use in the Idem-AWS plugin are documented briefly on the [Idem AWS Plug-In States](states) page.<br />

{{< tabs "Installing" >}}
{{< tab "Installing the Idem AWS Plug-In" >}}
To install the latest "idem-AWS" Plug-In

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

{{< /tab >}}
{{< /tabs >}}

After Installing the Plug-In you can now set up the credentials needed for the Plug-In to [authenticate](/Getting-Started/Authenticate/) to AWS.<br />
Then you could follow a few [use case examples](/How-to-use-Idem/Use-Cases/).