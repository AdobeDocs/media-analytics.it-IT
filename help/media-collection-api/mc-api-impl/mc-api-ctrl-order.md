---
title: Controllo dell’ordine degli eventi
description: Scopri come controllare l’ordine degli eventi e come in alcuni casi gli eventi vengono riordinati in base alla marca temporale fornita nell’oggetto playerTime .
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 2%

---

# Controllo dell’ordine degli eventi{#controlling-the-order-of-events}

Il tracciamento video in streaming è un’operazione altamente dipendente dal tempo e occasionalmente le chiamate di tracciamento API di Media Collection arrivano fuori dall’ordine di back-end. In questa situazione, il back-end tenta di mettere in coda e riordinare gli eventi in base alla marca temporale fornita nell&#39;oggetto `playerTime` .  Ciò si verifica con alcuni limiti. Attualmente, il riordino potrebbe non riuscire se i ritardi tra le chiamate fuori servizio sono superiori a un secondo. Negli aggiornamenti futuri, il &quot;tempo di ritardo accettabile&quot; può essere ottimizzato e configurabile.

## Esempio di evento fuori ordine

Gli eventi fuori ordine si verificano quando gli eventi passano attraverso la rete che a volte causano un ritardo.

Ad esempio, puoi inviare un evento `adBreakStart` seguito da un evento `adStart` . Si tratta di un caso d’uso comune, perché è necessario che un annuncio inizi all’interno di un’interruzione pubblicitaria.

Se l’annuncio è pronto e non è necessario creare un buffer, entrambi gli eventi si verificano quasi istantaneamente e il `playerTime.ts` per entrambi gli eventi è molto vicino tra loro, ma non dovrebbe mai essere uguale.

> &quot;playerTime.ts&quot; degli eventi non dovrebbe mai essere uguale per qualsiasi evento, in quanto l&#39;algoritmo di ordinamento non sarebbe in grado di sapere quale evento si è verificato per primo. Dovrebbe esserci almeno una differenza di 1 millisecondo per ogni 2 eventi consecutivi.

Poiché entrambi gli eventi si verificano molto vicini l&#39;uno all&#39;altro nel momento in cui si attivano le chiamate di rete, è possibile che arrivino fuori servizio. In questo esempio, l’evento `adStart` arriva prima dell’evento `adBreakStart` .


È disponibile una finestra temporale di eventi: 5 secondi o un massimo di 10 eventi. Gli eventi vengono bufferizzati prima di inviarli alla pipeline di elaborazione. Quando le condizioni vengono soddisfatte, sono trascorsi 5 secondi o vengono ricevuti più di 10 eventi, gli eventi vengono riordinati in base al `playerTime.ts` e quindi inviati nel nuovo ordine alla pipeline di elaborazione.

>[!IMPORTANT]
>
>Esiste un evento di eccezione che viene inviato immediatamente alla pipeline di elaborazione ed è l’evento `sessionStart` .
