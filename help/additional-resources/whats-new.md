---
title: Novità di Media Analytics
description: Novità include informazioni sulle nuove funzioni e notifiche.
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 59%

---


# Novità di Media Analytics{#whats-new}

![Banner](assets/media_analytics_banner.png)


Questa pagina descrive nuove funzioni, correzioni e avvisi importanti relativi a Media Analytics. Inoltre, mette in evidenza nuova documentazione, corsi di formazione e tutorial video per aiutarti a ottenere il massimo da Media Analytics.


## Note sulla versione

Note sulla versione di Adobe Experience Cloud

Le note sulla versione di Adobe Experience Cloud descrivono nuove funzioni, correzioni e avvisi importanti relativi a Adobe Experience Cloud. Sono incluse le ultime modifiche apportate a Media Analytics. Inoltre mette in evidenza documentazione, corsi di formazione ed esercitazioni video utili per ottenere il massimo da Experience Cloud.

## Nuove funzionalità

| Funzione | [Disponibilità generale](https://experienceleague.adobe.com/docs/analytics/release-notes/releases.html?lang=it) - data di Target | Descrizione |
| ----------- | ---------- | ---------- |
| [Pannello Visualizzatori simultanei di contenuti multimediali](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 17 settembre 2020 | Il pannello Visualizzatori simultanei di contenuti multimediali in Workspace consente di comprendere dove si è verificato il picco di concorrenza o in che punto i visitatori hanno abbandonato il contenuto. Fornisce informazioni utili sulla qualità dei contenuti e sul livello di coinvolgimento degli utenti che li visualizzano, e aiuta a risolvere problemi o a pianificare tenendo conto di volumi/scala. |
| [Piattaforme e dispositivi supportati](../getting-started/supported-devices.md) | 18 giugno 2020 | La [!UICONTROL Media Launch Extension] con AEP Mobile SDK ora supporta i seguenti dispositivi OTT:<ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul> |
| [Tracciare lo stato del lettore](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html) | 29 maggio 2020 | I clienti [!UICONTROL Media Analytics] possono visualizzare le interazioni dei visualizzatori durante la riproduzione facendo uso di un set standard di variabili della soluzione per visualizzazione a schermo intero, sottotitoli, modalità muto, immagine nell’immagine e messa a fuoco. È inoltre possibile creare degli stati del lettore personalizzati. [!UICONTROL Player State Tracking] sono ora disponibili per la generazione di rapporti in [!UICONTROL Analysis Workspace]. Questa funzione richiede uno dei seguenti elementi: <ul><li>SDK di [!DNL JavaScript] Media 3.0 o versione successiva</li><li>Per l’utilizzo con l’SDK di [!DNL Adobe Experience Platform] (AEP):</li><li>[!UICONTROL Media Analytics Extension] (per il web): [!UICONTROL Adobe Media Analytics] (3.x SDK) per audio e video v1.0 o versione successiva</li><li>[!UICONTROL Media Analytics Extension] (per dispositivi mobili): [!UICONTROL Adobe Media Analytics for Audio] e video v2.0 o versione successiva</li><li>[!UICONTROL Media Collection]</li></ul> |


## Notifiche importanti

| Funzione | [Disponibilità generale](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) - data di Target | Descrizione |
| ----------- | ---------- | ---------- |
| [Piattaforme e dispositivi supportati](../getting-started/supported-devices.md) | 31 agosto 2021 | Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe terminerà anche il supporto per l’SDK di Media Analytics per iOS e Android. Per ulteriori informazioni, consulta Domande frequenti sull’SDK di Media Analytics relative alla fine del supporto. |
| [Domande frequenti sull’SDK di Media Analytics relative alla fine del supporto](sdk-implement/end-of-support-faqs.md) | Autunno 2019 | Sviluppo delle funzioni terminato per gli SDK Media Analytics per iOS e Android.  Le nuove funzioni introdotte a partire dall’autunno 2019 vengono abilitate utilizzando le estensioni Media Analytics e l’API Media Collection. |
| [Panoramica dei contenuti multimediali](media-overview.md) | 20 febbraio 2019 | Adobe supporta solo TLS 1.1 o versione successiva. Con questa modifica, Adobe non raccoglierà più dati dagli utenti finali con dispositivi o browser Web meno recenti che utilizzano TLS 1.0. |
| [Piattaforme e dispositivi supportati](../getting-started/supported-devices.md) | 19 febbraio 2019 | Di seguito sono elencate le versioni minime supportate per ogni SDK della piattaforma. <br>- iOS: iOS 6+ <br>- Android: Android 5.0+ - Lollipop <br>- Cromatura: v22+<br>- Mozilla: v27+<br>- Safari: v7+<br>- IE: v1+ |
| [Parametri audio e video ](metrics-and-metadata/audio-video-parameters.md) | 7 febbraio 2019 | Adobe Analytics for Video and Audio ha rilasciato una modifica al nome di una metrica. <i>Inizia file multimediale</i> adesso è denominato <i>Avvia file multimediale</i>. Questa modifica ha lo scopo di riflettere gli standard di settore in fatto di metriche e reporting e di rendere la metrica più semplice da identificare nella reportistica. |
| [Parametri audio e video ](metrics-and-metadata/audio-video-parameters.md) | 13 settembre 2018 | È stata apportata una modifica alle etichette per alcune dimensioni, metriche e rapporti, per consentire il tracciamento tra contenuti di analisi video e audio. Le etichette modificate includono: *Inizia video* modificata in *Avvia file multimediale*, *lunghezza video* modificata in *lunghezza contenuto* e *nome video* modificata in *nome contenuto*. I rapporti video in Reports and Analytics sono stati tutti aggiornati per l’utilizzo del nome “file multimediale” al posto di “video”. Le modifiche apportate all’etichetta non hanno modificato la raccolta dati o i dati storici. Tieni presente queste modifiche nel caso in cui le utilizzi all’interno del Report Builder oppure in qualsiasi altro dispositivo automatizzato per l’estrazione di dati esterno che potrebbe esserne influenzato. |




<!-- | title | date | description | -->