---

copyright:
  years:  2024, 2025
lastupdated: "2025-12-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Release notes for the {{site.data.keyword.agent}}
{: #release-notes-agent}

Use these release notes to learn about updates to the {{site.data.keyword.agent}}.
{: shortdesc}



## 15 December 2025
{: #logs-router-agent-dec1525}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.7.1
:   {{site.data.keyword.agent}} version 1.7.1 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on Fluent Bit [v4.0.8](https://fluentbit.io/announcements/v4.0.8/){: external}.

   This version includes the following notable changes:

   * Change to ensure the record will have proper timestamp and metadata
   * `failed log` platform metric now reports correctly, instead of twice as high as the actual value of dropped logs 

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.1.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.1.deb.sha256){: external}

   Ubuntu 20

   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.1.deb){: external}
   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.1.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.1.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.1.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.1.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.1.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.1.zip.sha256){: external}

## 30 October 2025
{: #logs-router-agent-oct3025}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.7.0
:   {{site.data.keyword.agent}} version 1.7.0 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on Fluent Bit [v4.0.8](https://fluentbit.io/announcements/v4.0.8/){: external}.

   This version includes the following notable changes:

   * Updated Fluent Bit major version to 4.0.8.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.7.0.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.7.0.deb.sha256){: external}

   Ubuntu 20

   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.0.deb){: external}
   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.7.0.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.7.0.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.0.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.0.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.0.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.7.0.zip.sha256){: external}

## 12 September 2025
{: #logs-router-agent-sep1225}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.6.3
:   {{site.data.keyword.agent}} version 1.6.3 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on Fluent Bit [v3.2.10](https://fluentbit.io/announcements/v3.2.10/){: external}.

   This version includes the following notable changes:

   * Improved caching of access tokens in VSIs when using Trusted Profiles to reduce calls to IAM.
   * Added [parameter](/docs/cloud-logs?topic=cloud-logs-agent-helm-configure-maxunavailable) in Helm to specify the max number of pods that can be unavailable during the rolling update process.
   * Added multi-line support for non-orchestrated environments:
      * [Linux](/docs/cloud-logs?topic=cloud-logs-agent-multiline-linux)
      * [Windows](/docs/cloud-logs?topic=cloud-logs-agent-multiline-windows)
   * Added tutorials for multiline support:
      * [Multiline parsing for Log4j (orchestrated)](/docs/cloud-logs?topic=cloud-logs-multiline-log4j-helm)
      * [Multiline parsing for Log4j (non-orchestrated)](/docs/cloud-logs?topic=cloud-logs-multiline-log4j)
      * [Multiline parsing for Winston (orchestrated)](/docs/cloud-logs?topic=cloud-logs-multiline-winston-helm)
      * [Multiline parsing for Winston (non-orchestrated)](/docs/cloud-logs?topic=cloud-logs-multiline-winston)

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.3.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.3.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.3.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.3.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.3.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.3.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.3.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.3.deb.sha256){: external}

   Ubuntu 20

   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.3.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.3.deb){: external}
   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.3.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.3.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.3.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.3.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.3.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.3.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.3.zip.sha256){: external}

## 26 August 2025
{: #logs-router-agent-aug2625}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.6.2
:   {{site.data.keyword.agent}} version 1.6.2 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on Fluent Bit [v3.2.10](https://fluentbit.io/announcements/v3.2.10/){: external}.

   This version includes the following notable changes:

   * [Added `systemLogsParser` to helm for the ability to use a parser specific for system logs.](/docs/cloud-logs?topic=cloud-logs-agent-helm-log-files)
   * [Provided an optional parameter in helm (`maxLogLength`) to truncate logs after a specified length.](/docs/cloud-logs?topic=cloud-logs-agent-helm-maxloglength)
   * Fixed an error that was logging dropped messages even though the messages were still being processed.
   * Ensure custom configurations are preserved during upgrades.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.2.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.2.deb.sha256){: external}

   Ubuntu 20

   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.2.deb){: external}
   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.2.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.2.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.2.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.2.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.2.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.2.zip.sha256){: external}



