---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Deploying, managing, and removing {{site.data.keyword.logs_full_notm}} extensions (WIP)
{: #extensions-mgmt}

{{site.data.keyword.logs_full}} offers a number of data extensions. Each extension contains a set of predefined items – alerts, parsing rules, dashboards, saved views, actions, and so on. To be used, these extensions need to be deployed into your {{site.data.keyword.logs_full_notm}} instance. Once deployed they can be managed or removed, as required.
{: shortdesc}

To learn more about extensions, see [About {{site.data.keyword.logs_full_notm}} extensions.](/docs/cloud-logs?topic=cloud-logs-extensions)

## Deploying an extension
{: #ext_deploy}

To deploy an extension:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Integrations icon** ![Integrations icon](/icons/integrations.svg "Integrations") > **Extensions**.

4. Click **Deploy** on the tile of the extension you want to deploy.

5. Select the *Applications* and *Subsystems* where the extension will be applied.

6. By default everything defined in the extension will be deployed. You can remove the checkmark for any item you don't want to deploy.

7. Click **+ Deploy** to install the extension in your {{site.data.keyword.logs_full_notm}} instances.


## Modifying a deployed extension dashboard
{: #ext_modify}

After deploying an extension you can change a deployed custom dashboard by [modifying the dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards#modify_dashboard).

You can also change the *Applications* and *Subsystems* associated with the deployed extension.

If you have modified assets deployed by the extension (for example, dashboards), make sure that you keep a copy of those assets by editing them and saving them with **Save As** before updating the *Applications* and *Subsystems* associated with the deployed extension. When you update the *Applications* and *Subsystems* values in the extension, all assets are updated with the default extension assets and are associated with the new *Applications* and *Subsystems* values.
{: attention}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Integrations icon** ![Integrations icon](/icons/integrations.svg "Integrations") > **Extensions**.

4. Click the tile of the deployed extension you want to modify.

5. Change the *Applications* and *Subsystems* values as needed.

6. Click **Update**.

## Removing an extension
{: #ext_remove}

To remove an extension you already have deployed in your instance:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Integrations icon** ![Integrations icon](/icons/integrations.svg "Integrations") > **Extensions**.

4. Click the tile of the deployed extension you want to remove.

5. Click **- Remove**.

6. Select if your want to delete or keep the deployed assets.

   If you choose to delete the deployed assets, the extension is deleted along with the assets deployed by the extension in your {{site.data.keyword.logs_full_notm}} instance.

   If you choose to keep the deployed assets when deleting the extension, the assets deployed by the extension will remain in your {{site.data.keyword.logs_full_notm}} instance, but will no longer be associated with the extension. If you deploy the extension again, a new copy of the extension will be deployed and the assets previously deployed will remain in your {{site.data.keyword.logs_full_notm}} instance and will not be overwritten.

7. Click **Remove**.
