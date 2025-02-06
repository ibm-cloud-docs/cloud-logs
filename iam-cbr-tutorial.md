---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-06"


keywords: tutorials, cbr, firewall, allowlist, rules
subcollection: cloud-logs
content-type: tutorial
completion-time: 10m

---

{{site.data.keyword.attribute-definition-list}}

# Restricting access to {{site.data.keyword.logs_full_notm}} from a network zone
{: #iam-cbr-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

In this tutorial, you will set up [context-based restrictions](/docs/cloud-logs?topic=cloud-logs-iam-cbr) that prevent any access to the {{site.data.keyword.logs_full_notm}} instance unless the request originates from an allowed network zone.
{: shortdesc}

## Before you begin
{: #iam-cbr-tutorial-prereqs}

Before you use [context-based restrictions](/docs/cloud-logs?topic=cloud-logs-iam-cbr) with an {{site.data.keyword.logs_full_notm}} instances you need:

- An instance of {{site.data.keyword.logs_full_notm}}
- A role of `Administrator` for context-based restrictions

## Navigate to the context-based restrictions console
{: #iam-cbr-tutorial-console}
{: step}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click **Manage** > **Context-based restrictions**.

## Create a new rule
{: #iam-cbr-tutorial-new-rule}
{: step}

1. Click **Rules**.
2. In the service section, select **{{site.data.keyword.logs_full_notm}}** from the menu.
3. In the APIs section, select **All** in Service APIs.

## Scope the rule
{: #iam-cbr-tutorial-scope}
{: step}

Now, you can choose the resources where you want to apply the context-based restrictions. You can specify a particular instance, or you can apply the restrictions to all {{site.data.keyword.logs_full_notm}} instances.

In this tutorial, you will choose a specific {{site.data.keyword.logs_full_notm}} instance.

1. In the resources section, select **specific resources**.
2. Click **Add a condition** and select the **Service instance** option from the menu.
3. Select the {{site.data.keyword.logs_full_notm}} instance you want the rule to affect.
4. Click **Continue**.

![Scope the rule](/images/logs-cbr-tutorial/cbr_1.png){: caption="Scope the rule"}

## Create a network zone
{: #iam-cbr-tutorial-network-zone}
{: step}

Now that you know which resources the rule will affect, you need to define what the rule will allow. To do this, create a new _network zone_ and apply it to the rule.

1. In the network zone section, Click **Create +** .
2. Provide a meaningful name and description for the network zone.
3. Add the IP addresses to the `Allowed IP addresses` field. Only these IP addresses will be permitted to interact with the {{site.data.keyword.logs_full_notm}} instance you selected in the previous step.

   ![Create network zone](/images/logs-cbr-tutorial/create_nw_zone.png){: caption="Create a network zone"}

5. Click **Next** and then **Create**.
6. Select the newly created network zone and click **Add**.
7. Click **Continue**.

## Describe your rule
{: #iam-cbr-tutorial-describe-rule}
{: step}

In the final step, you can add a description for the rule and choose how you want to enforce it. Once you've made your selections, click **Create**.

![Scope the rule](/images/logs-cbr-tutorial/cbr_3.png){: caption="Create your rule"}

After you create, enforce, or disable enforcement of a rule, it might take up to 10 minutes for the change to take effect.
{: note}

## Verify the rule
{: #iam-cbr-tutorial-verify}
{: step}

An easy way to verify whether the rule is working as expected is to try accessing your {{site.data.keyword.logs_full_notm}} instance's dashboard from IPs other than those allowed. You should be blocked from accessing the dashboard.

Next, try accessing the dashboard from an allowed IP address. You should be able to access the dashboard.

Another way to verify the rule is through [CLI commands](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-temp).
If you try to run commands from an IP address that is not allowed for the specified instance, the command will fail with a `forbidden` error message.

Example command : `ibmcloud logs alerts`

![Scope the rule](/images/logs-cbr-tutorial/cbr_4.png){: caption="Failed to execute command from a blocked IP"}
