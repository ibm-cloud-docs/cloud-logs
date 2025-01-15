---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-15"

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

    For more information about Trusted Profiles, see [Generating a Trusted Profile for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).

4. Generate an API Key for service ID authentication.

    For authentication with trusted profiles, this step is not required.

    For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).

## Download the agent files
{: #agent-windows-step2}
{: step}

Complete the following steps:

1. Log in to your Windows environment.

2. Download the Windows agent ZIP archive.

    For information about the current {{site.data.keyword.agent}} version, see the [agent release notes](/docs/cloud-logs?topic=cloud-logs-release-notes-agent).

3. Validate the checksum by running the following command:

    ```bat
    sha256sum -c <sha256_filename>
    ```
    {: pre}

    Where `<sha256_filename>` is the filename of the download `*.sha256` file.

4. Using Powershell, expand the Windows agent archive in the `Program Files` directory.

    ```bat
    Expand-Archive -Path <archive_filename> -DestinationPath "C:\Program Files\"
    ```
    {: pre}

    Where `<archive_filename>` is the name of the downloaded `*.zip` file.

5. Change the directory to the expanded Windows agent archive.

    ```bat
    cd "C:\Program Files\logs-agent"
    ```
    {: pre}

6. Download the configuration file from the `C:\Program Files\logs-agent` location.

    ```text
    wget https://logs-router-agent-config.s3.us.cloud-object-storage.appdomain.cloud/configure-logs-agent.ps1
    ```
    {: codeblock}

## Deploy the {{site.data.keyword.agent}} to collect the Windows event log
{: #agent-windows-deploy-step3}
{: step}

Run the configuration Powershell script.

```bat
./configure-logs-agent.ps1 -TargetHost <target_host> -TargetPort <target_port> -AuthMode <auth_mode> -IAMEnv <IAM_environment> [[-IAMApiKey] <iam_api_key>] [-TrustedProfile] <trusted_profile_id>] -Channels <channels_list> [[-DBPath] <database_path>] [-VSISecureAccess]
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
:   (Optional) Specify the {{site.data.keyword.iamshort}} API key (required for `IAMAPIKey` mode). Make sure you follow the instructions in [Generating an API Key](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).

    For more information about {{site.data.keyword.iamshort}} API Keys, see [Managing API Keys](/docs/account?topic=account-manapikey).
    {: tip}

`-TrustedProfile <trusted_profile_id>`
:   (Optional) Specify the trusted profile ID (required for `VSITrustedProfile` mode). When using trusted profiles, set to the ID configured in [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).

    For more information on Trusted Profiles, see [Creating a Trusted Profile](/docs/account?topic=account-create-trusted-profile).
    {: tip}

`-Channels <channels_list>`
:   (Optional) If a channels list is provided, a default `winevtlog` input plug-in will be configured to read events from the specified channels. Specify which channels to read from the Windows Event Log as a comma-separated list without spaces.

`-DBPath <database_path>`
:   (Optional) If the `Channels` parameter is provided, set this parameter to the database file to store the position of proccessed events. If this parameter is not set and the `Channels` parameter is provided, the default database file will be `C:\Program Files\logs-agent\winevtlog.sqlite`.

`-VSISecureAccess`
:   (Optional) Set this flag if you have secure access enabled in your VSI. This option is not enabled by default.

## Configure the {{site.data.keyword.agent}} to include or exclude files
{: #agent-windows-deploy-step4}
{: step}

You can configure the {{site.data.keyword.agent}} to include or exclude files that the agent monitors.

1. Create the input plug-in configuration file `input-tail.conf` in `C:\Program Files\logs-agent\etc`.

2. Add the *INPUT* section.

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

4. Modify the `C:\Program Files\logs-agent\etc\fluent-bit.conf` file to include the reference to the `C:\Program Files\logs-agent\etc\input-windows-event-log.conf`.

    ```yaml
    @INCLUDE C:\Program Files\logs-agent\etc\input-windows-event-log.conf
    ```
    {: codeblock}

    The main configuration file `C:\Program Files\logs-agent\etc\fluent-bit.conf` imports other files with the tag `@INCLUDE <path_to_file>`.


## Add metadata
{: #agent-windows-deploy-step5}
{: step}

You must configure the {{site.data.keyword.agent}} to include `applicationName` and `subsystemName`. You can also add custom metadata.

- The application name is the environment that produces and sends logs to an {{site.data.keyword.logs_full_notm}} instance. Set the value to the hostname by using the variable `${COMPUTERNAME}` or entering the computer host name.
- The subsystem name is the service or application that produces and sends logs to an {{site.data.keyword.logs_full_notm}} instance. For example, you can set it to the provider name.

```yaml
[FILTER]
    Name modify
    Match winevtlog.*
    Copy ProviderName subsystemName
    Add applicationName ${COMPUTERNAME}
    Add meta.source ${SOURCE}
    Add meta.channel ${Channel}
    Add meta.providerName ${ProviderName}
    Add meta.environment prod
    Add meta.platform windows

[FILTER]
    Name nest
    Match winevtlog.*
    Operation nest
    Wildcard meta.*
    Nest_under meta
    Remove_prefix meta.
```
{: codeblock}

## Verify the agent configuration
{: #agent-windows-deploy-step6}
{: step}

Check that the agent configuration is correct by running the agent.

```bat
.\bin\fluent-bit.exe -c C:\Program Files\logs-agent\etc\fluent-bit.conf
```
{: pre}

The agent will start and establish a connection to the desired target.



## Create a Windows service
{: #agent-windows-deploy-step7}
{: step}


Windows services are long-running background processes and are the preferred way to run the agent on Windows.

Complete the following steps:

1. To register the agent as a Windows service run the following command.

    A single space is required after `binpath=`.{: note}

    ```bat
    sc.exe create fluent-bit binpath= "C:\Program Files\logs-agent\bin\fluent-bit.exe -c C:\Program Files\logs-agent\etc\fluent-bit.conf"
    ```
    {: pre}

2. For agents using `IAMAPIKey` to authenticate, create an API Key in the registry for the `fluent-bit` service.

    ```bat
    New-ItemProperty -Path "HKLM:\System\CurrentControlSet\Services\fluent-bit" -Name "Environment" -Value "IAM_API_KEY=<my_api_key>" -PropertyType MultiString
    ```
    {: pre}

3. Start the Windows service

    ```bat
    sc.exe start fluent-bit
    ```
    {: pre}


## Verify logs are being delivered to your target destination
{: #agent-windows-deploy-step8}
{: step}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view.
