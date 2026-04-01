---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-01"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


#  Archive Retention Tags
{: #retention-tags}

In {{site.data.keyword.logs_full_notm}}, you can work with retention tags to get an extra layer of granularity for your data retention, in addition to our TCO Optimizer. Using our new Archive Retention feature, you can now control and modify the lenth of time your logs are archived.
{: shortdesc}

## Overview
{: #retention-tags-overview}

When creating a new policy for your data retention in your TCO Quota Optimizer screen, you now have the option to define a lifecycle policy - the length of archieve retention for a specific group of logs, defined by application, subsystem, and severity.

Users can choose between 4 default retention periods: default, short, intermediate, or long. The names and values for the latter three are subjective and determined by the tag names set by the user in his/her s3 bucket configuration. While one user may define a "short" retention period as 3 days, another may define this period as 15 days. Another user may choose to change the name of the "short" retention period to "minimum."
(image)


Note:
Only new archived files are affected by these new settings.
Files created before the new lifecycle policy have no retention tag and are not changed retroactively. The data retention policy that applied to them before the new lifecycle policy - default or defined - will continue to apply even after the new settings are put in place.

## Configuration
{: #retention-tags-configuration}

1. Create an s3 bucket for configuration.
2. Configure GetObjectTagging and PutObjectTagging permissions.
- `Search S3 in your AWS search bar and select this service`.
- `Find and click the bucket of choice for storing the archive`.
- `Navigate to the permissions tab. Edit the Bucket Policy`.
(Image)

- `Paste the following code and update the name of your bucket:`

(Code)

- `Click Save`.

3. (Image)

## Create a Lifecycle Policy
{: #retention-tags-create-a-lifecycle-policy}

The following section demonstrates one method of creating a lifecycle policy using AWS CLI. The example below sets a policy to remove archive files with the retention "short" after 15 days.

1. Define a policy in a local lifecycle.jason file.
(Code)
2. Apply the policy
(code)

Note:
- This command will completely override the current policy of the bucket, if exists.
- If you wish to append your existing policy, proceed with this command first and only then update lifecycle policy.

3. Verify that the policy has been changed.
(Code)

## Define Archive Retention Settings
{: #retention-tags-define-archive-retention-settings}

Once you configure your cx-data bucket in S3, set your Archive Retention Settings.
1. In your {{site.data.keyword.logs_full_notm}} navigation bar, click **Data Flow > Select Setup Archive**.
2. In the Archive Retention section, name Retention Periods 2, 3 and 4. You may opt for names "Short,"Intermediate," and "Long" as in the example below, or you many choose otherwise. The value for each period - the length of time data will be retained in a specific retention period - is managed by the s3 storage lifecycle defined in your AWS account.
3. Click ACTIVATE. You will receive a popup message that reads: "An archive retention policy has been added to the bucket-name Bucket successfully."

Note:
 - `Only once you have activated your archive retention settings will they appear in your TCO Quota Optimizer`.
 - `When modifying existing archive retention settings, the ACTIVATE button will be replaced with a SAVE button`.

 4. View your changes by navigating to **Data Flow > TCO Quota Optimizer**.

 ## TCO Override
 {: #retention-tags-TCO-Override}

 Configuring a TCO override replaces the TCO policy for the specified application-subsystem-severity combination, including any associated Archive Retention Tags. In these cases, the Archive Retention Tag is overridden and reverts to the default tag.

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

## Previously Archived Files
{: #retention-previously-archived-files}

Files created before the new lifecycle policy have no retention tag and are not changed retroactively when you establish a new retention policy. The data retention policy that applied to them beforehand - whether default or defined - will continue to apply even after your new settings are put in place.
(code)

## Additional Resources
{: #retention-S3-bucket-configuration}

- S3 Bucket Configuration

## Support
