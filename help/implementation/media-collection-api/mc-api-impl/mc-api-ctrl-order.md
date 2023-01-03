---
title: Controllo dell’ordine degli eventi
description: Scopri come controllare l’ordine degli eventi e come in alcuni casi gli eventi vengono riordinati in base alla marca temporale fornita nell’oggetto playerTime.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '326'
ht-degree: 100%

---

# Controllo dell’ordine degli eventi {#controlling-the-order-of-events}

Il tracciamento video in streaming è un’operazione altamente dipendente dal tempo e occasionalmente le chiamate di tracciamento API di Media Collection al back-end fuori servizio. In questa situazione, il back-end tenta di mettere in coda e riordinare gli eventi in base alla marca temporale fornita nell’oggetto `playerTime`.  Ciò si verifica con alcuni limiti. Attualmente, il riordino potrebbe non riuscire se i ritardi tra le chiamate fuori servizio sono superiori a un secondo. Negli aggiornamenti futuri, il “tempo di ritardo accettabile” può essere ottimizzato e configurabile.

## Esempio di evento fuori servizio

Gli eventi fuori servizio si verificano quando passano attraverso la rete, che a volte causa un ritardo.

Ad esempio, puoi inviare un evento `adBreakStart` seguito da un evento `adStart`. Si tratta di un caso d’uso comune, perché è necessario che un annuncio inizi all’interno di un’interruzione pubblicitaria.

Se l’annuncio è pronto e non è necessario il buffering, entrambi gli eventi si verificano quasi istantaneamente e i `playerTime.ts` di entrambi gli eventi sono molto vicini tra loro, ma non dovrebbero mai essere uguali.

> Il dato “playerTime.ts” di più eventi non dovrebbe mai essere uguale, in quanto l’algoritmo di ordinamento non sarebbe in grado di sapere quale evento si è verificato per primo. Dovrebbe esserci una differenza della marca temporale di almeno 1 millisecondo per ogni 2 eventi consecutivi.

Poiché entrambi gli eventi si verificano molto vicini l’uno all’altro nel momento in cui si attivano le chiamate di rete, è possibile che arrivino fuori servizio. In questo esempio, l’evento `adStart` arriva prima dell’evento `adBreakStart`.


È disponibile una finestra temporale di eventi: 5 secondi o un massimo di 10 eventi. Gli eventi vengono bufferizzati prima di inviarli alla pipeline di elaborazione. Quando le condizioni vengono soddisfatte, sono trascorsi 5 secondi o vengono ricevuti più di 10 eventi, gli eventi vengono riordinati in base ai `playerTime.ts` e quindi inviati nel nuovo ordine alla pipeline di elaborazione.

>[!IMPORTANT]
>
>Esiste un evento di eccezione che viene inviato immediatamente alla pipeline di elaborazione ed è l’evento `sessionStart`.
