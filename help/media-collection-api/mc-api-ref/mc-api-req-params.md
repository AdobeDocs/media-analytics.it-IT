---
seo-title: Parametri di richiesta
title: Parametri di richiesta
uuid: f 83 e 9 ef 1-803 d -4152-a 6 c 7-acaa 325036 b 9
translation-type: tm+mt
source-git-commit: 4c5fe469d5ef858e1caa65a25cc23d2a84637144

---


# Request parameters{#request-parameters}

## Dati di Analytics

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | L'URL del server Adobe Analytics |
| `analytics.reportSuite` | Y | `sessionStart` | ID che identifica i dati di reporting di Analytics |
| `analytics.enableSSL` | N | `sessionStart` | True o false per abilitare SSL |
| `analytics.visitorId` | N | `sessionStart` | L'ID visitatore Adobe è un ID personalizzato che puoi utilizzare tra più applicazioni Adobe. The Heartbeat `visitorId` equals the Analytics `VID.` |

## Dati visitatore

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | L'ID organizzazione Experience Cloud; identifica la tua organizzazione nell'ecosistema Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Questo è l'ID utente di Experience Cloud (ECID). Nella maggior parte dei casi, questo è l'ID che devi usare per identificare un utente. The Heartbeat `marketingCloudUserId` equals the `MID` in Adobe Analytics. Anche se tecnicamente non richiesto, questo parametro è necessario per accedere alla famiglia di app Experience Cloud. |
| `visitor.aamLocationHint` | N | `sessionStart` | Fornisce i dati di Adobe Audience Manager Edge |
| `appInstallationId` | N | `sessionStart` | Appinstallationid identifica l'app e il dispositivo in modo univoco |

## Dati contenuto

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Identificatore univoco per il contenuto |
| `media.name` | N | `sessionStart` | Nome del contenuto per il contenuto |
| `media.length` | Y | `sessionStart` | Lunghezza contenuto (secondi) |
| `media.contentType` | Y | `sessionStart` | Formato del flusso (può essere qualsiasi stringa, alcuni valori ridirezionati sono "Live", "VOD" o "Linear") |
| `media.playerName` | Y | `sessionStart` | Nome del lettore responsabile del rendering del contenuto |
| `media.channel` | Y | `sessionStart` | Canale di distribuzione del contenuto. Potrebbe trattarsi di un nome applicazione mobile o di un nome di sito Web, nome proprietà |
| `media.resume` | N | `sessionStart` | Indica se un utente sta riprendendo una sessione precedente (anziché avviare una nuova sessione) |
| `media.sdkVersion` | N | `sessionStart` | Il vertice dell'SDK utilizzato dal lettore |

## Metadati standard di contenuto

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | Il nome del programma o della serie |
| `media.season` | N | `sessionStart` | Il numero di stagione che mostra o serie appartiene a |
| `media.episode` | N | `sessionStart` | Numero dell'episodio |
| `media.assetId` | N | `sessionStart` | L'identificatore univoco del contenuto della risorsa video, ad esempio l'identificatore dell'episodio serie TV, l'identificatore delle risorse del filmato o l'identificatore eventi live. In genere questi ID sono derivati da autorità di metadati quali EIDR, TMS/Gracenote o Rovi. Tali identificatori possono essere di altri sistemi proprietari o interni. |
| `media.genre` | N | `sessionStart` | Tipo di contenuto definito dal produttore del contenuto |
| `media.firstAirDate` | N | `sessionStart` | Data di inizio del contenuto per la televisione |
| `media.firstDigitalDate` | N | `sessionStart` | Data in cui il contenuto viene messo in primo piano su qualsiasi piattaforma digitale |
| `media.rating` | N | `sessionStart` | Classificazione come definito dalle linee guida per i genitori TV |
| `media.originator` | N | `sessionStart` | Autore del contenuto |
| `media.network` | N | `sessionStart` | Il nome di rete/canale |
| `media.showType` | N | `sessionStart` | Il tipo di contenuto, espresso sotto forma di numero intero compreso tra 0 e 3: <ul> <li>0 - Episodio completo </li> <li>1 - Anteprima </li> <li>2 - Clip </li> <li>3 - Altro </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Tipo di annuncio caricato |
| `media.pass.mvpd` | N | `sessionStart` | MVPD fornito dall'autenticazione Adobe |
| `media.pass.auth` | N | `sessionStart` | Indica che l'utente è stato autorizzato dall'autenticazione Adobe (può essere true solo se impostato) |
| `media.dayPart` | N | `sessionStart` | L'ora del giorno in cui è stato trasmesso il contenuto |
| `media.feed` | N | `sessionStart` | Tipo di feed, ad esempio "West-HD" |

