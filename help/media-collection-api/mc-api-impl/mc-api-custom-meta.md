---
seo-title: Supporto per metadati personalizzati
title: Supporto per metadati personalizzati
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Supporto per metadati personalizzati{#custom-metadata-support}

Potete fornire coppie chiave-valore personalizzate per gli `sessionStart`, `chapterStart`e `adStart` gli eventi. Queste informazioni devono essere fornite nella chiave JSON `customMetadata`, posizionata accanto alla `params` chiave.

La chiave `customMetadata` JSON deve contenere un oggetto di coppie key:value. La chiave deve contenere solo caratteri alfanumerici, sottolineatura e punto/punto.

[Eventi API della raccolta MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

