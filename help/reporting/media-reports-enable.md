---
title: Abilitazione di rapporti sui contenuti multimediali
description: Scopri la suite di rapporti sui file multimediali che raccoglie le metriche sui file multimediali.  Per configurare i rapporti sui file multimediali prima dell’invio dei dati multimediali, effettua le seguenti operazioni.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e0a8d2d16a746a717d54bdb171f66f3a7d112251
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Abilitazione di rapporti sui contenuti multimediali {#media-reports-enablement}

Ogni suite di rapporti che raccoglie metriche multimediali deve essere configurata prima dell’invio dei dati multimediali.

I clienti più esperti possono utilizzare i pannelli per contenuti multimediali in Analysis Workspace solo dopo avere abilitato Media Core e il tracciamento per la [Qualità dell’esperienza](/help/use-cases/track-qos/track-qos-overview.md).

>[!TIP]
>
>Per sfruttare le nuove funzionalità, i clienti Media Analytics esistenti devono riabilitare il tracciamento dei contenuti multimediali per i loro RSID.

1. In [Reports &amp; Analytics](https://my.omniture.com/login/) fai clic su **[!UICONTROL Admin > Report Suites].**
1. Seleziona le suite di rapporti in cui stai raccogliendo dati multimediali e fai clic su **[!UICONTROL Edit Settings > Media Management > Media Reporting].**

   ![](assets/media-reporting.png)

1. Sulla pagina **[!UICONTROL Media Reporting]**, abilita **[!UICONTROL Media Core],** e, facoltativamente, abilita **[!UICONTROL Media Ads],** **[!UICONTROL Media Chapters],** e **[!UICONTROL Media Quality].**

   La misurazione dei file multimediali include i seguenti moduli:

   * **Media Core**

      La misurazione dei contenuti multimediali di base viene utilizzata per i contenuti multimediali. Questo utilizzerà le eVar della soluzione (o personalizzate) per tenere traccia di Contenuto, Tipo di contenuto, Nome del lettore di contenuti e Canale di contenuto. Gli eventi di soluzione (o personalizzati) verranno utilizzati per gli eventi di inizio media, inizio contenuto, completamente contenuto e tempo trascorso contenuto.

   * **Annunci multimediali**

      La misurazione degli annunci multimediali viene utilizzata per la misurazione degli annunci all’interno del contenuto multimediale. Questo utilizzerà le eVar della soluzione per misurare Annuncio, Nome dell’Ad Player, Annuncio pubblicitario e Annuncio in posizione contenitore. Gli eventi della soluzione saranno utilizzati per gli eventi di inizio annuncio, completamento annuncio, tempo trascorso annuncio e tempo trascorso video.

   * **Capitoli multimediali**

      La misurazione dei capitoli video viene utilizzata per la misurazione dei capitoli. Un capitolo è una suddivisione dei contenuti all’interno di un singolo supporto. Questo utilizzerà un eVar della soluzione per memorizzare l’ID del capitolo. Gli eventi della soluzione verranno utilizzati per gli eventi di inizio capitolo, completamento capitolo e tempo capitolo trascorso. I metadati aggiuntivi del capitolo Nome e Posizione capitolo saranno forniti come classificazioni dell’ID capitolo.

   * **Qualità dei supporti**

      La misurazione della qualità video viene utilizzata per misurare la qualità di riproduzione dei contenuti. Questo utilizzerà le eVar della soluzione per memorizzare il tempo di avvio, gli eventi buffer, la durata totale del buffer, gli switch bitrate, il bitrate medio, gli errori e i fotogrammi rilasciati. Eventi per la soluzione saranno utilizzati per tempo di avvio, perdite prima dell’avvio, flussi interessati dal buffer, eventi buffer, durata totale buffer, flussi interessati dalla modifica del bitrate, modifiche del bitrate, bitrate medio, flussi interessati da errori, eventi di errore, flussi interessati da fotogrammi saltati e fotogrammi saltati.

   * **Metadati annuncio video &amp; video**

      I metadati possono essere allegati al media e/o all’annuncio per descrivere o classificare ulteriormente questi ultimi. I video standardizzati e i metadati degli annunci vengono raccolti tramite variabili e classificazioni della soluzione. I valori includono: spettacolo, stagione, episodio, ID risorsa, genere, prima messa in onda, prima pubblicazione digitale, valutazione contenuto, creatore, rete, tipo di programma, carico pubblicitario, MVPD, autorizzato, parte del giorno, ID di sessione media, inserzionista, ID campagna e ID creativo.

   * **Metadati annuncio audio &amp; audio**

      I metadati possono essere allegati all’audio e/o all’annuncio per descrivere o classificare ulteriormente questi ultimi. Gli audio standardizzati e i metadati degli annunci vengono raccolti tramite variabili e classificazioni della soluzione. Valori da includere: artista, album, etichetta, autore, editore, stazione, spettacolo, stagione, episodio, ID risorsa, genere, prima data aria, prima data digitale, valutazione contenuto, referente, tipo di spettacolo, caricamento annuncio, parte giorno, ID sessione media, inserzionista, ID campagna e ID creativo.
   L’abilitazione di ogni modulo riserva un set di variabili e crea un nuovo set di rapporti. Ad eccezione di Qualità, i rapporti non conterranno alcun dato, a meno che l’implementazione corrispondente non sia stata completata. L’implementazione del modulo Core implementa anche il modulo Qualità se lo abiliti.

   Se non tieni traccia degli annunci, dei capitoli o della qualità di riproduzione, puoi attivare opzioni aggiuntive in qualsiasi momento.

1. Fai clic su **[!UICONTROL Save].**

   Se questa suite di rapporti è già configurata per la raccolta dei dati multimediali, dopo aver fatto clic su **[!UICONTROL Save]**, viene visualizzata una pagina di configurazione aggiuntiva. Se vedi la pagina **[!UICONTROL Media Core measurement]**, continua con il passaggio successivo.

1. (Condizionale) Sulla pagina **[!UICONTROL Media Core measurement]**, scegli di continuare a utilizzare le variabili personalizzate o scegli di utilizzare le variabili della soluzione.

   | Opzione | Note |
   | --- | --- |
   | Continua a utilizzare variabili personalizzate | Pro e contro:<ul> <li> **Pro:** la tendenza dei contenuti continua a funzionare dopo la migrazione. </li> <li> **Contro:** richiede di mantenere due eVar personalizzate e tre eventi personalizzati assegnati ai contenuti multimediali. Riutilizzi un eVar personalizzato e un evento personalizzato. </li> </ul> Per continuare a utilizzare variabili personalizzate: <ol> <li>Seleziona **[!UICONTROL Use Custom Variables,]** quindi fai clic su **[!UICONTROL Save.]** </li> <li>Quando richiesto, mappa le eVar ed eventi personalizzati correnti e fai clic su **[!UICONTROL Save:]** </li> </ol> |
   | Migrazione a variabili della soluzione | Pro e contro:<ul> <li> **Pro:** riutilizzi tre eVar personalizzate e quattro eventi personalizzati. </li> <li> **Contro:** perdi **tutte** le tendenze storiche e il confronto per i report multimediali. Ciò significa che non è possibile impostare le visualizzazioni dei contenuti o il tempo di riproduzione dei contenuti per le date precedenti alla migrazione a heartbeat. </li> </ul> **Limitazione:**  non eseguire la migrazione alle variabili della soluzione a meno che non si sia certi di non voler mantenere questa tendenza. Tutti i clienti devono utilizzare le variabili della soluzione e le regole di elaborazione per inserire i dati multimediali nelle proprietà e eVar esistenti, solo se devono preservare la continuità storica. Per migrare alle variabili della soluzione: seleziona **[!UICONTROL Use Solution Variables]** e fai clic su **[!UICONTROL Save].** <br><br> IMPORTANTE: la migrazione alle variabili della soluzione comporta la perdita di **tutte** le tendenze storiche e il confronto per i report multimediali. |

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate nelle tabelle Metriche e metadati (ad es. [Parametri audio e video](/help/implementation/variables/audio-video-parameters.md)) che sono descritti in Reporting/Variabile riservata come “classificazione”. Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento dei contenuti multimediali. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà multimediali. Durante il processo di aggiornamento, l’Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di questi, Adobe aggiunge di nuovo quelli mancanti.
