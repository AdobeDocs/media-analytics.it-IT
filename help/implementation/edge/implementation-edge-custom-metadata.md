---
title: Supporto per metadati personalizzati - Formato XDM
description: Scopri come inviare metadati personalizzati con gli eventi di tracciamento dei contenuti multimediali utilizzando il formato Experience Edge XDM.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 80caffab1630b138724b310e3bdcc58f682a2f8b
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---


# Supporto per metadati personalizzati: formato XDM

L&#39;API di Experience Edge consente di inviare metadati personalizzati per contenuti multimediali insieme ai campi XDM standard negli eventi API `sessionStart`, `adStart` e `chapterStart`. I metadati personalizzati dei contenuti multimediali inviati tramite il formato XDM possono essere inoltrati sia ad **Adobe Analytics** che a **Adobe Experience Platform**.

Per le implementazioni API di Media Collection, vedere [Supporto metadati personalizzati](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md).

## Panoramica

I metadati personalizzati dei contenuti multimediali possono essere inviati in due posizioni all’interno di una richiesta Experience Edge, ciascuna con un comportamento di indirizzamento diverso:

| Posizione | Inviato ad Adobe Analytics | Inviato a Adobe Experience Platform | Caso d&#39;uso |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅ Sì | ✅ Sì | Dati aziendali necessari in entrambi i sistemi |
| `_data` | ✅ Sì | ❌ No | Flag specifici di Analytics o hint di elaborazione |

I metadati personalizzati si applicano a tre tipi di eventi:

| Evento | I metadati si applicano a |
|-------|-------------------|
| `sessionStart` | Contenuto principale (intera sessione) |
| `adStart` | Pubblicità individuale |
| `chapterStart` | Capitolo o segmento di contenuto |

## Struttura

### `xdm.mediaCollection.customMetadata` (Analytics + AEP)

I metadati personalizzati sono un **array di oggetti nome-valore** all&#39;interno dell&#39;oggetto `mediaCollection`:

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

<InlineAlert variant="warning" slots="text" />

`customMetadata` deve essere un **array** all&#39;interno di `mediaCollection`, non al livello principale `xdm`.

**Errato:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**Corretto:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data` (solo Analytics)

L&#39;oggetto `_data` è un costrutto speciale di Experience Edge che invia dati esclusivamente ad Adobe Analytics, ignorando i set di dati di AEP. I metadati personalizzati devono essere inseriti in `__adobe.analytics.contextData`.

A differenza di `xdm.mediaCollection.customMetadata` che utilizza un **array di oggetti nome-valore**, il mapping `_data` utilizza un **oggetto chiave-valore** flat direttamente in `contextData`:

| Approccio | Struttura | Destinazione |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | Array di `{"name": "...", "value": "..."}` oggetti | Analytics + AEP |
| `_data.__adobe.analytics.contextData` | Oggetto chiave-valore flat `{"key": "value"}` | Solo Analytics |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### Convenzioni di denominazione

- **Formato XDM:** prefisso con spazio dei nomi tenant che utilizza un carattere di sottolineatura. È inoltre possibile creare strutture nel gruppo di campi personalizzato del tenant, ad esempio `_<tenant>.<struct_name>.<field_name>`.
- Formato **`_data`:** campi sono posizionati in `_data.__adobe.analytics.contextData` — non è richiesto alcun prefisso di sottolineatura nel nome del campo (ad esempio, `debugFlag`)

## Metadati personalizzati del contenuto principale

Inviato con `sessionStart`. Si applica al supporto principale tracciato e rimane disponibile durante le chiamate di annunci e capitoli. Eventuali metadati personalizzati definiti qui verranno uniti automaticamente dal backend multimediale nelle corrispondenti chiamate di chiusura. Sarà incluso insieme a tutti i metadati personalizzati specifici definiti per annunci e capitoli.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Richiesta

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## Aggiungere metadati personalizzati

Inviato con `adStart`. Specifico per ogni singolo annuncio pubblicitario. I metadati personalizzati da `sessionStart` vengono inoltre uniti automaticamente dal backend multimediale nella chiamata di chiusura dell&#39;annuncio insieme a eventuali metadati personalizzati specifici dell&#39;annuncio qui definiti.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Richiesta

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## Metadati personalizzati del capitolo

Inviato con `chapterStart`. Specifico per ogni capitolo o segmento di contenuto. I metadati personalizzati di `sessionStart` vengono inoltre uniti automaticamente dal backend multimediale nella chiamata di chiusura del capitolo insieme ai metadati personalizzati specifici del capitolo qui definiti.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Richiesta

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## Utilizzo dell&#39;oggetto `_data` (metadati solo Analytics)

Utilizza l&#39;oggetto `_data` quando hai bisogno di metadati in Adobe Analytics che devono **non** essere memorizzati nei set di dati di AEP, ad esempio flag temporanei, variabili di debug o hint di elaborazione specifici per Analytics.

<InlineAlert variant="warning" slots="text" />

I dati inviati tramite `_data` non sono memorizzati in Adobe Experience Platform e non sono disponibili per Real-Time CDP, Journey Orchestration o altri servizi AEP.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Richiesta

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

In questo esempio:

- `_mycompany.league` → inviati ad Analytics e AEP
- `debugMode` e `testFlag` (in `_data.__adobe.analytics.contextData`) → inviati solo ad Analytics


## Posizione dei dati a valle

<InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata` è il **percorso API in entrata** utilizzato per inviare metadati personalizzati con eventi. Dopo l&#39;elaborazione, i dati vengono inoltrati ad Adobe Analytics come variabili di dati di contesto e memorizzati in Adobe Experience Platform in `mediaReporting.customMetadata` e come campi appiattiti di livello superiore.

