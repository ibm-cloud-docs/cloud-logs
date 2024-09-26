---

copyright:
  years:  2024
lastupdated: "2024-09-26"
keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# IP addresses that must be opened in firewalls
{: #ips2open}

{{site.data.keyword.logs_full}} data is sent using specific IP addresses.
{: shortdesc}

## IP addresses used by {{site.data.keyword.logs_full_notm}} to connect to other services
{: #ip_to_services}

Use these IP addresses in firewalls and other configurations to ensure that the data received by your code, or another {{site.data.keyword.IBM_notm}} service, originates only from {{site.data.keyword.logs_full_notm}}.

### IP addresses used for {{site.data.keyword.cos_full_notm}}
{: #ip_cos}

These private IP addresses are used to archive logs to {{site.data.keyword.cos_full_notm}}.


| Region      | IP addresses     |
| ----------- | -------------- |
| Dallas (`us-south`) |  10.22.216.234  \n 10.249.200.0  \n 10.249.211.95 |
| Frankfurt (`eu-de`) | 10.16.206.126  \n 10.16.212.60  \n 10.223.57.126 |
| London (`eu-gb`) | 10.249.102.93  \n 10.249.105.135  \n 10.223.22.101 |
| Madrid (`eu-es`) | 10.22.182.15  \n 10.22.189.164  \n 10.22.211.255 |
| Osaka (`jp-osa`) | 10.12.22.161  \n 10.12.30.38  \n 10.12.46.24  |
| Sao Paulo (`br-sao`) | 10.12.178.24  \n 10.12.79.160  \n 10.51.193.140 |
| Sydney (`au-syd`) | 10.223.237.71  \n 10.223.243.160  \n 10.223.254.90 |
| Tokyo (`jp-tok`) | 10.223.197.221  \n 10.223.208.108  \n 10.223.220.15 |
| Toronto (`ca-tor`) | 10.223.153.79  \n 10.223.168.204  \n 10.223.176.163 |
| Washington, DC (`us-east`) | 10.22.41.104  \n 10.22.53.64  \n 10.22.56.46 |
{: caption="Private IP addresses for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

### IP addresses used for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}
{: #ip_en_es}

These public IP addresses are used to send events to {{site.data.keyword.en_full_notm}} and stream logs to {{site.data.keyword.messagehub_full}}.

| Region      | IP addresses     |
| ----------- | -------------- |
| Dallas (`us-south`) | 52.116.131.73  \n 150.239.164.167  \n 52.118.79.29 |
| Frankfurt (`eu-de`) | 149.81.7.29  \n 161.156.82.254  \n 149.81.165.38 |
| London (`eu-gb`) | 161.156.199.245  \n 141.125.111.204  \n 158.176.189.154 |
| Madrid (`eu-es`) | 13.120.86.96  \n 13.121.81.233  \n 13.122.90.134 |
| Osaka (`jp-osa`) | 163.68.90.193  \n 163.69.93.0  \n 163.73.83.233 |
| Sao Paulo (`br-sao`) | 13.116.82.31  \n 163.107.85.232  \n 163.109.87.9 |
| Sydney (`au-syd`) | 159.23.94.217  \n 130.198.9.241  \n 135.90.138.121 |
| Tokyo (`jp-tok`) | 162.133.137.8  \n 128.168.136.18  \n 165.192.138.249 |
| Toronto (`ca-tor`) | 163.66.94.68  \n 163.74.88.241  \n 163.74.88.241 |
| Washington, DC (`us-east`) | 150.239.81.194  \n 169.63.190.140  \n 150.239.222.67 |
{: caption="Public IP addresses for {{site.data.keyword.en_short}} and {{site.data.keyword.messagehub}}" caption-side="top"}


## IP addresses used by {{site.data.keyword.logs_full_notm}} private endpoints
{: #ip_endpoints}

The {{site.data.keyword.logs_full_notm}} private endpoints can be used to send logs, query logs or manage the instance. Use these IP addresses in firewalls and other configurations to ensure that the data sent by your code, is sent to {{site.data.keyword.logs_full_notm}}.

### Private ingress endpoints for {{site.data.keyword.logs_full_notm}}
{: #ip_ingress}

These are private ingress endpoints IP addresses for {{site.data.keyword.logs_full_notm}}.

| Region      | IP addresses     |
| ----------- | -------------- |
| Dallas (`us-south`) | 166.9.228.72  \n 166.9.229.63  \n 166.9.230.56 |
| Frankfurt (`eu-de`) | 166.9.209.206  \n 166.9.209.232  \n 166.9.210.12 |
| London (`eu-gb`) | 166.9.245.168  \n 166.9.245.200  \n 166.9.245.232 |
| Madrid (`eu-es`) | 166.9.226.22  \n 166.9.227.21  \n 166.9.225.20 |
| Osaka (`jp-osa`) | 166.9.247.54  \n 166.9.247.84  \n 166.9.247.118 |
| Sao Paulo (`br-sao`) | 166.9.246.86  \n 166.9.246.118  \n 166.9.246.142 |
| Sydney (`au-syd`) | 166.9.244.118  \n 166.9.244.150  \n 166.9.244.182 |
| Tokyo (`jp-tok`) | 166.9.249.125  \n 166.9.249.154  \n 166.9.249.190 |
| Toronto (`ca-tor`) | 166.9.209.7  \n 166.9.247.184  \n 166.9.247.221 |
| Washington, DC (`us-east`) | 166.9.231.251  \n 166.9.251.88  \n 166.9.233.27 |
{: caption="IP addresses for {{site.data.keyword.logs_full_notm}} private ingress endpoints" caption-side="top"}


### Private API endpoints for {{site.data.keyword.logs_full_notm}}
{: #ip_api}

These are the private API IP addresses used for {{site.data.keyword.logs_full_notm}}.

| Region      | IP addresses     |
| ----------- | -------------- |
| Dallas (`us-south`) | 166.9.228.70  \n 166.9.229.140  \n 166.9.230.27 |
| Frankfurt (`eu-de`) | 166.9.209.200  \n 166.9.209.233  \n 166.9.210.8 |
| London (`eu-gb`) | 166.9.245.169  \n 166.9.245.201  \n 166.9.245.233 |
| Madrid (`eu-es`) | 166.9.226.26  \n 166.9.227.25  \n 166.9.225.24 |
| Osaka (`jp-osa`) | 166.9.247.55  \n 166.9.247.85  \n 166.9.247.119 |
| Sao Paulo (`br-sao`) | 166.9.246.85  \n 166.9.246.117  \n 166.9.246.141 |
| Sydney (`au-syd`) | 166.9.244.117  \n 166.9.244.149  \n 166.9.244.181 |
| Tokyo (`jp-tok`) | 166.9.249.126  \n 166.9.249.155  \n 166.9.249.164 |
| Toronto (`ca-tor`) | 166.9.209.6  \n 166.9.209.34  \n 166.9.247.202 |
| Washington, DC (`us-east`) | 166.9.231.250  \n 166.9.251.87  \n 166.9.233.26 |
{: caption="{{site.data.keyword.logs_full_notm}} private API IP addresses" caption-side="top"}
