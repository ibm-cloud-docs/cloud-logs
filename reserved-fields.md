---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Reserving fields
{: #reserved-fields}

{{site.data.keyword.logs_full}} indexes your data in ingestion order. After the maximum number of stored fields is reached, more fields might not be available for querying. With reserved fields, you can explicitly define important fields that you always want to query while still allowing {{site.data.keyword.logs_full_notm}} to dynamically add other fields as they are encountered.
{: shortdesc}

With reserved fields, you can:

* Ensure that important fields are always available for queries.

* Specify the data type for each field to make storage and querying more efficient.

* Define the fields that you need so those fields are available for improved query performance.

When data is ingested, fields are mapped in an index. The automatic mapping dynamically adds fields, but those fields might be associated with an undesired data type if a field of the same name is ingested first. With reserved fields, you predefine fields and their associated data type.

Reserved fields are applied each day at 00:00 UTC when the daily index is created. Reserved fields are included in the [daily index limit](/docs/cloud-logs?topic=cloud-logs-priority-insight-index-limits).

## Data types
{: #rf-datatypes}

Each reserved field is associated with a data type.

| Data type | Description | Example JSON usage |
|-----------|-------------|--------------------|
| `boolean` | Represents a `true` or `false` value. The `boolean` data type is commonly used for logical checks and conditions. | `true` or `false` |
| `string` | A sequence of characters. The `string` data type is often used for text identifiers or alphanumeric data. Stored in UTF-8 format. | `"example text"` |
| `number` | A numeric value. The `number` data type can be either an integer or a floating-point value. The value can be used for calculations or measurements. | `123` or `45.67` |
{: caption="Field data types" caption-side="bottom"}

## Required permissions
{: #rf-howto-iam}

To configure reserved fields, you must have an IAM role with the required actions:

| Action | Description |
|--------|-------------|
| `logs.reserved-field.read` | View reserved fields. |
| `logs.reserved-field.manage` | Update, delete or create reserved fields. |
{: caption="IAM actions required for reserved fields" caption-side="bottom"}

## Defining reserved fields
{: #rf-howto}

You can define reserved fields in two ways:

* By selecting fields previously ingested, mapped, and indexed by {{site.data.keyword.logs_full_notm}}.

* By manually defining fields and their associated data type.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Data pipeline icon** ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Reserved fields**.

4. Click **+ Add field**.

5. In **Field Name**, enter a field name.

   * If the field is mapped by {{site.data.keyword.logs_full_notm}}, you can select the field and mapping from the list.

   You can also click **View full list** to see all the fields currently mapped. You can limit the list to a selected time period. Up to 7 days of fields that are processed by {{site.data.keyword.logs_full_notm}} are available.
   {: tip}

   * If the field is not mapped, you can enter a field name and select the **Type** to be associated with the field.

6. Click **Save**.

## Adding multiple reserved fields at the same time
{: #rf-maint}

If you would like to add multiple reserved fields that are mapped by {{site.data.keyword.logs_full_notm}} at the same time, you can use the **Add in bulk** option.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Data pipeline icon** ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Reserved fields**.

4. Click **Add in bulk**.

5. Select the existing fields that you want to add as reserved fields.

   You can search for fields as well as limit the search to a specific time period.
   {: tip}

6. Click **Add to list** to add the selected fields as reserved fields.

## Maintaining reserved fields
{: #rf-maint}

You can **Edit** a reserved field and **Remove** reserved fields you no long need.

For example, you might need to edit a reserved field if you find the data type associated with the field is incorrect.
