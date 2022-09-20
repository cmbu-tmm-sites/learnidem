---
title: "aws.acm.certificate_manager"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes a certificate and its associated private key. If this action succeeds, the certificate no longer appears in
the list that can be displayed by calling the ListCertificates action or be retrieved by calling the GetCertificate
action. The certificate will not be available for use by Amazon Web Services services integrated with ACM.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text, optional): The Amazon Resource Name (ARN) of certificate to identify the resource.
Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        resource_is_absent:
          aws.acm.certificate.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function.

Returns detailed metadata about the specified ACM certificate.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.acm.certificate
```
{{< /tab >}}

{{< tab "present" >}}

```
You can use ACM to manage SSL/TLS certificates for your AWS-based websites and applications.
Imports a certificate into AWS Certificate Manager (ACM) to use with services that are integrated with ACM.
Note that integrated services allow only certificate types and keys they support to be associated with their
resources. Further, their support differs depending on whether the certificate is imported into IAM or into ACM.
Requests an ACM certificate for use with other AWS services. To request an ACM certificate, you must specify a
fully qualified domain name (FQDN) in the DomainName parameter. You can also specify additional FQDNs in the
SubjectAlternativeNames parameter.
If you are requesting a private certificate, domain validation is not required. If you are requesting a public
certificate, each domain name that you specify must be validated to verify that you own or control the domain.
You can use DNS validation or email validation.

Args:
    name(Text): An Idem name of the resource.
    resource_id(Text, optional): The Amazon Resource Name (ARN) of certificate to identify the resource.
    certificate_arn(Text, optional): The Amazon Resource Name (ARN) of an imported certificate to replace.
        To import a new certificate, omit this field.
    certificate(Bytes, optional): The certificate to import.
    private_key(Bytes, optional): The private key that matches the public key in the certificate.
    certificate_chain(Bytes, optional): The PEM encoded certificate chain.

    domain_name(Text, optional): Fully qualified domain name (FQDN), such as www.example.com, that you want to
        secure with an ACM certificate.,
    validation_method(Text, optional): The method you want to use if you are requesting a public certificate to
        validate that you own or control domain.,
    subject_alternative_names(List, optional): Additional FQDNs to be included in the Subject Alternative Name
        extension of the ACM certificate.,
    idempotency_token(Text,Optional): Customer chosen string that can be used to distinguish between calls to
        RequestCertificate .,
    domain_validation_options(List[Dict[str, Any]], optional): The domain name that you want ACM to use to send you emails so that
        you can validate domain ownership. Defaults to None.
        * domain_name (str): A fully qualified domain name (FQDN) in the certificate request.
        * validation_domain (str): The domain name that you want ACM to use to send you validation emails. This domain name is the
            suffix of the email addresses that you want ACM to use. This must be the same as the DomainName
            value or a superdomain of the DomainName value. For example, if you request a certificate for
            testing.example.com, you can specify example.com for this value. In that case, ACM sends domain
            validation emails to the following five addresses:   admin@example.com
            administrator@example.com   hostmaster@example.com   postmaster@example.com
            webmaster@example.com
        * validation_domain (str): The domain name that you want ACM to use to send you validation emails. This domain name is the
            suffix of the email addresses that you want ACM to use. This must be the same as the DomainName
            value or a superdomain of the DomainName value. For example, if you request a certificate for
            testing.example.com, you can specify example.com for this value. In that case, ACM sends domain
            validation emails to the following five addresses:   admin@example.com
            administrator@example.com   hostmaster@example.com   postmaster@example.com
            webmaster@example.com
        * validation_method (str): Specifies the domain validation method.
        * resource_record (Dict[str, Any]): Contains the CNAME record that you add to your DNS database for domain validation.
            * Name (str): The name of the DNS record to create in your domain. This is supplied by ACM.
            * Type (str): The type of DNS record. Currently this can be CNAME.
            * Value (str): The value of the CNAME record to add to your DNS database. This is supplied by ACM.
        * validation_status (str): The validation status of the domain name.
            This can be one of the following values:
                PENDING_VALIDATION
                SUCCESS
                FAILED
    options(Dict[str, Any], optional): Currently, you can use this parameter to specify whether to add the certificate to a certificate
        transparency log. Certificate transparency makes it possible to detect SSL/TLS certificates that
        have been mistakenly or maliciously issued. Certificates that have not been logged typically
        produce an error message in a browser. For more information, see Opting Out of Certificate
        Transparency Logging. Defaults to None.
        * CertificateTransparencyLoggingPreference (str, optional): You can opt out of certificate transparency
            logging by specifying the DISABLED option. Opt in by specifying ENABLED.
    certificate_authority_arn(Text, optional): The Amazon Resource Name (ARN) of the private certificate authority
        (CA) that will be used to issue the certificate.,
    tags(Dict, optional): The collection of tags associated with the certificate. Defaults to None.
        * (Key): The key of the tag.
        * (Value, optional): The value of the tag.
    timeout(Dict, optional): Timeout configuration for request/import AWS Certificate.
        * create (Dict) -- Timeout configuration for request/imporng AWS Certificate
            * delay (int, Optional): The amount of time in seconds to wait between attempts.
            * max_attempts (int, Optional): Customized timeout configuration containing delay and max attempts.



Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls
        (For requesting a certificate: )
        [name]
          aws.acm.certificate_manager.present:
          - domain_name: www.example.com
          - validation_method: DNS
          - subject_alternative_names:
              - www.example.net
          - idempotency_token: ExampleIdempotancyToken
          - domain_validation_options:
              - domain_name: testing.example.com
              - validation_domain: example.com
          - options:
              - certificate_transparency_loggingPreference: DISABLED
          - certificate_authority_arn: arn:aws:acm-pca:region:account:certificate-authority/12345678-1234-1234-1234-123456789012
          - tags:
              - Key: class
                Value: test

        (For importing a certificate: )
        [name]
          aws.acm.certificate_manager.present:
          - resource_id: arn:aws:acm-pca:region:account:certificate-authority/12345678-1234-1234-1234-123456789012
          - certificate_arn: arn:aws:acm-pca:region:account:certificate-authority/12345678-1234-1234-1234-123456789012
          - certificate: example_certificate
          - private_key: -----BEGIN RSA PRIVATE KEY-----
              MIIEpQIBAAKCAQEA3Tz2mr7SZiAMfQyuvBjM9Oi..Z1BjP5CE/Wm/Rr500P
              RK+Lh9x5eJPo5CAZ3/ANBE0sTK0ZsDGMak2m1g7..3VHqIxFTz0Ta1d+NAj
              -----END RSA PRIVATE KEY-----
          - certificate_chain: example_certificate_chain
          - tags:
              - Key: class
                Value: test
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.acm.certificate_manager](https://docs.idemproject.io/idem-aws/en/latest/ref/states/acm/certificate_manager.html).
