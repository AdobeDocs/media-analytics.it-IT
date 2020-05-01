---
title: Opzioni di misurazione
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 47b4c7fe09da0d38c8faae1c3b4293ce48552bdc

---


# Opzioni di misurazione

Puoi abilitare il tracciamento audio e video utilizzando Adobe Launch con l’estensione Adobe Media Analytics, Media SDK o l’API di Media Collection.

## Adobe Launch con l’estensione Adobe Media Analytics

Adobe Launch è la soluzione di gestione tag di nuova generazione di Adobe. Launch offre un modo semplice per distribuire e gestire tutti i tag di analisi, marketing e pubblicità necessari per fornire esperienze cliente rilevanti. Per creare e mantenere integrazioni personalizzate con Launch, è necessario utilizzare le estensioni. Un&#39;estensione è un pacchetto JavaScript, HTML e CSS che estende l&#39;interfaccia utente e le funzionalità client di Launch. Per ulteriori informazioni, consulta la Guida utente del lancio della piattaforma [Experience](https://docs.adobe.com/content/help/it-IT/launch/using/overview.html)

L’estensione Adobe Media Analytics (MA) aggiunge l’SDK JavaScript Media (Media 2.x SDK) di base per audio e video. Questa estensione fornisce la funzionalità per aggiungere l&#39;istanza di tracciamento `MediaHeartbeat` a un sito o a un progetto Launch.

Adobe Launch con l’estensione Media Analytics richiede quanto segue:
* Devi essere un cliente Adobe Experience Cloud.
* Devi distribuire il codice di incorporamento Launch o DTM nelle tue pagine Web.
* [Estensione Analytics](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Estensione Experience Cloud ID](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK si integra con i lettori multimediali più comunemente utilizzati.

## API Media Collection (API RESTful)

Si integra con lettori senza supporto SDK o quando non è necessaria l&#39;integrazione SDK.<br>A partire dalla release v2.2.0, gli SDK Video Heartbeat Library (VHL) sono stati rinominati in Media Analytics SDK per supportare il tracciamento audio e video. L’SDK di Media 2.2.0 è completamente retrocompatibile con la serie SDK di VHL 2.x. La modifica del nome è semplicemente una modifica della convenzione di denominazione e non rappresenta modifiche funzionali.
