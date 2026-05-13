---
title: Come impostare un SDK mobile utilizzando i tag per i servizi di Streaming Media
description: Scopri come implementare Adobe Streaming Media Services per le app mobili.
feature: Streaming Media
role: User, Admin, Developer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
TQID: https://experienceleague.adobe.com/IfnXB76Qycsic-ezOzZX4X-5RakbTQ0tlt7va6q2fZ8
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 199
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
