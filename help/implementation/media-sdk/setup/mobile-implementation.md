---
title: Come configurare Mobile SDK utilizzando i tag per Streaming Media
description: Scopri come implementare Adobe Streaming Media per le app per dispositivi mobili.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: a7d897c6f6fbc6ed0d5b71f5801ab18ee21f0411
workflow-type: ht
source-wordcount: '187'
ht-degree: 100%

---

# Installare Mobile SDK {#install-mobile-sdks}

Per implementare Streaming Media per le app per dispositivi mobili su Android o iOS, installa e configura quanto segue:

* **Adobe Experience Platform Mobile SDK**

   Per raccogliere i dati, utilizza Tag in Adobe Experience Platform. Tag in Adobe Experience Platform è una soluzione di gestione dei tag che consente di distribuire il codice Analytics insieme ad altri requisiti di assegnazione tag.

* **Media SDK per Android** o **Media SDK per iOS**

* **Estensione Adobe Media Analytics for Audio and Video**

Per scaricare gli SDK e per ulteriori risorse di documentazione, consulta [Ottenere Media SDK ed estensioni tramite tag e SDK OTT](/help/getting-started/download-sdks.md)

* **Ottenere parametri di configurazione validi**

   Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.

* **Includi le seguenti API nel lettore multimediale**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.

   * *Un’API che fornisce informazioni sul lettore*: questo include informazioni sulla riproduzione in corso, quali il nome del file multimediale, la posizione dell’indicatore di riproduzione, gli annunci o il capitolo.
