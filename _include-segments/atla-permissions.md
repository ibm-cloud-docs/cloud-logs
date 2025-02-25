Due to the deprecation of {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}}, you might not be able to configure permissions for these two services using the UI. Permissions can be configured using the IBM Cloud CLI.

To configure permissions for {{site.data.keyword.la_full_notm}}, run:

```text
ibmcloud iam user-policy-create <USER_NAME> --roles <ROLES> --servicename logdna
```
{: pre}

To configure permissions for {{site.data.keyword.at_full_notm}}, run:

```text
ibmcloud iam user-policy-create <USER_NAME> --roles <ROLES> --servicename logdnaat
```
{: pre}

Where:

USER_NAME
:   Is the IBM Cloud user to be given the specified roles.

ROLES
:   Is a comma-delimited list of roles authorized for the user.

    If you are migrating manually, and not using the migration tool, you will need to configure the `manager` role as well.
    {: important}

