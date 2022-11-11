---
title: Come impostare un SDK per dispositivi mobili utilizzando i tag per gli elementi multimediali in streaming
description: Scopri come implementare Adobe Streaming Media per le app mobili.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 20%

---

# Installare gli SDK di Mobile {#install-mobile-sdks}

Per implementare lo streaming media per le app mobili su Android o iOS, installa e configura quanto segue:

* **Adobe Experience Platform Mobile SDK**

   Per raccogliere i dati, utilizza i tag in Adobe Experience Platform. I tag in Adobe Experience Platform è una soluzione di gestione tag che consente di distribuire il codice Analytics insieme ad altri requisiti di assegnazione tag.

* **Media SDK per Android** o **Media SDK per iOS**

* **Estensione Adobe Media Analytics for Audio and Video**

Per scaricare gli SDK e per ulteriori risorse di documentazione, consulta [Ottenere SDK per contenuti multimediali, estensioni tramite tag e SDK OTT](/help/getting-started/download-sdks.md)

* **Ottenere parametri di configurazione validi**

   Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.

* **Includere le seguenti API nel lettore multimediale**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.

   * *API che fornisce informazioni sul lettore* - Comprende informazioni sulla riproduzione in corso, quali il nome del supporto, la posizione della testina di riproduzione, gli annunci o il capitolo.
