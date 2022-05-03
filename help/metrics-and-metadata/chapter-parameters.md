---
title: 'Parametri per i capitoli '
description: “Scopri i parametri dei capitoli per implementazione, rete e reportistica.”
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c61e0bce6338a2fa89dafa29c4f600c5640d2d97
workflow-type: ht
source-wordcount: '1101'
ht-degree: 100%

---

# Parametri per i capitoli {#chapter-parameters}

Questo argomento descrive un elenco di dati di capitoli e/o segmenti, inclusi i valori dei dati di contesto, che Adobe raccoglie tramite le variabili di soluzione.

Descrizione dei dati della tabella:

* **Implementazione:** informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è obbligatorio per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Avvia media* è la chiamata di Analytics inviata all’avvio dei media, *Inizio annuncio* è la chiamata di Analytics inviata all’inizio dell’annuncio e così via; le chiamate *Chiudi* sono le chiamate di Analytics compilate inviate direttamente dal server Heartbeat al server Analytics al termine della sessione multimediale o alla fine dell’annuncio, del capitolo e così via. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Versione SDK min.* - Indica la versione SDK necessaria per accedere al parametro.
   * *Valore di esempio* - Fornisce un esempio di comune utilizzo delle variabili.
* **Parametri di rete:** visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **Reporting:** informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nella reportistica per impostazione predefinita (*Sì*) o se richiedono la configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata* - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome del rapporto* - Nome del rapporto Adobe Analytics per la variabile
   * *Dati contestuali* - Nome dei dati contestuali di Adobe Analytics passati al server di reportistica e utilizzati nelle regole di elaborazione.
   * *Feed di dati* - Nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome del tratto trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito e descritte nella variabile Reporting/Reserved (Reporting/Riservato) come “classificazione”.\
>Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento dei contenuti multimediali. Periodicamente Adobe aggiunge nuove proprietà e in questo caso i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà multimediali. Durante il processo di aggiornamento, l’Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di questi, Adobe aggiunge di nuovo quelli mancanti.

## Metadati capitolo {#chapter-metadata}

### Nome del capitolo

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [nome](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.chapter.friendlyName </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizia capitolo, Chiudi capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> “Il Big Bang Capitolo 2 - Incontri” </li><li> **Descrizione:**<br/> nome del capitolo e/o del segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> creato per impostazione predefinita...  </li> <li> **Variabile riservata:**<br/> classificazione </li> <li> **Nome rapporto:**<br/> nome del capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.dc:title </li> </ul> |

### Posizione del capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.chapter.index </li> <li> **Obbligatorio:**<br/> SDK: no. API: sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> Posizione (indice, numero intero) del capitolo all’interno del contenuto.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Posizione capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>position) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.chapterAssetViewDetails.index </li> </ul> |

### Offset del capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.chapter.offset </li> <li> **Obbligatorio:**<br/> SDK: no. API: sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio**<br/> 58 </li><li> **Descrizione:**<br/> Offset del capitolo all’interno del contenuto, in secondi dall’inizio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Offset capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.chapterAssetViewDetails.offset </li> </ul> |

### Durata capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.chapter.length </li> <li> **Obbligatorio:**<br/> SDK: no. API: sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> 486 </li><li> **Descrizione:**<br/> Durata del capitolo in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Durata capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>length) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>length) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.xmpDM:duration </li> </ul> |

### Capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Impostata automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID del capitolo generato automaticamente.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> Capitolo </li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>name) </li> <li> **Feed dati:**<br/> videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.@id </li> </ul> |

## Metriche dei capitoli {#chapter-Metrics}

### Inizio capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Impostata automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Avvio del capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> Numero di avvii del capitolo. **Importante:** se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Avvio capitolo</li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>view) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>view) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.chapterCount.value > 0 > “TRUE” </li> </ul> |

### Capitolo completato

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Impostata automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3</li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> Numero di completamenti del capitolo. **Importante:** se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Completamento capitolo</li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.completes.value </li> </ul> |

### Tempo trascorso capitolo

|   Implementazione  | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Impostata automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura capitolo </li> <li> **Versione SDK min.:** 1.3 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> Tempo trascorso sul capitolo. Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**   **</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo trascorso su capitolo</li> <li> **Dati contestuali:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaChapter.timePlayed.value </li> </ul> |

## API correlate {#related_apis_section}

* Android: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS: [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length)
* Javascript: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
