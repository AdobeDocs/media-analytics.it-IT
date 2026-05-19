---
title: Impostazione del tipo di richiesta HTTP nel lettore
description: Il corpo della richiesta per tutte le richieste API di Media Collection deve essere in formato JSON. Scopri come impostare il tipo di richiesta del contenuto nel lettore.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Zrsv5Kjec6ZHzcOEcj5Ek0zXdwM8cF7HFalKs-MKGQU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 75
ht-degree: 81%

---

# Impostazione del tipo di richiesta HTTP {#setting-the-http-request-type}

Il corpo della richiesta per tutte le richieste API di Media Collection deve essere in formato JSON, quindi devi impostare il tipo di richiesta del contenuto nel lettore. Ad esempio, in JavaScript è necessario impostare il `Content-Type` dell’intestazione della richiesta come segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
