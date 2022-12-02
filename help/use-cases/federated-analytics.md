---
title: Federated Analytics
description: Il servizio Federated Analytics fornisce un sistema per la condivisione di Adobe Analytics per eseguire lo streaming di dati multimediali tra due partner.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Federated Analytics {#federated-analytics}

Il servizio Federated Analytics fornisce un sistema per la condivisione di dati Adobe Media Analytics (audio e video) tra due partner.
I dati di misurazione standardizzati creati da Media Analytics sono il marchio distintivo di Federated Analytics, che consente di includere in un singolo report dati provenienti da più origini.
Attraverso le regole e la logica che regolano Federated Analytics, i dati sono facilmente controllati e personalizzati per soddisfare le esigenze di ogni partnership.
La funzione Federated Analytics rende la misurazione audio e video più efficiente, semplice e actionable.

## Vantaggi {#benefits}

* **Trasparente:** elimina la black box della creazione dei dati utilizzando la stessa logica tra le aziende.
* **Ampia copertura:** comprendi appieno la portata e l’impatto del consumo di audio e video tra partnership, piattaforme e dispositivi.
* **Protetto:** controlla la condivisione dei dati lato server tramite regole e logica.
* **Standard:** parla la stessa lingua dati dei tuoi partner.
* **Actionable:** quantifica dati audio e video per eseguire il benchmark dei lettori, monitorare le tendenze e rilevare le anomalie tramite Adobe Analytics.
* **Centralizzato:** raccogli i dati di misurazione audio e video in un’unica posizione Adobe.
* **Contrattuale:** soddisfa facilmente i requisiti legali per la condivisione dei dati.
* **Puntuale:** invia e ricevi dati in tempo reale.
* **Semplice:** assegna tag ai lettori una sola volta con gli SDK Adobe e condividi i dati con molti partner

## Definizioni {#definitions}

* **Mittente:** cliente che genera di dati di analisi audio e video sui propri lettori.
* **Destinatario:** cliente che riceve i dati di analisi audio e video dal mittente.

## Requisiti {#requirements}

* **Contratto per i flussi multimediali:** per poter accedere ai dati audio e video in Adobe Analytics, il Destinatario e il Mittente devono aver stipulato un contratto con Adobe Analytics per i flussi di dati multimediali. Per ulteriori informazioni, contatta il team dell’account.
* **Federated Addendum:** prima di inviare o ricevere i dati, ogni Mittente e Destinatario deve disporre di un addendum firmato insieme ad Adobe. È richiesto un addendum per cliente, non un addendum per partnership. Per ulteriori informazioni, contatta il team dell’account.

* **Implementazione di Media Analytics:** il mittente deve avere Media Analytics implementato su tutti i lettori che faranno parte del set di dati federati. Solo i dati di Media Analytics sono disponibili per la federazione. Consulta la documentazione: [Misurazione dei contenuti multimediali in streaming in Adobe Analytics](/help/media-overview.md)

* **Contratto di consulenza Adobe:** per la configurazione iniziale di regole federate tra il destinatario e il mittente è utile ricorrere ai servizi di consulenza per rivedere i dati e creare l’accordo di condivisione dei dati.

## Download del modulo di Federated Analytics

Per partecipare a Federated Analytics, scarica e completa il modulo [Accordo sulle regole federative](assets/federated_analytics_form.pdf).

## Processo {#process}

1. Mittente e Destinatario collaborano per compilare il modulo Federation Rules Agreement. Il modulo Federated Rules Agreement contiene campi speciali per il nostro team di progettazione e deve essere modificato SOLO con Adobe Acrobat. [Scarica Acrobat gratuitamente.](https://get.adobe.com/it/reader/)
1. I servizi di consulenza forniscono al Destinatario un file di dati di esempio con dati effettivi provenienti dai lettori del Mittente, per confermare ulteriormente la definizione di le regole di condivisione dei dati corrette, a condizione che i file di dati siano disponibili.
1. Il Mittente e il Destinatario garantiscono che l’accordo di condivisione dei dati soddisfi tutti i requisiti contrattuali tra le due parti.
1. I servizi di consulenza inviano il modulo compilato ad Adobe Engineering per configurare le regole di condivisione dei dati.
1. I dati vengono condivisi con la suite di rapporti per lo sviluppo in cui il Destinatario rivede e convalida i dati.
1. Una volta che il Destinatario conferma che i dati sono corretti, Adobe Engineering aggiorna le regole in modo che puntino a una suite di rapporti sulla produzione.
1. Il Destinatario rivede e convalida i dati nella suite di rapporti di produzione.
1. Se in futuro si verificassero modifiche al set di dati, il Mittente o il Destinatario possono inviare un ticket di assistenza clienti per ricevere supporto.
