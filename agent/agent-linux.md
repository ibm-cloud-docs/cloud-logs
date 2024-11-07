---

copyright:
  years:  2024
lastupdated: "2024-11-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing the {{site.data.keyword.agent}} for Linux
{: #agent-linux}

You can deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from RHEL8, RHEL9, Debian, and Ubuntu environments to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}


## Deploying the agent
{: #agent-linux-deploy}

Complete the following steps to deploy an agent to a supported Linux environment.

### Step 1. Define the authentication method for the agent
{: #agent-linux-deploy-step1}

Choose the type of identity and the authentication method for the agent. Then, create an API key if needed.

Complete the following steps:

1. Choose the type of identity: user, or service ID.

    You can use a user, or a service ID as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_full_notm}} service.

2. Grant permissions for ingestion to the identity that you have chosen.

    The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`.

    For more information, see [Setting up IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-agent-iam-permissions).

3. Generate an API Key for user authentication or for service ID authentication.

    

    For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-api-key).


### Step 2. Setting up and deploying the {{site.data.keyword.agent}} configuration
{: #agent-linux-deploy-step2}

Complete the following steps:

1. Log in to your Linux environment.

2. Download the required RPM or DEB packages. For information about the current {{site.data.keyword.agent}} version, see the [agent release notes.](/docs/cloud-logs?topic=cloud-logs-release-notes-agent)

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
   ./post-config.sh -h <target_host> -p <target_port> -t <target_path> -a <auth_mode> -k <iam_api_key> [--send-directly-to-icl] [-s <vsi_secure_access_enabled>] [-i <IAM_environment>]
   ```
   {: pre}

   

   Where

    `-t <target_path>`
    :   Specify `/logs/v1/singles` to send data to an {{site.data.keyword.logs_full_notm}} instance. 

    `-a <auth_mode>`
    :   Specify `IAMAPIKey` or `VSITrustedProfile`.

    `-k <iam_api_key>`
    :   Specify the {{site.data.keyword.iamshort}} API key (required for `IAMAPIKey` mode). Make sure you follow the instructions in [Generating an API Key](/docs/cloud-logs?topic=cloud-logs-api-key).

        For more information about {{site.data.keyword.iamshort}} API Keys, see [Managing API Keys](/docs/account?topic=account-manapikey).
        {: tip}

    `-d <trusted_profile_id>`
    :   Specify the trusted profile ID (required for `VSITrustedProfile` mode). When using trusted profiles, set to the ID configured in [Setting up Permissions for Ingestion](/docs/cloud-logs?topic=cloud-logs-agent-iam-permissions&interface=cli). You must create the instance with the metadata service enabled and link the trusted profile to your instance by specifying the ID when creating it. For more information, see [Creating virtual server instances](docs/vpc?topic=vpc-creating-virtual-servers).

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



### Step 3. Verify logs are being delivered to your target destination
{: #agent-linux-deploy-step4}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

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
