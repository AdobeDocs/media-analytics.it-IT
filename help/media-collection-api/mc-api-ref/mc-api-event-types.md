---
title: Tipi di eventi e descrizioni per contenuti multimediali in streaming
description: '"Quali sono i tipi di eventi Media Collection e le relative descrizioni? "'
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '353'
ht-degree: 100%

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

Se non invii un evento `sessionEnd`, la sessione abbandonata si interrompe normalmente (se non vengono ricevuti eventi per 10 minuti o se non si verifica alcun movimento dell’indicatore di riproduzione per 30 minuti) e viene eliminata dal backend.

## sessionComplete

Inviato quando viene raggiunta la fine del contenuto principale

>[!IMPORTANT]
>
>Fai riferimento agli [schemi di convalida JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) per ogni tipo di evento, per verificare i tipi e i requisiti corretti dei parametri dell’evento.
