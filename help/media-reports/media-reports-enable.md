---
seo-title: Abilitazione dei rapporti multimediali
title: Media reports enablement
uuid: d306068d-a308-4b6e-8a72-742dda0de428
translation-type: tm+mt
source-git-commit: ab400b673e97f9b47c6088e09b7e7d9e7b1c9ee6

---


# Media reports enablement{#media-reports-enablement}

Each report suite that collects media metrics must be configured before media data is sent.

>[!TIP]
>
>Per sfruttare le nuove funzionalità, i clienti esistenti di Media Analytics dovrebbero riabilitare il tracciamento dei supporti per i loro RSID.

1. In [Reporting e analisi](https://my.omniture.com/login/) fate clic su [!UICONTROL Admin] &gt; [!UICONTROL Report Suites].
1. Selezionate le suite di rapporti in cui state raccogliendo i dati multimediali e fate clic su [!UICONTROL Edit Settings] &gt; [!UICONTROL Media Management] &gt; [!UICONTROL Media Reporting].

   ![](assets/media-reporting.png){width="400px"}

1. On the  page, enable , and optionally enable , , and .**[!UICONTROL Media Reporting]****[!UICONTROL Media Core]****[!UICONTROL Media Ads]****[!UICONTROL Media Chapters]****[!UICONTROL Media Quality]**

   Media measurement includes the following modules:

   * **Media Core**

      La misurazione dei contenuti multimediali di base viene utilizzata per i contenuti multimediali. In questo modo si utilizzeranno le eVar della soluzione (o personalizzate) per tenere traccia di Contenuto, Tipo di contenuto, Nome lettore contenuto e Canale contenuto. Gli eventi della soluzione (o personalizzati) verranno utilizzati per gli avvii dei contenuti multimediali, gli avvii dei contenuti, i completamenti dei contenuti e il tempo trascorso per i contenuti.

   * **Annunci multimediali**

      La misura degli annunci multimediali viene utilizzata per la misurazione degli annunci all'interno del contenuto multimediale. Questo utilizzerà le eVar della soluzione per misurare Annuncio, Nome lettore pubblicitario, Contenitore annunci e Annuncio nella posizione del contenitore. Gli eventi della soluzione verranno utilizzati per Avvii annunci, Completamento annunci, Tempo annunci trascorso e Tempo video trascorso.

   * **Media Chapters**

      Video chapters measurement is used for the measurement of chapters. A chapter is a sub-division of content within a single media. Questo utilizzerà una eVar soluzione per memorizzare l'ID capitolo. Gli eventi della soluzione verranno utilizzati per gli avvii dei capitoli, per i completamenti dei capitoli e per il tempo trascorso per i capitoli. I metadati aggiuntivi del capitolo Nome e Posizione capitolo verranno forniti come classificazioni dell’ID capitolo.

   * **Media Quality**

      Video quality measurement is used for measuring the quality of the content playback. This will use Solution eVars to store Time to Start, Buffer Events, Total Buffer Duration, Bitrate Switches, Average Bitrate, Errors, and Dropped Frames. Solution events will be used for Time to Start, Drops before Start, Buffer Impacted Streams, Buffer Events, Total Buffer Duration, Bitrate Change Impacted Streams, Bitrate Changes, Avg Bitrate, Error Impacted Streams, Error Events, Dropped Frame Impacted Streams, and Dropped Frames.

   * **Video &amp; Video Ad Metadata**

      I metadati possono essere allegati a un supporto e/o a un annuncio per descrivere e classificare ulteriormente tale supporto o annuncio. I supporti standardizzati e i metadati degli annunci verranno raccolti tramite variabili e classificazioni della soluzione. Valori da includere: Mostra, Stagione, Episodio, ID risorsa, Genere, Data prima aria, Prima data digitale, Valutazione contenuto, Creatore, Rete, Tipo di spettacolo, Caricamenti annunci, MVPD, Autorizzato, Parte giorno, ID sessione media, Inserzionista, ID campagna e ID creativo.

   * **Metadati annuncio audio e audio**

      I metadati possono essere allegati all'audio e/o a un annuncio per descrivere e classificare ulteriormente tale audio/annuncio. L'audio standardizzato e i metadati degli annunci verranno raccolti tramite variabili e classificazioni della soluzione. Valori da includere: Artista, Album, Label, Author, Publisher, Station, Show, Stagione, Episodio, ID risorsa, Genere, Prima Aria Data, Prima Digitale, Valutazione contenuto, Creatore, Tipo di evento, Caricamenti annuncio, Giorno Parte, ID sessione multimediale, Inserzionista, ID campagna e ID creativo.
   Abilitando ciascun modulo si riserva un set di variabili e si crea un nuovo set di rapporti. Ad eccezione di Qualità, i rapporti non conterranno alcun dato, a meno che l'implementazione corrispondente non sia stata completata. L'implementazione del modulo Core implementa anche il modulo Quality se lo si abilita.

   Se non state ancora tracciando annunci, capitoli o qualità di riproduzione, potete attivare opzioni aggiuntive in qualsiasi momento.

1. Fai clic su **[!UICONTROL Save]**.

   Se questa suite di rapporti è già configurata per la raccolta dei dati multimediali, dopo aver fatto clic su di essa **[!UICONTROL Save]**, viene visualizzata una pagina di configurazione aggiuntiva. Se viene visualizzata la [!UICONTROL Media Core measurement] pagina, continuate con il passaggio successivo.

1. (Condizionale) Nella [!UICONTROL Media Core measurement] pagina, scegliere di continuare a utilizzare variabili personalizzate o scegliere di utilizzare variabili della soluzione.

   | Opzione | Note |
   | --- | --- |
   | Continua utilizzando variabili personalizzate | Pro e Cons:<ul> <li> **** Pro: La tendenza dei contenuti continua a funzionare dopo la migrazione. </li> <li> **** Cons: Richiede di mantenere due eVar personalizzate e tre eventi personalizzati assegnati ai supporti. È possibile riutilizzare un'eVar personalizzata e un evento personalizzato. </li> </ul> Per continuare a utilizzare variabili personalizzate: <ol> <li>Selezionate Usa variabili personalizzate, quindi fate clic su Salva. </li> <li>Quando richiesto, mappate le eVar ed eventi personalizzati correnti e fate clic su Salva: </li> </ol> |
   | Migrazione alle variabili della soluzione | Pro e Cons:<ul> <li> **** Pro: Puoi nuovamente utilizzare tre eVar personalizzate e quattro eventi personalizzati. </li> <li> **** Cons: Perdi **tutte** le tendenze storiche e i confronti per i report sui media. Ciò significa che non è possibile visualizzare i trend relativi alle visualizzazioni dei contenuti o al tempo di riproduzione dei contenuti per date precedenti alla migrazione a heartbeat. </li> </ul> **** Limitazione:  Non eseguire la migrazione alle variabili della soluzione a meno che non si sia certi di non voler mantenere questa tendenza. Tutti i clienti devono utilizzare le variabili di soluzione e le regole di elaborazione per inserire i dati multimediali nelle proprietà e nelle eVar esistenti, solo se devono preservare la continuità storica. Per migrare alle variabili della soluzione:Selezionate [!UICONTROL Use Solution Variables] e fate clic su [!UICONTROL Save]. <br><br> IMPORTANTE: La migrazione alle variabili della soluzione comporta la perdita di **tutte** le tendenze storiche e il confronto per i report multimediali. |

>[!IMPORTANT]
>
>Non modificate i nomi delle classificazioni per le variabili elencate nelle tabelle Metriche e metadati (ad esempio, parametri [](/help/metrics-and-metadata/audio-video-parameters.md)audio e video) che sono qui descritti in Variabile Reporting/Riservato come "classificazione". Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per il tracciamento dei supporti. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per poter accedere alle nuove proprietà del supporto. Durante il processo di aggiornamento, Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di essi, Adobe aggiunge di nuovo quelli mancanti.
