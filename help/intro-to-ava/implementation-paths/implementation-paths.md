---
title: Quali percorsi di implementazione di Streaming Media sono disponibili?
description: Scopri come Adobe Streaming Media implementa i percorsi, inclusa la raccolta dati di Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f88e8b02bc9723793822fa7647a2ceab9ada45e6
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 19%

---

# Percorsi di implementazione {#implementation-paths}

Per ogni percorso di implementazione, i clienti devono contattare il proprio rappresentante commerciale/responsabile commerciale per firmare un nuovo ordine di vendita in quanto Streaming Media Analytics ha un SKU univoco e le modifiche da un modello di prezzo basato sulle chiamate al server a un modello basato sui flussi video.

## Raccolta dati di Adobe Experience Platform con l’estensione Adobe Medium Analytics

>[!NOTE]
>Adobe Experience Platform Launch è stato riclassificato come una suite di tecnologie di raccolta dati nell’Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) come riferimento consolidato delle modifiche terminologiche.


I tag in Adobe Experience Platform costituiscono la soluzione Adobe di nuova generazione per la gestione dei tag. I tag offrono ai clienti un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate significative. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità a valore aggiunto inclusa.

I tag permettono a chiunque di generare e mantenere le proprie integrazioni, o estensioni. Queste sono disponibili per i clienti Adobe Experience Cloud in un’esperienza di tipo app-store per velocizzarne l’installazione, la configurazione e l’implementazione dei tag.

Un’estensione è un pacchetto di codice (JavaScript, HTML e CSS) che estende le funzionalità dei tag. Puoi generare, gestire e aggiornare le integrazioni tramite un&#39;interfaccia praticamente self-service. È possibile considerare le estensioni come app utilizzate per eseguire le attività.Per ulteriori informazioni, consulta *Panoramica sui tag* articolo [Documentazione di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)

L’estensione Adobe Medium Analytics (MA) aggiunge l’SDK JavaScript Media (Media 2.x SDK) di base per audio e video. Questa estensione fornisce la funzionalità per aggiungere `MediaHeartbeat` istanza di tracciamento per un sito o un progetto di raccolta dati.

Adobe Data Collection con l’estensione Media Analytics richiede quanto segue:
* Devi essere un cliente Adobe Experience Cloud.
* Devi distribuire la raccolta dati o il codice di incorporamento DTM sulle pagine web.
* [Estensione Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html)
* [Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html)


## Lato client

Si tratta di integrazioni solo per Media Analytics. Puoi scegliere l’SDK per Video Heartbeat e/o le integrazioni API Media Collection. Questo percorso può essere utilizzato in qualsiasi lettore video, compresi i lettori OVP e/o clienti come Brightcove, Ooyala, la piattaforma e così via.

Se Media Analytics è il percorso desiderato, consulta la sezione [Implementazione di Media SDK](/help/sdk-implement/setup/setup-overview.md) e [API di raccolta multimediale.](/help/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Per utilizzare Media Analytics, i clienti devono anche utilizzare Adobe Analytics.

## Adobe Primetime

Adobe Primetime è una soluzione Adobe Experience Cloud che aiuta programmatori e distributori di contenuti a monetizzare i contenuti multimediali su ogni schermo connesso.

Primetime elimina la complessità di raggiungere, monetizzare e attivare il pubblico globale tra dispositivi tramite una piattaforma modulare per la pubblicazione video, la pubblicità, la personalizzazione e l’analisi. Inoltre, Primetime offre soluzioni e valore in relazione ai seguenti elementi:

* Supporto per la misurazione accurata dei tipi di contenuto Lineare e VOD.
* Supporto per la misurazione di interruzioni pubblicitarie con (o senza) inserimento di annunci dinamici.
* Il modello di inserimento degli annunci senza soluzione di continuità di TVSDK consente analisi che misurano direttamente la riproduzione degli annunci, aumentando l&#39;accuratezza.
* Set affidabile di eventi e metadati per garantire la precisione tra buffering QoS o interruzioni della connettività mobile e problemi di interazioni con gli utenti finali come ricerca, sospensione e background su dispositivi mobili.
* Supporto integrato per Nielsen DTVR (lineare) con metadati ID3 e DCR con metadati CMS.


TVSDK è già integrato con l’SDK Media Analytics (Heartbeat), che rende l’implementazione molto più semplice e veloce su tutte le piattaforme supportate. Per sfruttare Primetime, segui le stesse linee guida e prerequisiti presenti in [Lato client](/help/intro-to-ava/implementation-paths/client-side-path.md) insieme ai seguenti documenti per le piattaforme: [Guida utente di Primetime.](https://helpx.adobe.com/it/primetime/user-guide.html)

Contatta anche il tuo rappresentante commerciale/responsabile commerciale per discutere cosa devi fare per acquistare TVSDK.
