---
title: Parametri di richiesta
description: null
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
translation-type: tm+mt
source-git-commit: 64a91795bd2f9120991be2a67e68c645dc24c8d1
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 6%

---

# Parametri di richiesta{#request-parameters}

## Dati di Analytics

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | URL del server Adobe Analytics |
| `analytics.reportSuite` | Y | `sessionStart` | ID che identifica i dati di reporting di Analytics |
| `analytics.enableSSL` | N | `sessionStart` | True o false per abilitare SSL |
| `analytics.visitorId` | N | `sessionStart` | L’ID visitatore Adobe è un ID personalizzato che puoi utilizzare in più applicazioni Adobe. Heartbeat `visitorId` è uguale a Analytics `VID.` |

## Dati dei visitatori

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | L&#39;ID organizzazione Experience Cloud; identifica la tua organizzazione all&#39;interno dell&#39;ecosistema Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Questo è l&#39;ID utente Experience Cloud (ECID). Nella maggior parte degli scenari, si tratta dell’ID da utilizzare per identificare un utente. Heartbeat `marketingCloudUserId` è uguale a `MID` in Adobe Analytics. Anche se non tecnicamente necessario, questo parametro è necessario per accedere alla famiglia di app di Experience Cloud. |
| `visitor.aamLocationHint` | N | `sessionStart` | Fornisce dati di Adobe Audience Manager Edge: se non viene inserito un valore, il valore è null. |
| `appInstallationId` | N | `sessionStart` | L&#39;appInstallationId identifica in modo univoco l&#39;app e il dispositivo |

## Dati contenuto

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Identificativo univoco per il contenuto |
| `media.name` | N | `sessionStart` | Nome leggibile per il contenuto |
| `media.length` | Y | `sessionStart` | Lunghezza del contenuto (secondi) |
| `media.contentType` | Y | `sessionStart` | Formato del flusso (può essere qualsiasi stringa, alcuni valori consigliati sono &quot;Live&quot;, &quot;VOD&quot; o &quot;Lineare&quot;) |
| `media.playerName` | Y | `sessionStart` | Nome del lettore responsabile del rendering del contenuto |
| `media.channel` | Y | `sessionStart` | Canale di distribuzione del contenuto. Può trattarsi di un nome di applicazione mobile o di un nome di sito web, di un nome di proprietà |
| `media.resume` | N | `sessionStart` | Indica se un utente sta riprendendo una sessione precedente o meno (anziché avviare una nuova sessione) |
| `media.sdkVersion` | N | `sessionStart` | Versione SDK utilizzata dal lettore |

