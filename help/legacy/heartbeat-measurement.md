---
title: Informazioni sulla misurazione con Heartbeat
description: Scopri come gli heartbeat vengono utilizzati per raccogliere le metriche video.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e6c28e30-8689-4bf4-8fa8-561343d308a9
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# Informazioni sulla misurazione con Heartbeat

I servizi multimediali di streaming di Adobe utilizzano gli &quot;heartbeat&quot; per raccogliere le metriche video. Durante la riproduzione del video gli heartbeat vengono inviati al server che li traccia per misurare il tempo di riproduzione. Le chiamate heartbeat vengono inviate ogni dieci secondi. Gli heartbeat generano metriche granulari di coinvolgimento video e rapporti di fallout video più precisi. i servizi di streaming media misurano gli heartbeat utilizzando Adobe Launch con l’estensione Media Analytics, Media SDK e l’API Media Collection. I componenti `AppMeasurement` e `VisitorID` vengono utilizzati per ricevere i dati video.

L’utilizzo di heartbeat nei servizi di streaming media offre i seguenti vantaggi:

| Funzione | Descrizione |
|---|---|
| Eventi multimediali | Eventi dettagliati e personalizzati vengono inviati ogni 10 secondi per il contenuto principale e a intervalli di 1 secondo per gli annunci |
| Metriche e dimensioni | Metriche, dimensioni e benchmark standardizzate e chiare per fornitori diversi. Con una soluzione standardizzata su tutte le piattaforme, puoi utilizzare variabili coerenti e standardizzate su tutti i contenuti multimediali e le piattaforme per consentire un confronto tra campagne, dispositivi e fornitori più efficiente. |
| Integrazioni | Experience Cloud ID è collegato a Adobe Experience Cloud per facilitare l’analisi incrociata. Con l’integrazione automatica di Adobe Experience Cloud, puoi segmentare il pubblico dei contenuti multimediali, targetizzarlo e formulare raccomandazioni per il contenuto multimediale in base alle preferenze degli utenti. |
| Prezzi | Tracciamento trasparente per flusso multimediale (singolo) |
| Implementazione e supporto | Configurazione semplificata con continui aggiornamenti e miglioramenti. Grazie a un processo di implementazione semplificato, puoi mappare rapidamente le variabili tramite l’API del lettore e convalidare le implementazioni tramite lo strumento Adobe Debug per garantire che tutte le variabili necessarie siano tracciate con precisione. |
| Condivisione con i partner | Federated Media e metriche certificate. Con i dati condivisi tramite Federated Media, puoi sfruttare le nostre funzionalità di condivisione dei contenuti multimediali all’avanguardia per valutare i dati in modo olistico tra tutti i partner di distribuzione di contenuti multimediali: operatori, programmatori e distributori. |
| Tracciamento avanzato | Tracciamento contenuto scaricato, tracciamento recupero errori e visualizzatori simultanei. Puoi tenere traccia del contenuto multimediale in streaming scaricato e riprodotto su un dispositivo indipendentemente dalla connettività. |
