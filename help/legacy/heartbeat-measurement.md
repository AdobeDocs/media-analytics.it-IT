---
title: Informazioni sulla misurazione heartbeat
description: Scopri come gli heartbeat vengono utilizzati per raccogliere le metriche video.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 30%

---

# Informazioni sulla misurazione Heartbeat

Adobe Analytics utilizza gli &quot;heartbeat&quot; per raccogliere le metriche video. Durante la riproduzione del video gli heartbeat vengono inviati al server che li traccia per misurare il tempo di riproduzione. Le chiamate heartbeat vengono inviate ogni dieci secondi. Gli heartbeat generano metriche granulari di coinvolgimento video e rapporti di fallout video più precisi. Adobe Analytics for Streaming Media misura gli heartbeat utilizzando Adobe Launch con l’estensione Media Analytics, Media SDK e l’API Media Collection. I componenti `AppMeasurement` e `VisitorID` vengono utilizzati per ricevere i dati video.

L’utilizzo di heartbeat in Adobe Analytics for Streaming Media offre i seguenti vantaggi:

| Funzione | Descrizione |
|---|---|
| Eventi multimediali | Eventi dettagliati e personalizzati vengono inviati ogni 10 secondi per il contenuto principale e a intervalli di 1 secondo per gli annunci |
| Metriche e dimensioni | Metriche, dimensioni e benchmark standardizzate e chiare per fornitori diversi. Con una soluzione standardizzata su tutte le piattaforme, puoi utilizzare variabili coerenti e standardizzate su tutti i contenuti multimediali e le piattaforme per consentire un confronto tra campagne, dispositivi e fornitori più efficiente. |
| Integrazioni | L’ID Experience Cloud è collegato a Adobe Experience Cloud per facilitare l’analisi incrociata. Con l’integrazione automatica di Adobe Experience Cloud, puoi segmentare il pubblico dei contenuti multimediali, targetizzarlo e formulare raccomandazioni multimediali in base alle preferenze degli utenti. |
| Prezzi | Tracciamento trasparente per flusso multimediale (singolo) |
| Implementazione e supporto | Configurazione semplificata con aggiornamenti e miglioramenti continui. Grazie a un processo di implementazione semplificato, puoi mappare rapidamente le variabili tramite l’API del lettore e convalidare le implementazioni tramite lo strumento di debug Adobe per garantire che tutte le variabili necessarie siano tracciate con precisione. |
| Condivisione partner | Federated Analytics e metriche certificate. Con i dati condivisi tramite Federated Analytics, puoi sfruttare le nostre funzionalità di condivisione dei contenuti multimediali all’avanguardia per valutare i dati in modo olistico tra tutti i partner di distribuzione dei contenuti multimediali: operatori, programmatori e distributori. |
| Tracciamento avanzato | Tracciamento del contenuto scaricato, tracciamento del recupero degli errori e visualizzatori simultanei. Puoi tenere traccia dei contenuti multimediali in streaming scaricati e riprodotti su un dispositivo indipendentemente dalla connettività. |
