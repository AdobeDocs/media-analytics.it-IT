---
title: Tracciamento stati dell’app
description: 'Gli stati dell’app sono schermate o visualizzazioni diverse all’interno dell’applicazione. Scopri come tracciare lo stato dell’app nell’applicazione utilizzando la chiamata trackState . '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 18%

---

# Tracciare gli stati dell’app{#track-app-states}

Per &quot;stati&quot; si intendono le diverse schermate o visualizzazioni disponibili nell&#39;app. Ogni volta che nell&#39;applicazione viene visualizzato un nuovo stato, devi inviare una chiamata `trackState` . Ad esempio, quando un utente passa dalla home page alla schermata dei dettagli video, invia una chiamata `trackState` . Gli stati vengono generalmente visualizzati utilizzando un rapporto sui percorsi, che consente di vedere in che modo gli utenti navigano nell’app e quali stati vengono visualizzati più comunemente.

## Chiamate a trackState

In genere, chiami `trackState` ogni volta che l’app carica una nuova schermata.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

Il nome dello stato viene riportato nella variabile &quot;Stato di visualizzazione&quot; in Adobe Mobile Services e viene registrata una visualizzazione per ogni chiamata `trackState`. Nelle altre interfacce di Analytics, &quot;Stato di visualizzazione&quot; è indicato come &quot;Nome pagina&quot;; Le &quot;Visualizzazioni di stato&quot; sono indicate come &quot;Visualizzazioni di pagina&quot;.

## Inviare dati contestuali

Oltre a &quot;Nome stato&quot;, puoi inviare dati contestuali aggiuntivi con ciascuna chiamata di tracciamento dello stato.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>I valori dei dati contestuali devono essere mappati su variabili personalizzate in Adobe Mobile Services.
