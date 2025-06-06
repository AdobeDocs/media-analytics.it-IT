---
title: Note sulla versione di Streaming Media Collection
description: Consulta le note sulla versione di Streaming Media Collection.
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 78%

---

# Note sulla versione di Streaming Media Collection (maggio 2023)

**Ultimo aggiornamento**: giovedì 29 maggio 2024

## Risorse correlate

Per informazioni sulle nuove funzioni e correzioni, nonché informazioni importanti per gli amministratori, consulta le risorse seguenti.

* [Note sulla versione di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=it)
* [Note sulla versione di Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=it)
* Scopri gli ultimi aggiornamenti sulle versioni dei [prodotti Adobe Experience Cloud](https://business.adobe.com/it/products/adobe-experience-cloud-products.html)

* [Tutorial su Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=it)

## *Note sulla versione corrente*

## Funzioni nuove e aggiornate di Adobe Streaming Media Collection {#cja-features}

| Funzione | Descrizione | Data prevista |
| ----------- | ---------- | ------- |
| Inviare dati web a un Edge Network di Adobe Experience Platform con Web SDK | È ora possibile [utilizzare Adobe Experience Platform Web SDK per inviare dati Web multimediali in streaming all&#39;Edge Network di Adobe Experience Platform](/help/implementation/edge/edge-web-sdk.md), consentendo di creare più campagne personalizzate e fornire più contenuti personalizzati, con conseguente aumento dei dati di tracciamento su cui generare i rapporti.<p>Questo miglioramento fornisce un metodo di raccolta unificato per le implementazioni web in tutte le soluzioni Platform, come Customer Journey Analytics, RT-CDP, AJO e inoltro eventi. In precedenza, l’unico modo per inviare i dati web multimediali in streaming alla rete Edge era utilizzare l’API Media Edge. | 29 maggio 2024 |
| Inviare dati Roku a Adobe Experience Platform Edge | Ora, quando [installi Streaming Media Collection con Experience Platform Edge](/help/implementation/edge/implementation-edge.md), puoi utilizzare Adobe Experience Platform Roku SDK per inviare dati multimediali in streaming a Adobe Experience Platform. | 12 aprile 2024 |
| Media Collection: integrazione con Experience Edge (API e Mobile SDK) | Ora puoi utilizzare l’API di Experience Edge e Mobile SDK per implementare Adobe Streaming Media Collection, consentendoti di creare campagne più personalizzate e fornire contenuti più personalizzati, con conseguente aumento dei dati di tracciamento da includere nei rapporti.<p>Questo miglioramento fornisce un metodo di raccolta unificato su tutte le soluzioni, ad esempio reporting di Customer Journey Analytics, RT-CDP, AJO e inoltro di eventi.  [Ulteriori informazioni](/help/implementation/edge/implementation-edge.md) | sabato 12 maggio 2023 |
| Pannello Visualizzatori simultanei di contenuti multimediali | Scopri dove si verificano picchi di concorrenza o abbandoni. Ottieni informazioni approfondite sulla qualità dei contenuti e sul livello di coinvolgimento dell’utente, utili anche per risolvere problemi o pianificare volumi e scala. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=it) | 9 agosto 2022 |
| Pannello Tempo trascorso su contenuti multimediali | La funzione Tempo trascorso su contenuti multimediali fornisce insight utili sul coinvolgimento degli utenti. Consente alle organizzazioni di media di ottenere informazioni più approfondite e dettagliate sul coinvolgimento degli utenti minuto per minuto attraverso un’analisi avanzata del tempo trascorso con funzionalità di ripartizione giornaliera. È possibile osservare il tempo impiegato per visualizzare i flussi multimediali in un determinato momento. È possibile suddividere la durata della riproduzione in base a granularità diverse, tra cui nuove granularità di 5, 15 e 30 minuti. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=it) | 9 agosto 2022 |
| Condividere le annotazioni nelle scorecard per dispositivi mobili | Puoi visualizzare le annotazioni create in Workspace nelle scorecard per dispositivi mobili. Ciò ti consente di condividere dettagli sui dati contestuali e informazioni approfondite sull’organizzazione e sulle campagne direttamente all’interno dei progetti delle scorecard per dispositivi mobili, visualizzabili nell’app mobile delle dashboard di Analytics. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=it) | 15 giugno 2022 |
| Report Builder per aggiornamenti Customer Journey Analytics | Include funzioni quali pianificazione e gestione dei blocchi dati. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=it) | 18 maggio 2022 |
| Annotazioni in Workspace | Le annotazioni in Workspace consentono di comunicare in modo efficace dettagli sui dati contestuali a beneficio degli utenti in tutta l’organizzazione. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=it) | L’implementazione graduale inizia il 23 marzo 2022 |
| Modalità anteprima dei progetti scorecard per dispositivi mobili | Avvia un’anteprima per vedere come si presenterà la scorecard per dispositivi mobili nell’app delle dashboard di Analytics, direttamente dal generatore di scorecard. La modalità di anteprima consente agli utenti di interagire con filtri e grafici nello stesso modo in cui farebbero nell’app, fornendo un’anteprima dell’esperienza prima di salvare e condividere la scorecard. Gli utenti possono inoltre utilizzare il selettore dispositivi in modalità anteprima per vedere come si presenterà la scorecard sui diversi dispositivi. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=it#preview) | 16 febbraio 2022 |


