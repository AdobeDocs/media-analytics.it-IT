---
title: Cos'è l'abilitazione Adobe Audience Manager?
description: Scoprite come collegare le azioni dell'applicazione ai dati di tracciamento dei supporti senza necessità di ulteriori regole di elaborazione e variabili personalizzate.
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 19%

---


# Abilitazione  Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), una piattaforma di gestione dei dati (DMP), consente di unire le risorse dei dati sul pubblico, semplificando la raccolta di informazioni rilevanti dal punto di vista commerciale sui visitatori del sito, la creazione di segmenti commerciabili e la distribuzione di contenuti e pubblicità mirati al pubblico giusto.

Con AAM, non sei legato a un venditore di dati, a uno scambio o a una piattaforma lato domanda. Inoltre, AAM è completamente agnostico quando si tratta delle risorse dati dei tuoi partner. Con l&#39;accesso a più origini dati, AAM offre agli editori digitali la possibilità di utilizzare un&#39;ampia varietà di dati di terze parti e la nostra cooperativa privata di dati. Per ulteriori informazioni sulle AAM, consultare la documentazione AAM [ Audience Manager documentazione del prodotto.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**Da VA a AAM trasferimento di dati -** Per contenuti video e annunci video, le metriche e i metadati raccolti utilizzando le variabili della soluzione (riservate) possono essere inviati automaticamente a AAM. Il trasferimento dei dati è disponibile su tutte le piattaforme, inclusi desktop, dispositivi mobili e OTT. Per abilitare questo trasferimento di dati lato server, è necessario contattare  Client Care di Adobe e richiedere che il feed sia abilitato.

>[!IMPORTANT]
>
>Per garantire un trasferimento fluido dei dati a AAM, è necessario disporre delle versioni più recenti delle librerie Media SDK.

I dati federati supportano completamente la condivisione dei dati per AAM. Consulta il team  Adobe per ricevere conferma delle impostazioni dei dati federati.

## Metodi OTT/AAM {#ott-aam-methods}

Puoi usare questi metodi per inviare segnali e recuperare segmenti di visitatori da  Audience Manager:

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
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Invia a Gestione dell&#39;audience un segnale con caratteristiche.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
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
   ADBMobile().audienceSubmitSignal()
   ```
