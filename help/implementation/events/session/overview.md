---
title: Tracciare la riproduzione dei contenuti
description: Scopri come tracciare la riproduzione core, compresi il caricamento, l’avvio, la pausa e il completamento del contenuto multimediale.
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 2%

---


# Tracciare la riproduzione dei contenuti

Il tracciamento della riproduzione di base riguarda il caricamento dei contenuti multimediali, l’avvio, la pausa, la ripresa, il completamento e la fine della sessione. Sebbene non siano obbligatori, anche il buffering e il tracciamento della ricerca sono componenti core di un’implementazione completa di riproduzione.

## Eventi del lettore

| Evento lettore | Azione |
| --- | --- |
| Caricamento file multimediale | Crea oggetto multimediale; chiama SessionStart |
| Avvio file multimediale | Chiama Play |
| Pausa | Inizio pausa chiamata |
| Riprendi da pausa | Chiama Play |
| File multimediale completato | Chiama sessione completata |
| Interruzione/scaricamento contenuti multimediali | Chiama SessionEnd |
| Avvio buffering | Chiama BufferStart |
| Fine buffering | Chiama riproduzione (ripresa) |
| La ricerca inizia | Chiama SeekStart |
| Fine ricerca | Chiama SeekComplete, quindi chiama Play |

## Passaggi di implementazione

1. **Identifica quando l&#39;utente attiva la riproduzione** (l&#39;utente fa clic su play o viene attivata la riproduzione automatica). Crea un oggetto multimediale con nome del contenuto, ID, lunghezza, tipo di flusso e tipo di file multimediale. Per le definizioni dei campi, vedere [Nome contenuto](/help/implementation/variables/core/content-name.md), [ID contenuto](/help/implementation/variables/core/content-id.md), [Lunghezza contenuto](/help/implementation/variables/core/content-length.md), [Tipo flusso](/help/implementation/variables/core/stream-type.md) e [Tipo contenuto](/help/implementation/variables/core/content-type.md).
1. **Allega facoltativamente metadati** — metadati standard (spettacolo, stagione, episodio, ecc.) e variabili di dati di contesto personalizzate. Vedi [Show](/help/implementation/variables/standard-metadata/show.md), [Season](/help/implementation/variables/standard-metadata/season.md), [Episode](/help/implementation/variables/standard-metadata/episode.md), [Genre](/help/implementation/variables/standard-metadata/genre.md) e [Network](/help/implementation/variables/standard-metadata/network.md) per i riferimenti alle chiavi di metadati standard.
1. **Chiamare [Avvio sessione](/help/implementation/events/session/session-start.md)** per iniziare a tenere traccia della sessione. In questo modo vengono caricati i dati e i metadati e viene avviata la misurazione QoS del tempo di avvio. SessionStart tiene traccia dell&#39;*intento* da riprodurre, non del primo fotogramma.
1. **Chiama [Play](/help/implementation/events/playback/play.md)** quando viene eseguito il rendering del primo fotogramma del contenuto sullo schermo.
1. **Chiama [Avvia pausa](/help/implementation/events/playback/pause-start.md)** quando il lettore si interrompe. Richiama di nuovo Play quando la riproduzione riprende. Non esiste un evento di ripresa separato.
1. **Chiama [Sessione completata](/help/implementation/events/session/session-complete.md)** quando il visualizzatore raggiunge la fine del contenuto.
1. **Chiama [Fine sessione](/help/implementation/events/session/session-end.md)** quando il lettore viene scaricato o il visualizzatore abbandona il contenuto senza raggiungere la fine. SessionEnd chiude immediatamente la sessione e non è possibile tenere traccia di altri eventi successivi.

>[!IMPORTANT]
>
>`SessionEnd` indica la fine di una sessione di tracciamento. Se la sessione è stata controllata correttamente fino al completamento, chiamare `SessionComplete` prima di `SessionEnd`. Qualsiasi altra chiamata di tracciamento viene ignorata dopo `SessionEnd`, tranne `SessionStart` per una nuova sessione.

## Riproduzione core

Gli esempi seguenti mostrano un flusso di sessione completo, dall’inizio alla fine della sessione, fino al completamento del contenuto e alla fine della sessione.

