---

copyright:
  years:  2024
lastupdated: "2024-09-25"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Required permissions to work with views
{: #iam-views}

You can configure {{site.data.keyword.iamlong}} to manage the permissions that you grant users to work with private and shared views in an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

| Service role         | Reader             | Writer              | Manager             |
|----------------------|--------------------|---------------------|---------------------|
| View shared views    | [Yes]{: tag-green} | [Yes]{: tag-green}  | [Yes]{: tag-green}  |
| View private views   | [No]{: tag-red}    | [Yes]{: tag-green}  | [Yes]{: tag-green}  |
| Manage shared views  | [No]{: tag-red}    | [Yes]{: tag-green}  | [Yes]{: tag-green}  |
| Manage private views | [No]{: tag-red}    | [Yes]{: tag-green}  | [Yes]{: tag-green}  |


For more information on how to grant permissions to users, see [Assign access to a user by using {{site.data.keyword.iamshort}}.](/docs/account?topic=account-cloudaccess)
