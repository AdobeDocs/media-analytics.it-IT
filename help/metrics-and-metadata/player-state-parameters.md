---
title: Parametri dello stato del lettore
description: '"Scopri i parametri di tracciamento dello stato del lettore per le proprietà a schermo intero, Chiudi didascalia, Disattiva audio e Immagine nell’immagine."'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: cd51ed3a-fe37-41e9-8243-dfd9deb514c1
feature: '"Media Analytics, variabili"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 1%

---

# Parametri dello stato del lettore{#player-state-parameters}

Questo argomento presenta un elenco dei dati sullo stato del lettore che Adobe raccoglie tramite variabili della soluzione.

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

## Proprietà stato lettore {#player-state-properties}

Le funzionalità di tracciamento dello stato del lettore possono essere collegate a un flusso audio o video. Le metriche di tracciamento dello stato del lettore standardizzate sono memorizzate come variabili di soluzione. Gli stati standard sono: fullScreen, muto, closeCaption, pictureInPicture e inFocus.

### Proprietà a schermo intero

#### Streams interessati dallo schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di flussi interessati da Schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> **** <br/> ImportanteSe questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.fullscreen.set<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Report**<br/> NameStreams interessato da Full Screen </li> <li> **Context**<br/> Data.media.States.fullscreen.set<br/> </li> <li> **Data**<br/> Feedvideo statefullscreen </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.fullscreen.set </li> </ul> |

#### Conteggi a schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di volte in cui è stato visualizzato uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> ****<br/> ImportanteSe questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.fullscreen.count<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Conteggio**<br/> a schermo intero del nome del rapporto </li> <li> **Context**<br/> Data.media.States.fullscreen.count<br/> </li> <li> **Data**<br/> Feedvideostatefullscreencount </li> <li> **Audience**<br/> Manager_contextdata.media.States.fullscreen.count </li> </ul> |



#### Durata totale schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneLa durata della visualizzazione di uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> ****<br/>  ImportanteSe questo evento è impostato, l&#39;ora è uguale a quella del video nello stato a schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.  </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.fullscreen.time<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Durata totale**<br/> nome report a schermo intero </li> <li> **Context**<br/> Data.media.States.fullscreen.time<br/> </li> <li> **Data**<br/> Feedvideostatefullscreentime </li> <li> **Audience**<br/> Manager_contextdata.media.States.fullscreen.time </li> </ul> |


### Chiudi proprietà didascalia

#### Streams interessati dai sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di flussi interessati dai sottotitoli. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato dei sottotitoli codificati. <br/> **** <br/>  ImportanteSe questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.closedcaptioning.set<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Report**<br/> NameStreams interessati dai sottotitoli </li> <li> **Context**<br/> Data.media.States.closedcaptioning.set<br/> </li> <li> **Data**<br/> Feedvideostateclosedcaptioning </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.closedcaptioning.set </li> </ul> |


#### Conteggi per sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di volte in cui è stato visualizzato il sottotitolo. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di sottotitoli codificati. <br/> ****<br/>  ImportanteSe questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era nello stato dei sottotitoli. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.closedcaptioning.count<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Conteggio sottotitoli**<br/> nome report </li> <li> **Context**<br/> Data.media.States.closedcaptioning.count<br/> </li> <li> **Data**<br/> Feedvideostateclosedcaptioningcount </li> <li> **Audience**<br/> Manager_contextdata.media.States.closedcaptioning.count </li> </ul> |


#### Durata totale sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneLa durata della visualizzazione dei sottotitoli codificati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> ****<br/>  ImportanteSe questo evento è impostato, l’ora è uguale a quella in cui il video si trovava nello stato dei sottotitoli. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.closedcaptioning.time<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Durata totale**<br/> dei sottotitoli </li> <li> **Context**<br/> Data.media.States.closedcaptioning.time<br/> </li> <li> **Data**<br/> Feedvideostateclosedcaptioningtime </li> <li> **Audience**<br/> Manager_contextdata.media.States.closedcaptioning.time </li> </ul> |


### Proprietà disattivazione audio

#### Streams interessati dall&#39;audio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di flussi interessati dall’audio. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> **** <br/> ImportanteSe questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.mute.set<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Report**<br/> NameStreams interessati da mute </li> <li> **Context**<br/> Data.media.States.mute.set<br/> </li> <li> **Data**<br/> Feedvideo statemute </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.mute.set </li> </ul> |

