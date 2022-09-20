---
title: "aws.lambda_aws.function_permission"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Remove specified permission from the lambda function.

Args:
    hub:
    ctx:
    name(str): Name/Id of the statement/permission
    function_name(str): The name of the Lambda function, version, or alias.
                    Name formats
                    Function name - my-function (name-only), my-function:v1 (with alias).
                    Function ARN - arn:aws:lambda:us-west-2:123456789012:function:my-function .
                    Partial ARN - 123456789012:function:my-function .
    resource_id(str, Optional): Name/Id of the statement/permission

Request Syntax:
    [statement_id]:
      aws.lambda_aws.function_permission.absent:
      - name: 'string'

Returns:
    Dict[str, Any]

Examples:

    . code-block:: sls

        test-001:
          aws.lambda_aws.function_permission.absent:
          - name: test-001
```
{{< /tab >}}

{{< tab "describe" >}}

```
Returns permissions associated with each lambda function.

Args:
    hub:
    ctx:

Request Syntax:
    [statement-id]:
      aws.lambda_aws.function_permission.present:
      - name: 'string'
        resource_id: 'string'
        statements:
        - action: 'string'
          effect: 'string'
          principal:
            'string'
          statement_id: 'string'


Returns:
    Dict[str, Any]

Examples:

    . code-block:: sls

        test-001:
          aws.lambda_aws.function_permission.present:
          - name: test-001
            resource_id: test-001
            function_name: ecd17a181d6588e27c976cdeff501e90750b0dcafebba907cc4aab3c
            action: lambda:GetAlias
            effect: Allow
            principal:
              AWS: arn:aws:iam::537227425989:user/idem-fixture-user-18964248-75dd-4765-80b2-100901a8c74e
```
{{< /tab >}}

{{< tab "present" >}}

```
Add specified permission to the lambda function.

Args:
    hub:
    ctx:
    name(str): Name/Id of the statement/permission
    action(str): The action that the principal can use on the function. For example, lambda:InvokeFunction or
            lambda:GetFunction.
    function_name(str): The name of the Lambda function, version, or alias.
                    Name formats
                    Function name - my-function (name-only), my-function:v1 (with alias).
                    Function ARN - arn:aws:lambda:us-west-2:123456789012:function:my-function .
                    Partial ARN - 123456789012:function:my-function .
    principal(str): The Amazon Web Services service or account that invokes the function. If you specify a service,
                use source_arn or source_account to limit who can invoke the function through that service.
    source_arn(str, Optional): For Amazon Web Services , the ARN of the Amazon Web Services resource that invokes the
                function. For example, an Amazon S3 bucket or Amazon SNS topic.
    source_account(str, Optional): For Amazon S3, the ID of the account that owns the resource. Use this together with SourceArn to
                    ensure that the resource is owned by the specified account. It is possible for an Amazon S3
                    bucket to be deleted by its owner and recreated by another account.
    resource_id(str, Optional): Name/Id of the statement/permission
    event_source_token(str, Optional): For Alexa Smart Home functions, a token that must be supplied by the invoker.
    qualifier(str, Optional): Specify a version or alias to add permissions to a published version of the function.
    revision_id(str, Optional): Only update the policy if the revision ID matches the ID that's specified. Use this option to avoid modifying a policy that has changed since you last read it.
    principal_org_id(str, Optional): The identifier for your organization in Organizations. Use this to grant permissions to all the Amazon Web Services accounts under this organization.
    function_url_auth_type(str, Optional): The type of authentication that your function URL uses. Set to AWS_IAM if you want to restrict access to authenticated IAM users only. Set to NONE if you want to bypass IAM authentication to create a public endpoint.


Request Syntax:
    [statement_id]:
      aws.lambda_aws.function_permission.present:
      - name: 'string'
        resource_id: 'string'
        action: 'string'
        function_name: 'string'
        principal:
            'string' : 'string'

Returns:
    Dict[str, Any]

Examples:

    . code-block:: sls

        test-001:
          aws.lambda_aws.function_permission.present:
          - action: lambda:GetAlias
          - effect: Allow
          - function_name: ecd17a181d6588e27c976cdeff501e90750b0dcafebba907cc4aab3c
          - name: test-001
          - principal:
              AWS: AIDAX2FJ77DC2AS7BAPBU
          - resource_id: test-001
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.lambda_aws.function_permission](https://docs.idemproject.io/idem-aws/en/latest/ref/states/lambda_aws/function_permission.html).