## 26 June 2025
{: #logs-router-agent-jun2625}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.6.1
:   {{site.data.keyword.agent}} version 1.6.1 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on Fluent Bit [v3.2.10](https://fluentbit.io/announcements/v3.2.10/){: external}.

   This version includes the following notable changes:

   * You can configure the Kubernetes metadata fields included with each log record. By default, only essential fields such as `pod_name`, `namespace_name`, and `container_name` are kept. This helps reduce the amount of metadata stored with each log and reduces storage costs. For more information see [Enabling the Kubernetes filter to enrich logs with Kubernetes metadata](/docs/cloud-logs?topic=cloud-logs-agent-helm-kubernetes-filter).

   * The ability to add custom configurations to all sections.

     Each of the service, parsers and pipeline (inputs, processors, filters and outputs) can optionally be configured with additional settings that are not necessarily exposed with the default configurations.

     The following configurations can be used for more advanced configurations if necessary:

     - `additionalServiceOptions`
     - `additionalKubeLogInputProcessors`
     - `additionalInputs`
     - `additionalFilters` (use `additionalKubeLogInputProcessors` if possible)
     - `additionalOutputs`
     - `additionalParsers`

   * Enhanced system file processing of `/var/log` (for example, `syslog`, `messages`, `kubelet.log`).

     Use the `systemLogs` configuration to replace the `additionalLogSourcePaths` configuration to get better details for your host files:

     - Timestamps are parsed according to the format of the syslog files.
     - The Kubernetes filter is skipped which will reduce warnings in the logs and improve performance.
     - In {{site.data.keyword.logs_full_notm}} the `subsystemName` is the name of the host filename without the path.
     - In {{site.data.keyword.logs_full_notm}} the `applicationName` is the hostname of the node.
     - The cluster name is still recorded in `kubernetes.cluster_name` to be consistent with the container logs for filtering.

   * Multiline patterns are easier to configure.
 
     The `enableMultiline: true` option can be used in conjunction with the `multilinePreprocessor` to override the default multiline processor to better fit your situation.

   * Option to skip the Kubernetes filter

     The `enableKubernetesFilter: false` option can be used to bypass the Kubernetes plug-in.  This will mean that some of the Kubernetes metadata will be unavailable and some of the advanced parsing features provided by the Kubernetes filter, such as using container annotations to control the parser, will be unavailable.

   * After an initial successful test of the connection between the {{site.data.keyword.agent}} and {{site.data.keyword.logs_full_notm}}, all failed log transmissions are retried, regardless of the error received.
   * Fixed a bug when `defaultMetadata` is set in the `values.yaml` file that resulted in an invalid configuration.

   The following new {{site.data.keyword.agent}} packages are available. 

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.1.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.1.deb.sha256){: external}

   Ubuntu 20

   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.1.deb){: external}
   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.1.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.1.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.1.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.1.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.1.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.1.zip.sha256){: external}

