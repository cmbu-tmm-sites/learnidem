---
title: "Install Idem"
weight: 10
---

Idem can be installed in different ways in multiple Operating System and container


{{< tabs "install" >}}
{{< tab "MacOS" >}} 

Installation instructions for MacOS using [Homebrew](https://brew.sh/):
```shell
# Install pyenv and pyenv-virtualenv
brew install pyenv pyenv-virtualenv
# Install Python 3.9.0
pyenv install 3.9.0
# Create a virtualenv called "salt-idem" using Python 3.9.0
virtualenv 3.9.0 salt-idem
# Activate the virtualenv
pyenv local salt-idem
# Update Python package manager
python -m pip install --upgrade pip
# Install Idem (you can also include providers, in this case the AWS Cloud Provider for Idem)
pip install idem idem-aws
```
{{< /tab >}}
{{< tab "Ubuntu" >}}
Ubuntu 18.04 & Python 3.6.9:

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
# Install Idem ( you can also include providers, in this case the AWS Cloud Provider for Idem)
pip3 install idem idem-aws 
# Verify Version
idem --version
```
{{< /tab >}}

{{< tab "Windows" >}}

Download and install [Windows for Python](https://www.python.org/downloads/windows/), making sure the python and pip executables are included in the PATH.

```shell
# Upgrade to the latest PIP to meet the Crypto requirements
python3 -m pip install --upgrade pip
# Install Idem ( you can also include providers, in this case the AWS Cloud Provider for Idem)
pip3 install idem idem-aws 
# Verify Version
idem --version
```
{{< /tab >}}

{{< /tabs >}}

At this point you can install [Cloud Providers](/Getting-Started/Install-Idem/Cloud-Providers/) then set up the credentials to [authenticate](/Getting-Started/Authenticate/) with the Idem Cloud Providers.