Per informazioni dettagliate sull&#39;implementazione per piattaforma, vedere [Inizio sessione](/help/implementation/events/session/session-start.md), [Riproduci](/help/implementation/events/playback/play.md), [Inizio pausa](/help/implementation/events/playback/pause-start.md), [Sessione completata](/help/implementation/events/session/session-complete.md) e [Fine sessione](/help/implementation/events/session/session-end.md).

## Buffering

L&#39;avvio del buffer segnala che il lettore è in attesa di dati. La fine del buffer viene dedotta quando si invia un evento Play dopo BufferStart (API basate su XDM). Su Mobile SDK, chiama esplicitamente anche BufferComplete.

Per informazioni dettagliate sull&#39;implementazione, vedere [Avvio buffer](/help/implementation/events/playback/buffer-start.md).

## Ricerca

La ricerca segnala che il visualizzatore sta pulendo. La fine della ricerca è seguita da Play per riprendere la riproduzione del contenuto.

Per informazioni dettagliate sull&#39;implementazione, vedere [Inizio pausa](/help/implementation/events/playback/pause-start.md) (inizio ricerca) e [Riproduci](/help/implementation/events/playback/play.md) (fine ricerca).

## Gestione degli arresti dell’app

La riproduzione in un’applicazione multimediale può essere interrotta in diversi modi: l’utente preme la pausa, l’app va in background, arriva una telefonata. Indipendentemente dalla causa, le istruzioni di tracciamento sono le stesse:

1. Chiama **PauseStart** quando l&#39;applicazione viene interrotta (passa in background, il contenuto multimediale è messo in pausa, ecc.).
1. Chiama **Play** quando l&#39;applicazione torna in primo piano e/o il contenuto multimediale riprende la riproduzione.

>[!NOTE]
>
>Non chiamare SessionStart quando l&#39;app torna dal background. Quando si chiama SessionStart, la riproduzione fino a quel punto non viene conteggiata nel tempo totale di riproduzione e i marcatori di avanzamento, i segmenti e i limiti dei capitoli precedenti vengono persi.

**Quando deve terminare una sessione in pausa?** Se l&#39;applicazione non consente la riproduzione in background, chiamare immediatamente PauseStart e quindi SessionEnd dopo circa un minuto in background. L’applicazione non può continuare a inviare ping di pausa dal background e tenere aperta la sessione a tempo indefinito offre un’esperienza insoddisfacente. Se l’applicazione non supporta la riproduzione in background (app audio, app video podcast), continua a inviare ping mentre è in background.

**Riavvio dopo un lungo periodo di background:** Se l&#39;app è stata messa in background abbastanza a lungo da far scadere la sessione (inattività di 30 minuti), chiamare SessionEnd per chiudere in modo pulito qualsiasi sessione residua, quindi chiamare SessionStart per iniziare una nuova sessione quando il visualizzatore ritorna.

## Ripresa di sessioni inattive

Una sessione scade automaticamente se non vengono ricevuti eventi per 10 minuti o se non si verifica alcun movimento dell’indicatore di riproduzione per 30 minuti. Se l&#39;utente restituisce dopo la scadenza di una sessione, chiamare nuovamente SessionStart per aprire una nuova sessione.

**Ripresa tra dispositivi (handoff tra dispositivi):** Quando un visualizzatore trasferisce la riproduzione tra dispositivi (ad esempio, il cast da un telefono a un televisore), utilizza il flag di ripresa per unire le sessioni nel reporting di Analytics:

1. Nel **dispositivo di origine**, chiamare SessionEnd quando il visualizzatore avvia il cast. Non chiamare SessionComplete: il contenuto non è terminato.
1. Nel **dispositivo di destinazione**, chiamare SessionStart con il flag di ripresa impostato su `true` e trasmettere gli stessi metadati di contenuto e la posizione della testina di riproduzione dal dispositivo di origine.

Se si imposta il flag di ripresa, Analytics incrementa [I contenuti riprendono](/help/reporting/metrics/content-resumes.md) invece di [Avvii file multimediali](/help/reporting/metrics/media-starts.md) per la seconda parte del passaggio.

**Ripresa manuale di una sessione precedentemente chiusa:** Se l&#39;applicazione memorizza i dati utente e può riprendere una sessione precedentemente chiusa, impostare il flag di ripresa all&#39;avvio della sessione. Consulta [Inizio sessione](/help/implementation/events/session/session-start.md#resuming-a-session) per informazioni dettagliate sull&#39;implementazione per tutte le piattaforme.