## 5 June 2025
{: #logs-router-agent-jun0525}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.6.0
:   {{site.data.keyword.agent}} version 1.6.0 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on Fluent Bit [v3.2.10](https://fluentbit.io/announcements/v3.2.10/){: external}.

   This version includes the following notable changes:

   * Updated Fluent Bit to version 3.2.10
   * It is now possible to configure the agent to use [proxies](/docs/cloud-logs?topic=cloud-logs-agent-proxy). 
   * The helm chart provided for {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}} now use the Fluent Bit yaml-based configuration files.  This replaces the classic configuration which will be deprecated by Fluent Bit at the end of 2025.  The helm `values.yaml` files used with helm versions before 1.6.0 are compatible with 1.6.0.  Users that customize their configurations might need to take actions before applying this version of the helm chart.  If you are editing the config map files after deploying the helm chart then you will need to make changes to your process.  There are additional configuration values introduce with 1.6.0 that give more flexibility in your agent configuration. For more information, see [Template to deploy the {{site.data.keyword.agent}} using a 1.6.x Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters).

   Backward compatibility: You can still use your existing `logs-values.yaml` file from version 1.5.x with version 1.6.0. The transition is designed to be non-disruptive.

   [Deprecated]{: tag-deprecated} The classic configuration mode will be officially unsupported by Fluent Bit by the end of 2025. We recommend migrating to the YAML format as soon as possible to stay aligned with future updates. You can continue to use the previous versions of the Helm charts that were based on the classic configuration mode with newer versions of the Fluent Bit agent, but by the end of 2025 the classic configuration mode will be unsupported by Fluent Bit.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.6.0.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.6.0.deb.sha256){: external}

   Ubuntu 20

   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.0.deb){: external}
   *  [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.6.0.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.6.0.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.0.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.0.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.0.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.6.0.zip.sha256){: external}

## 12 May 2025
{: #logs-router-agent-may1225}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.5.2
:   {{site.data.keyword.agent}} version 1.5.2 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on fluentbit [v3.2.7](https://fluentbit.io/announcements/v3.2.7/){: external}.

   This version includes the following notable changes:

   * Improved severity parsing by ensuring acceptable values. For more information, see [Understanding how the Logging agent parses severities](/docs/cloud-logs?topic=cloud-logs-agent-severity).
   * Addressed a situation where the agent reports a dropped logs message with a deserialization error response.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.2.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.2.deb.sha256){: external}

   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.2.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.2.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.2.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.2.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.2.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.2.zip.sha256){: external}

## 25 March 2025
{: #logs-router-agent-mar2525}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.5.1
:   {{site.data.keyword.agent}} version 1.5.1 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on fluentbit [v3.2.7](https://fluentbit.io/announcements/v3.2.7/){: external}.

   This version includes the following notable changes:

   * Added a notices file to the {{site.data.keyword.agent}} download to provide licensing information.
   * Changed the agent log line that contained a JSON key with a # sign to avoid an error when querying the log line in {{site.data.keyword.logs_full_notm}}.
   * Use the `openshift.io/required-scc` annotations when configuring the `SecurityContextConstraints` instead of the `priority` configuration in order to avoid conflicts with other OpenShift components.
   * Fixed vulnerabilities.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.1.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.1.deb.sha256){: external}

   Ubuntu 20
   
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.1.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.1.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.1.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.1.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.1.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.1.zip.sha256){: external}

## 7 March 2025
{: #logs-router-agent-mar0725}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.5.0
:   {{site.data.keyword.agent}} version 1.5.0 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, Debian 11, Debian 12, and Windows.  This release is based on fluentbit [v3.2.7](https://fluentbit.io/announcements/v3.2.7/){: external}.

   This version includes the following notable changes:

   * Updated fluent bit version to v3.2.7.
   * Added configuration in helm to restart pods upon a deployment change that only updates secrets or configmaps.
   * Fixed a bug with the Trusted Profile for VSI token renewal that intermittently reported 401 errors when the token expires.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.5.0.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.5.0.deb.sha256){: external}

   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.5.0.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.5.0.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.0.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.0.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.0.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.5.0.zip.sha256){: external}

## 13 December 2024
{: #logs-router-agent-dec1324}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.4.2
:   {{site.data.keyword.agent}} version 1.4.2 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, Debian 12, and Windows.  This release is based on fluentbit [v3.1.9](https://fluentbit.io/announcements/v3.1.9/){: external}.

   This version includes the following notable changes:

   * Moved agent cache to host storage to ensure that agent restarts are able to use the cache.
   * Added `PriorityClass` for the agent Helm installation to ensure that the daemonsets are deployed.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.2.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.2.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.2.deb.sha256){: external}

   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.2.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.2.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.2.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.2.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.2.zip.sha256){: external}

