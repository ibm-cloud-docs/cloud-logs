---

copyright:
  years:  2024
lastupdated: "2024-11-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Generating an IAM access report
{: #iam-access-report}

You can generate an {{site.data.keyword.iamlong}} (IAM) access report listing users, access groups, and service IDs that have access to the selected resource. You must have the Administrator role on the selected resource to view the report.
{: shortdesc}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed. 

4. For the instance where you want to generate an access report, click the **Actions** icon ![Actions icon](/icons/action-menu-icon.svg "Actions") > **Access report**.

   The generated report includes only details about the selected instance.
   {: note}

5. Click **Download CSV** to download the report as a CSV file or **Download JSON** to download the report as a JSON file.

For more information about {{site.data.keyword.iamlong}} access reports, see [Auditing access to resources](/docs/account?topic=account-access-report).


