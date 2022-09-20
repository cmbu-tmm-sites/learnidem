---
title: "aws.iam.open_id_connect_provider"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an OpenID Connect identity provider (IdP) resource object in IAM.
Deleting an IAM OIDC provider resource does not update any roles that reference the provider as a principal in their
trust policies. Any attempt to assume a role that references a deleted provider fails.

Args:
    name(Text): The idem name for IAM OIDC provider.
    resource_id(Text): The Amazon Resource Name (ARN) of the IAM OpenID Connect provider resource object to delete.

Request Syntax:
    [oidc-resource-id]:
      aws.iam.open_id_connect_provider.absent:
      - name: 'string'
      - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        oidc-provider-1:
          aws.iam.open_id_connect_provider.absent:
            - name: oidc-provider-1
            - resource_id: arn:aws:iam::565284315989:oidc-provider/test.example.com
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets information about the AWS IAM OpenID Connect provider

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.iam.open_id_connect_provider
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an IAM entity to describe an identity provider (IdP) that supports OpenID Connect (OIDC).

The OIDC provider that you create with this operation can be used as a principal in a role's trust policy.
Such a policy establishes a trust relationship between Amazon Web Services and the OIDC provider.

If you are using an OIDC identity provider from Google, Facebook, or Amazon Cognito, you don't need to create a
separate IAM identity provider. These OIDC identity providers are already built-in to Amazon Web Services and are
available for your use. Instead, you can move directly to creating new roles using your identity provider. To learn
more, see Creating a role for web identity or OpenID connect federation in the IAM User Guide.

When you create the IAM OIDC provider, you specify the following:
    * The URL of the OIDC identity provider (IdP) to trust
    * A list of client IDs (also known as audiences) that identify the application or applications allowed to
      authenticate using the OIDC provider.
    * A list of thumbprints of one or more server certificates that the IdP uses

You get all of this information from the OIDC IdP you want to use to access Amazon Web Services.

Args:
    name(Text): The idem name for IAM OIDC provider.

    url(Text): The URL of the identity provider. The URL must begin with https:// and should correspond to the iss
        claim in the provider's OpenID Connect ID tokens. Per the OIDC standard, path components are allowed but
        query parameters are not. Typically the URL consists of only a hostname, like https://server.example.org or
        https://example.com . The URL should not contain a port number.

        You cannot register the same provider multiple times in a single Amazon Web Services account. If you try to
        submit a URL that has already been used for an OpenID Connect provider in the Amazon Web Services account,
        you will get an error.

    thumbprint_list(List): A list of server certificate thumbprints for the OpenID Connect (OIDC) identity
        provider's server certificates. Typically this list includes only one entry. However, IAM lets you have up
        to five thumbprints for an OIDC provider. This lets you maintain multiple thumbprints if the identity
        provider is rotating certificates.

        The server certificate thumbprint is the hex-encoded SHA-1 hash value of the X.509 certificate used by the
        domain where the OpenID Connect provider makes its keys available. It is always a 40-character string.

        You must provide at least one thumbprint when creating an IAM OIDC provider. For example, assume that the
        OIDC provider is server.example.com and the provider stores its keys at
        https://keys.server.example.com/openid-connect. In that case, the thumbprint string would be the hex-encoded
         SHA-1 hash value of the certificate used by https://keys.server.example.com.

        For more information about obtaining the OIDC provider thumbprint, see Obtaining the thumbprint for an
        OpenID Connect provider in the IAM User Guide .

        (string) --
            Contains a thumbprint for an identity provider's server certificate.

            The identity provider's server certificate thumbprint is the hex-encoded SHA-1 hash value of the
            self-signed X.509 certificate. This thumbprint is used by the domain where the OpenID Connect provider
            makes its keys available. The thumbprint is always a 40-character string.

    resource_id(Text, optional): The Amazon Resource Name (ARN) of the IAM OpenID Connect provider resource object.

    client_id_list(List, optional): Provides a list of client IDs, also known as audiences. When a mobile or web
        app registers with an OpenID Connect provider, they establish a value that identifies the application. This
        is the value that's sent as the client_id parameter on OAuth requests.

        You can register multiple client IDs with the same provider. For example, you might have multiple
        applications that use the same OIDC provider. You cannot register more than 100 client IDs with a single
        IAM OIDC provider.

        There is no defined format for a client ID. The CreateOpenIDConnectProviderRequest operation accepts
        client IDs up to 255 characters long.

    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the IAM OpenID Connect (OIDC) provider.
        Each tag consists of a key name and an associated value. Defaults to None.
        * (Key): The key name that can be used to look up or retrieve the associated value. For example,
            Department or Cost Center are common choices.
        * (Value): The value associated with this tag. For example, tags with a key name of Department could have
            values such as Human Resources, Accounting, and Support. Tags with a key name of Cost Center
            might have values that consist of the number associated with the different cost centers in your
            company. Typically, many resources have tags with the same key name but with different values.
            Amazon Web Services always interprets the tag Value as a single string. If you need to store an
            array, you can store comma-separated values in the string. However, you must interpret the value
            in your code.
Request Syntax:
    [oidc-resource-name]:
      aws.iam.open_id_connect_provider.present:
      - name: 'string'
      - resource_id: 'string'
      - url: 'string'
      - client_id_list:
        - 'string'
      - thumbprint_list:
        - 'string'
      - tags:
        - Key: 'string'
          Value: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        oidcprovider-1:
          aws.iam.open_id_connect_provider.present:
          - name: oidcprovider-1
          - url: https://abc.example.com
          - client_id_list:
            - acd.amazonaws.com
            - xyz.com
          - thumbprint_list:
            - 9e99a48a9960b14926bb7f3b02e22da2b0ab7402
          - tags:
            - Key: Name
              Value: oidc-name
            - Key: env
              Value: dev
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.iam.open_id_connect_provider](https://docs.idemproject.io/idem-aws/en/latest/ref/states/iam/open_id_connect_provider.html).
