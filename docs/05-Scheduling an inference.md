# ⭐Scheduling a streaming inference

After you create a model, you can use it to monitor your asset in streaming. To use your model to monitor your asset, you do the following.

## 1. Schedule a streaming inference

When the model status is completed, click the button to schedule a streaming inference to start collecting data and detecting anomalies.

![image](https://user-images.githubusercontent.com/36343326/176591157-ca84e705-aead-420e-990d-590f925ef756.png)

![image](https://user-images.githubusercontent.com/36343326/176591110-d887bd68-3241-43a3-8b6d-6f557bbc1f2a.png)

## 2. Set alert configuration

Set alert configuration, specify alert name and sensitivity, and alert correlation and suppression.
![image-20220715155849989](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/image-20220715155849989.png)

Select or create new hooks for alert.

![image-20220715160532687](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/image-20220715160532687.png)

| Parameter                         | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| Alert Correlation and Suppression | Correlated anomalies if they occur within [x] data points of each other.<br />Send one alert for correlated anomalies.<br/>Send an alert for each anomaly: get notifications for new anomalies by receiving alerts at hooks. |
| Sensitivity                       | From 1 ~ 100, to define detector's sensitivity. The bigger the number the more sensitive to anomalies. Set a lower sensitivity to get notified only when severe anomalies are detected. Set a higher sensitivity to detect anomalies that are less severe. |

## 3. streaming Inference parameters

Specify the name for the inference and the time period that your model performs inference on the data coming from your pipeline.

` Inference Start time`: This start time can't be in the past. The first timestamp equal to or greater than the start time given will be used. Your data source must have data at the specified start time and the number of data points available must equal to or greater than your training sliding window (model_name’s sliding window = xxx).

`Data delay Offset` (this is an optional field): the amount of time (in seconds) you expect the data to be delayed for inference. For example, your source data comes every 5 minutes, so by default (i.e., data delay offset In Seconds = 0) the inference schedule assumes that records with a timestamp of 01:30:00 will be ready for inference by 01:35:00, records with a timestamp of 01:35:00 will be ready at 01:40:00, and so on. If you expect a 10-minute data delay (i.e., data delay offset In Seconds = 600), then the scheduler will inference records with a timestamp of 01:30:00 at 01:45:00, inference records with a timestamp of 01:35:00 at 01:50:00, and so on.

For the dataset, select or create an inference dataset.



![image-20220715160559270](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/image-20220715160559270.png)

## 4. Update a paused inference

If users already created a streaming inference which is running in other models, users could replace the trained model for a paused inference. Previous data will be kept and anomalies that were detected with the old model will still visible next to newly detected anomalies in the same inference data. Updating the model is only recommended if there weren't any major differences in the training parameters.

:warning: If an inference isn't listed here, make sure to pause it first. The inference will restart and be streaming immediately after updating.


![image-20220715160627676](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/image-20220715160627676.png)

![image](https://user-images.githubusercontent.com/36343326/176591367-fe6aa6e0-11a7-4854-aa98-74e79bc13c41.png)

![image](https://user-images.githubusercontent.com/36343326/176591438-dfbad83b-c300-41c1-a692-de23ce6c99b3.png)

## 5. Set a replay

After a model is doing streaming inference, users could choose to schedule a replay. This will trigger a backfill on your selected timestamp immediately to fix a failed inference or to override the existing data.

Replay: overwrite the data in a historical time range by running the inference with its current settings.

A max of 2000 data points can be replayed. For example, with a data frequency interval of 1 minute, you can replay a time range of about 1 day. 

Schedule replay/backfill for an existing streaming inference.
Select start date and time and Select end date and time.

The current replay must finish before creating a new one.Wait until the evaluation finishes before creating a replay. ![image](https://user-images.githubusercontent.com/36343326/176645839-c3fe65b1-ad9f-4211-8fc7-30ba96ab5c3d.png)

Replay is re-triggered only on selected range.

## 6. Inference detail

Starting the inference process. Click the **model name**, then the **Inference detail** tab gives you a chance review inference details such as the inference name, the dataset, and inference start time.

There are three kinds of inference status. 

| status       | Description                                              |
| ------------ | -------------------------------------------------------- |
| Active       | Inference is in processing.                              |
| User pause   | Inference is paused by users, you can restart inference. |
| System pause | Inference is failed for some reason.                     |

There are three kinds of actions for  streaming inference. 

- **Pause**

This will halt the inference process. You could stop the streaming inference to stop incurring cost. From the Model details, under inference tab, choose **restart.**

- **Restart**

This will resume a stopped inference schedule.From the Model details, under inference tab, choose **Pause**.

- **Deleting an paused inference**

When you don’t have any more use for your streaming inference,  you can delete a stopped streaming inference by choosing **Delete**.

You can click the **View details** button for the error messages when you find the training inference status gets to **Inactive**.
