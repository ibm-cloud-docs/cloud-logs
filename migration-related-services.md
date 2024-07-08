---

copyright:
  years:  2024
lastupdated: "2024-05-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Location availability for related services
{: #migration-related-locations}

{{site.data.keyword.logs_full}} integrates with several {{site.data.keyword.cloud_notm}} services that might, or might not, be available in all {{site.data.keyword.cloud_notm}} regions.
{: shortdesc}

## Routing services
{: #mig-route-locations}

Several {{site.data.keyword.cloud_notm}} services route data to {{site.data.keyword.logs_full}}.

| Geography             | Region                   | {{site.data.keyword.atracker_full_notm}} | {{site.data.keyword.logs_routing_full_notm}} | {{site.data.keyword.metrics_router_full_notm}} |
|-----------------------|--------------------------|--------------|-----------|-----------|
| `Asia Pacific`        | `Chennai (in-che)`        | [Yes]{: tag-green} | [No]{: tag-red} |[No]{: tag-red} |
| `Asia Pacific`        | `Osaka (jp-osa)`        | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
| `Asia Pacific`        | `Sydney (au-syd)`        | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| `Asia Pacific`        | `Tokyo (jp-tok)`        | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
| `Europe`              | `Frankfurt (eu-de)`  | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| `Europe`              | `London (eu-gb)`  | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| `Europe`              | `Madrid (eu-es)`  | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| `North America`       | `Dallas (us-south)`      | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| `North America`       | `Toronto (ca-tor)`      | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
| `North America`       | `Washington (us-east)`   | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| `South America`       | `Sao Paulo (br-sao)`   | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Table 1. Locations of routing services that send data to {{site.data.keyword.logs_full}}" caption-side="top"}

## Integrated services
{: #mig-integ-locations}

{{site.data.keyword.logs_full}} integrates with other {{site.data.keyword.cloud_notm}} services for storage and notification purposes.

| Geography             | Region                   | {{site.data.keyword.cos_full_notm}} | {{site.data.keyword.en_full_notm}} |
|-----------------------|--------------------------|--------------|-----------|
| `Asia Pacific`        | `Chennai (in-che)`        |  [Yes]{: tag-green} | [No]{: tag-red} |
| `Asia Pacific`        | `Osaka (jp-osa)`        |  [Yes]{: tag-green} | [No]{: tag-red} |
| `Asia Pacific`        | `Sydney (au-syd)`        |  [Yes]{: tag-green} | [Yes]{: tag-green} |
| `Asia Pacific`        | `Tokyo (jp-tok)`        |  [Yes]{: tag-green} | [No]{: tag-red} |
| `Europe`              | `Frankfurt (eu-de)`  |  [Yes]{: tag-green} | [Yes]{: tag-green} |
| `Europe`              | `London (eu-gb)`  |  [Yes]{: tag-green} | [Yes]{: tag-green} |
| `Europe`              | `Madrid (eu-es)`  |  [Yes]{: tag-green} | [Yes]{: tag-green} |
| `North America`       | `Dallas (us-south)`      |  [Yes]{: tag-green} | [Yes]{: tag-green} |
| `North America`       | `Toronto (ca-tor)`      |  [Yes]{: tag-green} | [No]{: tag-red} |
| `North America`       | `Washington (us-east)`   |  [Yes]{: tag-green} | [No]{: tag-red} |
| `South America`       | `Sao Paulo (br-sao)`   |  [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Table 2. Locations of {{site.data.keyword.cloud_notm}} services that integrate with {{site.data.keyword.logs_full}}" caption-side="top"}

{{site.data.keyword.cos_full_notm}} support in Chennai (in-che) is single data center support only.
{: note}
