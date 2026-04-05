---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-05"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Configuring archive retention tags to manage data retention
{: #retention-tags}

In {{site.data.keyword.logs_full_notm}}, you can use {{site.data.keyword.cos_full_notm}} object tags to manage automatically how long log data is available for search in the data bucket.
{: shortdesc}

After you configure the data bucket for an {{site.data.keyword.logs_full_notm}} instance, log data is stored in the bucket and you can search the data. You are responsible for the maintenance of the bucket and the data stored in the bucket.

By default, data in the bucket is kept indefinitely.

To delete objects automatically after a defined period (from the object creation date), you can configure {{site.data.keyword.cos_full_notm}} expiration rules (lifecycle policies) to manage automatically the deletion of object files based on number of days since the object creation date. However, if you want a more granular control on the data that is kept for search in the data bucket and delete files automatically by using different retention periods on the data, you must configure in {{site.data.keyword.cos_full_notm}} expiration rules that limit the scope by using the object tag `ICL_ARCHIVE_RETENTION` and use the tag values that you define in your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Deleting files from the data bucket](/docs/cloud-logs?topic=cloud-logs-about-bucket#about-bucket-cl-data-bucket-maintain).

Archive retention tags are attached to object files that are uploaded into the data bucket after they are defined and enabled in the {{site.data.keyword.logs_full_notm}} instance.


## Prerequisites
{: #retention-tags-prereqs}

- An {{site.data.keyword.cloud_notm}} account.
- An {{site.data.keyword.logs_full_notm}} instance.
- Permissions in {{site.data.keyword.logs_full_notm}} to configure archive retention tags. You need the role **Manager** that includes the action **logs.archive-retention.manage** and **logs.archive-retention.read**. For more information, see [Getting started with IAM](/docs/cloud-logs?topic=cloud-logs-iam).

## Configure custom archive retention tags in {{site.data.keyword.logs_full_notm}}
{: #retention-tags-step1}
{: step}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. In the dashboard, click **Data Pipeline** > **Retention Tags**.

    The Archive retention tags page opens.

    ![Archive retention tags.](images/archive-retention-tags.png "Archive retention tags."){: caption="Archive retention tags." caption-side="bottom"}

3. Click **Edit** and enter values for 1 or more retention tags.

    Define per tag how data is classified. You can define your own values and criteria.{: important}

    If you plan to have different retention policies per TCO data pipeline, enter the following values:

    - **high** for *Retention Tag 1*, where high represents data processed through the {{site.data.keyword.frequent-search}} TCO data pipeline.
    - **medium** for *Retention Tag 2*, where medium represents data processed through the {{site.data.keyword.monitoring}} TCO data pipeline.
    - **low** for *Retention Tag 3*, where low represents data processed through the {{site.data.keyword.compliance}} TCO data pipeline.

    If you plan to have different retention policies per log priority, enter the following values:

    - **critical** for for *Retention Tag 1*, where critical represents data that have a log priority set to `debug` or `verbose`.
    - **info** for for *Retention Tag 2*, where info represents data that have a log priority set to `info` or `warning`.
    - **debug** for for *Retention Tag 3*, where debug represents data that have a log priority set to `error` or `critical`.

4. Click **Activate** to enable this feature.


After you activate archive retention tags, consider the following information:

- This feature cannot be disabled.

    Retention tags cannot be deactivated once enabled.
    {: attention}

- Custom tags are available to configure TCO policies.

- You can modify the retention tags by clicking **Edit**.

- New files in your data bucket are tagged with the custom tag `ICL_ARCHIVE_RETENTION`. The value of the tag is set to a custom tag value or to `default`.


## Create expiration rules in {{site.data.keyword.cos_full_notm}}
{: #retention-tags-step2}
{: step}

To create expiration rules, see [Deleting stale data with expiration rules](/docs/cloud-object-storage?topic=cloud-object-storage-expiry).


## Configure TCO policies
{: #retention-tags-step3}
{: step}

Once you configure your cx-data bucket in S3, set your Archive Retention Settings.
1. In your {{site.data.keyword.logs_full_notm}} navigation bar, click **Data Flow > Select Setup Archive**.
2. In the Archive Retention section, name Retention Periods 2, 3 and 4. You may opt for names "Short,"Intermediate," and "Long" as in the example below, or you many choose otherwise. The value for each period - the length of time data will be retained in a specific retention period - is managed by the s3 storage lifecycle defined in your AWS account.
3. Click ACTIVATE. You will receive a popup message that reads: "An archive retention policy has been added to the bucket-name Bucket successfully."

Note:
 - `Only once you have activated your archive retention settings will they appear in your TCO Quota Optimizer`.
 - `When modifying existing archive retention settings, the ACTIVATE button will be replaced with a SAVE button`.

 4. View your changes by navigating to **Data Flow > TCO Quota Optimizer**.




You can use the `default` tag to define a default expiration period that you can apply to data that is not explicitly managed through a custom object tag.



 ## TCO Override
 {: #retention-tags-TCO-Override}

 Configuring a TCO override replaces the TCO policy for the specified application-subsystem-severity combination, including any associated Archive Retention Tags. In these cases, the Archive Retention Tag is overridden and reverts to the default tag.

 When creating a new policy for your data retention in your TCO Quota Optimizer screen, you now have the option to define a lifecycle policy - the length of archieve retention for a specific group of logs, defined by application, subsystem, and severity.

### Impact
{: #retention-tags-impact}

This behavior directly impacts S3 lifecycle policies that depend on retention tags. If the tag is overridden to the default, lifecycle policies associated with specific tags, like 'Revenue,' may not be applied as intended, potentially resulting in unintended data deletion.

### Prevention
{: #retention-tags-prevention}

If you manage S3 Lifecycle Policies based on Archive Retention Tags, review and adjust overrides to prevent unintended data deletion.

### Example
{: #retention-tags-example}

- `TCO override is not in use: Retention Tag = revenue, Lifecycle Policy transitions data to Glacier after 30 days and deletes it from Glacier after 1 year`.
- `TCO override is in use: Retention Tag = default, Lifecycle Policy expires data after 60 days (if set to default)`.

## Create a New Policy
{: #retention-tags-new-policy}
Once you create your Archive Retention settings, create a new data retention policy.

1. In your {{site.data.keyword.logs_full_notm}} navigation bar, click **Data Flow > select TCO Quota Optimizer**.
2. Click +ADD NEW POLICY.

(Image)
3. Input POLICY NAME.
4. Define APPLICATIONS, SUBSYSTEMS and SEVERITY level.
5. Define PRIORITY.
Note:
-  `If data is marked as ‘blocked’, it will not be archived`.
- `Only data marked as priority ‘High’, ‘Medium’, or ‘Low’ is archived. Only this data is eligible for additional archive retention settings`.

6. Define ARCHIVE RETENTION Settings

Notes:
- `When you add an archive retention policy, logs meeting the established criteria (application, subsystem, and severity level) will be retained in your archive for the period of time associated with the policy`.
- `If you do not specify your retention policy, logs meeting the established criteria will be retained in your archive for the default period of time`.

(Image)
