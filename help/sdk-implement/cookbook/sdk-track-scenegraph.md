---
seo-title: Tracciamento in scenegraph (Roku)
title: Tracciamento in scenegraph (Roku)
uuid: fa 85 e 546-c 79 b -4 df 4-8 c 03-d 6593 fa 296 d 5
translation-type: tm+mt
source-git-commit: 654aaef5d816e75429975d04c4e81ad4d4b6f706

---


# Tracking in SceneGraph (Roku){#tracking-in-scenegraph-roku}

## Introduzione {#section_vfr_zcz_y2b}

Roku ha introdotto un nuovo framework di programmazione per lo sviluppo di applicazioni: il framework di programmazione XML scenegraph. Questo nuovo framework offre due nuovi concetti chiave:

* Rendering scenegrafico delle schermate dell'applicazione
* Configurazione XML delle schermate scenegraph

L'SDK di Adobe Mobile per Roku è scritto in brightscript. L'SDK utilizza molti componenti non disponibili per un'app in esecuzione su scenegraph (ad esempio, thread). Pertanto, un sviluppatore di app Roku che intende utilizzare il framework scenegraph non può chiamare le API SDK di Adobe Mobile (questi ultimi sono simili a quelli disponibili nelle app brightscript precedenti).

## Architecture {#section_dj5_1dz_y2b}

To add SceneGraph support to the AdobeMobile SDK, Adobe has added a new API that creates a connector bridge between the AdobeMobile SDK and `adbmobileTask`. Quest'ultimo è un nodo scenegraph utilizzato per l'esecuzione dell'API dell'SDK. (Usage of `adbmobileTask` is explained in detail throughout the rest of this document.)

Il ponte del connettore è progettato come segue:

* Il bridge restituisce un'istanza compatibile con scenegraph dell'SDK di adobemobile. L'SDK compatibile con scenegraph dispone di tutte le API che l'SDK legacy espone.
* In scenegraph utilizzate le API SDK di adobemobile in modo molto simile a come sono state usate le API precedenti.
* Il ponte fornisce inoltre un meccanismo per ascoltare le callback per le API che restituiscono alcuni dati.

![](assets/SceneGraph_arch.png)

## Componenti {#section_jwl_wqx_1bb}

**Applicazione scenegraph:**

* Consumes `AdobeMobileLibrary` APIs via the SceneGraph connector bridge APIs.
* Registers for response callbacks on `adbmobileTask` for expected output data variables.

**Adobemobilelibrary:**

* Espone un set di API pubbliche (legacy), inclusa l'API del ponte connector.
* Restituisce un'istanza di connettore scenegraph che racchiude tutte le API pubbliche precedenti.
* Communicates with an `adbmobileTask` SceneGraph node for execution of APIs.

**Adbmobiletask Node:**

* A SceneGraph task node that executes `AdobeMobileLibrary` APIs on a background thread.
* Funge da delegato per tornare alle scene dell'applicazione.

## Public SceneGraph APIs {#section_jyd_hdz_y2b}

### Adbmobileconnector

