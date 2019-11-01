---
title: Controllo dell'ordine degli eventi
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Controllo dell'ordine degli eventi{#controlling-the-order-of-events}

Poiché l’API Media Collection è RESTful e il tracciamento video è un’operazione che dipende dal tempo, un implementatore potrebbe preoccuparsi delle chiamate di tracciamento API di Media Collection che arrivano al back-end in ordine. Il back-end *tenta* di mettere in coda e riordinare gli eventi in base alla marca temporale fornita nell' `playerTime` oggetto. Tuttavia, esiste un limite a questa capacità. Attualmente, il riordino potrebbe non riuscire se i ritardi tra le chiamate fuori servizio sono superiori a un secondo. Questo "tempo di ritardo accettabile" può essere ottimizzato e / o configurabile in aggiornamenti futuri.
