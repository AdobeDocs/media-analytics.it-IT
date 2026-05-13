---
title: 'Prova 1: riproduzione standard'
description: Scopri il test di riproduzione standard utilizzato nella convalida.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ChiE4jNDe-8GnbzNp8f9epCCFi6Hq9FkwrLzZEbcxcU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 854
ht-degree: 84%

---

# Prova 1: riproduzione standard{#test-standard-playback}

Questo caso di test convalida le operazioni generali di riproduzione e sequenza.

Le implementazioni di Media Analytics includono due tipi di chiamate di tracciamento:
* Chiamate effettuate direttamente al server di Adobe Analytics (AppMeasurement): queste si verificano per gli eventi di avvio di un file multimediale (Media Start) o di un annuncio (Ad Start).
* Chiamate effettuate al server di Media Analytics (heartbeat), che includono le chiamate in banda e fuori banda:
   * In banda: l’SDK invia chiamate di riproduzione temporizzate, o “ping”, a intervalli di 10 secondi durante la riproduzione del contenuto e a intervalli di un secondo durante gli annunci.
   * Fuori banda: queste chiamate possono essere eseguite in qualsiasi momento, e includono pausa, buffering, errori, contenuto completato, annuncio completato, ecc.

>[!NOTE]
>Il tracciamento dei contenuti multimediali si comporta allo stesso modo su tutte le piattaforme.

## Procedura del test

Completa e registra le seguenti azioni (in ordine):

1. **Caricare la pagina o l’app**

   **Server di tracciamento** (per tutti i siti web e le app mobili):

   * **Server di Adobe Analytics (AppMeasurement)**: per il servizio Experience Cloud Visitor ID è necessario un server di tracciamento RDC o un CNAME che viene risolto in un server di tracciamento RDC. Il server di tracciamento di Adobe Analytics deve terminare in “`.sc.omtrdc.net`” oppure essere un CNAME.

   * **Server di Media Analytics (heartbeat)**: questo server ha sempre il formato “`[namespace].hb.omtrdc.net`”, in cui `[namespace]` specifica il nome della tua azienda. Questo nome è fornito da Adobe.

   Devi convalidare alcune variabili chiave universali per tutte le chiamate di tracciamento:

   **Adobe Visitor ID (`mid`):** la variabile `mid` viene utilizzata per acquisire il valore impostato nel cookie AMCV. La variabile `mid` corrisponde al valore di identificazione principale sia per i siti web che per le app mobili e indica inoltre che il servizio Experience Cloud Visitor ID è configurato correttamente. Si trova sia nelle chiamate di Adobe Analytics (AppMeasurement) che in quelle di Media Analytics (heartbeat).

   * **Chiamata Start di Adobe Analytics**

     | Parametro | Valore (di esempio) |
     |---|---|
     | `pev2` | ms_s |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata per pagina del sito web**

     | Parametro | Valore (di esempio) |
     |---|---|
     | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata Lifecycle**

     | Parametro | Valore (di esempio) |
     |---|---|
     | `pev2` | ADBINTERNAL:Lifecycle |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata Start di Media Analytics**

     | Parametro | Valore (di esempio) |
     |---|---|
     | `s:event:type` | inizio |

     >[!NOTE]
     >
     >Nelle chiamate Start di Media Analytics (`s:event:type=start`) i valori `mid` potrebbero non essere presenti. Non si tratta di un errore. Potrebbero essere visualizzati solo dopo le chiamate Play di Media Analytics (`s:event:type=play`).

   * **Chiamata Play di Media Analytics**

     | Parametro | Valore (di esempio) |
     |---|---|
     | `s:event:type` | play |
     | `s:user:mid` | 30250035503789876473484580554595324209 |

