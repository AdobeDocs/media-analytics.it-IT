---
title: Informazioni sugli stati standard e personalizzati
description: In questo argomento viene descritta la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida per l’implementazione e la generazione di rapporti degli stati di riproduzione standard e personalizzati.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '251'
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

* Una sessione video è limitata a 10 stati di lettore personalizzati univoci.
* Se gli stati di più lettori passano, solo i primi 10 vengono conservati e inoltrati a valle del componente di elaborazione VA(?video analytics).
* Il massimo di 10 stati viene applicato a tutti gli stati, indipendentemente dal fatto che siano o meno chiusi.
* Lo stesso stato può essere avviato e terminato un numero qualsiasi di volte e viene conteggiato come un singolo stato.
* Ogni stato che supera il massimo consentito personalizzato? gli stati (10) vengono scartati.

## Stati personalizzati

Grazie alla possibilità di creare stati personalizzati, potete acquisire azioni personalizzate e aggiornare metadati personalizzati durante una sessione di riproduzione.

NECESSITÀ di ulteriori informazioni sugli stati personalizzati
