---
title: Nome del contenuto
description: Riporta il titolo leggibile di ogni sessione multimediale.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 10%

---


# Nome del contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome contenuto**. Per informazioni su come raccogliere questa variabile, vedere [Nome contenuto](/help/implementation/variables/core/content-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome contenuto** riporta il titolo leggibile di ogni sessione multimediale.

## Compilazione di questa dimensione

Il nome descrittivo viene impostato dal lettore all’inizio della sessione. Il valore riportato corrisponde a quello inviato.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.friendlyName` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>In Adobe Analytics, questo valore corrisponde anche a una classificazione **Video name** nella dimensione [Content](content.md). L’utente è responsabile di compilare e mantenere tale classificazione separatamente. Customer Journey Analytics utilizza direttamente questa dimensione.

>[!IMPORTANT]
>
>Se il nome del contenuto non è impostato, la dimensione viene scompilata per quella sessione.

## Elementi dimensionali

Ogni elemento è il titolo letterale riportato all&#39;inizio della sessione (ad esempio, `"Blinding Light"`).
