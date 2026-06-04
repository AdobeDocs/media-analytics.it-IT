---
title: Canale del contenuto
description: Segnala la stazione di distribuzione, la rete o la proprietà in cui è stata riprodotta ogni sessione.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# Canale del contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Canale contenuto**. Per informazioni su come raccogliere questa variabile, consulta [Canale contenuto](/help/implementation/variables/core/content-channel.md).*

>[!ENDSHADEBOX]

La dimensione **Canale contenuto** riporta la stazione di distribuzione, la rete o la proprietà in cui è stata riprodotta ogni sessione. Utilizzalo per interrompere la riproduzione per rete o sezione di una proprietà.

## Compilazione di questa dimensione

Il canale viene impostato dal lettore all’inizio della sessione e persiste per la sua durata.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.channel` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Se channel non è impostato, la dimensione viene scompilata per quella sessione.

## Elementi dimensionali

Ogni elemento rappresenta la stringa letterale impostata all&#39;inizio della sessione. Qualsiasi stringa viene accettata. I valori tipici sono un nome di rete, una parte del percorso di un sito o un identificatore di proprietà interno.
