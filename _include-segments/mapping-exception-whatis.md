A mapping exception can happen if new log fields are ingested with field names that were previously ingested by {{site.data.keyword.logs_full_notm}}, but have a different value type.  When {{site.data.keyword.logs_full_notm}} indexes ingested data, it tries to map the fields to one of the following types:

* `String`
* `Numeric`
* `Object`
* `Array`

If, for example, the field `user` has been ingested and the first received value is “username”, {{site.data.keyword.logs_full_notm}} will create an index of type `string` for the field `user`:

```json
"user": “username”`
```
{: codeblock}

If later on a new log is ingested that also has a field named “user” that is formatted like this:

```json
"user": {
  “email”: “username@yourcompany.com”,
  ”login”: “username”`
}
```
{: codeblock}

A mapping exception is created in {{site.data.keyword.logs_full_notm}}. Any searches looking for a field named `user` would be expected to have a `string` value based on the first log ingested with a `user` field.

Any searches looking for a `user` with the `array` type (`user.email` or `user.login`) will not return any results due to the mapping exception.
