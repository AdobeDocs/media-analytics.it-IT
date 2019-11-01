---
title: Tipi di evento e descrizioni
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Tipi di evento e descrizioni{#event-types-and-descriptions}

## sessionStart

Inviato con la `sessions` chiamata. Quando la risposta restituisce, l'ID sessione viene estratto dall'intestazione Posizione e utilizzato per le chiamate di eventi successive al server Raccolta.

## play

Inviato quando il lettore cambia stato in "play" da un altro stato (ad es., il `on('Playing')` callback viene attivato dal lettore). Altri stati da cui il lettore passa alla "riproduzione" includono "buffering", l'utente riprende dalla "pausa", il lettore recuperato da un errore, la riproduzione automatica e così via.

## ping

* **Contenuto principale -** Deve essere inviato ogni 10 secondi durante la riproduzione del contenuto principale, indipendentemente dagli altri eventi API inviati. Il primo evento di ping deve essere attivato 10 secondi dopo l’avvio della riproduzione del contenuto principale.
* **Contenuto annuncio -** Deve essere inviato ogni 1 secondo durante il tracciamento degli annunci.

Gli eventi ping *non* devono includere la `params` mappa nel corpo della richiesta.

## bitrateChange

Inviato quando l'immagine cambia.

## bufferStart

Inviato quando inizia il buffering. Non esiste un tipo di `bufferResume` evento. Un `bufferResume` dato viene ricavato quando si invia un `play` evento dopo `bufferStart`.

## pauseStart

Inviato quando l'utente preme Pausa. Non esiste un tipo di `resume` evento. Un `resume` dato viene ricavato quando si invia un `play` evento dopo un `pauseStart`.

## adBreakStart

Segnala l'inizio di un'interruzione annuncio

## adStart

Segnala l'inizio di un annuncio

## adComplete

Segnala il completamento di un annuncio

## adSkip

Segnala un salto annuncio

## adBreakComplete

Segnala il completamento di un annuncio

## ChapterStart

Segnala l’inizio di un segmento di capitolo

## ChapterSkip

Segnala un salto di capitolo

## ChapterComplete

Segnala il completamento di un capitolo

## error

Segnala un errore.

## sessionEnd

Questo viene utilizzato per notificare al backend di Media Analytics di chiudere immediatamente la sessione quando l’utente ha abbandonato la visualizzazione del contenuto e non è probabile che torni.

Se non si invia `sessionEnd`, una sessione abbandonata si interrompe normalmente (dopo che nessun evento viene ricevuto per 10 minuti, o quando non si verifica alcun movimento dell'indicatore di riproduzione per 30 minuti) e la sessione viene eliminata dal backend.

## sessionComplete

Inviato quando viene raggiunta la fine del contenuto principale

>[!IMPORTANT]
>
>Per verificare i tipi e i requisiti corretti dei parametri dell'evento, fare riferimento agli schemi [di convalida](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) JSON per ciascun tipo di evento.

