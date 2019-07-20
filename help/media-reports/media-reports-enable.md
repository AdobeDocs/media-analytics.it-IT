---
seo-title: Abilitazione dei rapporti sui file multimediali
title: Abilitazione dei rapporti sui file multimediali
uuid: d 306068 d-a 308-4 b 6 e -8 a 72-742 dda 0 de 428
translation-type: tm+mt
source-git-commit: 3fed0736b673d024b7a4b07d8324bfc62f747ed7

---


# Media reports enablement{#media-reports-enablement}

Ogni suite di rapporti che raccoglie metriche multimediali deve essere configurata prima dell'invio dei dati multimediali.

>[!TIP]
>
>Per sfruttare le nuove funzionalità, i clienti esistenti di Media Analytics devono riattivare il tracciamento dei contenuti multimediali per i loro RSIDS.

1. In [Reports &amp; Analytics](https://my.omniture.com/login/) click [!UICONTROL Admin] &gt; [!UICONTROL Report Suites].
1. Select the report suite(s) where you are collecting media data and click [!UICONTROL Edit Settings] &gt; [!UICONTROL Media Management] &gt; [!UICONTROL Media Reporting].
   ![](assets/media-reporting.png){width = "400 px"}

1. On the **[!UICONTROL Media Reporting]** page, enable **[!UICONTROL Media Core]**, and optionally enable **[!UICONTROL Media Ads]**, **[!UICONTROL Media Chapters]**, and **[!UICONTROL Media Quality]**.

   La misurazione file multimediali include i seguenti moduli:

   * **Media Core:**

      La misurazione media media viene utilizzata per i contenuti multimediali. Questo utilizzerà le evar della soluzione (o Personalizzate) per tenere traccia di Contenuto, Tipo di contenuto, Nome lettore contenuto e Canale contenuto. Gli eventi della soluzione (o Personalizzato) saranno utilizzati per gli avvii Contenuti multimediali, i contenuti, i completamenti dei contenuti e il tempo trascorso.

   * **Annunci multimediali:** La misurazione degli annunci multimediali viene utilizzata per la misurazione degli annunci nel contenuto multimediale. Questa opzione utilizza evvars della soluzione per misurare Ad, Ad Player Name, Ad Pod e Ad nella posizione del contenitore. Gli eventi della soluzione saranno utilizzati per Avvii annunci, Annunci pubblicitari, Tempo trascorso trascorso e Tempo video trascorso.
   * **Capitoli file multimediali:**

      La misurazione dei capitoli video viene utilizzata per misurare i capitoli. Un capitolo è una suddivisione di contenuto all'interno di un singolo elemento multimediale. Verrà utilizzato un evar della soluzione per memorizzare l'ID capitolo. Gli eventi della soluzione verranno utilizzati per Avvii capitolo, Completamento capitolo e Durata capitolo. I metadati capitolo aggiuntivi del Nome capitolo e della Posizione dei capitoli saranno forniti come classificazioni dell'ID capitolo.

   * **Qualità file multimediali:**

      La misurazione della qualità video viene utilizzata per misurare la qualità della riproduzione del contenuto. Questo utilizza le evar della soluzione per memorizzare il tempo in Avvio, Eventi buffer, Durata buffer totale, Switch bitrate, Bitrate medio, Errori e Fotogrammi rilasciati. Gli eventi della soluzione saranno utilizzati per il tempo all'avvio, i rilasci prima dell'avvio, i flussi interessati dal buffer, gli eventi buffer, la durata totale buffer, flussi interessati da bitrate, variazioni di bitrate, bitrate medio, flussi interessati dagli errori, eventi errore, flussi interessati dai fotogrammi rilasciati e fotogrammi rilasciati.

   * **Metadati annuncio video e video:**

      I metadati possono essere allegati a un file multimediale e/o ad un annuncio per descrivere e classificare ulteriormente questi elementi. I supporti standardizzati e i metadati degli annunci verranno raccolti tramite variabili e classificazioni della soluzione. Valori da includere: Show, Season, Episode, Asset ID, Genre, First Air Date, First Digital Date, Content Rating, Originator, Network, Show Type, Ad Upload, MVPD, Authorized, Day Part, Media Session ID, Advertiser, Campaign ID, and Creative ID.

   * **Metadati audio e audio:**

      I metadati possono essere associati all'audio e/o a un annuncio per descrivere e classificare ulteriormente tale audio o annuncio. L'audio standardizzato e i metadati degli annunci verranno raccolti tramite variabili e classificazioni della soluzione. Valori da includere: Artist, Album, Label, Author, Publisher, Station, Show, Season, Episode ID, Genre, First Air Date, First Digital Date, Content Ratings, Originator, Show Type, Ad Upload, Day Part, Media Session ID, Advertiser, Campaign ID, and Creative ID.
   L'abilitazione di ogni modulo riserva una serie di variabili e crea un nuovo set di report. A eccezione della Qualità, nei rapporti non saranno presenti dati, a meno che l'implementazione corrispondente sia stata completata. L'implementazione del modulo Core implementa anche il modulo Quality se lo attivate.

   Se non state ancora tracciando annunci, capitoli o qualità di riproduzione, potete abilitare opzioni aggiuntive in qualsiasi momento.

1. Fai clic su **[!UICONTROL Save]**.

   If this report suite is already configured to collect media data, after you click **[!UICONTROL Save]**, an additional configuration page is displayed. If you see the [!UICONTROL Media Core measurement] page, continue to the next step.

1. (Conditional) On the [!UICONTROL Media Core measurement] page, select to continue using custom variables or to use solution variables.

   | Opzione | Descrizione |
   | --- | --- |
   | Continuare a utilizzare variabili personalizzate | <ul> <li> **Professionisti:** Il tracciamento dei contenuti continua a funzionare dopo la migrazione. </li> <li> **Cons:** Richiede di mantenere due evar personalizzati e tre eventi personalizzati allocati ai supporti. Riassumi l'utilizzo di una evar personalizzata e di un evento personalizzato. </li> </ul> Per continuare a utilizzare variabili personalizzate: <ol> <li>Selezionate Usa variabili personalizzate, quindi fate clic su Salva. </li> <li>Quando richiesto, mappate le evar e gli eventi correnti e fate clic su Salva: </li> </ol> |
   | Migrazione alle variabili della soluzione | <ul> <li> **Professionisti:** Riassumi l'uso di tre evar personalizzati e quattro eventi personalizzati. </li> <li> **Cons:** Perderai **tutte** le tendenze e il confronto storico per i rapporti sui contenuti multimediali. Non è quindi possibile visualizzare le visualizzazioni di contenuto o il tempo di contenuto per qualsiasi data prima della migrazione ai heartbeat. </li> </ul> **Limitazione:** Non effettuare la migrazione alle variabili della soluzione, a meno che non desideri mantenere questa tendenza. Tutti i clienti devono utilizzare variabili di soluzione e regole di elaborazione per inserire i dati multimediali in prop ed evar esistenti, solo se devono mantenere continuità storica. Per effettuare la migrazione alle variabili della soluzione: Selezionate Usa variabili della soluzione e fate clic su Salva. |

   >[!IMPORTANT]
   >
   >Migrating to solution variables causes you to lose **all** historical trending and comparison for media reports.

>[!IMPORTANT]
>
>Do not change the classification names for any variables listed in the Metrics and metadata tables (e.g., [Audio and video parameters](../metrics-and-metadata/audio-video-parameters.md)) that are described there under Reporting/Reserved Variable as "classification". Le classificazioni multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento multimediale. Di tanto in tanto, Adobe aggiunge nuove proprietà e, quando ciò accade, i clienti devono riabilitare le suite di rapporti a ottenere l'accesso alle nuove proprietà del supporto. Durante il processo di aggiornamento Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se mancano alcuni di essi, Adobe ne aggiunge di nuovo quelli mancanti.