## Metadati standard del contenuto

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.streamFormat` | N | `sessionStart` | Formato flusso, ad esempio &quot;HD&quot; |
| `media.show` | N | `sessionStart` | Nome del programma o della serie |
| `media.season` | N | `sessionStart` | Numero di stagione a cui appartiene lo show o la serie |
| `media.episode` | N | `sessionStart` | Numero dell&#39;episodio |
| `media.assetId` | N | `sessionStart` | Identificatore univoco per il contenuto della risorsa video, ad esempio l&#39;identificatore dell&#39;episodio della serie TV, l&#39;identificatore della risorsa filmato o l&#39;identificatore dell&#39;evento live. In genere questi ID sono derivati da autorità di metadati come EIDR, TMS/Gracenote o Rovi. Questi identificatori possono anche provenire da altri sistemi proprietari o interni. |
| `media.genre` | N | `sessionStart` | Tipo di contenuto definito dal produttore del contenuto |
| `media.firstAirDate` | N | `sessionStart` | La data in cui il contenuto è andato in onda per la prima volta in televisione |
| `media.firstDigitalDate` | N | `sessionStart` | Data in cui il contenuto è stato trasmesso per la prima volta su qualsiasi piattaforma digitale |
| `media.rating` | N | `sessionStart` | La classificazione è definita dalle linee guida per i genitori televisivi |
| `media.originator` | N | `sessionStart` | Creatore del contenuto |
| `media.network` | N | `sessionStart` | Nome rete/canale |
| `media.showType` | N | `sessionStart` | Il tipo di contenuto, espresso come numero intero compreso tra 0 e 3: <ul> <li>0 - Episodio completo </li> <li>1 - Anteprima </li> <li>2 - Clip </li> <li>3 - Altro </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Il tipo di annuncio caricato |
| `media.pass.mvpd` | N | `sessionStart` | MVPD fornito dall&#39;autenticazione Adobe |
| `media.pass.auth` | N | `sessionStart` | Indica che l’utente è stato autorizzato dall’autenticazione di Adobe (può essere true solo se è impostato) |
| `media.dayPart` | N | `sessionStart` | Ora del giorno in cui il contenuto è stato trasmesso |
| `media.feed` | N | `sessionStart` | Tipo di feed, ad esempio &quot;West-HD&quot; |

## Dati annuncio

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Nome descrittivo dell’interruzione pubblicitaria |
| `media.ad.podIndex` | Y | `adBreakStart` | Indice del pod dell&#39;annuncio nel video |
| `media.ad.podSecond` | Y | `adBreakStart` | Il secondo a cui ha iniziato il pod |
| `media.ad.podPosition` | Y | `adStart` | Indice dell&#39;annuncio all&#39;interno dell&#39;interruzione pubblicitaria a partire da 1 |
| `media.ad.name` | N | `adStart` | Nome descrittivo dell&#39;annuncio |
| `media.ad.id` | Y | `adStart` | Nome dell’annuncio |
| `media.ad.length` | Y | `adStart` | Lunghezza dell’annuncio video in secondi |
| `media.ad.playerName` | Y | `adStart` | Nome del lettore responsabile del rendering dell&#39;annuncio |

## Metadati Ad Standard

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | Azienda o marchio il cui prodotto è presente nell’annuncio |
| `media.ad.campaignId` | N | `adStart` | ID della campagna pubblicitaria |
| `media.ad.creativeId` | N | `adStart` | ID dell’annuncio creativo |
| `media.ad.siteId` | N | `adStart` | ID del sito dell’annuncio |
| `media.ad.creativeURL` | N | `adStart` | URL dell’annuncio creativo |
| `media.ad.placementId` | N | `adStart` | ID di posizionamento dell’annuncio |

## Capitolo Dati

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifica la posizione del capitolo nel contenuto |
| `media.chapter.offset` | Y | `chapterStart` | Il secondo nella riproduzione in cui inizia il capitolo |
| `media.chapter.length` | Y | `chapterStart` | Lunghezza del capitolo in secondi |
| `media.chapter.friendlyName` | N | `chapterStart` | Il nome umano del capitolo |

## Dati di qualità

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Any | Il bitrate del flusso |
| `media.qoe.droppedFrames` | N | Qualsiasi | Numero di fotogrammi saltati nel flusso |
| `media.qoe.framesPerSecond` | N | Qualsiasi | Numero di fotogrammi al secondo |
| `media.qoe.timeToStart` | N | Qualsiasi | Tempo (in millisecondi) trascorso tra il momento in cui l’utente preme il tasto Play e il contenuto carica e inizia la riproduzione |

## Parametri del California Consumer Privacy Act (CCPA) {#ccpa-params}

| Chiave richiesta  | Obbligatorio | Attiva... |  Descrizione  |
| --- | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | `sessionStart` | Imposta su true quando l’utente finale rinuncia alla condivisione dei dati tra Adobe Analytics e altre soluzioni di Experience Cloud (ad Audience Manager) |
| `analytics.optOutShare` | N | `sessionStart` | Imposta su true quando l’utente finale ha rinunciato alla federazione dei propri dati (ad esempio, ad altri client Adobe Analytics). |

## Dettagli aggiuntivi {#additional-details}

### visitor.marketingCloudUserId

Passa l’ID utente Experience Cloud (noto anche come `MID` o `MCID`) nella chiamata `sessionStart` includendolo nella mappa `params` utilizzando la seguente chiave: **visitor.marketingCloudUserId**. Questa è una funzione utile se ti sei già integrato con altri prodotti Experience Cloud e hai già ottenuto il MCID.

>[!NOTE]
>
>Media Analytics (MA) è integrato con la famiglia Experience Cloud di app (Adobe Analytics, Audience Manager, Target e così via). È necessario un ID Experience Cloud per accedere a queste app. _L’ECID è ciò che è necessario utilizzare per identificare gli utenti nella maggior parte degli scenari._

### appInstallationId

* **Se  *non* passi un  `appInstallationId` valore -** Il back-end MA non genera più un MCID, ma si basa su Adobe Analytics per farlo. Si consiglia di inviare un MCID se disponibile oppure un `appInstallationId` (insieme al `marketingCloudOrgId` ancora obbligatorio) in modo che l’API di raccolta multimediale generi l’MCID e lo invii a tutte le chiamate.

* **Se si  ** ignora  `appInstallationId` il valore -** Il MCID  *può essere generato* dal back-end MA, se si passano i valori per  `appInstallationId` e i  `marketingCloudOrgId` parametri (obbligatori). Se si passa `appInstallationId` personalmente, è necessario mantenere il relativo valore sul lato client. Deve essere univoco per l&#39;app su un dispositivo e deve essere persistente finché l&#39;app non viene reinstallata.

>[!NOTE]
>
>L’ `appInstallationId` identifica in modo univoco l’app *e il dispositivo*. Deve essere univoco per ogni app su ciascun dispositivo, ovvero due utenti che utilizzano la stessa versione della stessa app su dispositivi diversi devono ciascuno inviare un `appInstallationId` diverso (univoco).

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Oltre a essere necessario per la generazione MCID quando non viene fornito, questo parametro viene utilizzato anche come valore per l&#39;ID dell&#39;editore (in base al quale Media Analytics esegue [corrispondenza delle regole di federazione.](/help/federated-analytics.md))

### ID utente legacy di Analytics (aid) e ID utente dichiarati (customerIDs)

* **analytics.aid:**

   Il valore di questa chiave deve essere una stringa che rappresenta l’ID utente legacy di Analytics
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

Questo parametro indica quale Adobe Audience Manager (AAM) Edge verrebbe colpito quando Adobe Analytics invia i dati del cliente ad Audience Manager. Se non trasmetti questo parametro, Adobe lo codifica a 1. Ciò è particolarmente importante quando gli utenti finali tendono a utilizzare i loro dispositivi in posizioni geograficamente distanti (ad esempio, Stati Uniti-Est, Stati Uniti-Ovest, Europa, Asia). In caso contrario, i dati utente verranno distribuiti su più AAM Edge.

### media.resume

Se l’app determina che una sessione è stata chiusa e ripresa in un secondo momento, ad esempio, l’utente ha lasciato il video ma alla fine è tornato e il lettore ha ripreso il video dal playhead in cui è stato arrestato, puoi inviare un parametro booleano opzionale **media.curriculum** all’interno del bucket dei parametri della chiamata `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
