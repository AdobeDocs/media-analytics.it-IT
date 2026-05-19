---
title: Cos’è l’abilitazione di Adobe Audience Manager?
description: Scopri come collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 93%

---

# Abilitazione di Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM) è una piattaforma di gestione dei dati (DMP) che consente di unire le risorse dei dati sul pubblico, semplificando così la raccolta di informazioni rilevanti dal punto di vista commerciale sui visitatori del sito, la creazione di segmenti commerciali e la distribuzione di pubblicità e contenuti mirati al pubblico giusto.

Con AAM, non sei vincolato a un fornitore di dati, un exchange o una DSP. Inoltre, AAM è completamente agnostico in merito alle risorse di dati dei tuoi partner. Con l’accesso a più origini di dati, AAM offre agli editori digitali la possibilità di utilizzare un’ampia varietà di dati di terze parti. Per ulteriori informazioni su AAM, consulta la documentazione di AAM: [documentazione del prodotto Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=it).

**Trasferimento dati da VA ad AAM:** per contenuti video e annunci video, le metriche e i metadati raccolti mediante variabili della soluzione (riservate) possono essere inviati automaticamente ad AAM. Il trasferimento di dati è disponibile su tutte le piattaforme, inclusi desktop, dispositivi mobili e OTT. Per abilitare questo trasferimento di dati lato server, contatta l’Assistenza clienti di Adobe e richiedi l’abilitazione di questo feed.

>[!IMPORTANT]
>
>Per garantire il corretto trasferimento dei dati ad AAM, devi usare le versioni più recenti delle librerie Media SDK.

Federated Data supporta completamente la condivisione dei dati per AAM. Collabora con il tuo team di Adobe per confermare le impostazioni di Federated Data.

## Metodi OTT/AAM {#ott-aam-methods}

Puoi utilizzare questi metodi per inviare segnali e recuperare segmenti di visitatori da Audience Manager:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

  Restituisce il profilo del visitatore ottenuto più di recente. Restituisce un oggetto vuoto se non è stato ancora inviato alcun segnale.

  ```js
  ADBMobile.audienceManager.getVisitorProfile();
  ```

* `getDpid() -`

  Restituisce il profilo del visitatore ottenuto più di recente. Restituisce un oggetto vuoto se non è stato ancora inviato alcun segnale.

  ```js
  ADBMobile.audienceManager.getDpid();
  ```

* `getDpuuid() -`

  Restituisce il DPUUID corrente.

  ```js
  ADBMobile.audienceManager.getDpuuid();
  ```

* `setDpidAndDpuuid() -`

  Imposta gli identificatori DPID e DPUUID. Se DPID e DPUUID sono impostati, verranno inviati con ciascun segnale.

  ```js
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  Invia al modulo Gestione del pubblico un segnale con caratteristiche.

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
  ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

  Restituisce il profilo del visitatore ottenuto più di recente. Restituisce un oggetto vuoto se non è stato ancora inviato alcun segnale.

  ```js
  ADBMobile().audienceVisitorProfile()
  ```

* `audienceDpid -`

  Restituisce il profilo del visitatore ottenuto più di recente. Restituisce un oggetto vuoto se non è stato ancora inviato alcun segnale.

  ```js
  ADBMobile().audienceDpid()
  ```

* `audienceDpuuid -`

  Restituisce il DPUUID corrente.

  ```js
  ADBMobile().audienceDpuuid()
  ```

* `audienceSetDpidAndDpuuid -`

  Imposta gli identificatori DPID e DPUUID. Se DPID e DPUUID sono impostati, verranno inviati con ciascun segnale.

  ```js
  ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
  ```

* `audienceSubmitSignal -`

  Invia al modulo Gestione del pubblico un segnale con caratteristiche.

  ```js
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```
