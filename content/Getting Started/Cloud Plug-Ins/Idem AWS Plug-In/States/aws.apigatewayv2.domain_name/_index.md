---
title: "aws.apigatewayv2.domain_name"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an API Gateway v2 domain name resource.

Args:
    name(string): An Idem name of the resource.
    resource_id(string, optional): AWS API Gateway v2 domain name.
        Idem automatically considers this resource being absent if this field is not specified.

Request syntax:
    [idem_test_aws_apigatewayv2_domain_name]:
      aws.apigatewayv2.domain_name.absent:
        - name: 'string'
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_domain_name:
          aws.apigatewayv2.domain_name.absent:
            - name: value
            - resource_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets the API Gateway v2 domain name resources for an AWS account.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.apigatewayv2.domain_name
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an API Gateway v2 domain name resource.

Args:
    name(string): An Idem name of the resource. This is also used as the name of the domain name during resource creation.
    resource_id(string, optional): AWS API Gateway v2 domain name.
    domain_name_configurations(List[Dict[str, Any]], optional): The domain name configurations. Defaults to None.
        * ApiGatewayDomainName (str, optional): A domain name for the API.
        * CertificateArn (str, optional): An AWS-managed certificate that will be used by the edge-optimized endpoint for this domain
            name. AWS Certificate Manager is the only supported source.
        * CertificateName (str, optional): The user-friendly name of the certificate that will be used by the edge-optimized endpoint for
            this domain name.
        * CertificateUploadDate (Text, optional): The timestamp when the certificate that was used by edge-optimized endpoint for this domain name
            was uploaded.
        * DomainNameStatus (str, optional): The status of the domain name migration. The valid values are AVAILABLE, UPDATING,
            PENDING_CERTIFICATE_REIMPORT, and PENDING_OWNERSHIP_VERIFICATION. If the status is UPDATING, the
            domain cannot be modified further until the existing operation is complete. If it is AVAILABLE,
            the domain can be updated.
        * DomainNameStatusMessage (str, optional): An optional text message containing detailed information about status of the domain name
            migration.
        * EndpointType (str, optional): The endpoint type.
        * HostedZoneId (str, optional): The Amazon Route 53 Hosted Zone ID of the endpoint.
        * SecurityPolicy (str, optional): The Transport Layer Security (TLS) version of the security policy for this domain name. The
            valid values are TLS_1_0 and TLS_1_2.
        * OwnershipVerificationCertificateArn (str, optional): The ARN of the public certificate issued by ACM to validate ownership of your custom domain.
            Only required when configuring mutual TLS and using an ACM imported or private CA certificate
            ARN as the regionalCertificateArn
    mutual_tls_authentication(Dict[str, Any], optional): The mutual TLS authentication configuration for a custom domain name. Defaults to None.
        * TruststoreUri (str, optional): An Amazon S3 URL that specifies the truststore for mutual TLS authentication, for example,
            s3://bucket-name/key-name. The truststore can contain certificates from public or private
            certificate authorities. To update the truststore, upload a new version to S3, and then update
            your custom domain name to use the new version. To update the truststore, you must have
            permissions to access the S3 object.
        * TruststoreVersion (str, optional): The version of the S3 object that contains your truststore. To specify a version, you must have
            versioning enabled for the S3 bucket.
    tags(Dict, optional): The collection of tags associated with a domain name.

Request Syntax:
    [idem_test_aws_apigatewayv2_domain_name]:
      aws.apigatewayv2.domain_name.present:
        - name: 'string'
        - domain_name_configurations: [
            {
                'ApiGatewayDomainName': 'string',
                'CertificateArn': 'string',
                'CertificateName': 'string',
                'CertificateUploadDate': datetime(2015, 1, 1),
                'DomainNameStatus': 'AVAILABLE'|'UPDATING'|'PENDING_CERTIFICATE_REIMPORT'|'PENDING_OWNERSHIP_VERIFICATION',
                'DomainNameStatusMessage': 'string',
                'EndpointType': 'REGIONAL'|'EDGE',
                'HostedZoneId': 'string',
                'SecurityPolicy': 'TLS_1_0'|'TLS_1_2',
                'OwnershipVerificationCertificateArn': 'string'
            }
        ]
        - mutual_tls_authentication: {
            'TruststoreUri': 'string',
            'TruststoreVersion': 'string
          }
        - tags: {
            'string': 'string'
          }

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_domain_name:
          aws.apigatewayv2.domain_name.present:
            - name: value
            - domain_name_configurations: [
                {
                    'ApiGatewayDomainName': value,
                    'CertificateArn': 'value,
                    'CertificateName': 'value,
                    'CertificateUploadDate': value,
                    'DomainNameStatus': value,
                    'DomainNameStatusMessage': value,
                    'EndpointType': value,
                    'HostedZoneId': value,
                    'SecurityPolicy': value,
                    'OwnershipVerificationCertificateArn': value
                }
            ]
            - mutual_tls_authentication: {
                'TruststoreUri': 'string',
                'TruststoreVersion': 'string
            }
            - tags: {
                value: value
            }
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed API Gateway v2 domain_name resource as a data-source.

Args:
    name(string): An Idem name of the resource.
    resource_id(string): AWS API Gateway v2 domain name.

Request syntax:
    [idem_test_aws_apigatewayv2_domain_name]:
      aws.apigatewayv2.domain_name.search:
        - resource_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_apigatewayv2_domain_name:
          aws.apigatewayv2.domain_name.search:
            - resource_id: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.apigatewayv2.domain_name](https://docs.idemproject.io/idem-aws/en/latest/ref/states/apigatewayv2/domain_name.html).
