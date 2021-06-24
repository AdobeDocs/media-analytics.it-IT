---
title: Condizioni di timeout
description: Scopri le condizioni di timeout dell’API Streaming Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---

# Condizioni di timeout{#timeout-conditions}

**Condizioni di timeout API di Media Collection**

L’API Media Collection, senza stato, non dispone dello stesso meccanismo dell’SDK Media per l’emissione di un nuovo ID sessione quando si verificano le condizioni di timeout. Quando si verifica una condizione di timeout, il back end chiude la sessione e tutte le chiamate successive effettuate con tale ID sessione vengono ignorate. La logica che gestisce un timeout sessione deve essere gestita nel client. In altre parole, il lettore dovrà monitorare le condizioni di timeout e ottenere un nuovo ID sessione se si verifica un timeout.

* **10 minuti: Nessun evento API**

   Se il back-end non riceve eventi API, la sessione verrà chiusa.
* **30 minuti: Nessuna modifica della sequenza di riproduzione**

   Se l&#39;indicatore di riproduzione non si sposta per 30 minuti (ad esempio, l&#39;utente colpisce Pause e se ne va), il back-end chiuderà la sessione.

>[!NOTE]
>
>Puoi anche forzare la fine di una sessione inviando una richiesta `events` con il tipo di evento `sessionEnd` .
