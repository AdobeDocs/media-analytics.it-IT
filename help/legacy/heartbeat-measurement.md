---
title: Informazioni sulla misurazione con Heartbeat
description: Scopri come gli heartbeat vengono utilizzati per raccogliere le metriche video.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: a7d897c6f6fbc6ed0d5b71f5801ab18ee21f0411
workflow-type: ht
source-wordcount: '311'
ht-degree: 100%

---

# Informazioni sulla misurazione con Heartbeat

Adobe Analytics utilizza gli “heartbeat” per raccogliere le metriche video. Durante la riproduzione del video gli heartbeat vengono inviati al server che li traccia per misurare il tempo di riproduzione. Le chiamate heartbeat vengono inviate ogni dieci secondi. Gli heartbeat generano metriche granulari di coinvolgimento video e rapporti di fallout video più precisi. Adobe Analytics for Streaming Media misura gli heartbeat utilizzando Adobe Launch con l’estensione Media Analytics, Media SDK e l’API Media Collection. I componenti `AppMeasurement` e `VisitorID` vengono utilizzati per ricevere i dati video.

L’utilizzo di heartbeat in Adobe Analytics for Streaming Media offre i seguenti vantaggi:

| Funzione | Descrizione |
|---|---|
| Eventi multimediali | Eventi dettagliati e personalizzati vengono inviati ogni 10 secondi per il contenuto principale e a intervalli di 1 secondo per gli annunci |
| Metriche e dimensioni | Metriche, dimensioni e benchmark standardizzate e chiare per fornitori diversi. Con una soluzione standardizzata su tutte le piattaforme, puoi utilizzare variabili coerenti e standardizzate su tutti i contenuti multimediali e le piattaforme per consentire un confronto più efficiente tra campagne, dispositivi e fornitori. |
| Integrazioni | Experience Cloud ID è collegato ad Adobe Experience Cloud per effettuare analisi incrociate più facilmente. Grazie all’integrazione automatica di Adobe Experience Cloud puoi segmentare il pubblico dei contenuti multimediali, targetizzarlo e fornire consigli sul contenuto multimediale in base alle preferenze degli utenti. |
| Prezzi | Tracciamento trasparente per flusso multimediale (singolo) |
| Implementazione e supporto | Configurazione semplificata con continui aggiornamenti e miglioramenti. Un processo di implementazione semplificato ti consente di mappare rapidamente le variabili tramite l’API del lettore e convalidare le implementazioni tramite lo strumento Adobe Debug per garantire che tutte le variabili necessarie siano tracciate con precisione. |
| Condivisione con i partner | Federated Analytics e metriche certificate. Con i dati condivisi tramite Federated Analytics puoi sfruttare le nostre funzionalità avanzate di condivisione dei contenuti multimediali per valutare i dati in modo olistico tra tutti i partner di distribuzione di contenuti multimediali: operatori, programmatori e distributori. |
| Tracciamento avanzato | Tracciamento del contenuto scaricato, tracciamento del recupero degli errori e visualizzatori simultanei. Puoi tenere traccia del contenuto multimediale in streaming che viene scaricato e riprodotto su un dispositivo indipendentemente dalla connettività. |
