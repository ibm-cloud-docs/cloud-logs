---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# Configuring the {{site.data.keyword.logs_routing_full}} agent for (r)Syslog logs
{: #agent-rsyslog}

You can deploy an {{site.data.keyword.logs_routing_full_notm}} agent to collect and route (r)Syslog messages from a Syslog server to a target of your choice. Valid targets are {{site.data.keyword.la_short}} and {{site.data.keyword.logs_full_notm}} instances.
{: shortdesc}


## Before you begin
{: #syslog-prereq}

Be sure that you have deployed the {{site.data.keyword.logs_routing_full_notm}} agent on Linux.
For more information, see [Managing the agent Linux environments](/docs/logs-router?topic=logs-router-agent-linux).


## Step 1. Setting up the {{site.data.keyword.logs_routing_full_notm}} agent configuration
{: #syslog-s1}

You can configure the {{site.data.keyword.logs_routing_full_notm}} agent to collect (r)Syslog messages through a Unix socket server (UDP or TCP) or over the network using TCP or UDP. 

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

### {{site.data.keyword.la_full_notm}} targets
{: #syslog-la}

1. [Go to the web UI for your {{site.data.keyword.la_short}} instance.](/docs/log-analysis?topic=log-analysis-launch&interface=ui)

2. When your agent is correctly configured, you can see logs through the default dashboard view. 

### {{site.data.keyword.logs_full_notm}} targets
{: #syslog-logs}

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

2. When your agent is correctly configured, you can see logs through the default dashboard view. 



