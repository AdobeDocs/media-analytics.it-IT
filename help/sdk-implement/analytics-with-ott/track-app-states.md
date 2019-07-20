---
seo-title: Tracciare gli stati delle app
title: Tracciare gli stati delle app
uuid: 2 f 98 fb 43-c 362-4 a 9 b -8732-fa 7 e 963 da 729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# Track app states{#track-app-states}

Per "stati" si intendono le diverse schermate o visualizzazioni disponibili nell'app. Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. Gli stati vengono generalmente visualizzati utilizzando un rapporto percorsi, per vedere in che modo gli utenti navigano nell'app e quali stati vengono visualizzati più frequentemente.

## Chiamate a trackState

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. In altre interfacce di Analytics, «Stato di visualizzazione» è indicato come «Nome pagina»; «Visualizzazioni stato» è indicato come «Visualizzazioni di pagina».

## Inviare dati contestuali

Oltre a "Nome stato", puoi inviare dati di contesto aggiuntivi con ogni chiamata di tracciamento dello stato.

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

