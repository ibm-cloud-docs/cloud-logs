---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-24"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Using Livetail
{: #livetail}

{{site.data.keyword.logs_full}} provides a Livetail view allowing you to view the data ingested by {{site.data.keyword.logs_full_notm}} as the data is received.
{: shortdesc}

## Accessing Livetail
{: #livetail-access}

To access Livetail:

1. In the console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list**.

2. Select your instance of {{site.data.keyword.logs_full_notm}}.

3. In the {{site.data.keyword.logs_full_notm}} navigation, click the **Livetail** icon ![Livetail icon](/icons/livetail.svg "Livetail").

## Livetail options
{: #livetail-options}

The following options are available when interacting with Livetail.

| Option | Usage |
|--------|-------|
| **Start** | Click to start the display of Livetail data. When selected Livetail data starts being displayed the option changes to **Pause** |
| **Pause** | Pauses running Livetail data. When seected the Livetail data pauses being displayed and the option changes to **Start** |
| **Clear** | Deletes the displayed data to the point when **Clear** is clicked. If **Clear** is clicked when the Livetail is still running, new data is displayed as it is ingested. |
| **Prettify** | Structures the displayed data as formatted objects. When selected the option changes to **Unprettify**.|
| **Unprettify** | Structures the displayed data as raw data lines. When selected the option changes to **Prettify**. |
| **Choose fields** | Limits the displayed data to the specified fields. One or more fields can be specified.
| **All Applications** | Limits the displayed data to the selected [application names](/docs/cloud-logs?topic=cloud-logs-metadata#md-app-name). |
| **All Subsystems** | Limits the displayed data to the selected [subsystem names](/docs/cloud-logs?topic=cloud-logs-metadata#md-sys-name). |
{: caption="Livetail options" caption-side="bottom"}

## Querying data
{: #livetail-query}

You can use grep, exact text, or a regex expression to search for specific data within the Livetail.

The following example shows how text and regex searches can be combined. First, a case-insensitive regex search of `mydata.io` is done. The search results are then filtered with an exact text search of `schemas`. Finally, a case-insensitive search of `TimE` is applied to the filtered results.

```text
| grep -i mydata\.io | grep "schemas" | grep -i TimE
```
{: codeblock}

