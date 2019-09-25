---
seo-title: Condizioni di timeout
title: Condizioni di timeout
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Condizioni di timeout{#timeout-conditions}

**Condizioni di timeout dell'API di Media Collection**

L'API di Media Collection, senza stato, non dispone dello stesso meccanismo dell'SDK di Media per l'emissione di un nuovo ID sessione quando si verificano le condizioni di timeout. Quando si verifica una condizione di timeout, il back end chiuderà la sessione e tutte le chiamate successive effettuate con tale ID sessione verranno ignorate. La logica che gestisce un timeout sessione deve essere gestita nel client. In altre parole, il lettore dovrà monitorare le condizioni di timeout e ottenere un nuovo ID sessione se si verifica un timeout.

* **10 minuti: Nessun evento API**

   Se il back-end non riceve eventi API, la sessione verrà chiusa.
* **30 minuti: Nessuna modifica dell'indicatore di riproduzione**

   Se l'indicatore di riproduzione non si sposta per 30 minuti (ad esempio, se l'utente tocca Pausa e se ne va), il back-end chiuderà la sessione.

>[!NOTE]
>
>Potete anche forzare la fine di una sessione inviando una `events` richiesta con il tipo di `sessionEnd` evento.

