---
title: "aws.eks.fargate_profile"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes an Fargate profile. When you delete a Fargate profile, any pods running on Fargate that were created
with the profile are deleted. If those pods match another Fargate profile, then they are scheduled on Fargate
with that profile. If they no longer match any Fargate profiles, then they are not scheduled on Fargate and they
may remain in a pending state. Only one Fargate profile in a cluster can be in the DELETING status at a time.
You must wait for a Fargate profile to finish deleting before you can delete any other profiles in that cluster.

Args:
    name(Text): An Idem name of the resource
    cluster_name(Text): The name of the Amazon EKS cluster associated with the Fargate profile to delete.
    resource_id(Text, Optional): AWS Fargate profile name. Idem considers name of fargate profile if
     this field is not specified.
    timeout(Dict, optional): Timeout configuration for operations on fargate_profile
        * delete (Dict) -- Timeout configuration for deleting fargate_profile
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- The maximum number of attempts to be made

Request Syntax:
    fargate_resource_id:
       aws.eks.fargate_profile.absent:
       - name: 'string'
       - cluster_name: 'string'
Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls
        fargate01-idem-cluster01:
          aws.eks.fargate_profile.absent:
          - resource_id: fargate01
          - name: fargate01
          - cluster_name: idem-cluster01
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function
Lists the Fargate profiles associated with the specified cluster in your Amazon Web Services account in the
specified Region.
Returns:
    Dict[str, Dict[str, Any]]
Examples:

    .. code-block:: sls
     fargate01-idem-cluster01:
          aws.eks.fargate_profile.present:
          - name: fargate01
          - cluster_name: idem-cluster01
          - pod_execution_role_arn: arn:aws:iam::537227425989:role/eksfargateprofile-role
          - subnets:
            - subnet-006a41c410b9485dd
            - subnet-01368936bb540ba1e
          - selectors:
            - labels: {}
              namespace: default
          - tags:
              fargate01: 'created via code'
```
{{< /tab >}}

{{< tab "present" >}}

```
Creates an Fargate profile for your Amazon EKS cluster. You must have at least one Fargate profile in a cluster
to be able to run pods on Fargate. The Fargate profile allows an administrator to declare which pods run on
Fargate and specify which pods run on which Fargate profile. This declaration is done through the profile’s
selectors. Each profile can have up to five selectors that contain a namespace and labels. A namespace is
required for every selector. The label field consists of multiple optional key-value pairs. Pods that match the
selectors are scheduled on Fargate. If a to-be-scheduled pod matches any of the selectors in the Fargate
profile, then that pod is run on Fargate. When you create a Fargate profile, you must specify a pod execution
role to use with the pods that are scheduled with the profile. For more information, see Pod Execution Role in the
Amazon EKS User Guide. Fargate profiles are immutable. However, you can create a new updated profile to replace an existing profile
and then delete the original after the updated profile has finished creating. If any Fargate profiles in a cluster are in
the DELETING status, you must wait for that Fargate profile to finish deleting before you can create any other
profiles in that cluster. For more information, see Fargate Profile in the Amazon EKS User Guide.

Args:
    name(Text): An Idem name of the resource
    cluster_name(Text): The name of the Amazon EKS cluster to apply the Fargate profile to.
    pod_execution_role_arn(Text): The Amazon Resource Name (ARN) of the pod execution role to use for pods that match the
        selectors in the Fargate profile.
    subnets(List[str], optional): The IDs of subnets to launch your pods into. At this time, pods running on Fargate are not
        assigned public IP addresses, so only private subnets (with no direct route to an Internet
        Gateway) are accepted for this parameter. Defaults to None.
        Private subnets selected for fargate profile creation must be in different availability zones. Defaults to None.
    selectors(List[Dict[str, Any]], optional): The selectors to match for pods to use this Fargate profile. Each selector must have an
        associated namespace. Optionally, you can also specify labels for a namespace. You may specify
        up to five selectors in a Fargate profile. Defaults to None.
        * namespace (str, optional): The Kubernetes namespace that the selector should match.
        * labels (Dict[str, str], optional): The Kubernetes labels that the selector should match. A pod must contain all of the labels that
            are specified in the selector for it to be considered a match.
    client_request_token(Text, optional): Unique, case-sensitive identifier that you provide to ensure the idempotency of the request. Defaults to None.
    tags(Dict, optional): The metadata to apply to the Fargate profile to assist with categorization and organization.
        Each tag consists of a key and an optional value. Defaults to None.
    resource_id(Text, optional): AWS Fargate Profile name
    timeout(Dict, optional): Timeout configuration for operations on fargate_profile
        * create (Dict) -- Timeout configuration for creating fargate_profile
            * delay -- The amount of time in seconds to wait between attempts.
            * max_attempts -- The maximum number of attempts to be made.

    Request Syntax:
        fargate_resource_id:
           aws.eks.fargate_profile.present:
           - name: 'string'
           - resource_id: 'string'
           - cluster_name: 'string'
           - pod_execution_role_arn: 'string'
           - subnets:
              - private_subnet_id
              - private_subnet_id
        - selectors:
               - labels: {}
                 namespace: 'string'


Returns:
    Dict[str, Any]

Examples:
    .. code-block:: sls

        fargate01-idem-cluster01:
          aws.eks.fargate_profile.present:
          - name: fargate01
          - cluster_name: idem-cluster01
          - pod_execution_role_arn: arn:aws:iam::537227425989:role/eksfargateprofile-role
          - subnets:
            - subnet-006a41c410b9485dd
            - subnet-01368936bb540ba1e
          - selectors:
            - labels: {}
              namespace: default
          - tags:
              fargate01: 'created via code'
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.eks.fargate_profile](https://docs.idemproject.io/idem-aws/en/latest/ref/states/eks/fargate_profile.html).
