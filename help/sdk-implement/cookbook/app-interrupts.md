---
title: Gestione Degli Interruzioni Dell'Applicazione Durante La Riproduzione
description: Scopri come gestire le interruzioni del tracciamento durante la riproduzione di contenuti multimediali.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# Gestione degli arresti dell’applicazione durante la riproduzione{#handling-application-interrupts-during-playback}

La riproduzione in un&#39;applicazione multimediale può essere interrotta in diversi modi: un utente preme esplicitamente la pausa o quando un utente mette l&#39;applicazione in background. Indipendentemente dalle cause di un&#39;interruzione nella riproduzione dei contenuti multimediali, le istruzioni di tracciamento sono le stesse:

1. Chiama **`trackPause`** quando l&#39;applicazione viene interrotta (passa in background, pause sui file multimediali, ecc.).
1. Chiama **`trackPlay`** quando l&#39;applicazione torna in primo piano e/o il supporto riprende la riproduzione.

>[!NOTE]
>
>Il team di Media Analytics ha visto le istanze in cui i clienti hanno chiamato `trackSessionStart` quando la loro app è tornata dal background. In questo modo, la riproduzione fino a quel punto non viene conteggiata verso il tempo totale di riproduzione, oltre a perdere i marcatori di avanzamento precedenti, i segmenti e così via. Al contrario, chiama `trackPlay` quando ritorna l&#39;app e/o riprende la riproduzione del contenuto multimediale.

## Domande frequenti sulla gestione degli arresti dell&#39;applicazione: {#faq-about-handling-application-interrupts}

* _Per quanto tempo un&#39;app deve essere messa in background prima della chiusura della sessione?_

   Se l&#39;applicazione consente la riproduzione in background, può continuare il tracciamento chiamando le nostre API e invieremo tutti i nostri normali ping di tracciamento. Non molte app video consentono la riproduzione in background eccetto YouTube Red, tuttavia, tutte le app audio lo consentono. Se l’applicazione non consente la riproduzione in background, è consigliabile rimanere nello stato di pausa per un minuto, quindi terminare la sessione di tracciamento. L&#39;applicazione non può continuare a inviare ping in pausa, perché nella maggior parte dei casi non è in grado di determinare se l&#39;utente tornerà a visualizzare il supporto o determinare quando verrà interrotto. È anche una brutta esperienza continuare a inviare ping quando in background.

* _Qual è il modo corretto per gestire il tracciamento del riavvio dopo che l’app è stata in background per molto tempo?_

   L&#39;applicazione deve chiamare `trackSessionEnd` per terminare la sessione di tracciamento. Dalla versione 2.1, l’SDK invia un ping &quot;end&quot; per notificare al back-end la chiusura della sessione di tracciamento.

* _E il riavvio della stessa sessione?_

   Per istruzioni dettagliate sul riavvio di una sessione di tracciamento, consulta questa pagina: [Riprende manualmente una sessione precedentemente chiusa](/help/sdk-implement/cookbook/resuming-inactive.md). L’SDK invia un ping di ripresa per notificare all’utente back-end che sta riprendendo manualmente la sessione.
