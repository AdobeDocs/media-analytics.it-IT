---
title: Prova 1 riproduzione standard
description: Scopri il test di riproduzione standard utilizzato nella convalida.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 2%

---

# Prova 1: Riproduzione standard{#test-standard-playback}

Questo caso di test convalida la riproduzione e la sequenza generali.

Le implementazioni di Media Analytics includono due tipi di chiamate di tracciamento:
* Chiamate effettuate direttamente al server Adobe Analytics (AppMeasurement) : queste chiamate si verificano sugli eventi &quot;Media Start&quot; e &quot;Ad Start&quot;.
* Chiamate effettuate al server Media Analytics (heartbeat), che includono chiamate in banda e fuori banda:
   * In-band - L’SDK invia chiamate di riproduzione temporizzate o &quot;ping&quot; a intervalli di 10 secondi durante la riproduzione del contenuto e a intervalli di un secondo durante gli annunci.
   * Out-of-band : queste chiamate possono essere eseguite in qualsiasi momento, e includono Pausa, buffering, errori, contenuto completato, annuncio completo, ecc.

>[!NOTE]
>Il tracciamento dei file multimediali si comporta allo stesso modo su tutte le piattaforme.

## Procedura di prova

Completa e registra le seguenti azioni (in ordine):

1. **Caricare la pagina o l’app**

   **Server di tracciamento**  (per tutti i siti web e le app mobili):

   * **Server Adobe Analytics (AppMeasurement):** per il servizio ID visitatore di Experience Cloud è necessario un server di monitoraggio RDC o un CNAME che si risolve in un server di monitoraggio RDC . Il server di tracciamento Adobe Analytics deve terminare con &quot;`.sc.omtrdc.net`&quot; o essere un CNAME.

   * **Server Media Analytics (Heartbeat) -** Questo server ha sempre il formato &quot;`[namespace].hb.omtrdc.net`&quot;, dove  `[namespace]` specifica il nome dell&#39;azienda. Questo nome è fornito dall’Adobe.

   Devi convalidare alcune variabili chiave universali per tutte le chiamate di tracciamento:

   **Adobe ID visitatore (`mid`):** la  `mid` variabile viene utilizzata per acquisire il valore impostato nel cookie AMCV. La variabile `mid` è il valore di identificazione principale sia per i siti web che per le app mobili e indica inoltre che il servizio ID visitatore di Experience Cloud è configurato correttamente. È disponibile sia nelle chiamate Adobe Analytics (AppMeasurement) che Media Analytics (heartbeat).

   * **Adobe Analytics Start call**

      | Parametro | Valore (campione) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Website Page call**

      | Parametro | Valore (campione) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata del ciclo di vita**

      | Parametro | Valore (campione) |
      |---|---|
      | `pev2` | ADBINTERNO:Ciclo di vita |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata iniziale di Media Analytics**

      | Parametro | Valore (campione) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Nelle chiamate di avvio di Media Analytics (`s:event:type=start`) i valori `mid` potrebbero non essere presenti. Questo va bene. Possono essere visualizzati solo dopo le chiamate di Media Analytics Play ( `s:event:type=play`).

   * **Chiamata a Play di Media Analytics**

      | Parametro | Valore (campione) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Avvia il lettore multimediale**

   All’avvio del lettore multimediale, Media SDK invia le chiamate chiave ai due server nell’ordine seguente:

   1. Server Adobe Analytics - Avvia chiamata
   1. Server Media Analytics - Avvia chiamata
   1. Server Media Analytics - &quot;Richiesta chiamata di avvio Adobe Analytics&quot;

   Le prime due chiamate di cui sopra contengono metadati e variabili aggiuntive. Per i parametri e i metadati della chiamata, consulta [Testare i dettagli della chiamata.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La terza chiamata di cui sopra comunica al server Media Analytics che Media SDK ha richiesto l’invio al server Adobe Analytics della chiamata di avvio di Adobe Analytics (`pev2=ms_s`).

1. **Visualizza l’interruzione degli annunci se disponibile**

   * **Inizio annuncio**

   All’avvio dell’annuncio, le seguenti chiamate chiave vengono inviate nell’ordine seguente:

   1. Server Adobe Analytics - Chiamata ad Start
   1. Server Media Analytics - Chiamata ad Start
   1. Server Media Analytics - &quot;Richiesta chiamata Adobe Analytics Ad Start&quot;

   Le prime due chiamate contengono metadati e variabili aggiuntive. Per i parametri e i metadati della chiamata, consulta [Testare i dettagli della chiamata.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   La terza chiamata comunica al server Media Analytics che Media SDK ha richiesto l’invio al server Adobe Analytics della chiamata Adobe Analytics Ad Start (`pev2=msa_s`).

   * **Ad Play**

      Durante la riproduzione di un annuncio, Media Analytics SDK invia al server Media Analytics eventi di riproduzione di tipo &quot;ad&quot; ogni secondo.

   * **Annuncio completato**

      Al 100% di un annuncio, deve essere inviata una chiamata Media Analytics Complete .



1. **Sospendi e riproduci per 30 secondi, se disponibile.**   **Pausa annunci**

   Durante l’Ad Pause, Media Analytics Heartbeat o le chiamate &quot;ping&quot; vengono inviate dall’SDK al server Media Analytics ogni secondo.

   >[!NOTE]
   >
   >Il valore della testina di riproduzione deve rimanere costante durante la pausa.

   Per i parametri e i metadati della chiamata, consulta [Testare i dettagli della chiamata.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Riprodurre il contenuto principale per 10 minuti senza interruzioni.**   **Riproduzione dei contenuti**

   Durante la riproduzione del contenuto principale, Media SDK invia heartbeat (chiamate di riproduzione) al server Media Analytics ogni 10 secondi.

   Note:

   * La posizione del playhead dovrebbe aumentare di 10 con ogni chiamata Play.
   * Il valore `l:event:duration` rappresenta il numero di millisecondi trascorsi dall&#39;ultima chiamata di tracciamento e deve corrispondere approssimativamente allo stesso valore per ogni chiamata di 10 secondi.

      Per i parametri e i metadati della chiamata, consulta [Testare i dettagli della chiamata.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pausa durante la riproduzione per almeno 30 secondi.** Quando il lettore multimediale viene messo in pausa, l’SDK invia le chiamate evento in pausa al server Media Analytics ogni 10 secondi. Al termine della pausa, gli eventi di riproduzione dovrebbero riprendere.

   Per i parametri e i metadati della chiamata, consulta [Testare i dettagli della chiamata.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Cercare/eliminare file multimediali.** Tuttavia, quando la riproduzione riprende dopo il lavaggio, il valore della testina di riproduzione deve riflettere la nuova posizione all’interno del contenuto principale, non viene inviata alcuna chiamata di tracciamento speciale.

1. **Riproduci file multimediali (solo VOD).** Quando viene riprodotto un file multimediale, è necessario inviare un nuovo set di chiamate Media Start (come se si trattasse di un nuovo inizio).

1. **Visualizza i file multimediali successivi nella playlist.** All’inizio del file multimediale successivo in una playlist, deve essere inviato un nuovo set di chiamate Media Start.

1. **Consente di commutare il contenuto multimediale o lo streaming.** Quando si passa a flussi in tempo reale, non deve essere inviata una chiamata completa di Media Analytics per il primo flusso. Le chiamate Media Start e Play devono iniziare con il nuovo nome dello show e dello streaming e con i valori corretti della testina di riproduzione e della durata del nuovo show.
