---
seo-title: Abilitazione di Audience Manager
title: Abilitazione di Audience Manager
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Abilitazione di Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), una piattaforma di gestione dei dati (DMP), consente di unire le risorse dei dati sul pubblico, semplificando la raccolta di informazioni rilevanti dal punto di vista commerciale sui visitatori del sito, la creazione di segmenti commerciabili e l'invio di contenuti e pubblicità mirati al pubblico giusto.

Con AAM, non sei legato a un venditore di dati, a uno scambio o a una piattaforma lato domanda. Inoltre, AAM è completamente agnostico quando si tratta delle risorse di dati dei tuoi partner. Con l'accesso a più origini dati, AAM offre agli editori digitali la possibilità di utilizzare un'ampia gamma di dati di terze parti e la nostra cooperativa privata di dati. Per ulteriori informazioni su AAM, consulta la documentazione di AAM relativa al prodotto [Audience Manager.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**Da VA a trasferimento dati AAM: per contenuti video e annunci video,** le metriche e i metadati raccolti utilizzando le variabili della soluzione (riservate) possono essere inviati automaticamente ad AAM. Il trasferimento dei dati è disponibile su tutte le piattaforme, inclusi desktop, dispositivi mobili e OTT. Per abilitare questo trasferimento di dati lato server, devi contattare Adobe Client Care e richiedere che il feed sia abilitato.

>[!IMPORTANT]
>
>Per garantire un trasferimento fluido dei dati ad AAM, devi disporre delle versioni più recenti delle librerie Media SDK.

Federated Data supporta completamente la condivisione dei dati su AAM. Consulta il tuo team Adobe per la conferma delle impostazioni dei dati federati.

## Metodi OTT/AAM {#ott-aam-methods}

Puoi usare questi metodi per inviare segnali e recuperare segmenti di visitatori da Audience Manager:

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

   Invia a Gestione dell'audience un segnale con caratteristiche.

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

   Invia a Gestione dell'audience un segnale con caratteristiche.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```

