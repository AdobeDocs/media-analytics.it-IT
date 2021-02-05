---
title: Parametri di richiesta
description: null
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: b1b94b4cde74908ea528fb69d78250dc1da1db80
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 6%

---


# Richiedi parametri{#request-parameters}

## Dati di Analytics

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | URL del server Adobe Analytics  |
| `analytics.reportSuite` | Y | `sessionStart` | L&#39;ID che identifica i dati di reporting di Analytics |
| `analytics.enableSSL` | N | `sessionStart` | True o false per abilitare SSL |
| `analytics.visitorId` | N | `sessionStart` | L&#39;ID visitatore  Adobe è un ID personalizzato che puoi utilizzare in più applicazioni  Adobe. Heartbeat `visitorId` è uguale a Analytics `VID.` |

## Dati visitatore

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | L&#39;ID organizzazione Experience Cloud ; identifica l&#39;organizzazione all&#39;interno del sistema Adobe Experience Cloud eco |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Questo è l&#39;ID utente del Experience Cloud  (ECID). Nella maggior parte dei casi si tratta dell’ID da utilizzare per identificare un utente. Heartbeat `marketingCloudUserId` è uguale a `MID` in  Adobe Analytics. Sebbene non sia tecnicamente richiesto, questo parametro è necessario per accedere alla famiglia di app  Experience Cloud. |
| `visitor.aamLocationHint` | N | `sessionStart` | Fornisce dati Adobe Audience Manager Edge |
| `appInstallationId` | N | `sessionStart` | L&#39;appInstallationId identifica in modo univoco l&#39;app e il dispositivo |

## Dati contenuto

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Identificativo univoco per il contenuto |
| `media.name` | N | `sessionStart` | Nome leggibile per il contenuto |
| `media.length` | Y | `sessionStart` | Lunghezza del contenuto (secondi) |
| `media.contentType` | Y | `sessionStart` | Formato del flusso (può essere una qualsiasi stringa, alcuni valori consigliati sono &quot;Live&quot;, &quot;VOD&quot; o &quot;Lineare&quot;) |
| `media.playerName` | Y | `sessionStart` | Nome del lettore responsabile del rendering del contenuto |
| `media.channel` | Y | `sessionStart` | Canale di distribuzione del contenuto. Può trattarsi di un nome di applicazione mobile o di un nome di sito Web, di un nome di proprietà |
| `media.resume` | N | `sessionStart` | Indica se un utente sta riprendendo una sessione precedente (anziché avviare una nuova sessione) |
| `media.sdkVersion` | N | `sessionStart` | Versione SDK utilizzata dal lettore |

