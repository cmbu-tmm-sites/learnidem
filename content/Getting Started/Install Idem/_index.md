---
title: "Install Idem"
weight: 10
---

Idem can be installed in different ways in multiple Operating System and in Containers, also as a [single binary](https://repo.idemproject.io/)<br>
Idem is written in [Python](https://www.python.org/) and distributed on [Pypi](https://pypi.org/project/pip/), so it is just a quick pip install away<br>
[Python 3.6+](https://www.python.org/downloads/) is required as prerequisite for version 15.0.X, however newer idem versions may require also newer [Python 3.7+](https://www.python.org/downloads/) releases.<br>

You can also pull the container image bundle that includes the idem + the selected plug-in, this is an excellent alternative to avoid system dependencies errors. More information under each [Cloud Plug-Ins](/Getting-Started/Cloud-Plug-Ins/) install instructions.


{{< tabs "install" >}}

{{< tab "macOS" >}} 

Idem and providers at the moment are version related for idem-azure-auto v0.0.3 is recommended idem v15.0.0 <br>
macOS 12.1 & [Python 3.7.3](https://www.python.org/downloads/release/python-373/):

```shell
# Optional but recommended, you can create a Virtual Enviroment  
mkdir environments
cd environments
python3 -m venv my_idem_env
source my_idem_env/bin/activate
# Upgrade to the latest PIP to meet the Crypto requirements
python3 -m pip install --upgrade pip
# Install Idem 
pip3 install idem
# Install Specific Idem Version
pip3 install idem==15.0.0
# Verify Version
idem --version
```
<p><b>Idem installation - macOS</b></p>
<script id="asciicast-8BqTYhsLKbJNhLEK2z1GnpAVP" src="https://asciinema.org/a/8BqTYhsLKbJNhLEK2z1GnpAVP.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>

{{< /tab >}}

{{< tab "Windows" >}}

Download and install [Windows for Python](https://www.python.org/downloads/windows/), making sure the python and pip executables are included in the PATH.

```shell
# Upgrade to the latest PIP to meet the Crypto requirements
python3 -m pip install --upgrade pip
# Install Idem 
pip3 install idem 
# Verify Version
idem --version
```
{{< /tab >}}

{{< tab "Ubuntu" >}}
Idem and providers at the moment are version related for idem-azure-auto v0.0.3 is recommended idem v15.0.1<br>
Ubuntu 18.04 & [Python 3.6.9](https://www.python.org/downloads/release/python-369/):

```shell
# Install Base Packages
sudo apt update && sudo apt -y upgrade
sudo apt install -y python3-pip build-essential libssl-dev libffi-dev python-dev python3-venv
# Optional, you can create a Virtual Enviroment  
mkdir environments
cd environments
python3 -m venv my_idem_env
source my_idem_env/bin/activate
# Upgrade to the latest PIP to meet the Crypto requirements
python3 -m pip install --upgrade pip
# Install Idem 
pip3 install idem 
# Install Specific Idem Version
pip3 install idem==15.0.0
# Verify Version
idem --version
```
<p><b>Idem installation - Ubuntu</b></p>
<script id="asciicast-ZlpSV4Dd1vMneJ8j8GRwo1a4R" src="https://asciinema.org/a/ZlpSV4Dd1vMneJ8j8GRwo1a4R.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>

{{< /tab >}}

{{< /tabs >}}

At this point you can install [Cloud Providers](/Getting-Started/Cloud-Providers/) then set up the credentials to [authenticate](/Getting-Started/Authenticate/) with the Idem Cloud Providers.


