---
seo-title: Convalida delle richieste degli eventi
title: Convalida delle richieste degli eventi
uuid: 1 fc 92 f 21-b 510-4 c 96-8 ea 2-47 e 819 f 4 a 96 e
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Validating event requests{#validating-event-requests}

Il corpo della richiesta JSON per ogni tipo di evento viene convalidato sul backend con gli schemi JSON. Il corpo della risposta HTTP viene compilato con un messaggio di errore quando la convalida non riesce per una chiamata API.

JSON validation schemas for each event type are publicly accessible here: `{uri}/api/v1/schemas/{eventType}` (e.g., `{uri}/api/v1/schemas/sessionEnd`). Questi schemi di convalida JSON sono l'autorità assoluta per determinare i parametri del corpo della richiesta corretti per ogni tipo di evento.

For example, the response to a request for the `sessionStart` validation schema appears something like this sample (slightly formatted for readability here):

```
HTTP/1.1 200 OK
Server: nginx/1.13.5
Date: Thu, 18 Jan 2018 15:44:50 GMT
Content-Type: application/json
Content-Length: 2716
Connection: keep-alive

{
  "$schema":"https://json-schema.org/draft-04/schema#",
  "id":"https://alpha.hb-api.omtrdc.net/api/v1/schemas/sessionStart",
  "definitions":
  {
    "playerTime":
    {
      "type":"object","properties":
      {
        "playhead":
        {"type":"number"},
        "ts":
        {"type":"integer"}
      },
      "required":["playhead","ts"],
      "additionalProperties":false
    },
    "eventType":
    {
      "type":"string",
      "enum":[
        "sessionStart",
        "play",
        "ping",
        "bufferStart",
        "pauseStart",
        "sessionComplete",
        "bitrateChange",
        "error",
        "adBreakStart",
        "adBreakComplete",
        "adStart",
        "adComplete",
        "adSkip",
        "sessionEnd"
      ]
    },
    "qoeData":
    {
      "type":"object","properties":
      {
        "media.qoe.bitrate":
        {"type":"integer"},
        "media.qoe.droppedFrames":
        {"type":"integer"},
        "media.qoe.framesPerSecond":
        {"type":"integer"},
        "media.qoe.timeToStart":
        {"type":"integer"}
      },
      "required":[],
      "additionalProperties":false
    },
    "customMetadata":
    {
      "type":"object",
      "patternProperties":
      {
        "^[a-zA-Z0-9_\\.]+$":
        {"type":"string"}
      },
      "additionalProperties":false
    },
    "sessionStart":
    {
      "properties":
      {
        "eventType":
        {"type":"string","enum":["sessionStart"]},
        "playerTime":
        {"$ref":"#/definitions/playerTime"},
        "params":
        {"type":"object",
          "properties":
          {
            "appInstallationId":
            {"type":"string"},
            "analytics.trackingServer":
            {"type":"string"},
            "analytics.reportSuite":
            {"type":"string"},
            <...>
            "visitor.marketingCloudOrgId"],
            "additionalProperties":false
          },
          "customMetadata":
          {"$ref":"#/definitions/customMetadata"},
          "qoeData":
          {"$ref":"#/definitions/qoeData"}
        },
        "required":["eventType","playerTime","params"],
        "additionalProperties":false
      }
    },
    "type":"object","$ref":"#/definitions/sessionStart"
  }
}
```

>[!NOTE]
>
>La convalida a livello di sessione non è possibile, poiché il contesto della sessione non è disponibile nel livello della raccolta.

