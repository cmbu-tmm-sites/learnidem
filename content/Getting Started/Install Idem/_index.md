---
title: "Install Idem"
weight: 10
---

Idem can be installed in different ways in multiple Operating System and container

MACOS:

UBUNTU ( 18.04 & Python 3.6.9 ):

    - Install Base Packages
        sudo apt update && sudo apt -y upgrade
        sudo apt install -y python3-pip build-essential libssl-dev libffi-dev python-dev python3-venv

    - Optional, you can create a Virtual Enviroment  
        mkdir environments
        cd environments
        python3 -m venv my_idem_env
        source my_idem_env/bin/activate

    - Upgrade to the latest PIP to meet the Crypto requirements
        python3 -m pip install --upgrade pip

    - Install Idem ( you can also include providers, in this case the AWS Cloud Provider for Idem)
        pip3 install idem idem-aws 

    - Verify Version

        idem --version
    
At this point you need to set up the credentials to [authenticate](/Getting-Started/Authenticate/)