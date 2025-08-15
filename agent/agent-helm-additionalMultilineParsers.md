---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring custom multiline parsers
{: #agent-helm-additionalMultilineParsers}

If you need to introduce a new multiline parser, the `additionalMultilineParsers` option allows you to introduce your own multiline parsers. This will add entries to the [multiline_parsers](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/multiline-parsers-section) section of the Fluent Bit yaml configuration.

```yaml
additionalMultilineParsers:
  - name: multiline_sample
    type: regex
    flush_timeout: 1000
    rules:
      - state: start_state
        regex: '/^\[\d+\/\d+\/\d+,.*$/'
        next_state: cont
      - state: cont
        regex: '/^[^\[].*$/'
        next_state: cont
      - state: cont
        regex: '/^$/'
        next_state: cont
```
{: screen}
