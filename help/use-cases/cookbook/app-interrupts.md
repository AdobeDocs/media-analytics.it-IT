---
title: Gestione degli arresti dell’applicazione durante la riproduzione
description: Scopri come gestire le interruzioni del tracciamento durante la riproduzione di contenuti multimediali.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/BlL-c1rf5d3juDKHybex9vrPvQsBIiNXVO2ug9LKl0g
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 62%

---

# Gestione degli arresti dell’applicazione durante la riproduzione{#handling-application-interrupts-during-playback}

La riproduzione in un’applicazione multimediale può essere interrotta in diversi modi. Ad esempio, un utente può mettere l’applicazione esplicitamente in pausa oppure in esecuzione in background. Indipendentemente dalle cause di un’interruzione nella riproduzione dei contenuti multimediali, le istruzioni di tracciamento sono le stesse.

1. Eseguire la chiamata **`trackPause`** quando l’applicazione viene interrotta (passa in background, l’elemento multimediale è messo in pausa, ecc.).
1. Eseguire la chiamata **`trackPlay`** quando l’applicazione torna in primo piano e/o l’elemento multimediale riprende la riproduzione.

>[!NOTE]
>
>La chiamata a `trackSessionStart` quando l&#39;app torna in background può comportare la mancata conteggio della riproduzione fino a quel punto rispetto al tempo totale di riproduzione, oltre alla perdita di marcatori di avanzamento precedenti, segmenti e così via. Invece, esegui la chiamata `trackPlay` quando l’app torna attiva e/o il contenuto multimediale riprende la riproduzione.

## Domande frequenti sulla gestione delle interruzioni dell’applicazione: {#faq-about-handling-application-interrupts}

* _Per quanto tempo un’app deve restare in background prima che venga chiusa la sessione?_

  Se l’applicazione consente la riproduzione in background, può continuare il tracciamento chiamando le nostre API e noi invieremo tutti i normali ping di tracciamento. Non molte app video consentono la riproduzione in background eccetto YouTube Red, tuttavia, tutte le app audio lo consentono. Se l’applicazione non consente la riproduzione in background, è consigliabile rimanere nello stato di pausa per un minuto, quindi terminare la sessione di tracciamento. L’applicazione non può continuare a inviare ping in pausa, perché nella maggior parte dei casi non è in grado di determinare se l’utente tornerà a visualizzare il contenuto multimediale o quando questo verrà interrotto. È anche una brutta esperienza continuare a inviare ping in background.

* _Qual è il modo corretto per gestire il tracciamento del riavvio dopo che l’app è stata in background per molto tempo?_

  L’applicazione deve eseguire la chiamata `trackSessionEnd` per terminare la sessione di tracciamento. Dalla versione 2.1, l’SDK invia un ping “end” per notificare al back-end la chiusura della sessione di tracciamento.

* _E il riavvio della stessa sessione?_

  Per informazioni sulla ripresa di una sessione di tracciamento, vedere [Ripresa di sessioni inattive](resuming-inactive.md).SDK invia un ping di ripresa per notificare al back-end che l’utente sta riprendendo manualmente la sessione.

* _Cosa succede se `trackSessionEnd` viene chiamato due volte per la stessa sessione?_

  Chiamare `trackSessionEnd` più volte per la stessa sessione è sicuro. Il backend chiude la sessione sul primo evento e rilascia automaticamente tutti gli eventi successivi per tale ID sessione, incluso un secondo `trackSessionEnd`. Ciò significa che le condizioni di gara, ad esempio il timeout di inattività di 30 minuti che si attiva nello stesso momento in cui lo spettatore chiude il lettore, non producono dati duplicati.

* _Cosa succede se `trackSessionStart` viene chiamato mentre una sessione è già attiva?_

  SDK ignora la seconda chiamata `trackSessionStart` se la sessione non è ancora stata chiusa. Se devi avviare una nuova sessione, chiama `trackSessionEnd` prima per chiudere esplicitamente quella corrente, quindi chiama `trackSessionStart` per la nuova sessione.
