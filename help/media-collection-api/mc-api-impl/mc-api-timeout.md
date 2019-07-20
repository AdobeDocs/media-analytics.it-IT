---
seo-title: Condizioni di timeout
title: Condizioni di timeout
uuid: 2 a 4 ea 13 e-a 561-4 adf-b 567-f 980301 b 32 c 8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Timeout conditions{#timeout-conditions}

**Condizioni timeout API per Media Collection**

L'API Media Collection, che è priva di staticità, non ha lo stesso meccanismo di Media SDK per il rilascio di un nuovo ID sessione quando si verificano condizioni di timeout. Quando si verifica una condizione di timeout, il back-end chiuderà la sessione e tutte le chiamate successive effettuate con quell'ID sessione verranno ignorate. La logica che gestisce un timeout sessione deve essere gestita nel client. In altre parole, il lettore dovrà monitorare le condizioni di timeout e ottenere un nuovo ID sessione se si verifica un timeout.

* **10 minuti: Nessun evento API**

   Se il back-end non riceve alcun evento API, chiuderà la sessione.
* **30 minuti: Nessuna modifica di Playhead**

   Se l'indicatore di riproduzione non si sposta per 30 minuti (ad es., l'utente si blocca e si allontana), la fine della sessione si chiude.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

