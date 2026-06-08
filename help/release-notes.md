---
title: Note sulla versione di Streaming Media Services
description: Consulta le note sulla versione di Streaming Media Services.
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 722
ht-degree: 36%

---

# Note sulla versione di Streaming Media Services

**Ultimo aggiornamento**: 4 giugno 2026

## 2026

| Funzione | Descrizione | Data |
| --- | --- | --- |
| **Dati pianificazione supporto** | Carica i dati pianificati per contenuti live passati per tenere traccia del pubblico per programma o segmento. I tipi di contenuto supportati includono:<ul><li>Piattaforme FAST (Free Ad Supported TV)</li><li>Flussi locali</li><li>Sport live</li></ul>Per ulteriori informazioni, vedi il caso d&#39;uso [Carica dati di pianificazione per tenere traccia del contenuto live](/help/use-cases/track-schedule-data.md). | Inizio rollout: 29 ottobre 2025<p>Disponibilità generale: ottobre 2026</p> |

## 2025

| Funzione | Descrizione | Data |
| --- | --- | --- |
| **`mediaTimed`campo XDM obsoleto** | L&#39;oggetto XDM `mediaTimed` è obsoleto a favore di `mediaReporting` percorsi di campo. I clienti che hanno implementato il connettore di origine di Analytics prima del 9 maggio 2025 devono migrare le proprie configurazioni. Per ulteriori informazioni, consulta le seguenti guide alla migrazione:<ul><li>[Migra i tipi di pubblico ai nuovi campi dei contenuti multimediali in streaming](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[Esegui la migrazione di Customer Journey Analytics per utilizzare i nuovi campi per contenuti multimediali in streaming](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[Migra la preparazione dati per i campi personalizzati ai nuovi campi multimediali in streaming](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[Migrare i profili ai nuovi campi dei contenuti multimediali in streaming](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | Ottobre 2025 |

## 2024

| Funzione | Descrizione | Data |
| --- | --- | --- |
| **Supporto Web SDK** | Invia dati web di contenuti multimediali in streaming a Adobe Experience Platform Edge Network utilizzando l’estensione tag Web SDK o Web SDK, abilitando un metodo di raccolta unificato tra le soluzioni Platform come Customer Journey Analytics, Real-time CDP, Journey Optimizer e l’inoltro di eventi. Per ulteriori informazioni, vedere [Configurare Web SDK per Streaming Media](/help/implementation/edge/web-sdk.md) o [Configurare l&#39;estensione tag Web SDK per Streaming Media](/help/implementation/edge/web-sdk-tags.md). | 29 maggio 2024 |
| **Supporto Roku** | Invia dati multimediali in streaming a Adobe Experience Platform utilizzando Roku Edge SDK. Per ulteriori informazioni, vedere [Configurare Roku Edge per Streaming Media](/help/implementation/edge/roku.md). | 12 aprile 2024 |

## 2023

| Funzione | Descrizione | Data |
| --- | --- | --- |
| **Supporto Experience Edge** | Implementa la raccolta multimediale in streaming utilizzando l’API di Media Edge o gli SDK per dispositivi mobili per iOS e Android.<ul><li>[Configura l&#39;API Media Edge per lo streaming di file multimediali](/help/implementation/edge/media-edge-api.md)</li><li>[Configura iOS per Streaming Media](/help/implementation/edge/ios.md) o [Configura iOS per Streaming Media con Tag](/help/implementation/edge/ios-tags.md)</li><li>[Configura Android per Streaming Media](/help/implementation/edge/android.md) o [Configura Android per Streaming Media con Tag](/help/implementation/edge/android-tags.md)</li></ul> | sabato 12 maggio 2023 |

## 2022

| Funzione | Descrizione | Data |
| --- | --- | --- |
| **Tracciamento di più stati del lettore** | Utilizza l&#39;API Media Collection per implementare più di [tracciamento stato lettore](/help/implementation/events/player-state/overview.md). | Settembre 2022 |
| Campi XDM rinominati | Nomi di campi XDM rinominati per coerenza:<ul><li>Parametri audio e video</li><li>Parametri annuncio</li><li>Parametri per i capitoli</li><li>Parametri per lo stato del lettore</li><li>Parametri per la qualità</li></ul> | Settembre 2022 |
| **Pannelli aggiunti a Customer Journey Analytics** | Sono stati aggiunti i pannelli [Visualizzatori simultanei di contenuti multimediali](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) e [Tempo di riproduzione dei contenuti multimediali trascorso](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent) a Customer Journey Analytics. | 9 agosto 2022 |
| **Pubblico medio per minuto** | Puoi utilizzare il pannello del pubblico medio per minuto [&#128279;](https://experienceleague.adobe.com/it/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel) per comprendere meglio il consumo medio dei contenuti. <br>Il pubblico medio per minuto consente di confrontare la programmazione di qualsiasi durata o genere. Inoltre, i clienti possono confrontare o aggiungere questo pubblico medio per minuto digitale alle metriche medie per minuto per TV lineare. Questo pannello offre maggiore flessibilità per misurare il pubblico medio in periodi di tempo personalizzati, nonché quando la classificazione della durata è stata aggiornata. | 16 marzo 2022 |

## 2021

| Funzione | Descrizione | Data |
| --- | --- | --- |
| **Tempo di riproduzione dei contenuti multimediali trascorso** | Il pannello [Playback Time Spent](https://experienceleague.adobe.com/it/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent) fornisce ad insight informazioni utili sul coinvolgimento dei visualizzatori e consente alle organizzazioni di media di ottenere informazioni più approfondite e dettagliate sul coinvolgimento degli utenti minuto per minuto attraverso un&#39;analisi avanzata del tempo trascorso con funzionalità di ripartizione giornaliera. È possibile osservare il tempo impiegato per visualizzare i flussi multimediali in un determinato momento. Puoi suddividere la durata della riproduzione in base a diverse granularità, tra cui nuove granularità di 5, 15 e 30 minuti. | Settembre 2021 |

## 2020

| Funzione | Descrizione | Data |
| --- | --- | --- |
| **Pannello Visualizzatori simultanei di contenuti multimediali** | Il pannello [Visualizzatori simultanei](https://experienceleague.adobe.com/it/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers) consente di comprendere dove si è verificato il picco di concorrenza o in che punto i visitatori hanno abbandonato il contenuto. Ottieni informazioni approfondite sulla qualità dei contenuti e sul livello di coinvolgimento dell’utente, utili anche per risolvere problemi o pianificare volumi e scala.<br><br>[Pannello visualizzatori simultanei di contenuti multimediali (tutorial)](https://experienceleague.adobe.com/it/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | Settembre 2020; Gennaio 2021 |
| **Piattaforme e dispositivi supportati** | L’estensione Media Launch con SDK di AEP ora supporta i seguenti dispositivi OTT: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Giugno 2020 |
