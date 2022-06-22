# Create a model

**Models** is the place where you can create a new model.

Click **Create a new model**.
![image](https://user-images.githubusercontent.com/36343326/175043087-24453360-a2a6-41db-85c9-cee02a0d1e5c.png)


To create a model, you should fill a model name.
![image](https://user-images.githubusercontent.com/36343326/175043374-999d68a9-f23b-46ed-87b5-90dd5bf08e8e.png)


Several parameters should be filled for multivariate anomaly detection application.
![image](https://user-images.githubusercontent.com/36343326/175043003-899fdd93-d535-4804-b341-e49410653217.png)


> 
> - To access your data source, you need to assign managed identity to Metrics-Advisor-for-Equipment. [How to assign role to a resource](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/managed_identity.md)

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
