---
title: Metriche calcolate
description: Scopri le metriche calcolate e le formule metriche nei servizi di streaming multimediale.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 72%

---

# Metriche calcolate{#calculated-metrics}

Le metriche calcolate per Adobe Streaming Media Services sono metriche personalizzate che ti consentono di ottenere dati mirati sui contenuti multimediali in streaming, come la media del tempo trascorso o la media degli annunci per flusso multimediale.

Per informazioni sulle metriche calcolate di Adobe Analytics, consulta [Metriche calcolate e metriche calcolate avanzate (derivate)](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=it) nella Guida ai componenti di Adobe Analytics.

>[!NOTE]
>
>Le metriche calcolate sono state introdotte il 13/09/18.

| Metrica | Descrizione | Formula |
|---|---|---|
| Media Annunci per flusso multimediale | Avvio annuncio per avvio file multimediali | `Ad Starts / Media Starts` |
| Media Capitoli per flusso multimediale | Avvio capitolo per avvio file multimediali | `Chapter Start / Media Starts` |
| Media Tempo trascorso dei contenuti multimediali | Tempo totale trascorso per avvio file multimediali (`HH:MM:SS`) | `Media Time Spent / Media Starts` |
| Media Tempo trascorso dei contenuti | Tempo trascorso contenuto per avvio contenuto (`HH:MM:SS`) | `Content Time Spent / Content Start` |
| Media Tempo trascorso dell’annuncio | Tempo trascorso annuncio per avvio annuncio (`HH:MM:SS`) | `Ad Time Spent / Ad Start` |
| Media Tempo trascorso capitolo | Tempo trascorso capitolo per avvio capitolo (`HH:MM:SS`) | `Chapter Time Spent / Chapter Start` |
| Tasso di completamento file multimediali | Percentuale di completamento dei contenuti rispetto ai file multimediali avviati (%) | `Content Completes/ Media Starts` |
| Tasso di completamento dei contenuti | Percentuale di completato dei contenuti rispetto all&#39;avvio dei contenuti (%) | `Content Completes / Content Starts` |
| Tasso di completamento degli annunci | Percentuale di completamento degli annunci rispetto all&#39;avvio degli annunci (%) | `Ad Completes / Ad Starts` |
| Tasso di completamento capitolo | Percentuale di completamento del capitolo rispetto all&#39;avvio del capitolo (%) | `Chapter Completes / Chapter Starts` |
| Abbandono prima della percentuale di avvio | Percentuale di abbandono prima degli avvii rispetto agli avvii dei file multimediali (%) | `Drops before Starts / Media Starts` |
| Percentuale durata pausa contenuti | Percentuale di pausa totale rispetto al tempo trascorso dei contenuti (%) | `Total Pause Duration / Content Time Spent` |
| Percentuale durata buffer dei contenuti | Percentuale di durata totale del buffer rispetto al tempo trascorso dei contenuti (% ) | `Total Buffer Duration / Content Time Spent` |
| Tempo contenuti per percentuale di avvio | Percentuale di tempo di avvio rispetto al tempo trascorso dei contenuti (%) | `Time to Start / Content Time Spent` |
| Percentuale tempo trascorso annunci | Percentuale tempo trascorso annunci e tempo trascorso dei contenuti (%) | `Ad Time Spent / Content Time Spent` |
