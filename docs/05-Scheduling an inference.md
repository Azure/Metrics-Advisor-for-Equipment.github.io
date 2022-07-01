## Scheduling inference
After you create a model, you can use it to monitor your asset in real-time. To use your model to monitor your asset, you do the following.

## 1. Create an near real time inference

When the model status is completed, click the button to create a inference. 
![image](https://user-images.githubusercontent.com/36343326/176591157-ca84e705-aead-420e-990d-590f925ef756.png)

![image](https://user-images.githubusercontent.com/36343326/176591110-d887bd68-3241-43a3-8b6d-6f557bbc1f2a.png)



​             

## 2. Set alert configuration

Set alert configuration, specify alert name and sensitivity, and  inference snoozing windows.
![image](https://user-images.githubusercontent.com/36343326/176591239-1aab9a06-0d90-4d13-8f2c-37edab1b1d92.png)

Select or create new hooks for alert.

![image](https://user-images.githubusercontent.com/36343326/176645158-90e62e49-b68a-4678-bfe1-65ed9661b770.png)

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| Snoozing window | If there is an alert has been triggered, for the selecting snoozing time, alert will not be triggered no matter whether there is an anomaly. |
| Sensitivity     | From 1 ~ 100, to define detector's sensitivity. The bigger the more sensitive to anomalies. |

## 3. Inference parameters

Specify the name for the inference and the time period that your model performs inference on the data coming from your pipeline.
For the dataset, select or create an inference dataset.
 
![image](https://user-images.githubusercontent.com/36343326/176644652-a9e9993b-6381-461d-ab04-7397c6663bff.png)


## 4. Use existing inference

If users already created some real time inference which are running in other models, users could reuse this inference id into a new trained model to do inference.  	

Select from existing real-time inferences by inference name and Metrics Advisor for Equipment will prefill the detection settings    (sensitivity and Snoozing window are all used existing inference and not allowed any change) in the portal and trigger inference starting from the current timestamp (None of the information for the selected inference is editable in this step).
![image](https://user-images.githubusercontent.com/36343326/176644500-84af22bd-370d-4e37-9d2e-aef42e21bea3.png)
  

                                             
![image](https://user-images.githubusercontent.com/36343326/176591367-fe6aa6e0-11a7-4854-aa98-74e79bc13c41.png)



![image](https://user-images.githubusercontent.com/36343326/176591438-dfbad83b-c300-41c1-a692-de23ce6c99b3.png)



## 5. Set a replay

After a model is doing real time inference, users could choose to schedule a replay. This will trigger an backfill on your selected timestamp immediately to fix a failed inference or to override the existing data.

Schedule replay/backfill for an existing real-time inference.
Select start date and time and Select end date and time.
![image](https://user-images.githubusercontent.com/36343326/176645839-c3fe65b1-ad9f-4211-8fc7-30ba96ab5c3d.png)

Replay is re-triggered only on selected range   .

## 6. Manage inference schedules

- **Setting inference as inactive**

This will halt the inference process.

From the Model details, under inference tab, choose **inactive.**

- **Setting inference as active**

This will resume a stopped inference schedule.
From the Model details, under inference tab, choose **active**.

- **Deleting an inactive inference**

From the Model details, under inference tab, choose **Delete**.



## 7. Inference detail

Starting the inference process. Click the **model name**, then the **Inference detail** tab gives you a chance review inference details such as the inference name, the dataset, and inference start time.

There are two kinds of inference status.

| status   | Description                                     |
| -------- | ----------------------------------------------- |
| Active   | Inference is in processing.                     |
| Inactive | Inference is paused, you can restart inference. |
| Inactive | Inference is failed for some reason.            |

You can click the **View details** button for the error messages when you find the training inference status gets to **Inactive**.



> **_NOTE:_** 
