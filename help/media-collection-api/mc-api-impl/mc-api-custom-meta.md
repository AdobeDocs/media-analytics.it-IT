---
title: Supporto per metadati personalizzati
description: Supporto per metadati personalizzati
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Supporto per metadati personalizzati{#custom-metadata-support}

Puoi fornire coppie chiave:valore personalizzate sugli eventi `sessionStart`, `chapterStart` e `adStart` . Queste informazioni devono essere fornite nella chiave JSON, `customMetadata`, posizionata accanto alla chiave `params` .

La chiave `customMetadata` JSON deve contenere un oggetto di coppie chiave:valore. La chiave deve contenere solo caratteri alfanumerici, sottolineatura e punto/punto.

[Eventi API della raccolta MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
