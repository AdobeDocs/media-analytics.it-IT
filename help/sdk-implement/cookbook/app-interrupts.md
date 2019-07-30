---
seo-title: La gestione dell'applicazione viene interrotta durante la riproduzione
title: La gestione dell'applicazione viene interrotta durante la riproduzione
uuid: 1 ccb 4507-bda 6-462 d-bf 67-e 22978 a 4 db 3 d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Handling application interrupts during playback{#handling-application-interrupts-during-playback}

La riproduzione in un'applicazione multimediale può essere sospesa in diversi modi: un utente preme in modo esplicito la pausa oppure quando un utente inserisce l'applicazione in background. A prescindere da ciò che causa un'interruzione nella riproduzione multimediale, le istruzioni di tracciamento sono le stesse:

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. In tal modo la riproduzione sarà verso l'alto per il tempo di riproduzione totale, insieme alla perdita di marcatori di avanzamento, segmenti e così via. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## FAQ about handling application interrupts: {#section_osf_xqs_h2b}

* _Per quanto tempo un'app deve essere messa in background prima della chiusura della sessione?_

   Se l'applicazione consente la riproduzione in background, può continuare il monitoraggio chiamando le nostre API e invieremo tutti i nostri intervalli di tracciamento regolari. Non molte app video consentono la riproduzione in background, ad eccezione di YouTube rosso, tuttavia, tutte le app audio consentono questa impostazione. Se l'applicazione non consente la riproduzione in background, è consigliabile rimanere in Pausa per un minuto, quindi terminare la sessione di tracciamento. L'applicazione non può continuare a inviare coppie di pause, perché nella maggior parte dei casi non può determinare se l'utente restituirà il contenuto per continuare a visualizzare il contenuto, oppure determinare quando verrà ucciso. Inoltre, è un'esperienza insoddisfacente continuare a inviare gli hit quando sono in background.

* _Qual è il modo corretto per gestire il tracciamento di riavvio dopo che l'app è rimasta in background per un periodo di tempo prolungato?_

   The application should call `trackSessionEnd` to end the tracking session. Dalla versione 2.1, l'SDK invia un ping "end" per notificare al back-end che la sessione di tracciamento è chiusa.

* _Come riavviare la sessione?_

   For detailed instructions on restarting a tracking session, see this page: [Manually resume a previously closed session.](/help/sdk-implement/cookbook/resuming-inactive.md) L'SDK invia una ripetizione per notificare al back-end che l'utente sta rimuovendo manualmente la sessione.

