---
title: Spiegazione dei segmenti di streaming multimediale
description: Scopri i segmenti di reporting associati al tipo di flusso multimediale, compresi Segmento, Descrizione e Regola per il tipo di flusso multimediale.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 75%

---

# Segmenti multimediali{#segments}

I segmenti ti consentono di identificare sottoinsiemi di visitatori in base a caratteristiche o interazioni con siti web. I segmenti multimediali in streaming ti consentono di identificare il tipo di flusso del visitatore, ad esempio audio, in diretta o in podcast. Per informazioni sui segmenti di Adobe Analytics, consulta [Informazioni sui segmenti](https://experienceleague.adobe.com/it/docs/analytics/components/segmentation/seg-overview) nella Guida ai componenti di Adobe Analytics.

| Segmento | Descrizione | Regola |
|---|---|---|
| Tipo di flusso multimediale: Tutto | Segmentazione di tutti i dati di flusso *multimediali* | “Il contenuto (ID) esiste” |
| Tipo di flusso multimediale: audio | Segmentazione di tutti i dati di flusso *audio* | “Il contenuto (ID) esiste” E “Tipo di flusso multimediale = `audio`” |
| Tipo di flusso multimediale: video | Segmentazione di tutti i dati di flusso *video* | “Il contenuto (ID) esiste” E “Tipo di flusso multimediale != `audio`” |
| Tipo di contenuto multimediale: VoD | Segmentazione di tutti i contenuti VoD | “Tipo di contenuto = `vod`” |
| Tipo di contenuto multimediale: live | Segmentazione di tutti i contenuti live | “Tipo di contenuto = `live`” |
| Tipo di contenuto multimediale: lineare | Segmentazione di tutti i contenuti lineari | “Tipo di contenuto = `linear`” |
| Tipo di contenuto multimediale: podcast | Segmentazione di tutti i contenuti Podcast | “Tipo di contenuto = `podcast`” |
| Tipo di contenuto multimediale: audiobook | Segmentazione di tutti i contenuti della cartella Audiook | “Tipo di contenuto = `audiobook`” |
| Tipo di contenuto multimediale: AoD | Segmentazione di tutti i contenuti AoD | “Tipo di contenuto = `aod`” |