## 6 December 2024
{: #logs-router-agent-dec0624}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.4.1
:   {{site.data.keyword.agent}} version 1.4.1 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, Debian 12, and Windows.  This release is based on fluentbit [v3.1.9](https://fluentbit.io/announcements/v3.1.9/){: external}.

   This version includes the following notable changes:

   * Windows Agent support. For more information, see [Deploying the {{site.data.keyword.agent}} for Windows](/docs/cloud-logs?topic=cloud-logs-agent-windows)
   * Multiline support with helm. For more information, see [Supporting multiline logs](/docs/cloud-logs?topic=cloud-logs-agent-multiline-new)

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.1.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.1.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.1.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.1.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.1.deb.sha256){: external}

   Windows

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.1.zip](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.1.zip){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.1.zip.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-agent-windows-1.4.1.zip.sha256){: external}

## 21 November 2024
{: #logs-router-agent-nov2124}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.4.0
:   {{site.data.keyword.agent}} version 1.4.0 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.1.9](https://fluentbit.io/announcements/v3.1.9/){: external}.

   This version includes the following notable changes:

   * Concurrent processing changes in {{site.data.keyword.logs_full_notm}} output plug-in.
      * Users might need to update the output plug-in to contain the `workers` option.
   * Improved error handling of connectivity issues when sending data directly to {{site.data.keyword.logs_full_notm}}.
   * Resolved an issue for some log entries incorrectly being grouped into the `ibm-subsystem-not found` subsystem.
   * Support for custom IAM environments.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.4.0.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.4.0.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.0.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.4.0.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.4.0.deb.sha256){: external}

## 24 October 2024
{: #logs-router-agent-oct2424}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.3.2
:   {{site.data.keyword.agent}} version 1.3.2 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.1.9](https://fluentbit.io/announcements/v3.1.9/){: external}.

   This version includes the following notable changes:

   * Update of fluentbit version to `v3.1.9`.
   * VSI trusted profile support for sending directly to {{site.data.keyword.logs_full_notm}}.
   * Support for multiple {{site.data.keyword.logs_full_notm}} outputs using different authentication forms.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.2.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.2.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.2.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.2.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.2.deb.sha256){: external}

## 10 October 2024
{: #logs-router-agent-oct1024}
{: release-note}

Release of the {{site.data.keyword.agent}}version 1.3.1
:   {{site.data.keyword.agent}} version 1.3.1 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.1.4](https://fluentbit.io/announcements/v3.1.4/){: external}.

   This version includes the following notable changes:

   * The `logger-icl-output-plugin` now uses a high resolution timestamp to keep the log order.
   * Removed double JSON marshaling in the output plug-ins.
   * Concurrency and performance improvements.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.1.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.1.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.1.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.1.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.1.deb.sha256){: external}

## 2 September 2024
{: #logs-router-agent-sep0224}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.3.0
:   {{site.data.keyword.agent}} version 1.3.0 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.1.4](https://fluentbit.io/announcements/v3.1.4/){: external}.

   This version includes the following notable changes:

   * The `logger-agent-plugin` now supports stanza-specific API keys.
   * The `systemd` plug-in is now enabled.

   The following new {{site.data.keyword.agent}} packages are available.

   Both packages are required for the installation.
   {: important}

   RHEL 8

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-rhel8-1.3.0.rpm.sha256){: external}

   RHEL 9

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.rpm](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.rpm){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.rpm.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.rpm.sha256){: external}

   Debian 11

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-deb11-1.3.0.deb.sha256){: external}


   Ubuntu 20

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.0.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.3.0.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.deb.sha256){: external}


