---
title: "aws.acm.certificate_validation"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function.

Returns detailed metadata about the specified ACM certificate required for its validation.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.acm.certificate_validation
```
{{< /tab >}}

{{< tab "present" >}}

```
Before the Amazon certificate authority (CA) can issue a certificate for your site, AWS Certificate Manager (ACM)
must prove that you own or control all of the domain names that you specify in your request. You can choose to prove
your ownership with either Domain Name System (DNS) validation or with email validation at the time you request a
certificate. In case of email validation, manual email approval of ACM certificate is required. Validation applies
only to publicly trusted certificates issued by ACM. ACM does not validate domain ownership for imported certificates
or for certificates signed by a private CA.

Args:
    name(Text): An Idem name of the resource.
    certificate_arn(Text): The Amazon Resource Name (ARN) of certificate.
    resource_id(Text, optional): The Amazon Resource Name (ARN) of certificate to identify the resource.
    validation_record_fqdns(List, optional): List of FQDNs that implement the validation. Only valid for DNS
        validation method ACM certificates. If this is set, the resource can implement additional sanity checks and
        has an explicit dependency on the resource that is implementing the validation.
    timeout(Dict, optional): Timeout configuration for waiting for Aws Certificate to get issued.
        * describe (Dict) -- Timeout configuration for describing certificate
            * delay (int, Optional): The amount of time in seconds to wait between attempts.
            * max_attempts (int, Optional): Customized timeout configuration containing delay and max attempts.
Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls
        [name]
          aws.acm.certificate_validation.present:
          - certificate_arn: arn:aws:acm:eu-west-2:sample_arn
          - resource_id: arn:aws:acm:eu-west-2:sample_arn
          - validation_record_fqdns:
            - abc.dp.example.net.
            - abc2.testing.example.net.
          - timeout:
            describe:
                delay: 10
                max_attempts: 20
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.acm.certificate_validation](https://docs.idemproject.io/idem-aws/en/latest/ref/states/acm/certificate_validation.html).
