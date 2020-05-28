---
title: Informazioni sugli stati standard e personalizzati
description: In questo argomento viene descritta la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida per l’implementazione e la generazione di rapporti degli stati di riproduzione standard e personalizzati.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# Informazioni sugli stati standard e personalizzati

Sono disponibili cinque stati di lettore standard e potete aggiungere stati personalizzati.

| Nome stato standard | Costante Media SDK | Nome API di Media Collection |
|-----------------------|------------------------------------------|-----------------------------|
| Schermo intero | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sottotitoli codificati | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Disattiva | `ADB.Media.PlayerState.Mute` | `mute` |
| Picture in Picture | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| A fuoco | `ADB.Media.PlayerState.InFocus` | `inFocus` |

I dati vengono calcolati nello stesso modo per gli stati standard e personalizzati, ma i dati vengono memorizzati in modo diverso per i report di Analytics.

**Per gli stati** standard - Quando abilitate il tracciamento dello stato del lettore dalla console di gestione multimediale nel reporting di Analytics (lato amministratore), sono disponibili 15 variabili di soluzione per il reporting e l&#39;esportazione di dati.

**Per gli stati** personalizzati: potete creare regole di elaborazione personalizzate per memorizzare i valori calcolati in eventi personalizzati e quindi utilizzare tali regole per reporting ed esportazioni di dati.

## Linee guida

* Una sessione video è limitata a 10 stati di lettore.
* È consentita qualsiasi combinazione di stati.
* Se gli stati di più lettori passano, solo i primi 10 vengono conservati e inoltrati a valle del componente di elaborazione VA.
* Il massimo di 10 stati viene applicato a tutti gli stati, indipendentemente dal fatto che siano o meno chiusi.
* Uno stato può iniziare e terminare più volte e viene conteggiato come un singolo stato. Ad esempio, `closedCapationing` può essere avviato e arrestato cinque volte, ma verrà conteggiato come un singolo stato.
* Ogni stato che supera il massimo di 10 stati consentiti viene eliminato.

## Stati personalizzati

Grazie alla possibilità di creare stati personalizzati, potete acquisire azioni personalizzate e aggiornare metadati personalizzati durante una sessione di riproduzione.

Per informazioni sulla creazione di stati personalizzati, consultate Guida di riferimento alle API [multimediali: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
