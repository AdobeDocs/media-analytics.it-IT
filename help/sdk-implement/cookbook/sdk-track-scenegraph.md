---
title: Tracciamento in SceneGraph (Roku)
description: Scopri come tenere traccia dei contenuti multimediali con il framework di programmazione XML Roku SceneGraph.
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
exl-id: e428d3cd-dbc7-48bb-82ff-61b6b892884c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 3%

---

# Tracciamento in SceneGraph (Roku){#tracking-in-scenegraph-roku}

## Introduzione {#introduction}

Roku ha introdotto un nuovo quadro di programmazione per lo sviluppo di applicazioni: il framework di programmazione XML di SceneGraph. Questo nuovo framework presenta due nuovi concetti chiave:

* Rendering di SceneGraph delle schermate dell&#39;applicazione
* Configurazione XML delle schermate di SceneGraph

L’SDK di Adobe Mobile per Roku è scritto in BrightScript. L’SDK utilizza molti componenti che non sono disponibili per un’app in esecuzione su SceneGraph (ad esempio, thread). Pertanto, uno sviluppatore di app Roku che intende utilizzare il framework SceneGraph non può chiamare le API SDK di Adobe Mobile (queste ultime sono simili a quelle disponibili nelle applicazioni BrightScript legacy).

## Architettura {#architecture}

Per aggiungere il supporto SceneGraph all&#39;SDK di Adobe Mobile, Adobe ha aggiunto una nuova API che crea un ponte di connettore tra l&#39;SDK di AdobeMobile e `adbmobileTask`. Quest&#39;ultimo è un nodo di SceneGraph utilizzato per l&#39;esecuzione dell&#39;API dell&#39;SDK. (L&#39;utilizzo di `adbmobileTask` viene spiegato in dettaglio in tutto il resto del documento.)

Il ponte di connessione è progettato per eseguire le seguenti operazioni:

* Il bridge restituisce un&#39;istanza compatibile con SceneGraph dell&#39;SDK AdobeMobile. L’SDK compatibile con SceneGraph dispone di tutte le API che l’SDK legacy espone.
* In SceneGraph utilizzi le API SDK di Adobe Mobile in modo molto simile a come utilizzavi le API legacy.
* Il bridge espone anche un meccanismo per ascoltare i callback per le API che restituiscono alcuni dati.

![](assets/SceneGraph_arch.png)

## Componenti {#components}

**Applicazione SceneGraph:**

* Utilizza le API `AdobeMobileLibrary` tramite le API del connettore SceneGraph bridge.
* Registri per i callback di risposta su `adbmobileTask` per le variabili di dati di output previste.

**AdobeMobileLibrary:**

* Espone un set di API pubbliche (legacy), inclusa l’API del bridge di connettore.
* Restituisce un&#39;istanza del connettore SceneGraph che racchiude tutte le API pubbliche legacy.
* Comunica con un nodo `adbmobileTask` SceneGraph per l&#39;esecuzione delle API.

**Nodo adbmobileTask:**

* Un nodo di attività di SceneGraph che esegue `AdobeMobileLibrary` API su un thread in background.
* Funge da delegato per restituire i dati alle scene dell&#39;applicazione.

## API pubbliche di SceneGraph {#public-scenegraph-apis}

### ADBMobileConnector

