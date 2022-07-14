# ⭐Creating a model and dataset

Once you have ingested your dataset, you can train an anomaly detection model:

## 1. Create a new model

Click **Create a new model**.
![image](https://user-images.githubusercontent.com/36343326/175043087-24453360-a2a6-41db-85c9-cee02a0d1e5c.png)

When you create a model, the model name must be unique. The model name can contain the following:

- Make sure your name doesn't include any invalid characters, such as spaces.

- Max character limit: 200 characters.

- Valid characters are: 0-9, a-z, A-Z, and # $ . \ - (hyphen) _ (underscore)

- Make sure that you don't have any duplicated names.

![image](https://user-images.githubusercontent.com/36343326/175043374-999d68a9-f23b-46ed-87b5-90dd5bf08e8e.png)

## 2. Create/Select a Dataset

#### Create a new dataset

Click **Create dataset**:

- `Dataset Granularity` is the smallest interval at which the sensor readings are recorded in your dataset. For example, suppose that data from some sensors is being recorded every 1 minute and other sensors are recording every 5 minutes. In this case, set the data frequency to an interval of 1 minute. If your data granularity unit is minute, make sure that your data granularity is a multiple or factors of 60. 

- `Data source` is the type of data source where your time series data is stored. Choose Azure SQL or Azure Blob.

- `Authentication type`  : you need to assign managed identity to Metrics Advisor for Equipment. [How to assign role to a resource](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/managed_identity.md).

- `Server name/Database name`: separate your SQL server name and database name with a “/”. The database and table names are case sensitive. 

- `Data schema` : Metrics Advisor for equipment accepts tables with only three columns, the time-series data from sensors on your equipment must be properly formatted in three columns. Each of the three columns in your data table/file should belong to one of the schema types below. No duplicate column headers are allowed. 

  - **Timestamp**: This is the column with time-series data. The timestamp column should contain datetime values in the yyyy-MM-ddTHH:mm:ss format and conform to ISO 8601.
  - **Variable name**: The variable name column should contain the name of the variable for each data point.
  - **Variable Value**: The value column should contain numeric values.

  Click **Load Data** to complete the creation, then you can find the created dataset.

![image](https://user-images.githubusercontent.com/36343326/175043003-899fdd93-d535-4804-b341-e49410653217.png)

#### Preview dataset

Verify that the dataset you specified can be loaded correctly. 







## 3. Training Parameters

First, you'll specify the details of your model, such as its training time range, and advanced settings.

![image](https://user-images.githubusercontent.com/36343326/175045723-4cb8bc63-bf87-4748-ae04-f790e0f805d6.png)

- When selecting training time range, you'll need to specify a subset of data on which to train your model. Your specified training time ranges must fall within the first recorded timestamp and the last recorded timestamp of your dataset.

  **_NOTE:_**  During this process, you'll make decisions about the balance between your training dataset and your evaluation dataset, and whether or not to use data labels in later process.

- Under training time range, use the time pickers to select the training dates and time that you want to include in your model. You could select multiple training time range, especially when your machine is off or in a state that your sensors are not producing useful data for identifying anomalies, you can filter out that date. 

## 4. Advanced settings

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

Starting the training process. You will see a progress status update every five minutes until the training is successful. Depending on the size of dataset used, the training can take up to an hour.

Click the **model name**, then the **Training model detail** tab gives you a chance review model details such as the model name, the dataset, and training time range.

There are three kinds of training model status.

| Status    | Description                                |
| --------- | ------------------------------------------ |
| Running   | Training is in processing.                 |
| Completed | Training is done, you can start inference. |
| Failed    | Training is failed for some reason.        |

You can click the **View details** button for the error messages when you find the training model status gets to **Failed**.

Once your model is trained, you can either check the results or configure an evaluation or inference scheduler.



#### Delete your models

To delete a model, you need to complete the following steps:

On the **Training detail** page, click 'Delete'.

![image](https://user-images.githubusercontent.com/36343326/176643591-6121a31f-7229-43c1-9eff-28ac189cec73.png)

**_NOTE:_**

- If training is running: Training must be completed before scheduling an inference and creating an evaluation.
- If training failed: Can't schedule an inference and evaluation on models with failed training. 



## 6. Datasets lists and dataset detail

#### Delete your dataset

To delete a dataset, you need to complete the following steps:

1. On the datasets list page, click 'Delete' on the data feed.

2. In the dataset details page, click 'Delete'.

   Removing a dataset means it won't be available to training, evaluation, or inferences anymore. This doesn't delete the data in the source system and it can't be undone.

   **Delete error**: Couldn't delete a dataset because it's used in training, evaluation, or an inference. Delete the dependencies first, then try again.

   

![image](https://user-images.githubusercontent.com/36343326/176643089-c06e12b8-0045-4ccd-b598-1b44ba1122ee.png)

