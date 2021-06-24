---
title: Quali percorsi di implementazione di Streaming Media sono disponibili?
description: Scopri Adobe dei percorsi di implementazione di Streaming Media, incluso Adobe Launch.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 10%

---

# Percorsi di implementazione {#implementation-paths}

Per ogni percorso di implementazione, i clienti devono contattare il proprio rappresentante commerciale/responsabile commerciale per firmare un nuovo ordine di vendita in quanto Streaming Media Analytics ha un SKU univoco e le modifiche da un modello di prezzo basato sulle chiamate al server a un modello basato sui flussi video.

* **Adobe Launch con l’estensione Adobe Medium Analytics**

   Adobe Launch è la soluzione di gestione tag di nuova generazione di Adobe. Launch offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate. Per generare e mantenere integrazioni personalizzate con Launch, utilizza le estensioni. Un’estensione è un pacchetto JavaScript, HTML e CSS che estende l’interfaccia utente e le funzionalità client di Launch. Per ulteriori informazioni, consulta la [Guida utente del Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html?lang=it)

   L’estensione Adobe Medium Analytics (MA) aggiunge l’SDK JavaScript Media (Media 2.x SDK) di base per audio e video. Questa estensione fornisce la funzionalità per aggiungere l&#39;istanza di tracciamento `MediaHeartbeat` a un sito o a un progetto Launch.

   Adobe Launch con estensione Media Analytics richiede quanto segue:
   * Devi essere un cliente Adobe Experience Cloud.
   * Devi distribuire il codice di incorporamento Launch o DTM sulle pagine web.
   * [Estensione Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html?lang=it)
   * [Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html?lang=it)


* **Lato client:** si tratta di integrazioni solo per Media Analytics. Puoi scegliere l’SDK per Video Heartbeat e/o le integrazioni API Media Collection. Questo percorso può essere utilizzato in qualsiasi lettore video, compresi i lettori OVP e/o clienti come Brightcove, Ooyala, la piattaforma e così via.

   Se Media Analytics è il percorso desiderato, consulta [Implementazione Media SDK](/help/sdk-implement/setup/setup-overview.md) e l&#39; [API Media Collection.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Per utilizzare Media Analytics, i clienti devono anche utilizzare Adobe Analytics.

* **Adobe Primetime:** Adobe Primetime è una soluzione Adobe Experience Cloud che consente ai programmatori e ai distributori di contenuti di monetizzare i contenuti multimediali su ogni schermo connesso.

   Primetime elimina la complessità di raggiungere, monetizzare e attivare il pubblico globale tra dispositivi tramite una piattaforma modulare per la pubblicazione video, la pubblicità, la personalizzazione e l’analisi. Inoltre, Primetime offre soluzioni e valore in relazione ai seguenti elementi:

   * Supporto per la misurazione accurata dei tipi di contenuto Lineare e VOD.
   * Supporto per la misurazione di interruzioni pubblicitarie con (o senza) inserimento di annunci dinamici.
   * Il modello di inserimento degli annunci senza soluzione di continuità di TVSDK consente analisi che misurano direttamente la riproduzione degli annunci, aumentando l&#39;accuratezza.
   * Set affidabile di eventi e metadati per garantire la precisione tra buffering QoS o interruzioni della connettività mobile e problemi di interazioni con gli utenti finali come ricerca, sospensione e background su dispositivi mobili.

<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK è già integrato con l’SDK Media Analytics (Heartbeat), che rende l’implementazione molto più semplice e veloce su tutte le piattaforme supportate. <!--Primetime also supports the partnership with Nielsen.--> Per sfruttare Primetime, segui le stesse linee guida e gli stessi prerequisiti presenti sul lato  [client ](/help/intro-to-ava/implementation-paths/client-side-path.md) insieme ai seguenti documenti per le tue piattaforme:  [Guida utente di Primetime.](https://helpx.adobe.com/it/primetime/user-guide.html)

Contatta anche il tuo rappresentante commerciale/responsabile commerciale per discutere cosa devi fare per acquistare TVSDK.
