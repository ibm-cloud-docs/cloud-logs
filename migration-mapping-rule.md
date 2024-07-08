---

copyright:
  years:  2024
lastupdated: "2024-04-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Mapping queries for views, alerts and dashboards
{: #migration-mapping-rule}

The {{site.data.keyword.logs_full}} migration tool maps queries as follows:
{: shortdesc}

This topic might change due to integration decisions that might be adopted from now to GA.
{: important}

## Metadata fields
{: #migration-mapping-fields}


Metadata fields are mapped by using a RegEX expression.


| {{site.data.keyword.la_full_notm}} field | {{site.data.keyword.logs_full_notm}} field |
|-------------|--------------------------------------------|
| `level`     | coralogix.metadata.severity                |
|             | coralogix.metadata.applicationName         |
|             | coralogix.metadata.subsystemName           |
{: caption="{{site.data.keyword.la_full_notm}} fields mapped to {{site.data.keyword.logs_full_notm}} fields" caption-side="bottom"}


For example:

```text
coralogix.metadata.applicationName:/wn-rest.*/
```
{: codeblock}


## Free text mapping
{: #free-text-mapping}

|  {{site.data.keyword.la_full_notm}} query |	{{site.data.keyword.logs_full_notm}} mapping |
|-------------|----------|
| abc	      | "abc"  |
| "abc"	      | "abc"  |
| "abc cdf"	  | "abc cdf" |
| 'abc'       | "abc" |
| 'abc'	      | "abc" |
| 'abc cdf'   | "abc cdf" |
| 'abc.ert sjdbsjk'	| "abc.ert sjdbsjk" |
|'return __GetElementTree(protocol, server' | "return __GetElementTree(protocol, server" |
{: caption="{{site.data.keyword.la_full_notm}} query mapped to {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

Free text with special characters such as `.`, `-`, `/` is map as-is always within double quotes `""``. No escape charcater is needed.

In Priority Insights, there is no upper and lower case difference in queries. If you use require queries that make this distinction, you need to review them manually and validate that the automated migration is still valid for you. {: note}



## TERM matching
{: #term-matching}

There are different use cases that need to be migrated:
1. Field search that matches anything that starts with a set of characters and includes lower case and upper case matches such as `action:iam` will map to `iam`, `iam1`, `IAM`, `IAM1`
2. Case-sensitive field search that matches anything that starts with a set of characters and the exact case such as `action:=iam` will map to `iam`, `iam1`
3. Exact field search that matches the exact value and includes lower case and upper case matches such as `name:==iam` Valid values are for example `iam` or `IAM`
4. Case-sensitive exact field search such as `action:===iam` Only `iam` is valid.



| {{site.data.keyword.la_full_notm}} action       | {{site.data.keyword.logs_full_notm}} mapping | Other information |
|-------------------|----------------------------------------------|------------|
| action:iam        | action.keyword:/`[Ii][Aa][Mm]`.*/              | Not implemented by the Migration Tool. It is not an efficient mapping. If your query matches anything that starts with a set of characters and must incluide lower case and upper case matches, you must manually modify the query that is migrated by the Migration Tool. |
| action:count	    | action.keyword:/count.*/                     | Implemented by the Migration Tool |
| action:IAM	    | action.keyword:/IAM.*/                       | Implemented by the Migration Tool |
| action:iam-g	    | action.keyword:/iam-g.*/                     | Implemented by the Migration Tool |
| action:"iam-g"	| action.keyword:/iam-g.*/                     | Implemented by the Migration Tool |
| action:'am-g'	    | action.keyword:/iam-g.*/                     | Implemented by the Migration Tool |
| action:=iam	    | action.keyword:/iam.*/                       | Implemented by the Migration Tool |
| action:==iam        | action.keyword:/`[Ii][Aa][Mm]`/              | Not implemented by the Migration Tool. It is not an efficient mapping. If your query matches anything that starts with a set of characters and must incluide lower case and upper case matches, you must manually modify the query that is migrated by the Migration Tool. |
| action:==iam      | action:"iam"                                 | Implemented by the Migration Tool |
| action:===iam     | action.keyword:/iam/                         | Implemented by the Migration Tool |
{: caption="{{site.data.keyword.la_full_notm}} action mapped to {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}


### Field search that matches anything that starts with a set of characters and includes lower case and upper case matches
{: #map-field-search}

In {{site.data.keyword.logs_full_notm}}, mapping searches that require to match case-sensitive data is not efficient and requires complex queries.

If your query matches anything that starts with a set of characters and must incluide lower case and upper case matches, you must manually modify the query that is migrated by the Migration Tool.
{: note}


Sample log:
- `field1:"abd def"`

Valid values in the data are:
- `abc defghj`
- `abc def`
- `abc def jki`

The rules implemented by the Migration Tool to map are:
- Add `.keyword` to the field name
- Use REGEX format for the query

Sample mapped query:

```text
field1.keyword:/abd def.*/
```
{: #codeblock}

### Case-sensitive field search that matches anything that starts with a set of characters and the exact case
{: #map-cs-field-search}

Sample logs:
- `field1:="abd def"`

Valid values in the data are:
- `abc defghj`
- `abc def`
- `abc def jki`

The rules implemented by the Migration Tool to map are:
- Add `.keyword` to the field name
- Use REGEX format for the query

Sample mapped query:

```text
field1.keyword:/abd def.*/
```
{: codeblock}

### Exact field search that matches the exact value and includes lower case and upper case matches
{: #map-exact-search}

In {{site.data.keyword.logs_full_notm}}, mapping searches that require to match case-sensitive data is not efficient and requires complex queries.

If your query matches anything that starts with a set of characters and must incluide lower case and upper case matches, you must manually modify the query that is migrated by the Migration Tool.
{: note}


The rules implemented by the Migration Tool to map are:
- Add double quotes
- Escape special characters
- Content of field muast be under 256 characters


Sample logs:
- `field1:=="abd def"`

Valid values in the data are :
- `abc def`
- `ABC def`
- `abc DEf`

```text
field1:"abd def"
```
{: codeblock}

### Case-sensitive exact field search
{: #map-cs-exact}

The rules implemented by the Migration Tool to map are:
- Add double quotes
- Escape special characters
- Content of field muast be under 256 characters


Sample logs:
- `field1:==="abd def"`

Valid value in the data is `abc def`.



Sample mapped query:

```text
field1:"abd def"
```
{: codeblock}

## Field Search
{: #map-field}

Term mapping rules apply based on `:`, `:=`, `:==` or `:===`
{: note}


| Field type           | {{site.data.keyword.la_full_notm}} query        | {{site.data.keyword.logs_full_notm}} mapping |
|----------------------|--------------------|--------------------------|
| JSON Field           | response:404	    | response:"404"
| Nested Field Search  |  user.id:12345	    | user.id:"12345"                 |
{: caption="Other {{site.data.keyword.la_full_notm}} fields mapped to {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}


### Use cases
{: #map-use-case}

The following {{site.data.keyword.la_full_notm}} query:

```text
query": "target.id:crn:v1:bluemix:public:cloud-object-storage:global:a/81de6380e6232019c6567c9c8de6dece:69002255-e226-424e-b6c7-23c887fdb8bf:bucket:at-frankfurt reason.reasonCode:403",
```
{: codeblock}

Maps into this {{site.data.keyword.logs_full_notm}} query:

```text
target.id.keyword:/crn:v1:bluemix:public:cloud-object-storage:global:a/81de6380e6232019c6567c9c8de6dece:69002255-e226-424e-b6c7-23c887fdb8bf:bucket:at-frankfurt.*/  reason.reasonCode.keyword:/403.*/
```
{: codeblock}


The following {{site.data.keyword.la_full_notm}} search:

```text
target.id:=="crn:v1:bluemix:public:cloud-object-storage:global:a/81de6380e6232019c6567c9c8de6dece:69002255-e226-424e-b6c7-23c887fdb8bf:bucket:logdna-logs-sydney"
```
{: codeblock}

Maps into this {{site.data.keyword.logs_full_notm}} search:

```text
target.id:"crn\:v1\:bluemix\:public\:cloud\-object\-storage\:global\:a\/81de6380e6232019c6567c9c8de6dece\:69002255\-e226\-424e\-b6c7\-23c887fdb8bf\:bucket\:logdna\-logs\-sydney"
```
{: codeblock}


## Group searches
{: #map-group-search}

The following {{site.data.keyword.la_full_notm}} group search:

```text
action:[iam-groups.group.update,iam-identity.account-profile.update,iam-am.policy.update]
```
{: codeblock}

Maps into this {{site.data.keyword.logs_full_notm}} group search:

```text
(action:"iam-groups.group.update" OR action:"iam-identity.account-profile.update" OR action:"iam-am.policy.update")
```
{: codeblock}

The following {{site.data.keyword.la_full_notm}} group search:

```text
action:("cloud-object-storage.object.create" | "cloud-object-storage.object-multipart.create")
```
{: codeblock}

Maps into this {{site.data.keyword.logs_full_notm}} group search:

```text
(action:"cloud-object-storage.object.create" OR action:"cloud-object-storage.object-multipart.create")
```
{: codeblock}


## Numeric range searches
{: #map-num-range}

The following {{site.data.keyword.la_full_notm}} numeric range search:

```text
(actionTime:>10000)
```
{: codeblock}

Maps into this {{site.data.keyword.logs_full_notm}} numeric range search:

```text
actionTime: [10000 TO *]
```
{: codeblock}

## Nested queries
{: #map-nexted}

Up to 3 levels of nested queries are mapped. For example this {{site.data.keyword.la_full_notm}} query:

```text
app:nginx-ingress-controller httpRequest.status:>499 (regional-compute OR regional-placement-group OR regional-instance-template OR regional-image OR cloudinit-service OR regional-baremetal OR regional-dedicated-compute OR regional-group OR regional-geography)
```
{: codeblock}

Maps to this {{site.data.keyword.logs_full_notm}} query:

```text
coralogix.metadata.subsystemName:/nginx-ingress-controller.*/ httpRequest.status.numeric:[499 TO *] ("regional-compute" OR "regional-placement-group" OR "regional-instance-template" OR "regional-image" OR "cloudinit-service" OR "regional-baremetal" OR "regional-dedicated-compute" OR "regional-group" OR "regional-geography")
```
{: codeblock}


