---
title: Parametri del capitolo
description: null
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: ef237fd0d9e2bcebe011d819224d98d450830d07
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 2%

---


# Parametri del capitolo{#chapter-parameters}

Questo argomento presenta un elenco di dati di capitoli e/o segmenti, compresi i valori dei dati di contesto, che  Adobe raccoglie tramite variabili della soluzione.

Descrizione dati tabella:

* **Implementazione:** informazioni su valori e requisiti di implementazione
   * *Chiave*  - Variabile, impostata manualmente nell&#39;app o automaticamente dall&#39;SDK per file multimediali del Adobe .
   * *Obbligatorio*  - Indica se il parametro è richiesto per il tracciamento video di base.
   * *Tipo*  - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con*  - Indica quando i dati vengono inviati:  *Media* Start è la chiamata di analisi inviata all’avvio del supporto,  *Ad* Started è la chiamata di analisi inviata all’avvio dell’annuncio e così via; le  ** chiusure sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server di analisi alla fine della sessione multimediale, oppure alla fine dell&#39;annuncio, del capitolo e così via. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione SDK* - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore*  di esempio - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** visualizza i valori passati ai server Adobe Analytics o Heartbeat . Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate da  Adobe Media SDK.
* **Rapporti:** informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile*  - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiedono una configurazione personalizzata (*Personalizzato*)
   * *Variabile*  riservata - Indica se i dati vengono acquisiti come evento,  eVar, prop o classificazione in una variabile riservata.
   * *Nome*  report - Nome del report di analisi dei Adobi  per la variabile
   * *Dati*  contestuali - Nome dei dati contestuali  Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed*  dati - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager*   - Nome caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono descritte in Reporting/Riservato Variabile come &quot;classificazione&quot;.\
>Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per il tracciamento dei supporti. Di tanto in tanto,  Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà del supporto. Durante il processo di aggiornamento  Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di loro,  Adobe aggiunge di nuovo quelli mancanti.

## Metadati capitolo {#chapter-metadata}

### Nome capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.capitolo.friendlyName </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:Inizio**<br/> capitolo, Chiudi capitolo </li> <li> **Min. Versione SDK:** 1.3 </li> <li> **Valore Campione:**<br/> &quot;Il Big Bang Capitolo 2 - Appuntamento&quot; </li><li> **Descrizione:**<br/> il nome del capitolo e/o del segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:stream:Chapter_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Creato per impostazione predefinita..  </li> <li> **Variabile Riservata:**<br/> Classificazione </li> <li> **Nome rapporto:Nome**<br/> capitolo </li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>friendlyName) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>friendlyName) </li> </ul> |

### Posizione capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.capitolo.index </li> <li> **Obbligatorio:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:Chiusura**<br/> capitolo </li> <li> **Min. Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> la posizione (indice, numero intero) del capitolo all&#39;interno del contenuto.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (l:stream:Chapter_pos) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/> Classificazione </li> <li> **Nome Rapporto:Posizione**<br/> Capitolo </li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>posizione) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>posizione) </li> </ul> |

### Offset capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.Chapter.offset </li> <li> **Obbligatorio:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:Chiusura**<br/> capitolo </li> <li> **Min. Versione SDK:** 1.3 </li> <li> **Valore Di Esempio:**<br/> 58 </li><li> **Descrizione:**<br/> l’offset del capitolo all’interno del contenuto (in secondi) dall’inizio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>offset) </li> <li> **Heartbeat:**<br/> (l:stream:Chapter_offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/> Classificazione </li> <li> **Nome rapporto:Offset**<br/> capitolo </li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>offset) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>offset) </li> </ul> |

### Lunghezza capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.Chapter.length </li> <li> **Obbligatorio:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:Chiusura**<br/> capitolo </li> <li> **Min. Versione SDK:** 1.3 </li> <li> **Valore Di Esempio:**<br/> 486 </li><li> **Descrizione:**<br/> la lunghezza del capitolo, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>length) </li> <li> **Heartbeat:**<br/> (l:stream:Chapter_length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/> Classificazione </li> <li> **Nome Rapporto:Lunghezza**<br/> Capitolo </li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>length) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>length) </li> </ul> |

### Capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:Chiusura**<br/> capitolo </li> <li> **Min. Versione SDK:** 1.3 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/> l’ID generato automaticamente del capitolo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (s:stream:capitolo_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome rapporto:**<br/> Capitolo </li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>name) </li> <li> **Feed dati:**<br/> videocapitolo </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>name) </li> </ul> |

## Metriche del capitolo {#chapter-Metrics}

### Inizio capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:Inizio**<br/> capitolo </li> <li> **Min. Versione SDK:** 1.3 </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di inizio del capitolo.  **Importante:**  se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=Chapter_start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Inizio**<br/> Capitolo</li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>view) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>view) </li> </ul> |

### Capitolo Completa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:Chiusura**<br/> capitolo </li> <li> **Min. Versione SDK:** 1.3</li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> Numero di completamento del capitolo.  **Importante:**  se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>completato) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=Chapter_complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Completamento**<br/> Capitolo</li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>completato) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>completato) </li> </ul> |

### Tempo capitolo trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:Chiusura**<br/> capitolo </li> <li> **Min. Versione SDK:** 1.3 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/> Tempo trascorso sul capitolo.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.Chapter.<br/>timePlayed) </li> <li> **Battito cardiaco:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Tempo**<br/> Capitolo trascorso</li> <li> **Dati contestuali:**<br/> (a.media.Chapter.<br/>timePlayed) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.Chapter.<br/>timePlayed) </li> </ul> |

## API correlate {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
