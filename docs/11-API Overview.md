# ⭐API Overview

>**_NOTE:_**
> Metrics Advisor for Equipment (Project Adel) is currently in private preview. Some features may not be supported or have limited capabilities.
The current API version is **2022-07-10-preview**.

| [REST API]() | [Python SDK]() |

Metrics Advisor for Equipment offers a full list of APIs, covering functionalities in:
* [Datasets](#datasets-4-apis)
* [Model training](#models-4-apis)
* [Model evaluation](#evaluations-4-apis)
* [Hook and alert configurations](#hooks-and-alert-configurations-10-apis)
* [Streaming inference schedule](#inference-schedule-10-apis)

You should also refer to [Quotas and limits](./08-Quota.md) for a quick reference and a detailed description the quotas and limits for Metrics Advisor for Equipment.

Here are the **32 APIs** in Metrics Advisor for Equipment:


## **Datasets** (4 APIs)

A dataset in Metrics Advisor for Equipment contains the metadata describing where the data is and what the data actually looks like. **Specifically, it contains the location of the data source, the data schema, and other information.** The dataset you created can be used for model training, evaluation, and/or real-time streaming inference.

| HTTP Method | API Path | Description | 
| :----------- | :-------- | :----------- | 
| PUT | `/datasets/{datasetName}` | **Create/add** a dataset for training, evaluation, or real-time inference.| 
| GET | `/datasets/{datasetName}` | **Get** dataset ianfo including data source type, data schema, data granularity, etc.| 
| GET | `/datasets[?skip][&maxpagesize][&sortBy][&orderBy]` | **List** models in a subscription. | 
| DELETE | `/datasets/{datasetName}` | **Delete** a dataset in a subscription. _This action doesn't delete the data in the source system._|


## **Models** (4 APIs)

A Metrics Advisor for Equipment model is a machine learning model that learns the patterns of normal behavior (i.e., training dataset) and detects abnormal behavior that could be potential equipment failure (or maintenance events). _On the backend, we will divide your training dataset into train & test sets and return the training and validaiton loss scores for your reference._

| HTTP Method | API Path | Description | 
| :----------- | :-------- | :----------- |  
| PUT | `/multivariate/models/{modelName}` | **Create** and train a model.| 
| GET | `/multivariate/models/{modelName}` | **Get** model info including training dataset, training time range(s), variables being used, training job status, etc.| 
| GET | `/multivariate/models[?skip][&maxpagesize][&sortBy][&orderBy][&status][&datasetNames][&topPerDataset]` | **List** models in a subscription. | 
| DELETE | `/multivariate/models/{modelName}` | **Delete** a model in a subscription.|


## **Evaluations** (4 APIs)

An evaluation is the process of using different dataset(s) to test the performance a trained model. You are highly recommended to review and tune the evaluation results with subject matter expertises (SMEs) at your company.

| HTTP Method | API Path | Description | 
| :----------- | :-------- | :----------- | 
| PUT | `/multivariate/evaluations/{evaluationName}` | **Create** a model evaluation. | 
| GET | `/multivariate/evaluations/{evaluationName}` | **Get** model evaluation info including model evaluated, evaluation dataset, evaluation time range, evaluation job status, etc. | 
| GET | `/multivariate/evaluations[?skip][&maxpagesize][&sortBy][&orderBy][&status][&modelNames][&topPerModel]` | **List** model evaluations in a subscription. | 
| DELETE | `/multivariate/evaluations/{evaluationName}` | **Delete** an evaluation in a subscription. |


## **Hooks and Alert Configurations** (10 APIs)

A **hook** is a channel to receive alert notifications.

| HTTP Method | API Path | Description | 
| :----------- | :-------- | :----------- | 
| PUT | `/hooks/{hookName}` | **Create** a hook. | 
| GET | `/hooks/{hookName}` | **Get** hook info including hook type and associated set up details. | 
| GET | `/hooks[?skip][&maxapgesize][&sortBy][&orderBy]` | **List** hooks in a subscription. | 
| DELETE | `/hooks/{hookName}` | **Delete** a hook in a subscription. |
| PATCH | `/hooks/{hookName}` | **Update** a hook. _Updatable properties differ by hook type._|


An **alert configuration** allows users to set up criteria that determine which anomalies should trigger an alert and via which hook(s). This setting can later be applied to a streaming inference schedule. You are highly recommended to evaluate the model first and consult subject matter expertises (SMEs) at your company when setting up alert configurations. 

| HTTP Method | API Path | Description | 
| :----------- | :-------- | :----------- | 
| PUT | `/alertConfigs/{alertConfigName}` | **Create** an alert configuration. | 
| GET | `/alertConfigs/{alertConfigName}` | **Get** alert configuration info including alert configuration type and associated settings. | 
| GET | `/alertConfigs[?skip][&maxapgesize][&sortBy][&orderBy]` | **List** alert configurations in a subscription. | 
| DELETE | `/alertConfigs/{alertConfigName}` | **Delete** an alert configuration in a subscription. |
| PATCH | `/alertConfigs/{alertConfigName}` | **Update** an alert configuration. _Updatable properties differ by alert configuraiton type._ | 


## **Inference Schedule** (10 APIs)

An **inference schedule** sets up a streaming inference pipeline to analyze incoming data in real-time.

| HTTP Method | API Path | Description | 
| :----------- | :-------- | :----------- | 
| PUT | `/inference/schedules/{scheduleName}` | **Create** an inference schedule.| 
| GET | `/inference/schedules/{scheduleName}` | **Get** inference schedule info including model used, dataset used, data delay offset (if applicable), schedule start time , alert configurations, etc.| 
| GET | `/inference/schedules[?skip][&maxpagesize][&sortBy][&orderBy][&status][&modelNames][&topPerModel]` | **List** inference schedules in a subscription. | 
| DELETE | `/inference/schedules/{scheduleName}` | **Delete** an inference schedule in a subscription.|
| PATCH | `/inference/schedules/{scheduleName}` | **Pause/resume or update** selected properties of an inference schedule. _Updatable properties: inference status, model to be inferenced with, data delay offset, alert configurations._| 
| GET | `/inference/schedules/{scheduleName}/getHistory` | **Retrieve detected anomalies** over a historical time period. |

A **replay** allows you to inference a historical time range with settings from an exiting inference schedule. The new anomaly detection results will **overwrite** the historical results in the replay time range but no alerts will be sent out.

| HTTP Method | API Path | Description | 
| :----------- | :-------- | :----------- |  
| PUT | `/inference/replays/{replayName}` | **Create** a replay on an inference schedule.| 
| GET | `/inference/replays/{replayName}` | **Get** replay info including associated inference schedule, replay time range, replay job status, etc.| 
| GET | `/inference/replays[?skip][&maxpagesize][&sortBy][&orderBy][&status][&scheduleName][&topPerSchedule]` | **List** replay jobs in a subscription. | 
| DELETE | `/inference/replays/{replayName}` | **Delete** a replay job in a subscription. _This action doesn't revert the inference results in the replay time range._|


## Next steps
* [REST API How-to Guide](/docs/12-API%20How-to%20Guide.md)
* [Metrics Advisor for Equipment Quotas and Limits](/docs/08-Quota.md)
* [Responsible Use of AI](/docs/10-Responsible%20use%20of%20AI.md)
