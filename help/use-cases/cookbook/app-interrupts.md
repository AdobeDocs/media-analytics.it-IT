---
title: Gestione degli arresti dell’applicazione durante la riproduzione
description: Scopri come gestire le interruzioni del tracciamento durante la riproduzione di contenuti multimediali.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 83%

---

# Gestione degli arresti dell’applicazione durante la riproduzione {#handling-application-interrupts-during-playback}

La riproduzione in un&#39;applicazione multimediale può essere interrotta in diversi modi. Ad esempio, un utente può premere esplicitamente la pausa oppure può mettere l&#39;applicazione in background. Indipendentemente dalle cause di un’interruzione nella riproduzione dei contenuti multimediali, le istruzioni di tracciamento sono le stesse.

1. Eseguire la chiamata **`trackPause`** quando l’applicazione viene interrotta (passa in background, l’elemento multimediale è messo in pausa, ecc.).
1. Eseguire la chiamata **`trackPlay`** quando l’applicazione torna in primo piano e/o l’elemento multimediale riprende la riproduzione.

>[!NOTE]
>
>Il team di Media Analytics ha visto istanze in cui i clienti hanno eseguito la chiamata `trackSessionStart` quando l’app è tornata dal background. In questo modo, la riproduzione fino a quel punto non viene conteggiata nel tempo totale di riproduzione e oltretutto si perdono i marcatori di avanzamento precedenti, i segmenti e così via. Invece, esegui la chiamata `trackPlay` quando l’app torna attiva e/o il contenuto multimediale riprende la riproduzione.

## Domande frequenti sulla gestione delle interruzioni dell’applicazione: {#faq-about-handling-application-interrupts}

* _Per quanto tempo un’app deve restare in background prima che venga chiusa la sessione?_

   Se l’applicazione consente la riproduzione in background, può continuare il tracciamento chiamando le nostre API e noi invieremo tutti i normali ping di tracciamento. Non molte app video consentono la riproduzione in background eccetto YouTube Red, tuttavia, tutte le app audio lo consentono. Se l’applicazione non consente la riproduzione in background, è consigliabile rimanere nello stato di pausa per un minuto, quindi terminare la sessione di tracciamento. L’applicazione non può continuare a inviare ping in pausa, perché nella maggior parte dei casi non è in grado di determinare se l’utente tornerà a visualizzare il contenuto multimediale o quando questo verrà interrotto. È anche una brutta esperienza continuare a inviare ping in background.

* _Qual è il modo corretto per gestire il tracciamento del riavvio dopo che l’app è stata in background per molto tempo?_

   L’applicazione deve eseguire la chiamata `trackSessionEnd` per terminare la sessione di tracciamento. Dalla versione 2.1, l’SDK invia un ping “end” per notificare al back-end la chiusura della sessione di tracciamento.

* _E il riavvio della stessa sessione?_

   Per informazioni sulla ripresa di una sessione di tracciamento, vedi [Ripresa delle sessioni inattive](resuming-inactive.md).L&#39;SDK invia un ping di ripresa per notificare al back-end che l&#39;utente sta riprendendo manualmente la sessione.