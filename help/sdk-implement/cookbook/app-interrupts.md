---
title: Gestione degli arresti dell’applicazione durante la riproduzione
description: Come gestire le interruzioni al tracciamento durante la riproduzione dei contenuti multimediali.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: 29b0d38e904a561d467ba0432b255fdb17d6b829
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Gestione degli arresti dell’applicazione durante la riproduzione{#handling-application-interrupts-during-playback}

La riproduzione in un&#39;applicazione multimediale può essere interrotta in diversi modi: un utente preme esplicitamente pause o quando un utente mette l&#39;applicazione in background. Indipendentemente dalle cause di un&#39;interruzione nella riproduzione dei contenuti multimediali, le istruzioni di tracciamento sono le stesse:

1. Chiama **`trackPause`** quando l’applicazione viene interrotta (va in background, pause per i supporti, ecc.).
1. Chiama **`trackPlay`** quando l&#39;applicazione ritorna in primo piano e/o il supporto riprende la riproduzione.

>[!NOTE]
>
>Il team di Media Analytics ha visto le istanze in cui i clienti chiamavano `trackSessionStart` quando la loro app è tornata in background. In questo modo, la riproduzione fino a quel momento non viene conteggiata per il tempo di riproduzione totale, oltre a perdere marcatori di avanzamento precedenti, segmenti e così via. Chiamare `trackPlay` quando l&#39;app ritorna e/o il supporto riprende la riproduzione.

## Domande frequenti sulla gestione degli arresti dell’applicazione: {#faq-about-handling-application-interrupts}

* _Per quanto tempo deve essere messa in background un&#39;app prima della chiusura della sessione?_

   Se l&#39;applicazione consente la riproduzione in background, può continuare il tracciamento chiamando le nostre API e invieremo tutti i nostri regolari ping di tracciamento. Non molte app video supportano la riproduzione in background tranne YouTube Red, tuttavia, tutte le app audio lo consentono. Se l’applicazione non consente la riproduzione in background, è consigliabile rimanere nello stato di pausa per un minuto, quindi terminare la sessione di tracciamento. L&#39;applicazione non può continuare a inviare ping in pausa, perché nella maggior parte dei casi non è in grado di determinare se l&#39;utente tornerà a visualizzare il supporto, o di determinare quando verrà ucciso. È anche una brutta esperienza per continuare a inviare ping quando in background.

* _Qual è il modo corretto per gestire il nuovo tracciamento dopo che l&#39;app è stata in background per molto tempo?_

   L&#39;applicazione deve chiamare `trackSessionEnd` per terminare la sessione di tracciamento. Dalla versione 2.1, l’SDK invia un ping &quot;end&quot; per notificare al back-end la chiusura della sessione di tracciamento.

* _E per riavviare la stessa sessione?_

   Per istruzioni dettagliate sul riavvio di una sessione di tracciamento, consultate questa pagina: [Riprendere manualmente una sessione precedentemente chiusa](/help/sdk-implement/cookbook/resuming-inactive.md). L’SDK invia un ping di ripresa per notificare al back-end che l’utente sta riprendendo manualmente la sessione.

