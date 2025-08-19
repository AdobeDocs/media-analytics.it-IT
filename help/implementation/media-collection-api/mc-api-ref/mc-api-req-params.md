---
title: Parametri di richiesta � API Streaming Media Services
description: Quali sono i parametri di richiesta API di Media Collection, le chiavi di richiesta e le descrizioni.
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 98%

---

# Parametri di richiesta {#request-parameters}

## Dati di Analytics

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | S | string | `sessionStart` | URL del server Adobe Analytics |
| `analytics.reportSuite` | S | string | `sessionStart` | ID che identifica i dati di reporting di Analytics |
| `analytics.enableSSL` | N | booleano | `sessionStart` | True o false per abilitare SSL |
| `analytics.visitorId` | N | string | `sessionStart` | L’identificatore Adobe Visitor ID è un ID personalizzato che puoi utilizzare in più applicazioni Adobe. `visitorId` dell’heartbeat è uguale a `VID.` di Analytics |

## Dati del visitatore

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | S | string | `sessionStart` | L’ID organizzazione di Experience Cloud permette di identificare la tua organizzazione nell’ecosistema Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | string | `sessionStart` | Questo è l’ID utente di Experience Cloud (ECID). Nella maggior parte degli scenari è l’ID da utilizzare per identificare un utente. `marketingCloudUserId` dell’heartbeat è uguale a `MID` in Adobe Analytics. Anche se tecnicamente non è necessario, questo parametro è richiesto per accedere alla famiglia di app di Experience Cloud. |
| `visitor.aamLocationHint` | N | numero intero | `sessionStart` | Fornisce dati edge di Adobe Audience Manager; se non viene inserito un valore, il valore è nullo. |
| `appInstallationId` | N | string | `sessionStart` | L’appInstallationId identifica in modo univoco l’app e il dispositivo |

## Dati del contenuto

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `media.id` | S | string | `sessionStart` | Identificativo univoco per il contenuto |
| `media.name` | N | string | `sessionStart` | Nome leggibile per il contenuto |
| `media.length` | S | number | `sessionStart` | Durata del contenuto (secondi) |
| `media.contentType` | S | string | `sessionStart` | Formato del flusso (può essere qualsiasi stringa, alcuni valori consigliati sono “Live”, “VOD” o “Linear”) |
| `media.playerName` | S | string | `sessionStart` | Nome del lettore responsabile del rendering del contenuto |
| `media.channel` | S | string | `sessionStart` | Canale di distribuzione del contenuto. Può trattarsi del nome di un’app mobile, di un sito web o di una proprietà |
| `media.resume` | N | booleano | `sessionStart` | Indica se un utente sta riprendendo una sessione precedente, anziché avviare una nuova sessione |
| `media.sdkVersion` | N | string | `sessionStart` | Versione SDK utilizzata dal lettore |

## Metadati standard del contenuto

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | string | `sessionStart` | Formato flusso, ad esempio “HD“ |
| `media.show` | N | string | `sessionStart` | Nome del programma o della serie |
| `media.season` | N | string | `sessionStart` | Numero della stagione a cui appartiene il programma o la serie |
| `media.episode` | N | string | `sessionStart` | Numero dell’episodio |
| `media.assetId` | N | string | `sessionStart` | Identificatore univoco per il contenuto della risorsa video, ad esempio l’identificatore dell’episodio della serie TV, della risorsa filmato o dell’evento in diretta. In genere questi ID hanno origine da autorità metadati come EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni. |
| `media.genre` | N | string | `sessionStart` | Tipo di contenuto definito dal produttore del contenuto |
| `media.firstAirDate` | N | string | `sessionStart` | Data in cui il contenuto è andato in onda per la prima volta in televisione |
| `media.firstDigitalDate` | N | string | `sessionStart` | Data in cui il contenuto è stato trasmesso per la prima volta su qualsiasi piattaforma digitale |
| `media.rating` | N | string | `sessionStart` | La classificazione è definita da TV Parental Guidelines |
| `media.originator` | N | string | `sessionStart` | Creatore del contenuto |
| `media.network` | N | string | `sessionStart` | Nome della rete o del canale |
| `media.showType` | N | string | `sessionStart` | Tipo di contenuto, espresso come numero intero compreso tra 0 e 3: <ul> <li>0 - Episodio completo </li> <li>1 - Anteprima </li> <li>2 - Clip </li> <li>3 - Altro </li> </ul> |
| `media.adLoad` | N | string | `sessionStart` | Tipo di annuncio caricato |
| `media.pass.mvpd` | N | string | `sessionStart` | MVPD fornita dall’autenticazione Adobe |
| `media.pass.auth` | N | string | `sessionStart` | Indica che l’utente è stato autorizzato dall’autenticazione Adobe (può essere true solo se è impostato) |
| `media.dayPart` | N | string | `sessionStart` | Ora del giorno in cui il contenuto è stato trasmesso |
| `media.feed` | N | string | `sessionStart` | Tipo di feed, ad esempio “West-HD” |

## Dati dell’annuncio

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | string | `adBreakStart` | Nome descrittivo dell’interruzione pubblicitaria |
| `media.ad.podIndex` | S | numero intero | `adBreakStart` | Indice del pod dell&#39;annuncio nel video |
| `media.ad.podSecond` | S | number | `adBreakStart` | Il secondo in cui è iniziato il pod |
| `media.ad.podPosition` | S | numero intero | `adStart` | Indice dell’annuncio nell’interruzione pubblicitaria, partendo da 1 |
| `media.ad.name` | N | string | `adStart` | Nome descrittivo dell’annuncio |
| `media.ad.id` | S | string | `adStart` | Nome dell’annuncio |
| `media.ad.length` | S | number | `adStart` | Lunghezza dell’annuncio video in secondi |
| `media.ad.playerName` | S | string | `adStart` | Nome del lettore che esegue il rendering dell’annuncio |

