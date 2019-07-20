---
seo-title: Supporto per metadati personalizzati
title: Supporto per metadati personalizzati
uuid: df 4109 dd -9 fca -4 c 33-a 7 d 5-8 e 6 eec 257527
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Custom metadata support{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. This information must be provided in the JSON key, `customMetadata`, positioned alongside the `params` key.

The `customMetadata` JSON key should contain an object of key:value pairs. La chiave deve contenere solo caratteri alfanumerici, sottolineato e punto/punto.

[Eventi API della raccolta MA](../mc-api-ref/mc-api-events-req.md)
