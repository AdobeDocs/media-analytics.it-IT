---
title: Panoramica delle variabili dei contenuti multimediali in streaming
description: Scopri come sono organizzate le variabili dei contenuti multimediali in streaming e come vengono mappate in Adobe Analytics e Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%
---

# Panoramica delle variabili dei contenuti multimediali in streaming

Le variabili sono dati forniti dal lettore multimediale su un flusso, ad esempio il nome del contenuto, il tipo di flusso, il nome dell’annuncio e la qualità di riproduzione. La maggior parte delle variabili viene impostata all’inizio della sessione e portata alla chiusura della sessione dal backend del file multimediale, che le utilizza per popolare le dimensioni e le metriche utilizzate nel reporting. Ogni pagina di variabili illustra come impostare tale variabile in ogni metodo di implementazione supportato.

## Invio delle variabili ad Adobe

Una singola variabile porta lo stesso valore a ogni applicazione o servizio Adobe, ma il formato di tale valore dipende da dove la invii. Nella tabella seguente sono elencati ogni applicazione o servizio e il formato di variabile previsto. La tabella delle proprietà in ogni pagina delle variabili mostra il valore esatto da utilizzare in ogni formato.

| Formato dei dati | Descrizione |
| --- | --- |
| Variabile dati contestuali | Il formato inviato ad Adobe Analytics, denominato con il prefisso `a.media` (ad esempio `a.media.name`). |
| Campo raccolta XDM | Il formato inviato a Customer Journey Analytics, espresso come percorso di campo XDM (ad esempio `xdm.mediaCollection.sessionDetails.name`). |
| caratteristica Audience Manager | Il formato inoltrato ad Audience Manager, con prefisso `c_contextdata` (ad esempio `c_contextdata.a.media.name`). |

>[!MORELIKETHIS]
>
>* [Panoramica eventi](/help/implementation/events/overview.md): gli eventi del lettore che contengono variabili
>* [Panoramica delle dimensioni](/help/reporting/dimensions/overview.md): dimensioni di reporting popolate dalle variabili
>* [Panoramica delle metriche](/help/reporting/metrics/overview.md): le metriche di reporting compilate dalle variabili
