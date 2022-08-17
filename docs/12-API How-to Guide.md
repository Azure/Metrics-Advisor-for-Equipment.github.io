# ⭐API How-to Guide

Azure Metrics Advisor for Equipment is a cloud-based [Azure Applied AI Service](https://docs.microsoft.com/en-us/azure/applied-ai-services/) that uses machine-learning models to scale predictive maintenance and proactively monitor the health of your physical assets. 

## Get started: Metrics Advisor for Equipment (Project Adel) REST API 2022-07-10-preview
>**_NOTE:_**
> Metrics Advisor for Equipment (Project Adel) is currently in private preview. Some features may not be supported or have limited capabilities.
The current API version is **2022-07-10-preview**.


In the following sections you will :
  1. [(Prerequisites) Create a Metrics Advisor resource in the Azure portal.](#1-prerequisites-create-a-metrics-advisor-resource-in-the-azure-portal)
  1. [Prepare data and create a dataset.](#2-prepare-data-and-create-a-dataset)
  1. [Train a Metrics Advisor for Equipment model.](#3-train-a-model)
  1. [Check model status training status.](#4-check-model-training-status)
  1. [Evaluate the model performance and download the evaluation results.](#5-evaluate-model-performance)
  1. [Post-process evaluation results and determine the desired alert settings.](#6-post-process-evaluation-results-and-determine-the-desired-alert-settings)
  1. [Configure and start an inference schedule.](#7-configure-and-start-an-inference-schedule)
  1. [Get streaming inference results and diagnose alerts.](#8-get-streaming-inference-results-and-diagnose-alerts)
  1. [Trigger a replay on an existing inference schedule to backfill/refresh detection results for a historical time period.](#9-trigger-a-replay-on-an-existing-inference-schedule)



## 1. (Prerequisites) Create a Metrics Advisor resource in the Azure portal
Here are three quick steps you need to take before using the Azure Metrics Advisor for Equipment fuctionalities: 
- [Find Metrics Advisor service on the Azure portal.](#find-metrics-advisor-service-on-the-azure-portal)
- [Create a Metrics Advisor resource.](#create-a-resource)
- [Get your endpoint URL and keys.](#get-endpoint-url-and-keys)

Let's get started:

### Find Metrics Advisor service on the Azure portal

The Azure portal is a single platform you can use to create and manage Azure services.

Follow the below instructions to find Metrics Advisor service on the Azure portal:

1. Navigate to the Azure portal home page: [Azure home page](https://portal.azure.com/#home).

1. Select **Create a resource** from the Azure home page.

1. Search for and choose **Metrics Advisor** from the search bar.

1. Select the **Create** button.

![Find Metrics Advisor service on the Azure portal](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/Visit_Azure_Portal_h.jpg "Find Metrics Advisor service on the Azure portal.")


### Create a resource

> **_NOTE:_**
> During private preview stage, Metrics Advisor for Equipment is only available in **West Europe, East Europe, and UK South**. Please make sure your subscription and resources are created in one of the available regions.

1. Next, you're going to fill out the **Create Metrics Advisor** fields with the following values:

    * **Subscription**. Select your current subscription. If you don't have one yet, you can [create an Azure subscription for free](https://azure.microsoft.com/free/cognitive-services).
    * **Resource group**. The [Azure resource group](/azure/cloud-adoption-framework/govern/resource-consistency/resource-access-management#what-is-an-azure-resource-group) that will contain your resource. You can create a new group or add it to a pre-existing group.
    * **Region**. Select *West Europe, East Europe, or UK South*.
    * **Name**. Enter a name for your resource. We recommend using a descriptive name, for example *YourNameMetricsAdvisor*.
    * **Pricing tier**. S0 is the only available pricing tier for now.
    * **Bring your own storage**. Choose Yes only if you need to store metrics data and detection results into your own Azure Database for PostgreSQL.

1. Confirm and select **Review + Create**.

1. Azure will run a quick validation check, after a few seconds you should see a green banner that says **Validation Passed**.

1. Once the validation banner appears, select the **Create** button from the bottom-left corner.

1. After you select **Create**, you'll be redirected to a new page that says **Deployment in progress**. The deployment could take up to 60 minutes to complete, although it normally finishes in less than 10 minutes. 

![Create a Metrics Advisor resource](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/Create_a_resource_h.jpg "Create a Metrics Advisor resource.")

### Get endpoint URL and keys

1. Once the deployment is done, you'll see a message that says, **Your deployment is complete**. Then, select the **Go to resource** button.

1. Copy the **KEY** and **endpoint** values from your Metrics Advisor resource, paste them in a convenient location, such as *Microsoft Notepad*. You'll need the key and endpoint values to connect your application to the Metrics Advisor for Equipment API.

1. If your overview page doesn't have the keys and endpoint visible, you can select the **Keys and Endpoint** button under the **Resource Management** section on the left navigation bar and retrieve them there.

![Get your endpoint URL and keys](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/Get_endpoint_and_keys_h.jpg "Get your endpoint URL and keys.")


That's it! You're now ready to start scaling predictive maintenance using Azure Metrics Advisor for Equipment.

## 2. Prepare data and create a dataset

### 2.1 Goal for this step 
* Preprocess your data according to the schema requriements. [Learn how to preprocess your data](#/docs/02-Preprocessing%20your%20data.md)
* Add the preprocess data to a dataset on Metrics Advsior for Equipment service so that you can use it for future model training, model evaluation, and/or real-time streaming inference.

### 2.2 REST API samples
For example, if you'd like to add a dataset that contains preprocessed data that is - 
- stored in Azure SQL
- in long-form format
- with 5-min data granularity

You can call `[PUT] https://{endpoint}/datasets/{datasetName}` and enter your information following the request sample below to add a dataset.

**Sample Request**

```json
{
  "parameters": {
    "endpoint": "{endpoint}", // Your Metrics Advisor resource endpoint URL  
    "apiVersion": "2022-07-10-preview",
    "Ocp-Apim-Subscription-Key": "{API key}", // Your Metrics Advisor resource key
    "Content-Type": "application/json",
    "datasetName": "prod_controlValve_5min_v1", // Unique and case-sensitive
    "body": {
      "datasetDescription": "{Optional field to add more details}",
      "dataSourceInfo": {
        "dataSourceType": "SqlServer",
        "authenticationType": "ManagedIdentity",
        "serverName": "{your_sql_server_name}", // Name of the Azure SQL server with your training, evaluation, and/or inference data
        "databaseName": "{your_database_name}", // Your Azure SQL database name (must be in the above server)
        "tableName": "{your_sql_table_name}" //Your Azure SQL table / SQL view name (must be in the above database)
      },
      "dataSchema": {
        "dataSchemaType": "LongTable",
        "timestampColumnName": "eventTimeStamp", // Replace with header of the column that contains datetime values
        "variableColumnName": "sensorName", // Replace with header of the column that contains the names of your input variables
        "valueColumnName": "sensorValue" // Replace with header of the column that contains numeric values
      },
      "dataGranularityNumber": 5,
      "dataGranularityUnit": "Minutes"
    }
  }
}
```

**Response**

You will get either a 201 or 200 reponse if the request was successful.


### 2.3 Parameter details 

**Request headers**

`Ocp-Apim-Subscription-Key`: Your Metrics Advisor resource key. This subscription key provides you access to this API.

`Content-Type`: Media type of the body sent to the API.

**URI parameter**

`datasetName`: Unique identifier of a dataset. _Cannot be changed once a dataset has been created._
  - Type: string
  - Case-sensitive: Yes
  - Character length: [1, 200]
  - Valid characters: A-Z, a-z, 0-9, _(underscore), and -(hyphen). Name starts with an _(underscore) or -(hyphen) will not be accepted.

**Query parameter**

**Required**

`apiVersion`: The current API version is **2022-07-10-preview**.


**Request body parameters**

The request accepts the following data in JSON format.

| **Parameters** | **Description** | **Type** | **Pattern** |
| :----------- | :----------- | :----------- | :----------- |
| `datasetDescription` | _Optional._ Provide more information about this dataset. | string | Character length: [0, 1024]
| `dataGranularityNumber` | _Required._ (Together with dataGranularityUnit) The frequency interval at which new records are added to your data.  | int32 | |
| `dataGranularityUnit` | _Required._ (Together with dataGranularityNumber) The unit of your data frequency interval. | string | Valid values: Minutes, Hours, Days, Weeks, Months, Years. |
| **dataSourceInfo** | 
| `dataSourceType` | _Required._ Type of your data scource. | string | Valid value: `SqlServer` |
| `authenticationType` | _Required._ Method to authenticate Metrics Advisor for Equipment to access your data source. | string | Valid value: `ManagedIdentity` | 
| `serverName` | _Required if dataSourceType = SqlServer._ Name of a SQL Server. | string | Case-sensitive: No|
| `databaseName` | _Required if dataSourceType = SqlServer._ Name of a SQL Database. | string | Case-sensitive: Yes|
| `tableName` | _Required if dataSourceType = SqlServer._ Name of a SQL table or SQL view. | string | Case-sensitive: Yes| 
|**dataSchema**| | 
| `dataSchemaType` | _Required._ Indicates how your data is formatted. <ul><li>`LongTable`: A long-form data table has a single column that stores all the variables</li><li>`WideTable`: A wide-form data table spreads variables across several columns</li></ul> | string | Valid value: "LongTable" | 
| `timestampColumnName` | _Required._ Header of the column that contains datetime values | string | Case-sensitive: Yes|
| `variableColumnName` | _Required if dataSchemaType = LongTable._ Header of the column that contains the the names of your input variables | string | Case-sensitive: Yes|
| `valueColumnName` | _Required if dataSchemaType = LongTable._ Header of the column that contains numeric values | string | Case-sensitive: Yes|


### 2.4 FAQ and best practices 

**Q: How do I find my SQL server name?**

A: In cases where you are not able to get an answer from your data engineering team, you can follow the below steps to locate your SQL server with a known database name. 
  ![Get_SQLServer_Name](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/Get_SQLServer_Name.png "Get_SQLServer_Name")

If you do not have an Azure SQL database yet, [create a single database](https://docs.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal).

**Q: What are the key things I should keep in mind when preparing my data?**

A: Here are three key things you should keep in mind: 
- Make sure that each variable has _at most_ one data point within each interval.
- Only *numerical* data is acceptable for Multivariate Anomaly Detector, but if there's categorical data in your dataset, we recommend you transform them into numerical values.  
  - For instance, the “on” and “off” of equipment status could be transformed into “0” and “1”, which could help the model learn better about the correlations between different signals.
- (Optional) Some of our users have developed more advanced ways to generate features to achieve the best possible outcome. These advanced methods are highly dependent on your business context and may require rounds of experimentation to identify the optimal feature set. To learn more, check out this [best pracice blog](#https://techcommunity.microsoft.com/t5/ai-cognitive-services-blog/4-sets-of-best-practices-to-use-multivariate-anomaly-detector/ba-p/3490848). 

**Q: How to align my data to a single data granularity?** 

A: Timestamps should be properly aligned for all your variables through aggregation or re-indexing. For example, your sensors record readings every minute but may not always at the exact same second, then you should align them to the same minute (see below). 
![Align data](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/Align_data.png "Align data to the granularity you specified.")

In cases where your sensors’ readings come at different frequencies, some users prefer to convert time series data with different frequencies into the same frequency. 

- For example, if some of your sensors record data every 5 minutes and others record every 10 minutes, then you can aggregate all data to 10-min intervals by taking the sum/mean/min/max etc. over a 10-min span for sensors that originally have 5-min frequency. 
- Alternatively, Metrics Advisor for Equipment will also help you fill in the missing data points when joining variables with different granularity, you could specify the fill-in method including linear, previous, subsequent, zero, or a fixed number at the [Train a model](#3-train-a-model) step.


**Q: What's the difference bewteen long and wide tables?**

A: 
- `LongTable`: A long-form data table has a single column that stores all the variables. Data stored in this format will have repeated values in the timestamps column.
- `WideTable`: A wide-form data table spreads variables across several columns. Data stored in this format will NOT have repeated values in the timestamps column.

![LongTable vs. WideTable](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/Long_Wide_Tables.png "Compare long-form data table and wide-form data table.")


### 2.5 Related APIs you may need
- `[GET] /datasets/{datasetName}`: **Get** dataset info including data source type, data schema, data granularity, etc.
- `[GET] /datasets[?skip][&maxpagesize][&sortBy][&orderBy]`: **List** models in a Metrics Advisor resource based on 
- `[DELETE] /datasets/{datasetName}`: **Delete** a dataset in a Metrics Advisor resource. _This action doesn't delete the data in the source system._



## 3. Train a model

### 3.1 Goal for this step 

Train a Metrics Advisor for Equipment model with the training dataset you've added. 
* For training data size, the maximum number of timestamps is 1000000, and a recommended minimum number is 15000 timestamps.

### 3.2 REST API samples
For example, if you'd like to train a model with the dataset your just added in step two above, you can call `[PUT] https://{endpoint}/multivariate/models/{modelName}` to create the model and start the model training process.

**Sample Request**

```json
{
  "parameters": {
    "endpoint": "{endpoint}", // Your Metrics Advisor resource endpoint URL  
    "apiVersion": "2022-07-10-preview",
    "Ocp-Apim-Subscription-Key": "{API key}", // Your Metrics Advisor resource key
    "Content-Type": "application/json",
    "modelName": "controlValve_5min_v1_model", // Unique and case-sensitive
    "body": {
      "modelDescription": "{Optional field to add more details}",
      "datasetName": "prod_controlValve_5min_v1",
      "trainingTimeRangeList": [
        {
          "startTime": "2022-03-17T08:00:00.000Z",
          "endTime": "2022-05-01T08:00:00.000Z"
        },
        {
          "startTime": "2022-05-02T08:00:00.000Z",
          "endTime": "2022-06-16T08:00:00.000Z"
        }
      ], // You can exclude certain time ranges for training here
      "slidingWindow": 300,
      "alignPolicy": {
        "alignMode": "Outer",
        "fillNAMethod": "Customized",
        "paddingValue": 0
      }
    }
  }
}
```

**Response**

You will get either a 201 or 200 reponse if the request was successful.


### 3.3 Parameter details 

**Request headers**

`Ocp-Apim-Subscription-Key`: Your Metrics Advisor resource key. This subscription key provides you access to this API.

`Content-Type`: Media type of the body sent to the API.

**URI parameter**

`modelName`: Unique identifier of a dataset. _Cannot be changed once a dataset has been created._
  - Type: string
  - Case-sensitive: Yes
  - Character length: [1, 200]
  - Valid characters: A-Z, a-z, 0-9, _(underscore), and -(hyphen). Name starts with an _(underscore) or -(hyphen) will not be accepted.

**Query parameter**

**Required**

`apiVersion`: The current API version is **2022-07-10-preview**.

**Request body parameters**

The request accepts the following data in JSON format.

| **Parameters** | **Description** | **Type** | **Pattern** |
| :----------- | :----------- | :----------- | :----------- |
| `modelDescription` | _Optional._ Provide more information about this model. | string | Character length: [0, 1024]|
| `datasetName` | _Required._ Data to be used for model training. | string | Case-sensitive: Yes |
| `trainingTimeRangeList` | _Required._ A list of time ranges used for model training. Both the start and end timestamps are inclusive. | string | `yyyy-MM-ddTHH:mm:ss`; conform to `ISO 8601` standard |
| `slidingWindow` | _Optional._ Controls how many previous data points get used to determine if the next data point is an anomaly. | int32 | <ul><li>Value range: [28, 2880]</li><li>Default value: 300</li></ul> |
| `alignMode` | _Optional._ How to align variables to the same data frequency interval before further processing. Inner mode returns results on timestamps where EVERY variable has a value. Outer mode returns results on timestamps where ANY variable has a value. | string | Default value: Outer |
| `fillNAMethod` | _Optional._ How to populate any missing values in the dataset. <ul><li>`Linear`: Fill `nan` values by linear interpolation.</li><li>`Previous`: Fill with the last valid value. E.g., [1, 2, nan, 3, nan, 4] -> [1, 2, 2, 3, 3, 4]</li><li>`Subsequent`: Fill with the next valid value. E.g., [1, 2, nan, 3, nan, 4] -> [1, 2, 3, 3, 4, 4]</li><li>`Customized`: Fill nan values with a specified valid value specified in `paddingValue` </li></ul>| string | Default value: Linear|
| `paddingValue` | _Optional._ Specify the value to be used for Customized fillNAMethod. **This is required if you chose Customized fillNAMethod** but optional for other methods. | float32 | |


### 3.4 FAQ and best practices 

**Q: What types of timestamps / time ranges should I exclude for model training?**

A: There are two types of data you should exclude from training to reduce noise:
- *Exclude* data when equipment/sensors are off or out-of-service.
- *Exclude* data before or after equipment/sensors restart. There usually will be irregular fluctuations right after a piece of equipment or a sensor restarts so including these data for model training may negatively impact the model’s performance.


**Q: How will `slidingWindow` be used?**

A: `slidingWindow` will also be used in streming inference and model evaluation. Let's take a look at these two scenarios separately. 

Suppose you have set `slidingWindow` = 1,440, and your input data is at one-minute granularity.

- **During streaming inference**: You want to predict whether the ONE data point at `2021-01-03T00:00:00Z `is anomalous. Your `startTime` and `endTime` will be the same value ("2021-01-03T00:00:00Z"). Your inference data source, however, must contain at least `(1,440 * 2) + 1` timestamps. Given thant 1,440 = 60 * 24, so your input data must start from at latest `2021-01-01T00:00:00Z`. 
  - Metrics Advisor for Equipment will take the leading data before the target data point ("2021-01-03T00:00:00Z") to decide whether the target is an anomaly. The length of the needed leading data is `2 * slidingWindow` or 2 * 1,440 in this case. We take twice the length ofyour sliding windown to prevent errors due to missing values in your leading data.

- **During model evaluation**: You've provided a time range for the model to inference, and thus the `endTime` will be greater than `startTime`. Inference in such scenarios is performed in a "moving window" manner. 
  - For example, Metrics Advisor for Equipment will use data from `2021-01-01T00:00:00Z` to `2021-01-02T23:59:00Z` (inclusive) to determine whether data at `2021-01-03T00:00:00Z` is an anomaly. Then it moves forward and uses data from `2021-01-01T00:01:00Z` to `2021-01-03T00:00:00Z` (inclusive) to determine whether data at `2021-01-03T00:01:00Z` is an anomaly. It moves on in the same manner (taking 2 * 1,440 data points to compare) until the last timestamp specified by `endTime` (or the actual last timestamp). 
  - Therefore, the number of timestamps in your evaluation dataset should ideally be greater than or equal to `slidingWindow` + (`endTime` - `startTime`).


**Q: How to determine the `slidingWindow` value for my model?**

A: `slidingWindow` contorls how many previous data points get used to determine if the next data point is an anomaly. For examle, if you set slidingWindow = k, then at least k+1 points should be accessible from the source file during **inference** to get valid detection results. Otherwise, you may get a "InsufficientHistoricalData" error. 

Please keep two things in mind when choosing a `slidingWindow` value:
1. **The properties of your data.** When your data is periodic, you could set the length of 1 - 3 cycles as the slidingWindow. When your data is at a high frequency (i.e., small data granularity) like minute-level or second-level, you could set a relatively higher value of slidingWindow.
1. **The trade-off between training/inference time and performance gain**. A larger slidingWindow may cause longer training/inference time. There is no guarantee that larger slidingWindows will lead to accuracy gains. A small slidingWindow may cause the model difficult to converge to an optimal solution. For example, it is hard to detect anomalies when slidingWindow has only two points.


**Q:What's the difference between Inner and Outer alignMode?**

A: `Inner` mode returns results on timestamps where EVERY variable has a value (i.e. the intersection of all variables). `Outer` mode returns results on timestamps where ANY variable has a value (i.e. the union of all variables).

Here is an example to explain different `alignModel` values:

*Variable-1*

|timestamp | value|
----------| -----|
|2020-11-01| 1  
|2020-11-02| 2  
|2020-11-04| 4  
|2020-11-05| 5

*Variable-2*

timestamp | value  
--------- | -
2020-11-01| 1  
2020-11-02| 2  
2020-11-03| 3  
2020-11-04| 4

*`Inner` join (i.e., take the intersection of the two variables)*

timestamp | Variable-1 | Variable-2
----------| - | -
2020-11-01| 1 | 1
2020-11-02| 2 | 2
2020-11-04| 4 | 4

*`Outer` join (i.e., take the union of the two variables)*

timestamp | Variable-1 | Variable-2
--------- | - | -
2020-11-01| 1 | 1
2020-11-02| 2 | 2
2020-11-03| `nan` | 3
2020-11-04| 4 | 4
2020-11-05| 5 | `nan`

**Q: Is there a limit on the number of models I can create?**

A: Yes, for detailed numebers please refer to the [Quotas and Limits](#/docs/08-Quota.md) page for the latest information. 


### 3.5 Related APIs you may need
- `[GET] /multivariate/models/{modelName}`: **Get** model info including training dataset, training time range(s), variables being used, training job status, etc.
- `[GET] /multivariate/models[?skip][&maxpagesize][&sortBy][&orderBy][&status][&datasetNames][&topPerDataset]`: **List** models in a Metrics Advisor resource. 
- `[DELETE] /multivariate/models/{modelName}`: **Delete** a model in a Metrics Advisor resource.



## 4. Check model training status

### 4.1 Goal for this step 

As the create model API is asynchronous, the model will not be ready to use immediately after you called create model API. Rather, you can query the status of models in two ways: 
- by [API key](#421-get-a-list-of-models), which will list all the models, or 
- by [model name](#422-get-a-model-by-model-name), which will list information about the specific model.

### 4.2 REST API samples

#### 4.2.1 Get a list of models 

To check the status and details of a list of models, you can call `[GET] /multivariate/models` and apply filters and/or sorting methods of your choice to this list. 

For example, if you'd like to list:
- the **top 2** models that are in **CREATED** status, and 
- were trained with **prod_controlValve_5min_v1** or **prod_controlValve_10min_v1**, and 
- arrange the output by **modelName** in **DESCENDING** order, and 
- only return one model each time

Your request URL will look like: 

`https://{endpoint}/metricsadvisor/adel/multivariate/models?api-version=2022-07-10-preview&skip=0&maxpagesize=1&sortBy=modelName&orderBy=DESCENDING&status=CREATED&datasetNames=prod_controlValve_5min_v1,prod_controlValve_10min_v1&topPerDataset=2`

Here is a sample of the **response** you would get: 

```json
// Sample response
{
  "responses": {
    "200": {
      "body": {
        "value": [
          {
            "modelName": "controlValve_5min_v1_model",
            "modelDescription": "Control valve model trained with 3-month data (excl. planned maintenance in May).",
            "datasetName": "prod_controlValve_5min_v1",
            "trainingTimeRangeList": [
              {
                "startTime": "2022-03-17T08:00:00.000Z",
                "endTime": "2022-05-01T08:00:00.000Z"
              },
              {
                "startTime": "2022-05-02T08:00:00.000Z",
                "endTime": "2022-06-16T08:00:00.000Z"
              }
            ],
            "slidingWindow": 300,
            "alignPolicy": {
              "alignMode": "Outer",
              "fillNAMethod": "Customized",
              "paddingValue": 0
            },
            "diagnosticsInfo": {
              "modelState": {
                "epochIds": [],
                "trainLosses": [],
                "validationLosses": [],
                "latenciesInSeconds": []
              },
              "variableStates": []
            },
            "status": "CREATED",
            "statusUpdatedTime": "2022-07-16T08:21:24.409Z",
            "errors": [],
            "createdTime": "2022-07-16T08:21:24.409Z"
          }
        ],
        // use nextLink to get more results
        "nextLink": "https://{endpoint}/metricsadvisor/adel/multivariate/models?api-version=2022-07-10-preview&skip=1&maxpagesize=1&sortBy=modelName&orderBy=DESCENDING&status=CREATED&datasetNames=prod_controlValve_5min_v1,prod_controlValve_10min_v1&topPerDataset=2" 
      }
    }
  }
}
```

#### 4.2.2 Get a model by model name 

To get the status and details of a specific model with its model name, you can use `[GET] /https://{endpoint}/multivariate/models/{modelName}`.

Here is a sample **response** if you try to get the details for a `COMPLETED` model: 

```json
// Sample response
{
  "responses": {
    "200": {
      "body": {
        "modelName": "controlValve_5min_v1_model",
        "modelDescription": "Control valve model trained with 3-month data (excl. planned maintenance in May).",
        "datasetName": "prod_controlValve_5min_v1",
        "trainingTimeRangeList": [
          {
            "startTime": "2022-03-17T08:00:00.000Z",
            "endTime": "2022-05-01T08:00:00.000Z"
          },
          {
            "startTime": "2022-05-02T08:00:00.000Z",
            "endTime": "2022-06-16T08:00:00.000Z"
          }
        ],
        "slidingWindow": 300,
        "alignPolicy": {
          "alignMode": "Outer",
          "fillNAMethod": "Customized",
          "paddingValue": 0
        },
        "diagnosticsInfo": {
          "modelState": { 
            // Summarizes information about a model training process
            "epochIds": [
              10,
              20,
              30,
              40,
              50,
              60,
              70,
              80,
              90,
              100
            ],
            "trainLosses": [
              0.6291328072547913,
              0.1671326905488968,
              0.12354248017072678,
              0.1025966405868533,
              0.0958492755889896,
              0.09069952368736267,
              0.08686016499996185,
              0.0860302299260931,
              0.0828735455870684,
              0.08235538005828857
            ],
            "validationLosses": [
              1.9232804775238037,
              1.0645641088485718,
              0.6031560301780701,
              0.5302737951278687,
              0.4698025286197664,
              0.4395163357257843,
              0.4182931482799006,
              0.4057914316654053,
              0.4056498706340729,
              0.3849248886108984
            ],
            "latenciesInSeconds": [
              0.3398594856262207,
              0.3659665584564209,
              0.37360644340515137,
              0.3513407707214355,
              0.3370304107666056,
              0.31876277923583984,
              0.3283309936523475,
              0.3503587245941162,
              0.30800247192382812,
              0.3327946662902832
            ]
          },
          "variableStates": [ 
            //Summarizes detailed information about the variables being used for model training
            {
              "variable": "temperature_delta",
              "filledNARatio": 0,
              "effectiveCount": 26208,
              "firstTimestamp": "2022-03-17T08:00:00.000Z",
              "lastTimestamp": "2022-06-16T08:00:00.000Z"
            },
            {
              "variable": "pressure_delta",
              "filledNARatio": 0,
              "effectiveCount": 26208,
              "firstTimestamp": "2022-03-17T08:00:00.000Z",
              "lastTimestamp": "2022-06-16T08:00:00.000Z"
            },
            {
              "variable": "travel_minimumValue",
              "filledNARatio": 0.9573031135531136, // filledNARatio > 0 indicates that there are missing values for this varaible at the tiem of training
              "effectiveCount": 25089,
              "firstTimestamp": "2022-03-17T08:00:00.000Z",
              "lastTimestamp": "2022-06-15T15:05:00.000Z"
            }
          ]
        },
        "status": "COMPLETED",
        "statusUpdatedTime": "2022-07-16T08:59:56.592Z",
        "errors": [],
        "createdTime": "2022-07-16T08:21:24.409Z"
      }
    }
  }
}
```

### 4.3 Parameter details 

**Request headers**

`Ocp-Apim-Subscription-Key`: Your Metrics Advisor resource key. This subscription key provides you access to this API.


**URI parameter**
>**_NOTE:_**
> This is only applicable when you try to get a spcific model by its name.

`modelName`: Unique identifier of a model. _Cannot be changed once a model has been created._
  - Type: string
  - Case-sensitive: Yes
  - Character length: [1, 200]
  - Valid characters: A-Z, a-z, 0-9, _(underscore), and -(hyphen). Name starts with an _(underscore) or -(hyphen) will not be accepted.

**Query parameter**

**Required**

`apiVersion`: The current API version is **2022-07-10-preview**.

**Optional**
>**_NOTE:_**
> These optional parameters are only applicable when you try to get a list of models.

`skip`: The number of records to skip from the list of records based on the sorting field and ordering method specified. 
  - Type: int32
  - Default value (i.e., if not otherwise specified in the URL): 0
  - Minimum value: 0

`maxpagesize`: The maximum number of records to be returned per page. If more records are requested via the API, @nextLink will contain the link to the next page.
  - Type: int32
  - Default value (i.e., if not otherwise specified in the URL): 10
  - Minimum value: 1

`sortBy`: The name of the field on which you want to sort records. 
  - Type: string
  - Default value (i.e., if not otherwise specified in the URL): `createdTime`

`orderBy`: Determines whether the records will be returned in descending or ascending order.
  - Type: string
  - Default value (i.e., if not otherwise specified in the URL): DESCENDING

`status`: Filter model evaluations by one of the evaluation statuses: CREATED, RUNNING, COMPLETED, or FAILED.
  - Type: string
  - Default value: all statuses will be returned unless otherwise specified in the URL.

`datasetNames`: Filter models by a list of training dataset name(s). For each dataset, by default the list of models are ranked by descending model created time (UTC).
  - Type: string
  - Pattern: comma-separated, no space allowed

`topPerDataset`: The total number of models to be returned per dataset, ordered by created time descending.
  - Type: string
  - Default value: -1 (the full list of models will be returned for all the dataset name(s) in your filter)

**Response parameters**

Besides what you've input when creating the model, here is a list of additional read-only parameters you would see in the API response: 


| **Parameters** | **Description** | **Type** | 
| :----------- | :----------- | :----------- | 
| **modelState**|  
| `epochIds` |  How many epochs the model has been trained out of a total of 100 epochs. For example, if the returned epochIds is [10, 20, 30, 40, 50], it means that the model has completed its 50th training epoch, i.e., the training process is 50% completed. | int32[] |
| `latenciesInSeconds` |  The time cost (in seconds) for every 10 epochs, which can help you estimate the training completion time. In the [sample response](#422-get-a-model-by-model-name) above, the 10th epoch takes approximately 0.33 second. | float32[] |
| `trainLosses` |  Indicates how well the model fits the training data. | float32[] | 
| `validationLosses` |  Indicates how well the model fits the test data. | float32[] | 
| **variableStates**| 
| `variable` | The name of the variable being used for model training. | string |
| `filledNARatio` | Proportion of `NaN` values filled for the variable. For example, if 1000 timestamps was used for training and a given variable only have values for 900 timestamps, then the filledNARatio for this variable is 0.1. | float32 |
| `effectiveCount` | Number of valid data points for the variable. For example, if 1000 timestamps was used for training and a given variable only have values for 900 timestamps, then the effectiveCount for this variable is 900. | int32 |
| `firstTimestamp` | The first timestamp taken from the data source for a given variable. Different variables may have a different firstTimestamp due to missing values. | timestamp |
| `lastTimestamp` | The last timestamp taken from the data source for a given variable. Different variables may have a different lastTimestamp due to missing values. | timestamp |
| `status`| Current status of the model training job. | string |
| `statusUpdatedTime`| The UTC time at which the training status of the model was last updated (if applicable). For instance, the time at which the model status changed from RUNNING to COMPLETED. | timestamp |
| `errors`| Errors during data processing and training.| ErrorResponse property (error codes and messages)|
| `createdTime` | The UTC time at which the model was created. | timestamp |

### 4.4 FAQ and best practices 
**Q：How to estimate which model is best to use according to training loss and validation loss?**

A: Generally speaking, it's hard to decide which model is the best without a labeled dataset. However, we can leverage the training and validation losses to have a rough estimation and discard those bad models. 

- First, check whether training losses converge. Divergent losses often indicate poor quality of the model. 
- Second, loss values may help identify whether underfitting or overfitting occurs. Models that are underfitting or overfitting may not have desired performance. 
- Third, although the definition of the loss function doesn't reflect the detection performance directly, loss values may be an auxiliary tool to estimate model quality. Low loss value is a necessary condition for a good model, thus we may discard models with high loss values.

### 4.5 Related APIs you may need

- `[PUT] /multivariate/models/{modelName}`: **Create** and train a model. 
- `[DELETE] /multivariate/models/{modelName}`: **Delete** a model in a Metrics Advisor resource.


## 5. Evaluate model performance

### 5.1 Goal for this step 

Now that you've successfully trained a model, we highly recommend you test the quality of a trained model on a new set of data and inspect the detected anomalies by creating a model evaluation. 

The results of a model evaluation can be [visually inspected](#/docs/04-Creating%20an%20evaluation%20and%20reviewing%20evaluation%20results.md) and further processed by applied filters based on your business needs, which we will talk more in [Step 6: Post-process evaluation results and determine the desired alert settings](#6-post-process-evaluation-results-and-determine-the-desired-alert-settings). 

Let's first start with creating an evaluation job.

### 5.2 REST API samples

For example, you've trained a model this data from March 2022 to June 2022 and now you'd like to test the model performance with some new data from the past month (in this case, June-16 to July-15). 

To create an evaluation job, you can call `[PUT] multivariate/evaluations/{evaluationName}` and kick off the model evaluation process.

**Sample Request**

```json
{
  "parameters": {
    "endpoint": "{endpoint}", // Your Metrics Advisor resource endpoint URL  
    "apiVersion": "2022-07-10-preview",
    "Ocp-Apim-Subscription-Key": "{API key}", // Your Metrics Advisor resource key
    "Content-Type": "application/json",
    "evaluationName": "prod_controlValve_5min_v1_model_evaluation", // Unique and case-sensitive
    "body": {
      "evaluationDescription": "{Optional field to add more details}",
      "modelName": "controlValve_5min_v1_model",
      "datasetName": "prod_controlValve_5min_v1", // Ensure this dataset has the same schema as your training dataset
      "startTime": "2022-06-16T08:05:00.000Z", 
      "endTime": "2022-07-15T08:00:00.000Z"
      // Both the start and end timestamps are inclusive
    }
  }
}
```
**Response**

You will get either a 201 or 200 reponse if the request was successful.


### 5.3 Parameter details 

**Request headers**

`Ocp-Apim-Subscription-Key`: Your Metrics Advisor resource key. This subscription key provides you access to this API.

`Content-Type`: Media type of the body sent to the API.

**URI parameter**

`evaluationName`: Unique identifier of a model evaluation. _Cannot be changed once an evaluation has been created._
  - Type: string
  - Case-sensitive: Yes
  - Character length: [1, 200]
  - Valid characters: A-Z, a-z, 0-9, _(underscore), and -(hyphen). Name starts with an _(underscore) or -(hyphen) will not be accepted.

**Query parameter**

**Required**

`apiVersion`: The current API version is **2022-07-10-preview**.

**Request body parameters**

The request accepts the following data in JSON format.

| **Parameters** | **Description** | **Type** | **Pattern** |
| :----------- | :----------- | :----------- | :----------- |
| `evaluationDescription` | _Optional._ Provide more information about this model evaluation. | string | Character length: [0, 1024]|
|`modelName` | _Required._ The trained model to be evaluated. | string | Case-sensitive: Yes| 
| `datasetName` | _Required._ The data being used to evaluate the model. This evaluation dataset should have the same schema and data granularity as the training dataset for the model. | string | Case-sensitive: Yes |
| `startTime` | _Required._ The first timestamp to be used for model evaluation. Ensure that this timestamp has data in your dataset. | timestamp | `yyyy-MM-ddTHH:mm:ss`; conform to `ISO 8601` standard |
| `endTime` | _Required._ The last timestamp equal to or less than the end time given will be used for model evaluation. If endTime equals to startTime, one single data point will be processed. **Please refer to [Quotas and Limits](#/docs/08-Quota.md) for the maximum number of data points that each evaluation job can take.** | timestamp | `yyyy-MM-ddTHH:mm:ss`; conform to `ISO 8601` standard |


### 5.4 FAQ and best practices

**Q: Is model evaluation absolutely needed?**

A: Thought model evaluation is not required, this step is highlight recommended for the following reasons: 

- Detailed information about abnormal equipment behavior events are provided in the evaluation output. Not only can you calculate the accuracy of the model results, but you can also partner with your subject matter experts (SMEs) to check if the explainability of the detected abnormal events meets your expectation. 
- If you have labels, you can see how the model's predictions compare to the label data. You can also leverage this comparison to determine the optimal alert configuration in preparation for setting up a streaming inference schedule.   

**Q: Is there a limit on the number of evaluations I can create for each model?**

A: Yes, for detailed numebers please refer to the [Quotas and Limits](#/docs/08-Quota.md) page for the latest information. 



### 5.5 Related APIs you may need

- `[GET] /multivariate/evaluations/{evaluationName}`: **Get** model evaluation info including model evaluated, evaluation dataset, evaluation time range, evaluation job status, etc. 
- `[GET] /multivariate/evaluations[?skip][&maxpagesize][&sortBy][&orderBy][&status][&modelNames][&topPerModel]`: **List** model evaluations in a Metrics Advisor resource.
- `[DELETE] /multivariate/evaluations/{evaluationName}`: **Delete** an evaluation in a Metrics Advisor resource.



## 6. Post-process evaluation results and determine the desired alert settings

### 6.1 Goal for this step 

After your model evaluation job succeeded, you can call the `[GET] /multivariate/evaluations/{evaluationName}` to retrieve the evaluation result via an Azure Blob URL provided in the API response body. 

In this section, we will also go through how to interpret the evaluation results and tune the results based on your success metrics and business needs. 


### 6.2 REST API samples


**Sample Response**

Let's first look at a sample response when you called `[GET] /multivariate/evaluations/{evaluationName}`. Note that you can download the detailed evaluation result thru the Azure Blob URL provided in the `resultUrl` field. 

```json
// Sample response for [GET] /multivariate/evaluations/{evaluationName}

{
  "responses": {
    "200": {
      "body": {
        "evaluationName": "prod_controlValve_5min_v1_model_evaluation",
        "evaluationDescription": "Evaluate controlValve_5min_v1_model performance with 0616-0715 data.",
        "modelName": "controlValve_5min_v1_model",
        "datasetName": "prod_controlValve_5min_v1",
        "startTime": "2022-06-16T08:05:00.000Z",
        "endTime": "2022-07-15T08:00:00.000Z",
        "status": "COMPLETED",
        "statusUpdatedTime": "2022-07-16T14:50:29.324Z",
        "errors": [],
        "resultUrl": "{azure_blob_url_with_SAS_token}", // Download detailed results with this link
        "variableStates": [
          //Summarizes information about the variables being used for model training
          {
            "variable": "temperature_delta",
            "filledNARatio": 0,
            "effectiveCount": 8352,
            "firstTimestamp": "2022-06-16T08:05:00.000Z",
            "lastTimestamp": "2022-07-15T08:00:00.000Z"
          },
          {
            "variable": "pressure_delta",
            "filledNARatio": 0,
            "effectiveCount": 8352,
            "firstTimestamp": "2022-06-16T08:05:00.000Z",
            "lastTimestamp": "2022-07-15T08:00:00.000Z"
          },
          {
            "variable": "travel_minimumValue",
            "filledNARatio": 0,
            "effectiveCount": 8352,
            "firstTimestamp": "2022-06-16T08:05:00.000Z",
            "lastTimestamp": "2022-07-15T08:00:00.000Z"
          }
        ],
        "createdTime": "2022-07-16T14:26:43.948Z"
      }
    }
  }
}
```
**Evaluation Result Details**

The json file you downloaded with the `resultUrl` will be look like this: 

```json

{
  "results": [
    {
      "timestamp": "2022-07-19T00:27:00.000Z",
      "errors": [
        {
          "code": "InsufficientHistoricalData",
          "message": "historical data is not enough."
        }
      ]
    },
    {
      "timestamp": "2022-07-19T00:28:00.000Z",
      "value": {
        "isAnomaly": false,
        "severity": 0,
        "score": 0.3928471326828003
      },
      "errors": []
    },
    {
      "timestamp": "2022-07-19T00:29:00.000Z",
      "value": {
        "isAnomaly": true,
        "severity": 0.5337404608726501,
        "score": 0.9171165823936462,
        "interpretation": [
          {
            "variable": "travel_minimumValue",
            "contributionScore": 0.6261499548828445,
            "correlationChanges": {
              "changedVariables": [],
              "changedValues": []
            }
          },
          {
            "variable": "temperature_delta",
            "contributionScore": 0.2585569577470235,
            "correlationChanges": {
              "changedVariables": [
                "pressure_delta"
              ],
              "changedValues": [
                0.1229392
              ]
            }
          },
          {
            "variable": "pressure_delta",
            "contributionScore": 0.115293087370132,
            "correlationChanges": {
              "changedVariables": [
                "temperature_delta"
              ],
              "changedValues": [
                0.1093203
              ]
            }
          }
          // More contributing variables
        ]
      },
      "errors": []
    }
    // More timestamps
  ]
}
```
The results contains a few key concepts:

- `InsufficientHistoricalData` error: This usually happens only with the first few timestamps because the model inferences data in a window-based manner and it requires enough historical data to make a decision. The minimum amount of historical data required depends on the size of your `slidingWindow` (see [how slidingWindow is used](#34-faq-and-best-practices)). 

- `isAnomaly`: **false** indicates the current timestamp is NOT an anomaly. **true** indicates an anomaly at the current timestamp.

- `score`: score is the raw output of the model on which the model makes a decision. Every timestamp should have a score, except the timestamps with InsufficientHistoricalData error.

- `severity`: this field is a derived value from score and normalized into a number between 0 and 1. It indicates the relative severity of a given anomaly. Note that severity value will only be available is a timestamp has been detected as an anomly (i.e., `isAnomaly` = true). For normal timestamps, it is always 0. 

- `interpretation`: this field is only available when `isAnomaly` = true for a given timestamp. Information listed aims to explain why the model detected a given timestamp as an anomaly and help you diagnose the root cause. Specifically - 
  
  - `variable`: Name of the top contributing variable to a given anomaly. Contributing variable are ranked in descending contributionScore order.

  - `contributionScore`: Higher contribution scores indicate higher possibility of the root cause. 

  - `correlationChanges`: A list of correlated variable(s) whose correlation with this contributing variable has changed significantly. This field can be empty if there were no significant correlation changes between the contributing variable and other variables. `changedVariables` contains the list of variable(s) whose correlation to the contributing variable has changed. `changedValues` contains values that indicates the extent to which the correlation(s) has changed for a given changedVariable.


### 6.3 Best practices for tuning evaluation results

First, you should decide the success metrics for the model. Metrics such as precision, true positive rate (i.e., recall), number of false positives per month, average forewarning time, etc. are commonly used ones by our customers.

Then, with the success metrics in mind, you are recommended to compare the evaluation results with label data (timesamps or time ranges where true equipment failures / anomalies happened). At first, there might be too many false alerts being identified by the model. If so, you try set up different threshold on `severity` to filter out less severe anomalies and see if the rest anomalies align better with your labels. 

- For example, you may have 100 timestamps with `isAnomaly` = true in the beginning, while probably only 20 of them are true anomalies. Then, you observed that more than half of the false positives have a severity lower than 0.3 while most true anomalies are above, so a threshold of 0.3 on severity could help you filter out a large portion of the false alerts. If your stakeholder only want to be notified when something serious happens, you can further raise the severity threshold to a higher value based on your business stakeholder's preference. 

- Note: on our web portal and alert configuration APIs, `sensitivity` is the name of the concept that's equivalent to a severity threshold. `sensitivity` is a number between 0 and 100, and is caculated as (1 -`severity`) * 100. In general, a high sensitivity value means the model is more sensitive to outliers and is likely to identify more anomalies. A low sensitivity value usually means the model will tolerate minor outliers.

Finally, once you've tested a few severity threshold (or `sensitivity` values), make a note of this number as you will need it when setting up the alert configuration for streaming inference.


### 6.4 Related APIs you may need

- `[PUT] /alertConfigs/{alertConfigName}`: **Create** an alert configuration.
- `[GET] /multivariate/evaluations[?skip][&maxpagesize][&sortBy][&orderBy][&status][&modelNames][&topPerModel]`: **List** model evaluations in a Metrics Advisor resource.
- `[DELETE] /multivariate/evaluations/{evaluationName}`: **Delete** an evaluation in a Metrics Advisor resource.


## 7. Configure your hook and alert preferences

### 7.1 Goal for this step 

If you felt confident with the model based on the evaluation result, the next step is to configure your alert preferences before setting up a streaming inference schedule to detect anomalies with the model in real-time. 

To do so, you can: 
1. set up a hook (i.e., an alert notification channel) by using `[PUT] /hooks/{hookName}` 
2. configure alert preference by using `[PUT] /alertConfigs/{alertConfigName}`
Set a lower sensitivity to get notified only when severe anomalies are detected. Set a higher sensitivity to detect anomalies that are less severe.​


### 7.2 Set up a hook 

#### 7.2.1 REST API samples

**Sample Request**

```json
{
  "parameters": {
    "endpoint": "{endpoint}",
    "apiVersion": "2022-07-10-preview",
    "Ocp-Apim-Subscription-Key": "{API key}",
    "Content-Type": "application/json",
    "hookName": "WebhookToDS",
    "body": {
      "hookType": "Webhook", 
      "hookDescription": "Webhook for data scientists to receive anomaly alerts for control valves.",
      "endpoint": "{https://datasciencecentral.contoso.example/api/AnomalyAlertControlValve}", // Replace with the endpoint to receive alerts
      "header": {},
      "credential": "https://contoso.key_vault.azure.example/secrets/00000000-0000-0000-0000-000000000000" // Optional if authentication is not needed
    }
  }
}
```
**Response**

You will get either a 201 or 200 reponse if the request was successful.


#### 7.2.2 Parameter details 

**Request headers**

`Ocp-Apim-Subscription-Key`: Your Metrics Advisor resource key. This subscription key provides you access to this API.

`Content-Type`: Media type of the body sent to the API.

**URI parameter**

`hookName`: Unique identifier of a hook. _Cannot be changed once a hook has been created._
  - Type: string
  - Case-sensitive: Yes
  - Character length: [1, 200]
  - Valid characters: A-Z, a-z, 0-9, _(underscore), and -(hyphen). Name starts with an _(underscore) or -(hyphen) will not be accepted.

**Query parameter**

**Required**

`apiVersion`: The current API version is **2022-07-10-preview**.

**Request body parameters**

The request accepts the following data in JSON format.

| **Parameters** | **Description** | **Type** | **Pattern** |
| :----------- | :----------- | :----------- | :----------- |
| `hookType`| _Required._ The type of the notification channel to receive alert. Only Webhook is supported in the current version. | string| |
| `hookDescription`| _Optional._ Detailed description of a hook.| string||
| `endpoint`| _Required._ The API address to be called when an alert is triggered. MUST be Https.
| `header`| _Optional._ Custom headers in the API call. A string map include key-value pairs.| key-value pair(s) | For example, a header could be {"Content-Type": "application/json"}
| `credential`| _Optional._ For authenticating to the endpoint. Optional if authentication is not needed. | string | URL |

### 7.3 Configure alert preferences

#### 7.3.1 REST API samples

**Sample Request**

```json
{
  "parameters": {
    "endpoint": "{endpoint}",
    "apiVersion": "2022-07-10-preview",
    "Ocp-Apim-Subscription-Key": "{API key}",
    "Content-Type": "application/json",
    "hookName": "WebhookToDS",
    "body": {
      "hookType": "Webhook", 
      "hookDescription": "Webhook for data scientists to receive anomaly alerts for control valves.",
      "endpoint": "{https://datasciencecentral.contoso.example/api/AnomalyAlertControlValve}", // Replace with the endpoint to receive alerts
      "header": {},
      "credential": "https://contoso.key_vault.azure.example/secrets/00000000-0000-0000-0000-000000000000" // Optional if authentication is not needed
    }
  }
}
```
**Response**

You will get either a 201 or 200 reponse if the request was successful.


#### 7.2.2 Parameter details 

**Request headers**

`Ocp-Apim-Subscription-Key`: Your Metrics Advisor resource key. This subscription key provides you access to this API.

`Content-Type`: Media type of the body sent to the API.

**URI parameter**

`hookName`: Unique identifier of a hook. _Cannot be changed once a hook has been created._
  - Type: string
  - Case-sensitive: Yes
  - Character length: [1, 200]
  - Valid characters: A-Z, a-z, 0-9, _(underscore), and -(hyphen). Name starts with an _(underscore) or -(hyphen) will not be accepted.

**Query parameter**

**Required**

`apiVersion`: The current API version is **2022-07-10-preview**.

**Request body parameters**

The request accepts the following data in JSON format.

| **Parameters** | **Description** | **Type** | **Pattern** |
| :----------- | :----------- | :----------- | :----------- |
| `hookType`| _Required._ The type of the notification channel to receive alert. Only Webhook is supported in the current version. | string| |
| `hookDescription`| _Optional._ Detailed description of a hook.| string||
| `endpoint`| _Required._ The API address to be called when an alert is triggered. MUST be Https.
| `header`| _Optional._ Custom headers in the API call. A string map include key-value pairs.| key-value pair(s) | For example, a header could be {"Content-Type": "application/json"}
| `credential`| _Optional._ For authenticating to the endpoint. Optional if authentication is not needed. | string | URL |


### 7.5 Related APIs you may need

- `[DELETE] /multivariate/evaluations/{evaluationName}`: **Delete** a evaluation in a Metrics Advisor resource.

## 8. Set up a streaming inference schedule


## 9. Get streaming inference results and diagnose alerts


## 10. Trigger a replay on an existing inference schedule
