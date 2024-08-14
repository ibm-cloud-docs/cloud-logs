---

copyright:
  years:  2024
lastupdated: "2024-08-14"
keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# IP addresses

{: #cidr}

{{site.data.keyword.logs_full}} data will be sent from these addresses. You can use these IP addresses in firewalls and other configurations to ensure that the data received by your code, or another {{site.data.keyword.IBM_notm}} service, originates only from {{site.data.keyword.logs_full}}.
{: shortdesc}

## Public IP addresses

These public IP addresses are used to send events to {{site.data.keyword.en_full}} and stream logs to {{site.data.keyword.messagehub}}.

{: #cidr_public_gen2}

### Frankfurt

{: #cidr_public_gen2_3}

| Region      | IP address     |
| ----------- | -------------- |
| Frankfurt 1 | 149.81.7.29    |
| Frankfurt 2 | 161.156.82.254 |
| Frankfurt 3 | 149.81.165.38  |
{: caption="Table 2. Frankfurt public IP addresses" caption-side="top"}

### London

{: #cidr_public_gen2_5}

| Region   | IP address      |
| -------- | --------------- |
| London 1 | 161.156.199.245 |
| London 2 | 141.125.111.204 |
| London 3 | 158.176.189.154 |
{: caption="Table 3. London public IP addresses" caption-side="top"}

### Madrid

{: #cidr_public_madrid}

| Region   | IP address    |
| -------- | ------------- |
| Madrid 1 | 13.120.86.96  |
| Madrid 2 | 13.121.81.233 |
| Madrid 3 | 13.122.90.134 |
{: caption="Table 4. Madrid public IP addresses" caption-side="top"}



### Toronto

{: #cidr_public_gen2_10}

| Region    | IP address    |
| --------- | ------------- |
| Toronto 1 | 163.66.94.68  |
| Toronto 2 | 163.74.88.241 |
| Toronto 3 | 163.74.88.241 |
{: caption="Table 9. Toronto public IP addresses" caption-side="top"}

### US East

{: #cidr_public_gen2_2}

| Region          | IP address     |
| --------------- | -------------- |
| Washington DC 1 | 150.239.81.194 |
| Washington DC 2 | 169.63.190.140 |
| Washington DC 3 | 150.239.222.67 |
{: caption="Table 10. US-East public IP addresses" caption-side="top"}

### US South

{: #cidr_public_gen2_1}

| Region   | IP address      |
| -------- | --------------- |
| Dallas 1 | 52.116.131.73   |
| Dallas 2 | 150.239.164.167 |
| Dallas 3 | 52.118.79.29    |
{: caption="Table 11. US-South public IP addresses" caption-side="top"}

## Private IP addresses

These private IP addresses are used to archive logs to {{site.data.keyword.cos_full_notm}}

{: #cidr_private_gen2}

### Frankfurt

{: #cidr_private_gen2_14}

| Region      | IP address    |
| ----------- | ------------- |
| Frankfurt 1 | 10.16.206.126 |
| Frankfurt 2 | 10.16.212.60  |
| Frankfurt 3 | 10.223.57.126 |
{: caption="Table 13. Frankfurt private IP addresses" caption-side="top"}

### London

{: #cidr_private_gen2_16}

| Region   | IP address     |
| -------- | -------------- |
| London 1 | 10.249.102.93  |
| London 2 | 10.249.105.135 |
| London 3 | 10.223.22.101  |
{: caption="Table 14. London private IP addresses" caption-side="top"}

### Madrid

{: #cidr_private_madrid}

| Region    | IP address    |
| --------- | ------------- |
| Madrid 1  | 10.22.182.15  |
| Madrid 2  | 10.22.189.164 |
| Madrid  3 | 10.22.211.255 |
{: caption="Table 15. Madrid public IP addresses" caption-side="top"}



### Toronto

{: #cidr_private_gen2_21}

| Region    | IP address     |
| --------- | -------------- |
| Toronto 1 | 10.223.153.79  |
| Toronto 2 | 10.223.168.204 |
| Toronto 3 | 10.223.176.163 |
{: caption="Table 20. Toronto private IP addresses" caption-side="top"}

### US South

{: #cidr_private_gen2_12}

| Region   | IP address    |
| -------- | ------------- |
| Dallas 1 | 10.22.216.234 |
| Dallas 2 | 10.249.200.0  |
| Dallas 3 | 10.249.211.95 |
{: caption="Table 21. US-South private IP addresses" caption-side="top"}

### US East

{: #cidr_private_gen2_13}

| Region          | IP address   |
| --------------- | ------------ |
| Washington DC 1 | 10.22.41.104 |
| Washington DC 2 | 10.22.53.64  |
| Washington DC 3 | 10.22.56.46  |
{: caption="Table 22. US-East private IP addresses" caption-side="top"}
