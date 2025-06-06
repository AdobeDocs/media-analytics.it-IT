---
title: Acquisire i dati del rapporto JSON sul tempo di riproduzione multimediale impiegato con le API di Analytics 2.0
description: Scopri come ottenere i dati del rapporto sul tempo di riproduzione dei contenuti multimediali impiegato utilizzando le API di Analytics 2.0. Visualizza una richiesta e una risposta di esempio.
feature: Media Analytics, Reports & Analytics Basics
role: User, Admin, Data Engineer
exl-id: 65e5b67a-26fc-433e-b99b-0ebbc24428ac
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 100%

---

# Acquisire i dati del rapporto JSON sul tempo di riproduzione multimediale impiegato con le API di Analytics 2.0 {#get-media-playback-time-spent-json-report-data}

È possibile ottenere i dati del rapporto sul tempo di riproduzione dei file multimediali utilizzando le [_*API di Analytics 2.0*_](https://www.adobe.io/apis/experiencecloud/analytics/docs.html).

1. Filtra i dati utilizzando qualsiasi segmento generato nell’interfaccia utente. Per filtrare secondo un ID di contenuto specifico, crea un nuovo segmento.
1. Imposta `elements` -> `id` nel corpo della richiesta a `metrics/playback_time_spent_seconds` oppure a `metrics/playback_time_spent_minutes` a seconda che si desideri ottenere l&#39;output in secondi o minuti.
1. Richiedi una quantità sufficiente di dati.

   * L’intervallo di dati specificato nel rapporto raccoglie tutti i dati del visualizzatore simultaneo _al termine della sessione video._
Devi tenere conto delle sessioni che iniziano in un giorno e terminano dopo la mezzanotte, cioè il giorno successivo.

   * Richiedi dati per un’altra giornata secondo il periodo previsto nella tua richiesta, ma nella tua analisi _*utilizza solo i dati previsti.*_

Un payload di richiesta per i dati di una giornata sarà simile al seguente esempio. La richiesta viene effettuata per 2 giorni consecutivi, ma nel reporting utilizzerai solo il primo giorno.

## Richiesta di esempio

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2021-09-02T00:00/2021-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/playback_time_spent_minutes"
            }
        ]
    },
    "settings": {
        "dimensionSort": "asc",
        "limit": "2000",
        "page": 0
  }
}
```

## Risposta di esempio

```JSON
{
   "totalPages":1,
   "firstPage":true,
   "lastPage":true,
   "numberOfElements":1440,
   "number":0,
   "totalElements":1440,
   "columns":{
      "dimension":{
         "id":"variables/daterangeminute",
         "type":"time"
      },
      "columnIds":[
         "column1"
      ]
   },
   "rows":[
      {
         "itemId":"12008020000",
         "value":"00:00 2021-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2021-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2021-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2021-09-02",
         "data":[
            768.0
         ]
      }
   ],
   "summaryData":{
      "filteredTotals":[
         17124.0
      ],
      "totals":[
         18453.0
      ]
   }
}
```


<!--
You can extract the Media Playback Time Spent report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html?lang=it)

        * `dateTo` - End date of the report.         

          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`

        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }

      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The Media Playback Time Spent report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->
