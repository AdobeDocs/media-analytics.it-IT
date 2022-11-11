---
title: Impostazione del tipo di richiesta HTTP nel lettore
description: Il corpo della richiesta per tutte le richieste API Streaming Media Collection deve essere in formato JSON. Scopri come impostare il tipo di richiesta del contenuto nel lettore.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '76'
ht-degree: 100%

---

# Impostazione del tipo di richiesta HTTP {#setting-the-http-request-type}

Il corpo della richiesta per tutte le richieste API di Media Collection deve essere in formato JSON, quindi devi impostare il tipo di richiesta del contenuto nel lettore. Ad esempio, in JavaScript è necessario impostare il `Content-Type` dell’intestazione della richiesta come segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
