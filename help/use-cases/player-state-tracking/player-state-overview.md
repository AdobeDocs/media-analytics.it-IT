---
title: Informazioni sul tracciamento dello stato del lettore
description: Scopri la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida relative all’implementazione e alla generazione di report.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/R4ByVgEI65JyN-LFdMX1CCBs4zVyppVgebN9OJxJNMM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 409
ht-degree: 100%

---

# Informazioni sul tracciamento dello stato del lettore

Per ottimizzare l’esperienza con i prodotti e promuovere l’attività aziendale, è importante comprendere il comportamento dei clienti durante la visualizzazione dei video. Questo include il tempo trascorso all’interno dei diversi stati del lettore.  È anche importante avere la possibilità di creare e misurare nuovi stati ed eventi del lettore in base alle esigenze.

Il tracciamento dello stato del lettore consente di acquisire l’interazione dell’utente durante la riproduzione utilizzando un set di variabili standard per l’intera schermata, i sottotitoli, la disattivazione dell’audio, gli effetti “picture-in-picture” e a fuoco.  Il tracciamento dello stato del lettore offre anche la possibilità di creare stati del lettore personalizzati. Puoi utilizzare le variabili di tracciamento dello stato del lettore per il reporting in Analysis Workspace.

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
