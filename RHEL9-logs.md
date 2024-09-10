---

copyright:
  years:  2024
lastupdated: "2024-09-10"

keywords:

subcollection: cloud-logs

content-type: tutorial
services: containers, cloud-logs, logs-router
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Send log data from a RHEL9 environment to {{site.data.keyword.logs_full_notm}}
{: #RHEL92logs}
{: toc-content-type="tutorial"}
{: toc-services="VSI, cloud-logs, linux"}
{: toc-completion-time="30m"}

In this tutorial, you will set up your VSI running RHEL9 to send your application logs to {{site.data.keyword.logs_full_notm}}.
These logs help you troubleshoot issues and improve the health and performance of your environment and your applications running in it.
{: shortdesc}

## Goals
{: #RHEL9logs_goals}

In this tutorial you will:

 - Deploy the [{{site.data.keyword.logs_routing_full_notm}} agent](/docs/logs-router?topic=logs-router-agent-about) in an existing VSI.

 - Configure it to use the (r)syslog input

 - Verify that log data is flowing to your [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs) instance.

 ## Before you begin
{: #RHEL92logs_prereqs}

Before you begin, make sure you have the following prerequisites.

 - Create a linux environment using RHEL9 as your operating system. In this tutorial, we will use a [VSI](https://cloud.ibm.com/docs/vpc?topic=vpc-creating-virtual-servers)

 - Provision an instance of [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-getting-started).

 - Install the JSON CLI processor [(`jq`)](https://jqlang.github.io/jq/download/){: external}.

 - Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

## Creating your API key
{: #RHEL9logs_key}
{: step}
{: ui}

Before you provision the {{site.data.keyword.logs_routing_full_notm}} agent, you need an IAM API key.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **API keys**.

3. Click **Create**.

4. Input a name and description for your API key. For example you can use `vsi-cloud-logs-key` as a name and `API key for sending VSI log data to Cloud Logs` for the description. You can customize these values if needed.

5. Click **Create**.

6. Click **Download** to save it to your computer in a file named `apikey.json`.

7. Open the file to view your API key.

	  The output is similar to:

	  ```json
      {
         "name": "vsi-cloud-logs-key",
         "description": "API key for sending VSI log data to Cloud Logs",
         "createdAt": "2024-09-04T08:54+0000",
         "apikey": "EaTtox-pcYzKo5Xa859DobiRmoChgEI5Q2wIpXA8cjtZ"
      }
	  ```
    {: screen}

    Protect the [API key](/docs/account?topic=account-manapikey&interface=ui). Anyone who can access the API key can impersonate your user.
    {: attention}

Note:

* Each time that you create an API key, a new IAM secret is generated.

* Make sure that you securely store the API key file, since it contains sensitive information.

## Creating your API key
{: #RHEL9logs_key}
{: step}
{: cli}

Before you provision the {{site.data.keyword.logs_routing_full_notm}} agent, you need an IAM API key.

1. Create an IAM API key by running the following command. You can customize the key name (`vsi-cloud-logs-key`), description (`--d`), and file name (`--file`) parameters if needed.

 	  ```sh
	  ibmcloud iam api-key-create vsi-cloud-logs-key --d 'API key for sending VSI log data to Cloud Logs' --file vsi-cloud-logs-key
	  ```
    {: pre}

2. Next, assign the _Sender_ role to your user to make sure you have the correct permissions to send logs. Replace the example email with your email.

   ```sh
   ibmcloud iam user-policy-create name@example.com --service-name logs --roles "Sender"
   ```
   {: pre}

3. Extract the API key from the file.

 	  ```sh
	  jq .apikey vsi-cloud-logs-key
	  ```
    {: pre}

	  The output is similar to:

	  ```text
	  EaTtox-pcYzKo5Xa859DobiRmoChgEI5Q2wIpXA8cjtZ
	  ```
    {: screen}

    Protect the [API key](/docs/account?topic=account-manapikey&interface=ui). Anyone who can access the API key can impersonate your user.
    {: attention}

Note:

* Each time that you create an API key, a new IAM secret is generated.

* Make sure that you securely store the API key file, since it contains sensitive information.

## Determining your logging endpoint
{: #RHEL92logs_endpoint}
{: step}
{: ui}

The second piece of information that is needed is the ingestion endpoint for your {{site.data.keyword.logs_full_notm}} instance.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg "Menu") &gt; **Observability**.

3. Click **Logging** > **Instances** and select the **Cloud Logs** tab.

4. Select your desired instance by clicking on its name.

5. On the left, select **Endpoints**.

6. Save the endpoint listed under **Public** > **Public Ingress endpoint** for the next steps. The endpoint is similar to `3a622101-7521-4002-bf91-8c26e17eedcf.ingress.eu-de.logs.cloud.ibm.com`


## Determining your logging endpoint
{: #RHEL92logs_endpoint}
{: step}
{: cli}

The second piece of information that is needed is the ingestion endpoint for your {{site.data.keyword.logs_full_notm}} instance. Use this command to retrieve the URL:

```sh
ibmcloud resource service-instances --service-name logs --long --output JSON | jq '[.[] | {name: .name, id: .id, region: .region_id, ingestion_endpoint: .extensions.external_ingress}]'
```
{: pre}

The endpoint is similar to:

```text
ingestion_endpoint: 3a622101-7521-4002-bf91-8c26e17eedcf.ingress.eu-de.logs.cloud.ibm.com
```
{: screen}

Save the endpoint for later.

## Connect to your VSI
{: #RHEL9logs_connect}
{: step}

Connect to your VSI to deploy the agent.

1. Log in to your {{site.data.keyword.cloud_notm}} account. Include the `--sso` option if you are using a federated ID.

   ```sh
   ibmcloud login
   ```
   {: pre}

2. Install the [infrastructure-service CLI plug-in](/docs/containers?topic=containers-cli-install)

   ```sh
   ibmcloud plugin install is
   ```
   {: pre}

3. List all instance you provisioned in your account

   ```sh
   ibmcloud is instances --output json | jq '[.[] | {name: .name, instance_id: .id, network_interface_id: .network_interfaces.[0].id}]'
   ```
   {: pre}

   You will see an output looking similar to:

   ```json
    [
      {
        "name": "ICL-VSI",
        "instance_id": "0787_x1x76xx6-4xx1-2exx-x995-44x6910879x4",
        "network_interface_id": "0738-12345x67-8901-234x-5678-9xx01xx23x4x"
      }
    ]
   ```
   {: screen}

   Keep the output of the instance you want to use for the next steps.

4. If you don't have a floating IP yet, run the following command to create one, replacing  `<network_interface_id>` with the output of the previous command. You can customize the name `ICL-VSI-floating-ip` if needed.

   ```sh
   ibmcloud is floating-ip-reserve ICL-VSI-floating-ip --nic <network_interface_id>
   ```
   {: pre}

4. Run the following command, replacing `<instance_id>` and `<network_interface_id>` with the output of the previous command.

   ```sh
   ibmcloud is instance-network-interfaces <instance_id> <network_interface_id> --json | jq '[.[] | {id: .id, address: .floating_ips.[0].address}]'
   ```
   {: pre}

   You will see an output looking similar to:

   ```json
    [
      {
        "id": "0738-12345x67-8901-234x-5678-9xx01xx23x4x",
        "address": "161.156.200.43"
      }
    ]
    ```
    {: screen}

    Save the address for the next step.

5. Now that you have your floating IP address, you can connect to your VSI.

   ```sh
   ssh -i <path to your private key file> root@<floating ip address>
   ```
   {: pre}

   You receive a response similar to the following example. When prompted to continue connecting, type yes.

   ```text
    The authenticity of host 'xxx.xxx.xxx.xxx (xxx.xxx.xxx.xxx)' can't be established.
    ECDSA key fingerprint is SHA256:abcdef1Gh/aBCd1EFG1H8iJkLMnOP21qr1s/8a3a8aa.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'xxx.xxx.xxx.xxx' (ECDSA) to the list of known hosts.
   ```
   {: screen}

   You are now accessing your server.

## Installing the agent
{: #RHEL92logs_install}
{: step}

Complete the following steps while you are connected to your VSI:

1. Download the required RPM package. For information about the current {{site.data.keyword.logs_routing_full_notm}} agent version, see the [agent release notes.](/docs/logs-router?topic=logs-router-release-notes-agent). Scroll down to RHEL9 and execute the following three commands to download the package (replace the version with the newest one available):

   ```sh
   yum install wget

   wget https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.rpm

   wget https://logs-router-agent-install-packages.s3.us.cloud-object-storage.appdomain.cloud/logs-router-agent-1.3.0.rpm.sha256
   ```
   {: pre}

2. Validate the checksum by running the following command:

   ```sh
   sha256sum -c <sha256_filename>
   ```
   {: pre}

   Where `<sha256_filename>` is the filename of the downloaded `*.sha256` file, for example `logs-router-agent-1.3.0.rpm.sha256`.
   It should output `OK`.

3. Install the agent package by running:

     ```sh
     rpm -ivh <rpm_filename>
     ```
     {: pre}

   Where `<rpm_filename>` is the name of the downloaded `*.rpm` file, for example `logs-router-agent-1.3.0.rpm`.

4. Download the configuration file and mark it as executable.

   ```sh
   wget https://logs-router-agent-config.s3.us.cloud-object-storage.appdomain.cloud/post-config.sh

   chmod +x post-config.sh
   ```
   {: codeblock}

5. Run the configuration script, replacing the values with the above gathered information:

   ```sh
   ./post-config.sh -h <target_host> -p 443 -t /logs/v1/singles -a IAMAPIKey -k <iam_api_key> --send-directly-to-icl
   ```
   {: pre}

   If you have secure access enabled in your VSI, add `-s true` to the command.

   | Parameter  |  Description |
   | ------------ | ------------ |
   | `<target_host>` | The endpoint of your ICL instance we gathered above. Replace `<target_host>` with the value. |
   | `<iam_api_key>` | Specifies the IAM API key that we obtained previously. Replace `<iam_api_key>` with the value. |

You should see the output confirming that the agent is running:
```text
IBM Cloud logger-agent is active and running!
```
{: screen}

## Modifying the agent YAML file to listen for (r)syslog logs
{: #RHEL92logs_yaml}
{: step}

After installing the agent, it will run in your environment. It will not send any logs until we configure the syslog input.

1. Open the `fluent-bit.conf` in an editor to modify it. Run the following command:

   ```sh
   vi /etc/fluent-bit/fluent-bit.conf
   ```
   {: pre}

2. Press `i` to change to `-- INSERT --` mode. Move your cursor to the end of the file and insert a new line.

3. Insert the following yaml snippet into the file, replacing `<SUBSYSTEM_NAME>` and `<APPLICATION_NAME>` with values meaningful to you. Those are crucial in ICL and help you to find your logs. You can set them for instance to the name of your VSI and region where it is running: `ICL-VSI`, `eu-gb`.

    ```yaml
      [INPUT]
        Name                syslog
        Path                /tmp/in_syslog
        Buffer_Chunk_Size   32000
        Buffer_Max_Size     64000
        Receive_Buffer_Size 512000

      [FILTER]
        Name modify
        Match *
        Add subsystemName <SUBSYSTEM_NAME>
        Add applicationName <APPLICATION_NAME>
      ```
     {: codeblock}

    Make sure the indentation matches the configuration which is already in the file. The keys below `[INPUT]` and `[FILTER]` should be indented by two spaces.

    The input will listen for syslog message on the unix socket.
    The filter adds the needed meta data.

4. Press `ESC` and type `:wq` to save your changes.

5. Restart the agent by executing

   ```sh
   systemctl daemon-reload && systemctl restart fluent-bit
   ```
   {: pre}


For viewing logs of your agent, you can use the following command: `journalctl -u fluent-bit --since 12:48 -f`, where you can replace the time after `since` with the current time minus a few minutes. This is usually the time in UTC.
{: tip}

## Verify that logs are being sent
{: #RHEL92logs_verify}
{: step}

To help ensure that your logs are successfully flowing to {{site.data.keyword.logs_full_notm}}, do the following steps:

1. Access the [{{site.data.keyword.logs_full_notm}} UI](/docs/cloud-logs?topic=cloud-logs-instance-launch) and click ![Livetail icon](/icons/livetail.svg "Livetail") **Livetail**.

2. Click `Start` to watch the logs as they arrive in real-time.

3. Send a test message by executing

   ```sh
   logger -u /tmp/in_syslog my_ident my_message
   ```
   {: pre}

   Wait for the log to appear in your UI.

