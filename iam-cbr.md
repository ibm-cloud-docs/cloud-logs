---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Protecting resources with context-based restrictions
{: #iam-cbr}

[Context-based restrictions](/docs/account?topic=account-context-restrictions-whatis&interface=ui) provide a way for administrators to limit access to resources. What if certain data must be accessed from trusted networks only? A properly configured policy restricts all access to data unless the request originates from an approved [network zone](/docs/account?topic=account-context-restrictions-whatis&interface=ui#network-zones-whatis) and endpoint type (public, private, or direct).
{: shortdesc}

## Using context-based restrictions
{: #setting-cbr}

A [context-based restriction](/docs/account?topic=account-context-restrictions-whatis&interface=ui) is comprised of a **rule** and one or more **contexts** (network zones and/or endpoint type). These restrictions do not replace IAM policies, but simply check that a request is coming from an allowed context, such as a range of IP addresses, VPCs, or service references.

A user must have the `Administrator` role on a service to create, update, or delete rules.  A user must have either the `Editor` or `Administrator` role to create, update, or delete network zones.

You can learn more about how context-based restrictions work in the [detailed documentation](/docs/account?topic=account-context-restrictions-create&interface=ui), or you can follow these tutorials:

- [Restricting access to {{site.data.keyword.logs_full_notm}} from a network zone](/docs/cloud-logs?topic=cloud-logs-iam-cbr-tutorial).
- [Restricting access to integrated services from {{site.data.keyword.logs_full_notm}} using context-based restrictions](/docs/cloud-logs?topic=cloud-logs-iam-cbr-tutorial-integrated-services)

## Protecting {{site.data.keyword.logs_full_notm}} resources
{: #resources-types-cbr}

You can create CBR rules to protect specific regions, resource groups and instances.

Instance
:   Protects a specific {{site.data.keyword.logs_full_notm}} instance. If you select an instance in your CBR rule, only traffic from resources in the network zones that you associate with the rule can interact with that instance.

Region
:   Protects {{site.data.keyword.logs_full_notm}} resources in a specific region. If you select a region in your CBR rule, then only traffic from resources in the network zones that you associate with the rule can interact with resources in that region.

Resource group
:   Protects {{site.data.keyword.logs_full_notm}} resources in a specific resource group.

## Creating network zones
{: #create-network-zone}

A network zone represents an allowlist of IP addresses where an access request is created. It defines a set of one or more network locations that are specified by the following attributes:

* IP addresses, which include individual addresses, ranges, or subnets.
* VPCs
* Service references, which allow access from other {{site.data.keyword.cloud_notm}} services.

### Creating network zones from the console
{: #create-network-zone-console}
{: ui}

1. Determine the resources that you want add to your allowlist.
2. Follow the steps to [create context-based restrictions in the console](/docs/account?topic=account-context-restrictions-create). Add the {{site.data.keyword.logs_full_notm}} service as a service reference to your network zones to allow {{site.data.keyword.logs_full_notm}} access to services and resources in your account.


## Creating rules
{: #create-rules}

Define rules to protect access to resources in your account. The contexts that you define in your rules determine how the resources in your network zones (allowlists) can interact with the resources defined in the rule.

### Creating rules from the console
{: #create-rule-console}
{: ui}

1. [Review the available contexts](#resources-types-cbr) and determine the rules that you want to create.

2. Follow the steps to [create context-based restrictions in the console](/docs/account?topic=account-context-restrictions-create).


## Limitations
{: #cbr-limitations}

- After you create, enforce, or disable enforcement of a rule, it might take up to 10 minutes for the change to take effect.
- An account is limited in the number of rules and network zones that can be supported. For more details see [Context-based restrictions limits](/docs/account?topic=account-context-restrictions-whatis#cbr-limits).
