---
title: Panoramica degli eventi multimediali in streaming
description: Scopri i tipi di evento multimediale e l’ordine in cui devono essere inviati.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# Eventi multimediali in streaming

Il tracciamento dei contenuti multimediali in streaming funziona inviando una sequenza di chiamate evento a un endpoint di raccolta dati di Adobe, ciascuna delle quali rappresenta una transizione nello stato del lettore. Ogni evento appartiene a una sessione attiva aperta da una chiamata [Session start](session/session-start.md). Le sessioni si chiudono automaticamente fino alla scadenza o possono essere chiuse immediatamente con una chiamata [Session end](session/session-end.md).

Gli eventi sono raggruppati in sei categorie (sessione, riproduzione, annunci, capitoli, stato del lettore e qualità), ciascuna delle quali copre un aspetto distinto dell’esperienza multimediale.

## Eventi sessione

Gli eventi di sessione si applicano a qualsiasi tipo di tracciamento dei contenuti multimediali, tra cui: video on-demand, flussi live, podcast e audiolibri. Essi definiscono i limiti della sessione di tracciamento stessa. L&#39;evento di sessione più importante è [Inizio sessione](session/session-start.md), in quanto quasi ogni altro tipo di evento dipende dall&#39;ID sessione generato. Invialo come primo evento quando un utente avvia una sessione, ad esempio quando preme play o quando il lettore inizia la riproduzione automatica.

Una volta aperta una sessione, utilizza [Sessione completata](session/session-complete.md) o [Fine sessione](session/session-end.md) per indicare la fine dell&#39;esperienza di visualizzazione. Invia la sessione completa quando il visualizzatore raggiunge la fine naturale del contenuto (il video termina, l’episodio del podcast termina o il capitolo finale di un audiolibro termina). La sessione completa non chiude la sessione; rimane aperta fino alla scadenza naturale, quindi tutti gli eventi finali come un ping finale vengono comunque acquisiti.

Se il visualizzatore esce prima di raggiungere la fine, invia [Fine sessione](session/session-end.md) per chiudere immediatamente la sessione. Invia la fine della sessione solo quando non seguiranno altri eventi (ad esempio, quando il lettore viene distrutto o la pagina viene scaricata). La fine della sessione è una chiusura difficile: una volta inviata, la sessione viene terminata e non è possibile tracciare ulteriori eventi al suo interno. Nella maggior parte dei casi, è più sicuro consentire la scadenza naturale della sessione. Alcuni esempi includono il visualizzatore che si mette in pausa a tempo indefinito, l’app che passa in background o il mancato caricamento del contenuto.

Una sessione scade automaticamente se non vengono ricevuti eventi per 10 minuti o se non viene rilevato alcun movimento della testina di riproduzione per 30 minuti. Se una delle condizioni è soddisfatta e il visualizzatore ritorna al contenuto, devi chiamare di nuovo Avvia sessione per aprire una nuova sessione prima di inviare qualsiasi altro evento.

## Eventi di riproduzione

Gli eventi di riproduzione tengono traccia delle transizioni di stato nel lettore multimediale durante una sessione. Costituiscono il nucleo del flusso di eventi e si applicano a qualsiasi tipo di contenuto.

L&#39;evento di riproduzione primario è [Riproduci](playback/play.md). Dopo aver chiamato l&#39;avvio della sessione, la riproduzione segnala che il contenuto è stato avviato, sia che si tratti dell&#39;avvio iniziale, di un trigger di riproduzione automatica o di un eventuale ritorno allo stato di riproduzione. [Pausa avvio](playback/pause-start.md) segnala che l&#39;utente ha sospeso la riproduzione. Non esiste un evento di ripresa dedicato; quando il visualizzatore riprende, invia di nuovo Play. La riproduzione funziona allo stesso modo dopo un arresto del buffering; invia [l&#39;avvio del buffer](playback/buffer-start.md) quando il lettore si blocca in attesa dei dati, quindi segui con Play quando il buffering si risolve.

Invia [ping](playback/ping.md) ogni 10 secondi durante la riproduzione del contenuto principale e ogni 1 secondo durante la riproduzione dell&#39;annuncio. Ping mantiene viva la sessione e registra il movimento della testina di riproduzione. Sugli SDK per dispositivi mobili, i ping vengono inviati automaticamente; su tutte le altre piattaforme devono essere inviati manualmente.

Invia [Modifica bitrate](playback/bitrate-change.md) ogni volta che l&#39;algoritmo del bitrate adattivo del lettore passa a un livello di qualità diverso. L’inclusione del nuovo valore bitrate nei dati QoE consente il reporting del bitrate medio.

