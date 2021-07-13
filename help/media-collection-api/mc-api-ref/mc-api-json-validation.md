---
title: Streaming degli schemi di convalida JSON di Media Analytics
description: Cosa sono gli schemi di convalida JSON per contenuti multimediali dinamici e come vengono utilizzati per determinare i parametri corretti del corpo della richiesta per ciascun tipo di evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 2%

---

# Schemi di convalida JSON{#json-validation-schemas}

Il back-end di Media Analytics convalida i parametri di richiesta per ciascun tipo di evento utilizzando gli schemi di convalida JSON. Questi schemi sono disponibili e fungono da autorità corrente per i tipi di parametri utilizzati nell’API MA.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Per ulteriori informazioni sull&#39;utilizzo degli schemi di convalida JSON, vedere [Convalida delle richieste di eventi.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
