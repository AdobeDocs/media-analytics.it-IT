---
seo-title: Segmenti
title: Segmenti
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Segmenti{#segments}

>[!NOTE]
>
>Questi segmenti di reporting associati a Media Stream Type sono stati introdotti il 13/9/18 insieme al `streamType` parametro.

| Segmento | Descrizione | Regola |
|---|---|---|
| Tipo di flusso multimediale: Tutto | Segmentazione di tutti i dati del flusso *multimediale* | "Contenuto (ID) esistente" |
| Tipo di flusso multimediale:Audio | Segmentazione di tutti i dati del flusso *audio* | "Content (ID) exists" E "Media Stream Type = `audio`" |
| Tipo di flusso multimediale: Video | Segmentazione di tutti i dati del flusso *video* | "Content (ID) exists" E "Media Stream Type != `audio`" |
| Tipo di contenuto multimediale: VoD | Segmentazione di tutti i contenuti VoD | "Tipo di contenuto = `vod`" |
| Tipo di contenuto multimediale:Live | Segmentazione di tutti i contenuti live | "Tipo di contenuto = `live`" |
| Tipo di contenuto multimediale:Linear | Segmentazione di tutti i contenuti lineari | "Tipo di contenuto = `linear`" |
| Tipo di contenuto multimediale: Podcast | Segmentazione di tutti i contenuti Podcast | "Tipo di contenuto = `podcast`" |
| Tipo di contenuto multimediale: Audiobook | Segmentazione di tutti i contenuti Audiobook | "Tipo di contenuto = `audiobook`" |
| Tipo di contenuto multimediale: AoD | Segmentazione di tutti i contenuti AoD | "Tipo di contenuto = `aod`" |

