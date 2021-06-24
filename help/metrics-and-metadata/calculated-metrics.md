---
title: Metriche calcolate per file multimediali in streaming
description: Scopri le metriche calcolate di Adobe Streaming Media e le formule metriche.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 2d9d4352b0fd71710a9952ba4a77f6796ea9f5cc
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 4%

---

# Metriche calcolate{#calculated-metrics}

Le metriche calcolate per lo streaming multimediale sono metriche personalizzate che ti consentono di ottenere dati mirati sullo streaming multimediale, come la media del tempo trascorso o la media degli annunci per flusso multimediale.

Per informazioni sulle metriche calcolate di Adobe Analytics, consulta [Metriche calcolate e metriche calcolate avanzate (derivate)](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=en) nella guida dei componenti di Adobe Analytics.

>[!NOTE]
>
>Queste metriche calcolate sono state introdotte il 13/09/18.

| Metrica | Descrizione | Formula |
|---|---|---|
| Media della Annunci per flusso multimediale | Avvii annunci per Media Starts | `Ad Starts / Media Starts` |
| Media della Capitoli per flusso multimediale | Inizio capitolo per Media Starts | `Chapter Start / Media Starts` |
| Media della Tempo trascorso per contenuti multimediali | Tempo totale trascorso per inizio supporto (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Media della Tempo contenuto trascorso | Tempo contenuto trascorso per inizio contenuto (HH:MM:SS) | `Content Time Spent / Content Start` |
| Media della Tempo annuncio trascorso | Tempo dell&#39;annuncio trascorso per Ad Starts (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Media della Tempo capitolo trascorso | Tempo del capitolo trascorso per inizio capitolo (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Frequenza di completamento contenuti multimediali | Tasso di contenuti completati rispetto ai file multimediali avviati (%) | `Content Completes/ Media Starts` |
| Tasso di completamento del contenuto | Tasso di contenuto completato rispetto a inizio contenuto (%) | `Content Completes / Content Starts` |
| Tasso di completamento dell’annuncio | Tasso di completamento degli annunci rispetto agli inizi degli annunci (%) | `Ad Completes / Ad Starts` |
| Tasso di completamento capitolo | Tasso di completamento del capitolo rispetto agli inizi del capitolo (%) | `Chapter Completes / Chapter Starts` |
| Abbandono prima della velocità di inizio | Tasso di calo prima degli avvii rispetto agli avvii dei file multimediali (%) | `Drops before Starts / Media Starts` |
| Frequenza di pausa contenuto | Tasso di pausa totale rispetto alla durata del contenuto (%) | `Total Pause Duration / Content Time Spent` |
| Velocità di caricamento del contenuto | Tasso di durata totale del buffer rispetto a tempo contenuto trascorso (% ) | `Total Buffer Duration / Content Time Spent` |
| Tempo di avvio del contenuto | Tasso di tempo di avvio rispetto a tempo di contenuto trascorso (%) | `Time to Start / Content Time Spent` |
| Velocità di acquisto | Tasso di tempo dell’annuncio e tempo del contenuto trascorso (%) | `Ad Time Spent / Content Time Spent` |
