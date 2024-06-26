---
title: Implementare il componente aggiuntivo Streaming Media Collection utilizzando l’Edge Network
description: Scopri come implementare il componente aggiuntivo Streaming Media Collection con Experience Platform Edge.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 6%

---

# Implementare il componente aggiuntivo Streaming Media Collection utilizzando l’Edge Network

La rete Edge di Adobe Experience Platform consente di inviare dati destinati a più prodotti a una posizione centralizzata. Experience Edge inoltra le informazioni appropriate ai prodotti desiderati. Questo concetto consente di consolidare le attività di implementazione, in particolare per quanto riguarda più soluzioni di dati.

L’immagine seguente illustra come implementare il componente aggiuntivo Adobe Streaming Media Collection per utilizzare Experience Platform Edge per rendere i dati disponibili in Analysis Workspace, in Adobe Analytics o Customer Journey Analytics:

![Flusso di lavoro in CJA](assets/streaming-media-edge.png)

Per una panoramica di tutte le opzioni di implementazione, inclusi i metodi di implementazione che non utilizzano Experience Platform Edge, vedi [Implementare il componente aggiuntivo Streaming Media Collection](/help/implementation/overview.md).

Indipendentemente dal fatto che si utilizzi Adobe Experience Platform Web SDK, Adobe Experience Platform Mobile SDK, Adobe Experience Platform Roku SDK o l’API per implementare il componente aggiuntivo Streaming Media Collection con Experience Edge, è necessario prima completare le sezioni seguenti:

## Configurare lo schema in Adobe Experience Platform

Per standardizzare la raccolta dati da utilizzare nelle applicazioni che sfruttano Adobe Experience Platform, Adobe ha creato lo standard aperto e pubblicamente documentato Experience Data Model (XDM).

Per creare e impostare uno schema:

1. In Adobe Experience Platform, inizia a creare lo schema come descritto in [Creare e modificare gli schemi nell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

1. Nella pagina Dettagli schema, durante la creazione dello schema, scegli [!UICONTROL **Evento esperienza**] quando si sceglie la classe base per lo schema.

   ![Gruppi di campi aggiunti](assets/schema-experience-event.png)

1. Seleziona [!UICONTROL **Successivo**].

1. Specifica un nome e una descrizione da visualizzare per lo schema, quindi seleziona [!UICONTROL **Fine**].

1. In [!UICONTROL **Composizione**] area, nel [!UICONTROL **Gruppi di campi**] sezione, seleziona [!UICONTROL **Aggiungi**], quindi cerca e aggiungi i seguenti nuovi gruppi di campi allo schema:
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Dopo aver aggiunto i gruppi di campi, questi devono essere visualizzati nel [!UICONTROL **Gruppi di campi**] sezione, come segue:

   ![Gruppi di campi aggiunti](assets/schema-field-groups-added.png)

1. Seleziona [!UICONTROL **Salva**] per salvare le modifiche.

1. (Facoltativo) Puoi nascondere alcuni campi non utilizzati dall’API di Media Edge. Nascondere questi campi semplifica la lettura e la comprensione dello schema, ma non è obbligatorio. Questi campi si riferiscono solo a quelli `MediaAnalytics Interaction Details` gruppo di campi.

+++ Espandi qui per visualizzare le istruzioni sui campi che puoi nascondere.

   1. In [!UICONTROL **Struttura**] , selezionare la `Media Collection Details` , quindi seleziona [!UICONTROL **Gestire i campi correlati**].

      ![manage-related-fields](assets/manage-related-fields.png)

   1. Abilita l’opzione per [!UICONTROL **Mostra nomi visualizzati per i campi**], quindi aggiorna lo schema come segue:

      * In `Media Collection Details` > `Advertising Details` , nascondi i seguenti campi di reporting: `Ad Completed`, `Ad Started`, e `Ad Time Played`.

      * In `Media Collection Details` > `Advertising Pod Details` , nascondi il seguente campo di reporting: `Ad Break ID`

      * In `Media Collection Details` > `Chapter Details` , nascondi i seguenti campi di reporting: `Chapter Completed`, `Chapter ID`, `Chapter Started`, e `Chapter Time Played`.

      * In `Media Collection Details` , nascondere il `List Of States` campo.

        ![nascondi stati raccolta file multimediali](assets/schema-hide-media-collection-states.png)

      * In `Media Collection Details` > `List Of States End` e `Media Collection Details` > `List Of States Start` , nascondi i seguenti campi di reporting: `Player State Count`, `Player State Set`, e `Player State Time`.

        ![campi da nascondere](assets/schema-hide-listofstates.png)

      * In `Media Collection Details` > `Qoe Data Details` , nascondi i seguenti campi di reporting: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration`, e `Total Stalling Duration`.

      * In `Media Collection Details` > `Session Details` , nascondi i seguenti campi di reporting: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played`, e `Video Segment`.

   1. Seleziona [!UICONTROL **Conferma**] per salvare le modifiche.

   1. In [!UICONTROL **Struttura**] , abilita l’opzione per [!UICONTROL **Mostra nomi visualizzati per i campi**], quindi seleziona la `List Of Media Collection Downloaded Content Events` campo.

   1. Seleziona [!UICONTROL **Gestire i campi correlati**], quindi aggiorna lo schema come segue:


      * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` , nascondi i seguenti campi di reporting: `Ad Completed`, `Ad Started`, e `Ad Time Played`.

      * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` , nascondi il seguente campo di reporting: `Ad Break ID`

      * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` , nascondi i seguenti campi di reporting: `Chapter Completed`, `Chapter ID`, `Chapter Started`, e `Chapter Time Played`.

      * In `List Of Media Collection Downloaded Content Events` > `Media Details` , nascondere il `List Of States` campo.

      * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` e `Media Collection Details` > `List Of States Start` , nascondi i seguenti campi di reporting: `Player State Count`, `Player State Set`, e `Player State Time`.

      * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` , nascondi i seguenti campi di reporting: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration`, e `Total Stalling Duration`.

      * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` , nascondi i seguenti campi di reporting: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played`, e `Video Segment`.

      * In `List Of Media Collection Downloaded Content Events` > `Media Details`  , nascondere il `Media Session ID` campo.

   1. Seleziona [!UICONTROL **Conferma**] per salvare le modifiche.

   1. In [!UICONTROL **Struttura**] , selezionare la `Media Reporting Details` campo, seleziona [!UICONTROL **Gestire i campi correlati**].

   1. Abilita l’opzione per [!UICONTROL **Mostra nomi visualizzati per i campi**], quindi aggiorna lo schema come segue:

      * In `Media Reporting Details` , nascondere i campi seguenti: `Error Details`, `List Of States End`, `List of States Start`, e `Media Session ID`.

   1. Seleziona [!UICONTROL **Conferma**] > [!UICONTROL **Salva**]  per salvare le modifiche.

1. Continua con [Creare un set di dati in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

## Creare un set di dati in Adobe Experience Platform

1. Assicurati di impostare uno schema come descritto in [Configurare lo schema in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. In Adobe Experience Platform, inizia a creare il set di dati come descritto in [Guida all’interfaccia utente dei set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=it#create).

   Quando selezioni uno schema per il set di dati, scegli lo schema creato in precedenza, come descritto in [Configurare lo schema in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Continua con [Configurare uno stream di dati nel Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

## Configurare uno stream di dati in Adobe Experience Platform

1. Assicurati di aver creato un set di dati come descritto in [Creare un set di dati in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

1. Creare un nuovo stream di dati come descritto in [Configurare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en).

   Durante la creazione dello stream di dati, accertati di effettuare le seguenti selezioni di configurazione:

   * In [!UICONTROL **Schema Evento**] durante la creazione dello stream di dati, accertati di selezionare lo schema creato in [Configurare lo schema in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform). Seleziona [!UICONTROL **Salva**].

     >[!IMPORTANT]
     >
         > Non selezionare [!UICONTROL **Save and Add Mapping**] perché così facendo si verificheranno errori di mappatura per il campo Timestamp.
     
     ![Crea uno stream di dati e seleziona uno schema](assets/datastream-create-schema.png)

   * Aggiungi uno dei seguenti servizi al flusso di dati, a seconda che si stia utilizzando Adobe Analytics o Customer Journey Analytics:

      * [!UICONTROL **Adobe Analytics**] (se utilizzi Adobe Analytics)

        Se utilizzi Adobe Analytics, accertati di definire una suite di rapporti come descritto in [Creare una suite di rapporti](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

      * [!UICONTROL **Adobe Experience Platform**] (se si utilizza Customer Journey Analytics)

     Per informazioni su come aggiungere un servizio a un flusso di dati, consulta la sezione &quot;Aggiungere servizi a un flusso di dati&quot; in [Configurare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![Aggiungere il servizio Adobe Analytics](assets/datastream-add-service.png)

   * Espandi [!UICONTROL **Opzioni avanzate**], quindi attiva [!UICONTROL **Media Analytics**] opzione.

     ![Opzione Media Analytics](assets/datastream-media-check.png)

1. Ora puoi implementare [API di Media Edge](/help/implementation/edge/implementation-edge-api.md) o [SDK di Media Edge](/help/implementation/edge/edge-mobile-sdk.md) per iniziare a raccogliere i dati di media analytics.

   Dopo aver raccolto alcuni dati, puoi [Crea una connessione nel Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

## Creare una connessione in Customer Journey Analytics

>[!NOTE]
>
>La procedura seguente è necessaria solo se si utilizza Customer Journey Analytics.


1. Assicurati di aver creato un flusso di dati come descritto in [Configurare uno stream di dati nel Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

1. In Customer Journey Analytics, creare una connessione come descritto in [Creare una connessione](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=it).

   Durante la creazione della connessione, per l’implementazione del componente aggiuntivo Streaming Media Collection sono necessarie le seguenti selezioni di configurazione:

   1. Seleziona il set di dati creato in precedenza, come descritto in [Creare un set di dati in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

   1. Assicurati che [!UICONTROL **Importa tutti i nuovi dati**] è attivata.

1. Continua con [Creazione di una visualizzazione dati nel Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

## Creazione di una visualizzazione dati nel Customer Journey Analytics

>[!NOTE]
>
>La procedura seguente è necessaria solo se si utilizza Customer Journey Analytics.

1. Assicurarsi di aver creato una connessione nel Customer Journey Analytics come descritto in [Crea una connessione nel Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

1. In Analisi del Percorso di clienti, crea una visualizzazione dati come descritto in [Creare o modificare una visualizzazione dati](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=it).

   Durante la creazione della visualizzazione dati, per implementare il componente aggiuntivo Streaming Media Collection sono necessarie le seguenti selezioni di configurazione:

   1. In [!UICONTROL **Connessione**] selezionare la connessione creata in precedenza, come descritto in [Crea una connessione nel Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

      La selezione della connessione creata può richiedere fino a 15 minuti.

   1. Il giorno [!UICONTROL **Componenti**] , nella scheda [!UICONTROL **Campi schema**] , cerca ogni componente elencato nelle tabelle seguenti e trascinalo nella sezione [!UICONTROL **Metriche**] pannello. Se esistono più campi con lo stesso nome, utilizza il percorso XDM per assicurarti che sia il campo corretto.

      **Contenuto principale - Metriche del contenuto**

      | Nome componente | Percorso XDM |
      |----------|---------|
      | Avvio file multimediale | mediaReporting.sessionDetails.isViewed |
      | Visualizzazioni segmento multimediale | mediaReporting.sessionDetails.hasSegmentView |
      | Avvio contenuti | mediaReporting.sessionDetails.isPlayed |
      | Completamenti contenuto | mediaReporting.sessionDetails.isCompleted |
      | Tempo trascorso dei contenuti | mediaReporting.sessionDetails.timePlayed |
      | Tempo trascorso dei contenuti multimediali | mediaReporting.sessionDetails.totalTimePlayed |
      | Tempo specifico riprodotto | mediaReporting.sessionDetails.uniqueTimePlayed |
      | Marcatore progresso 10% | mediaReporting.sessionDetails.hasProgress10 |
      | Pubblico medio per minuto | mediaReporting.sessionDetails.averageMinuteAudience |


      **Capitolo e annunci - Metriche Capitolo e annunci**

      | Nome componente | Percorso XDM |
      |----------|---------|
      | Capitolo avviato | mediaReporting.chapterDetails.isStarted |
      | Capitolo completato | mediaReporting.chapterDetails.isCompleted |
      | Tempo capitolo riprodotto | mediaReporting.chapterDetails.timePlayed |
      | Annuncio avviato | mediaReporting.advertisingDetails.isStarted |
      | Annuncio completato | mediaReporting.advertisingDetails.isCompleted |
      | Tempo di riproduzione dell’annuncio | mediaReporting.advertisingDetails.timePlayed |


      **QoE - Metriche QoE**

      | Nome componente | Percorso XDM |
      |----------|---------|
      | Ora di inizio | mediaReporting.qoeDataDetails.timeToStart |
      | Perdite prima degli inizi | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | Flussi interessati dal buffer | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | Flussi interessati dalla modifica del bitrate | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | Modifiche bitrate | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | Bitrate medio | mediaReporting.qoeDataDetails.bitrateAverage |
      | Frame rilasciati | mediaReporting.qoeDataDetails.droppedFrames |
      | Errori | mediaReporting.qoeDataDetails.errorCount |
      | Flussi interessati dall’errore | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | Flussi interessati da fotogrammi saltati | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |


      **Stato del lettore - Metriche dello stato del lettore**

      | Nome componente | Percorso XDM |
      |----------|---------|
      | Stato del lettore impostato | mediaReporting.states.isSet |
      | Conteggio dello stato del lettore | mediaReporting.states.count |
      | Ora stato lettore | mediaReporting.states.time |


   1. Aggiornare le etichette (in [!UICONTROL **Etichette di contesto**] menu a discesa) per i componenti nella tabella seguente. Cerca e trascina nel pannello i componenti che non sono già presenti nel pannello metriche.

      | Nome componente | Etichetta contesto |
      |---------|----------|
      | Timeout del server della sessione multimediale | Media: secondi dall’ultima chiamata |
      | Tempo trascorso dei contenuti multimediali | Media: tempo trascorso contenuti multimediali |
      | Durata totale buffer | Media: durata totale buffer |
      | Tempo di avvio | Media: tempo di avvio |
      | Durata totale pausa | Media: durata totale pausa |

   1. Per aggiungere suddivisioni al progetto di Customer Journey Analytics, aggiungi le dimensioni seguenti alla sezione [!UICONTROL **Dimension**] pannello:

      | Percorso XDM | Nome componente |
      |---------|----------|
      | mediaReporting.states.name | Nome stato lettore |
      | mediaReporting.sessionDetails.ID | ID sessione multimediale |

      Oltre alle dimensioni in questa tabella, puoi aggiungere qualsiasi altra dimensione che desideri rendere disponibile per filtrare i dati per nei progetti di Customer Journey Analytics.

1. Seleziona [!UICONTROL **Salva e continua**] > [!UICONTROL **Salva e termina**] per salvare le modifiche.

1. Continua con [Creazione e configurazione di un progetto nel Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Creazione e configurazione di un progetto nel Customer Journey Analytics

1. Assicurati di aver creato una visualizzazione dati nel Customer Journey Analytics come descritto in [Creazione di una visualizzazione dati nel Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

1. Nel Customer Journey Analytics, nel [!UICONTROL **Workspace**] , nella scheda [!UICONTROL **Progetti**] area, seleziona [!UICONTROL **Crea progetto**].

1. Seleziona [!UICONTROL **Progetto vuoto**] > [!UICONTROL **Crea**].

1. Nel nuovo progetto, seleziona la visualizzazione dati creata in precedenza.

   Quando crei i pannelli nel progetto, puoi utilizzare tutti i componenti aggiunti alla visualizzazione dati, come descritto in [Creazione di una visualizzazione dati nel Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

   I seguenti 4 pannelli sono esempi di pannelli che puoi creare:

   ![Pannello Contenuto principale](assets/main-content-panel.png)

   ![Pannello Capitolo e annunci](assets/chapter-and-ads-panel.png)

   ![Pannello QoE](assets/qoe-panel.png)

   ![Pannello Stato del piatto](assets/player-state-panel.png)

1. Seleziona la **Pannelli** nella barra a sinistra, quindi trascina [!UICONTROL **Visualizzatori simultanei contenuti multimediali**] e [!UICONTROL **Tempo di riproduzione dei contenuti multimediali trascorso**] pannello.

   I 2 pannelli dovrebbero essere simili al seguente:

   ![Pannello Visualizzatori simultanei di contenuti multimediali](assets/media-concurrent-viewers-panels.png)

   ![Pannello Tempo di riproduzione dei contenuti multimediali](assets/media-playback-time-spent-panels.png)

1. Condividere il progetto come descritto in [Condividere progetti](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   Se gli utenti con cui desideri condividere il file non sono disponibili, assicurati che gli utenti abbiano accesso come utente e amministratore al Customer Journey Analytics in Adobe Admin Console.

1. Continua con [Inviare dati ad Experience Platform Edge](#send-data-to-experience-platform-edge).

## Inviare dati ad Experience Platform Edge

A seconda del tipo di dati che desideri inviare ad Experience Platform Edge, puoi utilizzare uno dei seguenti metodi:

### Web: utilizzare Adobe Experience Platform Web SDK

* [Introduzione](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Inviare dati web ad Edge con Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)

* [Migrare ad Adobe Streaming Media per estensione Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Mobile: utilizzare Adobe Experience Platform Mobile SDK

Utilizza le seguenti risorse di documentazione per completare l’implementazione sia per iOS che per Android:

* [Introduzione](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Riferimento API](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Migrare ad Adobe Streaming Media per estensione Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku: SDK per Adobe Experience Platform Roku

* [Introduzione](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [SDK di Adobe Experience Platform Roku](https://github.com/adobe/aepsdk-roku/tree/main)

* [Migrare ad Adobe Streaming Media per estensione Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API: Web e altro

L’API è attualmente l’unico modo supportato per inviare dati web ad Experience Platform Edge.

L’API è disponibile anche se desideri utilizzare un’implementazione personalizzata delle API di Edge.

Per ulteriori informazioni sull’API di Media Edge, consulta le risorse seguenti:

* [Panoramica API di Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Guida introduttiva all’API di Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Guida alla risoluzione dei problemi API di Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Utilizzo del file delle specifiche API Open per le API di Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)