| Categoria | Nome metodo | Descrizione |
|---|---|---|
| **Costanti** |  |  |
|  | `sceneGraphConstants` | Returns an object containing `SceneGraphConstants`. Fare riferimento alla tabella riportata sopra per ulteriori dettagli. |
|  |  |  |
| **Registrazione di debug** |  |  |
|  | `setDebugLogging` | API scenegraph per impostare l'accesso di debug nell'SDK adbmobile. |
|  | `getDebugLogging` | API scenegraph per ottenere la registrazione di debug dall'SDK adbmobile. |
|  | Per ulteriori informazioni, consulta la sezione Registrazione debug dell'SDK legacy. |  |
|  |  |  |
| **Stato della privacy/Rinuncia** |  |  |
|  | `setPrivacyStatus` | API scenegraph per impostare lo stato di privacy nell'SDK adbmobile. |
|  | `getPrivacyStatus` | API scenegraph per ottenere lo stato di privacy dall'SDK adbmobile. |
|  | Per ulteriori informazioni, consulta la sezione Stato di privacy/rinuncia dell'SDK legacy. |  |
|  |  |  |
| **Analytics** |  |  |
|  | `trackState` | API scenegraph per tenere traccia dello stato sull'SDK adbmobile. |
|  | `trackAction` | API scenegraph per tenere traccia dell'azione nell'SDK adbmobile. |
|  | `trackingIdentifier` | API scenegraph per ottenere un identificatore di tracciamento dall'SDK adbmobile. |
|  | `userIdentifier` | API scenegraph per ottenere un identificatore utente dall'SDK adbmobile. |
|  | `setUserIdentifier` | API scenegraph per impostare l'identificatore utente nell'SDK adbmobile. |
|  | `getAllIdentifiers` | L'API scenegraph recupera tutte le identità utente conosciute e persistenti da Roku SDK. |
|  | Per ulteriori informazioni, consulta la sezione Analisi dell'SDK legacy. |  |
|  |  |  |
| **Experience Cloud** |  |  |
|  | `visitorSyncIdentifiers` | API scenegraph per sincronizzare identificatori Experience Cloud nell'SDK adbmobile. |
|  | `visitorMarketingCloudID` | API scenegraph per ottenere Experience Cloud ID dall'SDK adbmobile. |
|  | Per ulteriori informazioni, consulta la sezione Experience Cloud dell'SDK legacy. |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | API scenegraph per inviare un segnale di gestione dell'audience con caratteristiche. |
|  | `audienceVisitorProfile` | API scenegraph per ottenere un profilo visitatore Audience Manager dall'SDK adbmobile. |
|  | `audienceDpid` | API scenegraph per ottenere un'audience Dpid dall'SDK adbmobile. |
|  | `audienceDpuuid` | API scenegraph per ottenere un dpuuid audience dall'SDK adbmobile. |
|  | `audienceSetDpidAndDpuuid` | API scenegraph per impostare l'audience Dpid e il Dpuuid sull'SDK adbmobile. |
|  | Per ulteriori informazioni, consulta la sezione Audience Manager dell'SDK legacy. |  |
|  |  |  |
| **Mediaheartbeat** |  |  |
|  | `mediaTrackLoad` | API scenegraph per caricare il contenuto video per il tracciamento mediaheartbeat. |
|  | Mediatrackstart | API scenegraph per avviare la sessione di tracciamento video utilizzando mediaheartbeat. |
|  | `mediaTrackUnload` | API scenegraph per scaricare il contenuto video dal tracciamento mediaheartbeat. |
|  | `mediaTrackPlay` | API scenegraph per tenere traccia della riproduzione del contenuto video. |
|  | Mediatrackpause | API scenegraph per tenere traccia del contenuto video in pausa. |
|  | `mediaTrackComplete` | API scenegraph per tenere traccia della riproduzione completata per il contenuto video. |
|  | `mediaTrackError` | API scenegraph per tenere traccia degli errori di riproduzione. |
|  | Mediatrackevent | API scenegraph per tenere traccia degli eventi di riproduzione durante il tracciamento. Ad esempio: Annunci, Capitoli. |
|  | `mediaUpdatePlayhead` | API scenegraph per inviare gli aggiornamenti di playhead a mediaheartbeat durante il tracciamento video. |
|  | `mediaUpdateQoS` | API scenegraph per inviare aggiornamenti qos a mediaheartbeat durante il tracciamento video. |
|  | Per ulteriori informazioni, consulta la sezione mediaheartbeat dell'SDK legacy. |  |

### Scenegraphconstants

| Nome costante | Descrizione |
|---|---|
| `API_RESPONSE` | Used to retrieve the response object from `adbmobileTask` node's `adbmobileApiResponse` field |
| `DEBUG_LOGGING` | Used as `apiName` for `getDebugLogging` |
| `PRIVACY_STATUS` | Used as `apiName` for `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Used as `apiName` for `trackingIdentifier` |
| `USER_IDENTIFIER` | Used as `apiName` for `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Used as `apiName` for `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Used as `apiName` for `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Used as `apiName` for `audienceDpid` |
| `AUDIENCE_DPUUID` | Used as `apiName` for `audienceDpuuid` |

### Adbmobiletask Node

