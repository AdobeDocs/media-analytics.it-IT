---
seo-title: Implementazione di una richiesta di eventi
title: Implementazione di una richiesta di eventi
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementazione di una richiesta di eventi{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilizzate la richiesta [](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) Eventi per tutte le chiamate di tracciamento successive dopo aver ottenuto un ID sessione utilizzando la richiesta [Sessioni.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Specificate la posizione dell'indicatore di riproduzione e la marca temporale, il tipo di evento ed eventuali parametri facoltativi da includere nel corpo JSON della richiesta.

Il corpo della richiesta JSON per la richiesta [](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) Eventi ha la stessa struttura della richiesta Sessions, tuttavia controllate gli schemi [di convalida](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) JSON per i requisiti e i tipi di parametro.
