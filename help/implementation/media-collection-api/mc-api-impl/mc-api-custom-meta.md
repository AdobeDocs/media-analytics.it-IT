---
title: Supporto per metadati personalizzati
description: Scopri come fornire coppie chiave:valore personalizzate negli eventi sessionStart, chapterStart e adStart.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# Supporto per metadati personalizzati{#custom-metadata-support}

L&#39;API Media Collection consente di inviare coppie chiave-valore personalizzate insieme ai parametri standard negli eventi `sessionStart`, `adStart` e `chapterStart`. I metadati personalizzati vengono inoltrati a **Adobe Analytics** con i rispettivi eventi di chiusura dei contenuti multimediali.

Per rendere questi dati disponibili in Analysis Workspace, i clienti devono definire eVar personalizzate e configurare le regole di elaborazione per compilarle in base al proprio caso d’uso. Una volta mappati a eVar o proprietà, i dati diventano disponibili in Adobe Experience Platform anche tramite i percorsi eVar corrispondenti, a condizione che il [connettore di origine Analytics](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/analytics) sia configurato.

Per le implementazioni basate su XDM che utilizzano Experience Edge, consulta [Supporto metadati personalizzati - Formato XDM](/help/implementation/edge/implementation-edge-custom-metadata.md).

## Panoramica

I metadati personalizzati sono inclusi nel corpo della richiesta come oggetto `customMetadata`, posizionato accanto alla chiave `params`. Si applica a tre tipi di evento:

| Evento | I metadati si applicano a |
|-------|-------------------|
| `sessionStart` | Contenuto principale (intera sessione) |
| `adStart` | Pubblicità individuale |
| `chapterStart` | Capitolo o segmento di contenuto |

## Struttura

I metadati personalizzati sono un **oggetto** (coppie chiave-valore) piatto a livello di evento, insieme alla chiave `params`:

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### Parametri obbligatori per tipo di evento

| Evento | Richiesto `params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### Requisiti principali per la denominazione

- Evita di usare il prefisso `media.` nelle chiavi di metadati personalizzate: viene mappato sui campi multimediali standard e potrebbe sovrascriverlo nei rapporti di Analytics
- Il prefisso `a.` è riservato per i metadati standard di Adobe e non deve essere utilizzato

## Metadati personalizzati del contenuto principale

Inviato con `sessionStart`. Si applica al supporto principale tracciato e rimane disponibile durante le chiamate di annunci e capitoli. Eventuali metadati personalizzati definiti qui verranno uniti automaticamente dal backend multimediale nelle corrispondenti chiamate di chiusura. Sarà incluso insieme a tutti i metadati personalizzati specifici definiti per annunci e capitoli.

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## Aggiungere metadati personalizzati

Inviato con `adStart`. Specifico per ogni singolo annuncio pubblicitario. I metadati personalizzati da `sessionStart` vengono inoltre uniti automaticamente dal backend multimediale nella chiamata di chiusura dell&#39;annuncio insieme a eventuali metadati personalizzati specifici dell&#39;annuncio qui definiti.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## Metadati personalizzati del capitolo

Inviato con `chapterStart`. Specifico per ogni capitolo o segmento di contenuto. I metadati personalizzati di `sessionStart` vengono inoltre uniti automaticamente dal backend multimediale nella chiamata di chiusura del capitolo insieme ai metadati personalizzati specifici del capitolo qui definiti.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## Comportamento

- Tutti i valori dei metadati personalizzati devono essere **stringhe**. Converti numeri e booleani prima dell’invio.
- I metadati personalizzati vengono visualizzati in Analytics con il prefisso `c.` (ad esempio, `contentCategory` → `c.contentCategory`)
- Mappa i metadati personalizzati su eVar, prop o variabili di dati di contesto tramite le regole di elaborazione di Analytics
- I metadati di `sessionStart` persistono per l&#39;intera sessione; gli aggiornamenti richiedono una nuova sessione
- Ogni evento `adStart` e `chapterStart` può contenere metadati personalizzati diversi

## Documentazione correlata

- [Supporto per metadati personalizzati - Formato XDM](/help/implementation/edge/implementation-edge-custom-metadata.md) — Invio di metadati personalizzati tramite Experience Edge ad Analytics e AEP
- [Connettore di origine di Adobe Analytics per i dati della suite di rapporti](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/analytics) — Importa dati di Analytics in Adobe Experience Platform

<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->
