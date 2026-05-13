---
title: Nome del lettore dell’annuncio
description: Segnala quale lettore ha eseguito il rendering di ciascun annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 8%

---


# Nome del lettore dell’annuncio

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome del lettore dell&#39;annuncio**. Per informazioni su come raccogliere questa variabile, consulta [Il nome del lettore dell&#39;annuncio](/help/implementation/variables/ads/ad-player-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome del lettore dell&#39;annuncio** riporta il rendering di ciascun annuncio eseguito dal lettore (ad esempio, `"Freewheel"`, `"Google IMA"`). Il lettore di annunci può differire dal lettore di contenuto principale quando gli annunci sono uniti da un servizio di inserimento di annunci lato server.

## Compilazione di questa dimensione

Il nome del lettore dell&#39;annuncio viene impostato dal lettore a ogni evento `media.adStart`.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.playerName` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadplayername, post_videoadplayername` |

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale del lettore di annunci riportato in `media.adStart`.
