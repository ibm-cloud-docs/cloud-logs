---

copyright:
  years:  2023, 2024
lastupdated: "2024-09-02"

keywords:

subcollection: logs-router

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for the {{site.data.keyword.logs_routing_full}} agent
{: #release-notes-agent}

Use these release notes to learn about updates to the {{site.data.keyword.logs_routing_full}} agent.
{: shortdesc}

For release notes about {{site.data.keyword.logs_routing_full}} in general, see [Release notes for {{site.data.keyword.logs_routing_full}}](/docs/logs-router?topic=logs-router-release-notes).
{: note}



## 7 August 2024
{: #logs-router-agent-aug0724}
{: release-note}

Release of the {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.4
:   {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.4 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.1.4](https://fluentbit.io/announcements/v3.1.4/){: external}.

   This version includes the following notable changes:

   * Update to fluentbit version
   * `logSourceCRN` renamed to `customerCRN`
   * Changes to retry logic in agent when sending messages to {{site.data.keyword.logs_full_notm}}
   * Ability to send logs to {{site.data.keyword.logs_full_notm}} in JSON format

   The following new {{site.data.keyword.logs_routing_full_notm}} Agent packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.4.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.4.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.4.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.4.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.4.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.4.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.4.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.4.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-ubuntu20-1.2.4.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.4.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.4.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.4.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb.sha256){: external}


## 11 July 2024
{: #logs-router-agent-jul1124}
{: release-note}

Release of the {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.3
:   {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.3 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.0.4](https://fluentbit.io/announcements/v3.0.4/){: external}.

   This version includes the following notable changes:

   * Addition of a {{site.data.keyword.logs_routing_full_notm}} Agent image that can run as a container sidecar.
       * `icr.io/ibm/observe/logs-router-agent-sidecar`
   * Fixed bug related to efficiency in handling payloads.
   * Users can now send logs directly to {{site.data.keyword.logs_full_notm}} in Linux agent with the optional `--send-directly-to-icl` flag

   The following new {{site.data.keyword.logs_routing_full_notm}} Agent packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.3.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.3.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.3.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.3.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.3.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.3.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.3.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.3.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-ubuntu20-1.2.3.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.3.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.3.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.3.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.3.deb.sha256){: external}


## 10 June 2024
{: #logs-router-agent-jun1024}
{: release-note}

Release of the {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.2
:   {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.2 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.0.4](https://fluentbit.io/announcements/v3.0.4/){: external}.

   This version includes the following notable changes:

   * Enables per-message acknowledgements.  With this feature, each event bundle sent by the agent to the ingester is assigned an ID, and the {{site.data.keyword.logs_routing_full_notm}} ingester will send the agent an acknowledgement once the bundle has been sent through the data plane.  This helps avoid losing log events, for example due to abnormal connection closure or network outage, since the agent will resend unacknowledged bundles.

   The following new {{site.data.keyword.logs_routing_full_notm}} Agent packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.2.2.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.2.2.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-ubuntu20-1.2.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.2.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.2.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.2.deb.sha256){: external}

## 29 May 2024
{: #logs-router-agent-may2924}
{: release-note}

Release of the {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.0
:   {{site.data.keyword.logs_routing_full_notm}} Agent version 1.2.0 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL 9, Ubuntu 22, and Debian 12.  This release is based on fluentbit [v3.0.4](https://fluentbit.io/announcements/v3.0.4/){: external}, which includes a critical security fix for a vulnerability in the internal tracing interface. It is strongly recommended that you upgrade to this agent version.

   This version includes the following notable changes:

   * Fixes [CVE-2024-4323](https://fluentbit.io/blog/2024/05/21/statement-on-cve-2024-4323-and-its-fix/){: external}.
   * Fixes a bug in the `kubernetes` filter where the wrong labels and annotations can be applied when multiple pods or namespaces share a common base substring.
   * Enables IAM Trusted Profiles for non-containerized agents (agents running directly on Linux hosts).
   * Renames the Kubernetes `init` container to `logs-router-agent-init`.  The previous `logger-agent-init` tag can still be used, but the `logger-agent-init` tag will be disabled in the future and users are encouraged to update their deployment `yaml` file to reference the new image tag.

   The following new {{site.data.keyword.logs_routing_full_notm}} Agent packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.rpm.sha256){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.2.0.deb.sha256){: external}

## 1 May 2024
{: #logs-router-agent-may0124}
{: release-note}

Release of the {{site.data.keyword.logs_routing_full_notm}} Agent version 1.1.1
:   {{site.data.keyword.logs_routing_full_notm}} Agent version 1.1.1 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL 9, Ubuntu 22, and Debian 12.  This release is based on fluentbit [v3.0.2](https://fluentbit.io/announcements/v3.0.2/){: external}, which includes a critical fix for passing backpressure signals to input plugins from specific filter plugins.

   The following new {{site.data.keyword.logs_routing_full_notm}} Agent packages are available.

   Both packages are required for the installation.
   {: important}
   
   RHEL 9
   
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.rpm){: external}

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.rpm.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.1.deb.sha256){: external}


## 29 April 2024
{: #logs-router-agent-apr2924}
{: release-note}

Release of the {{site.data.keyword.logs_routing_full_notm}} Agent version 1.1.0
:   The following new {{site.data.keyword.logs_routing_full_notm}} Agent packages are available: 

   Both packages are required for the installation.
   {: important}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.rpm.sha256){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0.deb.sha256){: external}


   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-rhel8.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-rhel8.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-rhel8.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-rhel8.rpm.sha256){: external}


   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-debian11.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-debian11.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-debian11.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-debian11.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-ubuntu20.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-ubuntu20.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-ubuntu20.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-routing-agent-1.1.0-ubuntu20.deb.sha256){: external}