1. **Avviare il lettore multimediale**

   All’avvio del lettore multimediale, Media SDK invia le chiamate chiave ai due server nell’ordine seguente:

   1. Server di Adobe Analytics: chiamata Start
   1. Server di Media Analytics: chiamata Start
   1. Server di Media Analytics: “richiesta di chiamata Start di Adobe Analytics”

   Le prime due chiamate contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consulta [Dettagli delle chiamate di prova.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   La terza chiamata comunica al server di Media Analytics che Media SDK ha richiesto che la chiamata Start di Adobe Analytics (`pev2=ms_s`) sia inviata al server di Adobe Analytics.

1. **Visualizzare l’eventuale interruzione pubblicataria**

   * **Ad Start**

   All’avvio dell’annuncio, le seguenti chiamate chiave vengono inviate nell’ordine seguente:

   1. Server di Adobe Analytics: chiamata Ad Start
   1. Server di Media Analytics: chiamata Ad Start
   1. Server di Media Analytics: “richiesta di chiamata Ad Start di Adobe Analytics”

   Le prime due chiamate contengono metadati e variabili aggiuntive. Per i parametri e i metadati delle chiamate, consulta [Dettagli della chiamata di prova.](/help/legacy/validation/test-call-details.md#view-ad-playback)

   La terza chiamata comunica al server di Media Analytics che Media SDK ha richiesto che la chiamata Ad Start di Adobe Analytics (`pev2=msa_s`) sia inviata al server di Adobe Analytics.

   * **Ad Play**

     Durante la riproduzione di un annuncio, Media Analytics SDK invia al server eventi di riproduzione di tipo “ad” ogni secondo.

   * **Ad Complete**

     Quando un annuncio è stato completato, deve essere inviata una chiamata di completamento di Media Analytics.

1. **Se disponibile, sospendere la riproduzione dell’annuncio per 30 secondi.**  **Ad Pause**

   Durante la pausa dell’annuncio, gli heartbeat, o le chiamate “ping”, di Media Analytics vengono inviate ogni secondo dall’SDK al server di Media Analytics.

   >[!NOTE]
   >
   >Durante la pausa, il valore della testina di riproduzione deve rimanere costante.

   Per i parametri e i metadati delle chiamate, consulta [Dettagli della chiamata di prova.](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)

1. **Riprodurre il contenuto principale per 10 secondi senza interruzioni.**  **Content Play**

   Durante la riproduzione del contenuto principale, Media SDK inviaogni 10 secondi heartbeat (chiamate Play) al server di Media Analytics.

   Note:

   * La posizione della testina di riproduzione deve aumentare di 10 con ogni chiamata Play.
   * Il valore `l:event:duration` rappresenta il numero di millisecondi trascorsi dall’ultima chiamata di tracciamento e deve corrispondere approssimativamente allo stesso valore per ogni chiamata di 10 secondi.

     Per i parametri e i metadati della chiamata, consulta [Dettagli della chiamata di prova.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Pausa durante la riproduzione per almeno 30 secondi.** Quando il lettore multimediale viene messo in pausa, il SDK invia chiamate per l’evento Pausa al server Media Analytics ogni 10 secondi. Al termine della pausa, gli eventi Play devono riprendere.

   Per i parametri e i metadati della chiamata, consulta [Dettagli della chiamata di prova.](/help/legacy/validation/test-call-details.md#pause-main-content)

1. **Ricerca/Scorrimento file multimediali.** Durante lo scorrimento della testina di riproduzione dei contenuti multimediali, non vengono inviate chiamate di tracciamento particolari. Tuttavia, quando la riproduzione riprende dopo lo scorrimento, il valore della testina di riproduzione deve rispecchiare la nuova posizione all’interno del contenuto principale.

1. **Riproduci file multimediali (solo VOD).** Quando un file multimediale viene riprodotto di nuovo, è necessario inviare un nuovo set di chiamate Media Start (come se si trattasse di un nuovo avvio).

1. **Visualizza file multimediali successivi nella playlist.** All’avvio del contenuto successivo in una playlist, deve essere inviato un nuovo set di chiamate Media Start.

1. **Cambiare contenuto multimediale o flusso.** Quando si passa a un altro streaming in diretta, per il primo streaming non deve essere inviata una chiamata di completamento di Media Analytics. Le chiamate Media Start e Play devono iniziare con il nome del nuovo programmo e streaming, e con i valori corretti di testina di riproduzione e durata relativi al nuovo programma.
