---
title: Aggiornamenti della documentazione
description: null
uuid: 1f3e48df-83b6-418c-8cf7-d7946481f79
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Risorse{#resources}

## Note sulla versione{#release-notes} 

* [Note sulla versione](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## Aggiornamenti alla documentazione{#documentation-updates}

### Last updated: October, 2019 {#October-2019-update}

Numerose correzioni di modifica e formattazione.
Gli argomenti della guida sono stati estesi oltre a Media SDK, incluso un nuovo argomento della guida "Media Dimensions", al di fuori del tracciamento dei contenuti multimediali.


### Last updated: March 7, 2019 {#March-2019-update}

* Questo aggiornamento è stato utilizzato principalmente per la versione 2.2 di Media SDK sulle piattaforme JavaScript e OTT.
* La release 2.2 Media SDK sulle piattaforme JavaScript e OTT fornisce lo stesso supporto descritto di seguito per le piattaforme iOS e Android (aggiornamento 1 novembre 2018).

### Last updated: November 1, 2018 {#November-2018-update}

* Questo aggiornamento è stato utilizzato principalmente per la versione 2.2 di Media SDK sulle piattaforme Android e iOS.
* La versione 2.2 di Media SDK su Android e iOS fornisce il supporto per il tracciamento dell'audio su queste piattaforme, insieme a miglioramenti interni.
* Con l’aggiunta del tracciamento audio e con funzionalità di tracciamento audio e video ora disponibili sia in Media SDK che nell’API di Media Collection, è necessario un aggiornamento del nome relativamente all’ingrosso:

   * La soluzione globale è denominata Adobe Analytics for Audio and Video
   * La abbreviazione precedentemente utilizzata nei documenti, "Video Analytics", è ora "Media Analytics"
   * Nell’SDK, i riferimenti a "Video Heartbeat Library (VHL)" sono ora "Media SDK"
   * Nomi di file e URL (ad esempio, collegamenti a riferimenti API) che in precedenza facevano riferimento a "video" o "vhl" ora utilizzano "media" al loro posto
   * Nel codice, i nomi delle chiavi di metadati ora includono "MEDIA" invece di "VIDEO"
   * e così via...

* Oltre a quanto sopra, nella sezione Media SDK sono state apportate ulteriori ristrutturazioni, tra cui l’implementazione di metadati standard e il riferimento al ritorno ai propri argomenti (sono stati assorbiti negli argomenti *Track Core* nel precedente aggiornamento del documento). Questi argomenti, insieme al core ** Track, alla ricerca ** Track e agli argomenti relativi al buffering ** Track, ora sono raggruppati nella sezione *Track audio and video play*(Tracciare la riproduzione audio e video).

* Il modulo Analisi federata è stato aggiornato alla versione 3.2 per riflettere i nuovi parametri coinvolti nel tracciamento dell'audio.

### Aggiorna: 10 ottobre 2018 {#October-2018-update}

* La struttura del documento è stata "modificata" nell’area Implementazione SDK, combinando le singole guide all’implementazione della piattaforma (ma per lo più identiche) in un’unica sezione di implementazione SDK, con esempi di tracciamento specifici della piattaforma presentati nelle sottosezioni sotto argomenti comuni di tracciamento.
* I file sono stati rinominati in attesa della migrazione a un nuovo sistema doc. Sono stati eliminati tutti i prefissi DITA ( c_, r_, t_ ) che indicano rispettivamente il concetto, il riferimento e i tipi di argomento attività). Tutti i caratteri di sottolineatura ('_') sono stati sostituiti da trattini ('-'). Inoltre, i nomi dei file ora assomigliano maggiormente ai titoli degli argomenti.
* Aggiornamenti agli argomenti Generali di Convalida e Certificazione.
* Nuovo materiale introduttivo che include una presentazione delle opzioni di misurazione, aggiornamenti dei prerequisiti, percorsi di implementazione e abilitazione di Audience Manager.
* Aggiornamenti alle sezioni Metriche e Metadati, Reporting and Analysis, che riflettono l'aggiunta delle funzionalità di analisi audio.
