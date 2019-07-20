---
seo-title: Impostazione del tipo di richiesta HTTP nel lettore
title: Impostazione del tipo di richiesta HTTP nel lettore
uuid: b 8 fa 7233-e 654-4 acf-a 9 d 7-14158 cded 13 e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Setting the HTTP request type {#setting-the-http-request-type}

Il corpo della richiesta per tutte le richieste API di Media Collection deve essere in formato JSON, pertanto dovreste impostare il tipo di richiesta contenuto nel lettore. For example, in JavaScript you would set the `Content-Type` request header as follows:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

