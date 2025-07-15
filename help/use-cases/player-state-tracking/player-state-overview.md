---
title: Informazioni sul tracciamento dello stato del lettore
description: Scopri la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida relative all’implementazione e alla generazione di report.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 100%

---

# Informazioni sul tracciamento dello stato del lettore

Per ottimizzare l’esperienza con i prodotti e promuovere l’attività aziendale, è importante comprendere il comportamento dei clienti durante la visualizzazione dei video. Questo include il tempo trascorso all’interno dei diversi stati del lettore. È anche importante avere la possibilità di creare e misurare nuovi stati ed eventi del lettore in base alle esigenze.

Il tracciamento dello stato del lettore consente di acquisire l’interazione dell’utente durante la riproduzione utilizzando un set di variabili standard per l’intera schermata, i sottotitoli, la disattivazione dell’audio, gli effetti “picture-in-picture” e a fuoco. Il tracciamento dello stato del lettore offre anche la possibilità di creare stati del lettore personalizzati. Puoi utilizzare le variabili di tracciamento dello stato del lettore per il reporting in Analysis Workspace.

Per acquisire le modifiche allo stato del lettore, il tracciamento aggiorna i metadati della misurazione video. Ad esempio, per determinare il coinvolgimento video “true”, il tracciamento dello stato del lettore misura il tempo trascorso con il suono attivo rispetto alle visualizzazioni video passive con il suono disattivato, oppure il tempo trascorso in modalità normale rispetto alla modalità a schermo intero.

Il tracciamento dello stato del lettore offre i seguenti vantaggi:

* Fornisce variabili standard che misurano gli stati comuni come lo schermo intero o i sottotitoli
* Fornisce variabili personalizzabili per misurare gli stati personalizzati durante una sessione di riproduzione
* Misura il tempo trascorso all’interno di uno stato del lettore personalizzato
* Misura più stati che possono essere simultanei

![Tracciamento dello stato del lettore](assets/player_state_tracking.png)

## Requisiti

Il tracciamento dello stato del lettore richiede uno dei seguenti elementi per la raccolta dati:
* SDK Media JS 3.0+
* SDK Chromecast 3.0 per soluzioni Adobe Experience Cloud
* Estensione Media Analytics (per l’utilizzo con l’SDK Adobe Experience Platform (AEP))
   * Web: estensione Adobe Media Analytics (SDK 3.x) for Audio and Video 1.0+
   * Mobile: estensione Adobe Media Analytics for Audio and Video v2.0+
* API Media Collection

## Linee guida

Prima di implementare il tracciamento dello stato del lettore, considera le seguenti linee guida.

* Lo stato del lettore viene calcolato in tutti gli stati di riproduzione (senza suddivisione).
* È possibile misurare più stati del lettore contemporaneamente.
* Il numero massimo di stati del lettore che è possibile tracciare durante una riproduzione è 10.
* Le metriche dello stato del lettore vengono inviate ad Analytics per la generazione di rapporti solo sulla chiamata Chiusura del file multimediale.
* La conoscenza dello stato dell’applicazione non viene mantenuta dopo l’interruzione di uno stato. Al termine di uno stato, è necessario riavviarlo per continuare il tracciamento. Per ogni nuovo stato di riproduzione, è necessario riavviare lo stato del lettore.
* Gli stati del lettore vengono acquisiti per ogni singola sessione di riproduzione poiché non vengono calcolati tra le riproduzioni.
