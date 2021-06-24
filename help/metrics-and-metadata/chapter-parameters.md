---
title: Parametri del capitolo
description: '"Scopri i parametri dei capitoli per implementazione, rete e reporting."'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 2%

---

# Parametri del capitolo{#chapter-parameters}

Questo argomento presenta un elenco di dati di capitoli e/o segmenti, inclusi i valori dei dati di contesto, che l’Adobe raccoglie tramite variabili della soluzione.

Descrizione dei dati della tabella:

* **Implementazione:** informazioni su valori e requisiti di implementazione
   * *Chiave* : variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Medium.
   * *Obbligatorio*  - Indica se il parametro è necessario per il tracciamento video di base.
   * *Tipo*  - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* : indica quando i dati vengono inviati:  *Media* Startis è la chiamata di analisi inviata all’avvio di un file multimediale,  *Ad* Startis è la chiamata di analisi inviata all’avvio di un annuncio e così via; i  ** Closecalls sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server analytics alla fine della sessione multimediale, o la fine dell&#39;annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min Versione SDK* - Indica la versione SDK necessaria per accedere al parametro.
   * *Valore di esempio*  - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Medium.
* **Rapporti:** informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile*  - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiede una configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata*  - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome report* : nome del report Adobe Analytics per la variabile
   * *Dati contestuali* : nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed di dati* : nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* : nome della caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito descritte in Reporting/Riservato Variable come &quot;classificazione&quot;.\
>Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento dei contenuti multimediali. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà multimediali. Durante il processo di aggiornamento, l’Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di questi, Adobe aggiunge di nuovo quelli mancanti.

## Metadati capitolo {#chapter-metadata}

### Nome del capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.capitolo.friendlyName </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio capitolo, Chiudi capitolo </li> <li> **Min Versione SDK:** 1.3 </li> <li> **Valore Di Esempio:**<br/>  &quot;Il Big Bang Capitolo 2 - Incontri&quot; </li><li> **Descrizione:**<br/> il nome del capitolo e/o del segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>friendlyName) </li> <li> **Heartbeat:**<br/>  (nome_:stream:capitolo) </li> </ul> | <ul> <li> **Disponibile:**<br/> Creato per impostazione predefinita..  </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Nome capitolo </li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>friendlyName) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>friendlyName) </li> </ul> |

### Posizione capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.capitolo.index </li> <li> **Obbligatorio:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura capitolo </li> <li> **Min Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> la posizione (indice, numero intero) del capitolo all’interno del contenuto.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>position) </li> <li> **Heartbeat:**<br/>  (:stream:lcapitolo_pos) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Posizione capitolo </li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>posizione) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>posizione) </li> </ul> |

### Offset capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.capitolo.offset </li> <li> **Obbligatorio:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura capitolo </li> <li> **Min Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> 58 </li><li> **Descrizione:**<br/> l’offset del capitolo all’interno del contenuto (in secondi) dall’inizio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>offset) </li> <li> **Heartbeat:**<br/>  (:stream:lcapitolo_offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Offset capitolo </li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>offset) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>offset) </li> </ul> |

### Lunghezza capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.capitolo.length </li> <li> **Obbligatorio:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura capitolo </li> <li> **Min Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> 486 </li><li> **Descrizione:**<br/> la lunghezza del capitolo, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>length) </li> <li> **Heartbeat:**<br/>  (lunghezza :stream:capitolo_capitolo) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> lunghezza capitolo </li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>lunghezza) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>lunghezza) </li> </ul> |

### Capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura capitolo </li> <li> **Min Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID generato automaticamente del capitolo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>name) </li> <li> **Heartbeat:**<br/>  (:stream:schapter_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> Capitolo </li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>nome) </li> <li> **Feed di dati:**<br/> videocapitolo </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>nome) </li> </ul> |

## Metriche del capitolo {#chapter-Metrics}

### Inizio capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> inizio capitolo </li> <li> **Min Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di inizio del capitolo.  **Importante:**  se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>vista) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=capitolo_start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Inizio capitolo</li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>vista) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>vista) </li> </ul> |

### Capitolo Completo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura capitolo </li> <li> **Min Versione SDK:** 1.3</li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di completamento del capitolo.  **Importante:**  se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>completato) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=capitolo_complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> Capitolo Completato</li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>completato) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>completato) </li> </ul> |

### Tempo capitolo trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura capitolo </li> <li> **Min Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> il tempo trascorso sul capitolo.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.capitolo.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> tempo del capitolo trascorso</li> <li> **Dati contestuali:**<br/>  (a.media.capitolo.<br/>timePlayed) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitolo.<br/>timePlayed) </li> </ul> |

## API correlate {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
