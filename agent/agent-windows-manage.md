---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing the Windows agent
{: #agent-windows-manage}

You can deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from Windows systems to an {{site.data.keyword.logs_full_notm}} instance. For more information on supported Windows environments, see [{{site.data.keyword.agent}} for non-orchestarted environments](/docs/cloud-logs?topic=cloud-logs-agent-about#agent-about-std).
{: shortdesc}

The agent can be run as a Windows service to collect logs in the background. You can manage the agent by using `sc.exe`.


## Deploying the agent
{: #agent-windows-manage-deploy}

See [Deploying the {{site.data.keyword.agent}} for Windows](/docs/cloud-logs?topic=cloud-logs-agent-windows).

## Removing the logging agent
{: #agent-windows-manage-delete}

To remove the agent, remove the application directory.

   * Using the command prompt:

     ```bat
     rmdir /S "C:\Program Files\logs-agent"
     ```
     {: pre}

   * Using Powershell:

     ```bat
     Remove-Item -Path "C:\Program Files\logs-agent" -Recurse -Force
     ```
     {: pre}



## Updating the logging agent
{: #agent-windows-manage-update}

To update the agent, download a new agent Windows agent ZIP archive and follow the instructions below to update the {{site.data.keyword.agent}}. For information about the current {{site.data.keyword.agent}} version, see the [agent release notes](/docs/cloud-logs?topic=cloud-logs-release-notes-agent). For instructions on installing the Windows agent, see [Deploy agent for Windows servers](/docs/cloud-logs?topic=cloud-logs-agent-windows#agent-windows-deploy-step3).

1. Expand the Windows agent archive in the `upgrade` directory of your currently installed agent using Powershell.

     ```bat
     Expand-Archive -Path <archive_filename> -DestinationPath "C:\Program Files\logs-agent\upgrade"
     ```
     {: pre}

   Where `<archive_filename>` is the name of the downloaded `*.zip` file.

2. Copy the upgraded {{site.data.keyword.agent}} program files.

    ```bat
    Get-ChildItem -Path "C:\Program Files\logs-agent\upgrade\logs-agent\bin" -Include *.exe,*.dll -File -Recurse | Copy-Item -Destination "C:\Program Files\logs-agent\bin" -Force
    Get-ChildItem -Path "C:\Program Files\logs-agent\upgrade\logs-agent\version.txt"  -File -Recurse | Copy-Item -Destination "C:\Program Files\logs-agent\version.txt" -Force
    ```
    {: pre}

3. Remove the temporary upgrade files.

    ```bat
    Remove-Item -Path "C:\Program Files\logs-agent\upgrade\" -Recurse -Force

    Remove-Item -Path $extractPath -Recurse -Force
    ```
    {: pre}


## Finding the installed agent version
{: #agent-windows-find-version}

Run the following command to find the installed agent version:

   * Using the command prompt:

     ```bat
     type "C:\Program Files\logs-agent\version.txt"
     ```
     {: pre}
 
   * Using Powershell:

     ```bat
     Get-Content -Path "C:\Program Files\logs-agent\version.txt"
     ```
     {: pre}


## Creating a service that can be started and stopped by a non-root user
{: #agent-windows-nonroot}

By default, only administrators can manage services. To grant a specific user or group the ability to start and stop the service, use `sc.exe sdset` to modify the sercurity descriptor of the agent service.

   * Get the current security descriptor by running the following command.

     ```bat
     sc.exe sdshow fluent-bit
     ```
     {: pre}

     The output will be the security descriptor for the agent service and will be similar to the following.

     ```bat
     D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A; ;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)
     ```
     {: pre}

   * Add a new user to the service security descriptor.

     The format for granting permissions is `A;;RPWP;;;SID` where `RP` and `WP` are permissions to start and stop the service, and `SID` is the security identifier if a user or group.

     ```bat
     sc.exe sdset fluent-bit D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)(A;;RPWP;;;S-1-5-21-USER_SID)
     ```
     {: pre}
