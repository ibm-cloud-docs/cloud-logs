---

copyright:
  years:  2024, 2025
lastupdated: "2025-11-13"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Linux extension
{: #extensions-linux}

In {{site.data.keyword.logs_full}}, you can use the Linux extension to gain insights into your Linux environment logs.
{: shortdesc}

Linux is a Unix-like, open source and community-developed operating system (OS) for computers, servers, mainframes, mobile devices and embedded devices. It is supported on almost every major computer platform, including x86, ARM and SPARC, making it one of the most widely supported operating systems.

The Linux command is a utility of the Linux operating system. All basic and advanced tasks can be done by running commands. The commands are run on the Linux terminal. The terminal is a command-line interface to interact with the system. Commands in Linux are case-sensitive.



## Before you begin
{: #extensions-linux-overview}

With this extension, you can create alerts for Linux behaviors that might indicate security issues.

When deploying the extension you will need to select:

- `applicationName`: The application name is the environment that produces and sends logs to {{site.data.keyword.logs_full_notm}}.
- `subsystemName`: The subsystem name is the service or application that produces and sends logs to {{site.data.keyword.logs_full_notm}}.


## What this extension deploys
{: #extensions-activity-tracking-deploys}

This extension includes one or more items.

| Includes | Number |
|----------|--------|
| [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts) | 16 |
| [Dashboards](/docs/cloud-logs?topic=cloud-logs-about_dashboards) | 0 |
| [Enrichments](/docs/cloud-logs?topic=cloud-logs-enriching-data) | 0 |
| [Events to metrics](/docs/cloud-logs?topic=cloud-logs-configure-event2metrics) | 0 |
| [Rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) | 1 |
| [Views](/docs/cloud-logs?topic=cloud-logs-custom_views) | 0  |
{: caption="Items included when extension is deployed" caption-side="bottom"}

Before deploying this extension, make sure that deploying the extension will not cause you to exceed [limits for your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-limits). If deploying the extension results in limits being exceeded, the deployment will fail.
{: tip}

## Deploying the extension
{: #extensions-linux-deploy}

You can deploy this extension in any {{site.data.keyword.logs_full_notm}} instance that collects Linux logs. This extension includes a set of pre-configured resources that help you monitor potential security issues.

For more information about deploying the extension, see [Deploying, managing, and removing {{site.data.keyword.logs_full_notm}} extensions](/docs/cloud-logs?topic=cloud-logs-extensions-mgmt).


{{/_include-segments/extensions-validate.md}}

## Parsing rule
{: #extensions-linux-rules}

You can use the provided parsing rule to parse and extract log data to prepare for monitoring and analysis.


The provided parsing rule extracts the Linux command and username from the log message.


## Alerts
{: #extensions-linux-alerts}

You can deploy any of the following alerts:

* `Linux - No Logs From Linux`: This alert triggers if there are no logs in the last 12 hours for Linux in the account.
* `Linux - Suspicious SSH Errors Observed`: This alert triggers whenever suspicious SSH / SSHD error messages are seen that indicate a fatal or suspicious error that could be caused by exploiting attempts.
* `Linux - Anomalous Data Transferred`: This alert triggers whenever anomalous data transfer takes place within a short interval of time on a Linux system using command line tools such as `wget`, `scp`, `rsync`, `ftp`, or `sftp`.
* `Linux - Action performed on Command History`: This alert triggers whenever an action is performed on the file containing the bash command history on a Linux system. A user can either view the command history or delete it. For this alert, the threshold value set is 3 times in 20 minutes. You can modify this threshold value for your requirements.
* `Linux - Kernel Module Activity Observed`: This alert triggers whenever kernel module-related activities such as loading, unloading, and so on are observed on a Linux system.
* `Linux - OS Credentials Dumping Attempted`: This alert triggers whenever someone attempts to view or dump the contents of `/etc/passwd` or `/etc/shadow` files on a Linux system.
* `Linux - SSH Authorized Keys Usage Observed`: This alert triggers whenever a user uses SSH-authorized keys on a Linux system. SSH key pairs are two cryptographically secure keys that can be used to authenticate a client to an SSH server. Each key pair consists of a public key and a private key.
* `Linux - System Time Changed`: This alert triggers whenever the system date and time are changed.
* `Linux - Possible Buffer Overflow Attempt`: This alert triggers whenever a malicious actor makes a buffer overflow attempt. This alert checks for 4 common indicators of buffer overflow.
* `Linux - Data Encoding Observed`: This alert triggers whenever data encoding using `base64` or `execve` is observed in a Linux system.
* `Linux - Ubuntu UFW Firewall Disabled`: This alert triggers when the Ubuntu firewall is disabled and is in an inactive state.
* `Linux - PAM Configuration Modified`: This alert triggers when a user attempts to modify pluggable authentication modules (PAM) on a Linux machine. Linux Pluggable Authentication Modules is a suite of libraries that allows a Linux system administrator to configure methods to authenticate users. It provides a flexible and centralized way to switch authentication methods for secured applications by using configuration files instead of changing application code.
* `Linux - Critical Bash Commands Used`: This alert triggers when critical bash commands such as `cat`, `rm`, `nc`, `ncat`, `netcat`, `useradd`, `cryptcat`, `trap`, `grep`, and so on are run on a Linux machine.
* `Linux - Reverse Shell Command Executed`: This alert triggers whenever a Python or a Bash reverse shell command is executed in a Linux environment.
* `Linux - Kernal Parameters Configuration File Modified`: This alert triggers whenever a user configures kernel parameters on a Linux system by using the `sysctl` command and by modifying the configuration files in the `/etc/sysctl.d/` directory.
* `Linux - Possible Password Spraying Attempt`: This alert triggers when there is a possible password spraying attempt. Password spraying uses one password (for example, `Password01`) or a small list of commonly used passwords that might match the complexity policy of the domain. Logins are attemted with the password against different accounts on a network to avoid account lockouts that would normally occur when brute forcing a single account with many passwords.