## Eventi annuncio

Gli eventi annuncio tengono traccia degli annunci pubblicitari all’interno di una sessione multimediale. Gli scenari comuni includono annunci pre-roll prima dell’inizio di un video, annunci mid-roll inseriti a intervalli durante un video in formato lungo o un flusso live e annunci post-roll dopo la fine del contenuto. Una singola interruzione pubblicitaria può contenere uno o più annunci singoli.

Ogni interruzione pubblicitaria segue la stessa struttura. [Inizio interruzione annuncio](ads/ad-break-start.md) apre l&#39;interruzione e [Interruzione annuncio completata](ads/ad-break-complete.md) la chiude. Questi due eventi fungono da bookend che racchiudono tutti i singoli eventi pubblicitari. Durante l&#39;interruzione, invia [Inizio annuncio](ads/ad-start.md) quando inizia la riproduzione di ogni singolo annuncio. Seguilo con [Annuncio completato](ads/ad-complete.md) se l&#39;annuncio viene riprodotto per l&#39;intera durata oppure [Annuncio ignorato](ads/ad-skip.md) se il visualizzatore seleziona il pulsante Ignora. Se si omette uno dei bookend, tutti gli eventi pubblicitari nell’interruzione vengono ignorati e la durata dell’annuncio viene erroneamente attribuita al contenuto principale.

L’esempio seguente mostra la sequenza di eventi corretta per una singola interruzione pubblicitaria contenente tre annunci, in cui il visualizzatore ha saltato il terzo:

1. Avvio dell’interruzione pubblicitaria
2. Inizio annuncio
3. Annuncio completato
4. Inizio annuncio
5. Annuncio completato
6. Inizio annuncio
7. Salta annuncio
8. Interruzione annuncio completata

## Eventi capitolo

Gli eventi dei capitoli sono facoltativi e tengono traccia dei segmenti di contenuto denominati all’interno di una sessione. Sono adatti a contenuti naturalmente divisi in parti distinte. Esempi comuni includono capitoli in un audiolibro, atti in un documentario, lezioni in un corso video o segmenti in un episodio di podcast. Utilizza gli eventi dei capitoli quando desideri comprendere il coinvolgimento degli utenti a livello di segmento, ad esempio per identificare quali capitoli i tipi di pubblico tendono a saltare.

Invia [Inizio capitolo](chapters/chapter-start.md) quando inizia un capitolo. Se il visualizzatore guarda fino alla fine del capitolo, invia [Capitolo completato](chapters/chapter-complete.md). Se il visualizzatore cerca oltre il limite del capitolo senza guardarlo fino al completamento, invia invece [Salta capitolo](chapters/chapter-skip.md). Per poter aprire un nuovo capitolo, è necessario chiuderlo con Capitolo completato o Salta capitolo. I capitoli non possono sovrapporsi.

## Eventi di stato del lettore

Gli eventi di stato del lettore tengono traccia di come i visualizzatori interagiscono con i controlli del lettore durante una sessione. Sono utili per comprendere l’utilizzo delle funzioni di accessibilità, ad esempio la frequenza con cui i visualizzatori abilitano i sottotitoli o la disattivazione dell’audio. Rivelano inoltre pattern di visualizzazione come la visualizzazione a schermo intero o in linea e il multitasking &quot;picture-in-picture&quot;.

I cinque stati tracciabili sono: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` e `inFocus`. Invia [Inizio stato](player-state/state-start.md) quando il lettore immette uno di questi stati e [Fine stato](player-state/state-end.md) quando esce. Più stati possono essere attivi contemporaneamente; un visualizzatore può essere a schermo intero e disattivato simultaneamente e più stati possono essere terminati all&#39;interno della stessa chiamata evento.

## Eventi di errore

L&#39;evento [Error](error.md) registra un errore di riproduzione durante una sessione: una richiesta di flusso non riuscita, un errore di codec o un errore di consegna esterno. Invialo ogni volta che si verifica un errore significativo. Un evento di errore non chiude la sessione; la riproduzione può continuare e gli eventi successivi vengono tracciati nella stessa sessione. Se l’errore non è recuperabile, eseguilo insieme a Session end (Fine sessione) per chiudere esplicitamente la sessione.

>[!MORELIKETHIS]
>
>* [Panoramica delle variabili](/help/implementation/variables/overview.md): dati trasferiti dagli eventi ad Adobe
>* [Panoramica delle dimensioni](/help/reporting/dimensions/overview.md): dimensioni di reporting compilate dagli eventi
>* [Panoramica delle metriche](/help/reporting/metrics/overview.md): le metriche di reporting compilate dagli eventi
