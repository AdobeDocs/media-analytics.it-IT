---
seo-title: Analisi federate
title: Analisi federate
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: tm+mt
source-git-commit: a80097ac92c422bcf9c04a18ee91a20d3d383af4

---


# Analisi federate{#federated-analytics}

Il servizio Analisi federata fornisce un sistema per la condivisione di dati Adobe Media (audio e video) Analytics tra due partner. I dati di misurazione standardizzati creati da Media Analytics sono il marchio distintivo per Federated Analytics, consentendo lo scorrimento degli stessi dati in un singolo report da più origini. Attraverso le regole e la logica che regolano l'analisi federata, i dati sono facilmente controllati e individualizzati per soddisfare le esigenze di ogni partnership. La funzione Analisi federata rende la misurazione audio e video più efficiente, semplice e utilizzabile.

## Vantaggi {#section_804FFE8671594A6FB769CBE79EF9D627}

* **** Trasparente: Elimina dalla casella nera la creazione dei dati utilizzando la stessa logica tra le aziende
* **** Ampia: Comprendere appieno la portata e l'impatto del consumo audio e video tra partnership, piattaforme e dispositivi
* **** Protetto: Controllo della condivisione dei dati lato server tramite regole e logica
* **** Standard: Parla la stessa lingua dati dei tuoi partner
* **** Azioni: Quantificazione di dati audio e video per eseguire il benchmark dei lettori, monitorare le tendenze e rilevare le anomalie tramite Adobe Analytics
* **** Centralizzato: Raccogliere i dati di misurazione audio e video in una posizione Adobe
* **** Contrattuale: Soddisfare facilmente i requisiti legali per la condivisione dei dati
* **** Temporaneamente: Inviare e ricevere dati in tempo reale
* **** Facile: Assegnare tag ai lettori una sola volta con gli SDK Adobe, condividere i dati a molti partner

## Definizioni {#section_ypl_mb3_vbb}

* **** Mittente: Generazione di dati di analisi audio e video da parte dei clienti sui lettori di proprietà
* **** Ricevitore: Ricezione da parte del cliente dei dati di analisi audio e video dal mittente

## Requisiti {#section_4758843A8941441B9A4D0D7A61077A6E}

* **** Contratto Streams Media: Per poter accedere ai dati audio e video in Adobe Analytics, il destinatario e il mittente devono aver stipulato un contratto con Adobe Analytics per i flussi di dati multimediali. Per ulteriori informazioni, contattate il team di account.
* **** Federated Addendum: Prima di inviare o ricevere i dati, ogni mittente e ricevente deve disporre di un addendum firmato insieme ad Adobe. È richiesto un addendum per cliente, non un addendum per partnership. Per ulteriori informazioni, contattate il team di account.
* **** Implementazione di Media Analytics: Il mittente deve avere Media Analytics implementato su tutti i lettori che faranno parte del set di dati federati. Solo i dati di Media Analytics sono disponibili per la federazione. Consulta la documentazione: Misurazione [di audio e video in Adobe Analytics](media-overview.md)

* **** Contratto di consulenza Adobe: Per la configurazione iniziale di regole federate tra il destinatario e il mittente è utile lavorare con i servizi di consulenza per rivedere i dati e creare il contratto di condivisione dei dati.

## Processo {#section_byb_kb3_vbb}

1. Mittente e Ricevitore collaborano per completare il modulo del contratto per le regole federative. **** Scarica la versione corrente del modulo qui: Modulo di accordo sulle regole [federative.](/assets/federated_analytics_form.pdf)

   [!NOTA Questo modulo contiene campi speciali per il nostro team di progettazione e deve essere modificato SOLO tramite Adobe Acrobat. [Scarica Acrobat gratuitamente.](https://get.adobe.com/reader/)
1. I servizi di consulenza forniscono un file di dati di esempio a Receiver con dati effettivi provenienti dai lettori Mender, per confermare ulteriormente che le regole di condivisione dei dati corrette sono definite, a condizione che i file di dati siano disponibili.
1. Il mittente e il ricevente garantiscono che il contratto di condivisione dei dati soddisfi tutti i requisiti contrattuali tra le due parti.
1. I servizi di consulenza inviano il modulo compilato ad Adobe Engineering per configurare le regole di condivisione dei dati.
1. I dati vengono condivisi con la suite di rapporti per lo sviluppo in cui il destinatario rivede e convalida i dati.
1. Una volta che il ricevente conferma che i dati sono corretti, Adobe Engineering aggiorna le regole per puntare a una suite di rapporti sulla produzione.
1. Il ricevente rivede e convalida i dati nella suite di rapporti di produzione.
1. Se si verificano modifiche al set di dati in futuro, Mittente o Ricevitore può inviare un ticket di assistenza clienti per l'assistenza.

