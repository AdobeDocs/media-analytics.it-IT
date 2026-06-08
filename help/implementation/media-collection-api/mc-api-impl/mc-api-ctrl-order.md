---
title: Controllo dell’ordine degli eventi
description: Scopri come controllare l’ordine degli eventi e come in alcuni casi gli eventi vengono riordinati in base alla marca temporale fornita nell’oggetto playerTime.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 73%

---

# Controllo dell’ordine degli eventi{#controlling-the-order-of-events}

Il tracciamento video in streaming è un’operazione altamente dipendente dal tempo e occasionalmente le chiamate di tracciamento API di Media Collection al back-end in ordine errato. In questa situazione, il back-end tenta di mettere in coda e riordinare gli eventi in base alla marca temporale fornita nell’oggetto `playerTime`.  Ciò si verifica con alcuni limiti. Attualmente, il riordino potrebbe non riuscire se i ritardi tra le chiamate fuori servizio sono superiori a un secondo. Negli aggiornamenti futuri, il “tempo di ritardo accettabile” può essere ottimizzato e configurabile.

## Esempio di evento in ordine errato

Gli eventi in ordine errato si verificano quando passano attraverso la rete, che a volte causa un ritardo.

Ad esempio, puoi inviare un evento `adBreakStart` seguito da un evento `adStart`. Si tratta di un caso d’uso comune, perché è necessario che un annuncio inizi all’interno di un’interruzione pubblicitaria.

Se l&#39;annuncio è pronto e non è necessario il buffering, entrambi gli eventi si verificano quasi immediatamente e `playerTime.ts` per entrambi gli eventi sono molto vicini tra loro. Tuttavia, non dovrebbero mai essere uguali, poiché l’algoritmo di ordinamento non saprebbe quale evento si è verificato per primo. Mantieni sempre una differenza di marca temporale di almeno 1 millisecondo per qualsiasi evento consecutivo.

Poiché entrambi gli eventi si verificano molto vicini l’uno all’altro nel momento in cui si attivano le chiamate di rete, è possibile che arrivino in ordine errato. In questo esempio, l’evento `adStart` arriva prima dell’evento `adBreakStart`.

È disponibile una finestra temporale di eventi: 5 secondi o un massimo di 10 eventi. Gli eventi vengono bufferizzati prima di inviarli alla pipeline di elaborazione. Quando le condizioni vengono soddisfatte (sono trascorsi 5 secondi o vengono ricevuti più di 10 eventi), gli eventi vengono riordinati in base a `playerTime.ts` e quindi inviati nel nuovo ordine alla pipeline di elaborazione.

>[!IMPORTANT]
>
>Esiste un evento di eccezione che viene inviato immediatamente alla pipeline di elaborazione ed è l’evento `sessionStart`.
