# Creating a model

## About the left navigation panel

After you navigate to the workspace,  a navigation panel appears in the left side of the Metrics Advisor for Equipment UI. 

The first three items in the left navigation panel—**Models**, **Datasets**, **Visulazaiton** and **Settings**. If you select:

- **Models**, you can use the models navigation bar to access all existing models, or create a new model.
- **Datasets**, you can use the datasets navigation bar to access all existing datasets, or create a new dataset.
- **Visulazaiton**, you can use the visulazaiton navigation bar to access a inference graphs and contribution rank.

## Create a new model

Click **Create a new model**.
![image](https://user-images.githubusercontent.com/36343326/175043087-24453360-a2a6-41db-85c9-cee02a0d1e5c.png)

### Model name

When you create a model, the model name must be unique .The model name can contain the following:

o	Make sure your name don't include any invalid characters, such as spaces.
o	Valid characters are: 200 characters.
o	Valid characters are: 0-9, a-z, A-Z, and # $ . \ - (hyphen) _ (underscore)
o	Make sure that you don't have any duplicated names.

![image](https://user-images.githubusercontent.com/36343326/175043374-999d68a9-f23b-46ed-87b5-90dd5bf08e8e.png)

### Create/Select a Dataset 

1. On the **Create dataset** page:

   - For **Dataset ID**, enter a unique dataset name.

   - For **Data location**, choose a geographic [location](https://cloud.google.com/bigquery/docs/locations) for the dataset. After a dataset is created, the location can't be changed.

     **Note:** If you choose `EU` or an EU-based region for the dataset location, your Core BigQuery Customer Data resides in the EU. Core BigQuery Customer Data is defined in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#13-google-bigquery-service).

     

   - For **Default table expiration**, choose one of the following options:

     - **Never:** (Default) Tables created in the dataset are never automatically deleted. You must delete them manually.

     - **Number of days after table creation:** This value determines when a newly created table in the dataset is deleted. This value is applied if you do not set a table expiration when the table is [created](https://cloud.google.com/bigquery/docs/tables#create-table).

       **Note:** If your project is not associated with a billing account, BigQuery automatically sets the default table expiration for datasets that you create in the project. You can specify a shorter default table expiration for a dataset, but you can't specify a longer default table expiration.

   - Click **Create dataset**.

![image](https://user-images.githubusercontent.com/36343326/175043003-899fdd93-d535-4804-b341-e49410653217.png)

To access your data source, you need to assign managed identity to Metrics-Advisor-for-Equipment. [How to assign role to a resource](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/managed_identity.md)

Click **Load** to complete the creation, then you can find the created dataset.

You've ingested your dataset, and you've reviewed any issues with the job, the files, or the sensors. You've also decided which sensors are providing the data that will be used to train your model. Now it's time to move forward with creating the model.

First, you'll specify the details of your model, such as its training time range, advanced settings.

![image](https://user-images.githubusercontent.com/36343326/175045723-4cb8bc63-bf87-4748-ae04-f790e0f805d6.png)

When selecting training time range, you'll need to configure your input data. During that process, you'll make decisions about the balance between your training dataset and your evaluation dataset, and whether or not to use data labels.

Under training time range-include, use the timepickers to select the training dates and time that you want to include in your model.
Under training time range-exclude, use the timepickers to select the training dates and time that you want to exclude in your model.

Optionally, customize your advanced settings. 
•	Sliding Window – How many data points are used to determine anomalies. An integer between 28 and 2,880. The default value is 300. 
•	Missing data Filling Method – we will automatically fill in missing data. Options are Linear, Previous, Subsequent, and Customized, and the default value is Linear.
•	However, if too much original data is missing, it might affect your results.

Choose **Create**.
## Next steps

Starting the training process

The **Model deatils** page gives you a chance review model details such as the name, the dataset, or training time range.


- [Training](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/training.md)
