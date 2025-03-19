---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Considerations for workloads in the Montreal region
{: #montreal-temp}

{{site.data.keyword.cloud_notm}} is opening a newly supported location in Montreal. Montreal support for different {{site.data.keyword.cloud_notm}} services will be made available over a time. The {{site.data.keyword.cloud_notm}} observability services ({{site.data.keyword.logs_full_notm}}, {{site.data.keyword.mon_full_notm}}, {{site.data.keyword.atracker_full_notm}}, {{site.data.keyword.logs_routing_full_notm}}, and {{site.data.keyword.metrics_router_full_notm}}) will be made available in Montreal after you might already have workloads from other {{site.data.keyword.cloud_notm}} services in Montreal.
{: shortdesc}

## Observability support for Montreal before the observability services are available in Montreal
{: #montreal-temp-before}

Until the {{site.data.keyword.logs_routing_full_notm}} service is available in Montreal, platform logs are delivered to the {{site.data.keyword.logs_full_notm}} instance configured for the Washington DC (`us-east`) region. Logs sent from Montreal include a `logSourceCRN` field such as `ca-mon`, `mon01`, `mon02`, or `mon03`. If an {{site.data.keyword.logs_routing_full_notm}} tenant is not configured in `us-east`, then you need to [create a tenant in `us-east`](/docs/logs-router?topic=logs-router-tenant-create&interface=ui) to receive platform logs for the Montreal region.

Activity tracking events from Montreal can be configured in {{site.data.keyword.atracker_full_notm}} to be sent to any region.

If you have an {{site.data.keyword.atracker_full_notm}} [route](/docs/atracker?topic=atracker-route_v2&interface=ui) defined that contains a wildcard rule, then your Montreal events will be found in the [target](/docs/atracker?topic=atracker-target_v2&interface=ui) associated with the route. If you have a default target specified in the [{{site.data.keyword.atracker_full_notm}} settings](/docs/atracker?topic=atracker-settings&interface=ui), then your Montreal data will be located in that default target unless another routing rule directs the events to another target destination. A rule of some type must be configured to route `us-east` data to handle events sent by Montreal.

Platform metrics from Montreal can be configured in {{site.data.keyword.metrics_router_full_notm}} to be sent to any region.

If you have an {{site.data.keyword.metrics_router_full_notm}} [route](/docs/metrics-router?topic=metrics-router-route-manage&interface=ui) defined that contains a wildcard rule, then your Montreal metrics will be found in the [target](/docs/metrics-router?topic=metrics-router-target-manage&interface=ui) associated with the route. If you have a default target specified in the [{{site.data.keyword.metrics_router_full_notm}} settings](/docs/metrics-router?topic=metrics-router-settings&interface=ui), then your Montreal data will be located in that default target unless another routing rule directs the metrics to another target destination. A rule of some type must be configured to route `us-east` data to handle metrics sent by Montreal.

You need to have one or more {{site.data.keyword.logs_full_notm}} instances to work with platform logs and activity tracking events from Montreal. You also need an {{site.data.keyword.mon_full_notm}} instance in the region where you route platform metrics.

## Actions after observability services are available in Montreal
{: #montreal-temp-before}

After {{site.data.keyword.cloud_notm}} observability services are available in Montreal, you can reconfigure your routing to send to {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.mon_full_notm}} instances in Montreal. You need to configure Logs Routing for the Montreal region to continue receiving platform logs for the region.
