---
title: Versione app
description: Segnala la versione dell’applicazione del lettore multimediale utilizzata per ogni sessione di streaming.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%
---

# Versione app

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Versione app**. Per informazioni su come raccogliere questa variabile, vedere [Versione app](/help/implementation/variables/core/app-version.md).*

>[!ENDSHADEBOX]

La dimensione **Versione app** riporta la stringa di versione dell&#39;applicazione del lettore multimediale configurata all&#39;inizializzazione di SDK. Utilizzalo per identificare quali versioni del lettore sono in uso attivo, correlare cambiamenti di qualità o comportamentali con versioni specifiche e dare priorità al supporto per le versioni ampiamente utilizzate.

>[!NOTE]
>
>Questa dimensione acquisisce la versione dell&#39;**applicazione lettore multimediale**, non la libreria SDK di Adobe. La versione della libreria SDK di Adobe viene raccolta automaticamente come campo interno separato.

## Compilazione di questa dimensione

La versione dell’app viene impostata una volta al momento dell’inizializzazione del SDK e viene inclusa automaticamente in ogni richiesta di avvio di sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica tramite mappatura campo XDM quando si utilizzano le implementazioni di Edge. Per le implementazioni solo Analytics, mappare i dati contestuali `media.sdkVersion` a un eVar personalizzato utilizzando una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | Nessuna colonna di feed dati dedicata. Per le implementazioni basate solo su Analytics, utilizza la colonna feed dati dell’eVar personalizzato configurato tramite la regola di elaborazione. |
| Audience Manager | `c_contextdata.media.sdkVersion` (implementazioni solo Analytics) |

## Elementi dimensionali

Ogni elemento rappresenta la stringa di versione letterale configurata all&#39;inizializzazione di SDK. Utilizza uno schema di versioni coerente nelle tue implementazioni in modo che le stringhe di versione si accumulino in modo prevedibile nei rapporti.
