---
title: Percorsi di implementazione
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 12%

---


# Percorsi di implementazione {#implementation-paths}

Per ogni percorso di implementazione, i clienti devono contattare il proprio rappresentante commerciale/responsabile commerciale per firmare un nuovo ordine di vendita, in quanto Media Analytics dispone di uno SKU univoco e le modifiche da un modello di tariffazione basato sulle chiamate server a un modello basato sui flussi video.

* **Adobe Launch con l’estensione Adobe Media Analytics**

   Adobe Launch è la soluzione di gestione tag di nuova generazione di Adobe. Launch offre un modo semplice per distribuire e gestire tutti i tag di analisi, marketing e pubblicità necessari per fornire esperienze cliente rilevanti. Per creare e mantenere integrazioni personalizzate con Launch, è necessario utilizzare le estensioni. Un&#39;estensione è un pacchetto JavaScript, HTML e CSS che estende l&#39;interfaccia utente e le funzionalità client di Launch. Per ulteriori informazioni, consulta la Guida utente del lancio della piattaforma [Experience](https://docs.adobe.com/content/help/it-IT/launch/using/overview.html)

   L’estensione Adobe Media Analytics (MA) aggiunge l’SDK JavaScript Media (Media 2.x SDK) di base per audio e video. Questa estensione fornisce la funzionalità per aggiungere l&#39;istanza di tracciamento `MediaHeartbeat` a un sito o a un progetto Launch.

   Adobe Launch con l’estensione Media Analytics richiede quanto segue:
   * Devi essere un cliente Adobe Experience Cloud.
   * Devi distribuire il codice di incorporamento Launch o DTM nelle tue pagine Web.
   * [Estensione Analytics](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Estensione Experience Cloud ID](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Lato client** : integrazioni solo per Media Analytics. Potete scegliere l’SDK Video Heartbeat e/o le integrazioni API Media Collection. Questo percorso può essere utilizzato in qualsiasi lettore video, inclusi i lettori OVP e/o cliente come Brightcove, Ooyala, la piattaforma e così via.

   Se Media Analytics è il percorso previsto, consultate Implementazione [](/help/sdk-implement/setup/setup-overview.md) Media SDK e API per la raccolta [di file multimediali.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Per utilizzare Media Analytics, i clienti devono anche utilizzare Adobe Analytics.

* **Adobe Primetime -** Adobe Primetime è una soluzione Adobe Experience Cloud che aiuta programmatori e distributori di contenuti a monetizzare i contenuti multimediali su ogni schermo connesso.

   Primetime elimina la complessità di raggiungere, monetizzare e attivare audience globali tra dispositivi, fornendo una piattaforma modulare per la pubblicazione video, la pubblicità, la personalizzazione e l&#39;analisi. Inoltre, Primetime offre soluzioni e valore in base alle seguenti caratteristiche:

   * Supporto per la misurazione accurata dei tipi di contenuto Lineare e VOD.
   * Supporto per la misurazione di interruzioni pubblicitarie con (o senza) inserimento di annunci dinamici.
   * Il modello di inserimento degli annunci senza soluzione di continuità di TVSDK consente analisi che misurano direttamente la riproduzione degli annunci, aumentando così la precisione.
   * Set affidabile di eventi e metadati per garantire l&#39;accuratezza nei buffering QoS o nelle interruzioni della connettività mobile e nelle interazioni con gli utenti finali, ad esempio per cercare, mettere in pausa e mettere in background i dispositivi mobili.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK è già integrato con l’SDK Media Analytics (Heartbeats), che semplifica e velocizza notevolmente l’implementazione in tutte le piattaforme supportate. <!--Primetime also supports the partnership with Nielsen.--> Per sfruttare Primetime, segui le stesse linee guida e gli stessi prerequisiti presenti nel lato [](/help/intro-to-ava/implementation-paths/client-side-path.md) client insieme ai seguenti documenti per le tue piattaforme: [Guida Utente Primetime.](https://helpx.adobe.com/it/primetime/user-guide.html)

Contatta anche il tuo rappresentante commerciale/responsabile commerciale per conoscere le attività da intraprendere per acquistare TVSDK.
