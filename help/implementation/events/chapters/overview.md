---
title: Tracciamento capitoli e segmenti
description: Come implementare il tracciamento di capitoli e segmenti con l’SDK per contenuti multimediali.
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
    internal-label: Variables
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 39%
---

# Tracciare capitoli e segmenti

Il tracciamento di capitoli e segmenti è disponibile per capitoli o segmenti multimediali personalizzati. Alcuni utilizzi comuni per il tracciamento dei capitoli sono la definizione di segmenti personalizzati in base ai contenuti multimediali (ad esempio gli inning di baseball) o la definizione di segmenti di contenuto tra interruzioni di annunci. Il tracciamento dei capitoli **not** è richiesto per le implementazioni di tracciamento dei contenuti multimediali di base.

Il tracciamento dei capitoli include gli inizi dei capitoli, i completamenti dei capitoli e i salti dei capitoli. Utilizza l’API del lettore multimediale con logica di segmentazione personalizzata per identificare gli eventi dei capitoli e popolare le variabili dei capitoli.

## Eventi del lettore

| Evento lettore | Azione |
| --- | --- |
| Inizio capitolo | Crea oggetto capitolo; chiama ChapterStart |
| Capitolo completato | Chiama ChapterComplete |
| Salta capitolo | Chiama ChapterSkip |

## Passaggi di implementazione

1. Identifica quando si verifica l’evento di inizio del capitolo e crea l’oggetto capitolo. Per le definizioni dei campi, vedere [Nome capitolo](/help/implementation/variables/chapters/chapter-name.md), [Posizione capitolo](/help/implementation/variables/chapters/chapter-position.md), [Lunghezza capitolo](/help/implementation/variables/chapters/chapter-length.md) e [Offset capitolo](/help/implementation/variables/chapters/chapter-offset.md).
1. Facoltativamente, crea variabili di dati di contesto per metadati di capitoli personalizzati.
1. Chiama [Inizio capitolo](/help/implementation/events/chapters/chapter-start.md) per iniziare a tracciare il capitolo.
1. Quando la riproduzione raggiunge il limite finale del capitolo, chiamare [Chapter complete](/help/implementation/events/chapters/chapter-complete.md).
1. Se l&#39;utente ignora il capitolo prima del completamento, chiamare [Salta capitolo](/help/implementation/events/chapters/chapter-skip.md).
1. Per i capitoli aggiuntivi, ripetere i passaggi da 1 a 5.
