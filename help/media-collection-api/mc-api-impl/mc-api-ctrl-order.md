---
title: Controllo dell’ordine degli eventi
description: Controllo dell’ordine degli eventi
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Controllo dell&#39;ordine degli eventi{#controlling-the-order-of-events}

Poiché l’API Media Collection è RESTful e il tracciamento video è un’operazione altamente dipendente dal tempo, un implementatore potrebbe preoccuparsi delle chiamate di tracciamento API Media Collection che arrivano al back-end non più disponibile. Il back-end *fa* tenta di mettere in coda e riordinare gli eventi in base alla marca temporale fornita nell&#39;oggetto `playerTime`. Tuttavia, esiste un limite a questa funzionalità. Attualmente, il riordino potrebbe non riuscire se i ritardi tra le chiamate fuori servizio sono superiori a un secondo. Questo &quot;ritardo accettabile&quot; può essere ottimizzato e / o configurato in aggiornamenti futuri.
