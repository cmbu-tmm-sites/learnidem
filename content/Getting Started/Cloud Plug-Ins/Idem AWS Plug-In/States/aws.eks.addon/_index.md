---
title: "aws.eks.addon"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Delete an Amazon EKS add-on. When you remove the add-on, it will also be deleted from the cluster. You can
always manually start an add-on on the cluster using the Kubernetes API.

Args:
    name(Text): An Idem name of the EKS addon resource.
    cluster_name(Text): The name of the cluster to delete the add-on from.
    resource_id(Text, optional): AWS EKS addon name. Idem automatically considers this resource being absent
     if this field is not specified.
    preserve(Boolean, optional): Specifying this option preserves the add-on software on your cluster but Amazon
        EKS stops managing any settings for the add-on. If an IAM account is associated with the add-on,
        it is not removed.
    timeout(Dict, optional): Timeout configuration for creating or updating cluster.
        * delete (Dict) -- Timeout configuration for deleting cluster
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- Customized timeout configuration containing delay and max attempts.

Request syntax:

    [idem-eks-addon-name]:
          aws.eks.addon.absent:
          - cluster_name: 'string'
          - resource_id: 'string'
          - preserve: boolean

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        kube-proxy:
          aws.eks.addon.absent:
          - cluster_name: eks-cluster-1
          - resource_id: kube-proxy
          - preserve: True
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists the available add-ons.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.eks.addon
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Creates an Amazon EKS add-on. Amazon EKS add-ons help to automate the provisioning and lifecycle management of
common operational software for Amazon EKS clusters. Amazon EKS add-ons require clusters running version 1.18 or
later because Amazon EKS add-ons rely on the Server-side Apply Kubernetes feature, which is only available in
Kubernetes 1.18 and later. For more information, see Amazon EKS add-ons in the Amazon EKS User Guide.

Args:
    name(Text): An Idem name of the EKS addon resource.
    resource_id(Text, optional): AWS EKS addon name.
    cluster_name(Text): The name of the cluster to create the add-on for
    addon_version(Text): The version of the add-on. The version must match one of the versions returned
        by ` DescribeAddonVersions
    service_account_role_arn(Text, optional):The Amazon Resource Name (ARN) of an existing IAM role to bind to the add-on's
        service account. The role must be assigned the IAM permissions required by the add-on. If you don't specify
        an existing IAM role, then the add-on uses the permissions assigned to the node IAM role.
    resolve_conflicts(Text, optional): How to resolve parameter value conflicts when migrating an existing add-on
        to an Amazon EKS add-on
    tags(Dict, optional): The metadata to apply to the cluster to assist with categorization and organization.
        Each tag consists of a key and an optional value. You define both
    timeout(Dict, optional): Timeout configuration for creating or updating addon.
        * create (Dict) -- Timeout configuration for creating addon
            * delay(int, default=10) -- The amount of time in seconds to wait between attempts.
            * max_attempts(int, default=60) -- Customized timeout configuration containing delay and max attempts.
        * update (string) -- Timeout configuration for updating addon
            * delay(int, default=10) -- The amount of time in seconds to wait between attempts.
            * max_attempts(int, default=60) -- Customized timeout configuration containing delay and max attempts.
Request Syntax:

    [eks-addon-name]:
          aws.eks.addon.present:
          - cluster_name: 'string'
          - addon_version: 'string'
          - resource_id: 'string'
          - service_account_role_arn: 'string'
          - resolve_conflicts: 'string'
          - tags:
            - Key: 'string'
              Value: 'string'
          - timeout:
               create:
                  delay: 'integer'
                  max_attempts: 'integer'
               update:
                  delay: 'integer'
                  max_attempts: 'integer

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        kube-proxy:
          aws.eks.addon.present:
          - cluster_name: eks-12j44i4k
          - addon_version: v1.19.8-eksbuild.1
          - resource_id: kube-proxy
          - service_account_role_arn: arn:role-ejwew124
          - resolve_conflicts: "OVERWRITE"
          - tags:
            - Key: Name
              Value: eks-addon-name
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.eks.addon](https://docs.idemproject.io/idem-aws/en/latest/ref/states/eks/addon.html).