---
title: "aws.ecr.repository_policy"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the repository policy associated with the specified repository.

Args:
    name(string): An Idem name of the resource.
    repository_name(string): The name of the repository that contains the policy to delete.
    resource_id(string, optional): The registry id and repository name with a separator '-'. Format: [registry_id]-[repository_name].
        Idem automatically considers this resource being absent if this field is not specified.
    registry_id(string, optional): The Amazon Web Services account ID associated with the registry that contains the repository policy to
        delete. If you do not specify a registry, the default registry is assumed. Defaults to None.

Request syntax:
    [idem_test_aws_ecr_repository_policy]:
      aws.ecr.repository_policy.absent:
        - name: 'string'
        - repository_name: value
        - resource_id: 'string'
        - registry_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_ecr_repository_policy:
          aws.ecr.repository_policy.absent:
            - name: value
            - repository_name: value
            - resource_id: value
            - registry_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describes policies for image repositories in a registry in a way that can be recreated/managed with the corresponding "present" function.

Returns:
    Dict[str, Dict[str, Any]]

Examples:

    .. code-block:: bash

        $ idem describe aws.ecr.repository_policy
```
{{< /tab >}}

{{< tab "present" >}}

```
Applies a repository policy to the specified repository to control access permissions.
For more information, see Amazon ECR Repository policies in the Amazon Elastic Container Registry User Guide.

Args:
    name(string): An Idem name of the resource.
    repository_name(string): The name of the repository to receive the policy.
    policy_text(Dict or string): The JSON repository policy text to apply to the repository.
    resource_id(string, optional): The registry id and repository name with a separator '-'. Format: [registry_id]-[repository_name].
    registry_id(string, optional): The Amazon Web Services account ID associated with the registry that contains the repository. If you
        do not specify a registry, the default registry is assumed.
    force(bool, optional): If the policy you are attempting to set on a repository policy would prevent you from setting another policy
        in the future, you must force the SetRepositoryPolicy operation. This is intended to prevent accidental repository lock outs.

Request Syntax:
    [idem_test_aws_ecr_repository_policy]:
      aws.ecr.repository_policy.present:
        - name: 'string'
        - repository_name: 'string'
        - policy_text: 'string'
        - registry_id: 'string'
        - force: True|False

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_ecr_repository_policy:
          aws.ecr.repository.present:
            - name: value
            - repository_name: value
            - policy_text: value
            - registry_id: value
            - force: True
```
{{< /tab >}}

{{< tab "search" >}}

```
Use an un-managed ECR repository policy as a data-source.

Args:
    name(string): An Idem name of the resource.
    repository_name(string): The name of the repository that contains the policy to search.
    registry_id(string, optional): The Amazon Web Services account ID associated with the registry that contains the repository
        with the policy to search. If you do not specify a registry, the default registry is assumed. Defaults to None.

Request syntax:
    [idem_test_aws_ecr_repository_policy]:
      aws.ecr.repository_policy.search:
        - name: 'string'
        - repository_name: 'string'
        - registry_id: 'string'

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        idem_test_aws_ecr_repository_policy:
          aws.ecr.repository_policy.search:
            - name: value
            - repository_name: value
            - registry_id: value
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ecr.repository_policy](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ecr/repository_policy.html).
