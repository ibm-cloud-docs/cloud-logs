---

copyright:
  years:  2024
lastupdated: "2024-11-28"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why am I receiving a warning message when logging into helm to install the {{site.data.keyword.agent}}?
{: #ts-helm-proxy}
{: troubleshoot}
{: support}

When logging in to the helm registry you receive a message that using a password on the CLI is insecure.
{: shortdesc}

When running a command similar to the following to log in to the helm registry:
{: tsSymptoms}

```text
helm registry login -u iambearer -p $(ibmcloud iam oauth-tokens --output json | jq -r .iam_token | cut -d " " -f2) icr.io
```
{: pre}

A message similar to the following is returned:

```text
WARNING: Using --password via the CLI is insecure. Use --password-stdin.
Error: Get "https://icr.io/v2/": unauthorized: {"errors":[{"code":"UNAUTHORIZED","message":"Authorization required. See https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-auth-req","detail":"Authorization required. See https://cloud.ibm.com/docs/Registry?topic=Registry-troubleshoot-auth-req"}]}
```
{: screen}

Your environment might have a proxy in place that is dropping the headers that include the access token.
{: tsCauses}

Do the following to determine if a proxy is in place and install the {{site.data.keyword.agent}} a different way or resolve your proxy configuration.
{: tsResolve}

1. Run the following command to determine if a proxy is in place and is causing the problem.

   ```sh
   curl -v https://icr.io/v2/
   ```
   {: pre}

2. If the command returns `401`, use the [Cloud Shell](/docs/cloud-shell) to deploy the {{site.data.keyword.agent}} using the {{site.data.keyword.agent}} deployment steps.
