---
title: "azure.subscription.subscriptions"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
**Autogenerated function**

Delete Subscription. This state disables the subscription and deletes respective alias.
Once subscription is in disabled state, after 90 days it gets deleted automatically.

Args:
    name(str): The identifier for this state.
    alias(str): The alias name of the subscription to delete.

Returns:
    Dict

Examples:

    .. code-block:: sls

        subscription_is_absent:
          azure.subscription.subscriptions.absent:
            - name: value
            - alias: value
```
{{< /tab >}}

{{< tab "describe" >}}

```
**Autogenerated function**

Describe subscriptions in a way that can be recreated/managed with the corresponding "present" function

Lists all subscriptions.

Returns:
    Dict[str, Any]

Examples:

    .. code-block:: sls

        $ idem describe azure.subscription.subscriptions
```
{{< /tab >}}

{{< tab "present" >}}

```
**Autogenerated function**

Create or update Subscription

Args:
    name(str): The identifier for this state.
    alias(str): The alias name of the subscription to create or update. Can include alphanumeric,
      underscore, parentheses, hyphen, period (except at end), and Unicode characters that match
      the allowed characters.Regex pattern: ^[-\w\._\(\)]+$.
    billing_scope: billing scope associated with billing account id and enrollment account id to create subscription
    display_name: subscription display name
    workload: type of workload where subscription needs to be created. Can be Production/DevTest
    resource_id: resource unique id

Returns:
    Dict

Examples:

    .. code-block:: sls

    azure.subscription.subscriptions.present:
        - name: create_subscription_3
        - alias: dupSubTest
        - billing_scope: /providers/Microsoft.Billing/billingAccounts/{billingAccountID}/enrollmentAccounts/{enrollmentAccountId}}
        - display_name: Subscription Display Name
        - workload: Production
```
{{< /tab >}}

{{< /tabs >}}

