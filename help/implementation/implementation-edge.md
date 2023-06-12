---
title: Primi passaggi nella configurazione di un’implementazione per Analytics per contenuti in streaming
description: Scopri come implementare Adobe Streaming Media.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 29d58b41-9a49-4b71-bdc5-4e2848cd3236
source-git-commit: e3380ad898b551b6e0bbf5624d8419c5a95496f6
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 7%

---

# Installare Media Analytics con Experience Platform Edge

Adobe Experience Platform Edge consente di inviare dati destinati a più prodotti a una posizione centralizzata. Experience Edge inoltra le informazioni appropriate ai prodotti desiderati. Questo concetto consente di consolidare le attività di implementazione, in particolare per quanto riguarda più soluzioni di dati.

L’immagine seguente illustra un’implementazione di Media Analytics che utilizza Experience Platform Edge:

![Implementazione Edge](assets/media-analytics-implementation-overview.png)

>[!IMPORTANT]
>
>Attualmente, puoi inviare dati a Experience Edge solo utilizzando l’SDK di Adobe Experience Platform Mobile.


<!-- Replace the above sentence with this after it web releases: You can send data to Experience Edge using any of the following implementation methods:

* Adobe Experience Platform Web SDK (Coming soon)
* Adobe Experience Platform Mobile SDK
* Edge Network Server API

Regardless of which Experience Edge implementation method you use for configuring media tracking, you must first complete the following sections:

-->

Completa le sezioni seguenti per implementare Media Analytics con Experience Platform Edge:

