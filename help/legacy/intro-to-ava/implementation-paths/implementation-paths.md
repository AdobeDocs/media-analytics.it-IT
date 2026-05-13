---
title: Quali percorsi di implementazione di contenuti multimediali in streaming sono disponibili?
description: Scopri i percorsi di implementazione di contenuti multimediali in streaming di Adobe, inclusa la raccolta dati di Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/U9PBQc7dHNmONZc06t1Xi7EITkveGUkzcst6Sakqqzo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: eb9732ab-8232-4b21-bc4c-89de86dbe4d7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 676
ht-degree: 89%

---

# Percorsi di implementazione {#implementation-paths}

**QUESTO CONTENUTO È STATO SPOSTATO NEL FILE CORRENTE DEI PERCORSI DI IMPLEMENTAZIONE**

Per ogni percorso di implementazione, i clienti devono contattare il proprio rappresentante commerciale o il team dell’account Adobe per firmare un nuovo ordine di vendita, poiché Customer Journey Analytics Streaming Media Collection e Adobe Analytics for Streaming Media hanno una SKU univoca e cambiano da un modello di prezzo basato sulle chiamate al server a un modello basato sui flussi video.

## Raccolta dati di Adobe Experience Platform con l’estensione Adobe Medium Analytics

>[!NOTE]
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=it) come riferimento consolidato delle modifiche terminologiche.


I tag in Adobe Experience Platform costituiscono la soluzione Adobe di nuova generazione per la gestione dei tag. I tag offrono ai clienti un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate significative. I tag vengono forniti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto.

I tag permettono a chiunque di generare e mantenere le proprie integrazioni, o estensioni. Le estensioni sono disponibili per i clienti di Adobe Experience Cloud in un’esperienza di tipo app-store, per velocizzare l’installazione, la configurazione e l’implementazione dei tag.

Un’estensione è un pacchetto di codice (JavaScript, HTML e CSS) che estende le funzionalità dei tag. Puoi generare, gestire e aggiornare le integrazioni tramite un&#39;interfaccia praticamente self-service. Puoi considerare le estensioni come app da utilizzare per eseguire le attività.Per ulteriori informazioni, consulta l&#39;articolo *Panoramica sui tag* nella [Documentazione di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)

L’estensione Adobe Media Analytics (MA) aggiunge l’SDK principale JavaScript Media (Media 2.x SDK) per audio e video. Questa estensione offre le funzionalità necessarie per aggiungere l’istanza di tracciamento `MediaHeartbeat` a un progetto o sito di raccolta dati.

Adobe Data Collection con l’estensione Media Analytics richiede quanto segue:
* È necessario essere un cliente Adobe Experience Cloud.
* È necessario distribuire sulle pagine web il codice di raccolta dati o DTM da incorporare.
* [Estensione Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=it)
* [Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=it)


## Lato client

Si tratta di integrazioni disponibili solo per Media Analytics. Puoi scegliere l’SDK di heartbeat video e/o le integrazioni API di Media Collection. Questo percorso può essere utilizzato su qualsiasi lettore video, tra cui lettori OVP e/o clienti come Brightcove, Ooyala, thePlatform e così via.

Se Media Analytics è il percorso desiderato, consulta la sezione [Implementazione di Media SDK](/help/legacy/setup/legacy-setup-overview.md) e l’[API di Media Collection.](/help/implementation/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Per utilizzare Media Analytics, i clienti devono utilizzare anche Adobe Analytics.

## Adobe Primetime

Adobe Primetime è una soluzione Adobe Experience Cloud che consente a programmatori e distributori di contenuti di monetizzare i contenuti multimediali su ogni schermo connesso.

Primetime semplifica il raggiungimento, la monetizzazione e l’attivazione del pubblico globale tra dispositivi mediante una piattaforma modulare per la pubblicazione video, la pubblicità, la personalizzazione e l’analisi. Inoltre, Primetime offre soluzioni e valore in relazione ai seguenti elementi:

* Supporto per la misurazione accurata dei tipi di contenuto Lineare e VOD.
* Supporto per la misurazione di interruzioni pubblicitarie con (o senza) inserimento di annunci dinamici.
* Il modello di inserimento facile di annunci di TVSDK offre analisi che misurano direttamente la riproduzione degli annunci, aumentandone l’accuratezza.
* Set affidabile di eventi e metadati per garantire maggiore accuratezza tra buffering QoS o interruzioni della connettività mobile e problemi di interazione degli utenti finali, tra cui ricerca, sospensione e background su dispositivi mobili.
* Supporto integrato per Nielsen DTVR (lineare) con metadati ID3 e DCR con metadati CMS.


TVSDK è già integrato con l’SDK Media Analytics (Heartbeat), il quale rende l’implementazione molto più semplice e veloce su tutte le piattaforme supportate. Per utilizzare Primetime, attieniti alle linee guida e ai prerequisiti indicati in [Lato client](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md), nonché ai seguenti documenti per le piattaforme: [Guida utente di Primetime.](https://helpx.adobe.com/it/primetime/user-guide.html)

Contatta inoltre il tuo rappresentante/Account Manager per informazioni su come acquistare TVSDK.