| Categoria | Nome metodo | Descrizione |
|---|---|---|
| **Costanti** |  |  |
|  | `sceneGraphConstants` | Restituisce un oggetto contenente `SceneGraphConstants`. Per ulteriori informazioni, fare riferimento alla tabella precedente. |
|  |  |  |
| **Debug Logging** |  |  |
|  | `setDebugLogging` | API di SceneGraph per impostare la registrazione di debug sull&#39;SDK ADBMobile. |
|  | `getDebugLogging` | API di SceneGraph per ottenere la registrazione di debug dall&#39;SDK ADBMobile. |
|  | Per ulteriori informazioni consulta la sezione Debug Logging dell’SDK legacy. |  |
|  |  |  |
| **Stato privacy / Rinuncia** |  |  |
|  | `setPrivacyStatus` | API di SceneGraph per impostare lo stato di privacy sull&#39;SDK di ADBMobile. |
|  | `getPrivacyStatus` | API di SceneGraph per ottenere lo stato di privacy dall’SDK di ADBMobile. |
|  | Per ulteriori informazioni, consulta la sezione Stato di rinuncia/privacy dell’SDK legacy. |  |
|  |  |  |
| **Analytics** |  |  |
|  | `trackState` | API di SceneGraph per tenere traccia dello stato nell’SDK ADBMobile. |
|  | `trackAction` | API di SceneGraph per tenere traccia dell&#39;azione sull&#39;SDK ADBMobile. |
|  | `trackingIdentifier` | API di SceneGraph per ottenere un identificatore di tracciamento dall&#39;SDK ADBMobile. |
|  | `userIdentifier` | API di SceneGraph per ottenere un identificatore utente dall&#39;SDK di ADBMobile. |
|  | `setUserIdentifier` | API di SceneGraph per impostare l&#39;identificatore utente nell&#39;SDK ADBMobile. |
|  | `getAllIdentifiers` | L&#39;API di SceneGraph recupera tutte le identità utente note e mantenute dall&#39;SDK Roku. |
|  | Per ulteriori informazioni consulta la sezione Analytics dell’SDK legacy. |  |
|  |  |  |
| **Experience Cloud** |  |  |
|  | `visitorSyncIdentifiers` | API di SceneGraph per sincronizzare gli identificatori di Experience Cloud sull’SDK di ADBMobile. |
|  | `visitorMarketingCloudID` | API di SceneGraph per ottenere l&#39;ID Experience Cloud del visitatore dall&#39;SDK di ADBMobile. |
|  | Per ulteriori informazioni consulta la sezione Experience Cloud dell’SDK legacy. |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | API di SceneGraph per inviare un segnale di gestione dell&#39;audience con caratteristiche. |
|  | `audienceVisitorProfile` | API di SceneGraph per ottenere un profilo visitatore di audience manager dall’SDK di ADBMobile. |
|  | `audienceDpid` | API di SceneGraph per ottenere un Dpid di pubblico dall’SDK di ADBMobile. |
|  | `audienceDpuuid` | API di SceneGraph per ottenere un pubblico Dpuuid dall&#39;SDK di ADBMobile. |
|  | `audienceSetDpidAndDpuuid` | API di SceneGraph per impostare audience Dpid e Dpuuid sull&#39;SDK di ADBMobile. |
|  | Per ulteriori informazioni consulta la sezione Audience Manager dell’SDK legacy. |  |
|  |  |  |
| **MediaHeartbeat** |  |  |
|  | `mediaTrackLoad` | API di SceneGraph per caricare contenuti video per il tracciamento MediaHeartbeat. |
|  | mediaTrackStart | API di SceneGraph per avviare la sessione di tracciamento video utilizzando MediaHeartbeat. |
|  | `mediaTrackUnload` | API di SceneGraph per scaricare contenuti video dal tracciamento MediaHeartbeat. |
|  | `mediaTrackPlay` | API di SceneGraph per tenere traccia della riproduzione di contenuto video. |
|  | mediaTrackPause | API di SceneGraph per tenere traccia del contenuto video in pausa. |
|  | `mediaTrackComplete` | API di SceneGraph per tenere traccia della riproduzione completata per il contenuto video. |
|  | `mediaTrackError` | API di SceneGraph per tenere traccia degli errori di riproduzione. |
|  | mediaTrackEvent | API di SceneGraph per tenere traccia degli eventi di riproduzione durante il tracciamento. Ad esempio: Annunci, capitoli. |
|  | `mediaUpdatePlayhead` | API di SceneGraph per inviare aggiornamenti di playhead a MediaHeartbeat durante il tracciamento video. |
|  | `mediaUpdateQoS` | API di SceneGraph per inviare aggiornamenti QoS a MediaHeartbeat durante il tracciamento video. |
|  | Per ulteriori informazioni consulta la sezione MediaHeartbeat dell’SDK legacy. |  |

### SceneGraphConstants

| Nome costante | Descrizione |
|---|---|
| `API_RESPONSE` | Utilizzato per recuperare l&#39;oggetto di risposta dal campo `adbmobileTask` del nodo `adbmobileApiResponse` |
| `DEBUG_LOGGING` | Utilizzato come `apiName` per `getDebugLogging` |
| `PRIVACY_STATUS` | Utilizzato come `apiName` per `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Utilizzato come `apiName` per `trackingIdentifier` |
| `USER_IDENTIFIER` | Utilizzato come `apiName` per `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Utilizzato come `apiName` per `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Utilizzato come `apiName` per `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Utilizzato come `apiName` per `audienceDpid` |
| `AUDIENCE_DPUUID` | Utilizzato come `apiName` per `audienceDpuuid` |

### Nodo adbmobileTask

