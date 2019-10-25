---
seo-title: Gestione degli arresti dell’applicazione durante la riproduzione
title: Gestione degli arresti dell’applicazione durante la riproduzione
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Gestione degli arresti dell’applicazione durante la riproduzione{#handling-application-interrupts-during-playback}

La riproduzione in un'applicazione multimediale può essere interrotta in diversi modi: un utente preme esplicitamente pause o quando un utente mette l'applicazione in background. Indipendentemente dalle cause di un'interruzione nella riproduzione dei supporti, le istruzioni di tracciamento sono le stesse:

1. Chiamata **`trackPause`** quando l’applicazione viene interrotta (va in background, pause per i supporti, ecc.).
1. Chiama **`trackPlay`** quando l’applicazione torna in primo piano e/o il supporto riprende la riproduzione.

>[!NOTE]
>
>Il team di Media Analytics ha visto le istanze in cui i clienti hanno chiamato `trackSessionStart` quando la loro app è tornata in background. In questo modo, la riproduzione fino a quel momento non viene conteggiata per il tempo di riproduzione totale, oltre a perdere marcatori di avanzamento precedenti, segmenti e così via. Al contrario, chiamate `trackPlay` quando l'app ritorna e/o il supporto riprende la riproduzione.

## Domande frequenti sulla gestione degli arresti dell’applicazione: {#faq-about-handling-application-interrupts}

* _Per quanto tempo deve essere messa in background un'app prima della chiusura della sessione?_

   Se l'applicazione consente la riproduzione in background, può continuare il tracciamento chiamando le nostre API e invieremo tutti i nostri regolari ping di tracciamento. Non molte app video supportano la riproduzione in background tranne YouTube Red, tuttavia, tutte le app audio lo consentono. Se l’applicazione non consente la riproduzione in background, è consigliabile rimanere nello stato di pausa per un minuto, quindi terminare la sessione di tracciamento. L'applicazione non può continuare a inviare ping in pausa, perché nella maggior parte dei casi non è in grado di determinare se l'utente tornerà a visualizzare il supporto, o di determinare quando verrà ucciso. È anche una brutta esperienza per continuare a inviare ping quando in background.

* _Qual è il modo corretto per gestire il nuovo tracciamento dopo che l'app è stata in background per molto tempo?_

   L’applicazione deve chiamare `trackSessionEnd` per terminare la sessione di tracciamento. Dalla versione 2.1, l’SDK invia un ping "end" per notificare al back-end la chiusura della sessione di tracciamento.

* _E per riavviare la stessa sessione?_

   Per istruzioni dettagliate sul riavvio di una sessione di tracciamento, consultate questa pagina: Riprendere [manualmente una sessione precedentemente chiusa.](/help/sdk-implement/cookbook/resuming-inactive.md) L’SDK invia un ping di ripresa per notificare al back-end che l’utente sta riprendendo manualmente la sessione.

