---
title: 'Prova 1: riproduzione standard'
description: Scopri il test di riproduzione standard utilizzato nella convalida.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 100%

---

# Prova 1: riproduzione standard {#test-standard-playback}

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

      | Parametro | Valore (campione) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata per pagina del sito web**

      | Parametro | Valore (campione) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata Lifecycle**

      | Parametro | Valore (campione) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chiamata Start di Media Analytics**

      | Parametro | Valore (campione) |
      |---|---|
      | `s:event:type` | inizio |

      >[!NOTE]
      >
      >Nelle chiamate Start di Media Analytics (`s:event:type=start`) i valori `mid` potrebbero non essere presenti. Non si tratta di un errore. Potrebbero essere visualizzati solo dopo le chiamate Play di Media Analytics (`s:event:type=play`).

   * **Chiamata Play di Media Analytics**

      | Parametro | Valore (campione) |
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

1. **Pausa durante la riproduzione per almeno 30 secondi.** Quando il lettore multimediale viene messo in pausa, l’SDK invia chiamate per l’evento Pausa al server Media Analytics ogni 10 secondi. Al termine della pausa, gli eventi Play devono riprendere.

   Per i parametri e i metadati della chiamata, consulta [Dettagli della chiamata di prova.](/help/legacy/validation/test-call-details.md#pause-main-content)

1. **Ricerca/Scorrimento nei file multimediali.** Durante lo scorrimento della testina di riproduzione dei contenuti multimediali, non vengono inviate chiamate di tracciamento particolari. Tuttavia, quando la riproduzione riprende dopo lo scorrimento, il valore della testina di riproduzione deve rispecchiare la sua nuova posizione all’interno del contenuto principale.

1. **Nuova riproduzione di file multimediali (solo VOD).** Quando un file multimediale viene riprodotto di nuovo, è necessario inviare un nuovo set di chiamate Media Start (come se si trattasse di un nuovo avvio).

1. **Visualizzazione dei contenuti successivi nella playlist.** All’avvio del contenuto successivo in una playlist, deve essere inviato un nuovo set di chiamate Media Start.

1. **Passaggio a un altro contenuto multimediale o streaming.** Quando si passa a un altro streaming in diretta, per il primo streaming non deve essere inviata una chiamata di completamento di Media Analytics. Le chiamate Media Start e Play devono iniziare con il nome del nuovo programmo e streaming, e con i valori corretti di testina di riproduzione e durata relativi al nuovo programma.
