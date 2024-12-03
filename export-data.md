---

copyright:
  years:  2024
lastupdated: "2024-12-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


#  Exporting data
{: #export-data}

In {{site.data.keyword.logs_full}}, you can export raw data using the **Settings** > **Export** option in the **Logs** section of the UI.
{: shortdesc}


## Export data from a view in the UI
{: #query-data-ui-1}

In the Explore **Logs** page, complete the following steps to export data for a selected period of time:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click ![Explore logs icon](/icons/explore.svg "Explore logs") **Logs**. Then click  ![Settings icon](/icons/setting.svg "Settings icon") **Settings**  > **Export**.

4. Select the file type for the exported data. Valid options are `JSON` and `CSV`.

5. Enter the name of the file where data is exported.

6. Select an export time range.

7. Select the number of pages that you want to export.

    You can export up to the first 20 pages, that is, aproximately 2000 logs records.
    {: note}

8. Select the filter applied to the export.

    Choose `All data` to export all data available for a period of time.

    Choose `Current view preferences` to export data filtered by the view that is selected.

9. Click **Export**.
