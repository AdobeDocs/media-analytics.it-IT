---
title: Tracciare gli stati dell’app
description: Per “stati dell'app” si intendono le diverse schermate o visualizzazioni disponibili nell'app. Scopri come tenere traccia degli stati dell’app nell’applicazione utilizzando la chiamata trackState.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/fVNQ4CIqXbSYyi32rBlB2B9S6YTsBwxJhD3XaeDcDIE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 100%

---

# Tracciare gli stati dell’app{#track-app-states}

Per &quot;stati&quot; si intendono le diverse schermate o visualizzazioni disponibili nell&#39;app. Ogni volta che nell&#39;applicazione viene visualizzato un nuovo stato, è necessario inviare una chiamata `trackState`. Ad esempio, quando un utente passa dalla pagina Home alla schermata dei dettagli video, invia una chiamata `trackState`. Per visualizzare gli stati si usa solitamente un rapporto sui percorsi che consente di vedere in che modo gli utenti navigano nell’app e quali stati vengono visualizzati maggiormente.

## Chiamate a trackState

In genere, l&#39;utente invia una chiamata `trackState` ogni volta che l’app carica una nuova schermata.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

In Adobe Mobile Services, il Nome dello stato è riportato nella variabile &quot;View State&quot;, e viene registrata una visualizzazione per ogni chiamata `trackState`. Nelle altre interfacce di Analytics, &quot;Stato di visualizzazione&quot; è indicato come &quot;Nome pagina&quot; e le visualizzazioni degli stati sono indicate come &quot;Visualizzazioni di pagina&quot;.

## Inviare dati contestuali

Oltre a &quot;Nome stato&quot;, con ogni chiamata di tracciamento dello stato puoi inviare anche dati di contesto aggiuntivi.

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
