# ⭐API How-to Guide

Azure Metrics Advisor for Equipment is a cloud-based [Azure Applied AI Service](https://docs.microsoft.com/en-us/azure/applied-ai-services/) that uses machine-learning models to scale predictive maintenance and proactively monitor the health of your physical assets. 

## Get started: Metrics Advisor for Equipment (Project Adel) REST API 2022-07-10-preview
>**_NOTE:_**
> Metrics Advisor for Equipment (Project Adel) is currently in private preview. Some features may not be supported or have limited capabilities.
The current API version is **2022-07-10-preview**.


In the following sections you will :
  1. [(Prerequisites) Create a Metrics Advisor resource in the Azure portal.](#1-prerequisites-create-a-metrics-advisor-resource-in-the-azure-portal)
  1. Prepare nad preprocess your data.
  1. [Create a dataset.](#2-prepare-data-and-create-a-dataset)
    `[PUT] https://{endpoint}/datasets/{datasetName}`
  1. [Train a Metrics Advisor for Equipment model.](#3-train-a-model)
  1. [Evaluate the model performance and download the evaluation results.](#4-evaluate-model-performance)
  1. [Post-process evaluation results and determine the desired alert settings.](#5-post-process-evaluation-results-and-determine-the-desired-alert-settings)
  1. [Configure and start an inference schedule.](#6-configure-and-start-an-inference-schedule)
  1. [Get streaming inference results and diagnose alerts.](#7-get-streaming-inference-results-and-diagnose-alerts)
  1. [Trigger a replay on an existing inference schedule to backfill/refresh detection results for a historical time period.](#8-trigger-a-replay-on-an-existing-inference-schedule)



## 1. (Prerequisites) Create a Metrics Advisor resource in the Azure portal
Here are three quick steps you need to take before using the Azure Metrics Advisor for Equipment fuctionalities: 
1. [Find Metrics Advisor service on the Azure portal.](#find-metrics-advisor-service-on-the-azure-portal)
2. [Create a Metrics Advisor resource.](#create-a-resource)
3. [Get your endpoint URL and keys.](#get-endpoint-url-and-keys)

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

### Goal for this step 


### REST API samples

`[PUT] https://{endpoint}/datasets/{datasetName}`

```json
// Sample Request
{
    "parameters": {
      "endpoint": "{endpoint}", // Replace with your Metrics Advisor resource endpoint URL  
      "apiVersion": "2022-07-10-preview",
      "Ocp-Apim-Subscription-Key": "{API key}", // Replace with your Metrics Advisor resource key
      "Content-Type": "application/json",
      "datasetName": "prod_controlValve_5min_v1", // Unique and case-sensitive. Valid characters are: A-Z, a-z, 0-9, _(underscore), and -(hyphen).
    "body": {
      "datasetDescription": "Prod data for control valves; aligned to 5min granularity.",
      "dataSourceInfo": {
        "dataSourceType": "SqlServer",
        "authenticationType": "ManagedIdentity",
        "serverName": "{your_sql_server_name}", // Replace with your Azure SQL server name
        "databaseName": "{your_database_name}", // Replace with your database name (must be in the server provided above)
        "tableName": "{your_sql_table_name}" // Replace with your SQL table or SQL view name (must be in the database provided above)
      },
      "dataSchema": {
        "dataSchemaType": "LongTable",
        "timestampColumnName": "eventTimeStamp", // Replace with the header of the column that contains datetime values
        "variableColumnName": "sensorName", // Replace with the header of the column that contains the names of your input variables
        "valueColumnName": "sensorValue" // Replace with the header of the column that contains numeric values
      },
      "dataGranularityNumber": 5,
      "dataGranularityUnit": "Minutes"
    }
  }
}
```


```json
// Sample Response

{  
  "responses": { // You will get either a 201 or 200 reponse
    "201": { 
      "body": {
        "datasetName": "prod_controlValve_5min_v1",
        "datasetDescription": "Prod data for control valves; aligned to 5min granularity.",
        "dataSourceInfo": {
          "dataSourceType": "SqlServer",
          "authenticationType": "ManagedIdentity",
          "serverName": "{your_sql_server_name}",
          "databaseName": "{your_database_name}",
          "tableName": "{your_sql_table_name}"
        },
        "dataSchema": {
          "dataSchemaType": "LongTable",
          "timestampColumnName": "eventTimeStamp",
          "variableColumnName": "sensorName",
          "valueColumnName": "sensorValue"
        },
        "dataGranularityNumber": 5,
        "dataGranularityUnit": "Minutes",
        "createdTime": "2022-07-15T13:10:02.493Z"
      }
    },
    "200": {
      "body": {
        "datasetName": "prod_controlValve_5min_v1",
        "datasetDescription": "Prod data for control valves; aligned to 5min granularity.",
        "dataSourceInfo": {
          "dataSourceType": "SqlServer",
          "authenticationType": "ManagedIdentity",
          "serverName": "{your_sql_server_name}",
          "databaseName": "{your_database_name}",
          "tableName": "{your_sql_table_name}"
        },
        "dataSchema": {
          "dataSchemaType": "LongTable",
          "timestampColumnName": "eventTimeStamp",
          "variableColumnName": "sensorName",
          "valueColumnName": "sensorValue"
        },
        "dataGranularityNumber": 5,
        "dataGranularityUnit": "Minutes",
        "createdTime": "2022-07-15T13:10:02.493Z"
      }
    }
  }
}
```
### FAQ and best practices 
- How to align my data to a single data granularity? 
  - Make sure that each variable has at most one data point within each interval.
- How do I find my SQL server, database, and table names?
  - 
  - If you do not have an Azure SQL database, [create a single database](#https://docs.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal).



### Parameter details 

#### URI parameter

`datasetName`: Unique identifier of a dataset. _Cannot be changed once a dataset has been created._
  - Type: string
  - Case-sensitive: Yes
  - Character length: [1, 200]
  - Valid characters: A-Z, a-z, 0-9, _(underscore), and -(hyphen). Name starts with an _(underscore) or -(hyphen) will not be accepted.

#### Query parameter
`apiVersion`: The current API version is **2022-07-10-preview**.

#### Request body parameters
The request accepts the following data in JSON format.

| **Required for** |**Parameters** | **Description** | **Type** | **Pattern** |
| :----------- | :----------- | :----------- | :----------- | :----------- |
| Optional | datasetDescription | Provide more information about this dataset. | string | Character length: [0, 1024]
| PUT | dataGranularityNumber | (Together with dataGranularityUnit) The frequency interval at which new records are added to your data.  | int32 | |
| PUT | dataGranularityUnit | (Together with dataGranularityNumber) The unit of your data frequency interval. | string | Valid values: Minutes, Hours, Days, Weeks, Months, Years. |
| **dataSourceInfo** | 
| PUT | dataSourceType | Type of your data scource. | string | Valid value: "SqlServer" |
| PUT | authenticationType | Method to authenticate Metrics Advisor for Equipment to access your data source. | string | Valid value: "ManagedIdentity" | 
| PUT (if dataSourceType = SqlServer ) | serverName | Name of a SQL Server. | string | Case-sensitive: No|
| PUT (if dataSourceType = SqlServer ) | databaseName | Name of a SQL Database. | string | Case-sensitive: Yes|
| PUT (if dataSourceType = SqlServer ) | tableName | Name of a SQL table or SQL view. | string | Case-sensitive: Yes| 
|**dataSchema**| | 
| PUT | dataSchemaType | Indicates how your data is formatted. <li>`LongTable`: A long-form data table has a single column that stores all the variables</li><li>`WideTable`: A wide-form data table spreads a variable across several columns</li> | string | Valid value: "LongTable" | 
| PUT  | timestampColumnName | Header of the column that contains datetime values | string | Case-sensitive: Yes|
| PUT | variableColumnName | Header of the column that contains the the names of your input variables | string | Case-sensitive: Yes|
| PUT (if dataSchemaType = LongTable ) | valueColumnName | Header of the column that contains numeric values | string | Case-sensitive: Yes|




Portal View: 


## 3. Train a model


## 4. Evaluate model performance


## 5. Post-process evaluation results and determine the desired alert settings


## 6. Configure and start an inference schedule


## 7. Get streaming inference results and diagnose alerts


## 8. Trigger a replay on an existing inference schedule