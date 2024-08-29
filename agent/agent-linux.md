---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.logs_routing_full}} agent for Linux
{: #agent-linux}

You can deploy an {{site.data.keyword.logs_routing_full_notm}} agent to collect and route infrastructure and application logs from RHEL8, RHEL9, Debian, and Ubuntu environments to a target of your choice.
{: shortdesc}


## Deploying the agent
{: #agent-linux-deploy}

Complete the following steps to deploy an agent to a supported Linux environment.

### Step 1. Define the authentication method for the agent
{: #agent-linux-deploy-step1}

Choose the type of identity and the authentication method for the agent. Then, create an API key if needed.

Complete the following steps:

1. Choose the type of identity: user, service ID, or trusted profile.

    You can use a user, a service ID, or a trusted profile as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_routing_full}} service.

2. Grant permissions for ingestion to the identity that you have chosen.

    The role that is required for sending logs to {{site.data.keyword.logs_routing_full_notm}} is `Writer`.

    For more information, see [Setting up IAM permissions for ingestion](/docs/logs-router?topic=logs-router-agent-iam-permissions).

3. Generate an API Key for user authentication or for service ID authentication.

    For authentication with trusted profiles, this step is not required.

    For more information, see [Generating an API Key for ingestion](/docs/logs-router?topic=logs-router-api-key).


### Step 2. Setting up and deploying the {{site.data.keyword.logs_routing_full_notm}} agent configuration
{: #agent-linux-deploy-step2}

Complete the following steps:

1. Log in to your Linux environment.

2. Download the required RPM or DEB packages. For information about the current {{site.data.keyword.logs_routing_full_notm}} agent version, see the [agent release notes.](/docs/logs-router?topic=logs-router-release-notes-agent)

3. Validate the checksum by running the following command:

   ```sh
   sha256sum -c <sha256_filename>
   ```
   {: pre}

   Where `<sha256_filename>` is the filename of the download `*.sha256` file.

5. Install the agent.

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
   ./post-config.sh -h <target_host> -p <target_port> -t <target_path> -a <auth_mode> -k <iam_api_key> -d <trusted_profile_id> [--send-directly-to-icl] [-s <vsi_secure_access_enabled>]
   ```
   {: pre}

   <target_host>
   :   Is the [ingestion endpoint](/docs/logs-router?topic=logs-router-endpoints) where logs will be sent. For example, `ingester.private.eu-gb.logs-router.cloud.ibm.com`.

    <target_port>
    :   Specify `3443`.

    <target_path>
    :   Specify `/v1/logs/ws`.

    <auth_mode>
    :   Specify `IAMAPIKey` or `VSITrustedProfile`.

    <iam_api_key>
    :   Specify the {{site.data.keyword.iamshort}} API key (required for `IAMAPIKey` mode). Make sure you follow the instructions in [Generating an API Key](/docs/logs-router?topic=logs-router-api-key).

        For more information about {{site.data.keyword.iamshort}} API Keys, see [Managing API Keys](/docs/account?topic=account-manapikey).
        {: tip}

    <trusted_profile_id>
    :   Specify the trusted profile ID (required for `VSITrustedProfile` mode). When using trusted profiles, set to the ID configured in [Setting up Permissions for Ingestion](/docs/logs-router?topic=logs-router-agent-iam-permissions&interface=cli). You must create the instance with the metadata service enabled and link the trusted profile to your instance by specifying the ID when creating it. For more information see [Creating virtual server instances](docs/vpc?topic=vpc-creating-virtual-servers).

        For more information on Trusted Profiles, see [Creating a Trusted Profile](/docs/account?topic=account-create-trusted-profile).
        {: tip}

    --send-directly-to-icl

    :   (Optional) Use this option to send logs directly to {{site.data.keyword.logs_full_notm}}, bypassing the {{site.data.keyword.logs_routing_full_notm}} data plane. This option is useful when you have multiple {{site.data.keyword.logs_full_notm}} instances within the same account and require advanced logging configurations. For example, you can direct logs from different environments (for example, development and production) to separate {{site.data.keyword.logs_full_notm}} instances.

        When using this option, make sure you specify values specific to your {{site.data.keyword.logs_full_notm}} instance:

        - <target_host>: Specify the host for {{site.data.keyword.logs_full_notm}} ingestion, which can be found in the `Endpoints` section of your {{site.data.keyword.logs_full_notm}} instance `Overview`. Make sure you use the ingress endpoint.

        - <target_port>: specify `443`.

        - <target_path>: Specify `/logs/v1/singles`.

    -s
    :   (Optional) Set this to `true` if you have secure access enabled in your VSI. It will be set to `false` by default. For example, `-s true`.



### Step 3. Verify logs are being delivered to your target destination
{: #agent-linux-deploy-step4}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.la_short}} instance.](/docs/log-analysis?topic=log-analysis-launch&interface=ui)

2. When your agent is correctly configured, you can see logs through the default dashboard view.

### Step 4. (Optional) Add additional metadata fields
{: #agent-linux-deploy-step5}

You can add additional metadata fields to the routed logs.

1. Edit the `fluent-bit.conf` file in the `/etc/fluent-bit/` folder.

2. Add your custom metadata using this structure:

   ```yaml
    [FILTER]
       Name record_modifier
       Match *
       Record <meta.key_name> <your_custom_value>
   ```
   {: codeblock}

   Where `<meta.key_name>` is the name of the metadata field to be added (for example, `meta.env`) and `<your_custom_value>` is the value to be assigned to the field (for example, the name of your environment).

   For example, if you want to add an environment and region name as metadata, the configuration would be similar to this:

   ```yaml
   [FILTER]
       Name record_modifier
       Match *
       Record meta.cluster_name my-cluster
       Record meta.env production
       Record meta.region us-east
   ```
   {: codeblock}

3. Save the configuration file.

4. Restart the agent to apply the changes.

