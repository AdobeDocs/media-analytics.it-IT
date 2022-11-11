---
title: Parametri per i capitoli
description: “Scopri i parametri dei capitoli per implementazione, rete e reportistica.”
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 100%

---

# Parametri per i capitoli {#chapter-parameters}

Questo argomento descrive un elenco di dati di capitoli e/o segmenti, inclusi i valori dei dati di contesto, che Adobe raccoglie tramite le variabili di soluzione.

Descrizione dei dati della tabella:

* **Implementazione**: informazioni sui valori e i requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è necessario per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con*: indica quando i dati vengono inviati. *Avvia file multimediale* è la chiamata di Analytics inviata all’avvio del file multimediale. *Avvia annuncio* è la chiamata di Analytics inviata all’avvio dell’annuncio e così via. Le chiamate di *Chiusura* sono le chiamate compilate di Analytics inviate direttamente dal server heartbeat a quello di Analytics al termine della sessione multimediale, oppure dell’annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Versione SDK min.*: indica la versione SDK necessaria per accedere al parametro.
   * *Valore di esempio*: fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete**: mostra i valori trasferiti ai server di Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **Reporting**: informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile*:  Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiede la configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata*:  Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome del rapporto*:  Nome del report Adobe Analytics per la variabile
   * *Dati contestuali*: nome dei dati contestuali di Adobe Analytics trasferiti al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed di dati*: nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager*: nome degli elementi presenti in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito e descritte nella variabile Reporting/Reserved (Reporting/Riservato) come “classificazione”.\
>Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento dei contenuti multimediali. Periodicamente Adobe aggiunge nuove proprietà e in questo caso i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà multimediali. Durante il processo di aggiornamento, l’Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di questi, Adobe aggiunge di nuovo quelli mancanti.

## Metadati capitolo {#chapter-metadata}

### Nome del capitolo

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/>  [nome](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.chapter.friendlyName </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizia capitolo, Chiudi capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> “Il Big Bang Capitolo 2 - Incontri” </li><li> **Descrizione:**<br/> nome del capitolo e/o del segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> creato per impostazione predefinita...  </li> <li> **Variabile riservata:**<br/> classificazione </li> <li> **Nome rapporto:**<br/> nome del capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.dc:title </li> <li> **Percorso campo XDM per raccolta:**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **Percorso campo XDM per reporting:**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### Posizione del capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.chapter.index </li> <li> **Obbligatorio:**<br/> SDK: no. API: sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> Posizione (indice, numero intero) del capitolo all’interno del contenuto.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.capitolo.<br/>position) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Posizione capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>posizione) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>posizione) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.index </li> <li> **Percorso campo XDM per raccolta:**<br/> mediaCollection.chapterDetails.index </li> <li> **Percorso campo XDM per reporting:**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### Offset del capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.chapter.offset </li> <li> **Obbligatorio:**<br/> SDK: no. API: sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio**<br/> 58 </li><li> **Descrizione:**<br/> Offset del capitolo all’interno del contenuto, in secondi dall’inizio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.capitolo.<br/>offset) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Offset capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>offset) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.offset </li> <li> **Percorso campo XDM per raccolta:**<br/> mediaCollection.chapterDetails.offset </li> <li> **Percorso campo XDM per reporting:**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### Durata capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.chapter.length </li> <li> **Obbligatorio:**<br/> SDK: no. API: sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> 486 </li><li> **Descrizione:**<br/> Durata del capitolo in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.capitolo.<br/>length) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Durata capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>lunghezza) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>lunghezza) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.xmpDM:duration </li> <li> **Percorso campo XDM per raccolta:**<br/> mediaCollection.chapterDetails.length </li> <li> **Percorso campo XDM per reporting:**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### Capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID del capitolo generato automaticamente.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.capitolo.<br/>name) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> Capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>nome) </li> <li> **Feed dati:**<br/> videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>nome) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.@id </li> <li> **Percorso campo XDM per reporting:**<br/> mediaReporting.chapterDetails.ID </li> </ul> |

## Metriche dei capitoli {#chapter-Metrics}

### Inizio capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Avvio del capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> Numero di avvii del capitolo. **Importante:** se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.capitolo.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Avvio capitolo</li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>vista) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>vista) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.chapterCount.<br/>value > 0 => “TRUE” </li> <li> **Percorso campo XDM per reporting:**<br/>‧mediaReporting.chapterDetails.isStarted </li> </ul> |

### Capitolo completato

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3</li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> Numero di completamenti del capitolo. **Importante:** se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.capitolo.<br/>complete) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Completamento capitolo</li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>completato) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>completato) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.<br/>completes.value </li> <li> **Percorso campo XDM per reporting:**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### Tempo trascorso capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> Tempo trascorso sul capitolo. Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.capitolo.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo trascorso su capitolo</li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>timePlayed) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.<br/>timePlayed.value </li> <li> **Percorso campo XDM per reporting:**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## API correlate {#related_apis_section}

* Android: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS: [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
