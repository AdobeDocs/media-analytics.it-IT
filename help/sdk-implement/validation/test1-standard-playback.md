---
title: Riproduzione standard Test 1
description: Questo argomento descrive il test di riproduzione standard utilizzato per la convalida.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Prova 1: Riproduzione standard{#test-standard-playback}

Questo test case convalida la riproduzione generale e la sequenza. È un elemento obbligatorio della richiesta di certificazione.

## Modulo di richiesta di certificazione

**Scarica il modulo di richiesta di certificazione qui: ==&gt;Modulo di richiesta** di [certificazione.](cert_req_form.docx)

## Panoramica del test di certificazione 1

Le implementazioni di Media Analytics includono due tipi di chiamate di tracciamento:
* Chiamate effettuate direttamente al server Adobe Analytics (AppMeasurement) - Queste chiamate si verificano negli eventi "Media Start" e "Ad Start".
* Chiamate al server Media Analytics (heartbeat), che includono chiamate in banda e fuori banda:
   * In-band - L’SDK invia chiamate di riproduzione temporizzate o "ping" a intervalli di 10 secondi durante la riproduzione del contenuto e a intervalli di un secondo durante gli annunci.
   * Out-of-band - Queste chiamate possono essere eseguite in qualsiasi momento, e includono Pausa, Buffering, errori, contenuto completo, annuncio completo, ecc.

>[!NOTE]
>Il tracciamento dei file multimediali si comporta allo stesso modo su tutte le piattaforme.

## Procedura di prova

Completa e registra le azioni seguenti (in ordine):

1. **Carica la pagina o l’app**

   **Server** di tracciamento (per tutti i siti Web e le app mobili):

   * **Server Adobe Analytics (AppMeasurement) - Per il servizio ID visitatore Experience Cloud è necessario un server o un CNAME di tracciamento RDC che si risolve in un server di tracciamento RDC.** Il server di tracciamento di Adobe Analytics deve terminare con "`.sc.omtrdc.net`" o essere un CNAME.

   * **Server di Media Analytics (Heartbeats) -** Questo server ha sempre il formato "`[namespace].hb.omtrdc.net`", dove `[namespace]` specifica il nome della società. Questo nome è fornito da Adobe.
   Devi convalidare determinate variabili chiave universali per tutte le chiamate di tracciamento:

   **`mid`ID visitatore Adobe (**): La `mid` variabile viene utilizzata per acquisire il valore impostato nel cookie AMCV. La `mid` variabile è il valore di identificazione principale sia per i siti Web che per le app mobili e indica inoltre che il servizio ID visitatori di Experience Cloud è configurato correttamente. È disponibile sia nelle chiamate Adobe Analytics (AppMeasurement) che Media Analytics (heartbeat).

   * **Chiamata di avvio di Adobe Analytics**

      | Parametro | Valore (campione) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata alla pagina del sito Web**

      | Parametro | Valore (campione) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Ciclo di vita**

      | Parametro | Valore (campione) |
      |---|---|
      | `pev2` | ADBINTERNO:Ciclo Di Vita |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata di avvio di Media Analytics**

      | Parametro | Valore (campione) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Nelle chiamate di avvio di Media Analytics (`s:event:type=start`) i `mid` valori potrebbero non essere presenti. Questo va bene. Potrebbero essere visualizzati solo dopo le chiamate alla riproduzione di Media Analytics ( `s:event:type=play`).

   * **Riproduzione di Media Analytics**

      | Parametro | Valore (campione) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Avviare il lettore multimediale**

   All’avvio del lettore multimediale, Media SDK invia le chiamate chiave ai due server nel seguente ordine:

   1. Server Adobe Analytics - Avvia chiamata
   1. Server di Media Analytics - Avvia chiamata
   1. Server di Media Analytics - "Richiesta chiamata di avvio di Adobe Analytics"
   Le prime due chiamate di cui sopra contengono metadati e variabili aggiuntive. Per i parametri delle chiamate e i metadati, consultate [Test dei dettagli delle chiamate.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La terza chiamata precedente indica al server Media Analytics che Media SDK ha richiesto l'invio della chiamata di avvio di Adobe Analytics (`pev2=ms_s`) al server Adobe Analytics.

1. **Visualizza annuncio se disponibile**

   * **Inizio annuncio**
   All’avvio dell’annuncio, le seguenti chiamate chiave vengono inviate nell’ordine seguente:

   1. Server Adobe Analytics - Chiamata Ad Start
   1. Server di Media Analytics - Chiamata Ad Start
   1. Server di Media Analytics - "Richiesta chiamata Adobe Analytics Ad Start"
   Le prime due chiamate contengono metadati e variabili aggiuntivi. Per i parametri delle chiamate e i metadati, consultate [Test dei dettagli delle chiamate.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   La terza chiamata indica al server Media Analytics che Media SDK ha richiesto l'invio della chiamata Adobe Analytics Ad Start (`pev2=msa_s`) al server Adobe Analytics.

   * **Aggiungi riproduzione**

      Durante la riproduzione di un annuncio, Media Analytics SDK invia al server Media Analytics eventi di riproduzione di tipo "ad" ogni secondo.

   * **Annuncio completato**

      Nel punto 100% di un annuncio, deve essere inviata una chiamata Completa di Media Analytics.



1. **Metti in pausa la riproduzione per 30 secondi, se disponibile.**  **Pausa annuncio**

   In Ad Pause, le chiamate heartbeat o "ping" di Media Analytics vengono inviate dall’SDK al server di Media Analytics ogni secondo.

   >[!NOTE]
   >
   >Il valore dell'indicatore di riproduzione deve rimanere costante durante la pausa.

   Per i parametri delle chiamate e i metadati, consultate [Test dei dettagli delle chiamate.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Riproduci il contenuto principale per 10 minuti senza interruzioni.**  Riproduzione **contenuto**

   Durante la riproduzione del contenuto principale, Media SDK invia heartbeat (chiamate Play) al server Media Analytics ogni 10 secondi.

   Note:

   * La posizione dell'indicatore di riproduzione dovrebbe aumentare di 10 con ogni chiamata Play.
   * Il `l:event:duration` valore rappresenta il numero di millisecondi trascorsi dall’ultima chiamata di tracciamento e deve corrispondere all’incirca allo stesso valore per ogni chiamata di 10 secondi.

      Per i parametri delle chiamate e i metadati, consultate [Test dei dettagli delle chiamate.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Sospendi durante la riproduzione per almeno 30 secondi.** Quando il lettore multimediale viene messo in pausa, le chiamate dell’evento pause vengono inviate dall’SDK al server di Media Analytics ogni 10 secondi. Al termine della pausa, gli eventi di riproduzione dovrebbero riprendere.

   Per i parametri delle chiamate e i metadati, consultate [Test dei dettagli delle chiamate.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Cercare/scorrere contenuti multimediali.** Durante il trascinamento dell'indicatore di riproduzione multimediale, non vengono inviate chiamate di tracciamento speciali, tuttavia, quando la riproduzione viene ripresa dopo il trascinamento, il valore dell'indicatore di riproduzione deve riflettere la nuova posizione all'interno del contenuto principale.

1. **Riproduci file multimediali (solo VOD).** Quando si riproduce un file multimediale, è necessario inviare una nuova serie di chiamate Media Start (come se si trattasse di un nuovo inizio).

1. **Visualizzare il file multimediale successivo nella playlist.** All’inizio del file multimediale successivo in una playlist, deve essere inviato un nuovo set di chiamate Media Start.

1. **Consente di commutare il contenuto multimediale o lo streaming.** Quando si passa da un flusso live a un altro, non deve essere inviata una chiamata completa di Media Analytics per il primo flusso. Le chiamate a Media Start e Riproduci devono iniziare con il nuovo nome di spettacolo e flusso e con i valori corretti per l'indicatore di riproduzione e la durata della nuova presentazione.

