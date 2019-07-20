---
seo-title: Segmenti
title: Segmenti
uuid: 61906 b 8 c -3362-4463-82 be-fe 0 e 741 a 5 eb 3
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Segmenti{#segments}

>[!NOTE]
>
>These reporting segments associated with Media Stream Type were introduced on 9/13/18 along with the `streamType` parameter.

| Segmento | Descrizione | Regola |
|---|---|---|
| Tipo flusso media: Tutto | Segment all *media* stream data | " Contenuto (ID) esiste " |
| Tipo flusso media: Audio | Segment all *audio* stream data | "Content (ID) exists" AND "Media Stream Type = `audio`" |
| Tipo flusso media: Video | Segment all *video* stream data | "Content (ID) exists" AND "Media Stream Type != `audio`" |
| Tipo di contenuto multimediale: Vod | Segmentare tutti i contenuti vod | "Content Type = `vod`" |
| Tipo di contenuto multimediale: Live | Segmentare tutto il contenuto live | "Content Type = `live`" |
| Tipo di contenuto multimediale: Linear | Segmentare tutti i contenuti lineari | "Content Type = `linear`" |
| Tipo di contenuto multimediale: Podcast | Segmentare tutti i contenuti dei podcast | "Content Type = `podcast`" |
| Tipo di contenuto multimediale: Audiobook | Segmentare tutti i contenuti di audiobook | "Content Type = `audiobook`" |
| Tipo di contenuto multimediale: Aod | Segmentare tutti i contenuti aod | "Content Type = `aod`" |

