---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-16"

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

You need to have one or more {{site.data.keyword.logs_full_notm}} instances to work with platform logs and activity tracking events from Montreal. You also need an {{site.data.keyword.mon_full_notm}} instance in the region where you route platform metrics.

### Platform logs
{: #montreal-temp-before-logs}

Until the {{site.data.keyword.logs_routing_full_notm}} service is available in Montreal, platform logs are delivered to the {{site.data.keyword.logs_full_notm}} instance configured for the Washington DC (`us-east`) region. Logs sent from Montreal include a `logSourceCRN` field such as `ca-mon`, `mon01`, `mon02`, or `mon03`. If an {{site.data.keyword.logs_routing_full_notm}} tenant is not configured in `us-east`, then you need to [create a tenant in `us-east`](/docs/logs-router?topic=logs-router-tenant-create&interface=ui) to receive platform logs for the Montreal region.

### Activity tracking events
{: #montreal-temp-before-events}

Activity tracking events from Montreal can be configured in {{site.data.keyword.atracker_full_notm}} to be sent to any region.

If you have an {{site.data.keyword.atracker_full_notm}} [route](/docs/atracker?topic=atracker-route_v2&interface=ui) defined that contains a wildcard rule, then your Montreal events will be found in the [target](/docs/atracker?topic=atracker-target_v2&interface=ui) associated with the route. If you have a default target specified in the [{{site.data.keyword.atracker_full_notm}} settings](/docs/atracker?topic=atracker-settings&interface=ui), then your Montreal data will be located in that default target unless another routing rule directs the events to another target destination. A rule of some type must be configured to route `ca-mon`, `mon01`, `mon02` and `mon03` data to handle events sent by Montreal based services.

### Platform metrics
{: #montreal-temp-before-metrics}

Platform metrics from Montreal can be configured in {{site.data.keyword.metrics_router_full_notm}} to be sent to any region.

If you have an {{site.data.keyword.metrics_router_full_notm}} [route](/docs/metrics-router?topic=metrics-router-route-manage&interface=ui) defined that contains a wildcard rule, then your Montreal metrics will be found in the [target](/docs/metrics-router?topic=metrics-router-target-manage&interface=ui) associated with the route. You can also define a route rule with a `ca-mon`, `mon01`, `mon02` and `mon03` location [inclusion filter](/docs/metrics-router?topic=metrics-router-route_rules_definitions&interface=ui#route_rules_definitions_filters). If you have a default target specified in the [{{site.data.keyword.metrics_router_full_notm}} settings](/docs/metrics-router?topic=metrics-router-settings&interface=ui), then your Montreal data will be located in that default target unless you have a route that overrides it.

## Actions to prepare for observability services in Montreal
{: #montreal-temp-transition}

Between 21 July 2025 and 1 August 2025, the platform logs and platform metrics for services operating in the Montreal region will transition from Washington DC to Montreal.  During this time you will need to update the routing configurations for Montreal platform data in order to avoid losing data.
{: attention}

### Platform log preparation actions
{: #montreal-temp-transition-logs}

You need to configure {{site.data.keyword.logs_routing_full_notm}} for the Montreal region to continue receiving platform logs for the region.

In order to avoid missing platform logs during the transition to Montreal, configure the {{site.data.keyword.logs_routing_full_notm}} service for the Montreal region to send to the same {{site.data.keyword.logs_full_notm}} instance that is configured for Washington (`us-east`).  Once the {{site.data.keyword.logs_full_notm}} service is available in the Montreal region, you can choose when to migrate the platform logs to an {{site.data.keyword.logs_full_notm}} instance in the Montreal (`ca-mon`) region.

### Platform metrics preparation actions
{: #montreal-temp-transition-metrics}

If platform metrics in your account are managed by the {{site.data.keyword.metrics_router_full_notm}} and you have a route defined as described in [Platform metrics](/docs/logs?topic=montreal-temp&interface=ui#montreal-temp-before-metrics), no further action is required.

If [platform metrics are configured](/docs/monitoring?topic=monitoring-platform_metrics_enabling) to route your Montreal platform metrics by a `us-east` {{site.data.keyword.mon_full_notm}} instance, create an {{site.data.keyword.mon_full_notm}} support ticket with title `"Enable Monitoring Provisioning in Montreal"` to enable the provisioning of an {{site.data.keyword.mon_full_notm}} instance in `ca-mon` . After you provision your {{site.data.keyword.mon_full_notm}} instance in `ca-mon`, [configure platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling) with your new {{site.data.keyword.mon_full_notm}} `ca-mon` instance to avoid the loss of Montreal metrics.

### Activity tracking events preparation actions
{: #montreal-temp-transition-at-events}

If {{site.data.keyword.atracker_full_notm}} in your account has been configured as described in [Activity tracking events](/docs/logs?topic=montreal-temp&interface=ui#montreal-temp-before-events), then no further actions are required during the transition period.

## Actions after observability services are available in Montreal
{: #montreal-temp-after}

After {{site.data.keyword.cloud_notm}} observability services are available in Montreal, you can reconfigure your routing to send to {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.mon_full_notm}} instances in Montreal.
