---
title: Supporto per metadati personalizzati
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Supporto per metadati personalizzati{#custom-metadata-support}

Potete fornire coppie chiave-valore personalizzate per gli `sessionStart`, `chapterStart`e `adStart` gli eventi. Queste informazioni devono essere fornite nella chiave JSON `customMetadata`, posizionata accanto alla `params` chiave.

La chiave `customMetadata` JSON deve contenere un oggetto di coppie key:value. La chiave deve contenere solo caratteri alfanumerici, sottolineatura e punto/punto.

[Eventi API della raccolta MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

