---

copyright:
  years:  2024
lastupdated: "2024-09-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the {{site.data.keyword.agent}} for (r)Syslog logs
{: #agent-rsyslog}

You can deploy a {{site.data.keyword.agent}} to collect and route (r)Syslog messages from a Syslog server to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}



## Before you begin
{: #syslog-prereq}

Be sure that you have deployed the {{site.data.keyword.agent}} on Linux.
For more information, see [Managing the agent Linux environments](/docs/cloud-logs?topic=cloud-logs-agent-linux).


## Step 1. Setting up the {{site.data.keyword.agent}} configuration
{: #syslog-s1}

You can configure the {{site.data.keyword.agent}} to collect (r)Syslog messages through a Unix socket server (UDP or TCP) or over the network using TCP or UDP.

1. Edit the `fluent-bit.conf` file in the `/etc/fluent-bit/` folder.

2. Choose the type of configuration for the agent to collect the Syslog messages. Add the following input sections:

   - To listen for Syslog messages on the Unix socket

     ```yaml

     [INPUT]
         Name                syslog
         Path                /tmp/in_syslog
         Buffer_Chunk_Size   32000
         Buffer_Max_Size     64000
         Receive_Buffer_Size 512000
      ```
     {: codeblock}

   - To listen for Syslog messages on the Network mode over TCP

     ```yaml

     [INPUT]
         Name     syslog
         Parser   syslog-rfc3164
         Listen   0.0.0.0
         Port     5140
         Mode     tcp

     ```
    {: codeblock}


   - To listen for Syslog messages on the Unix socket mode over UDP

     ```yaml

     [INPUT]
         Name      syslog
         Parser    syslog-rfc3164
         Path      /tmp/fluent-bit.sock
         Mode      unix_udp
         Unix_Perm 0644

     ```
    {: codeblock}

## Step 2. Stop and start the agent
{: #syslog-s2}

Run the following commands.

```sh
systemctl daemon-reload
```
{: pre}

```sh
systemctl restart fluent-bit
```
{: pre}

Run the following command to start the agent if you want to receive the Syslog messages from localhost in TCP mode.

```sh
<FLUENT-BIT-INSTALL-DIR>/bin/fluent-bit -c /etc/fluent-bit/fluent-bit.conf
```
{: pre}

Do not run the agent to receive the Syslog messages from localhost in TCP mode. Doing so results in recursive reading of logs.
{: important}

## Step 3. Verify that logs are being delivered to your target destination
{: #syslog-s3}

Complete the following steps depending on your target type.

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

2. When your agent is correctly configured, you can see logs through the default dashboard view.
