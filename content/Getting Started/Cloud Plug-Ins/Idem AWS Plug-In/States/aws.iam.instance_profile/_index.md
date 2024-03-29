---
title: "aws.iam.instance_profile"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Deletes the specified instance profile. The instance profile must not have an associated role.  Make sure that
you do not have any Amazon EC2 instances running with the instance profile you are about to delete. Deleting a
role or instance profile that is associated with a running instance will break any applications running on the
instance.  For more information about instance profiles, see About instance profiles.

Args:
    name(Text): AWS Instance Profile Name.
    resource_id(Text, Optional): AWS Instance Profile Name. If not specified, Idem will use "name"
     parameter to identify the role policy on AWS.

Returns:
    Dict[str, Any]

Request Syntax:
  [iam-instance-profile-name]:
    aws.iam.instance_profile.present:
      - name: 'string'

Examples:

    .. code-block:: sls

        instance-profile-test:
          aws.iam.instance_profile.absent:
            - name: instance-profile-test
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe the resource in a way that can be recreated/managed with the corresponding "present" function


Lists the instance profiles that have the specified path prefix. If there are none, the operation returns an
empty list. For more information about instance profiles, see About instance profiles.  IAM resource-listing
operations return a subset of the available attributes for the resource. For example, this operation does not
return tags, even though they are an attribute of the returned object. To view all of the information for an
instance profile, see GetInstanceProfile.  You can paginate the results using the MaxItems and Marker
parameters.


Returns:
    Dict[str, Any]

Examples:

    .. code-block:: bash

        $ idem describe aws.iam.instance_profile
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

 Creates a new instance profile. For information about instance profiles, see Using roles for applications on
Amazon EC2 in the IAM User Guide, and Instance profiles in the Amazon EC2 User Guide.  For information about the
number of instance profiles you can create, see IAM object quotas in the IAM User Guide.
Tags can be set on a newly created instance profile, or updated on an existing one.
Roles are set and updated as a day-2 operation.

Args:
    name(Text): AWS Instance Profile Name.
    resource_id(Text, Optional): AWS Instance Profile Name.
    path(Text, Optional): The path to the instance profile.
    roles(Text, Optional): A list with up to one role name. Instance profile can be associated with a single role.
    tags(Dict or List, optional): Dict in the format of {tag-key: tag-value} or List of tags in the format of
        [{"Key": tag-key, "Value": tag-value}] to associate with the IAM instance profile. Each tag consists of
        a key name and an associated value. Defaults to None.
        * (Key): The key name that can be used to look up or retrieve the associated value. For example,
            Department or Cost Center are common choices.
        * (Value): The value associated with this tag. For example, tags with a key name of Department could have
            values such as Human Resources, Accounting, and Support. Tags with a key name of Cost Center
            might have values that consist of the number associated with the different cost centers in your
            company. Typically, many resources have tags with the same key name but with different values.
            Amazon Web Services always interprets the tag Value as a single string. If you need to store an
            array, you can store comma-separated values in the string. However, you must interpret the value
            in your code.

Returns:
    Dict[str, Any]

Request Syntax:
  [iam-instance-profile-name]:
    aws.iam.instance_profile.present:
      - name: 'string'
      - resource_id: 'string'
      - path: 'string'
      - roles:
        - RoleName: 'string'
      - Tags:
        - Key: 'string'
          Value: 'string'

Example:

    .. code-block:: sls

    inst-profile-1:
      aws.iam.instance_profile.present:
      - name: inst-profile-1
      - path: /aws-service-inst-profile/
      - roles:
        - RoleName: role-1
      - Tags:
        - Key: test-1
          Value: test-1-val
```
{{< /tab >}}

{{< tab "search" >}}

```
Provides details about a specific instance profile as a data-source.

Args:
    name(Text): AWS Instance Profile name to identify the resource.
    resource_id(Text, Optional): AWS Instance Profile name to identify the resource.

Request Syntax:
    [Idem-state-name]:
       aws.iam.instance_profile.search:
          - name: 'string'
          - resource_id: 'string'

Response Syntax:
    The following fields will be returned to the `new_state` of the response.

      - name: 'string'
      - resource_id: 'string'
      - arn: 'string'
      - path: 'string'
      - roles:
        - RoleName: 'string'
        - RoleArn: 'string'
        - RoleId: 'string'
      - Tags:
        - Key: 'string'
          Value: 'string'

Examples:

    Input state file:

    .. code-block:: sls

        instance-profile-test-search:
          aws.iam.instance_profile.search:
            - name: instance-profile-test-search
            - resource_id: instance-profile-test-search

    Sample response:
          - name: inst-profile-1
          - resource_id: inst-profile-1
          - arn:
          - path: /aws-service-inst-profile/
          - roles:
            - RoleName: role-1
            - RoleArn: arn:aws:iam::000000000000:role/idem-test-role-09e61fc9-d078-48a6-b297-8969a509c7cd
            - RoleId: tpx1mo6cjpsvh95ex5mq
          - Tags:
            - Key: test-1
              Value: test-1-val
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.iam.instance_profile](https://docs.idemproject.io/idem-aws/en/latest/ref/states/iam/instance_profile.html).
