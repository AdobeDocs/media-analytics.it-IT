---
seo-title: Tracciamento in SceneGraph (Roku)
title: Tracciamento in SceneGraph (Roku)
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
translation-type: tm+mt
source-git-commit: 3e115cbbae77413743764ed0757af9ac99965d6e

---


# Tracciamento in SceneGraph (Roku){#tracking-in-scenegraph-roku}

## Introduzione {#introduction}

Roku ha introdotto un nuovo quadro di programmazione per lo sviluppo di applicazioni: il framework di programmazione XML di SceneGraph. Questo nuovo framework presenta due nuovi concetti chiave:

* Rendering di SceneGraph delle schermate applicazione
* Configurazione XML delle schermate di SceneGraph

L’SDK di Adobe Mobile per Roku è scritto in BrightScript. L’SDK utilizza molti componenti che non sono disponibili per un’app in esecuzione su SceneGraph (ad esempio, thread). Di conseguenza, uno sviluppatore di app Roku che intende utilizzare il framework SceneGraph non può chiamare le API SDK di Adobe Mobile (queste sono simili a quelle disponibili nelle app BrightScript precedenti).

## Architettura {#architecture}

Per aggiungere il supporto di SceneGraph all’SDK di Adobe Mobile, Adobe ha aggiunto una nuova API che crea un ponte di connessione tra l’SDK di Adobe Mobile e `adbmobileTask`. Quest'ultimo è un nodo di SceneGraph utilizzato per l'esecuzione dell'API dell'SDK. (L'utilizzo di `adbmobileTask` è spiegato in dettaglio nel resto del documento.)

Il ponte di connessione è progettato per essere eseguito come segue:

* Il bridge restituisce un’istanza compatibile con SceneGraph dell’SDK AdobeMobile. L’SDK compatibile con SceneGraph include tutte le API che l’SDK precedente espone.
* Le API SDK di Adobe Mobile vengono utilizzate in SceneGraph in modo molto simile a quello delle API legacy.
* Il bridge inoltre espone un meccanismo di ascolto delle callback per le API che restituiscono alcuni dati.

![](assets/SceneGraph_arch.png)

## Componenti {#components}

**Applicazione SceneGraph:**

* Utilizza `AdobeMobileLibrary` le API tramite le API del connettore di SceneGraph.
* Registri per i callback di risposta su `adbmobileTask` per le variabili di dati di output previste.

**AdobeMobileLibrary:**

* Mostra un set di API pubbliche (legacy), inclusa l'API del bridge di connettore.
* Restituisce un'istanza del connettore SceneGraph che racchiude tutte le API pubbliche legacy.
* Comunica con un nodo `adbmobileTask` SceneGraph per l’esecuzione di API.

**nodo adbmobileTask:**

* Nodo attività di SceneGraph che esegue `AdobeMobileLibrary` le API in un thread in background.
* Funge da delegato per restituire i dati alle scene dell’applicazione.

## API Public SceneGraph {#public-scenegraph-apis}

### ADBMobileConnector

| Categoria | Nome metodo | Descrizione |
|---|---|---|
| **Costanti** |  |  |
|  | `sceneGraphConstants` | Restituisce un oggetto contenente `SceneGraphConstants`. Per ulteriori informazioni, fare riferimento alla tabella precedente. |
|  |  |  |
| **Registrazione debug** |  |  |
|  | `setDebugLogging` | API di SceneGraph per impostare la registrazione di debug sull’SDK ADBMobile. |
|  | `getDebugLogging` | API di SceneGraph per ottenere la registrazione di debug dall’SDK ADBMobile. |
|  | Per ulteriori informazioni, consulta la sezione Debug Logging dell’SDK precedente. |  |
|  |  |  |
| **Stato privacy / Rifiuto** |  |  |
|  | `setPrivacyStatus` | API di SceneGraph per impostare lo stato di privacy nell’SDK ADBMobile. |
|  | `getPrivacyStatus` | API di SceneGraph per ottenere lo stato di privacy dall’SDK ADBMobile. |
|  | Per ulteriori informazioni, consulta la sezione relativa al rifiuto/allo stato della privacy dell’SDK precedente. |  |
|  |  |  |
| **Analytics** |  |  |
|  | `trackState` | API di SceneGraph per tenere traccia dello stato nell’SDK ADBMobile. |
|  | `trackAction` | API di SceneGraph per tenere traccia dell’azione sull’SDK ADBMobile. |
|  | `trackingIdentifier` | API di SceneGraph per ottenere un identificatore di tracciamento dall’SDK ADBMobile. |
|  | `userIdentifier` | API di SceneGraph per ottenere un identificatore utente dall’SDK ADBMobile. |
|  | `setUserIdentifier` | API di SceneGraph per impostare l’identificatore utente nell’SDK ADBMobile. |
|  | `getAllIdentifiers` | L’API SceneGraph recupera tutte le identità utente note e persistenti dall’SDK Roku. |
|  | Per ulteriori informazioni, consulta la sezione Analisi dell’SDK legacy. |  |
|  |  |  |
| **Experience Cloud** |  |  |
|  | `visitorSyncIdentifiers` | API di SceneGraph per sincronizzare gli identificatori Experience Cloud nell’SDK ADBMobile. |
|  | `visitorMarketingCloudID` | API di SceneGraph per ottenere l’ID Experience Cloud del visitatore dall’SDK ADBMobile. |
|  | Per ulteriori informazioni, consulta la sezione Experience Cloud dell’SDK legacy. |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | API di SceneGraph per inviare un segnale di gestione dell'audience con caratteristiche. |
|  | `audienceVisitorProfile` | API di SceneGraph per ottenere un profilo visitatore di Audience Manager dall’SDK ADBMobile. |
|  | `audienceDpid` | API di SceneGraph per ottenere un feed di pubblico dall’SDK ADBMobile. |
|  | `audienceDpuuid` | API di SceneGraph per ottenere un audience Dpuuid dall’SDK ADBMobile. |
|  | `audienceSetDpidAndDpuuid` | API di SceneGraph per impostare audience Dpid e Dpuuid nell’SDK di ADBMobile. |
|  | Per ulteriori informazioni, consulta la sezione Audience Manager dell’SDK precedente. |  |
|  |  |  |
| **MediaHeartbeat** |  |  |
|  | `mediaTrackLoad` | API di SceneGraph per caricare il contenuto video per il tracciamento di MediaHeartbeat. |
|  | mediaTrackStart | API di SceneGraph per avviare la sessione di tracciamento video utilizzando MediaHeartbeat. |
|  | `mediaTrackUnload` | API di SceneGraph per scaricare il contenuto video dal tracciamento di MediaHeartbeat. |
|  | `mediaTrackPlay` | API di SceneGraph per tenere traccia della riproduzione del contenuto video. |
|  | mediaTrackPause | API di SceneGraph per tenere traccia del contenuto video in pausa. |
|  | `mediaTrackComplete` | API di SceneGraph per tenere traccia della riproduzione completata per il contenuto video. |
|  | `mediaTrackError` | API di SceneGraph per tenere traccia degli errori di riproduzione. |
|  | mediaTrackEvent | API di SceneGraph per tenere traccia degli eventi di riproduzione durante il tracciamento. Ad esempio: Annunci, capitoli. |
|  | `mediaUpdatePlayhead` | API di SceneGraph per l’invio di aggiornamenti dell’indicatore di riproduzione a MediaHeartbeat durante il tracciamento video. |
|  | `mediaUpdateQoS` | API di SceneGraph per l’invio di aggiornamenti QoS a MediaHeartbeat durante il tracciamento video. |
|  | Per ulteriori informazioni, consulta la sezione MediaHeartbeat dell’SDK precedente. |  |

### SceneGraphConstants

| Nome costante | Descrizione |
|---|---|
| `API_RESPONSE` | Utilizzato per recuperare l'oggetto response dal campo del `adbmobileTask` nodo `adbmobileApiResponse` |
| `DEBUG_LOGGING` | Usato come `apiName` per `getDebugLogging` |
| `PRIVACY_STATUS` | Usato come `apiName` per `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Usato come `apiName` per `trackingIdentifier` |
| `USER_IDENTIFIER` | Usato come `apiName` per `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Usato come `apiName` per `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Usato come `apiName` per `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Usato come `apiName` per `audienceDpid` |
| `AUDIENCE_DPUUID` | Usato come `apiName` per `audienceDpuuid` |

### nodo adbmobileTask

<table>
<thead>
<tr>
<td> Campo </td><td> Type (Tipo) </td><td> impostazione predefinita </td><td> Utilizzo </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assocarray </td>
<td> Non valido </td>
<td> NON modificare questo campo o lasciare che sia utilizzato dall'applicazione. Questo campo viene utilizzato da ADBMobile SceneGraphConnector per indirizzare le chiamate API tramite i nodi di SceneGraph e per recuperare le risposte. Pertanto, questo campo/chiave è riservato per AdobeMobileSDK per la compatibilità con SceneGraph. <b></b> Importante: Qualsiasi modifica apportata a questo campo potrebbe causare un funzionamento non corretto di AdobeMobileSDK.</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> Non valido </td>
<td> Tutte le API eseguite su AdobeMobileSDK restituiranno risposte in questo campo. Registratevi per una callback per ascoltare gli aggiornamenti a questo campo per ricevere gli oggetti di risposta. Segue il formato dell'oggetto response:  
<codeblock>
response = { "apiName" : &lt;SceneGraphConstants.
               API_NAME&gt; "returnValue: &lt;API_RESPONSE&gt; } 
</codeblock>
Un'istanza di questo oggetto risposta verrà inviata per qualsiasi chiamata API su AdobeMobileSDK che deve restituire un valore come indicato nella guida di riferimento API. Ad esempio, una chiamata API per visitorMarketingCloudID() restituirà il seguente oggetto di risposta: 
<codeblock>
response = { "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID "returnValue: "07050x25671x33760x72644x14" } 
</codeblock>
Oppure, anche i dati della risposta possono non essere validi: 
<codeblock>
response = { "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID "returnValue: non valido } 
</codeblock>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

Firma API: `ADBMobile().getADBMobileConnectorInstance()`\
Ingresso: Tipo `adbmobileTask`di reso: `ADBMobileConnector`

#### `sgConstants`

Firma API: `ADBMobile().sgConstants()`Ingresso: None\
Tipo di restituzione: `SceneGraphConstants`

>[!NOTE]
>Per informazioni dettagliate, consultate il riferimento `ADBMobileConnector` API.

### Costanti ADBMobile

|  Funzione  | Nome costante | Descrizione   |
|---|---|---|
| Versione | `version` | Costante per il recupero delle informazioni sulla versione di AdobeMobileLibrary |
| Privacy/rinuncia | `PRIVACY_STATUS_OPT_IN` | Costante per lo stato di privacy selezionato in |
|  | `PRIVACY_STATUS_OPT_OUT` | Costante dello stato di privacy rifiutata |
| Costanti MediaHeartbeat | Fare riferimento alle costanti presenti in questa pagina: Metodi <br/><br/>[Media Heartbeat.](/help/sdk-implement/track-av-playback/track-core/track-core-roku.md) | Utilizzate queste costanti con le API MediaHeartbeat |
| Metadati standard | Fare riferimento alle costanti presenti in questa pagina: Parametri di metadati <br/><br/>[standard.](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Utilizzate queste costanti per associare metadati video/annunci standard nelle API MediaHeartbeat |

Le `MediaHeartbeat` API di utilità definite a livello globale presenti nella precedente AdobeMobileLibrary sono accessibili *come accade* nell’ambiente SceneGraph, in quanto non utilizzano componenti Brightscript non disponibili nei nodi SceneGraph. Per ulteriori informazioni su questi metodi, vedere la tabella seguente:

### Metodi globali per MediaHeartbeat

| Metodo | Descrizione |
| --- | --- |
| `adb_media_init_mediainfo` | Questo metodo restituisce un oggetto Media Information inizializzato `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | Questo metodo restituisce l'oggetto Ad Information inizializzato `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | Questo metodo restituisce l’oggetto Informazioni capitolo inizializzato.  `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | Questo metodo restituisce l'oggetto AdBreak Information inizializzato.  `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | Questo metodo restituisce un oggetto Informazioni QoS inizializzato.  `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementazione {#implementation}

1. **Scarica la libreria Roku -** Scarica la libreria Roku [più recente.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)

1. **Configurare l'ambiente di sviluppo**

   1. Copia `adbmobile.brs` (AdobeMobileLibrary) nella `pkg:/source/` directory.

   1. Per il supporto di Scene Graph, copiate `adbmobileTask.brs` e `adbMobileTask.xml` inserite nella `pkg:/components/` directory.

1. **Inizializza**

   1. Importa `adbmobile.brs` nella scena.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Create un’istanza di `adbmobileTask` nodo nella scena.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Ottenete un'istanza di `adbmobile` connettore per SceneGraph utilizzando l' `adbmobileTask` istanza.

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Ottenete costanti `adbmobile` SG.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Registra un callback per la ricezione dell'oggetto risposta per tutte le chiamate `AdbMobile` API.

      ```
      m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE,  
                                   "onAdbmobileApiResponse") 
      
      ' Sample implementation of the callback 
      ' Listen for all the constants for which API calls are made on the SDK 
      function onAdbmobileApiResponse() as void 
          responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
      
          if responseObject <> invalid 
              methodName = responseObject.apiName 
              retVal = responseObject.returnValue 
      
              if methodName = m.adbmobileConstants.DEBUG_LOGGING 
                  if retVal 
                      print "API Response: DEBUG LOGGING: " + "True" 
                  else 
                      print "API Response: DEBUG LOGGING: " + "False" 
                  endif 
              else if methodName = m.adbmobileConstants.PRIVACY_STATUS 
                  print "API Response: PRIVACY STATUS: " + retVal 
              else if methodName = m.adbmobileConstants.TRACKING_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: TRACKING IDENTIFIER: " + retVal 
                  else 
                      print "API Response: TRACKING IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.USER_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: USER IDENTIFIER: " + retVal 
                  else 
                      print "API Response: USER IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.VISITOR_MARKETING_CLOUD_ID 
                  if retVal <> invalid 
                      print "API Response: MCID: " + retVal 
                  else 
                      print "API Response: MCID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPUUID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPUUID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPUUID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_VISITOR_PROFILE 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE VISITOR PROFILE: Valid Object" 
                  else 
                      print "API Response: AUDIENCE VISITOR PROFILE: " + "invalid" 
                  endif 
              endif 
          endif 
      end function 
      ```

## Implementazione di esempio {#sample-implementation}

### Chiamate API di esempio per l’SDK legacy

```
'get an instance of SDK 
m.adbmobile = ADBMobile() 
   
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
   
'execute getter APIs 
debugLogging = m.adbmobile.getDebugLogging()
```

### Chiamate API di esempio per SDK SG

```
'create adbmobileTask instance 
m.adbmobileTask = createObject("roSGNode", "adbmobileTask") 
   
'get an instance of SDK using task instance 
m.adbmobile =  
  ADBMobile().getADBMobileConnectorInstace(m.adbmobileTask) 
m.adbmobileConstants = m.adbmobile.sceneGraphConstants() 
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
  
'execute getter APIs 
m.adbmobileTask.ObserverField(m.adbConstants.API_RESPONSE,  
                              "onAdbmobileApiResponse") 
m.adbmobile.getDebugLogging() 
   
'listen for return data in registered callbacks 
function onAdbmobileApiResponse() as void 
    responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
  
        if responseObject <> invalid 
            methodName = responseObject.apiName 
            retVal = responseObject.returnValue 
  
        if methodName = m.adbmobileConstants.DEBUG_LOGGING 
            if retVal 
                print "API Response: DEBUG LOGGING: " + "True" 
            else 
                print "API Response: DEBUG LOGGING: " + "False" 
         endif 
    endif 
end function
```

