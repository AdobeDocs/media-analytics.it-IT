---
title: MVPD
description: Segnala il provider via cavo, satellite o virtuale tramite il quale l'utente ha eseguito l'autenticazione.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 8%

---


# MVPD

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **MVPD**. Per informazioni su come raccogliere questa variabile, vedere [MVPD](/help/implementation/variables/standard-metadata/mvpd.md).*

>[!ENDSHADEBOX]

La dimensione **MVPD** (distributore di programmazione video multicanale) segnala il provider tramite il quale l&#39;utente ha eseguito l&#39;autenticazione tramite Adobe Pass (ad esempio, `"Comcast"` o `"DirecTV"`). Utilizzalo per interrompere il coinvolgimento da parte del provider di autenticazione.

## Compilazione di questa dimensione

MVPD viene impostato dal lettore all’inizio della sessione quando il contenuto viene inviato dietro Adobe Pass.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pass.mvpd` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videomvpd, post_videomvpd` |

## Elementi dimensionali

Ogni elemento è il nome letterale di MVPD riportato all’inizio della sessione. Utilizza l’identificatore canonico Adobe Pass MVPD per provider, in modo che i dati vengano aggregati a una singola riga per provider.
