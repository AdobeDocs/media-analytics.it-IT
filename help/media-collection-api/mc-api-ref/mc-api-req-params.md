---
seo-title: Parametri di richiesta
title: Parametri di richiesta
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: 5fc38098bcd497f3305f76ae2b23757b5f81ac69

---


# Request parameters{#request-parameters}

## Dati di Analytics

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | L'URL del server Adobe Analytics |
| `analytics.reportSuite` | Y | `sessionStart` | ID che identifica i dati di reporting di Analytics |
| `analytics.enableSSL` | N | `sessionStart` | True o false per abilitare SSL |
| `analytics.visitorId` | N | `sessionStart` | L’ID visitatore Adobe è un ID personalizzato che puoi utilizzare in più applicazioni Adobe. Heartbeat `visitorId` è uguale ad Analytics `VID.` |

## Dati visitatore

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | L’ID organizzazione Experience Cloud; identifica la tua organizzazione all'interno del sistema eco di Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Questo è l’ID utente di Experience Cloud (ECID). Nella maggior parte dei casi si tratta dell’ID da utilizzare per identificare un utente. Heartbeat `marketingCloudUserId` equivale a `MID` in Adobe Analytics. Sebbene non sia tecnicamente richiesto, questo parametro è necessario per accedere alla famiglia di app Experience Cloud. |
| `visitor.aamLocationHint` | N | `sessionStart` | Fornisce i dati Edge di Adobe Audience Manager |
| `appInstallationId` | N | `sessionStart` | L'appInstallationId identifica in modo univoco l'app e il dispositivo |

## Dati contenuto

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Identificatore univoco per il contenuto |
| `media.name` | N | `sessionStart` | Nome leggibile per il contenuto |
| `media.length` | Y | `sessionStart` | Lunghezza contenuto (secondi) |
| `media.contentType` | Y | `sessionStart` | Formato del flusso (può essere una qualsiasi stringa, alcuni valori consigliati sono "Live", "VOD" o "Lineare") |
| `media.playerName` | Y | `sessionStart` | Nome del lettore responsabile del rendering del contenuto |
| `media.channel` | Y | `sessionStart` | Canale di distribuzione del contenuto. Può trattarsi di un nome di applicazione mobile o di un nome di sito Web, di un nome di proprietà |
| `media.resume` | N | `sessionStart` | Indica se un utente sta riprendendo una sessione precedente (anziché avviare una nuova sessione) |
| `media.sdkVersion` | N | `sessionStart` | Versione SDK utilizzata dal lettore |

## Metadati standard contenuto

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | Il nome del programma o della serie |
| `media.season` | N | `sessionStart` | Numero di stagione a cui appartiene lo spettacolo o la serie |
| `media.episode` | N | `sessionStart` | Numero dell'episodio |
| `media.assetId` | N | `sessionStart` | Identificatore univoco per il contenuto della risorsa video, ad esempio l’identificatore episodio della serie TV, l’identificatore della risorsa filmato o l’identificatore evento live. In genere questi ID sono derivati da autorità di metadati quali EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni. |
| `media.genre` | N | `sessionStart` | Tipo di contenuto definito dal produttore del contenuto |
| `media.firstAirDate` | N | `sessionStart` | Data in cui il contenuto è stato trasmesso per la prima volta in televisione |
| `media.firstDigitalDate` | N | `sessionStart` | Data in cui il contenuto è stato trasmesso per la prima volta su qualsiasi piattaforma digitale |
| `media.rating` | N | `sessionStart` | La valutazione definita dalle linee guida TV per i genitori |
| `media.originator` | N | `sessionStart` | Il creatore del contenuto |
| `media.network` | N | `sessionStart` | Nome rete/canale |
| `media.showType` | N | `sessionStart` | Il tipo di contenuto, espresso come numero intero compreso tra 0 e 3: <ul> <li>0 - Episodio completo </li> <li>1 - Anteprima </li> <li>2 - Clip </li> <li>3 - Altro </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Il tipo di annuncio caricato |
| `media.pass.mvpd` | N | `sessionStart` | MVPD fornito dall'autenticazione Adobe |
| `media.pass.auth` | N | `sessionStart` | Indica che l'utente è stato autorizzato dall'autenticazione Adobe (può essere true solo se è impostato) |
| `media.dayPart` | N | `sessionStart` | Ora del giorno in cui è stato trasmesso il contenuto |
| `media.feed` | N | `sessionStart` | Tipo di feed, ad esempio "West-HD" |

## Dati annuncio

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Nome descrittivo dell'interruzione dell'annuncio |
| `media.ad.podIndex` | Y | `adBreakStart` | Indice del contenitore annuncio nel video |
| `media.ad.podSecond` | Y | `adBreakStart` | Il secondo all’inizio del contenitore |
| `media.ad.podPosition` | Y | `adStart` | L'indice dell'annuncio all'interno dell'interruzione dell'annuncio a partire da 1 |
| `media.ad.name` | N | `adStart` | Nome descrittivo dell'annuncio |
| `media.ad.id` | Y | `adStart` | Nome dell'annuncio |
| `media.ad.length` | Y | `adStart` | Lunghezza del video annuncio in secondi |
| `media.ad.playerName` | Y | `adStart` | Nome del lettore responsabile del rendering dell'annuncio |

