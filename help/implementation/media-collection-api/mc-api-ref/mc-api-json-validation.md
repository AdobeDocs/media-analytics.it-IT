---
title: Schemi di convalida JSON di Streaming Media Analytics
description: Quali sono gli schemi di convalida JSON per i contenuti multimediali dinamici e come vengono utilizzati per determinare i parametri corretti del corpo della richiesta per ciascun tipo di evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '82'
ht-degree: 100%

---

# Schemi di convalida JSON {#json-validation-schemas}

Il backend di Media Analytics convalida i parametri di richiesta per ciascun tipo di evento utilizzando gli schemi di convalida JSON. Questi schemi sono disponibili e fungono da autorità corrente per i tipi di parametri utilizzati nell’API MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Per ulteriori informazioni sull’utilizzo degli schemi di convalida JSON, consulta [Convalida delle richieste evento.](../mc-api-impl/mc-api-validate-reqs.md)
