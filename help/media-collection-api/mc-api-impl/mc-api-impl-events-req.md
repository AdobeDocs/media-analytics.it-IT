---
seo-title: Implementazione di una richiesta di eventi
title: Implementazione di una richiesta di eventi
uuid: 3 bfa 313 c-ff 74-4 e 2 e-bbde -6 f 4 a 6221 d 85 b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementing an events request{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Specificate il percorso e la marca temporale di riproduzione, il tipo di evento ed eventuali parametri facoltativi che desiderate includere nel corpo JSON della richiesta.

The JSON request body for the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the Sessions request, however check the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for parameter requirements and types.
