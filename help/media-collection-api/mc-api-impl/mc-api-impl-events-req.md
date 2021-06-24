---
title: Implementazione di una richiesta di eventi
description: Scopri come utilizzare l’endpoint della richiesta Eventi per tutte le chiamate di tracciamento successive dopo aver ottenuto un ID sessione
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 5%

---

# Implementazione di una richiesta di eventi{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilizza la [Richiesta eventi](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) per tutte le chiamate di tracciamento successive dopo aver ottenuto un ID sessione utilizzando la richiesta [Sessions.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Specifica la posizione dell’indicatore di riproduzione e la marca temporale, il tipo di evento e eventuali parametri facoltativi da includere nel corpo JSON della richiesta.

Il corpo della richiesta JSON per la [richiesta di eventi](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) ha la stessa struttura di quella della richiesta di sessioni, tuttavia controlla gli [schemi di convalida JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) per i requisiti e i tipi di parametri.
