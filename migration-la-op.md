---

copyright:
  years:  2024
lastupdated: "2024-09-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migration steps for instances that collect application and operational logs
{: #migration-la-op}


To migrate {{site.data.keyword.la_full_notm}} instances that collect operational and application logs,

- You must provision {{site.data.keyword.logs_full_notm}} instances in the account to replace the existing {{site.data.keyword.la_full_notm}} instances.

- You must also configure your data sources to send data to these {{site.data.keyword.logs_full_notm}} instances.

    You can configure an Logging agent on supported platforms such as Kubernetes clusters, Red Hat OpenShift clusters, and Linux servers, or send data directly to {{site.data.keyword.logs_full_notm}} by using the ingestion endpoint. Sources sending logs can be in {{site.data.keyword.cloud_notm}}, on-prem, or running in another cloud service.

The Migration tool migrates instances replicating the current account architecture.


To migrate {{site.data.keyword.la_full_notm}} instances, complete the following steps for each instance:

1. Run the migration tool to collect information about what instances need to be migrated and their resources.

    ```text
    ibmcloud logging migrate generate-terraform --scope account --service logdna
    ```
    {: pre}


2. Migrate an instance by running one of these commands:

    * To generate terraform scripts that you can modify, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --terraform
       ```
       {: pre}

    * To migrate an instance by applying Terraform, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --terraform -f
       ```
       {: pre}

    * To migrate an instance directly without Terraform, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --api
       ```
       {: pre}

    You must migrate all your {{site.data.keyword.la_full_notm}} instances that collect platform logs before you use the Migration tool to configure {{site.data.keyword.logs_routing_full_notm}} in the account.{: important}

3. Manually configure notification channels such as email.

   {{site.data.keyword.logs_full_notm}} alerting is done by using the {{site.data.keyword.en_full_notm}} service.
   {: note}

4. Configure the {{site.data.keyword.agent}} to send logs.

    - [Managing the Logging agent for Linux](/docs/cloud-logs?topic=cloud-logs-agent-linux).
    - [Managing the Logging agent for IBM Cloud Kubernetes Service clusters](/docs/cloud-logs?topic=cloud-logs-agent-std-cluster).
    - [Managing the Logging agent for Red Hat OpenShift on IBM Cloud clusters](/docs/cloud-logs?topic=cloud-logs-agent-openshift).
    - [Using the Logging agent to collect and route (r)Syslog messages](/docs/cloud-logs?topic=cloud-logs-agent-rsyslog).

5. Validate that the new configuration is working for your requirements.

6. Migrate IAM permissions. For more information, see [Migrating IAM permissions](/docs/cloud-logs?topic=cloud-logs-migration-iam).

7. After you validate your configuration is operating as required, delete your {{site.data.keyword.la_full_notm}} instances and your legacy configurations to send data.
