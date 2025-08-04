---
title: Migrare un’implementazione del connettore di origine Analytics ai campi XDM Streaming Media aggiornati
description: Scopri come migrare un’implementazione del connettore di origine Analytics ai campi XDM Streaming Media aggiornati
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a0a357c3fe7e958b0b6491c84f17f26a806ea205
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Aggiornamento dell’implementazione di un connettore di origine Analytics ai nuovi campi XDM per Streaming Media

>[!NOTE]
>
>Queste informazioni sono destinate alle organizzazioni che utilizzano il [connettore di origine di Analytics](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/analytics) per inserire in Adobe Experience Platform i dati di Streaming Media provenienti da Adobe Analytics e utilizzarli con il reporting di Customer Journey Analytics o con qualsiasi altro servizio Platform.
>
>Le modifiche non influiscono su Adobe Analytics come applicazione autonoma, incluse la raccolta, l’elaborazione e il reporting di dati. Strumenti come Feed dati e Regole di elaborazione rimangono invariati, pertanto non sono necessari aggiornamenti all’implementazione di Analytics.

È ora disponibile una nuova implementazione di Raccolta dati di Adobe (connettore di origine di Analytics) per il servizio Streaming Media che esegue la migrazione da un set di campi XDM a un altro.

## Nuovo percorso campo XDM

Come parte di questa migrazione, il percorso del campo XDM `mediaReporting` è stato aggiunto agli schemi XDM utilizzati nei flussi di raccolta dati di Adobe (connettore di origine di Analytics). Qualsiasi schema di raccolta dati Adobe esistente o appena generato includerà automaticamente questo nuovo campo.

## Sostituzione del percorso del campo XDM precedente

Tutti i flussi di raccolta dati di Adobe (connettore di origine di Analytics) che trasferiscono dati di Streaming Media da Adobe Analytics a Adobe Experience Platform stanno attualmente inviando dati sia sul nuovo percorso del campo XDM `mediaReporting` che sul vecchio percorso del campo XDM `media.mediaTimed`. Entrambi questi percorsi saranno disponibili per tre mesi, fino alla fine di ottobre 2025. Dopo ottobre, i campi `media.mediaTimed` diventeranno completamente obsoleti e i dati acquisiti dopo ottobre includeranno solo `mediaReporting`. Dopo l&#39;eliminazione, i campi `media.mediaTimed` non saranno più visibili nell&#39;interfaccia utente dello schema di Adobe Experience Platform e l&#39;acquisizione dei dati in questi campi verrà interrotta. Di conseguenza, questi campi non saranno più disponibili per l’utilizzo in alcun servizio Adobe Experience Platform.

I dati acquisiti prima di tale data rimarranno disponibili per il reporting.

## Differenze aggiuntive con il nuovo percorso campo XDM

Con la nuova implementazione del connettore di origine Adobe per Streaming Media, le chiamate keep-alive da Adobe Analytics vengono ora acquisite in Adobe Experience Platform.

In precedenza, queste chiamate non si riflettevano nelle app Platform, come Customer Journey Analytics. Di conseguenza, l’organizzazione potrebbe osservare le seguenti differenze nei rapporti:

* **Conteggi accurati delle sessioni**: in alcuni casi, ciò potrebbe significare una deflazione nei conteggi delle sessioni, perché le chiamate keep-alive consentono di mantenere le sessioni attive degli utenti anche in assenza di interazioni multimediali dirette. Queste chiamate keep-alive vengono generate ogni 20 minuti dopo l’ultimo evento, per riproduzione multimediale, con l’intento di mantenere aperta la visita. Per garantire il tracciamento ottimale delle sessioni in Customer Journey Analytics, si consiglia di configurare la scadenza della visita in 30 minuti nella visualizzazione dati.

* **Aumento del numero di eventi**: perché le chiamate keep-alive vengono ora conteggiate nella metrica Eventi di Customer Journey Analytics. Se desideri escludere le chiamate keep-alive dal reporting, puoi creare un filtro che escluda gli eventi il cui Tipo evento è `media.keepalive`.

Questa modifica garantisce un maggiore allineamento tra i rapporti di Analytics e di CJA.

## Migrare la configurazione esistente

Per garantire una transizione senza problemi, tutti i clienti devono migrare le impostazioni esistenti dai campi `media.mediaTimed` ai campi `mediaReporting` prima della fine di ottobre 2025. Le aree interessate sono quelle che si basano sull&#39;utilizzo di `media.mediaTimed` e devono essere migrate come descritto nelle sezioni seguenti.

### Customer Journey Analytics**

È possibile migrare i rapporti di CJA in due modi:

>[!NOTE]
>
>Dopo aver scelto una delle opzioni seguenti, è necessario sostituire manualmente ogni campo `media.mediaTimed` utilizzato nei report di Customer Journey Analytics con il relativo campo derivato corrispondente o il Percorso campo XDM per reporting.

* **Per conservare i dati storici**: i team di Adobe hanno sviluppato un modello Customer Journey Analytics predefinito che introduce un set di campi derivati che combinano i vecchi e i nuovi campi XDM in un unico campo. Questo modello può essere abilitato tramite connessione Customer Journey Analytics su richiesta. Contatta il team di supporto Adobe per assistenza nell’abilitare i nuovi campi. Questi campi derivati non vengono conteggiati per il limite di campi derivati della tua organizzazione.

  Per visualizzare un elenco dei mapping, vedere [Mappatura dei parametri di Media Analytics per Adobe Experience Platform e Customer Journey Analytics](/help/use-cases/xdm-updates/parameters-mapping.md).

* **Se i dati storici non sono necessari**: è sufficiente utilizzare il percorso del campo XDM per reporting al momento della generazione del rapporto. Per ulteriori informazioni, vedere [Migrare Customer Journey Analytics per utilizzare i nuovi campi di Streaming Media](/help/use-cases/xdm-updates/migrate-cja-setup.md).

### Real-Time CDP

Tutti i tipi di pubblico e i profili devono essere basati su `mediaReporting`. Per ulteriori informazioni, consulta [Migrare i profili ai nuovi campi di Streaming Media](/help/use-cases/xdm-updates/migrate-profiles.md).

### Flusso di dati e raccolta dati

Configurazioni dinamiche e mappatura dati devono utilizzare `mediaReporting`. Per ulteriori informazioni, vedere [Migrare la preparazione dati per i campi personalizzati ai nuovi campi di Streaming Media](/help/use-cases/xdm-updates/migrate-dataprep.md).

### Altri servizi di cui è necessaria la migrazione

* Adobe Journey Optimizer: le configurazioni di campagna e percorso devono incorporare `mediaReporting`.

* Inoltro eventi: solo i campi `mediaReporting` devono essere inclusi nelle configurazioni.

* Servizi di query: le query devono fare riferimento a `mediaReporting` campi.

* Configurazioni tag: qualsiasi impostazione di tag deve fare riferimento a `mediaReporting` campi.

* Connessioni e destinazioni: i flussi di dati di importazione ed esportazione devono essere strutturati intorno a `mediaReporting` campi.

È interessato qualsiasi altro flusso che si basa sui campi `media.mediaTimed` e richiede aggiornamenti della logica.

## Passaggi successivi e supporto

Tutti i clienti che utilizzano Raccolta dati di Adobe per Streaming Media devono completare le migrazioni entro il periodo di transizione specificato.

Per eventuali domande o esigenze di supporto, contatta il team di supporto Adobe.

