---
seo-title: Tracciare gli stati delle app
title: Tracciare gli stati delle app
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# Track app states{#track-app-states}

Per "stati" si intendono le diverse schermate o visualizzazioni disponibili nell'app. Ogni volta che nell’applicazione viene visualizzato un nuovo stato, dovreste inviare una `trackState` chiamata. Ad esempio, quando un utente si sposta dalla home page alla schermata dei dettagli del video, invia una `trackState` chiamata. Gli stati vengono generalmente visualizzati utilizzando un rapporto sui percorsi, per consentire agli utenti di vedere in che modo navigano nell'app e quali stati vengono visualizzati più comunemente.

## Chiamate a trackState

In genere si chiama `trackState` ogni volta che l'app carica una nuova schermata.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. In altre interfacce di Analytics, "Stato di visualizzazione" è indicato come "Nome pagina"; "Viste di stato" è riportato come "Visualizzazioni di pagina".

## Invia dati contestuali

Oltre a "Nome stato", con ogni chiamata di tracciamento dello stato puoi inviare anche dati di contesto aggiuntivi.

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