## Dati annuncio

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Nome intuitivo dell'interruzione di annuncio |
| `media.ad.podIndex` | Y | `adBreakStart` | Indice del contenitore annuncio nel video |
| `media.ad.podSecond` | Y | `adBreakStart` | Il secondo in cui il contenitore è iniziato |
| `media.ad.podPosition` | Y | `adStart` | Indice dell'annuncio all'interno dell'interruzione di annuncio a partire da 1 |
| `media.ad.name` | N | `adStart` | Nome intuitivo dell'annuncio |
| `media.ad.id` | Y | `adStart` | Nome dell'annuncio |
| `media.ad.length` | Y | `adStart` | Lunghezza del video ad secondi |
| `media.ad.playerName` | Y | `adStart` | Nome del lettore responsabile del rendering dell'annuncio |

## Metadati standard

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | La società o il marchio il cui prodotto viene presentato nell'annuncio |
| `media.ad.campaignId` | N | `adStart` | ID della campagna pubblicitaria |
| `media.ad.creativeId` | N | `adStart` | ID dell'annuncio creativo |
| `media.ad.siteId` | N | `adStart` | ID del sito di annunci |
| `media.ad.creativeURL` | N | `adStart` | L'URL dell'annuncio creativo |
| `media.ad.placementId` | N | `adStart` | ID posizionamento dell'annuncio |

## Dati capitolo

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifica la posizione del capitolo nel contenuto |
| `media.chapter.offset` | Y | `chapterStart` | Il secondo nella riproduzione in cui inizia il capitolo |
| `media.chapter.length` | Y | `chapterStart` | Lunghezza del capitolo in secondi |
| `media.chapter.friendlyName` | N | `chapterStart` | Il nome intuitivo del capitolo |

## Dati di qualità

| Chiave richiesta  | Obbligatorio | Imposta su… |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Any | Bitrate del flusso |
| `media.qoe.droppedFrames` | N | Any | Numero di fotogrammi rilasciati nel flusso |
| `media.qoe.framesPerSecond` | N | Any | Il numero di fotogrammi al secondo |
| `media.qoe.timeToStart` | N | Any | Il tempo trascorso (in millisecondi) trascorsi tra la riproduzione degli hit degli utenti e il caricamento e la riproduzione del contenuto |

## Additional Details {#section_ryt_ccy_lcb}

### visitor. marketingclouduserid

Pass the Experience Cloud User ID (also known as the `MID` or `MCID`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. Questa funzione è utile se ti sei già integrato con altri prodotti Experience Cloud e hai già ottenuto il MCID.

>[!NOTE]
>
>Media Analytics (MA) è integrato con la famiglia di app Experience Cloud (Adobe Analytics, Audience Manager, Target e così via). Hai bisogno di un Experience Cloud ID per accedere a queste app. _L'ECID è ciò che dovrebbe essere utilizzato per identificare gli utenti nella maggior parte dei casi._

### Appinstallationid

* **Se non trasmettete *un*`appInstallationId`valore -** il back-end MA non genererà più un MCID, ma si affiderà ad Adobe Analytics per farlo. Adobe's recommendation is to either send a MCID if available, or an `appInstallationId` (along with the still mandatory `marketingCloudOrgId`) so that the Media Collection API generates the MCID and sends it on all calls.

* ***Se*trasmettete`appInstallationId`valore -** L'MCID *può essere* generato dal back-end MA, se trasmettete valori per `appInstallationId` e i `marketingCloudOrgId` parametri (richiesti). If you do pass `appInstallationId` yourself, you must persist its value on the client side. Deve essere univoco per l'app su un dispositivo e deve rimanere persistente fintanto che l'app non viene nuovamente installata.

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. It needs to be unique for each app on each device, i.e., two users using the same version of the same app on different devices must each send a different (unique) `appInstallationId`.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor. marketingcloudorgid

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching.](../../federated-analytics.md))

### ID utente legacy di Analytics (aid) e ID utente dichiarati (customerids)

* **analytics. aid:**

   Il valore di questa chiave deve essere una stringa che rappresenta l'ID utente legacy di Analytics
* **visitor. customerids:**

   Il valore di questa chiave deve essere un oggetto del seguente formato:

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>> 
   }
   ```

Note that the `visitor.customerIDs` value can have any number of objects in the presented format.

### visitor. aamlocationhint

Questo parametro indica quale Adobe Audience Manager (AAM) viene raggiunto quando Adobe Analytics invia i dati dei clienti ad Audience Manager. Se non trasmettete questo parametro, Adobe lo codifica a 1. Questo è particolarmente importante quando gli utenti finali tendono a utilizzare i propri dispositivi in posizioni geograficamente remote (ad es., USA-East, USA-West, Europa, Asia). In caso contrario, i dati utente verranno distribuiti su più bordi AAM.

### media. resume

If the app determines that a session was closed and then resumed at a later time, e.g., the user left the video but eventually came back, and the player resumed the video from the playhead where it was stopped, you can send an optional boolean **media.resume** parameter inside the params bucket of the `sessionStart` call.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
