---
title: Tracciare la riproduzione
description: Scopri gli eventi di riproduzione e come implementare il tracciamento di riproduzione, pausa, buffer, ping e cambiamento del bitrate.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 2%

---


# Tracciare la riproduzione

Gli eventi di riproduzione tengono traccia delle transizioni di stato nel lettore multimediale durante una sessione. Costituiscono il nucleo del flusso di eventi e si applicano a qualsiasi tipo di contenuto.

## Eventi del lettore

| Evento lettore | Azione |
| --- | --- |
| Riproduzione o ripresa di contenuti multimediali | Chiama Play |
| Pause contenuti multimediali | Avvio pausa chiamata |
| Inizio buffering | Avvio del buffer di chiamata |
| Fine buffering | Chiama Play |
| Modifiche al bitrate | Modifica bitrate di chiamata |
| Il timer si attiva | Chiamata ping |

## Passaggi di implementazione

1. **Chiama [Riproduci](play.md)** dopo [Inizio sessione](../session/session-start.md) quando viene eseguito il rendering del primo fotogramma del contenuto sullo schermo. Invia anche Riproduci quando la riproduzione riprende dopo una pausa o un arresto del buffer. Non esiste un evento di ripresa separato.
1. **Chiama [Pausa avvio](pause-start.md)** quando l&#39;utente mette in pausa la riproduzione. Invia riproduzione quando riprende la riproduzione.
1. **Chiama [Avvio buffer](buffer-start.md)** quando il lettore non attende più i dati. Nelle API basate su XDM, la fine del buffer viene dedotta quando invii l’evento Play successivo. Su Mobile SDK, chiama esplicitamente `BufferComplete` anche quando viene risolto il buffering.
1. **Chiama [Ping](ping.md)** ogni 10 secondi durante la riproduzione del contenuto principale e ogni 1 secondo durante la riproduzione dell&#39;annuncio. Ping mantiene viva la sessione e registra il movimento della testina di riproduzione. Gli SDK per dispositivi mobili inviano automaticamente i ping; tutte le altre piattaforme devono inviarli manualmente.
1. **Chiama [Modifica bitrate](bitrate-change.md)** ogni volta che il lettore negozia un nuovo bitrate. Includi i dati QoE correnti (bitrate, fotogrammi al secondo, fotogrammi saltati) in modo che il backend possa calcolare [bitrate medio](/help/reporting/metrics/average-bitrate.md) e le metriche di qualità correlate.