## Funzioni nuove e aggiornate di Adobe Streaming Media Collection {#sm-features}

| Funzione | Descrizione | Data prevista |
| ----------- | ---------- | ------- |
| Tracciamento di più stati del lettore | Utilizza l’API Media Collection per implementare il tracciamento di più stati del lettore. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=it) | Settembre 2022 |
| Campi XDM rinominati | Nomi di campi XDM rinominati per coerenza:<br>* Parametri per audio e video<br>* Parametri per annunci<br>* Parametri per capitoli<br>* Parametri per lo stato del lettore<br>* Parametri di qualità | Settembre 2022 |
| Riferimento a Device Co-op | È stato rimosso il riferimento ad Adobe Experience Cloud Device Co-op e ai requisiti del servizio Experience Cloud ID. | Agosto 2022 |
| Nomi di campi e percorsi XDM aggiornati per la raccolta e il reporting | È stato aggiornato quanto segue:<br>* Parametri per audio e video<br>* Parametri per annunci<br>* Parametri per capitoli<br>* Parametri per lo stato del lettore<br>* Parametri di qualità | Agosto 2022 |
| Pubblico medio per minuto | I clienti Media Analytics possono utilizzare il pannello Pubblico medio per minuto per comprendere meglio il consumo medio dei loro contenuti. <br>Il pubblico medio per minuto consente di confrontare la programmazione di qualsiasi durata o genere. Inoltre, i clienti possono confrontare o aggiungere questo pubblico medio per minuto digitale alle metriche medie per minuto per TV lineare. Questo pannello offre maggiore flessibilità per misurare il pubblico medio in periodi di tempo personalizzati, nonché quando la classificazione della durata è stata aggiornata.  [Ulteriori informazioni](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=it) | 16 marzo 2022 |
| Pannello Tempo trascorso su contenuti multimediali | Scopri in che modo il pannello Tempo trascorso su contenuti multimediali consente agli utenti che usano contenuti multimediali di comprendere i propri spettatori in base al tempo di visualizzazione durante il giorno secondo una determinata granularità. <br>[Pannello Tempo trascorso su contenuti multimediali (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=it) | Gennaio 2022 |


## *Note sulle versioni precedenti*

| Funzione | Descrizione | Data aggiornamento o prevista |
| ----------- | ---------- | -------------- |
| Pannello Tempo trascorso su contenuti multimediali | La funzione Tempo trascorso su contenuti multimediali di Adobe Streaming Media fornisce insight utili sul coinvolgimento degli utenti. Consente alle organizzazioni di media di ottenere informazioni più approfondite e dettagliate sul coinvolgimento degli utenti minuto per minuto attraverso un’analisi avanzata del tempo trascorso con funzionalità di ripartizione giornaliera. È possibile osservare il tempo impiegato per visualizzare i flussi multimediali in un determinato momento. Puoi suddividere la durata della riproduzione in base a diverse granularità, tra cui nuove granularità di 5, 15 e 30 minuti. [Ulteriori informazioni...](/help/reporting/workspace/media-playback-time-spent.md) | Settembre 2021 |
| Pannello Visualizzatori simultanei di contenuti multimediali in Analytics Workspace | Scopri dove si verificano picchi di concorrenza o abbandoni. Ottieni informazioni approfondite sulla qualità dei contenuti e sul livello di coinvolgimento dell’utente, utili anche per risolvere problemi o pianificare volumi e scala. [Ulteriori informazioni](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Pannello Visualizzatori simultanei di contenuti multimediali in Analytics Workspace (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=it#analysis-workspace) | Settembre 2020 <br><br><br>Gennaio 2021 |
| Piattaforme e dispositivi supportati | L’estensione Media Launch con SDK di AEP ora supporta i seguenti dispositivi OTT: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Giugno 2020 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
