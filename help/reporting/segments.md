---
title: Spiegazione dei segmenti di streaming multimediale
description: “Scopri i segmenti di reporting associati al tipo di flusso multimediale, compresi Segmento, Descrizione e Regola per il tipo di flusso multimediale”.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: "Media Analytics, Segmentation"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 100%

---

# Segmenti {#segments}

I segmenti ti consentono di identificare sottoinsiemi di visitatori in base a caratteristiche o interazioni con siti web. I segmenti multimediali in streaming ti consentono di identificare il tipo di flusso del visitatore, ad esempio audio, in diretta o in podcast. Per informazioni sui segmenti di Adobe Analytics, vedi [Informazioni su segmenti e contenitori](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=it) nella Guida ai componenti di Adobe Analytics.

>[!NOTE]
>
>Questi segmenti di reporting associati a Media Stream Type sono stati introdotti il 13/09/18 insieme al parametro `streamType`.

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
