---
title: Parametri del capitolo
description: null
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Parametri del capitolo{#chapter-parameters}

Questo argomento presenta un elenco dei dati relativi ai capitoli e/o ai segmenti, compresi i valori dei dati contestuali, raccolti da Adobe tramite variabili della soluzione.

Descrizione dati tabella:

* **** Implementazione: Informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è richiesto per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analisi inviata all’avvio del supporto, *Ad Start* è la chiamata di analisi inviata all’inizio e all’inizio dell’annuncio, e così via; le chiamate *Close* sono le chiamate di analisi compilate inviate direttamente dal server Heartbeat al server di analisi alla fine della sessione multimediale, o la fine dell'annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione* SDK - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore* di esempio - Fornisce un esempio di utilizzo comune delle variabili.
* **** Parametri di rete: Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **** Reporting: Informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiedono una configurazione personalizzata (*Personalizzato*)
   * *Variabile* riservata - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome* report - Nome del report Adobe Analytics per la variabile
   * *Dati* contestuali - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed* dati - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono descritte in Reporting/Riservato Variabile come "classificazione".\
>Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per il tracciamento dei supporti. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per poter accedere alle nuove proprietà del supporto. Durante il processo di aggiornamento, Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di essi, Adobe aggiunge di nuovo quelli mancanti.

## Metadati capitolo {#chapter-metadata}

### Nome capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [nome](./chapter-parameters.md#related_apis_section) </li> <li> ****<br/>  Chiave API: media.capitolo.friendlyName </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Inizio capitolo, Chiudi capitolo </li> <li> **Min.** Versione SDK: 1.3 </li> <li> ****<br/> Valore campione: "Il Big Bang Capitolo 2 - Dating" </li><li> **Descrizione:**<br/>il nome del capitolo e/o del segmento.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>friendlyName) </li> <li> ****<br/> Heartbeat: (s:stream:nome_capitolo) </li> </ul> | <ul> <li> ****<br/> Disponibile: Creato per impostazione predefinita..  </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto:Nome capitolo </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>friendlyName) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>friendlyName) </li> </ul> |

### Posizione capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> ****<br/>  Chiave API: media.capitolo.index </li> <li> ****<br/> Obbligatorio: SDK: No; API: Sì. </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiudi capitolo </li> <li> **Min.** Versione SDK: 1.3 </li> <li> ****<br/> Valore campione: 2 </li><li> **Descrizione:**<br/>la posizione (indice, numero intero) del capitolo all'interno del contenuto.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>posizione) </li> <li> ****<br/> Heartbeat: (l:stream:capitolo_pos) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto:Posizione capitolo </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>posizione) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>posizione) </li> </ul> |

###  Offset capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> ****<br/>  Chiave API: media.Chapter.offset </li> <li> ****<br/> Obbligatorio: SDK: No; API: Sì. </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiudi capitolo </li> <li> **Min.** Versione SDK: 1.3 </li> <li> ****<br/> Valore campione: 58 </li><li> **Descrizione:**<br/>l’offset del capitolo all’interno del contenuto (in secondi) dall’inizio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>offset) </li> <li> ****<br/> Heartbeat: (l:stream:Chapter_offset) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto: Offset capitolo </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>offset) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>offset) </li> </ul> |

### Lunghezza capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/>  Chiave API: media.Chapter.length </li> <li> ****<br/> Obbligatorio: SDK: No; API: Sì. </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiudi capitolo </li> <li> **Min.** Versione SDK: 1.3 </li> <li> ****<br/> Valore campione: 486 </li><li> **Descrizione:**<br/>la lunghezza del capitolo, in secondi.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>length) </li> <li> ****<br/> Heartbeat: (l:flusso:lunghezza_capitolo) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto:Lunghezza capitolo </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>length) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>length) </li> </ul> |

###  Capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiudi capitolo </li> <li> **Min.** Versione SDK: 1.3 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>ID generato automaticamente del capitolo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>nome) </li> <li> ****<br/> Heartbeat: (s:stream:capitolo_id) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Capitolo </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>nome) </li> <li> ****<br/> Feed dati: videocapitolo </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>nome) </li> </ul> |

## Metriche del capitolo {#chapter-Metrics}

### Inizio capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente  </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:Yes </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con:Inizio capitolo </li> <li> **Min.** Versione SDK: 1.3 </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>il numero di inizio del capitolo.  **** Importante:Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>view) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=Chapter_start) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Inizio capitolo g </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>view) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>view) </li> </ul> |

### Capitolo Completa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente  </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:Yes </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiudi capitolo </li> <li> **Min.** Versione SDK: 1.3</li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>Numero di completamento del capitolo.  **** Importante:Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>completato) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=Chapter_complete) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Capitolo Completamento g </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>completato) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>completato) </li> </ul> |

### Tempo capitolo trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente  </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:Yes </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiudi capitolo </li> <li> **Min.** Versione SDK: 1.3 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>Tempo trascorso sul capitolo.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.Chapter.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Tempo capitolo trascorso g </li> <li> ****<br/> Dati contestuali: (a.media.Chapter.<br/>timePlayed) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Chapter.<br/>timePlayed) </li> </ul> |

## API correlate {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
