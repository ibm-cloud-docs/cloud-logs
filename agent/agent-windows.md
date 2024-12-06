---

copyright:
  years:  2024
lastupdated: "2024-12-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Deploying the {{site.data.keyword.agent}} for Windows
{: #agent-windows}

You can deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from Windows systems to an {{site.data.keyword.logs_full_notm}} instance. For more information on supported Windows environments, see [{{site.data.keyword.agent}} for non-orchestarted environments](/docs/cloud-logs?topic=cloud-logs-agent-about#agent-about-std).
{: shortdesc}

Complete the following steps to deploy an agent to a supported Windows system.

## Define the authentication method for the agent
{: #agent-windows-deploy-step1}
{: step}

Choose the type of identity and the authentication method for the agent. Then, create an API key if needed.

Complete the following steps:

1. Choose the type of identity: Service ID or Trusted Profile

    You can use a service ID or a Trusted Profile to authenticate with the {{site.data.keyword.logs_full_notm}} service. Trusted Profile are only supported on Virtual Servers for VPC. You must create the instance with the metadata service enabled and link the trusted profile to your instance by specifying the ID when creating it. For more information see [Creating virtual server instances](/docs/vpc?topic=vpc-creating-virtual-servers).

2. Grant permissions for ingestion to the identity that you have chosen.

    The `Sender` role is required to send logs to {{site.data.keyword.logs_full_notm}}.

    For more information, see [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).
   
    For more information about Trusted Profiles, see [Generating a Trusted Profile for ingestion](/docs/account?topic=cloud-logs-iam-ingestion-trusted-profile).

4. Generate an API Key for service ID authentication.

    For authentication with trusted profiles, this step is not required. 

    For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).

## Download the ZIP archive
{: #agent-windows-step2}
{: step}

Complete the following steps:

1. Download the Windows agent ZIP archive.

    For information about the current {{site.data.keyword.agent}} version, see the [agent release notes](/docs/cloud-logs?topic=cloud-logs-release-notes-agent).

2. Validate the checksum by running the following command:

    ```bat
    sha256sum -c <sha256_filename>
    ```
    {: pre}

    Where `<sha256_filename>` is the filename of the download `*.sha256` file.



## Set up and deploy the {{site.data.keyword.agent}} configuration
{: #agent-windows-deploy-step3}
{: step}

Complete the following steps:

1. Log in to your Windows environment.

2. Using Powershell, expand the Windows agent archive in the `Program Files` directory.

    ```bat
    Expand-Archive -Path <archive_filename> -DestinationPath "C:\Program Files\"
    ```
    {: pre}

    Where `<archive_filename>` is the name of the downloaded `*.zip` file.

3. Change the directory to the expanded Windows agent archive.

    ```bat
    cd "C:\Program Files\logs-agent"
    ```
    {: pre}


4. Download the configuration file from the following location.

   ```text
   https://logs-router-agent-config.s3.us.cloud-object-storage.appdomain.cloud/configure-logs-agent.ps1
   ```
   {: codeblock}

5. Run the configuration Powershell script.

   ```bat
   ./configure-logs-agent.ps1 [-TargetHost] <target_host> [-TargetPort] <target_port> [-AuthMode] <auth_mode> [[-IAMEnv] <IAM_environment>] [[-IAMApiKey] <iam_api_key>] [[-TrustedProfile] <trusted_profile_id>] [[-Channels] <channels_list>] [[-DBPath] <database_path>] [-VSISecureAccess]
   ```
   {: pre}

   Where

   `-TargetHost <target_host>`
   :   The host for {{site.data.keyword.logs_full_notm}} ingestion, found in the `Endpoints` section of your {{site.data.keyword.logs_full_notm}} instance `Overview`. Use the ingress endpoint. For more information, see [Ingress endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_ingress)

   `-TargetPort <target_port>`
   :   Specifies the ingress endpoint port which will depend on your network connectivity to {{site.data.keyword.logs_full_notm}}. Specify `3443` for {{site.data.keyword.logs_routing_full_notm}}. 
        - `443`: Public ingress endpoint
        - `443`: Private ingress endpoint (VPE)
        - `3443`: Private ingress endpoint (CSE)

   `-IAMEnv <IAM_environment>`
   :   (Optional) Specifies whether a public or private endpoint is used for IAM authentication. `Production` indicates to use the public endpoint. `PrivateProduction` specifies to use the private endpoint. `Production` is the default.

       If your system does not have access to the public internet, you must use `PrivateProduction` to use the private endpoint.
       {: important}

   `-AuthMode <auth_mode>`
   :   Specify `IAMAPIKey` or `VSITrustedProfile`.

   `-IAMApiKey <iam_api_key>`
   :   (Optional) Specify the {{site.data.keyword.iamshort}} API key (required for `IAMAPIKey` mode). Make sure you follow the instructions in [Generating an API Key](/docs/cloud-logs?topic=cloud-logs-api-key).

       For more information about {{site.data.keyword.iamshort}} API Keys, see [Managing API Keys](/docs/account?topic=account-manapikey).
       {: tip}

   `-TrustedProfile <trusted_profile_id>`
   :   (Optional) Specify the trusted profile ID (required for `VSITrustedProfile` mode). When using trusted profiles, set to the ID configured in [Setting up Permissions for Ingestion](/docs/cloud-logs?topic=cloud-logs-agent-iam-permissions&interface=cli).

       For more information on Trusted Profiles, see [Creating a Trusted Profile](/docs/account?topic=account-create-trusted-profile).
       {: tip}

   `-Channels <channels_list>`
   :   (Optional) If a channels list is provided, a default `winevtlog` input plug-in will be configured to read events from the specified channels. Specify which channels to read from the Windows Event Log as a comma-separated list without spaces.

   `-DBPath <database_path>`
   :   (Optional) If the `Channels` parameter is provided, set this parameter to the database file to store the position of proccessed events. If this parameter is not set and the `Channels` parameter is provided, the default database file will be `C:\Program Files\logs-agent\winevtlog.sqlite`.

   `-VSISecureAccess`
   :   (Optional) Set this flag if you have secure access enabled in your VSI. This option is not enabled by default.

5. Verify the agent configuration.
    
    Check that the agent configuration is correct by running the agent.

    ```bat
    .\bin\fluent-bit.exe -c etc\fluent-bit.conf
    ```
    {: pre}

    The agent will start and establish a connection to the desired target.

6. Create a Windows service.
    
    Windows services are long-running background processes and are the preferred way to run the agent on Windows.

   * To register the agent as a Windows service run the following command. A single space is required after `binpath=`.

     ```bat
     sc.exe create fluent-bit binpath= "C:\Program Files\logs-agent\bin\fluent-bit.exe -c C:\Program Files\logs-agent\etc\fluent-bit.conf"
     ```
     {: pre}

   * For agents using `IAMAPIKey` to authenticate, create an API Key in the registry for the `fluent-bit` service.

     ```bat
     New-ItemProperty -Path "HKLM:\System\CurrentControlSet\Services\fluent-bit" -Name "Environment" -Value "IAM_API_KEY=<my_api_key>" -PropertyType MultiString
     ```
     {: pre}

   * Start the Windows service

     ```bat
     sc.exe start fluent-bit
     ```
     {: pre}

## Reading the Windows event log
{: #agent-windows-deploy-step5}
{: step}

A commonly used input plug-in on Windows systems is the Windows Event Log input plug-in which gathers events from specific channels. To congifure the agent to read, gather, and forward events from this source using the current API from `winevt.h`, complete the following steps:

1. Edit the input plug-in configuration file `input-windows-event-log.conf` in `C:\Program Files\logs-agent\etc` if one was created during the configuration step. If no file exists, create a new `.CONF` file for this input section. The main configuration file `etc\luent-bit.conf` imports other files with the tag `@INCLUDE <path_to_file>`.

2. Create a new *INPUT* section.

    Set the **Channels** with the channels you want to read events from.

    Set the **Tag** with an identifier that can help with parsing.

    ```yaml
    [INPUT]
        Name         winevtlog
        Tag          winevtlog.*
        Channels     Application,Setup,Windows PowerShell
    ```
    {: codeblock}

3. Save the configuration file.

4. Restart the agent to apply the changes.

    ```bat
    sc.exe stop fluent-bit && sc.exe start fluent-bit
    ```
    {: codeblock}

## Including or excluding files
{: #agent-windows-deploy-step5}
{: step}

You can configure the agent to include or exclude files that the agent monitors.

Complete the following steps:

1. Create or edit the input plug-in configuration file `input-tail.conf` in `C:\Program Files\logs-agent\etc`. The main configuration file `etc\luent-bit.conf` imports other files with the tag `@INCLUDE <path_to_file>`.

2. Modify the *INPUT* section.

    Set the **Path** with the directories and files that you want to monitor.

    Set the **Exclude_Path** with the directories and files that you want to exclude from monitoring.

    ```yaml
    [INPUT]	
        Name              tail
        Tag               *
        Path              C:\logs\*.log
        Path_Key          file
        Exclude_Path      C:\logs\audit.log
        DB                C:\logs\fluent-bit.DB
        Buffer_Chunk_Size 32KB
        Buffer_Max_Size   256KB
        Skip_Long_Lines   On
        Refresh_Interval  10
    ```
    {: codeblock}

3. Save the configuration file.

4. Restart the agent to apply the changes.

    ```bat
    sc.exe stop fluent-bit && sc.exe start fluent-bit
    ```
    {: codeblock}

## Adding additional metadata fields
{: #agent-windows-deploy-step4}
{: step}

You can add additional metadata fields to the routed logs.

Complete the following steps:

1. Edit the `fluent-bit.conf` file in the `logs-agent\etc\` folder.

2. Add your custom metadata using this structure: `Add <meta.key_name> <your_custom_value>`

    ```yaml
    [FILTER]
      Name modify
      Match winevtlog.*
      Copy ProviderName subsystemName
      Add applicationName ${COMPUTERNAME}
      Add meta.agentVersion agentVersion

    [FILTER]
      Name nest
      Match winevtlog.*
      Operation nest
      Wildcard meta.*
      Nest_under meta
      Remove_prefix meta.
    ```
    {: codeblock}

    Where

    `Copy Channel applicationName`
    :   Copies the value of the Channel field in the matched log line into a new field called `applicationName`.
 
    `Copy ProviderName subsystemName`
    :   Copies the value of the `ProviderName` field into a new field called `subsystemName`.
    
    `<meta.key_name>`
    :   Is the name of the metadata field to be added (for example, `meta.env`) and `<your_custom_value>` is the value to be assigned to the field (for example, the name of your environment).

    For example, if you are using the `winevtlog` input plug-in and want to add the agent version and the region as metadata, the configuration would be similar to this:

    ```yaml
    [FILTER]
      Name modify
      Match winevtlog.*
      Copy ProviderName subsystemName
      Add applicationName ${COMPUTERNAME}
      Add agentVersion 1.4.0
      Add region us-east
    ```
    {: codeblock}

3. Save the configuration file.

4. Restart the agent to apply the changes.

    ```bat
    sc.exe stop fluent-bit && sc.exe start fluent-bit
    ```
    {: codeblock}

## Verify logs are being delivered to your target destination
{: #agent-windows-deploy-step6}
{: step}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view.

3. Add fields to enable filtering logs by specific fields.

    For example, create a filter `.CONF` file and add a field called `applicationName` set to the `%COMPUTERNAME%` as a `modify` filter.
   
    ```yaml
    [FILTER]
      Name modify
      Match winevtlog.*
      ...
      Add applicationName ${COMPUTERNAME}
    ```
    {: codeblock}

    Add this filter to the agent configuration by appending the line `@INCLUDE <path_to_filter_file>` in the `etc\luent-bit.conf` file. You can then set the `applicationname` filter in a view to the name of your Windows host.
