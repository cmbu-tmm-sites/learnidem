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
azurerm:
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
Please note that the output string from that command is your `ACCT_KEY`

To use the encrypted credentials file, export the encryption key and path to the fernet file as an environment variable:
```shell
export ACCT_KEY=<encryption key>
export ACCT_FILE=/path/to/credentials.yaml.fernet
```
Idem retrieves the credentials from these variables while executing states. These values can also be passed as `--acct-key` and `--acct-file` options while applying the states.

Credentials can be grouped using Profiles and you can define multiple profiles in same file (e.g. default, dev, staging, etc).

```yaml
azurerm:
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

Then you can reference those account profiles with the option `--acct-profile`

```shell
idem describe azure.compute.virtual_machines --acct-profile tmm
```
<script id="asciicast-SiXcq1OmVkca57LNf2m6N4wWK" src="https://asciinema.org/a/SiXcq1OmVkca57LNf2m6N4wWK.js" async theme="asciinema" data-autoplay="true" data-size="small" loop="true"></script>