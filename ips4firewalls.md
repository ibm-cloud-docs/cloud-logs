---

copyright:
  years:  2024
lastupdated: "2024-09-25"
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


### Osaka
{: #ip_en_es_jposa}

| Region  | IP address    |
| ------- | ------------- |
| Osaka 1 | 163.68.90.193 |
| Osaka 2 | 163.69.93.0   |
| Osaka 3 | 163.73.83.233 |
{: caption="Osaka public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}

### Sao Paulo
{: #ip_en_es_brsao}

| Region      | IP address     |
| ----------- | -------------- |
| Sao Paulo 1 | 13.116.82.31   |
| Sao Paulo 2 | 163.107.85.232 |
| Sao Paulo 3 | 163.109.87.9   |
{: caption="Sao Paulo public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}


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


### Osaka
{: #ip_cos_jposa}

| Region  | IP address   |
| ------- | ------------ |
| Osaka 1 | 10.12.22.161 |
| Osaka 2 | 10.12.30.38  |
| Osaka 3 | 10.12.46.24  |
{: caption="Osaka private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

### Sao Paulo
{: #ip_cos_brsao}

| Region      | IP address    |
| ----------- | ------------- |
| Sao Paulo 1 | 10.12.178.24  |
| Sao Paulo 2 | 10.12.79.160  |
| Sao Paulo 3 | 10.51.193.140 |
{: caption="Sao Paulo private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}


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

## Private ingress endpoints for {{site.data.keyword.logs_full_notm}}
{: #ip_ingress}

The following table shows the private ingress endpoints for {{site.data.keyword.logs_full_notm}}.

### Frankfurt
{: #ip_ingress_eufr}

| Region      | IP address    |
| ----------- | ------------- |
| Frankfurt (eu-de) | 166.9.209.206 |
|  | 166.9.209.232 |
|  | 166.9.210.12 |
{: caption="Frankfurt private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### London
{: #ip_ingress_eugb}

| Region   | IP address     |
| -------- | -------------- |
| London (eu-gb)| 166.9.245.168 |
|  | 166.9.245.200 |
|  | 166.9.245.232 |
{: caption="London private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### Madrid
{: #ip_ingress_eues}

| Region    | IP address    |
| --------- | ------------- |
| Madrid (eu-es)  | 166.9.226.22 |
|  | 166.9.227.21 |
|  | 166.9.225.20 |
{: caption="Madrid private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


### Osaka
{: #ip_ingress_jposa}

| Region  | IP address   |
| ------- | ------------ |
| Osaka (jp-osa) | 166.9.247.54 |
|  | 166.9.247.84 |
|  | 166.9.247.118 |
{: caption="Osaka private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### Sao Paulo
{: #ip_ingress_brsao}

| Region      | IP address    |
| ----------- | ------------- |
| Sao Paulo (br-sao) | 166.9.246.86 |
|  | 166.9.246.118 |
|  | 166.9.246.142 |
{: caption="Sao Paulo private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


### Sydney
{: #ip_ingress_ausyd}

| Region   | IP address     |
| -------- | -------------- |
| Sydney (au-syd) | 166.9.244.118 |
|  | 166.9.244.150 |
|  | 166.9.244.182 |
{: caption="Sydney private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### Tokyo
{: #ip_ingress_jptok}

| Region  | IP address     |
| ------- | -------------- |
| Tokyo (jp-tok)  | 166.9.249.125 |
|  | 166.9.249.154 |
|  | 166.9.249.190 |
{: caption="Tokyo private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


### Toronto
{: #ip_ingress_cator}

| Region    | IP address     |
| --------- | -------------- |
| Toronto (ca-tor) | 166.9.209.7 |
|  | 166.9.247.184 |
|  | 166.9.247.221 |
{: caption="Toronto private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### US South (Dallas)
{: #ip_ingress_ussouth}

| Region   | IP address    |
| -------- | ------------- |
| Dallas (us-south) | 166.9.228.72 |
|  | 166.9.229.63 |
|  | 166.9.230.56 |
{: caption="US-South private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### US East (Washington)
{: #ip_ingress_useast}

| Region          | IP address   |
| --------------- | ------------ |
| Washington DC (us-east) | 166.9.231.251 |
|  | 166.9.251.88 |
|  | 166.9.233.27 |
{: caption="US-East private ingress IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

## Private API endpoints for {{site.data.keyword.logs_full_notm}}
{: #ip_api}

These private API IP addresses are used to archive logs to {{site.data.keyword.logs_full_notm}}.

### Frankfurt
{: #ip_api_eufr}

| Region               | IP address    |
| ----------------- | ------------- |
| Frankfurt (eu-de) | 166.9.209.200 |
|                   | 166.9.209.233 |
|                   | 166.9.210.8   |
{: caption="Frankfurt private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}ip

### London
{: #ip_api_eugb}

| Region         | IP address    |
| -------------- | ------------- |
| London (eu-gb) | 166.9.245.169 |
|                | 166.9.245.201 |
|                | 166.9.245.233 |
{: caption="London private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### Madrid
{: #ip_api_eues}

| Region         | IP address   |
| -------------- | ------------ |
| Madrid (eu-es) | 166.9.226.26 |
|                | 166.9.227.25 |
|                | 166.9.225.24 |
{: caption="Madrid private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


### Osaka
{: #ip_api_jposa}

| Region         | IP address    |
| -------------- | ------------- |
| Osaka (jp-osa) | 166.9.247.55  |
|                | 166.9.247.85  |
|                | 166.9.247.119 |
{: caption="Osaka private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### Sao Paulo
{: #ip_api_brsao}

| Region             | IP address    |
| ------------------ | ------------- |
| Sao Paulo (br-sao) | 166.9.246.85  |
|                    | 166.9.246.117 |
|                    | 166.9.246.141 |
{: caption="Sao Paulo private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


### Sydney
{: #ip_api_ausyd}

| Region          | IP address    |
| --------------- | ------------- |
| Sydney (au-syd) | 166.9.244.117 |
|                 | 166.9.244.149 |
|                 | 166.9.244.181 |
{: caption="Sydney private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### Tokyo
{: #ip_api_jptok}

| Region           | IP address    |
| ---------------- | ------------- |
| Tokyo (jp-tok)   | 166.9.249.126 |
|                  | 166.9.249.155 |
|                  | 166.9.249.164 |
{: caption="Tokyo private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


### Toronto
{: #ip_api_cator}

| Region           | IP address    |
| ---------------- | ------------- |
| Toronto (ca-tor) | 166.9.209.6   |
|                  | 166.9.209.34  |
|                  | 166.9.247.202 |
{: caption="Toronto private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### US South (Dallas)
{: #ip_api_ussouth}

| Region            | IP address    |
| ----------------- | ------------- |
| Dallas (us-south) | 166.9.228.70  |
|                   | 166.9.229.140 |
|                   | 166.9.230.27  |
{: caption="US-South private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

### US East (Washington)
{: #ip_api_useast}

| Region                  | IP address    |
| ------------------------| ------------- |
| Washington DC (us-east) | 166.9.231.250 |
|                         | 166.9.251.87  |
|                         | 166.9.233.26  |
{: caption="US-East private API IP addresses for {{site.data.keyword.logs_full_notm}}" caption-side="top"}
