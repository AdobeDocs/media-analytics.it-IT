---
title: Informazioni sul tracciamento dello stato del lettore
description: Questo argomento descrive la funzione di tracciamento dello stato del lettore, compresi i requisiti e le linee guida per l’implementazione e la generazione di rapporti degli stati del lettore.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# Informazioni sul tracciamento dello stato del lettore

Per ottimizzare l&#39;esperienza di prodotto e il valore dell&#39;unità aziendale, è importante comprendere il comportamento dei clienti durante la visualizzazione dei video. Ciò include il tempo trascorso all&#39;interno di diversi stati del lettore.  E per ottimizzare la comprensione, è necessario disporre della flessibilità necessaria per creare e misurare nuovi stati ed eventi dei giocatori in base alle esigenze.

Il Tracciamento dello stato del lettore consente di catturare l’interazione del visualizzatore durante la riproduzione utilizzando un set standard di variabili della soluzione per la visualizzazione a schermo intero, i sottotitoli codificati, l’audio, l’immagine nell’immagine e la messa a fuoco.  Il tracciamento dello stato del lettore offre inoltre la flessibilità necessaria per creare stati del lettore personalizzati.  Le variabili di tracciamento dello stato del lettore sono inoltre disponibili per il reporting in Analysis Workspace.

Per acquisire le modifiche allo stato del lettore, il tracciamento dello stato del lettore aggiorna i metadati delle misurazioni video. Ad esempio, per determinare il &quot;vero&quot; coinvolgimento video, il tracciamento dello stato del lettore misura il tempo trascorso con il suono attivato rispetto alle visualizzazioni video passive o non impegnate quando il suono è spento o il tempo trascorso in modalità Normale o Schermo intero.

Il tracciamento dello stato del lettore offre i seguenti vantaggi:

* Fornisce variabili standard che misurano gli stati comuni, come schermo intero o sottotitoli codificati
* Fornisce variabili personalizzabili per misurare gli stati personalizzati durante una sessione di riproduzione
* Misura il tempo trascorso nello stato di un lettore personalizzato
* Misura più stati che possono essere simultanei

![Tracciamento dello stato del lettore](assets/player_state_tracking.png)

## Requisiti

Il tracciamento dello stato del lettore richiede quanto segue per Media Analytics Extension da usare con Adobe Experience Platform (AEP SDK):
* Web: Adobe Media Analytics (SDK 3.x) per audio e video v1.0+
* Mobile: Adobe Media Analytics for Audio and Video v2.0+

Se decidi di non utilizzare l’SDK AEP, con il tracciamento dello stato del lettore puoi usare quanto segue:
* Media JS SDK 3.0+
* Versione API di Media Collection?

## Linee guida

Prima di implementare il tracciamento dello stato del lettore, attenersi alle seguenti linee guida.

* Lo stato del lettore viene calcolato in tutti gli stati di riproduzione - (nessuna suddivisione)
* È possibile misurare più stati del lettore contemporaneamente
* Il numero massimo di stati del lettore che è possibile tenere traccia durante una riproduzione è 10 
* Le metriche dello stato del lettore vengono inviate ad Analytics per la generazione di rapporti SOLO sulla chiamata Media Close
* Gli stati del lettore vengono catturati per ogni singola sessione di riproduzione; lo stato del lettore non viene calcolato per tutte le riproduzioni 
