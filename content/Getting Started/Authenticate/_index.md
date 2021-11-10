---
title: "Authenticate"
weight: 20
---

## Managing Credentials

To perform the idem operations, we would require credentials of the environment almost always.
Idem suggests the following steps for passing credentials:

{{< tabs "install" >}}
{{< tab "idem-aws" >}}

Create a `credentials.yaml` file - the `default` profile will be used unless specified in the command or state file:

```yaml
aws:
  default:
    aws_access_key_id: <Your Access Key ID>
    aws_secret_access_key: <Your Secret Access Key>
    region_name: <AWS Region>
```
{{< /tab >}}
{{< tab "idem-azure" >}}

{{< /tab >}}
{{< /tabs >}}

Encrypt the credentials file using the idem encrypt command, this creates a fernet file and outputs an encryption key:

```shell
idem encrypt /path/to/credentials.yaml
```
Please note that the output string from that command is your `ACCT_KEY`

To use the encrypted credentials file, export the encryption key and path to the fernet file as an environment variable:
```shell
export ACCT_KEY=gBklLTlVxiGT1gtliGNldMThiuEA5Rxlwon6g5aJhlg=
export ACCT_FILE=/path/to/credentials.yaml.fernet
```
Idem retrieves the credentials from these variables while executing states. These values can also be passed as `--acct-key` and `--acct-file` options while applying the states.

Credentials can be grouped using Profiles and you can define multiple profiles in same file (e.g. default, dev, staging, etc).