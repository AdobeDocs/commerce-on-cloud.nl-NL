---
title: Regionale IP-adressen
description: Zie een lijst met IP-adressen voor de AWS- en Azure-regio's die door Adobe Commerce worden gebruikt op cloudinfrastructuur voor integratieomgevingen.
exl-id: 1137f5cf-4879-46d7-878c-bf47de7a0e34
source-git-commit: f2214dd56625847132298892635c7cf738c3d71f
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Regionale IP-adressen

De volgende lijsten maken een lijst van de inkomende en uitgaande IP adressen die door Adobe Commerce op de milieu&#39;s van de cloudinfrastructuur [ integratie ](../architecture/pro-architecture.md#integration-environment) worden gebruikt. Deze IP adressen zijn stabiel, maar zouden kunnen veranderen. Adobe brengt klanten op de hoogte alvorens om het even welke IP adresveranderingen aan te brengen.

De syntaxis voor het aanpakken van de integratieomgevingen is als volgt:

```text
<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud
```

- **Unieke identiteitskaart** = 7 willekeurige alpha-numerieke karakters
- **identiteitskaart van het Project** = 13-karakter project identiteitskaart
- **Gebied** = AWS of Azure gebiedsnaam

U kunt de opdracht `ping` of `dig` gebruiken om het inkomende IP-adres op te halen:

**pingelen**

```bash
ping integration-abcd123-abcd78910.us-3.magentosite.cloud
```

Monsterrespons:

```console
PING integration-abcd123-abcd78910.us-3.magentosite.cloud (34.210.133.187): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
```

**Dig**

```bash
dig +short integration-abcd123-abcd78910.us-3.magentosite.cloud
```

Samplereactie

```bash
34.210.133.187
```

Als u een collectieve firewall hebt die de uitgaande verbindingen van SSH blokkeert, kunt u de binnenkomende IP adressen aan uw lijst van gewenste personen toevoegen.

## AWS-regio&#39;s

|     | Verenigde Staten |       |      | Europa |      |      |      | Azië-Stille Oceaan |
| --- | :------------ | :---- | :--- | :----- | :--- | :--- | :--- | :----------- |
|     | VS | VS-3 | VS-5 | EU | EU-3 | EU-5 | EU-6 | AP-3 |
| Binnenkomend | <!--US-->52.200.159.23<p>52.200.159.125<p>52.200.160.5 | <!--US-3-->34.210.133.187<p>34.214.72.239<p>34.215.10.85 | <!--US-5-->50.112.160.58<p>54.213.195.223<p>35.163.170.185 | <!--EU-->52.209.44.44<p>52.209.23.96<p>52.51.117.101 | <!--EU-3-->34.240.75.192<p>34.251.110.37<p>52.19.113.35 | <!--EU-5-->35.157.81.88<p>3.122.198.131<p>52.28.102.195 | <!--EU-6-->35.181.23.47<p>35.181.24.165<p>35.180.237.48 | <!--AP-3-->52.65.39.201<p>52.65.10.202<p>52.65.30.37 |
| Uitgaand | <!--US-->52.200.155.111<p>52.200.149.44<p>50.17.163.75 | <!--US-3-->34.210.166.180<p>34.215.83.92<p>34.213.20.158 | <!--US-5-->54.70.238.217<p>52.88.113.98<p>52.36.188.230 | <!--EU-->52.51.163.159<p>52.209.44.60<p>52.208.156.247 | <!--EU-3-->34.240.57.142<p>52.16.140.48<p>52.209.134.55 | <!--EU-5-->3.121.163.221<p>3.121.79.229<p>18.197.3.230 | <!--EU-6-->52.47.155.26<p>35.181.0.157<p>35.181.12.15 | <!--AP-3-->52.65.143.178<p>13.54.80.197<p>52.62.224.4 |

## Azure-gebieden

|          | Verenigde Staten | Europa |
| -------- | :-------------- | :-------------- |
|          | US-A1 | AZ-WESTEUROPE-1 |
| Binnenkomend | <!--US-A1--> 20.186.27.68<p>20.186.58.163<p>20.186.113.8 | <!--AZ-W-1-->50.112.160.58<p>54.213.195.223<p>35.163.170.185 |
| Uitgaand | <!--US-A1-->20.186.58.163<p>20.186.27.68<p>20.186.113.8 | <!--AZ-W-1-->104.45.78.98<p>51.105.168.218<p>51.105.163.143 |
