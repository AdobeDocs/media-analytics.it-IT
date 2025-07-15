---
title: 'Implementazione di una richiesta di eventi '
description: Scopri come utilizzare l’endpoint Richiesta eventi per tutte le chiamate di tracciamento successive dopo aver ottenuto un ID sessione
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Implementazione di una richiesta di eventi {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilizza la [Richiesta eventi](../mc-api-ref/mc-api-events-req.md) per tutte le chiamate di tracciamento successive dopo aver ottenuto un ID sessione utilizzando la [Richiesta sessioni.](../mc-api-ref/mc-api-sessions-req.md) Specifica la posizione dell’indicatore di riproduzione e la marca temporale, il tipo di evento ed eventuali altri parametri facoltativi da includere nel corpo della richiesta JSON.

Il corpo della richiesta JSON per la [Richiesta eventi](../mc-api-ref/mc-api-events-req.md) ha la stessa struttura della Richiesta sessioni, tuttavia verifica gli [schemi di convalida JSON](../mc-api-ref/mc-api-json-validation.md) per conoscere i requisiti e i tipi di parametri.
