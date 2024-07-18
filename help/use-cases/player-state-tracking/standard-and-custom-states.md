---
title: Stati standard e personalizzati
description: Scopri la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida per l’implementazione e la generazione rapporti per gli stati del lettore standard e personalizzati.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: cdc5ea361829c749dfbb457288ac5ba51a530961
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 99%

---

# Stati standard e personalizzati

Sono disponibili cinque stati del lettore standard e puoi aggiungere stati personalizzati.

| Nome dello stato standard | Costante Media SDK | Nome dell’API di raccolta multimediale |
|-----------------------|------------------------------------------|-----------------------------|
| A schermo intero | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sottotitoli | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Disattiva audio | `ADB.Media.PlayerState.Mute` | `mute` |
| Immagine nell’immagine | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| In focus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

I dati vengono calcolati nello stesso modo per gli stati standard e personalizzati, ma vengono memorizzati in modo diverso per i rapporti di Analytics.

**Per gli stati standard**: quando abiliti il tracciamento dello stato del lettore dalla console Media Management nella generazione rapporti di Analytics (lato amministratore), sono disponibili 15 variabili di soluzione per i rapporti e le esportazioni di dati.

**Per gli stati personalizzati**: puoi creare regole di elaborazione personalizzate per memorizzare i valori calcolati in eventi personalizzati e quindi utilizzarle per i rapporti e le esportazioni di dati.

## Linee guida

* Una sessione video è limitata a 10 stati del lettore.
* È consentita qualsiasi combinazione di stati.
* Se passano gli stati di più lettori, solo i primi 10 vengono conservati e inoltrati a valle al componente di elaborazione VA.
* Il massimo di 10 stati è applicato a tutti gli stati, indipendentemente dalla loro chiusura o meno.
* Uno stato può iniziare e terminare più volte e viene conteggiato come un singolo stato. Ad esempio: `closedCapationing` può essere avviato e arrestato cinque volte, ma verrà conteggiato come un singolo stato.
* Ogni stato che supera il massimo di 10 stati consentiti viene eliminato.

## Stati personalizzati

Con la possibilità di creare stati personalizzati, è possibile acquisire azioni personalizzate e aggiornare metadati personalizzati durante una sessione di riproduzione.

Per informazioni sulla creazione di stati personalizzati, consulta la sezione [Guida di riferimento dell’API multimediale: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)
