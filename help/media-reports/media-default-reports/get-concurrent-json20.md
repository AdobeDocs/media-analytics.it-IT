---
title: Ottenere dati del rapporto JSON per visualizzatori simultanei con le API di Analytics 2.0
description: null
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
translation-type: tm+mt
source-git-commit: 687ae6f2037590b58b30ea776635898c93ca144f
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 5%

---


# Ottenere dati del rapporto JSON per visualizzatori simultanei con le API di Analytics 2.0{#get-concurrent-viewers-json-report-data}

È possibile ottenere i dati dei rapporti dei visualizzatori simultanei utilizzando [_*API di Analytics 2.0*_](https://www.adobe.io/apis/experiencecloud/analytics/docs.html).

1. Filtrare i dati utilizzando qualsiasi segmento creato sull&#39;interfaccia utente. Per filtrare in base a un ID contenuto specifico, create un nuovo segmento.
1. Impostate la variabile `elements` -> `id` nell&#39;organismo della richiesta a `metrics/concurrent_viewers_visitors`.
1. Richiedete una quantità sufficiente di dati.

   * L&#39;intervallo di dati specificato nel rapporto raccoglie tutti i dati dei visualizzatori simultanei _al termine della sessione video._
È necessario tenere conto delle sessioni che iniziano in un giorno e terminano dopo la mezzanotte, che è il giorno successivo.

   * Richiedi un altro giorno di dati per il periodo previsto nella tua richiesta, ma nella tua analisi _*utilizzare solo i dati previsti.*_

Un payload di richiesta di esempio per un giorno di dati sarà simile al seguente esempio. La richiesta viene eseguita per 2 giorni consecutivi, ma nel reporting si utilizza solo il primo giorno.

## Richiesta di esempio

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2020-09-02T00:00/2020-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/concurrent_viewers_visitors"
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
         "value":"00:00 2020-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2020-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2020-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2020-09-02",
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
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/report-suites-admin.html)

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

   The concurrent viewers report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->
