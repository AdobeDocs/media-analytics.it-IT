---
title: Configurare il reporting per le implementazioni di Edge
description: Configura Customer Journey Analytics per generare rapporti sui dati multimediali in streaming raccolti tramite Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 7%

---

# Configurare il reporting per le implementazioni di Edge

Dopo aver implementato Streaming Media Collection tramite Edge Network, configura Customer Journey Analytics per creare rapporti sui dati raccolti.

>[!NOTE]
>
>Questa pagina descrive i rapporti in Customer Journey Analytics, la destinazione consigliata per le implementazioni di Edge. Se invece il tuo stream di dati invia dati multimediali in streaming ad Adobe Analytics, consulta [Configurare la generazione di rapporti per le implementazioni basate solo su Analytics](analytics-reporting.md).

* **Prerequisiti**: completa un&#39;implementazione di Edge e raccogli alcuni dati. Consulta la [Panoramica sull&#39;implementazione di Edge](/help/implementation/edge/overview.md) e il metodo di implementazione scelto.

## Creare una connessione in Customer Journey Analytics

1. In Customer Journey Analytics creare una connessione come descritto in [Creare una connessione](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-connections/create-connection). Durante la creazione della connessione, verificare che la casella di controllo **[!UICONTROL Import all new data]** sia abilitata.

## Creare una visualizzazione dati in Customer Journey Analytics

1. In Customer Journey Analytics creare una visualizzazione dati come descritto in [Creare o modificare una visualizzazione dati](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-dataviews/create-dataview).

   1. Nel campo **[!UICONTROL Connection]** selezionare la connessione creata in precedenza. La visualizzazione delle nuove connessioni può richiedere fino a 15 minuti.

   1. Nella scheda **[!UICONTROL Components]**, nella sezione **[!UICONTROL Schema fields]**, cerca ogni componente della tabella seguente e trascinalo nel pannello **[!UICONTROL Dimensions]** o **[!UICONTROL Metrics]** appropriato. Se esistono più campi con lo stesso nome, utilizza il percorso XDM per confermare il campo corretto. Applicare l&#39;etichetta di contesto visualizzata nell&#39;elenco a discesa **[!UICONTROL Context labels]** nelle impostazioni del componente.

      | Componente | Tipo | Percorso XDM | Etichetta contesto |
      |---|---|---|---|
      | [Contenuto](/help/reporting/dimensions/content.md) | Dimensione | `mediaReporting.sessionDetails.name` | Media: ID contenuto |
      | [Nome contenuto](/help/reporting/dimensions/content-name.md) | Dimensione | `mediaReporting.sessionDetails.friendlyName` | Media: nome video |
      | [Lunghezza contenuto](/help/reporting/dimensions/content-length.md) | Dimensione | `mediaReporting.sessionDetails.length` | Media: lunghezza video |
      | [Mostra](/help/reporting/dimensions/show.md) | Dimensione | `mediaReporting.sessionDetails.show` | Contenuti multimediali: Mostra |
      | [Stagione](/help/reporting/dimensions/season.md) | Dimensione | `mediaReporting.sessionDetails.season` | Media: Season |
      | [Episodio](/help/reporting/dimensions/episode.md) | Dimensione | `mediaReporting.sessionDetails.episode` | Media: Episodio |
      | Tipo di evento | Dimensione | `eventType` | Media: tipo evento |
      | [Tempo di contenuto trascorso](/help/reporting/metrics/content-time-spent.md) | Metrica | `mediaReporting.sessionDetails.timePlayed` | Media: tempo trascorso sui contenuti |
      | [Tempo trascorso per contenuti multimediali](/help/reporting/metrics/media-time-spent.md) | Metrica | `mediaReporting.sessionDetails.totalTimePlayed` | Media: tempo trascorso contenuti multimediali |
      | [Durata totale pausa](/help/reporting/metrics/total-pause-duration.md) | Metrica | `mediaReporting.sessionDetails.pauseTime` | Media: durata totale pausa |
      | [Ora di inizio](/help/reporting/metrics/time-to-start.md) | Metrica | `mediaReporting.qoeDataDetails.timeToStart` | Media: ora di inizio |
      | [Durata totale buffer](/help/reporting/metrics/total-buffer-duration.md) | Metrica | `mediaReporting.qoeDataDetails.bufferTime` | Media: durata totale buffer |
      | Timeout del server della sessione multimediale | Metrica | `mediaReporting.sessionDetails.secondsSinceLastCall` | Media: secondi dall’ultima chiamata |

      >[!IMPORTANT]
      >
      >Le etichette di contesto in questa tabella sono necessarie per il funzionamento dei pannelli per contenuti multimediali in streaming. Customer Journey Analytics li utilizza per calcolare automaticamente le metriche derivate da **Visualizzatori simultanei** e **Tempo di riproduzione trascorso** (utilizzate dai pannelli [Visualizzatori simultanei di contenuti multimediali](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) e [Tempo di riproduzione trascorso](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)) e per popolare le opzioni di reporting nel pannello [Pubblico medio per minuto dei contenuti multimediali](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel).

      A questo punto puoi aggiungere altre [dimensioni](/help/reporting/dimensions/overview.md) o [metriche](/help/reporting/metrics/overview.md) alla visualizzazione dati. Ogni pagina elenca il percorso XDM per quel componente.

