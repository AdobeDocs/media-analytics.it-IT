---
title: Visualizzatori simultanei di contenuti multimediali
description: null
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Visualizzatori simultanei di contenuti multimediali{#media-concurrent-viewers}

Il dashboard Visualizzatori simultanei di contenuti multimediali mostra i visualizzatori simultanei in un giorno. I dati possono essere filtrati in base al contenuto, al tipo di dispositivo o al Paese.

>[!TIP]
>
> Questo rapporto si basa su sessioni multimediali attive simultanee.  Per visualizzare i visualizzatori simultanei per visitatore univoco, con le funzionalità aggiuntive per applicare un segmento, suddividerli e confrontarli, utilizza il pannello [Visualizzatori simultanei di contenuti multimediali in Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html).


![](assets/video-concurrent-viewers.png)

## Funzioni del rapporto {#report-features}

Di seguito sono riportate alcune caratteristiche di questo rapporto:

* Questo non è in tempo reale. Ha una latenza normale Adobe Analytics.
* La relazione copre un arco temporale di 24 ore. L’asse x è basato sul fuso orario della suite di rapporti.
* Mostra i visualizzatori simultanei con granularità al minuto.
* Esiste un *Report visualizzatori simultanei di contenuti multimediali* che mostra quanti visualizzatori visualizzano o ascoltano in tutti i contenuti.
* Nel rapporto *Media Detail* è presente un rapporto per visualizzatori simultanei che mostra quanti visualizzatori visualizzano o ascoltano un elemento multimediale specifico.
* Il rapporto funziona solo in un giorno.
* Il cliente può esaminare i rapporti storici dei visualizzatori simultanei (limitati a un solo giorno).

## Limitazioni {#limitations}

Di seguito sono riportate alcune limitazioni per questo rapporto:

* Se l’intervallo selezionato non è un giorno intero, non verranno visualizzati dati.
* Non è possibile esportare i dati, ad esempio il ReportBuilder.
* Non è possibile presentare i dati in un formato tabella.
* Non puoi inviare un rapporto tramite e-mail.
* Anche se non si tiene traccia degli annunci, è necessario riattivare il tracciamento dei contenuti multimediali e selezionare il modulo Media Ad.
* Questa funzionalità fornirà dati precisi quando si utilizza una libreria heartbeat con funzionalità di tracciamento in pausa.
