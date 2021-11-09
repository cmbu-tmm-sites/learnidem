---
title: "Authenticate"
weight: 20
---

Managing Credentials

To perform the idem operations, we would require credentials of the environment almost always.
Idem suggests the following steps for passing credentials:

Create a credentials.yml file and define the credentials of environment. The credentials can be grouped using profiles and we can define multiple profiles in same file (e.g. dev, staging, etc).
Use acct encrypt command to generate an encrypted fernet file of credentials.yml. The command also prints the key that was used for encryption.
Set ACCT_KEY and ACCT_FILE environment variables with key and path to fernet file respectively. Idem retrieves the credentials from these variables while executing states. These values can also be passed as acct-key and acct-file options while applying the states.