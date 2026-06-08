---
title: Tracciare gli annunci
description: Panoramica dell’implementazione del tracciamento degli annunci con Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# Tracciare gli annunci

Il tracciamento della riproduzione degli annunci copre le interruzioni, gli avvii, i completamenti e i salti degli annunci. Utilizza l’API del lettore multimediale per identificare gli eventi chiave del lettore e popolare le variabili annuncio richieste.

## Eventi del lettore

| Evento lettore | Azione |
| --- | --- |
| Avvio dell’interruzione pubblicitaria | Crea un oggetto di interruzione pubblicitaria; chiama AdBreakStart |
| Inizio annuncio | Crea un oggetto annuncio; chiama AdStart |
| Annuncio completato | Chiama AdComplete |
| Salta annuncio | Chiama AdSkip |
| Interruzione annuncio completata | Chiama AdBreakComplete |

## Passaggi di implementazione

1. Identifica quando inizia il limite dell’interruzione dell’annuncio, incluso il pre-roll, e crea un oggetto di interruzione pubblicitaria. Per le definizioni dei campi, vedere [Nome interruzione annuncio](/help/implementation/variables/ads/ad-break-name.md) e [Ora inizio interruzione annuncio](/help/implementation/variables/ads/ad-break-start-time.md).
1. Chiama [Inizio interruzione annuncio](/help/implementation/events/ads/ad-break-start.md) per iniziare a tenere traccia dell&#39;interruzione annuncio.
1. Identifica quando inizia l’annuncio e crea un oggetto annuncio. Per le definizioni dei campi, vedi [Nome annuncio](/help/implementation/variables/ads/ad-name.md), [ID annuncio](/help/implementation/variables/ads/ad-id.md), [Lunghezza annuncio](/help/implementation/variables/ads/ad-length.md), [Posizione annuncio nel pod](/help/implementation/variables/ads/ad-in-pod-position.md) e [Nome annuncio lettore](/help/implementation/variables/ads/ad-player-name.md).
1. Facoltativamente, allega metadati standard di annunci. Consulta [Inserzionista](/help/implementation/variables/ads/advertiser.md), [ID campagna](/help/implementation/variables/ads/campaign-id.md), [ID Creative](/help/implementation/variables/ads/creative-id.md), [URL Creative](/help/implementation/variables/ads/creative-url.md), [ID posizionamento](/help/implementation/variables/ads/placement-id.md) e [ID sito](/help/implementation/variables/ads/site-id.md) per le chiavi disponibili.
1. Chiama [Inizio annuncio](/help/implementation/events/ads/ad-start.md) per iniziare a tracciare l&#39;annuncio.
1. Al termine della riproduzione dell&#39;annuncio, chiamare [Annuncio completato](/help/implementation/events/ads/ad-complete.md).
1. Se il visualizzatore ha saltato l&#39;annuncio, chiama [L&#39;annuncio salta](/help/implementation/events/ads/ad-skip.md) invece di Annuncio completato.
1. Per annunci aggiuntivi nella stessa interruzione pubblicitaria, ripeti i passaggi da 3 a 7.
1. Al termine dell&#39;interruzione pubblicitaria, chiamare [Interruzione pubblicitaria completata](/help/implementation/events/ads/ad-break-complete.md).

>[!IMPORTANT]
>
>**Annunci pre-roll: non chiamare `trackPlay` prima di `AdBreakStart` e `AdStart`.** Il primo ping `play` sugli incrementi di contenuto principale [Inizia il contenuto](/help/reporting/metrics/content-starts.md). Se `trackPlay` viene chiamato prima che gli eventi dell&#39;annuncio pre-roll si attivino e il visualizzatore si abbandona durante l&#39;annuncio, il contenuto inizia a essere incrementato anche se non è mai stato riprodotto alcun contenuto principale. Per gli scenari pre-roll, ritardare `trackPlay` fino a dopo l&#39;invio di `AdBreakStart` e `AdStart`.

>[!NOTE]
>
>Il valore della testina di riproduzione segnalato durante la riproduzione dell&#39;annuncio rappresenta la posizione del visualizzatore all&#39;interno del **contenuto principale**, non all&#39;interno dell&#39;annuncio. Per un annuncio pre-roll che precede un video di 10 minuti, la testina di riproduzione è `0` in tutto l&#39;annuncio. Per un annuncio mid-roll che inizia con il segno dei 5 minuti, la testina di riproduzione rimane a `300` (secondi) per la durata dell’annuncio.

## Problemi comuni

### Chiamate principali:play impreviste tra annunci

Se si verificano `main:play` chiamate tra annunci consecutivi, esiste un intervallo di oltre 250 millisecondi tra la chiamata AdComplete e la chiamata AdStart successiva. Quando si verifica questo gap, Media SDK si basa sull’invio di ping del contenuto principale, che possono impostare la metrica di inizio contenuto in anticipo per gli scenari pre-roll.

**Causa:** Media SDK non ha impostato informazioni sugli annunci e il lettore è in uno stato di riproduzione, pertanto attribuisce la durata del gap al contenuto principale.

**Risoluzione:** ritarda la chiamata AdComplete per ogni annuncio (tranne l&#39;ultimo) anziché chiamarla immediatamente al termine dell&#39;annuncio. Eseguire il batch delle chiamate come segue:

* A ogni **inizio annuncio**: se esiste un annuncio precedente che non è stato ancora contrassegnato come completato, chiamare AdComplete *prima* chiamando AdStart per il nuovo annuncio.
* A ogni **fine risorsa annuncio**: non chiamare AdComplete immediatamente; rinvialo.
* All&#39;**interruzione annuncio completata**: chiama AdComplete per l&#39;ultimo annuncio (se non già chiamato), quindi chiama AdBreakComplete.

Questo modello assicura che AdComplete e il successivo AdStart vengano attivati in modalità back-to-back, eliminando così qualsiasi lacuna.
