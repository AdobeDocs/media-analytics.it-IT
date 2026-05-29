---
title: Spiegazione di rinuncia e privacy
description: Scopri come gestire il consenso, la rinuncia e la privacy.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 750
ht-degree: 4%

---

# Rinuncia e privacy

Quando un utente rinuncia al tracciamento, la libreria di contenuti multimediali in streaming interrompe immediatamente tutte le attività di raccolta dati. Non vengono inviate chiamate di avvio della sessione, ping heartbeat né dati di tracciamento degli eventi ai server di raccolta dati di Adobe per tale utente.

## Rinuncia / Consenso

I controlli di rinuncia funzionano per dispositivo o browser. Il rispetto del consenso degli utenti è responsabilità dell&#39;organizzazione incaricata dell&#39;attuazione. Per una panoramica delle procedure di privacy di Adobe, visita il [Centro per la privacy di Adobe](https://www.adobe.com/it/privacy.html).

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Il Web SDK rispetta le preferenze di consenso impostate utilizzando il comando `setConsent`. Quando il consenso è impostato su `"out"`, Web SDK smette di inoltrare tutti gli eventi, incluse le chiamate di tracciamento dei contenuti multimediali in streaming, ad Edge Network. Lo stato di consenso persiste nell’archiviazione del browser tra le sessioni.

Prima di implementare la rinuncia, accertati che il Web SDK sia configurato con il componente Streaming Media. Per ulteriori informazioni, vedere [Configurare Web SDK](../implementation/edge/edge-web-sdk.md).

Imposta il consenso alla rinuncia utilizzando lo standard di consenso Adobe 2.0:

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

Valori di consenso:

* `"y"`: consenso (raccolta dati consentita)
* `"n"`: Opted out (raccolta dati soppressa)
* `"p"`: in sospeso (in attesa della decisione dell&#39;utente; nessun dato raccolto fino alla risoluzione)

Per ripristinare il tracciamento, chiamare di nuovo `setConsent` con `"y"` come valore `collect.val`.

Per altri formati, incluso IAB TCF 2.0, vedere il comando [setConsent](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/setconsent) nella documentazione di Web SDK.

>[!TAB iOS]

Adobe Experience Platform Mobile SDK rispetta lo stato di privacy impostato utilizzando `MobileCore.setPrivacyStatus()`. Se si imposta lo stato su `.optedOut`, verrà eliminata tutta la raccolta dati in tutte le estensioni di AEP, incluso Streaming Media. Lo stato persiste nelle sessioni dell’app.

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

Per ripristinare il tracciamento, impostare di nuovo lo stato di privacy su `.optedIn`:

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

Per ulteriori informazioni, consulta [Privacy e RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) nella documentazione di AEP Mobile SDK.

>[!TAB Android]

Adobe Experience Platform Mobile SDK rispetta lo stato di privacy impostato utilizzando `MobileCore.setPrivacyStatus()`. Se si imposta lo stato su `MobilePrivacyStatus.OPT_OUT`, verrà eliminata tutta la raccolta dati in tutte le estensioni di AEP, incluso Streaming Media. Lo stato persiste nelle sessioni dell’app.

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

Per ripristinare il tracciamento, impostare di nuovo lo stato di privacy su `MobilePrivacyStatus.OPT_IN`:

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

Per ulteriori informazioni, consulta [Privacy e RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) nella documentazione di AEP Mobile SDK.

>[!TAB Roku]

AEP Roku SDK utilizza `setConsent()` con lo standard di consenso Adobe 2.0. L&#39;impostazione di `collect.val` su `"n"` interrompe immediatamente tutte le raccolte di dati, inclusi gli eventi multimediali in streaming.

Valori di consenso:

* `"y"` — Consenso accordato (raccolta dati consentita)
* `"n"` — Opted out (raccolta dati soppressa)
* `"p"` — In sospeso (in attesa della decisione dell&#39;utente; nessun dato raccolto fino alla risoluzione)

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

Per ripristinare il tracciamento, impostare `collect.val` su `"y"` e chiamare di nuovo `setConsent()`.

È inoltre possibile impostare un valore di consenso predefinito all&#39;inizializzazione di SDK utilizzando `updateConfiguration()` con la chiave `ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT`. Per ulteriori informazioni, consulta la [documentazione di AEP Roku SDK](https://github.com/adobe/aepsdk-roku).

>[!TAB API Media Edge]

L’API di Media Edge è un’implementazione lato server. Nessun livello SDK applica automaticamente il consenso: l’applicazione deve controllare lo stato del consenso dell’utente prima di effettuare chiamate API ed eliminare le richieste per gli utenti che hanno rinunciato.

Per la rinuncia completa, non pubblicare sull&#39;endpoint `/va/v2/sessions` (o su qualsiasi endpoint evento successivo) per gli utenti che hanno rinunciato:

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

Per ulteriori informazioni, consulta il [Riferimento API di Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

La libreria Media SDK JS 3.x fa riferimento allo stato di rinuncia di Adobe Visitor API (Identity Service). Quando un utente rinuncia utilizzando l’API Visitor, Media SDK sopprime automaticamente tutte le chiamate di tracciamento.

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

Sostituisci `YOUR_ORG_ID@AdobeOrg` con il tuo ID organizzazione da Adobe Admin Console.

Per ripristinare il tracciamento, passare `false` a `setOptOut()`.

Per ulteriori informazioni, vedere [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

>[!TAB Chromecast]

Chromecast Media SDK 3.x rispetta lo stato di privacy impostato utilizzando `ADBMobile.config.setPrivacyStatus()`. L&#39;impostazione dello stato su `PRIVACY_STATUS_OPT_OUT` comporta l&#39;eliminazione di tutte le raccolte di dati.

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

Per ripristinare il tracciamento, imposta di nuovo lo stato su acconsentito:

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

È inoltre possibile impostare lo stato di privacy predefinito all&#39;inizializzazione di SDK nell&#39;oggetto `ADBMobileConfig`:

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB API Media Collection]

L’API Media Collection è un’implementazione lato server. L’applicazione deve controllare lo stato del consenso dell’utente prima di effettuare chiamate API ed eliminare le richieste per gli utenti che hanno rinunciato.

Per la rinuncia completa, non pubblicare sull’endpoint delle sessioni per gli utenti che hanno rinunciato.

Per le rinunce parziali in base al CCPA, includere i flag di rinuncia nell&#39;oggetto `params` della richiesta `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`: Imposta su `true` per rifiutare la condivisione dei dati tra Adobe Analytics e altre soluzioni Experience Cloud (come Audience Manager).
* `analytics.optOutShare`: impostato su `true` per rinunciare alla condivisione di dati federati con altri client Adobe Analytics.

Per un elenco completo dei parametri disponibili, consulta il [Riferimento dei parametri della richiesta API di Media Collection](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md).

>[!ENDTABS]