## Metadati standard dell’annuncio

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | string | `adStart` | Azienda o marchio il cui prodotto è inserito nell’annuncio |
| `media.ad.campaignId` | N | string | `adStart` | ID della campagna pubblicitaria |
| `media.ad.creativeId` | N | string | `adStart` | ID del contenuto creativo |
| `media.ad.siteId` | N | string | `adStart` | ID del sito dell’annuncio |
| `media.ad.creativeURL` | N | string | `adStart` | URL del contenuto dell’annuncio |
| `media.ad.placementId` | N | string | `adStart` | ID di posizionamento dell’annuncio |

## Dati sui capitoli

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | S | numero intero | `chapterStart` | Identifica la posizione del capitolo nel contenuto |
| `media.chapter.offset` | S | number | `chapterStart` | Il secondo nella riproduzione da cui inizia il capitolo |
| `media.chapter.length` | S | number | `chapterStart` | Durata del capitolo in secondi |
| `media.chapter.friendlyName` | N | string | `chapterStart` | Nome descrittivo del capitolo |

## Dati sulla qualità

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | numero intero | Qualsiasi | Velocità in bit media (in bps). Il bitrate medio è calcolato come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione. |
| `media.qoe.droppedFrames` | N | numero intero | Qualsiasi | Numero di fotogrammi non elaborati nel flusso |
| `media.qoe.framesPerSecond` | N | numero intero | Qualsiasi | Numero di fotogrammi al secondo |
| `media.qoe.timeToStart` | N | numero intero | Qualsiasi | Tempo (in millisecondi) trascorso tra il momento in cui l’utente preme il tasto Play e quando il contenuto si carica e inizia la riproduzione |

## Parametri relativi al California Consumer Privacy Act (CCPA) {#ccpa-params}

| Chiave della richiesta  | Obbligatorio | Chiave tipo di richiesta | Impostata su... |  Descrizione |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | booleano | `sessionStart` | Impostato su true se l’utente finale rinuncia alla condivisione dei dati tra Adobe Analytics e altre soluzioni di Experience Cloud (ad esempio Audience Manager). |
| `analytics.optOutShare` | N | booleano | `sessionStart` | Impostato su true se l’utente finale rinuncia alla federazione dei propri dati (ad esempio ad altri clienti di Adobe Analytics). |

## Dettagli aggiuntivi {#additional-details}

### visitor.marketingCloudUserId

Passa l’ID utente Experience Cloud (noto anche come `MID` o `MCID`) alla chiamata `sessionStart` includendolo all’interno della mappa `params` e utilizzando la seguente chiave: **visitor.marketingCloudUserId**. Questa è una funzione utile se è già stata effettuata l’integrazione con altri prodotti Experience Cloud ed è già stato ottenuto il MCID.

>[!NOTE]
>
>Media Analytics (MA) è integrato con la famiglia di app di Experience Cloud (Adobe Analytics, Audience Manager, Target e così via). È necessario un Experience Cloud ID per accedere a queste app. _Nella maggior parte degli scenari, per identificare gli utenti dovrai usare l’ECID._

### appInstallationId

* **Se *non* si passa un valore `appInstallationId` -** Il back-end MA non genera più un MCID, ma si basa su Adobe Analytics a questo scopo. Adobe consiglia di inviare un MCID se disponibile oppure un `appInstallationId` (insieme a `marketingCloudOrgId`, sempre obbligatorio), in modo che l’API Media Collection generi l’identificativo MCID e lo invii a tutte le chiamate.

* **Se si *passa* un valore `appInstallationId` -** L’identificativo MCID *può* essere generato dal back-end MA, se si trasmettono i valori per `appInstallationId` e i parametri `marketingCloudOrgId` (obbligatori). Se trasmetti `appInstallationId`, devi assicurarti di renderlo persistente lato client. Deve essere specifico per l’app su un dispositivo e deve essere mantenuto finché l’app non viene reinstallata.

>[!NOTE]
>
>`appInstallationId` identifica in modo univoco l’app *e il dispositivo*. Deve essere univoco per ogni app su ciascun dispositivo, ovvero due utenti che utilizzano la stessa versione della stessa app su dispositivi diversi devono inviare ciascuno un `appInstallationId` diverso (univoco).

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Oltre a essere necessario per la generazione di MCID se non viene fornito, questo parametro viene utilizzato anche come valore per l’ID dell’editore (in base al quale Media Analytics esegue la [corrispondenza della regola federativa.](/help/use-cases/federated-media.md))

### ID dell’utente legacy di Analytics (aid) e ID degli utenti dichiarati (customerID)

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

Tieni presente che il valore `visitor.customerIDs` può contenere un numero qualsiasi di oggetti nel formato presentato.

### visitor.aamLocationHint

Questo parametro indica quale rete Edge di Adobe Audience Manager (AAM) viene raggiunta quando Adobe Analytics invia i dati del cliente ad Audience Manager. Se non si immette alcun valore, tale valore sarà nullo. Ciò è particolarmente importante se gli utenti finali utilizzano i loro dispositivi in posizioni geograficamente distanti (ad esempio, Stati Uniti orientali, Stati Uniti occidentali, Europa, Asia). In caso contrario, i dati dell’utente saranno distribuiti su più reti Edge di AAM.

### media.resume

Se l’app determina che una sessione è stata chiusa e ripresa in un secondo momento (ad esempio se l’utente interrompe il video e lo riprende più tardi dal punto in cui era stata interrotta la riproduzione), puoi inviare un parametro booleano facoltativo **media.resume** all’interno del bucket dei parametri della chiamata `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