1. Seleziona **[!UICONTROL Save and continue]** → **[!UICONTROL Save and finish]** per salvare le modifiche.

## Creare e configurare un progetto in Customer Journey Analytics

1. In Customer Journey Analytics, nella scheda **[!UICONTROL Workspace]**, nell&#39;area **[!UICONTROL Projects]**, selezionare **[!UICONTROL Create project]**.

1. Selezionare **[!UICONTROL Blank project]** → **[!UICONTROL Create]**.

1. Nel nuovo progetto, seleziona la visualizzazione dati creata in precedenza.

   Quando crei i pannelli nel progetto, puoi utilizzare tutti i componenti aggiunti alla visualizzazione dati.

1. Seleziona l&#39;icona **Panels** nella barra a sinistra, quindi trascina i pannelli **[!UICONTROL Media average minute audience]**, **[!UICONTROL Media concurrent viewers]** e **[!UICONTROL Media playback time spent]**.

1. (Condizionale) Se hai aggiunto metadati personalizzati allo schema, imposta la persistenza per i campi personalizzati, come descritto in [Impostazioni dei componenti di persistenza](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) nella guida di Customer Journey Analytics.

1. Condividi il progetto come descritto in [Condividi progetti](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=it).

   >[!NOTE]
   >
   >Se gli utenti con cui desideri condividere il file non sono disponibili, assicurati che abbiano accesso come utenti e amministratori a Customer Journey Analytics da Adobe Admin Console.

## Pannelli multimediali disponibili in Customer Journey Analytics

Analysis Workspace in Customer Journey Analytics include tre pannelli multimediali dedicati per i clienti con il componente aggiuntivo Streaming Media Collection. Questi pannelli forniscono visualizzazioni predefinite per le esigenze di reporting di contenuti multimediali in streaming più comuni.

* **[Pubblico medio per minuto](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**: confronta il consumo medio di contenuto tra programmi di qualsiasi durata o genere. Supporta sia le modalità di contenuto specifico (basato sulla durata) che le modalità di periodo di tempo personalizzate e consente di aggiornare le classificazioni di durata dopo il fatto.
* **[Visualizzatori simultanei di contenuti multimediali](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**: analizza i visualizzatori simultanei nel tempo per identificare i picchi di concorrenza e i punti di rilascio. Supporta granularità configurabile e suddivisione per serie per segmenti, dimensioni o intervalli di date.
* **[Tempo di riproduzione dei contenuti multimediali trascorso](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**: analizza la durata della riproduzione nel tempo con dettagli sui periodi di picco e minimo. Supporta granularità e formato di output configurabili (ore o minuti).

>[!MORELIKETHIS]
>
>* [Panoramica delle dimensioni](/help/reporting/dimensions/overview.md)
>* [Panoramica delle metriche](/help/reporting/metrics/overview.md)