* [Definire una suite di rapporti](#define-a-report-suite)
* [Configurare lo schema in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform)
* [Creare un set di dati in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform)
* [Configurare uno stream di dati in Adobe Experience Platform](#configure-a-datastream-in-adobe-experience-platform)
* [Creare una connessione in Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics)
* [Creazione di una visualizzazione dati nel Customer Journey Analytics](#create-a-data-view-in-customer-journey-analytics)
* [Creazione e configurazione di un progetto nel Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics)
* [Inviare dati ad Experience Platform Edge con l’estensione Edge](#send-data-to-experience-platform-edge-with-the-edge-extension)

## Definire una suite di rapporti

>[!NOTE]
>
>Una suite di rapporti è necessaria solo se utilizzi Adobe Analytics. Una suite di rapporti non è necessaria se intendi utilizzare il Customer Journey Analytics per i rapporti.

Se prevedi di utilizzare Adobe Analytics per il reporting, devi disporre di una suite di rapporti da utilizzare con l’implementazione di Streaming Media. Per informazioni sulla definizione di una suite di rapporti, consulta [Report Suite Manager](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html?lang=en).

Dopo aver definito una suite di rapporti, continua con [Configurare lo schema in Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

## Configurare lo schema in Adobe Experience Platform

Per standardizzare la raccolta dati da utilizzare nelle applicazioni che sfruttano Adobe Experience Platform, Adobe ha creato lo standard aperto e pubblicamente documentato Experience Data Model (XDM).

Per creare e impostare uno schema:

1. In Adobe Experience Platform, inizia a creare lo schema come descritto in [Creare e modificare gli schemi nell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   Durante la creazione dello schema, scegli [!UICONTROL **XDM ExperienceEvent**] dal [!UICONTROL **Crea schema**] menu a discesa.

1. In [!UICONTROL **Composizione**] area, nel [!UICONTROL **Gruppi di campi**] sezione, seleziona [!UICONTROL **Aggiungi**], quindi cerca e aggiungi i seguenti nuovi gruppi di campi allo schema:
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Dopo aver aggiunto i gruppi di campi, questi devono essere visualizzati nel [!UICONTROL **Gruppi di campi**] sezione, come segue:

   ![Gruppi di campi aggiunti](assets/schema-field-groups-added.png)

1. In [!UICONTROL **Struttura**] , selezionare la `endUserIds` > `_experience` gruppo di campi, quindi seleziona [!UICONTROL **Gestire i campi correlati**].

   ![Pulsante Gestisci campi correlati](assets/manage-related-fields.png)

1. Aggiorna lo schema come segue:

   * In `Adobe Analytics ExperienceEvent Template` gruppo di campi, nascondi tutti i campi tranne `EndUserIDs`.

   * In `endUserIds` > `_experience` > `Adobe Advertising Cloud end user IDs` gruppo di campi, nasconde tutti i campi tranne `Identifier` campo.

   * In `endUserIds` > `_experience` > `Adobe Analytics Cloud Custom end user IDs` gruppo di campi, nasconde tutti i campi tranne `Identifier` campo.

     ![campi da nascondere](assets/schema-hide-fields.png)

1. Seleziona [!UICONTROL **Conferma**] per salvare le modifiche.

1. In [!UICONTROL **Struttura**] , selezionare la `Implementation Details` gruppo di campi, seleziona [!UICONTROL **Gestire i campi correlati**], quindi aggiorna lo schema come segue:

   * In `Implementation Details` > `Implementation details` gruppo di campi, nascondi tutti i campi tranne `version`.

     ![campi da nascondere](assets/schema-hide-fields2.png)

1. Seleziona [!UICONTROL **Conferma**] per salvare le modifiche.

1. In [!UICONTROL **Struttura**] , selezionare la `Media Collection Details` gruppo di campi, seleziona [!UICONTROL **Gestire i campi correlati**], quindi aggiorna lo schema come segue:

   * In `Media Collection Details` gruppo di campi, nascondere `List Of States` gruppo di campi.

     ![nascondi stati raccolta file multimediali](assets/schema-hide-media-collection-states.png)

   * In `Media Collection Details` > `Advertising Details` gruppo di campi, nascondi i campi di reporting seguenti: `Ad Completed`, `Ad Started`, e `Ad Time Played`.

   * In `Media Collection Details` > `Advertising Pod Details` gruppo di campi, nascondi il seguente campo di reporting: `Ad Break ID`

   * In `Media Collection Details` > `Chapter Details` gruppo di campi, nascondi i seguenti campi di reporting: `Chapter ID`, `Chapter Completed`, `Chapter Started`, e `Chapter Time Played`.

   * In `Media Collection Details` > `Qoe Data Details` gruppo di campi, nascondi i seguenti campi di reporting: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, e `Total Stalling Duration`.

   * In `Media Collection Details` > `Session Details` gruppo di campi, nascondi i seguenti campi di reporting: `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`, e `Pccr`.

   * In `Media Collection Details` > `List Of States End` e `Media Collection Details` > `List Of States Start` gruppi di campi, nascondi i seguenti campi di reporting: `Player State Count`, `Player State Set`, e `Player State Time`.

     ![campi da nascondere](assets/schema-hide-listofstates.png)

1. Seleziona [!UICONTROL **Conferma**] per salvare le modifiche.

1. In [!UICONTROL **Struttura**] , selezionare la `List Of Media Collection Downloaded Content Events` gruppo di campi, seleziona [!UICONTROL **Gestire i campi correlati**], quindi aggiorna lo schema come segue:

   * In `List Of Media Collection Downloaded Content Events` > `Media Details` gruppo di campi, nascondere `List Of States` gruppo di campi.

   * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` gruppo di campi, nascondi i campi di reporting seguenti: `Ad Completed`, `Ad Started`, e `Ad Time Played`.

   * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` gruppo di campi, nascondi il seguente campo di reporting: `Ad Break ID`

   * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` gruppo di campi, nascondi i seguenti campi di reporting: `Chapter ID`, `Chapter Completed`, `Chapter Started`, e `Chapter Time Played`.

   * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` gruppo di campi, nascondi i seguenti campi di reporting: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, e `Total Stalling Duration`.

   * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` gruppo di campi, nascondi i seguenti campi di reporting: `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`, e `Pccr`.

   * In `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` e `Media Collection Details` > `List Of States Start` gruppi di campi, nascondi i seguenti campi di reporting: `Player State Count`, `Player State Set`, e `Player State Time`.

   * In `List Of Media Collection Downloaded Content Events` > `Media Details`  gruppo di campi, nascondere `Media Session ID` campo.

1. Seleziona [!UICONTROL **Conferma**] per salvare le modifiche.

1. In [!UICONTROL **Struttura**] , selezionare la `Media Reporting Details` gruppo di campi, seleziona [!UICONTROL **Gestire i campi correlati**], quindi aggiorna lo schema come segue:

   * In `Media Reporting Details` gruppo di campi, nascondere i seguenti gruppi di campi: `Error Details`, `List Of States End`, `List of States Start`, `Playhead`, e `Media Session ID`.

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

        Se utilizzi Adobe Analytics, accertati di definire una suite di rapporti come descritto nella sezione [Definire una suite di rapporti](#define-a-report-suite) in questo articolo.

      * [!UICONTROL **Adobe Experience Platform**] (se si utilizza Customer Journey Analytics)

     Per informazioni su come aggiungere un servizio a un flusso di dati, consulta la sezione &quot;Aggiungere servizi a un flusso di dati&quot; in [Configurare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![Aggiungere il servizio Adobe Analytics](assets/datastream-add-service.png)

   * Espandi [!UICONTROL **Opzioni avanzate**], quindi attiva [!UICONTROL **Media Analytics**] opzione.

     ![Opzione Media Analytics](assets/datastream-media-check.png)

1. Continua con [Crea una connessione nel Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

## Creare una connessione in Customer Journey Analytics

>[!NOTE]
>
>La procedura seguente è necessaria solo se si utilizza Customer Journey Analytics.


1. Assicurati di aver creato un flusso di dati come descritto in [Configurare uno stream di dati nel Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

1. In Customer Journey Analytics, creare una connessione come descritto in [Creare una connessione](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=it).

   Durante la creazione della connessione, per l’implementazione di Streaming Media sono necessarie le seguenti selezioni di configurazione:

   1. Seleziona il set di dati creato in precedenza, come descritto in [Creare un set di dati in Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

   1. Assicurati che [!UICONTROL **Importa tutti i nuovi dati**] è attivata.

1. Continua con [Creazione di una visualizzazione dati nel Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

## Creazione di una visualizzazione dati nel Customer Journey Analytics

>[!NOTE]
>
>La procedura seguente è necessaria solo se si utilizza Customer Journey Analytics.

1. Assicurarsi di aver creato una connessione nel Customer Journey Analytics come descritto in [Crea una connessione nel Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

1. In Analisi del Percorso di clienti, crea una visualizzazione dati come descritto in [Creare o modificare una visualizzazione dati](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=it).

   Durante la creazione della visualizzazione dati, per l’implementazione di Streaming Media sono necessarie le seguenti selezioni di configurazione:

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

1. Condividere il progetto come descritto in [Condividere progetti](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=it).

   >[!NOTE]
   >
   >   Se gli utenti con cui desideri condividere il file non sono disponibili, assicurati che gli utenti abbiano accesso come utente e amministratore al Customer Journey Analytics in Adobe Admin Console.

1. Continua con [Invia dati a Experience Platform Edge](#send-data-to-experience-platform-edge).

## Inviare dati ad Experience Platform Edge utilizzando l’SDK di AEP Mobile

Puoi utilizzare Adobe Experience Platform Mobile SDK per inviare dati mobili a Experience Platform Edge. In alternativa, puoi utilizzare un’implementazione personalizzata delle API Edge.<!-- I guess we don't need/want to document this? -->)

Utilizza le seguenti risorse di documentazione per completare l’implementazione sia per iOS che per Android:

* [introduzione](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Riferimento API](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Migrazione ad Adobe Streaming Media per l’estensione Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) (Per gli utenti che eseguono la migrazione dall’estensione Media a Edge)