## Metadati standard contenuto

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.streamFormat` | N | `sessionStart` | Formato flusso, ad esempio &quot;HD&quot; |
| `media.show` | N | `sessionStart` | Il nome del programma o della serie |
| `media.season` | N | `sessionStart` | Numero di stagione a cui appartiene lo spettacolo o la serie |
| `media.episode` | N | `sessionStart` | Numero dell&#39;episodio |
| `media.assetId` | N | `sessionStart` | Identificatore univoco per il contenuto della risorsa video, ad esempio l’identificatore episodio della serie TV, l’identificatore della risorsa filmato o l’identificatore evento live. In genere questi ID sono derivati da autorità di metadati quali EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni. |
| `media.genre` | N | `sessionStart` | Tipo di contenuto definito dal produttore del contenuto |
| `media.firstAirDate` | N | `sessionStart` | Data in cui il contenuto è stato trasmesso per la prima volta in televisione |
| `media.firstDigitalDate` | N | `sessionStart` | Data in cui il contenuto è stato trasmesso per la prima volta su qualsiasi piattaforma digitale |
| `media.rating` | N | `sessionStart` | La valutazione definita dalle linee guida TV per i genitori |
| `media.originator` | N | `sessionStart` | Il creatore del contenuto |
| `media.network` | N | `sessionStart` | Nome rete/canale |
| `media.showType` | N | `sessionStart` | Il tipo di contenuto, espresso come numero intero compreso tra 0 e 3: <ul> <li>0 - Episodio completo </li> <li>1 - Anteprima </li> <li>2 - Clip </li> <li>3 - Altro </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Il tipo di annuncio caricato |
| `media.pass.mvpd` | N | `sessionStart` | MVPD fornito dall&#39;autenticazione  Adobe |
| `media.pass.auth` | N | `sessionStart` | Indica che l&#39;utente è stato autorizzato dall&#39;autenticazione  Adobe (può essere true solo se è impostata) |
| `media.dayPart` | N | `sessionStart` | Ora del giorno in cui è stato trasmesso il contenuto |
| `media.feed` | N | `sessionStart` | Tipo di feed, ad esempio &quot;West-HD&quot; |

## Dati annuncio

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Nome descrittivo dell&#39;interruzione dell&#39;annuncio |
| `media.ad.podIndex` | Y | `adBreakStart` | Indice del contenitore annuncio nel video |
| `media.ad.podSecond` | Y | `adBreakStart` | Il secondo all’inizio del contenitore |
| `media.ad.podPosition` | Y | `adStart` | L&#39;indice dell&#39;annuncio all&#39;interno dell&#39;interruzione dell&#39;annuncio a partire da 1 |
| `media.ad.name` | N | `adStart` | Nome descrittivo dell&#39;annuncio |
| `media.ad.id` | Y | `adStart` | Nome dell&#39;annuncio |
| `media.ad.length` | Y | `adStart` | Lunghezza del video annuncio in secondi |
| `media.ad.playerName` | Y | `adStart` | Nome del lettore responsabile del rendering dell&#39;annuncio |

## Aggiungi metadati standard

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | La società o il marchio il cui prodotto è presente nell&#39;annuncio |
| `media.ad.campaignId` | N | `adStart` | ID della campagna pubblicitaria |
| `media.ad.creativeId` | N | `adStart` | L&#39;ID dell&#39;annuncio creativo |
| `media.ad.siteId` | N | `adStart` | L&#39;ID del sito dell&#39;annuncio |
| `media.ad.creativeURL` | N | `adStart` | L&#39;URL dell&#39;annuncio creativo |
| `media.ad.placementId` | N | `adStart` | L&#39;ID di posizionamento dell&#39;annuncio |

## Dati del capitolo

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifica la posizione del capitolo nel contenuto |
| `media.chapter.offset` | Y | `chapterStart` | Il secondo nella riproduzione in cui inizia il capitolo |
| `media.chapter.length` | Y | `chapterStart` | Lunghezza del capitolo in secondi |
| `media.chapter.friendlyName` | N | `chapterStart` | Il nome umano del capitolo |

## Dati di qualità

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Any | Bitrate del flusso |
| `media.qoe.droppedFrames` | N | Qualsiasi | Numero di fotogrammi saltati nel flusso |
| `media.qoe.framesPerSecond` | N | Qualsiasi | Numero di fotogrammi al secondo |
| `media.qoe.timeToStart` | N | Qualsiasi | Tempo (in millisecondi) trascorso tra il momento in cui l&#39;utente accede al programma di riproduzione e il momento in cui il contenuto viene caricato e riprodotto |

## Parametri dell&#39;Atto sulla privacy dei consumatori California (CCPA) {#ccpa-params}

| Chiave richiesta  | Obbligatorio | Imposta su... |  Descrizione  |
| --- | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | `sessionStart` | Impostato su true quando l&#39;utente finale ha rinunciato a condividere i propri dati tra  Adobe Analytics e altre soluzioni  Experienci Cloud (ad es.  Audience Manager) |
| `analytics.optOutShare` | N | `sessionStart` | Impostato su true quando l&#39;utente finale ha rinunciato alla federazione dei propri dati (ad esempio, ad altri client Adobe Analytics ). |

## Dettagli aggiuntivi {#additional-details}

### visitor.marketingCloudUserId

Passa l&#39;ID utente  Experience Cloud (noto anche come `MID` o `MCID`) sulla chiamata `sessionStart` includendolo nella mappa `params` utilizzando la seguente chiave: **visitor.marketingCloudUserId**. Questa funzione è utile se avete già integrato con altri prodotti  Experience Cloud e avete già ottenuto il MCID.

>[!NOTE]
>
>Media Analytics (MA) è integrato con la famiglia di app  Experience Cloud ( Adobe Analytics,  Audience Manager, Target e così via). Per accedere a queste app è necessario un ID Experience Cloud . _L’ECID è l’elemento da utilizzare per identificare gli utenti nella maggior parte degli scenari._

### appInstallationId

* **Se  *non* trasmettete un  `appInstallationId` valore,** il back-end MA non genererà più un MCID, ma conterà  Adobe Analytics per farlo.  raccomandazione  Adobe consiste nell&#39;inviare un MCID, se disponibile, oppure un `appInstallationId` (insieme al `marketingCloudOrgId` ancora obbligatorio) in modo che l&#39;API di Media Collection generi il MCID e lo invii a tutte le chiamate.

* **Se si  ** ignora  `appInstallationId` il valore -** Il MCID  *può essere* generato dal back-end MA, se si passano i valori per  `appInstallationId` e i  `marketingCloudOrgId` parametri (obbligatori). Se non si passa `appInstallationId` se stessi, è necessario mantenere il relativo valore sul lato client. Deve essere univoco per l&#39;app su un dispositivo e deve essere persistente finché l&#39;app non viene reinstallata.

>[!NOTE]
>
>La `appInstallationId` identifica in modo univoco l&#39;app *e il dispositivo*. Deve essere univoco per ogni app su ciascun dispositivo, ovvero due utenti che utilizzano la stessa versione della stessa app su dispositivi diversi devono inviare ognuno un `appInstallationId` diverso (univoco).

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Oltre a essere necessario per la generazione MCID quando non viene fornito, questo parametro viene utilizzato anche come valore per l&#39;ID editore (in base al quale Media Analytics esegue [corrispondenza tra le regole di federazione.](/help/federated-analytics.md))

### ID utente legacy di Analytics (aid) e ID utente dichiarati (customerID)

* **analytics.aid:**

   Il valore di questa chiave deve essere una stringa che rappresenta l&#39;ID utente legacy di Analytics
* **visitor.customerIDs:**

   Il valore di questa chiave deve essere un oggetto del seguente formato:

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>>
   }
   ```

Il valore `visitor.customerIDs` può avere un numero qualsiasi di oggetti nel formato presentato.

### visitor.aamLocationHint

Questo parametro indica quale Adobe Audience Manager (AAM) Edge viene colpito quando  Adobe Analytics invia i dati del cliente  Audience Manager. Se non trasmettete questo parametro,  Adobe lo codifica a 1. Ciò è particolarmente importante quando gli utenti finali tendono a utilizzare i loro dispositivi in posizioni geograficamente distanti (ad esempio, USA-est, USA-Ovest, Europa, Asia). In caso contrario, i dati dell&#39;utente verranno distribuiti su più AAM Bordi.

### media.resume

Se l&#39;app determina che una sessione è stata chiusa e quindi ripresa in un secondo momento, ad esempio, l&#39;utente ha lasciato il video ma alla fine è tornato e il lettore ha ripreso il video dall&#39;indicatore di riproduzione in cui è stato interrotto, potete inviare un parametro booleano opzionale **media.curriculum** all&#39;interno del bucket dei param della chiamata `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
