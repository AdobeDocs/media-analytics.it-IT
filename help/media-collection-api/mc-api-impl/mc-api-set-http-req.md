---
seo-title: Impostazione del tipo di richiesta HTTP nel lettore
title: Impostazione del tipo di richiesta HTTP nel lettore
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Impostazione del tipo di richiesta HTTP {#setting-the-http-request-type}

Il corpo della richiesta per tutte le richieste API di Media Collection deve essere in formato JSON, pertanto devi impostare il tipo di richiesta di contenuto nel lettore. Ad esempio, in JavaScript l’intestazione della `Content-Type` richiesta viene impostata come segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

