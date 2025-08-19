---
title: Come impostare un SDK mobile utilizzando i tag per i servizi di Streaming Media
description: Scopri come implementare Adobe Streaming Media Services per le app mobili.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 70%

---

# Installare Mobile SDK {#install-mobile-sdks}

Per implementare i servizi multimediali in streaming di Adobe per le app mobili su Android o iOS, installa e configura quanto segue:

* **Adobe Experience Platform Mobile SDK**

  Per raccogliere i dati, utilizzare una delle seguenti opzioni:
   * Tag in Adobe Experience Platform. Tag in Adobe Experience Platform è una soluzione di gestione dei tag che consente di distribuire il codice Analytics insieme ad altri requisiti di assegnazione tag.
   * Adobe Experience Platform Edge

* **Media SDK per Android** o **Media SDK per iOS**

* **Estensione Adobe Media Analytics for Audio and Video**

Per scaricare gli SDK e per ulteriori risorse di documentazione, consulta [Ottenere Media SDK ed estensioni tramite tag e SDK OTT](/help/getting-started/download-sdks.md)

* **Ottenere parametri di configurazione validi**

  Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.

* **Includi le seguenti API nel lettore multimediale**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.

   * *Un’API che fornisce informazioni sul lettore*: questo include informazioni sulla riproduzione in corso, quali il nome del file multimediale, la posizione dell’indicatore di riproduzione, gli annunci o il capitolo.
