---
seo-title: Riproduzione di Test 1 Standard
title: Riproduzione di Test 1 Standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Test 1: Riproduzione standard{#test-standard-playback}

Questo caso di test convalida la riproduzione generale e la sequenza. È richiesto come parte del modulo richiesta di certificazione.

**Scarica il modulo della richiesta di certificazione qui: = = &gt;**  [Modulo di richiesta certificazione.](cert_req_form.docx)

Le implementazioni dei file multimediali sono costituite dai seguenti tipi di chiamate di tracciamento:
* Le chiamate per file multimediali e Ad avvio vengono inviate direttamente al server appmeasurement (Adobe Analytics).
* Le chiamate heartbeat di Media Analytics vengono inviate all'inizio e ogni dieci secondi (per contenuto) o di un secondo (per annunci) al server di tracciamento Media Analytics.

>[!NOTE]
>Il monitoraggio dei contenuti multimediali si comporta allo stesso modo su tutte le piattaforme.

È necessario completare e registrare queste azioni nel seguente ordine:

1. **Caricare la pagina o l'app**

   **Server di tracciamento** (per tutti i siti Web e le app mobili):

   * **Appmeasurement (Adobe Analytics):** un server di tracciamento RDC o un CNAME che risolve un server di tracciamento RDC è richiesto per il servizio ID visitatore Experience Cloud. Il server di tracciamento di Analytics deve terminare con "`.sc.omtrdc.net`oppure essere un CNAME.

   * **Media Analytics (Heartbeats) -** Questo server ha sempre il formato "`[namespace].hb.omtrdc.net`, dove `[namespace]` specifica il nome della società. Questo nome viene fornito da Adobe.
   Devi convalidare alcune variabili chiave universali in tutte le chiamate di tracciamento:

   **ID visitatore Adobe (`mid`):** La `mid` variabile viene utilizzata per acquisire il valore impostato nel cookie AMCV. La `mid` variabile è il valore di identificazione principale sia per i siti Web che per le app mobili, e indica anche che il servizio ID visitatore Experience Cloud è configurato correttamente. Si trova sia nelle chiamate appmeasurement che Media Analytics.

   * **Chiamata di riproduzione Media Analytics**

      | Parametro | Valore (esempio) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Chiamata Start di Media Analytics**

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

   * **Chiamata di avvio heartbeat**

      | Parametro | Valore (esempio) |
      |---|---|
      | `s:event:type` | start |

   * **Chiamata avvio VA**

      >[!NOTE]
      >
      >In VA Start Calls (`s:event:type=start`) i `mid` valori potrebbero non essere presenti. Questo è OK. Possono essere visualizzati solo fino a quando VA Play ( `s:event:type=play`).

      | Parametro | Valore (esempio) |
      |---|---|
      | `pev2` | ms_ s |


1. **Avviare il lettore multimediale**

   All'avvio del lettore multimediale, le chiamate principali vengono inviate nel seguente ordine:

   1. Inizio analisi file multimediali
   1. Avvio heartbeat
   1. Analytics Analytics start
   Le prime due chiamate sopra contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md)

1. **Visualizza interruzione di annuncio se disponibile**

   * **Inizio annuncio**
   All'avvio dell'annuncio multimediale, le seguenti chiamate chiave vengono inviate nel seguente ordine:

   1. Inizio analisi annunci multimediali
   1. Avvio heartbeat
   1. Inizio analisi annunci heartbeat
   Le prime due chiamate contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Ad Play**

      Durante la riproduzione degli annunci, le chiamate Heartbeat vengono inviate al server Heartbeat ogni secondo.

   * **Annuncio completo**

      A 100% punti su un annuncio pubblicitario, viene inviata una chiamata completa Heartbeat.



1. **Sospendere la riproduzione degli annunci per 30 secondi, se disponibile.****Pausa annuncio**

   Durante la pausa degli annunci, le chiamate Heartbeat vengono inviate al server Heartbeat ogni secondo.

   >[!NOTE]
   >
   >Il valore della linea di scansione deve rimanere costante durante la pausa.

1. **Riproduci contenuti multimediali principali per 10 minuti senza interruzioni.****Riproduzione contenuto**

   Durante la riproduzione del contenuto principale, le chiamate heartbeat vengono inviate al server Media Analytics ogni dieci secondi.

   Note:

   * La posizione dell'indicatore di riproduzione deve essere incrementata di 10 con ogni chiamata di riproduzione.
   * Il `l:event:duration` valore rappresenta il numero di millisecondi trascorsi dall'ultima chiamata di tracciamento e dovrebbe essere circa lo stesso valore per ogni chiamata di 10 secondi.

      Per i parametri e i metadati delle chiamate, consultate [Dettagli sulle chiamate di test.](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **Sospendi durante la riproduzione per almeno 30 secondi.** Alla pausa del lettore multimediale, le chiamate all'evento pause verranno inviate ogni 10 secondi. Dopo la pausa, gli eventi di riproduzione dovrebbero riprendere.

1. **Cercare/scorrere gli elementi multimediali.** Quando si esegue lo scorrimento dell'indicatore di riproduzione multimediale, non vengono inviate chiamate di tracciamento speciali, tuttavia, quando la riproduzione multimediale riprende dopo lo scorrimento del valore dell'indicatore di riproduzione deve riflettere la nuova posizione all'interno del contenuto principale.

1. **Riproduci i supporti (solo VOD).** Quando si riproducono i contenuti multimediali, è necessario inviare una nuova serie di chiamate per iniziare, come se si trattasse di una nuova visualizzazione multimediale.

1. **Visualizza i contenuti multimediali successivi nella playlist.** Quando si avvia l'inizio del supporto successivo in una playlist, è necessario inviare una nuova serie di chiamate di avvio multimediale.

1. **Consente di scambiare supporti o flusso.** Quando si passano i flussi dal vivo, non è necessario inviare una chiamata completa Heartbeat per il primo flusso. Le chiamate di avvio multimediale e le chiamate di riproduzione per file multimediali devono iniziare con il nome del nuovo show e del flusso e con i valori corretti della linea di scansione e della durata per la nuova visualizzazione.

