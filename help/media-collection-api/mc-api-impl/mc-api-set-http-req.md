---
title: Impostazione del tipo di richiesta HTTP nel lettore
description: null
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Impostazione del tipo di richiesta HTTP {#setting-the-http-request-type}

Il corpo della richiesta per tutte le richieste API di Media Collection deve essere in formato JSON, pertanto devi impostare il tipo di richiesta di contenuto nel lettore. Ad esempio, in JavaScript l’intestazione della `Content-Type` richiesta viene impostata come segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

