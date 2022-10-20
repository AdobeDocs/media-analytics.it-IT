---
title: Cos’è l’abilitazione di Adobe Audience Manager?
description: Scopri come collegare le azioni dell’applicazione ai dati di tracciamento dei contenuti multimediali senza la necessità di ulteriori regole di elaborazione e variabili personalizzate.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 3e996d243d060a6fd07d2ddbabf05e39eca40758
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 26%

---

# Abilitazione dell’Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), una piattaforma di gestione dati (DMP, Data Management Platform), ti aiuta a unire le risorse dei dati sul pubblico, semplificando la raccolta di informazioni rilevanti dal punto di vista commerciale sui visitatori del sito, la creazione di segmenti commerciabili e la distribuzione di contenuti e pubblicità mirati al pubblico giusto.

Con AAM, non sei legato a una piattaforma lato vendita, scambio o domanda di dati. Inoltre, AAM è completamente agnostico quando si tratta delle risorse di dati dei tuoi partner. Con l&#39;accesso a più sorgenti di dati, AAM offre agli editori digitali la possibilità di utilizzare un&#39;ampia varietà di dati di terze parti. Per ulteriori informazioni su AAM, consulta la documentazione AAM [Documentazione del prodotto Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=it).

**Trasferimento dati da VA a AAM -** Per contenuti video e annunci video, le metriche e i metadati raccolti utilizzando variabili della soluzione (riservate) possono essere inviati automaticamente a AAM. Il trasferimento di dati è disponibile su tutte le piattaforme, inclusi desktop, dispositivi mobili e OTT. Per abilitare questo trasferimento di dati lato server, contatta l’Assistenza clienti di Adobe e richiedi l’abilitazione di questo feed.

>[!IMPORTANT]
>
>Per garantire un corretto trasferimento dei dati a AAM, usa le versioni più recenti delle librerie Media SDK.

Federated Data supporta completamente la condivisione dei dati per AAM. Collabora con il tuo team di Adobe per confermare le impostazioni di Federated Data.

## Metodi OTT/AAM {#ott-aam-methods}

Puoi utilizzare questi metodi per inviare segnali e recuperare segmenti di visitatori dall’Audience Manager:

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

   Imposta gli identificatori DPID e DPUUID. Se impostati, DPID e DPUUID saranno inviati congiuntamente con ogni segnale.

   ```js
   ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Invia a Gestione dell&#39;audience un segnale con caratteristiche.

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

   Restituisce il profilo del visitatore ottenuto più di recente. Restituisce un oggetto vuoto t se non è stato ancora inviato alcun segnale.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Restituisce il DPUUID corrente.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Imposta gli identificatori DPID e DPUUID. Se impostati, DPID e DPUUID saranno inviati congiuntamente con ogni segnale.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Invia a Gestione dell&#39;audience un segnale con caratteristiche.

   ```js
   traitData = {}
   traitData["sampleTrait"] = "sampleValue"
   ADBMobile().audienceSubmitSignal(traitData)
   ```