#### Conteggi disattivati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di volte in cui è stato visualizzato l’opzione Muto. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> ****<br/>  ImportanteSe questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Muto. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.mute.count<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Conteggio**<br/> nome report disattivato </li> <li> **Context**<br/> Data.media.States.mute.count<br/> </li> <li> **Data**<br/> Feedvideo statemutecount </li> <li> **Audience**<br/> Manager_contextdata.media.States.mute.count </li> </ul> |

#### Durata totale disattivazione

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneLa durata dell’audio in modalità disattivazione (Muto). Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> ****<br/> ImportanteSe questo evento è impostato, l&#39;ora è uguale a quanto tempo il video era nello stato Muto. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.mute.time<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Durata totale report**<br/> NameMute </li> <li> **Context**<br/> Data.media.States.mute.time<br/> </li> <li> **Data**<br/> Feedvideo statemutetime </li> <li> **Audience**<br/> Manager_contextdata.media.States.mute.time </li> </ul> |


### Proprietà immagine


#### Streams interessati da Picture in Picture

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di flussi interessati da Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato immagine nell&#39;immagine. <br/> **** <br/> ImportanteSe questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.pictureinpicture.set<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Report**<br/> NameStreams interessati da Picture in Picture </li> <li> **Context**<br/> Data.media.States.pictureinpicture.set<br/> </li> <li> **Data**<br/> Feedvideostatepictureinpicture </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.pictureinpicture.set </li> </ul> |


#### Conteggio immagini

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di volte in cui è stato visualizzato Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato immagine nell&#39;immagine. <br/> **** <br/> ImportanteSe questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.pictureinpicture.count<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Rapporto**<br/> NomeImmagine nell&#39;immagine </li> <li> **Context**<br/> Data.media.States.pictureinpicture.count<br/> </li> <li> **Data**<br/> Feedvideostatepictureinpicturecount </li> <li> **Audience**<br/> Manager_contextdata.media.States.pictureinpicture.count </li> </ul> |


#### Durata totale immagine

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneLa durata della visualizzazione Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato immagine nell&#39;immagine. <br/> **** <br/> ImportanteSe questo evento è impostato, l&#39;ora è uguale a quanto tempo il video era nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.pictureinpicture.time<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Durata totale rapporto**<br/> NomeImmagine nell&#39;immagine </li> <li> **Context**<br/> Data.media.States.pictureinpicture.time<br/> </li> <li> **Data**<br/> Feedvideostatepictureinpicturetime </li> <li> **Audience**<br/> Manager_contextdata.media.States.pictureinpicture.time </li> </ul> |


### In Proprietà dello stato attivo

#### Streams interessati da In Focus

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di flussi interessati da In Focus. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno Stato attivo. <br/> **** <br/> ImportanteSe questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.infocus.set<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Report**<br/> NameStreams interessati da In Focus </li> <li> **Context**<br/> Data.media.States.infocus.set<br/> </li> <li> **Data**<br/> Feedvideostateinfocus </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.infocus.set </li> </ul> |


#### Conteggi in focus

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl numero di volte in cui è stato visualizzato In focus. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno Stato attivo. <br/> ****<br/>  ImportanteSe questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato In focus. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.infocus.count<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Conteggio**<br/> del focus del nome del report </li> <li> **Context**<br/> Data.media.States.infocus.count<br/> </li> <li> **Data**<br/> Feedvideostateinfocuscount </li> <li> **Audience**<br/> Manager_contextdata.media.States.infocus.count </li> </ul> |


#### Durata totale messa a fuoco

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Impostazione automatica**<br/> chiave SDK  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> ObbligatorioNo </li> <li> ****<br/> Numero di serie </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min SDK versione**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneIl periodo di tempo in focus visualizzato. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno Stato attivo. <br/> **** <br/> ImportanteSe questo evento è impostato, l&#39;ora è uguale a quanto tempo il video era nello stato In focus. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.infocus.time<br/></li> <li> ****<br/> HeartbeatN/D </li> </ul> | <ul> <li> ****<br/> DisponibileSì </li> <li> **Riservato**<br/> Variableevent </li> <li> **Durata totale del report**<br/> NameIn Focus </li> <li> **Context**<br/> Data.media.States.infocus.time<br/> </li> <li> **Data**<br/> Feedvideostateinfocustomime </li> <li> **Audience**<br/> Manager_contextdata.media.States.infocus.time </li> </ul> |

## Elenco delle proprietà per le identità XDM

I dati memorizzati in Analytics possono essere utilizzati per qualsiasi scopo e le metriche dello stato del lettore possono essere importate in Adobe Experience Platform utilizzando XDM e utilizzate con il Customer Journey Analytics.

| Proprietà dello stato del lettore | Mappatura |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## API correlate {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