## Aggiungi metadati standard

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | La società o il marchio il cui prodotto è presente nell'annuncio |
| `media.ad.campaignId` | N | `adStart` | ID della campagna pubblicitaria |
| `media.ad.creativeId` | N | `adStart` | L'ID dell'annuncio creativo |
| `media.ad.siteId` | N | `adStart` | L'ID del sito dell'annuncio |
| `media.ad.creativeURL` | N | `adStart` | L'URL dell'annuncio creativo |
| `media.ad.placementId` | N | `adStart` | L'ID di posizionamento dell'annuncio |

## Dati del capitolo

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifica la posizione del capitolo nel contenuto |
| `media.chapter.offset` | Y | `chapterStart` | Seconda fase della riproduzione in cui inizia il capitolo |
| `media.chapter.length` | Y | `chapterStart` | Lunghezza del capitolo in secondi |
| `media.chapter.friendlyName` | N | `chapterStart` | Il nome umano del capitolo |

## Dati di qualità

| Chiave richiesta | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Any | Bitrate del flusso |
| `media.qoe.droppedFrames` | N | Any | Numero di fotogrammi saltati nel flusso |
| `media.qoe.framesPerSecond` | N | Any | Numero di fotogrammi al secondo |
| `media.qoe.timeToStart` | N | Any | Tempo (in millisecondi) trascorso tra il momento in cui l'utente accede al programma di riproduzione e il momento in cui il contenuto viene caricato e riprodotto |

## Dettagli aggiuntivi {#section_ryt_ccy_lcb}

### visitor.marketingCloudUserId

Passa l’ID utente di Experience Cloud (noto anche come `MID` o `MCID`) alla `sessionStart` chiamata inserendolo nella `params` mappa utilizzando la seguente chiave: **visitor.marketingCloudUserId**. Questa funzione è utile se hai già effettuato l’integrazione con altri prodotti Experience Cloud e hai già ottenuto il MCID.

>[!NOTE]
>
>Media Analytics (MA) è integrato con la famiglia di app Experience Cloud (Adobe Analytics, Audience Manager, Target e così via). Per accedere a queste app è necessario un Experience Cloud ID. _L’ECID è l’elemento da utilizzare per identificare gli utenti nella maggior parte degli scenari._

### appInstallationId

* **Se *non*trasmettete un`appInstallationId`valore,** il back-end MA non genererà più un MCID, ma si affiderà ad Adobe Analytics per farlo. Adobe consiglia di inviare un MCID, se disponibile, oppure un `appInstallationId` (insieme al file ancora obbligatorio `marketingCloudOrgId`) in modo che l'API di Media Collection generi il MCID e lo invii a tutte le chiamate.

* **Se si *passa*il valore -`appInstallationId`Il MCID** può essere *generato dal back-end MA, se si passano i valori per* e i `appInstallationId` `marketingCloudOrgId` parametri (obbligatori). Se `appInstallationId` si passa da soli, è necessario mantenere il relativo valore sul lato client. Deve essere univoco per l'app su un dispositivo e deve essere persistente finché l'app non viene reinstallata.

>[!NOTE]
>
>L'utente identifica in `appInstallationId` modo univoco l'app *e il dispositivo*. Deve essere univoco per ogni app su ciascun dispositivo, ovvero due utenti che utilizzano la stessa versione della stessa app su dispositivi diversi devono inviare ciascuno un'app diversa (univoca) `appInstallationId`.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

Oltre a essere necessario per la generazione MCID quando non viene fornito, questo parametro viene utilizzato anche come valore per l'ID editore (in base al quale Media Analytics esegue la corrispondenza della regola di [federazione.](/help/federated-analytics.md))

### ID utente legacy di Analytics (aid) e ID utente dichiarati (customerID)

* **analytics.aid:**

   Il valore di questa chiave deve essere una stringa che rappresenta l'ID utente legacy di Analytics
* **visitor.customerIDs:**

   Il valore di questa chiave deve essere un oggetto del seguente formato:

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>> 
   }
   ```

Il `visitor.customerIDs` valore può avere un numero qualsiasi di oggetti nel formato presentato.

### visitor.aamLocationHint

Questo parametro indica quale Adobe Audience Manager (AAM) Edge verrebbe colpito quando Adobe Analytics invia i dati del cliente ad Audience Manager. Se non trasmettete questo parametro, Adobe lo codifica a 1. Ciò è particolarmente importante quando gli utenti finali tendono a utilizzare i loro dispositivi in posizioni geograficamente distanti (ad esempio, USA-est, USA-Ovest, Europa, Asia). In caso contrario, i dati dell'utente verranno distribuiti su più bordi AAM.

### media.curriculum

Se l’app determina che una sessione è stata chiusa e quindi ripresa in un secondo momento, ad esempio, l’utente ha lasciato il video ma alla fine è tornato e il lettore ha ripreso il video dall’indicatore di riproduzione in cui è stato interrotto, potete inviare un parametro booleano facoltativo **media.curriculum** all’interno del bucket params della `sessionStart` chiamata.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
