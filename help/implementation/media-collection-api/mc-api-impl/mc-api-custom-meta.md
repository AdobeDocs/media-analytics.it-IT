---
title: 'Supporto per metadati personalizzati '
description: Scopri come fornire coppie chiave:valore personalizzate negli eventi sessionStart, chapterStart e adStart.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 62%

---

# Supporto per metadati personalizzati {#custom-metadata-support}

È possibile fornire coppie chiave:value personalizzate negli eventi `sessionStart`, `chapterStart` e `adStart`. Queste informazioni devono essere fornite nella chiave JSON, `customMetadata`, posizionata accanto alla chiave `params`.

La chiave JSON `customMetadata` deve contenere un oggetto di coppie chiave:value. La chiave deve contenere solo caratteri alfanumerici, sottolineatura e punto/punto.

[Eventi API della raccolta MA](../mc-api-ref/mc-api-events-req.md)

## Esempio

Attualmente puoi inviare un evento `sessionStart` con la seguente coppia chiave:value:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Per la configurazione precedente, i dati di reporting inviati ad analytics sono i seguenti:

`c.a.media.channel=channel-2`

### Consiglio

È consigliabile utilizzare uno spazio dei nomi separato per i metadati personalizzati. Ad esempio:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

Nell’esempio consigliato, i dati di reporting per i metadati personalizzati inviati ad analytics sono i seguenti:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
