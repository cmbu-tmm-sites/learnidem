---
title: "Authenticate"
weight: 30
---

## Managing Credentials

To perform the idem operations, we would require credentials of the environment almost always.
Idem suggests the following steps for passing credentials:

{{< tabs "install" >}}
<!--  tab "idem-aws"

Create a `credentials.yaml` file - the `default` profile will be used unless specified in the command or state file:

```yaml
aws:
  default:
    aws_access_key_id: <Your Access Key ID>
    aws_secret_access_key: <Your Secret Access Key>
    region_name: <AWS Region>
```
 /tab  -->
{{< tab "idem-azure-auto" >}}

Create a `credentials.yaml` file - the `default` profile will be used unless specified in the command or state file:

```yaml
azure:
   default:
      client_id: "<Your Client ID>"
      secret: "<Your Secret key>"
      subscription_id: "<Your Subcription Key ID>"
      tenant: "<Your Tenant Key ID>"
```

{{< /tab >}}
{{< /tabs >}}


Encrypt the credentials file using the idem encrypt command, this creates a fernet file and outputs an encryption key:

```shell
idem encrypt /path/to/credentials.yaml
```
Please note that the output string from the command above is the key Idem uses for accessing the encrypted credentials fernet file

```shell
<output encryption key>
```

Example:
```shell
DvBsYojgU5gy51CecvhhC7Ywrsq9NL3CSg_XcLMKKn4=
```

Before start using Idem, you need to make sure your session includes the <b>ACCT_KEY</b> & <b>ACCT_FILE</b> OS environment varialbles, otherwise export the encryption key and path to the fernet file as an OS environment variable for your session:

```shell
export ACCT_KEY=<output encryption key>
export ACCT_FILE=/path/to/credentials.yaml.fernet
```
Example:
```shell
export ACCT_KEY=DvBsYojgU5gy51CecvhhC7Ywrsq9NL3CSg_XcLMKKn4=
export ACCT_FILE=/home/demouser/environments/credentials.yaml.fernet
```

Idem securely retrieves the credentials combining those OS environment variables before executing states.<br> 
You can also pass those values as parameters of the [Idem cli](Getting-Started/Basic-Commands/) `--acct-key` and `--acct-file` options while applying the states.

Example:
```shell
idem describe azure.virtual_networks.network_interfaces --acct-key DvBsYojgU5gy51CecvhhC7Ywrsq9NL3CSg_XcLMKKn4= --acct-file /home/demouser/environments/credentials.yaml.fernet
```
## Credentials and Profiles

Credentials can be grouped by Plug-Ins (azure, aws, etc ) and Profiles (within each Plug-Ins section),<br> you can define multiple Plug-Ins and Profiles in a single configuration file (e.g. default, dev, staging, etc).<br> It is recommended to always include/define the "default" profile.<br>

E.g. credentials.yaml file with multiple account profiles.

```yaml
azure:
   default:
      client_id: "<Your Client ID>"
      secret: "<Your Secret key>"
      subscription_id: "<Your Subcription Key ID>"
      tenant: "<Your Tenant Key ID>"
   tmm:
      client_id: "<Your Client ID>"
      secret: "<Your Secret key>"
      subscription_id: "<Your Subcription Key ID>"
      tenant: "<Your Tenant Key ID>"
aws:
  default:
    aws_access_key_id: <Your Access Key ID>
    aws_secret_access_key: <Your Secret Access Key>
    region_name: <AWS Region>
```

With Idem, You use the account profile flag `--acct-profile` to indicate which specific profile and associated set of credentials to be used. Please note that if you don't specific the account profile flag `--acct-profile`, the default profile is going to be always used (if profile default is defined at the configuration yaml)<br>

The following command will instruct [Idem](/Getting-Started/Install-Idem/) to use the Azure credentials associated to the "default" profile

```shell
idem describe azure.compute.virtual_machines 
```

The following command will instruct [Idem](/Getting-Started/Install-Idem/) to use the Azure credentials associated to the "tmm" profile  ( per credentials.yaml file from lines above)

```shell
idem describe azure.compute.virtual_machines --acct-profile tmm
```

[Describe](/Use-Cases/Describe/) Azure VM Machines within the "tmm" profile example:
<script id="asciicast-SiXcq1OmVkca57LNf2m6N4wWK" src="https://asciinema.org/a/SiXcq1OmVkca57LNf2m6N4wWK.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>