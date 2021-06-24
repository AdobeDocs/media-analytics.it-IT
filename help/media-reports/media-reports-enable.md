---
title: Abilitazione dei report multimediali
description: Scopri la suite di rapporti sui file multimediali che raccoglie le metriche sui file multimediali.  Per configurare i rapporti sui file multimediali prima dell’invio dei dati multimediali, effettua le seguenti operazioni.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---

# Abilitazione dei report multimediali{#media-reports-enablement}

Ogni suite di rapporti che raccoglie metriche multimediali deve essere configurata prima dell’invio dei dati multimediali.

>[!TIP]
>
>Per sfruttare le nuove funzionalità, i clienti Media Analytics esistenti devono riabilitare il tracciamento dei contenuti multimediali per i loro RSID.

1. In [Reports &amp; Analytics](https://my.omniture.com/login/) fai clic su **[!UICONTROL Admin > Report Suites].**
1. Seleziona le suite di rapporti in cui stai raccogliendo dati multimediali e fai clic su **[!UICONTROL Edit Settings > Media Management > Media Reporting].**

   ![](assets/media-reporting.png){width=&quot;400px&quot;}

1. Nella pagina **[!UICONTROL Media Reporting]** , abilita **[!UICONTROL Media Core],** ed eventualmente abilita **[!UICONTROL Media Ads],** **[!UICONTROL Media Chapters],** e **[!UICONTROL Media Quality].**

   La misurazione dei file multimediali include i seguenti moduli:

   * **Media Core**

      La misurazione dei contenuti multimediali di base viene utilizzata per i contenuti multimediali. Questo utilizzerà le eVar della soluzione (o personalizzate) per tenere traccia di Contenuto, Tipo di contenuto, Nome del lettore di contenuti e Canale di contenuto. Gli eventi di soluzione (o personalizzati) verranno utilizzati per Media Starts, Content Starts, Content Completes e Content Time Spent.

   * **Annunci multimediali**

      La misurazione degli annunci multimediali viene utilizzata per la misurazione degli annunci all’interno del contenuto multimediale. Questo utilizzerà le eVar della soluzione per misurare Annuncio, Nome dell’Ad Player, Annuncio pubblicitario e Annuncio in posizione contenitore. Gli eventi della soluzione saranno utilizzati per gli annunci Starts, Ad Completes, Ad Time Spent e Video Time Spent.

   * **Capitoli multimediali**

      La misurazione dei capitoli video viene utilizzata per la misurazione dei capitoli. Un capitolo è una suddivisione dei contenuti all’interno di un singolo supporto. Questo utilizzerà un eVar della soluzione per memorizzare l&#39;ID del capitolo. Gli eventi della soluzione verranno utilizzati per gli eventi di inizio capitolo, completamento capitolo e tempo capitolo trascorso. I metadati aggiuntivi del capitolo Nome e Posizione capitolo saranno forniti come classificazioni del capitolo ID.

   * **Qualità dei supporti**

      La misurazione della qualità video viene utilizzata per misurare la qualità di riproduzione dei contenuti. Questo utilizzerà le eVar della soluzione per memorizzare il tempo di avvio, gli eventi buffer, la durata totale del buffer, gli switch bitrate, il bitrate medio, gli errori e i fotogrammi rilasciati. Gli eventi della soluzione saranno utilizzati per l&#39;avvio, le perdite prima dell&#39;avvio, i flussi interessati dal buffer, gli eventi buffer, la durata totale del buffer, i flussi interessati dalla modifica del bitrate, le modifiche del bitrate, il bitrate medio, i flussi interessati dagli errori, gli eventi di errore, i flussi interessati dai fotogrammi rilasciati e i fotogrammi rilasciati.

   * **Metadati annuncio video e video**

      I metadati possono essere allegati a un supporto e/o a un annuncio per descrivere e classificare ulteriormente tale supporto/annuncio. I media standardizzati e i metadati degli annunci verranno raccolti tramite variabili e classificazioni della soluzione. Valori da includere: Mostra, Stagione, Episodio, Asset ID, Genere, First Air Date, First Digital Date, Valutazione del contenuto, Originator, Network, Show Type, Ad Loads, MVPD, Authorized, Day Part, Media Session ID, Advertiser, Campaign ID e Creative ID.

   * **Metadati annuncio audio e audio**

      I metadata possono essere allegati all&#39;audio e/o a un annuncio per descrivere e classificare ulteriormente tale audio/annuncio. I metadati standardizzati di audio e annunci verranno raccolti tramite variabili e classificazioni della soluzione. Valori da includere: Artista, Album, Etichetta, Autore, Editore, Stazione, Mostra, Stagione, Episodio, Asset ID, Genere, Prima Aria Data, Prima Digitale, Valutazione Contenuto, Originatore, Tipo di Spettacolo, Caricamento Annuncio, Parte Giorno, ID sessione Media, Inserzionista, ID campagna e ID creativo.
   L’abilitazione di ogni modulo riserva un set di variabili e crea un nuovo set di rapporti. Ad eccezione di Quality, i rapporti non conterranno alcun dato, a meno che l’implementazione corrispondente non sia stata completata. L’implementazione del modulo Core implementa anche il modulo Quality se lo abiliti.

   Se non tieni traccia degli annunci, dei capitoli o della qualità di riproduzione, puoi attivare opzioni aggiuntive in qualsiasi momento.

1. Fai clic su **[!UICONTROL Save].**

   Se questa suite di rapporti è già configurata per raccogliere dati multimediali, dopo aver fatto clic su **[!UICONTROL Save]** viene visualizzata una pagina di configurazione aggiuntiva. Se viene visualizzata la pagina **[!UICONTROL Media Core measurement]** , continua con il passaggio successivo.

1. (Condizionale) Nella pagina **[!UICONTROL Media Core measurement]** , scegli di continuare a utilizzare variabili personalizzate o di utilizzare variabili della soluzione.

   | Opzione | Note |
   | --- | --- |
   | Continua a utilizzare variabili personalizzate | Pro e Cons:<ul> <li> **Pros:** la tendenza dei contenuti continua a funzionare dopo la migrazione. </li> <li> **Cons:** richiede di mantenere due eVar personalizzate e tre eventi personalizzati assegnati ai contenuti multimediali. Riutilizzi un eVar personalizzato e un evento personalizzato. </li> </ul> Per continuare a utilizzare variabili personalizzate: <ol> <li>Seleziona **[!UICONTROL Use Custom Variables,]** e fai clic su **[!UICONTROL Save.]** </li> <li>Quando richiesto, mappa le eVar ed eventi personalizzati correnti e fai clic su **[!UICONTROL Save:]** </li> </ol> |
   | Migrazione a variabili della soluzione | Pro e Cons:<ul> <li> **Pro:** recuperi l’utilizzo di tre eVar personalizzate e quattro eventi personalizzati. </li> <li> **Cons:** si perdono  **** tutti i trend storici e i confronti per i report multimediali. Ciò significa che non è possibile impostare le visualizzazioni dei contenuti o il tempo di riproduzione dei contenuti per le date precedenti alla migrazione a heartbeat. </li> </ul> **Restrizione:**  non eseguire la migrazione alle variabili della soluzione a meno che non si sia certi di non voler mantenere questa tendenza. Tutti i clienti devono utilizzare le variabili della soluzione e le regole di elaborazione per inserire i dati multimediali nelle proprietà e eVar esistenti, solo se devono preservare la continuità storica. Per migrare alle variabili della soluzione: Selezionare **[!UICONTROL Use Solution Variables]** e fare clic su **[!UICONTROL Save].** <br><br> IMPORTANTE: La migrazione alle variabili della soluzione comporta la perdita di  **** tutti i trend storici e il confronto per i report multimediali. |

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate nelle tabelle Metriche e metadati (ad esempio, [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)) che sono qui descritti in Reporting/Reserved Variable come &quot;classificazione&quot;. Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento dei contenuti multimediali. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà multimediali. Durante il processo di aggiornamento, l’Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di questi, Adobe aggiunge di nuovo quelli mancanti.
