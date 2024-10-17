---

copyright:
  years:  2024
lastupdated: "2024-10-17"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting a timeout error when running my Linux agent configuration script. What do I do?
{: #ts-no-public}
{: troubleshoot}
{: support}

When running the Linux agent `post-config.sh` configuration script I get a timeout message.
{: shortdesc}

You get the following error message: 
{: tsSymptoms}

```text
"msg":"Error setting up IAM Tokenmanager","error":"timeout while trying to set up Tokenmanager","stacktrace":"main.FLBPluginInit\n\t/root/pkg/plugin/logger-icl-output-plugin.go:80\n_cgoexp_eee5b56c7e4a_FLBPluginInit\n\t_cgo_gotypes.go:68\nruntime.cgocallbackg1\n\t/usr/local/go/src/runtime/cgocall.go:315\nruntime.cgocallbackg\n\t/usr/local/go/src/runtime/cgocall.go:234\nruntime.cgocallback\n\t/usr/local/go/src/runtime/asm_amd64.s:998"}

[error] [go proxy]: plugin 'logger-icl-output-plugin' failed to initialize
```
{: screen}


Your system does not have access to the public internet.
{: tsCauses}


Change your configuration to use a private endpoint. Specify `PrivateProduction` for `IAM_Environment` in your [output plugin parameters](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters#agent-plugin-parameters-authentication-parms) in your `/etc/fluent-bit/output-logs-router-agent.conf` file or specify the `-i PrivateProduction` option when running the [`post-config.sh` configuration script](/docs/cloud-logs?topic=cloud-logs-agent-linux#agent-linux-deploy-step2).
{: tsResolve}

The API key used for the agent must have the [`sender`](/docs/cloud-logs?topic=cloud-logs-iam) role to {{site.data.keyword.logs_full_notm}}.
{: note}
