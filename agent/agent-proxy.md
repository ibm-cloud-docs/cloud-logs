---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Configuring the {{site.data.keyword.agent}} to use proxies
{: #agent-proxy}

You can use a proxy as an intermediary between the {{site.data.keyword.agent}} and {{site.data.keyword.iamlong}} (IAM) or your {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

If you need to install the {{site.data.keyword.agent}} in an environment that enforces strict connectivity control for network outbound traffic where firewalls are blocking all non-entitled connections to outside service endpoints, the {{site.data.keyword.agent}} traffic can be re-directed via a proxy.

Proxies can act like a firewall or filter to control outbound traffic, providing more control about the data leaving your environment and thus enhancing privacy and security.

For example, they can hide your internal IP addresses to the outside world.
In this setup requests sent from the {{site.data.keyword.agent}} are routed through the proxy and can be blocked or forwarded to their original destination.

Configuring and securing a proxy is normally the responsibility of your network administrators.

It is possible to configure the {{site.data.keyword.agent}} to use a proxy.

You can set the URL of the proxy to use by exporting the environment variables `HTTP_PROXY`, `HTTPS_PROXY` and `NO_PROXY` (or the lowercase versions). The variables must contain a complete URL, or a http scheme is assumed when setting them to `host[:port]`.

Examples of valid environment variables are: `HTTPS_PROXY="https://example.proxy:443"`, `HTTP_PROXY="192.168.1.1:8080"`, and `HTTP_PROXY="localhost"`.

For example, if you export the environment variable `HTTPS_PROXY="https://example.proxy:443"`, all HTTPS request from the {{site.data.keyword.agent}} will be routed through the proxy listening on `https://example.proxy:443`.
Those request include calls to {{site.data.keyword.iamlong}} (IAM) to get  authorization tokens and requests for sending logs to your {{site.data.keyword.logs_full_notm}} instance.

Looking at this example in a more detail, the {{site.data.keyword.agent}} creates a request for IAM to get an authorization token and sends it.
By setting the environment variable `HTTPS_PROXY`, this call will be forwarded to the proxy listening on that address.
This proxy can then decide whether the request can be sent or if it should be blocked.

In the first case, it will be forwarded to the original address (IAM), while in the second case the agent will display an error because the token is required for sending logs.

If you want specific requests to not be routed through the proxy, you can set this by exporting the URL in the environment variable `NO_PROXY`.

Multiple URLS can be exported in a comma separated list.
