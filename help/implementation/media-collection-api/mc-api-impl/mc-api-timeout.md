---
title: Condizioni di timeout
description: Scopri le condizioni di timeout dell’API di Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 95%

---

# Condizioni di timeout{#timeout-conditions}

**Condizioni di timeout API di Media Collection**

L’API Media Collection, senza stato, non dispone dello stesso meccanismo dell’SDK Media per l’emissione di un nuovo ID sessione quando si verificano le condizioni di timeout. Quando si verifica una condizione di timeout, il back end chiude la sessione e tutte le chiamate successive effettuate con tale ID sessione vengono ignorate. La logica che gestisce un timeout sessione deve essere gestita nel client. In altre parole, il lettore dovrà monitorare le condizioni di timeout e ottenere un nuovo ID sessione se si verifica un timeout.

* **10 minuti: nessun evento API**

  Se il back-end non riceve eventi API, la sessione verrà chiusa.
* **30 minuti: nessuna modifica della sequenza di riproduzione**

  Se l’indicatore di riproduzione non si sposta per 30 minuti (ad esempio, l’utente preme Pause e se ne va), il back-end chiuderà la sessione.

>[!NOTE]
>
>Puoi anche forzare la fine di una sessione inviando una `events` richiesta con `sessionEnd` tipo di evento.