## 7 August 2024
{: #logs-router-agent-aug0724}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.2.4
:   {{site.data.keyword.agent}} version 1.2.4 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.1.4](https://fluentbit.io/announcements/v3.1.4/){: external}.

   This version includes the following notable changes:

   * Update to fluentbit version
   * `logSourceCRN` renamed to `customerCRN`
   * Changes to retry logic in agent when sending messages to {{site.data.keyword.logs_full_notm}}
   * Ability to send logs to {{site.data.keyword.logs_full_notm}} in JSON format

   The following new {{site.data.keyword.agent}} packages are available.

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

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.4.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.4.deb.sha256){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.4.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-ubuntu20-1.2.4.deb){: external}


   Debian 12 & Ubuntu 22

   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb){: external}
   * [https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb.sha256](https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.2.4.deb.sha256){: external}


## 11 July 2024
{: #logs-router-agent-jul1124}
{: release-note}

Release of the {{site.data.keyword.agent}} version 1.2.3
:   {{site.data.keyword.agent}} version 1.2.3 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.0.4](https://fluentbit.io/announcements/v3.0.4/){: external}.

   This version includes the following notable changes:

   * Addition of a {{site.data.keyword.agent}} image that can run as a container sidecar.
       * `icr.io/ibm/observe/logs-router-agent-sidecar`
   * Fixed bug related to efficiency in handling payloads.
   * Users can now send logs directly to {{site.data.keyword.logs_full_notm}} in Linux agent with the optional `--send-directly-to-icl` flag

   The following new {{site.data.keyword.agent}} packages are available.

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

Release of the {{site.data.keyword.agent}} version 1.2.2
:   {{site.data.keyword.agent}} version 1.2.2 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL8, RHEL 9, Ubuntu 20, Ubuntu 22, and Debian 11, and Debian 12.  This release is based on fluentbit [v3.0.4](https://fluentbit.io/announcements/v3.0.4/){: external}.

   This version includes the following notable changes:

   * Enables per-message acknowledgements.  With this feature, each event bundle sent by the agent to the ingester is assigned an ID, and the {{site.data.keyword.logs_routing_full_notm}} ingester will send the agent an acknowledgement once the bundle has been sent through the data plane.  This helps avoid losing log events, for example due to abnormal connection closure or network outage, since the agent will resend unacknowledged bundles.

   The following new {{site.data.keyword.agent}} packages are available.

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

Release of the {{site.data.keyword.agent}} version 1.2.0
:   {{site.data.keyword.agent}} version 1.2.0 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL 9, Ubuntu 22, and Debian 12.  This release is based on fluentbit [v3.0.4](https://fluentbit.io/announcements/v3.0.4/){: external}, which includes a critical security fix for a vulnerability in the internal tracing interface. It is strongly recommended that you upgrade to this agent version.

   This version includes the following notable changes:

   * Fixes [CVE-2024-4323](https://fluentbit.io/blog/2024/05/21/statement-on-cve-2024-4323-and-its-fix/){: external}.
   * Fixes a bug in the `kubernetes` filter where the wrong labels and annotations can be applied when multiple pods or namespaces share a common base substring.
   * Enables IAM Trusted Profiles for non-containerized agents (agents running directly on Linux hosts).
   * Renames the Kubernetes `init` container to `logs-router-agent-init`.  The previous `logger-agent-init` tag can still be used, but the `logger-agent-init` tag will be disabled in the future and users are encouraged to update their deployment `yaml` file to reference the new image tag.

   The following new {{site.data.keyword.agent}} packages are available.

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

Release of the {{site.data.keyword.agent}} version 1.1.1
:   {{site.data.keyword.agent}} version 1.1.1 is available for {{site.data.keyword.containerlong_notm}}, {{site.data.keyword.openshiftlong_notm}}, RHEL 9, Ubuntu 22, and Debian 12.  This release is based on fluentbit [v3.0.2](https://fluentbit.io/announcements/v3.0.2/){: external}, which includes a critical fix for passing backpressure signals to input plugins from specific filter plugins.

   The following new {{site.data.keyword.agent}} packages are available.

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

Release of the {{site.data.keyword.agent}} version 1.1.0
:   The following new {{site.data.keyword.agent}} packages are available:

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