<table>
<thead>
<tr>
<td> Campo </td><td> Type (Tipo) </td><td> impostazione predefinita </td><td> Utilizzo </td>
</tr>
</thead>
<tbody>
<tr>
<td> Adbmobileapicall </td>
<td> assocarray </td>
<td> Non valido </td>
<td> NON modificate questo campo o lasciate che sia utilizzato dall'applicazione. Questo campo viene usato dal gestore adbmobile scenegraphconnector per indirizzare le chiamate API tramite nodi scenegraph e per recuperare le risposte. Pertanto, questa chiave/campo è riservato per adobemobilesdk per compatibilità scenegraph. <b>Importante:</b> Qualsiasi modifica a questo campo potrebbe causare il funzionamento errato di adobemobilesdk.</td>
</tr>
<tr>
<td> Adbmobileapiresponse </td>
<td> assocarray </td>
<td> Non valido </td>
<td> Sola lettura Tutte le API eseguite su adobemobilesdk restituiranno le risposte su questo campo. Registrarsi per ricevere un callback in modo da ricevere gli aggiornamenti di questo campo per ricevere gli oggetti di risposta. Segue il formato dell'oggetto response:  
<codeblock>
response = {"apiname": &lt; Scenegraphconstants.
 API_ NAME &gt; 
 " Returnvalue: &lt; API_ RESPONSE &gt;} 
</codeblock>
Un'istanza di questo oggetto di risposta verrà inviata per qualsiasi chiamata API su adobemobilesdk che deve restituire un valore come nella guida di riferimento API. Ad esempio, una chiamata API per visitormarketingcloudid () restituirà il seguente oggetto risposta: 
<codeblock>
response = {"apiname": m.
 adbmobileconstants.
 VISITOR_ MARKETING_ CLOUD_ ID 
 " Returnvalue: " 07050 x 25671 x 33760 x 72644 x 14 "} 
</codeblock>
OR, anche i dati di risposta non possono essere validi: 
<codeblock>
response = { 
 " Apiname ": m.
 adbmobileconstants.
 VISITOR_ MARKETING_ CLOUD_ ID 
 " Returnvalue: invalid} 
</codeblock>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

API Signature: `ADBMobile().getADBMobileConnectorInstance()`\
Input: `adbmobileTask`
Return Type: `ADBMobileConnector`

#### `sgConstants`

API Signature: `ADBMobile().sgConstants()`
Input: None\
Return Type: `SceneGraphConstants`

>[!NOTE]
>Refer to the `ADBMobileConnector` API reference for details.

### Costanti adbmobile

|  Funzione  | Nome costante | Descrizione   |
|---|---|---|
| Gestione versioni | `version` | Costante per il retreiving di adobemobilelibrary verison info |
| Privacy/Rinuncia | `PRIVACY_STATUS_OPT_IN` | Costante per lo stato di privacy selezionata |
|  | `PRIVACY_STATUS_OPT_OUT` | La costante per lo stato di privacy ha acconsentito |
| Costanti mediaheartbeat | Refer to the constants on this page: <br/><br/>[Media Heartbeat Methods.](../../sdk-implement/track-av-playback/track-core/track-core-roku.md) | Utilizzare queste costanti con le API mediaheartbeat |
| Metadati standard | Refer to the constants on this page: <br/><br/>[Standard Metadata Parameters.](../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Utilizzate queste costanti per allegare metadati Video/Annuncio standard nelle API mediaheartbeat |

Globally defined utility `MediaHeartbeat` APIs on the legacy AdobeMobileLibrary are accessible *as is* in the SceneGraph enviromnent because they do not use any Brightscript components that are unavailable in SceneGraph nodes. Per ulteriori informazioni su questi metodi, fare riferimento alla tabella seguente:

### Metodi globali per mediaheartbeat

| Metodo | Descrizione |
| --- | --- |
| `adb_media_init_mediainfo` | This method returns an initialized Media Information object `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | This method returns initialized Ad Information object `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | This method returns initialized Chapter Information object.  `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | This method returns initialized AdBreak Information object.  `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | This method returns an initialized QoS Information object.  `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementazione {#section_dbz_ydz_y2b}

1. **Scarica la libreria Roku:** scarica la [libreria Roku più recente.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.0)

1. **Configurare l'ambiente di sviluppo**

   1. Copy `adbmobile.brs` (AdobeMobileLibrary) into your `pkg:/source/` directory.

   1. For Scene Graph support, copy `adbmobileTask.brs` and `adbMobileTask.xml` into your `pkg:/components/` directory.

1. **Inizializza**

   1. Import `adbmobile.brs` into your Scene.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Create an instance of `adbmobileTask` node into your Scene.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Get an instance of `adbmobile` connector for SceneGraph using the `adbmobileTask` instance.

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Get `adbmobile` SG constants.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Register a callback for receiving response object for all `AdbMobile` API calls.

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

## Sample Implementation {#section_mld_lfz_y2b}

### Chiamate API di esempio su Legacy SDK

```
'get an instance of SDK 
m.adbmobile = ADBMobile() 
   
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
   
'execute getter APIs 
debugLogging = m.adbmobile.getDebugLogging()
```

### Chiamate API di esempio su SG SDK

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

