---
seo-title: Riproduzione di Test 1 Standard
title: Riproduzione di Test 1 Standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Test 1: Standard playback{#test-standard-playback}

Questo caso di test convalida la riproduzione generica e la sequenza ed è richiesto come parte del modulo di richiesta di certificazione. Download the certification request form here: [Certification Request Form.](cert_req_form_nielsen.docx)

Le implementazioni dei video sono costituite dai seguenti tipi di chiamate di tracciamento:
* Le chiamate Video e Avvio annunci vengono inviate direttamente al server appmeasurement.
* Le chiamate heartbeat di Media Analytics (MA) vengono inviate all'inizio e ogni dieci secondi al server di tracciamento Adobe VA.

>[!NOTE]
>Il monitoraggio dei video si comporta allo stesso modo su tutte le piattaforme, su desktop e dispositivi mobili.

È necessario completare e registrare le azioni nell'ordine seguente:

1. **Caricare la pagina o l'app**

   **Server di tracciamento** (per tutti i siti Web e le app mobili):

   * **Appmeasurement (Adobe Analytics):** un server di tracciamento RDC o un CNAME che risolve un server RDC è richiesto per il servizio ID visitatore Experience Cloud. The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **Media Analytics (Heartbeats):** questo server ha sempre il formato `[namespace].hb.omtrdc.net`, dove `[namespace]` viene definito dalla società di accesso e fornito da Adobe.
   Devi convalidare determinate variabili chiave, universali in tutte le chiamate di tracciamento:

   **ID visitatore Adobe (`mid`):** La `mid` variabile viene utilizzata per acquisire il valore impostato nel cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Si trova sia nelle chiamate appmeasurement che Media Analytics (MA).

   * **Chiamata Heartbeat Play**

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
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. Questo è OK. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Parametro | Valore (esempio) |
      |---|---|
      | `pev2` | ms_ s |


1. **Avviare il lettore video**

   All'avvio del lettore video, le chiamate principali vengono inviate nel seguente ordine:

   1. Inizio analisi video
   1. Avvio heartbeat
   1. Analytics Analytics start
   Le prime due chiamate sopra contengono metadati e variabili aggiuntive. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Visualizza interruzione di annuncio se disponibile**

   * **Inizio annuncio**
   All'avvio dell'annuncio video, le seguenti chiamate chiave vengono inviate nel seguente ordine:

   1. Inizio analisi annunci video
   1. Avvio heartbeat
   1. Inizio analisi annunci heartbeat
   Le prime due chiamate contengono metadati e variabili aggiuntive. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Ad Play**

      Durante la riproduzione degli annunci, le chiamate Heartbeat vengono inviate al server Heartbeat ogni secondo.

   * **Annuncio completo**

      A 100% punti su un annuncio pubblicitario, viene inviata una chiamata completa Heartbeat.



1. **Sospendere la riproduzione degli annunci per 30 secondi, se disponibile.****Pausa annuncio**

   Durante la pausa degli annunci, le chiamate Heartbeat vengono inviate al server Heartbeat ogni secondo.

   >[!NOTE]
   >
   >Il valore della linea di scansione deve rimanere costante durante la pausa.

1. **Riproduci video principale per 10 minuti senza interruzioni.**** Riproduzione contenuto**

   Durante la riproduzione di contenuto principale normale, le chiamate Heartbeat vengono inviate al server Heartbeat ogni dieci secondi.

   Note:

   * La posizione dell'indicatore di riproduzione deve essere incrementata di 10 con ogni chiamata di riproduzione.
   * The `l:event:duration` value represents the number of milliseconds since the last tracking call and should be roughly the same value on each 10 second call.

      For call parameters and metadata, see [Test call details](../../sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **Sospendi durante la riproduzione per almeno 30 secondi.** Alla pausa del lettore video, le chiamate all'evento sospenderanno ogni 10 secondi. Dopo la pausa, gli eventi di riproduzione dovrebbero riprendere.

1. **Ricerca/scorrimento video.** Quando si esegue lo scorrimento dell'indicatore di riproduzione video, non vengono inviate chiamate di tracciamento speciali, tuttavia, quando la riproduzione video riprende dopo lo scorrimento del valore dell'indicatore di riproduzione deve riflettere la nuova posizione all'interno del contenuto principale.

1. **Riproduci video (solo VOD).** Quando un video viene riprodotto, è necessario inviare una nuova serie di chiamate di avvio video, come se si trattasse di una nuova visualizzazione video.

1. **Visualizzare il video successivo nella playlist.** All'inizio del video del video successivo in una playlist, è necessario inviare una nuova serie di chiamate di avvio video.

1. **Consente di scambiare video o flusso.** Quando si passano i flussi dal vivo, non è necessario inviare una chiamata completa Heartbeat per il primo flusso. Le chiamate di avvio video e le chiamate di riproduzione video devono iniziare con il nuovo nome e il nome del flusso e con i valori corretti della linea di scansione e della durata per il nuovo show.