**Adobe Analytics:**

- Dopo l’elaborazione, i metadati personalizzati vengono inoltrati ad Adobe Analytics come variabili di dati di contesto. Il prefisso `_tenant` viene rimosso automaticamente, pertanto le regole di elaborazione fanno riferimento solo al percorso del campo dopo `_tenant` (ad esempio, `_mycompany.contentCategory` diventa `contentCategory`)
- I dati inviati tramite `_data` vengono inoltrati anche ad Adobe Analytics e sono disponibili tramite le regole di elaborazione
- Utilizza le regole di elaborazione per mappare le variabili di dati di contesto su eVar, prop o altre variabili di Analytics. Per informazioni dettagliate, consulta [Mappatura delle variabili di dati per Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping).

**Adobe Experience Platform:**

- I campi di metadati personalizzati devono essere definiti come campi personalizzati nello schema XDM (ad esempio, `_mycompany`) e possono essere memorizzati e interrogati in AEP come campi appiattiti

  ![Definizione di campo personalizzato nello schema XDM](assets/custom_metadata.png)
- Per la creazione di report e query, i metadati personalizzati sono disponibili in `mediaReporting.customMetadata` e anche come campi appiattiti di livello superiore. Utilizza quello più adatto al tuo caso d’uso.
- Accessibile per segmentazione, Journey Orchestration e attivazione Real-Time CDP

## Comportamento

- Tutti i valori dei metadati personalizzati devono essere **stringhe**. Converti numeri e booleani prima dell’invio.
- I metadati di `sessionStart` persistono per l&#39;intera sessione; gli aggiornamenti richiedono una nuova sessione
- Ogni evento `adStart` e `chapterStart` può contenere metadati personalizzati diversi
- Preferisci i campi XDM standard (`sessionDetails`, `advertisingDetails`, `chapterDetails`) ai metadati personalizzati quando esiste un campo standard


## Documentazione correlata

- [Supporto per metadati personalizzati](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md). — API MC (formato JSON)
- [Tipo di dati Dettagli raccolta multimediale](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) — Riferimento schema XDM
- [Mappatura variabile dati per Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) — Mappatura dati contestuali di Analytics per campi XDM

<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->
