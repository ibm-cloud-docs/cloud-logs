---

copyright:
  years:  2024
lastupdated: "2024-10-17"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why is the UI displaying a message that a bucket isn't connected? 
{: #ts-cos-config}
{: troubleshoot}
{: support}

The {{site.data.keyword.logs_full}} UI displays an error message that a bucket is not connected when a bucket is connected to the {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

You get the following error message: `You haven't connected a bucket yet`.
{: tsSymptoms}


After a recent update to the {{site.data.keyword.logs_full_notm}} service broker and UI, you might encounter an issue where the UI incorrectly shows "You haven't connected a bucket yet" for existing instances that have {{site.data.keyword.cos_full_notm}} (COS) buckets attached.
{: tsCauses}


To resolve this issue for affected instances, you can run a set of commands to update the instance, ensuring the correct values are reflected in the UI.
{: tsResolve}

Follow the steps below to resolve this issue for existing instances with attached COS buckets.

1. Log in to your {{site.data.keyword.cloud_notm}} account through the CLI.
    - If you don’t have the CLI installed, refer to [Installing the IBM Cloud CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. Install [`jq`](https://jqlang.github.io/jq/download/){: external} to parse the JSON response from the CLI:

   - On macOS:
        ```bash
        brew install jq
        ```
   - On Ubuntu/Debian:
        ```bash
        sudo apt-get install jq
        ```
   - On RHEL/CentOS:
        ```bash
        sudo yum install jq
        ```

3. Retrieve the currently configured retention period for the instance by running the following command:

    ```bash
    ibmcloud resource service-instance $GUID --output json | jq '.[].extensions.retention_period'
    ```
    {: codeblock}

    Replace `$GUID` with the actual instance GUID.

4. Update the instance by using the following command:

    ```bash
    ibmcloud resource service-instance-update $GUID -p '{"retention_period": "<retention_period>"}'
    ```
    {: codeblock}

    Replace `<retention_period>` with the value retrieved in step 3.

5. Verify that the UI now displays the correct bucket attachment status.

## Next steps
{: #next-steps}

After running the above commands, the UI will correctly reflect the bucket. If further issues persist, [contact IBM Cloud support](/docs/get-support) for assistance.


