---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-08"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Deploying the {{site.data.keyword.agent}} for Linux
{: #agent-linux}

You can deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from Linux environments such as RHEL8, RHEL9, Debian, and Ubuntu to an {{site.data.keyword.logs_full_notm}} instance. For more information on supported Linux environments, see [{{site.data.keyword.agent}} for non-orchestarted environments](/docs/cloud-logs?topic=cloud-logs-agent-about#agent-about-std).
{: shortdesc}

These instructions are for Red Hat Linux systems but can be used for other Linux RPM-based servers.
{: note}

Complete the following steps to deploy an agent to a supported Linux environment.

## Define the authentication method for the agent
{: #agent-linux-deploy-step1}
{: step}

Choose the type of identity and the authentication method for the agent. Then, create a trusted profile or an API key. The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`.

You can use a service ID or a trusted profile as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_full}} service. For more information, see [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).

Choose one of the following options:

### Option 1: Authentication using a trusted profile
{: #agent-helm-linux-deploy-step1-tp}

Create a Trusted Profile. For more information, see [Generating a Trusted Profile for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).

### Option 2: Authentication using a service ID API key
{: #agent-helm-linux-deploy-step1-key}

Generate an API Key for service ID authentication. For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).


## Download the required RPM or DEB packages
{: #agent-linux-step2}
{: step}

Complete the following steps:

1. Download the required RPM or DEB packages.

    For information about the current {{site.data.keyword.agent}} version, see the [agent release notes](/docs/cloud-logs?topic=cloud-logs-release-notes-agent).

2. Validate the checksum by running the following command:

    ```sh
    sha256sum -c <sha256_filename>
    ```
    {: pre}

    Where `<sha256_filename>` is the filename of the download `*.sha256` file.



## Set up and deploy the {{site.data.keyword.agent}} configuration
{: #agent-linux-deploy-step3}
{: step}

Complete the following steps:

1. Log in to your Linux environment.

2. Install the agent.

   * For RHEL run:

     ```sh
     rpm -ivh <rpm_filename>
     ```
     {: pre}

   * For Debian and Ubuntu run:

     ```sh
     dpkg -i <deb_filename>
     ```
     {: pre}

   Where `<rpm_filename>` or `<deb_filename>` is the name of the downloaded `*.rpm` or `*.deb` file.

6. Download the configuration file.

   ```text
   https://logs-router-agent-config.s3.us.cloud-object-storage.appdomain.cloud/post-config.sh
   ```
   {: codeblock}

7. Run the configuration script.

   ```sh
   ./post-config.sh -h <target_host> -p <target_port> -t <target_path> -a <auth_mode> -k <iam_api_key> [--send-directly-to-icl] [-s <vsi_secure_access_enabled>] [-i <IAM_environment>]
   ```
   {: pre}

   

   Where

    `-t <target_path>`
    :   Specify `/logs/v1/singles` to send data to an {{site.data.keyword.logs_full_notm}} instance. 

    `-a <auth_mode>`
    :   Specify `IAMAPIKey` or `VSITrustedProfile`.

    `-k <iam_api_key>`
    :   Specify the {{site.data.keyword.iamshort}} API key (required for `IAMAPIKey` mode). Make sure you follow the instructions in [Generating an API Key](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).

        For more information about {{site.data.keyword.iamshort}} API Keys, see [Managing API Keys](/docs/account?topic=account-manapikey).
        {: tip}

    `-d <trusted_profile_id>`
    :   Specify the trusted profile ID (required for `VSITrustedProfile` mode). When using trusted profiles, set to the ID configured in [Setting up Permissions for Ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions&interface=cli). You must create the instance with the metadata service enabled and link the trusted profile to your instance by specifying the ID when creating it. For more information see [Creating virtual server instances](/docs/vpc?topic=vpc-creating-virtual-servers).

        For more information on Trusted Profiles, see [Creating a Trusted Profile](/docs/account?topic=account-create-trusted-profile).
        {: tip}

    `--send-directly-to-icl`
    :   Set this parameter to send logs directly to {{site.data.keyword.logs_full_notm}}.

    `-h <target_host>`
    : The host for {{site.data.keyword.logs_full_notm}} ingestion, found in the `Endpoints` section of your {{site.data.keyword.logs_full_notm}} instance `Overview`. Use the ingress endpoint. For more information, see [Ingress endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_ingress)

    `-i <IAM_environment>`
    :   Specifies whether a public or private endpoint is used for IAM authentication. `Production` indicates to use the public endpoint. `PrivateProduction` specifies to use the private endpoint. `Production` is the default.

        If your system does not have access to the public internet, you must use `PrivateProduction` to use the private endpoint.
        {: important}


    `-p <target_port>`
    :   Use `443` to send logs directly to {{site.data.keyword.logs_full_notm}}. 

    `-s <vsi_secure_access_enabled>`
    :   (Optional) Set this to `true` if you have secure access enabled in your VSI. It will be set to `false` by default. For example, `-s true`.


## Add additional metadata fields
{: #agent-linux-deploy-step4}
{: step}

You can add additional metadata fields to the routed logs.

Complete the following steps:

1. Edit the `fluent-bit.conf` file in the `/etc/fluent-bit/` folder.

2. Add your custom metadata using this structure: `Add <meta.key_name> <your_custom_value>`

    ```yaml
    [FILTER]
      Name modify
      Match *
      Add subsystemName subsystemName
      Add applicationName applicationName
      Add meta.hostname ${HOSTNAME}
      Add meta.environment prod   # Sample values: prod, staging, dev, qa
      Add meta.platform linux

    [FILTER]
      Name nest
      Match *
      Operation nest
      Wildcard meta.*
      Nest_under meta
      Remove_prefix meta.
    ```
    {: codeblock}

    Where

    - `applicationName`: The application name defines the environment that produces and sends logs to {{site.data.keyword.logs_full_notm}}. You must add an applicationName, for example, you can set it to `${HOSTNAME}`.
    - `subsystemName`: The subsystem name is the service or application that produces and sends logs to {{site.data.keyword.logs_full_notm}}. You must add a subsystemName.
    - `<meta.key_name>` is the name of the metadata field to be added (for example, `meta.env`) and `<your_custom_value>` is the value to be assigned to the field (for example, the name of your environment).

    For example, if you want to add the agent version and the region as metadata, the configuration would be similar to this:

    ```yaml
    [FILTER]
      Name modify
      Match *
      Add subsystemName subsystemName
      Add applicationName ${HOSTNAME}
      Add meta.environment prod
      Add meta.platform linux
      Add region us-east
    ```
    {: codeblock}

3. Save the configuration file.

4. Restart the agent to apply the changes.

    ```pre
    systemctl daemon-reload && systemctl restart fluent-bit
    ```
    {: codeblock}


## Include or exclude files
{: #agent-linux-deploy-step5}
{: step}

You must configure the log files that the {{site.data.keyword.agent}} monitors.
{: important}

Complete the following steps:

1. Edit the `fluent-bit.conf` file in the `/etc/fluent-bit/` folder.

2. Modify the *INPUT* section.

    Set the **Path** with the directories and files that you want to monitor.

    Set the **Exclude_Path** with the directories and files that you want to exclude from monitoring.

    ```yaml
    [INPUT]
      Name              tail
      Tag               *
      Path              /var/log/*.log
      Path_Key          file
      Exclude_Path      /var/log/audit.log
      DB                /var/log/fluent-bit.DB
      Buffer_Chunk_Size 32KB
      Buffer_Max_Size   256KB
      Skip_Long_Lines   On
      Refresh_Interval  10
      storage.type      filesystem
      storage.pause_on_chunks_overlimit on
    ```
    {: codeblock}

3. Modify the *SERVICE* section.
    
    Set the **storage.path** to a location in the file system to store streams and data.

4. Save the configuration file.

5. Restart the agent to apply the changes.

    ```pre
    systemctl daemon-reload && systemctl restart fluent-bit
    ```
    {: codeblock}

## Verify logs are being delivered to your target destination
{: #agent-linux-deploy-step6}
{: step}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view.

    For example, if you set the applicationName to the hostname in your agent, you can set the applicationname filter in a view to the name of your host.

## Updating the agent
{: #agent-linux-update}

You can update the agent by downloading the desired agent packages and running the appropriate command for your environment. For information about the current {{site.data.keyword.agent}} version, see the [agent release notes.](/docs/logs-router?topic=logs-router-release-notes-agent)

    * For RHEL run:

     ```sh
     rpm -Uvh <rpm_filename>
     ```
     {: pre}

   * For Debian and Ubuntu run:

     ```sh
     dpkg -i <deb_filename>
     ```
     {: pre}

   Where `<rpm_filename>` or `<deb_filename>` is the name of the downloaded `*.rpm` or `*.deb` file.
