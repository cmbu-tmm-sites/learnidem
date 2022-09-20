---
title: "aws.lambda_aws.function"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes a Lambda function. To delete a specific function version, use the Qualifier parameter.
Otherwise, all versions and aliases are deleted.

To delete Lambda event source mappings that invoke a function, use DeleteEventSourceMapping . For Amazon Web
Service services and resources that invoke your function directly, delete the trigger in the service where you
originally configured it.

Args:
    resource_id(Text): The name/ ARN/ partial ARN of the AWS Lambda function, version, or alias.
    qualifier(Text, optional): Specify a version or alias to get details about a published version of the function.
    name(Text): The name of the Lambda function, version, or alias.
        Name formats
            Function name - my-function (name-only), my-function:v1 (with alias).
            Function ARN - arn:aws:lambda:us-west-2:123456789012:function:my-function .
            Partial ARN - 123456789012:function:my-function .
    hub:
    ctx:

Request Syntax:
    [lambda_function-id]:
      aws.lambda.function.absent:
      - name: 'string'
      - qualifier: 'string'

Returns:
    Dict[str, Any]

Examples:

    . code-block:: sls

        resource_is_absent:
            aws.lambda.function.absent:
                - name: resource_is_absent
                - qualifier: 1
```
{{< /tab >}}

{{< tab "describe" >}}

```
Returns a list of Lambda functions, with the version-specific configuration of each. Lambda returns up to 50
functions per call. Set FunctionVersion to ALL to include all published versions of each function in addition to
the unpublished version.

Args:
    hub:
    ctx:

Request Syntax:
    [lambda_function-id]:
      aws.lambda.function.describe:
      - name: 'string'
      - qualifier: 'string'

Returns:
    Dict[str, Any]

Examples:

    . code-block:: sls

        test_dyanmodb_table:
            aws.lambda.function.describe:
                - name: test_dyanmodb_table
                - qualifier: 1
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates a Lambda function. To create a function, you need a deployment package and an execution role . The
deployment package is a .zip file archive or container image that contains your function code. The execution role
grants the function permission to use Amazon Web Services, such as Amazon CloudWatch Logs for log
streaming and X-Ray for request tracing.

When you create a function, Lambda provisions an instance of the function and its supporting resources. If your
function connects to a VPC, this process can take a minute or so. During this time, you can't invoke or modify
the function. The State , StateReason , and StateReasonCode fields in the response from GetFunctionConfiguration
indicate when the function is ready to invoke. For more information, see Function States .

A function has an unpublished version, and can have published versions and aliases. The unpublished version
changes when you update your function's code and configuration. A published version is a snapshot of your
function code and configuration that can't be changed. An alias is a named resource that maps to a version,
and can be changed to map to a different version. Use the Publish parameter to create version 1 of your function
from its initial configuration.

