---
title: Informazioni sugli stati standard e personalizzati
description: Scopri la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida per l’implementazione e la generazione di rapporti per gli stati del lettore standard e personalizzati.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Informazioni sugli stati standard e personalizzati

Sono disponibili cinque stati del lettore standard e puoi aggiungere i tuoi stati personalizzati.

| Nome dello stato standard | Costante Media SDK | Nome API di Media Collection |
|-----------------------|------------------------------------------|-----------------------------|
| A schermo intero | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sottotitoli | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Disattiva | `ADB.Media.PlayerState.Mute` | `mute` |
| Immagine nell&#39;immagine | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| In focus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

I dati vengono calcolati nello stesso modo per gli stati standard e personalizzati, ma i dati vengono memorizzati in modo diverso per i rapporti di Analytics.

**Per gli stati** standard - Quando abiliti il tracciamento dello stato del lettore dalla console Gestione Media nel reporting di Analytics (lato amministratore), sono disponibili 15 variabili di soluzione per il reporting e l’esportazione di dati.

**Per gli stati** personalizzati: puoi creare regole di elaborazione personalizzate per memorizzare i valori calcolati in eventi personalizzati e quindi utilizzare tali regole per i rapporti e le esportazioni di dati.

## Linee guida

* Una sessione video è limitata a 10 stati del lettore.
* È consentita qualsiasi combinazione di stati.
* Se gli stati di più lettori passano, solo i primi 10 vengono conservati e inoltrati a valle al componente di elaborazione VA.
* Il massimo di 10 Stati è applicato a tutti gli Stati, indipendentemente dalla loro chiusura o meno.
* Uno stato può iniziare e terminare più volte e viene conteggiato come un singolo stato. Ad esempio, `closedCapationing` può essere avviato e arrestato cinque volte, ma verrà conteggiato come un singolo stato.
* Ogni stato che supera il massimo di 10 stati consentiti viene eliminato.

## Stati personalizzati

Con la possibilità di creare stati personalizzati, è possibile acquisire azioni personalizzate e aggiornare metadati personalizzati durante una sessione di riproduzione.

Per informazioni sulla creazione di stati personalizzati, consulta la [Guida di riferimento API di Media: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
