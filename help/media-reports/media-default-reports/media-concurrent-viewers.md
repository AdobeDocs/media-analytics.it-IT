---
title: 'Visualizzatori simultanei di contenuti multimediali '
description: “Scopri il dashboard dei visualizzatori simultanei di contenuti multimediali utilizzata per visualizzare i visualizzatori simultanei nell’arco di una giornata. I dati possono essere filtrati in base al contenuto, al tipo di dispositivo o al Paese.”
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Media Analytics, Reports & Analytics Basics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '290'
ht-degree: 100%

---

# Visualizzatori simultanei di contenuti multimediali {#media-concurrent-viewers}

Il dashboard dei visualizzatori simultanei di contenuti multimediali mostra i visualizzatori simultanei nell’arco di una giornata. I dati possono essere filtrati in base al contenuto, al tipo di dispositivo o al Paese.

>[!TIP]
>
> Questo rapporto si basa su sessioni multimediali attive simultanee. Per visualizzare i visualizzatori simultanei per visitatore univoco, con le funzionalità aggiuntive per applicare, suddividere e confrontare un segmento, utilizza la variabile [Pannello visualizzatori simultanei di contenuti multimediali in Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=it).

![](assets/video-concurrent-viewers.png)

## Caratteristiche del rapporto {#report-features}

Di seguito sono riportate alcune caratteristiche di questo rapporto:

* Il rapporto non è in tempo reale. Ha una latenza normale di Adobe Analytics.
* Il rapporto copre un intervallo temporale di 24 ore. L’asse x corrisponde all’ora del giorno basata sul fuso orario della suite di rapporti.
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
* Anche se non si tiene traccia degli annunci, è necessario riattivare il tracciamento dei contenuti multimediali e selezionare il modulo relativo all’annuncio multimediale.
* Questa funzionalità fornirà dati precisi quando si utilizza una libreria heartbeat con funzionalità di tracciamento in pausa.
