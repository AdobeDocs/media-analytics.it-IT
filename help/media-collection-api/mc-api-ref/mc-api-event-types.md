---
title: Tipi e descrizioni di eventi multimediali in streaming
description: '"Quali sono i tipi di evento e le descrizioni di Media Collection? "'
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# Tipi di eventi e descrizioni{#event-types-and-descriptions}

## sessionStart

Inviato con la chiamata `sessions` . Quando la risposta restituisce , estrai l’ID sessione dall’intestazione Posizione e lo utilizzi per le chiamate successive all’evento al server di raccolta.

## play

Inviato quando il lettore cambia lo stato in &quot;riproduzione&quot; da un altro stato (ovvero, il callback `on('Playing')` viene attivato dal lettore). Altri stati da cui il giocatore si sposta a &quot;giocare&quot; includono &quot;buffering&quot;, l&#39;utente riprende da &quot;messo in pausa&quot;, il giocatore recuperato da un errore, autoplay, e così via.

## ping

* **Contenuto principale :** deve essere inviato ogni 10 secondi durante la riproduzione del contenuto principale, indipendentemente dagli altri eventi API inviati. Il primo evento ping deve attivarsi 10 secondi dopo l’avvio della riproduzione del contenuto principale.
* **Contenuto annuncio:** deve essere inviato ogni 1 secondo durante il tracciamento degli annunci.

Gli eventi ping devono *non* includere la mappa `params` nel corpo della richiesta.

## bitrateChange

Inviato quando cambia l&#39;amarezza.

## bufferStart

Inviato all’avvio del buffering. Nessun tipo di evento `bufferResume`. Un `bufferResume` viene dedotto quando si invia un evento `play` dopo `bufferStart`.

## pauseStart

Inviato quando l&#39;utente preme Pause. Nessun tipo di evento `resume`. Un `resume` viene dedotto quando si invia un evento `play` dopo un `pauseStart`.

## adBreakStart

Segnala l&#39;inizio di un&#39;interruzione pubblicitaria

## adStart

Segnala l&#39;inizio di un annuncio

## adComplete

Segnala il completamento di un&#39;interruzione pubblicitaria

## adSkip

Segnala un salto annuncio

## adBreakComplete

Segnala il completamento di un&#39;interruzione pubblicitaria

## capitoloStart

Segnala l’inizio di un segmento di capitolo

## capitoloSkip

Segnala un salto di capitolo

## capitoloComplete

Segnala il completamento di un capitolo

## error

Segnala un errore.

## sessionEnd

Viene utilizzato per notificare al backend di Media Analytics la chiusura immediata della sessione quando l’utente ha abbandonato la visualizzazione del contenuto ed è improbabile che ritorni.

Se non si invia un `sessionEnd`, una sessione abbandonata si interrompe normalmente (dopo che non vengono ricevuti eventi per 10 minuti o quando non si verifica alcun movimento dell&#39;indicatore di riproduzione per 30 minuti) e la sessione viene eliminata dal backend.

## sessionComplete

Inviato quando viene raggiunta la fine del contenuto principale

>[!IMPORTANT]
>
>Per verificare i tipi e i requisiti corretti dei parametri evento, fai riferimento agli schemi di convalida [JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) per ciascun tipo di evento.
