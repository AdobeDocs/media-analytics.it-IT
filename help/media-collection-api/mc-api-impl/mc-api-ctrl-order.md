---
seo-title: Controlling the order of events
title: Controllo dell'ordine degli eventi
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Controlling the order of events{#controlling-the-order-of-events}

Poiché l’API Media Collection è RESTful e il tracciamento video è un’operazione che dipende dal tempo, un implementatore potrebbe preoccuparsi delle chiamate di tracciamento API di Media Collection che arrivano al back-end in ordine. Il back-end *tenta* di mettere in coda e riordinare gli eventi in base alla marca temporale fornita nell' `playerTime` oggetto. Tuttavia, esiste un limite a questa capacità. Attualmente, il riordino potrebbe non riuscire se i ritardi tra le chiamate fuori servizio sono superiori a un secondo. Questo "tempo di ritardo accettabile" può essere ottimizzato e / o configurabile in aggiornamenti futuri.
