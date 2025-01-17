---
title: Tipi di eventi e descrizioni per contenuti multimediali in streaming
description: 'Quali sono i tipi di evento Media Collection e le relative descrizioni? '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 98722998606af3761652e282c31338bb966eb654
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 79%

---

# Tipi di eventi e descrizioni {#event-types-and-descriptions}

## sessionStart

Inviato con la chiamata di `sessions`. Quando viene restituita la risposta, puoi estrarre l’ID sessione dall’intestazione Posizione e utilizzarlo per le successive chiamate evento al server di raccolta.

## play

Inviato quando il lettore passa allo stato “riproduzione” da un altro stato (ovvero quando il callback `on('Playing')` viene attivato dal lettore). Il lettore può passare alla modalità “riproduzione” da altri stati quali “buffering”, ripresa dopo “in pausa”, ripristino in seguito a un errore, riproduzione automatica e così via.

## ping

* **Contenuto principale -** Deve essere inviato ogni 10 secondi durante la riproduzione del contenuto principale, indipendentemente dagli altri eventi API inviati. Il primo evento ping deve attivarsi 10 secondi dopo l’avvio della riproduzione del contenuto principale.
* **Contenuto annuncio -** Deve essere inviato con una cadenza di 1 secondo durante il tracciamento degli annunci.

Gli eventi ping *non* devono includere la mappa `params` nel corpo della richiesta.

## bitrateChange

Inviato quando cambia il bitrate.

## bufferStart

Inviato all’avvio del buffering. Non esiste un tipo di evento `bufferResume`. L’evento `bufferResume` viene dedotto quando si invia un evento `play` dopo `bufferStart`.

## pauseStart

Inviato quando l’utente preme Pausa. Non esiste un tipo di evento `resume`. L’evento `resume` viene dedotto quando si invia un evento `play` dopo `pauseStart`.

## adBreakStart

Segnala l’inizio di un’interruzione pubblicitaria

## adStart

Segnala l’inizio di un annuncio

## adComplete

Segnala il completamento di un’interruzione pubblicitaria

## adSkip

Segnala il salto di un annuncio

## adBreakComplete

Segnala il completamento di un’interruzione pubblicitaria

## chapterStart

Segnala l’inizio di un segmento capitolo

## chapterSkip

Segnala il salto di un capitolo

## chapterComplete

Segnala il completamento di un capitolo

## error

Segnala un errore.

## sessionEnd

Viene utilizzato per notificare al backend di Media Analytics di chiudere immediatamente la sessione quando l’utente abbandona la visualizzazione del contenuto ed è improbabile che ritorni.

Se un `sessionEnd` non viene inviato, una sessione abbandonata [si interrompe normalmente](../mc-api-impl/mc-api-timeout.md) (se non vengono ricevuti eventi per 10 minuti o se non si verifica alcun movimento dell&#39;indicatore di riproduzione per 30 minuti). Inoltre, tutte le successive chiamate multimediali effettuate con tale ID sessione verranno eliminate.

## sessionComplete

Inviato quando viene raggiunta la fine del contenuto principale

>[!IMPORTANT]
>
>Fai riferimento agli [schemi di convalida JSON](mc-api-json-validation.md) per ogni tipo di evento, per verificare i tipi e i requisiti corretti dei parametri dell’evento.

## stateStart

Segnala l’inizio del tracciamento dello stato del lettore.

Per ulteriori informazioni, vedere [Implementazione e reporting](/help/use-cases/player-state-tracking/implementation-and-reporting.md).

## stateEnd

Segnala la fine del tracciamento dello stato del lettore.

Per ulteriori informazioni, vedere [Implementazione e reporting](/help/use-cases/player-state-tracking/implementation-and-reporting.md).
