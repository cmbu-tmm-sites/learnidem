---
title: "aws.ec2.snapshot"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deregisters the specified Snapshot

    Deletes the specified snapshot. When you make periodic snapshots of a volume, the snapshots are incremental, and
    only the blocks on the device that have changed since your last snapshot are saved in the new snapshot. When you
    delete a snapshot, only the data not needed for any other snapshot is removed. So regardless of which prior
    snapshots have been deleted, all active snapshots will have access to all the information needed to restore the
    volume. You cannot delete a snapshot of the root device of an EBS volume used by a registered AMI. You must
    first de-register the AMI before you can delete the snapshot. For more information, see Delete an Amazon EBS
    snapshot in the Amazon Elastic Compute Cloud User Guide.

    Args:
        name (str): An Idem name of the snapshot.
        resource_id(str): The snapshot ID.

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            resource_is_absent:
              aws_auto.ec2.snapshot.absent:
                - name: value
                - resource_id: value
                - snapshot_id: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
Describe the resource in a way that can be recreated/managed with the corresponding "present" function

Gets information about the AWS Snapshot(s)

Returns:
    Dict[str, Any]

Examples:
    .. code-block:: bash

        $ idem describe aws_auto.ec2.snapshot
```
{{< /tab >}}

{{< tab "present" >}}

```
Register an AWS Snapshot.

    Creates crash-consistent snapshots of multiple EBS volumes and stores the data in S3. Volumes are chosen by
    specifying an instance. Any attached volumes will produce one snapshot each that is crash-consistent across the
    instance. Boot volumes can be excluded by changing the parameters.  You can create multi-volume snapshots of
    instances in a Region and instances on an Outpost. If you create snapshots from an instance in a Region, the
    snapshots must be stored in the same Region as the instance. If you create snapshots from an instance on an
    Outpost, the snapshots can be stored on the same Outpost as the instance, or in the Region for that Outpost.

    Args:
        name (str):
            An Idem name for the snapshot resource.

        resource_id (str, optional):
            AWS Snapshot snapshot_id.

        volume_id (str, required):
            AWS Volume volume_id of the volume the snapshot is to be created from.

        description (str, optional):
            A description propagated to every snapshot specified by the instance. Defaults to None.

        outpost_arn (str, optional):
            The Amazon Resource Name (ARN) of the Outpost on which to create the local snapshots.   To
            create snapshots from an instance in a Region, omit this parameter. The snapshots are created in
            the same Region as the instance.   To create snapshots from an instance on an Outpost and store
            the snapshots in the Region, omit this parameter. The snapshots are created in the Region for
            the Outpost.   To create snapshots from an instance on an Outpost and store the snapshots on an
            Outpost, specify the ARN of the destination Outpost. The snapshots must be created on the same
            Outpost as the instance.   For more information, see  Create multi-volume local snapshots from
            instances on an Outpost in the Amazon Elastic Compute Cloud User Guide. Defaults to None.

        tags (dict, optional):
            Dict in the format of ``{tag-key: tag-value}`` to associate with the Snapshot.

            * Key (str):
                The key name that can be used to look up or retrieve the associated value.

            * Value (str):
                The value associated with this tag. For example tags with the key name of Name could have
                the AWS snapshot_id as the associated value.

    Returns:
        Dict[str, Any]

    Examples:
        .. code-block:: sls

            resource_is_present:
              aws_auto.ec2.snapshot.present:
                - name: some-snapshot-ARN
                - resource_id: some-snapsshot-ARN
                - volume_id: some-volume-ARN
                - tags:
                    - Key: name
                      Value: ONE
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.ec2.snapshot](https://docs.idemproject.io/idem-aws/en/latest/ref/states/ec2/snapshot.html).
