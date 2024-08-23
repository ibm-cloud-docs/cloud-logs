---

copyright:
  years:  2024
lastupdated: "2024-08-23"
keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# IP addresses that must be opened in firewalls
{: #ips2open}

{{site.data.keyword.logs_full}} data is sent from specific IP addresses. Use these IP addresses in firewalls and other configurations to ensure that the data received by your code, or another {{site.data.keyword.IBM_notm}} service, originates only from {{site.data.keyword.logs_full}}.
{: shortdesc}

## IP addresses used for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}
{: #ip_en_es}

These public IP addresses are used to send events to {{site.data.keyword.en_full_notm}} and stream logs to {{site.data.keyword.messagehub_full}}.

### Frankfurt
{: #ip_en_es_eufr}

| Region      | IP address     |
| ----------- | -------------- |
| Frankfurt 1 | 149.81.7.29    |
| Frankfurt 2 | 161.156.82.254 |
| Frankfurt 3 | 149.81.165.38  |
{: caption="Frankfurt public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}

### London
{: #ip_en_es_eugb}

| Region   | IP address      |
| -------- | --------------- |
| London 1 | 161.156.199.245 |
| London 2 | 141.125.111.204 |
| London 3 | 158.176.189.154 |
{: caption="London public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}


### Madrid
{: #ip_en_es_eues}

| Region   | IP address    |
| -------- | ------------- |
| Madrid 1 | 13.120.86.96  |
| Madrid 2 | 13.121.81.233 |
| Madrid 3 | 13.122.90.134 |
{: caption="Madrid public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}





### Sydney
{: #ip_en_es_ausyd}

| Region   | IP address     |
| -------- | -------------- |
| Sydney 1 | 159.23.94.217  |
| Sydney 2 | 130.198.9.241  |
| Sydney 3 | 135.90.138.121 |
{: caption="Sydney public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}

### Tokyo
{: #ip_en_es_jptok}

| Region  | IP address      |
| ------- | --------------- |
| Tokyo 1 | 162.133.137.8   |
| Tokyo 2 | 128.168.136.18  |
| Tokyo 3 | 165.192.138.249 |
{: caption="Tokyo public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}

### Toronto
{: #ip_en_es_cator}

| Region    | IP address    |
| --------- | ------------- |
| Toronto 1 | 163.66.94.68  |
| Toronto 2 | 163.74.88.241 |
| Toronto 3 | 163.74.88.241 |
{: caption="Toronto public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}

### US East (Washington)
{: #ip_en_es_useast}

| Region          | IP address     |
| --------------- | -------------- |
| Washington DC 1 | 150.239.81.194 |
| Washington DC 2 | 169.63.190.140 |
| Washington DC 3 | 150.239.222.67 |
{: caption="US-East public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}

### US South (Dallas)
{: #ip_en_es_ussouth}

| Region   | IP address      |
| -------- | --------------- |
| Dallas 1 | 52.116.131.73   |
| Dallas 2 | 150.239.164.167 |
| Dallas 3 | 52.118.79.29    |
{: caption="US-South public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}

## IP addresses used for {{site.data.keyword.cos_full_notm}}
{: #ip_cos}

These private IP addresses are used to archive logs to {{site.data.keyword.cos_full_notm}}.

### Frankfurt
{: #ip_cos_eufr}

| Region      | IP address    |
| ----------- | ------------- |
| Frankfurt 1 | 10.16.206.126 |
| Frankfurt 2 | 10.16.212.60  |
| Frankfurt 3 | 10.223.57.126 |
{: caption="Frankfurt private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

### London
{: #ip_cos_eugb}

| Region   | IP address     |
| -------- | -------------- |
| London 1 | 10.249.102.93  |
| London 2 | 10.249.105.135 |
| London 3 | 10.223.22.101  |
{: caption="London private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

### Madrid
{: #ip_cos_eues}

| Region    | IP address    |
| --------- | ------------- |
| Madrid 1  | 10.22.182.15  |
| Madrid 2  | 10.22.189.164 |
| Madrid  3 | 10.22.211.255 |
{: caption="Madrid public IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}





### Sydney
{: #ip_cos_ausyd}

| Region   | IP address     |
| -------- | -------------- |
| Sydney 1 | 10.223.237.71  |
| Sydney 2 | 10.223.243.160 |
| Sydney 3 | 10.223.254.90  |
{: caption="Sydney private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

### Tokyo
{: #ip_cos_jptok}

| Region  | IP address     |
| ------- | -------------- |
| Tokyo 1 | 10.223.197.221 |
| Tokyo 2 | 10.223.208.108 |
| Tokyo 3 | 10.223.220.15  |
{: caption="Tokyo private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}


### Toronto
{: #ip_cos_cator}

| Region    | IP address     |
| --------- | -------------- |
| Toronto 1 | 10.223.153.79  |
| Toronto 2 | 10.223.168.204 |
| Toronto 3 | 10.223.176.163 |
{: caption="Toronto private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

### US South (Dallas)
{: #ip_cos_ussouth}

| Region   | IP address    |
| -------- | ------------- |
| Dallas 1 | 10.22.216.234 |
| Dallas 2 | 10.249.200.0  |
| Dallas 3 | 10.249.211.95 |
{: caption="US-South private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

### US East (Washington)
{: #ip_cos_useast}

| Region          | IP address   |
| --------------- | ------------ |
| Washington DC 1 | 10.22.41.104 |
| Washington DC 2 | 10.22.53.64  |
| Washington DC 3 | 10.22.56.46  |
{: caption="US-East private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}
