---
title: Impostazione del tipo di richiesta HTTP nel lettore
description: 'Il corpo della richiesta per tutte le richieste API Streaming Media Collection deve essere in formato JSON. Scopri come impostare il tipo di richiesta del contenuto nel lettore. '
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 12%

---

# Impostazione del tipo di richiesta HTTP {#setting-the-http-request-type}

Il corpo della richiesta per tutte le richieste API di Media Collection deve essere in formato JSON, quindi devi impostare il tipo di richiesta del contenuto nel lettore. Ad esempio, in JavaScript l’intestazione di richiesta `Content-Type` viene impostata come segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
