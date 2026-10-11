---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-11"

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
| Set a personal default view | [No]{: tag-red} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| Save column configuration on a view | [No]{: tag-red} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="required permissions" caption-side="bottom"}

Users with Reader access can open shared views and see all their saved preferences, but cannot create, modify, set any view as their personal default, or set an instance-level default view. Only users with Manager role can set, edit, replace or remove the instance-level default view for all the users of the instance. This prevents accidental changes that would affect the default experience for all users of a particular instance.
{: note}

For more information on how to grant permissions to users, see [Assign access to a user by using {{site.data.keyword.iamshort}}.](/docs/iam?topic=iam-account-services&interface=ui).
