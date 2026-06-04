---
title: Configurare il reporting per le implementazioni di Edge
description: Configura Customer Journey Analytics per generare rapporti sui dati multimediali in streaming raccolti tramite Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 18%

---

# Configurare il reporting per le implementazioni di Edge

Dopo aver implementato Streaming Media Collection tramite Edge Network, configura Customer Journey Analytics per creare rapporti sui dati raccolti. Questa pagina descrive come creare una connessione, una visualizzazione dati e un progetto per contenuti multimediali in streaming.

>[!NOTE]
>
>Questa pagina descrive i rapporti in Customer Journey Analytics, la destinazione consigliata per le implementazioni di Edge. Se invece il tuo stream di dati invia dati multimediali in streaming ad Adobe Analytics, consulta [Configurare la generazione di rapporti per le implementazioni basate solo su Analytics](analytics-reporting.md).

* **Prerequisiti**: completa un&#39;implementazione di Edge e raccogli alcuni dati. Consulta la [Panoramica sull&#39;implementazione di Edge](/help/implementation/edge/overview.md) e il metodo di implementazione scelto.

## Creare una connessione in Customer Journey Analytics

1. In Customer Journey Analytics creare una connessione come descritto in [Creare una connessione](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=it).

   Durante la creazione della connessione, per lo streaming multimediale sono necessarie le seguenti selezioni:

   1. Seleziona il set di dati creato durante l’implementazione.

   1. Verificare che l&#39;impostazione **[!UICONTROL Import all new data]** sia abilitata.

1. Continua con [Crea una visualizzazione dati in Customer Journey Analytics](#create-a-data-view-in-customer-journey-analytics).

## Creare una visualizzazione dati in Customer Journey Analytics

1. In Customer Journey Analytics creare una visualizzazione dati come descritto in [Creare o modificare una visualizzazione dati](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=it).

   1. Nel campo **[!UICONTROL Connection]** selezionare la connessione creata in precedenza.

      La selezione di una nuova connessione può richiedere fino a 15 minuti.

   1. Nella scheda **[!UICONTROL Components]**, nella sezione **[!UICONTROL Schema fields]**, cerca ogni componente nelle tabelle seguenti e trascinalo nel pannello **[!UICONTROL Metrics]**. Se esistono più campi con lo stesso nome, utilizza il percorso XDM per confermare il campo corretto.

      **Contenuto principale - Metriche del contenuto**

      | Nome componente | Percorso XDM |
      |----------|---------|
      | Avvio file multimediale | mediaReporting.sessionDetails.isViewed |
      | Visualizzazioni segmento multimediale | mediaReporting.sessionDetails.hasSegmentView |
      | Avvio contenuti | mediaReporting.sessionDetails.isPlayed |
      | Completamenti contenuti | mediaReporting.sessionDetails.isCompleted |
      | Tempo trascorso dei contenuti | mediaReporting.sessionDetails.timePlayed |
      | Tempo trascorso dei contenuti multimediali | mediaReporting.sessionDetails.totalTimePlayed |
      | Tempo specifico riprodotto | mediaReporting.sessionDetails.uniqueTimePlayed |
      | Indicatore di avanzamento al 10% | mediaReporting.sessionDetails.hasProgress10 |
      | Pubblico medio per minuto | mediaReporting.sessionDetails.averageMinuteAudience |

      **Capitolo e annunci - Metriche capitolo e annunci**

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

   1. Aggiornare le etichette (nel menu a discesa **[!UICONTROL Context labels]**) per i componenti nella tabella seguente. Cerca e trascina nel pannello i componenti che non sono già presenti nel pannello metriche.

      | Nome componente | Etichetta contesto |
      |---------|----------|
      | Timeout del server della sessione multimediale | Media: secondi dall’ultima chiamata |
      | Tempo trascorso dei contenuti multimediali | Media: tempo trascorso contenuti multimediali |
      | Durata totale buffer | Media: durata totale buffer |
      | Tempo prima dell’inizio | Media: tempo di avvio |
      | Durata totale pausa | Media: durata totale pausa |

   1. Per aggiungere suddivisioni al progetto, aggiungi le dimensioni seguenti al pannello **[!UICONTROL Dimensions]**:

      | Percorso XDM | Nome componente |
      |---------|----------|
      | mediaReporting.states.name | Nome stato lettore |
      | mediaReporting.sessionDetails.ID | ID sessione multimediale |

      Oltre alle dimensioni in questa tabella, puoi aggiungere qualsiasi altra dimensione in base alla quale desideri filtrare i dati nei progetti.

1. Seleziona **[!UICONTROL Save and continue]** > **[!UICONTROL Save and finish]** per salvare le modifiche.

1. Continua con [Crea e configura un progetto in Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Creare e configurare un progetto in Customer Journey Analytics

1. In Customer Journey Analytics, nella scheda **[!UICONTROL Workspace]**, nell&#39;area **[!UICONTROL Projects]**, selezionare **[!UICONTROL Create project]**.

1. Seleziona **[!UICONTROL Blank project]** > **[!UICONTROL Create]**.

1. Nel nuovo progetto, seleziona la visualizzazione dati creata in precedenza.

   Quando crei i pannelli nel progetto, puoi utilizzare tutti i componenti aggiunti alla visualizzazione dati.

1. Seleziona l&#39;icona **Panels** nella barra a sinistra, quindi trascina il pannello **[!UICONTROL Media concurrent viewers]** e il pannello **[!UICONTROL Media playback time spent]**.

1. (Condizionale) Se hai aggiunto metadati personalizzati allo schema, imposta la persistenza per i campi personalizzati, come descritto in [Impostazioni dei componenti di persistenza](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) nella guida di Customer Journey Analytics.

1. Condividi il progetto come descritto in [Condividi progetti](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >Se gli utenti con cui desideri condividere il file non sono disponibili, assicurati che abbiano accesso come utenti e amministratori a Customer Journey Analytics da Adobe Admin Console.

>[!MORELIKETHIS]
>
>* [Pannelli multimediali in Workspace](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [Panoramica delle dimensioni](/help/reporting/dimensions/overview.md)
>* [Panoramica delle metriche](/help/reporting/metrics/overview.md)
