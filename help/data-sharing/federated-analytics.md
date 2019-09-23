---
seo-title: Analisi federate
title: Analisi federate
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: tm+mt
source-git-commit: ef6e37791cd365b12d964b2a06831a563f605104

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
* **** Implementazione di Media Analytics: Il mittente deve avere Media Analytics implementato su tutti i lettori che faranno parte del set di dati federati. Solo i dati di Media Analytics sono disponibili per la federazione. Consulta la documentazione: Misurazione [di audio e video in Adobe Analytics](/help/media-overview.md)

* **** Contratto di consulenza Adobe: Per la configurazione iniziale di regole federate tra il destinatario e il mittente è utile lavorare con i servizi di consulenza per rivedere i dati e creare il contratto di condivisione dei dati.

## Processo {#section_byb_kb3_vbb}

1. Mittente e Ricevitore collaborano per completare il modulo del contratto per le regole federative.
1. Scarica la versione corrente del modulo qui: Modulo di accordo sulle regole [federative.](/assets/federated_analytics_form.pdf)
1. The Federated Rules Agreement form contains special fields for our engineering team and should ONLY be edited using Adobe Acrobat. [Download Acrobat for free.](https://get.adobe.com/reader/)
1. Consulting services provides a sample data file to Receiver with actual data from Sender players, to further confirm correct data sharing rules are defined, provided data files are available.
1. Sender and Receiver ensure the data sharing agreement will meet all contractual requirements between the two parties.
1. Consulting services sends the completed form to Adobe Engineering to set-up data sharing rules.
1. Data is shared to the development report suite where Receiver will review and validate data.
1. Once Receiver confirms data is correct, Adobe Engineering updates the rules to point to a production report suite.
1. Receiver will review and validate data in the production report suite.
1. If changes occur to the data set in the future, Sender or Receiver can submit a customer care ticket for support.