Args:
    resource_id(Text): The name/ ARN/ partial ARN of the AWS Lambda function, version, or alias.
    name(Text): The name of the Lambda function.
        Name formats
            Function name - my-function .
            Function ARN - arn:aws:lambda:us-west-2:123456789012:function:my-function .
            Partial ARN - 123456789012:function:my-function .
        The length constraint applies only to the full ARN. If you specify only the function name, it is limited
            to 64 characters in length.
    role(Text): The Amazon Resource Name (ARN) of the function's execution role.
    code(Dict[str, Any]): The code for the function.
        * ZipFile (ByteString, optional): The base64-encoded contents of the deployment package. Amazon Web Services SDK and Amazon Web
            Services CLI clients handle the encoding for you.
        * S3Bucket (str, optional): An Amazon S3 bucket in the same Amazon Web Services Region as your function. The bucket can be
            in a different Amazon Web Services account.
        * S3Key (str, optional): The Amazon S3 key of the deployment package.
        * S3ObjectVersion (str, optional): For versioned objects, the version of the deployment package object to use.
        * ImageUri (str, optional): URI of a container image in the Amazon ECR registry.
    runtime(Text, optional): The identifier of the function's runtime . Runtime is required if the deployment package
        is a .zip file archive.
    revision_id(Text, optional): Only update the function if the revision ID matches the ID that's specified.
            Use this option to avoid modifying a function that has changed since you last read it.
    destination_config(dict, optional): A destination for events after they have been sent to a function for
            processing.
    maximum_event_age_in_seconds(int, optional): The maximum age of a request that Lambda sends to a function for
            processing.
    maximum_retry_attempts (int, optional): The maximum number of times to retry when the function returns an error.
    qualifier(Text): The version of the Lambda function.
    architectures(list, optional): The instruction set architecture that the function supports. Enter a string array
            with one of the valid values (arm64 or x86_64). The default value is x86_64 .
    code_signing_config_arn(Text, optional): To enable code signing for this function, specify the ARN of a
            code-signing configuration. A code-signing configuration includes a set of signing profiles, which
            define the trusted publishers for this function.
    image_config(Dict[str, Any], optional): Container image configuration values that override the values in the container image Dockerfile. Defaults to None.
        * EntryPoint (List[str], optional): Specifies the entry point to their application, which is typically the location of the runtime
            executable.
        * Command (List[str], optional): Specifies parameters that you want to pass in with ENTRYPOINT.
        * WorkingDirectory (str, optional): Specifies the working directory.
    file_system_configs(List[Dict[str, Any]], optional): Connection settings for an Amazon EFS file system. Defaults to None.
        * Arn (str): The Amazon Resource Name (ARN) of the Amazon EFS access point that provides access to the file
            system.
        * LocalMountPath (str): The path where the function can access the file system, starting with /mnt/.
    layers(list, optional): A list of function layers to add to the function's execution environment. Specify each
            layer by its ARN, including the version.
    tags(Dict[str, str], optional): A list of tags to apply to the function. Defaults to None.
    tracing_config(Dict[str, Any], optional): Set Mode to Active to sample and trace a subset of incoming requests with X-Ray. Defaults to None.
        * Mode (str, optional): The tracing mode.
    kms_key_arn(Text, optional): The ARN of the Amazon Web Services Key Management Service (KMS) key that's used to
            encrypt your function's environment variables. If it's not provided, Lambda uses a default service key.
    environment(Dict[str, Any], optional): Environment variables that are accessible from function code during execution. Defaults to None.
        * Variables (Dict[str, str], optional): Environment variable key-value pairs. For more information, see Using Lambda environment
            variables.
    dead_letter_config(Dict[str, Any], optional): A dead letter queue configuration that specifies the queue or topic where Lambda sends
        asynchronous events when they fail processing. For more information, see Dead Letter Queues. Defaults to None.
        * TargetArn (str, optional): The Amazon Resource Name (ARN) of an Amazon SQS queue or Amazon SNS topic.
    package_type(Text, optional): The type of deployment package. Set to Image for container image and set Zip for
            ZIP archive.
    vpc_config(Dict[str, Any], optional): For network connectivity to Amazon Web Services resources in a VPC, specify a list of security
        groups and subnets in the VPC. When you connect a function to a VPC, it can only access
        resources and the internet through that VPC. For more information, see VPC Settings. Defaults to None.
        * SubnetIds (List[str], optional): A list of VPC subnet IDs.
        * SecurityGroupIds (List[str], optional): A list of VPC security groups IDs.
    publish(bool, optional): Set to true to publish the first version of the function during creation.
    memory_size(int, optional): The amount of memory available to the function at runtime. Increasing the function
            memory also increases its CPU allocation. The default value is 128 MB. The value can be any multiple of
            1 MB.
    function_timeout(int, optional): The amount of time (in seconds) that Lambda allows a function to run before
            stopping it. The default is 3 seconds. The maximum allowed value is 900 seconds.
    description(Text, optional): A description of the function.
    handler(Text, optional): The name of the method within your code that Lambda calls to execute your function.
            Handler is required if the deployment package is a .zip file archive. The format includes the file name.
            It can also include namespaces and other qualifiers, depending on the runtime.
    timeout(Dict, optional): Timeout configuration for create/update/deletion of AWS IAM Policy.
        * create (Dict): Timeout configuration for creating AWS IAM Policy
            * delay (int, Optional): The amount of time in seconds to wait between attempts.
            * max_attempts (int, Optional): Customized timeout configuration containing delay and max attempts.
        * update(Dict, optional): Timeout configuration for updating AWS IAM Policy
            * delay (int, Optional): The amount of time in seconds to wait between attempts.
            * max_attempts: (int, Optional) Customized timeout configuration containing delay and max attempts.
    hub:
    ctx:

Request Syntax:
    [lambda_function-id]:
      aws.lambda.function.present:
      - name: 'string'
      - runtime: 'string'
      - role: 'string'
      - code: 'Dict'
      - handler: 'string'
      - description: 'string'
      - function_timeout: 'int'
      - memory_size: 'int'
      - publish: 'bool'
      - vpc_config: 'Dict'
      - package_type: 'string'
      - dead_letter_config: 'string'
      - environment: 'Dict'
      - kms_key_arn: 'string'
      - tracing_config: 'Dict'
      - layers: 'list'
      - file_system_configs: 'list'
      - image_config: 'Dict'
      - code_signing_config_arn: 'string'
      - architectures: 'list'
      - version: 'string'
      - tags:
        - Key: 'string'
          Value: 'string'

Returns:
    Dict[str, Any]

Examples:

    . code-block:: sls

        test_dyanmodb_table:
          aws.lambda.function.present:
            - name: test_dyanmodb_table
            - resource_id: test_dyanmodb_table
            - run_time: nodejs12.x
            - role: arn:aws:iam::123456789012:role/lambda-role
            - code:{
                       'S3Bucket': 'my-bucket-1xpuxmplzrlbh',
                        'S3Key': 'function.zip',
                    },
            - tags:
              - Key: DEPARTMENT
                Value: Assets
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.lambda_aws.function](https://docs.idemproject.io/idem-aws/en/latest/ref/states/lambda_aws/function.html).
