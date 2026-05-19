---
title: Visualizzatori simultanei di contenuti multimediali
description: Scopri la dashboard dei visualizzatori simultanei di contenuti multimediali utilizzata per visualizzare i visualizzatori simultanei nell’arco di una giornata. I dati possono essere filtrati in base al contenuto, al tipo di dispositivo o al paese.
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Streaming Media, Workspace Basics
role: User, Admin
TQID: https://experienceleague.adobe.com/8pqoGpVCRXvovD-cNPNOvFQFvJco3sWUq3SuXEOVeJI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 299
ht-degree: 90%

---

# Rapporti sui visualizzatori simultanei di contenuti multimediali {#media-concurrent-viewers}

Il dashboard dei visualizzatori simultanei di contenuti multimediali mostra i visualizzatori simultanei nell’arco di una giornata. I dati possono essere filtrati in base al contenuto, al tipo di dispositivo o al Paese.

>[!TIP]
>
> Questo rapporto si basa su sessioni multimediali attive simultanee.  Per visualizzare i visualizzatori simultanei per visitatore univoco, con le funzionalità aggiuntive per applicare, suddividere e confrontare un segmento, utilizza la variabile [Pannello visualizzatori simultanei di contenuti multimediali in Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=it).
>

![](assets/video-concurrent-viewers.png)

## Caratteristiche del rapporto {#report-features}

Di seguito sono riportate alcune caratteristiche di questo rapporto:

* Il rapporto non è in tempo reale. Ha una latenza normale di Adobe Analytics.
* Il rapporto copre un arco temporale di 24 ore. L’asse x corrisponde all’ora del giorno basata sul fuso orario della suite di rapporti.
* Mostra i visualizzatori simultanei con granularità al minuto.
* È disponibile un *Rapporto dei visualizzatori simultanei di contenuti multimediali* che mostra quanti utenti stanno guardando oppure ascoltando tutti i contenuti.
* È disponibile un Rapporto sui visualizzatori simultanei all’interno del rapporto sui *Dettagli dei contenuti multimediali* che mostra quanti utenti stanno guardando oppure ascoltando un elemento multimediale specifico.
* Il rapporto funziona soltanto per una giornata.
* Il cliente può esaminare i rapporti storici dei visualizzatori simultanei (limitati a una sola giornata).

## Limitazioni {#limitations}

Di seguito sono riportate alcune limitazioni per questo rapporto:

* Se l’intervallo selezionato non corrisponde a un’intera giornata, non saranno visualizzati dati.
* Non è possibile esportare i dati, ad esempio il ReportBuilder.
* Non è possibile presentare i dati in un formato tabella.
* Non puoi inviare un rapporto tramite e-mail.
* Anche se non si tiene traccia degli annunci, è necessario abilitare di nuovo il tracciamento dei contenuti multimediali e selezionare il modulo relativo all’annuncio multimediale.
* Questa funzionalità fornirà dati precisi quando si utilizza una libreria heartbeat con funzionalità di tracciamento in pausa.
