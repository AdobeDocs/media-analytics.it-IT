---
title: Spiegazione dei segmenti di streaming multimediale
description: '"Scopri i segmenti di reporting associati al tipo di flusso multimediale, compresi Segmento, Descrizione e Regola per il tipo di flusso multimediale."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics, Segmentazione"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 14%

---

# Segmenti{#segments}

I segmenti ti consentono di identificare sottoinsiemi di visitatori in base a caratteristiche o interazioni con siti web. I segmenti multimediali in streaming ti consentono di identificare il tipo di flusso del visitatore, ad esempio audio, in diretta o in podcast. Per informazioni sui segmenti di Adobe Analytics, consulta [Informazioni su segmenti e contenitori](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=en) nella Guida dei componenti di Adobe Analytics.

>[!NOTE]
>
>Questi segmenti di reporting associati a Media Stream Type sono stati introdotti il 13/09/18 insieme al parametro `streamType` .

| Segmento | Descrizione | Regola |
|---|---|---|
| Tipo di flusso multimediale: Tutto | Segmenta tutti i dati del flusso *media* | &quot;Contenuto (ID) esiste&quot; |
| Tipo di flusso multimediale: Audio | Segmenta tutti i dati di streaming *audio* | &quot;Contenuto (ID) esiste&quot; E &quot;Tipo flusso multimediale = `audio`&quot; |
| Tipo di flusso multimediale: Video | Segmenta tutti i dati del flusso *video* | &quot;Contenuto (ID) esiste&quot; E &quot;Tipo flusso multimediale != `audio`&quot; |
| Tipo di contenuto multimediale: VoD | Segmenta tutti i contenuti VoD | &quot;Tipo di contenuto = `vod`&quot; |
| Tipo di contenuto multimediale: Live | Segmenta tutti i contenuti live | &quot;Tipo di contenuto = `live`&quot; |
| Tipo di contenuto multimediale: Lineare | Segmentazione di tutti i contenuti lineari | &quot;Tipo di contenuto = `linear`&quot; |
| Tipo di contenuto multimediale: Podcast | Segmenta tutti i contenuti Podcast | &quot;Tipo di contenuto = `podcast`&quot; |
| Tipo di contenuto multimediale: Audiobook | Segmenta tutti i contenuti della cartella Audiook | &quot;Tipo di contenuto = `audiobook`&quot; |
| Tipo di contenuto multimediale: AoD | Segmenta tutti i contenuti AoD | &quot;Tipo di contenuto = `aod`&quot; |
