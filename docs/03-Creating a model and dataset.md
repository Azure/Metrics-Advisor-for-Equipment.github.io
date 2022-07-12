# ⭐Creating a model and dataset

You've ingested your dataset, and you've reviewed any issues with the job, the files, or the sensors. You've also decided which sensors are providing the data that will be used to train your model. Now it's time to move forward with creating the model.

## 1. About the left navigation panel

After you navigate to the workspace,  a navigation panel appears in the left side of the Metrics Advisor for Equipment UI.

The first three items in the left navigation panel—**Models**, **Datasets**, **Visualization** and **Settings**. If you select:

- **Models**, you can use the models navigation bar to access all existing models, or create a new model.
- **Datasets**, you can use the datasets navigation bar to access all existing datasets, or create a new dataset.
- **Visualization**, you can use the visualization navigation bar to access a inference graphs and contribution rank.
![image](https://user-images.githubusercontent.com/36343326/176643695-d39385ed-26f3-4501-bb36-d4f79559e532.png)

## 2. Create a new model

Click **Create a new model**.
![image](https://user-images.githubusercontent.com/36343326/175043087-24453360-a2a6-41db-85c9-cee02a0d1e5c.png)

When you create a model, the model name must be unique. The model name can contain the following:

- Make sure your name doesn't include any invalid characters, such as spaces.

- Max character limit: 200 characters.

- Valid characters are: 0-9, a-z, A-Z, and # $ . \ - (hyphen) _ (underscore)

- Make sure that you don't have any duplicated names.

![image](https://user-images.githubusercontent.com/36343326/175043374-999d68a9-f23b-46ed-87b5-90dd5bf08e8e.png)

## 3. Create/Select a Dataset

#### Create a new dataset

Click **Create dataset**:

- `Dataset Granularity` is the smallest interval at which the sensor readings are recorded in your dataset. For example, sensor A records data every 1 min and sensor B records data every 5 min. In such cases, please use 1 min as your data granularity and all the sensor data should be pre-processed (rounded to the nearest 1min timestamps). 

- `Data source` is the type of data source where your time series data is stored. Choose Azure SQL or Azure Blob.

- `Authentication type`  : you need to assign managed identity to Metrics Advisor for Equipment. [How to assign role to a resource](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/managed_identity.md).

- `Server name/Database name`: separate your SQL server name and database name with a “/”.

- `Data schema` : Metrics Advisor for equipment accepts tables with only three columns, the time-series data from sensors on your equipment must be properly formatted in three columns. Each of the three columns in your data table/file should belong to one of the schema types below. No duplicate column headers are allowed. 

  - **Timestamp**: This is the column with time-series data.
  - **Variable name**: This is the column with the names of all the sensors you plan to include.
  - **Value**: This is the column with data collected by your sensors. You must have a double (numerical) as the data type for values in this column.

  Click **Load Data** to complete the creation, then you can find the created dataset.

![image](https://user-images.githubusercontent.com/36343326/175043003-899fdd93-d535-4804-b341-e49410653217.png)

#### Preview dataset











## 4. Training Parameters

First, you'll specify the details of your model, such as its training time range, and advanced settings.

![image](https://user-images.githubusercontent.com/36343326/175045723-4cb8bc63-bf87-4748-ae04-f790e0f805d6.png)

- When selecting training time range, you'll need to specify a subset of data on which to train your model. Your specified training time ranges must fall within the first recorded timestamp and the last recorded timestamp of your dataset.

  **_NOTE:_**  During this process, you'll make decisions about the balance between your training dataset and your evaluation dataset, and whether or not to use data labels in later process.

- Under training time range, use the time pickers to select the training dates and time that you want to include in your model. You could select multiple training time range, especially when your machine is off or in a state that your sensors are not producing useful data for identifying anomalies, you can filter out that date. 

## 5. Advanced settings

Optionally, There are several advanced settings to enable data ingested in a customized way:

- `sliding Window` - How many data points are used to determine anomalies. Our model takes a segment of data points to decide if the next data point is an anomaly. The length of this segment is sliding window. The default value is 300, but you can choose an integer between 28 and 2,880. 

> **_IMPORTANT NOTE:_**  Please keep two things in mind when choosing a `sliding Window` value:
>
> 1. The granularity of your data: When your data is at a high frequency (small granularity) like minute-level or second-level, you could set a relatively higher value of `sliding Window`.
> 2. Too large of a window can slow down performance without improving accuracy. Too small of a window makes it harder to detect anomalies. For data with frequency at the minute or second level, it's safer to set a higher value here. 

- `Missing data Filling Method` – we will automatically fill in missing data. Options are `Linear`, `Previous`, `Subsequent`, and `Custom`, and the default value is Linear. if you choose custom, then you need to fill the value for custom filling method.
- However, if too much original data is missing, it might affect your results.

Choose **Create**.

## 5. Training model detail

Starting the training process. Click the **model name**, then the **Training model detail** tab gives you a chance review model details such as the model name, the dataset, and training time range.

There are three kinds of training model status.

| Status    | Description                                |
| --------- | ------------------------------------------ |
| Running   | Training is in processing.                 |
| Completed | Training is done, you can start inference. |
| Failed    | Training is failed for some reason.        |

You can click the **View details** button for the error messages when you find the training model status gets to **Failed**.

## 6. Manage datasets

#### Search datasets by name

To search datasets by name you can enter a dataset name in the search box.

#### Sort datasets

Data feeds can be sorted by using the following methods:

- by created time

#### Delete your data feed

To delete a dataset, you need to complete the following steps:

1. On the datasets list page, click 'Delete' on the data feed.

2. In the dataset details page, click 'Delete'.

![image](https://user-images.githubusercontent.com/36343326/176643089-c06e12b8-0045-4ccd-b598-1b44ba1122ee.png)

## 7. Manage models

#### Search models by name

To search models by name you can enter a model name in the search box.

#### Sort models

Models can be sorted by using the following methods:

- by created time

#### Delete your models

To delete a model, you need to complete the following steps:

On the **Training detail** page, click 'Delete'.

![image](https://user-images.githubusercontent.com/36343326/176643591-6121a31f-7229-43c1-9eff-28ac189cec73.png)

**_NOTE:_**

- If training is running: Training must be completed before scheduling an inference and creating an evaluation.
- If training failed: Can't schedule an inference and evaluation on models with failed training. 