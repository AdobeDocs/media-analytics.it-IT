---
seo-title: Riproduzione di Test 1 Standard
title: Riproduzione di Test 1 Standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Test 1: Riproduzione standard{#test-standard-playback}

Questo caso di test convalida la riproduzione generale e la sequenza. È un elemento obbligatorio della richiesta di certificazione.

## Modulo richiesta di certificazione

**Scarica il modulo della richiesta di certificazione qui: = = &gt;**  [Modulo di richiesta certificazione.](cert_req_form.docx)

## Panoramica di Test Test 1

Le implementazioni di Media Analytics includono due tipi di chiamate di tracciamento:
* Chiamate effettuate direttamente al server Adobe Analytics (appmeasurement) - Queste chiamate si verificano negli eventi «Inizio file multimediale» e «Inizio annuncio».
* Chiamate effettuate al server Media Analytics (heartbeats) - che includono chiamate a banda larga e fuori banda:
   * In-banda - L'SDK invia chiamate di riproduzione temporizzate o «coppie» a intervalli di 10 secondi durante la riproduzione del contenuto e a intervalli di un secondo durante gli annunci.
   * Out-of-band - Queste chiamate possono verificarsi in qualsiasi momento e includere Pause, Buffering, errori, contenuto completo, ad complete, ecc.

>[!NOTE]
>Il monitoraggio dei contenuti multimediali si comporta allo stesso modo su tutte le piattaforme.

## Procedura di test

Completa e registra le seguenti azioni (nell'ordine):

1. **Caricare la pagina o l'app**

   **Server di tracciamento** (per tutti i siti Web e le app mobili):

   * **Server Adobe Analytics (appmeasurement):** un server di tracciamento RDC o un CNAME che risolve un server di tracciamento RDC è richiesto per il servizio ID visitatore di Experience Cloud. Il server di tracciamento di Adobe Analytics deve terminare con "`.sc.omtrdc.net`oppure essere un CNAME.

   * **Server Media Analytics (Heartbeats) -** Questo server ha sempre il formato "`[namespace].hb.omtrdc.net`, dove `[namespace]` specifica il nome della società. Questo nome viene fornito da Adobe.
   Devi convalidare alcune variabili chiave universali in tutte le chiamate di tracciamento:

   **ID visitatore Adobe (`mid`):** La `mid` variabile viene utilizzata per acquisire il valore impostato nel cookie AMCV. La `mid` variabile è il valore di identificazione principale sia per i siti Web che per le app mobili, e indica anche che il servizio ID visitatore Experience Cloud è configurato correttamente. Si trova in entrambe le chiamate di Adobe Analytics (appmeasurement) e Media Analytics (heartbeats).

   * **Chiamata di avvio di Adobe Analytics**

      | Parametro | Valore (esempio) |
      |---|---|
      | `pev2` | ms_ s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata pagina Web**

      | Parametro | Valore (esempio) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata del ciclo di vita**

      | Parametro | Valore (esempio) |
      |---|---|
      | `pev2` | ADBINTERNAL: Ciclo di vita |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata di avvio di Media Analytics**

      | Parametro | Valore (esempio) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Nelle chiamate Start di Media Analytics (`s:event:type=start`) i `mid` valori potrebbero non essere presenti. Questo è OK. Possono essere visualizzati solo dopo che le chiamate di Media Analytics Play ( `s:event:type=play`) sono state eseguite.

   * **Chiamata di Media Analytics Play**

      | Parametro | Valore (esempio) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Avviare il lettore multimediale**

   Quando viene avviato il lettore multimediale, Media SDK invia le chiamate chiave ai due server nel seguente ordine:

   1. Server Adobe Analytics - Chiamata di avvio
   1. Server Media Analytics - Chiamata di avvio
   1. Server Media Analytics - "Chiamata di avvio Adobe Analytics richiesta"
   Le prime due chiamate sopra contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La terza chiamata sopra indica al server Media Analytics che Media SDK ha richiesto che il call call di Adobe Analytics (`pev2=ms_s`) venga inviato al server Adobe Analytics.

1. **Visualizza interruzione di annuncio se disponibile**

   * **Inizio annuncio**
   All'avvio dell'annuncio, le seguenti chiamate chiave vengono inviate nel seguente ordine:

   1. Server Adobe Analytics - Chiamata ad Avvio
   1. Server Media Analytics - Chiamata ad Avvio
   1. Server Media Analytics - "Chiamata Adobe Analytics Ad Start richiesta"
   Le prime due chiamate contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   La terza chiamata indica al server Media Analytics che Media SDK ha richiesto che la chiamata ad Adobe Analytics Ad Start (`pev2=msa_s`) venga inviata al server Adobe Analytics.

   * **Ad Play**

      Durante la riproduzione di annunci, Media Analytics SDK invia ogni secondo eventi di riproduzione di tipo «annuncio» al server Media Analytics.

   * **Annuncio completo**

      A 100% punti di un annuncio, è necessario inviare una chiamata Completa di Media Analytics.



1. **Sospendere la riproduzione degli annunci per 30 secondi, se disponibile.****Pausa annuncio**

   Durante la pausa pubblicitaria, le chiamate heartbeat di Media Analytics o «ping» vengono inviate dall'SDK al server Media Analytics ogni secondo.

   >[!NOTE]
   >
   >Il valore della linea di scansione deve rimanere costante durante la pausa.

   Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Riproduci contenuto principale per 10 minuti senza interruzioni.****Riproduzione contenuto**

   Durante la riproduzione del contenuto principale, Media SDK invia heartbeats (chiamate Play) al server Media Analytics ogni 10 secondi.

   Note:

   * La posizione dell'indicatore di riproduzione deve essere incrementata di 10 con ogni chiamata di riproduzione.
   * Il `l:event:duration` valore rappresenta il numero di millisecondi trascorsi dall'ultima chiamata di tracciamento e dovrebbe essere circa lo stesso valore per ogni chiamata di 10 secondi.

      Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Sospendi durante la riproduzione per almeno 30 secondi.** Alla pausa del lettore multimediale, le chiamate all'evento pause verranno inviate dall'SDK al server Media Analytics ogni 10 secondi. Una volta terminata la pausa, gli eventi di riproduzione dovrebbero riprendere.

   Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Cercare/scorrere gli elementi multimediali.** Lo scorrimento dell'indicatore di riproduzione multimediale non consente di inviare chiamate di tracciamento speciali. Tuttavia, quando la riproduzione multimediale riprende dopo lo scorrimento, il valore della linea di scansione deve riflettere la nuova posizione all'interno del contenuto principale.

1. **Riproduci i supporti (solo VOD).** Quando si riproducono i contenuti multimediali, è necessario inviare una nuova serie di chiamate per file multimediali (come se si trattasse di una nuova inizio).

1. **Visualizza i contenuti multimediali successivi nella playlist.** Nella sezione Inizio file multimediali successivi in una playlist, è necessario inviare una nuova serie di chiamate per file multimediali.

1. **Consente di scambiare supporti o flusso.** Quando si passano i flussi live, non è necessario inviare una chiamata completa di Media Analytics al primo flusso. Le chiamate Start Start e le chiamate Play iniziano con il nuovo nome e il nome del flusso, e con i valori corretti della linea di scansione e della durata per la nuova visualizzazione.

