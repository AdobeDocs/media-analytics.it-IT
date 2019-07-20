---
seo-title: Abilitazione di Audience Manager
title: Abilitazione di Audience Manager
uuid: 8 a 7 f 9343-ebc 3-4087-9 d 7 e -5972640 d 2455
translation-type: tm+mt
source-git-commit: 8ae15f1e14731a97d212ab66816a777b4dcc897e

---


# Audience Manager enablement{#audience-manager-enablement}

Adobe Audience Manager (AAM), una piattaforma di gestione dati (DMP), consente di riunire le risorse dati relative al pubblico, semplificando la raccolta di informazioni commerciali sui visitatori del sito, la creazione di segmenti commercializzabili e la trasmissione di pubblicità e contenuti mirati al pubblico giusto.

Con AAM non sei legato a un venditore di dati, a uno scambio o a una piattaforma lato domanda. Inoltre, AAM è totalmente agnostico per quanto riguarda le risorse dati dei tuoi partner. Con l'accesso a più origini dati, AAM offre agli editori digitali la possibilità di utilizzare un'ampia gamma di dati di terze parti e la nostra co-op dati privata. To learn more about AAM, see the AAM documentation [Audience Manager Product Documentation.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**Trasferimento di dati VA nel trasferimento di dati di AAM -** Per i contenuti video e i video pubblicitari, le metriche e i metadati raccolti utilizzando le variabili della soluzione (riservato) possono essere inviati automaticamente ad AAM. Il trasferimento di dati è disponibile su tutte le piattaforme, inclusi desktop, dispositivi mobili e OTT. Per abilitare questo trasferimento di dati lato server, dovete contattare Adobe Client Care e chiedere di abilitare il feed.

>[!IMPORTANT]
>
>Per garantire il trasferimento uniforme dei dati ad AAM, dovresti essere nelle versioni più recenti delle librerie di Media SDK.

I dati Federati supportano completamente la condivisione di dati in AAM. Per confermare le impostazioni dei dati federati, contattate il team Adobe.

## OTT / AAM methods {#section_yqq_5br_v2b}

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

   Restituisce il profilo del visitatore ottenuto più di recente. Restituisce un obje vuoto se non è stato ancora inviato alcun segnale.

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

