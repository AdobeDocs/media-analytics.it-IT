---
title: Opzioni di misurazione
description: null
uuid: null
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 10%

---


# Opzioni di misurazione{#measurement-options}

Puoi abilitare il tracciamento audio e video utilizzando Adobe Launch con l’estensione Adobe Medium Analytics, Media SDK o l’API Media Collection.

## Adobe Launch con l’estensione Adobe Medium Analytics

Adobe Launch è la soluzione di gestione tag di nuova generazione di Adobe. Launch offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate. Per generare e mantenere integrazioni personalizzate con Launch, utilizza le estensioni. Un’estensione è un pacchetto JavaScript, HTML e CSS che estende l’interfaccia utente e le funzionalità client di Launch. Per ulteriori informazioni, consulta la [Guida utente del Experience Platform Launch](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html)

L’estensione Adobe Medium Analytics (MA) aggiunge l’SDK JavaScript Media (Media 2.x SDK) di base per audio e video. Questa estensione fornisce la funzionalità per aggiungere l&#39;istanza di tracciamento `MediaHeartbeat` a un sito o a un progetto Launch.

Adobe Launch con estensione Media Analytics richiede quanto segue:
* Devi essere un cliente Adobe Experience Cloud.
* Devi distribuire il codice di incorporamento Launch o DTM sulle pagine web.
* [Estensione Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Estensione Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK si integra con i lettori multimediali più comunemente utilizzati.

## API Media Collection (API RESTful)

Si integra con lettori senza supporto SDK o quando non è necessaria l&#39;integrazione SDK.<br>A partire dalla versione v2.2.0, gli SDK della libreria Video Heartbeat (VHL) vengono rinominati SDK di Media Analytics per supportare il tracciamento audio e video. Media 2.2.0 SDK è completamente retrocompatibile con la serie VHL 2.x SDK. La modifica del nome è semplicemente una modifica nella convenzione di denominazione e non rappresenta le modifiche funzionali.
