---
title: Tipo di flusso
description: Rileva se ogni sessione multimediale era costituita da contenuti audio o video.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 6%

---


# Tipo di flusso

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Tipo di flusso**. Per informazioni su come raccogliere la variabile, vedere [Tipo di flusso](/help/implementation/variables/core/stream-type.md).*

>[!ENDSHADEBOX]

La dimensione **Tipo di flusso** acquisisce se ogni sessione multimediale era costituita da contenuto audio o video. È disponibile in Adobe Analytics dopo che [Media Core è abilitato](/help/reporting/media-reports-enable.md) per la suite di rapporti e in Customer Journey Analytics per qualsiasi set di dati che include dati multimediali in streaming.

## Compilazione di questa dimensione

Il tipo di flusso viene impostato dal lettore all’inizio della sessione e trasmesso alla chiamata di chiusura della sessione. Non viene calcolato o derivato. Il valore riportato corrisponde esattamente a quello inviato durante la raccolta.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.streamType` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videostreamtype` |
| Audience Manager | `c_contextdata.a.media.streamType` |

>[!IMPORTANT]
>
>Se il tipo di flusso non è impostato, la dimensione viene scompilata per quella sessione. Tali sessioni sono escluse dai segmenti integrati Solo audio e Solo video e il segmento Tutti i file multimediali in streaming verrà sottovalutato se utilizzato in combinazione con raggruppamenti del tipo di flusso.

## Elementi dimensionali

| Valore | Descrizione |
| --- | --- |
| `video` | La sessione era costituita da contenuti video. |
| `audio` | La sessione era costituita da contenuti audio come un podcast, un audiolibro o un flusso musicale. |

I valori personalizzati sono tecnicamente accettati dalle API della raccolta, ma non sono consigliati. Non corrisponderanno ai segmenti incorporati descritti di seguito e potrebbero causare rapporti non coerenti tra le implementazioni.

## Segmenti consigliati

Il tipo di flusso è la base per i segmenti [!UICONTROL Media Stream Type] incorporati in Adobe Analytics. Utilizza questi segmenti per eseguire l’ambito di qualsiasi rapporto di contenuti multimediali in streaming per un tipo di contenuto specifico:

| Segmento | Regola |
| --- | --- |
| [!UICONTROL All streaming media] | Il contenuto (ID) esiste |
| [!UICONTROL Audio only] | Il contenuto (ID) esiste e il tipo di flusso = `audio` |
| [!UICONTROL Video only] | Il contenuto (ID) esiste e il tipo di flusso != `audio` |

>[!TIP]
>
>Il segmento [!UICONTROL Video only] utilizza una regola `!=` anziché `= video` per acquisire correttamente le sessioni in cui il tipo di flusso potrebbe essere stato impostato su un valore personalizzato diverso da `audio`.