<table>
<thead>
<tr>
<td> Campo </td><td> Tipo </td><td> impostazione predefinita </td><td> Utilizzo </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assocarray </td>
<td> Non valido </td>
<td> NON modificare questo campo o lasciare che sia utilizzato dall'applicazione. Questo campo viene utilizzato da ADBMobile SceneGraphConnector per indirizzare le chiamate API tramite i nodi SceneGraph e per recuperare le risposte. Pertanto, questa chiave/campo è riservata ad AdobeMobileSDK per la compatibilità con SceneGraph. <b>Importante:</b> eventuali modifiche a questo campo possono causare il malfunzionamento di AdobeMobileSDK.</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> Non valido </td>
<td> Tutte le API eseguite su AdobeMobileSDK restituiranno risposte in questo campo di sola lettura. Registrati per un callback per ascoltare gli aggiornamenti a questo campo per ricevere gli oggetti di risposta. Di seguito è riportato il formato dell'oggetto di risposta:  
<pre>
response = {
  "apiName" : &lt;SceneGraphConstants.
               API_NAME&gt; 
  "returnValue : &lt;API_RESPONSE&gt; 
}</pre>
Un'istanza di questo oggetto di risposta verrà inviata per qualsiasi chiamata API su AdobeMobileSDK che dovrebbe restituire un valore come indicato nella guida di riferimento API. Ad esempio, una chiamata API per visitorMarketingCloudID() restituirà il seguente oggetto di risposta: 
<pre>
response = {
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : "07050x25671x33760x72644x14"  
} 
</pre>
OR, anche i dati di risposta possono non essere validi: 
<pre>
response = {  
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : non valido 
} 
</pre>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

Firma API: `ADBMobile().getADBMobileConnectorInstance()`\
Ingresso: `adbmobileTask`
Tipo di ritorno: `ADBMobileConnector`

#### `sgConstants`

Firma API: `ADBMobile().sgConstants()`
Ingresso: Nessuno\
Tipo di ritorno: `SceneGraphConstants`

>[!NOTE]
>Per ulteriori informazioni, consulta il riferimento API `ADBMobileConnector` .

### Costanti ADBMobile

|  Funzione  | Nome costante | Descrizione   |
|---|---|---|
| Controllo delle versioni | `version` | Costante per il recupero delle informazioni sulla versione di AdobeMobileLibrary |
| Privacy/rinuncia | `PRIVACY_STATUS_OPT_IN` | Costante per lo stato di privacy optata in |
|  | `PRIVACY_STATUS_OPT_OUT` | Costante per lo stato di privacy rifiutata |
| Costanti MediaHeartbeat | Fai riferimento alle costanti di questa pagina: <br/><br/>[Metodi Media Heartbeat.](/help/sdk-implement/track-av-playback/track-core/track-core-roku.md) | Utilizza queste costanti con le API MediaHeartbeat |
| Metadati standard | Fai riferimento alle costanti di questa pagina: <br/><br/>[Parametri metadati standard.](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Utilizza queste costanti per allegare metadati video/annunci standard nelle API MediaHeartbeat |

Le API definite a livello globale `MediaHeartbeat` della libreria AdobeMobile legacy sono accessibili *così come* nell&#39;ambiente SceneGraph in quanto non utilizzano componenti BrightScript non disponibili nei nodi SceneGraph. Per ulteriori informazioni su questi metodi, consulta la tabella seguente:

### Metodi globali per MediaHeartbeat

| Metodo | Descrizione |
| --- | --- |
| `adb_media_init_mediainfo` | Questo metodo restituisce un oggetto Media Information inizializzato `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | Questo metodo restituisce l&#39;oggetto Ad Information inizializzato `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | Questo metodo restituisce l&#39;oggetto informazioni capitolo inizializzato.  `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | Questo metodo restituisce l&#39;oggetto AdBreak Information inizializzato.  `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | Questo metodo restituisce un oggetto QoS Information inizializzato.  `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementazione {#implementation}

1. **Scarica la libreria Roku -** Scarica la libreria Roku  [più recente.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)

1. **Configurare l&#39;ambiente di sviluppo**

   1. Copia `adbmobile.brs` (AdobeMobileLibrary) nella directory `pkg:/source/`.

   1. Per il supporto di Scene Graph, copia `adbmobileTask.brs` e `adbMobileTask.xml` nella directory `pkg:/components/`.

1. **Inizializza**

   1. Importa `adbmobile.brs` nella tua scena.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Crea un&#39;istanza del nodo `adbmobileTask` nella tua Scene.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Ottieni un&#39;istanza del connettore `adbmobile` per SceneGraph utilizzando l&#39;istanza `adbmobileTask` .

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Ottieni `adbmobile` costanti SG.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Registra un callback per ricevere l&#39;oggetto risposta per tutte le chiamate API `AdbMobile`.

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
