---
seo-title: Tipi di evento e descrizioni
title: Tipi di evento e descrizioni
uuid: bc 4 f 75 a 7-ea 22-47 eb-a 50 d -5 f 41274 c 41 d 6
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Event types and descriptions{#event-types-and-descriptions}

## Sessionstart

Sent with the `sessions` call. Quando la risposta viene restituita, estraete l'ID sessione dall'intestazione Posizione e lo utilizzate per le chiamate successive all'evento al server di raccolta.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). Gli altri stati da cui il lettore si sposta in "playing" includono "buffering", l'utente ripreso da "paused", il lettore recuperato da un errore, la riproduzione automatica e così via.

## ping

* **Contenuto principale -** Deve essere inviato ogni 10 secondi durante la riproduzione del contenuto principale, a prescindere da altri eventi API che sono stati inviati. Il primo evento di ping dovrebbe attivarsi 10 secondi dopo l'inizializzazione della riproduzione del contenuto principale.
* **Contenuto annuncio:** deve essere inviato ogni 1 secondi durante il tracciamento degli annunci.

Ping events should *not* include the `params` map in the request body.

## Bitratechange

Inviato quando cambia il bitanger.

## Bufferstart

Inviato al momento dell'avvio del buffering. There is no `bufferResume` event type. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## Pausestart

Inviato quando l'utente preme Pausa. There is no `resume` event type. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## Adbreakstart

Indica l'inizio di un'interruzione di annuncio

## Adstart

Indica l'inizio di un annuncio

## Adcomplete

Segnala il completamento di un'interruzione di annuncio

## Adskip

Segnala un annuncio ad hoc

## Adbreakcomplete

Segnala il completamento di un'interruzione di annuncio

## Chapterstart

Indica l'inizio di un segmento di capitolo

## Chapterskip

Segnala un salto di capitolo

## Chaptercomplete

Segnala la compilazione di un capitolo

## error

Segnala che si è verificato un errore.

## Sessionend

Questo viene usato per notificare al back-backend Media Analytics la chiusura immediata della sessione quando l'utente ha abbandonato la visualizzazione del contenuto e non lo restituisce.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## Sessioncomplete

Inviato al raggiungimento della fine del contenuto principale

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

