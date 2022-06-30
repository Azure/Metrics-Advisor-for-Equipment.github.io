## Scheduling inference
After you create a model, you can use it to monitor your asset in real-time. To use your model to monitor your asset, you do the following.

## 1. Create an near real time inference

When the model status is completed, click the button to create a inference. 
![image](https://user-images.githubusercontent.com/36343326/176591157-ca84e705-aead-420e-990d-590f925ef756.png)

![image](https://user-images.githubusercontent.com/36343326/176591110-d887bd68-3241-43a3-8b6d-6f557bbc1f2a.png)


Set alert configuration, specify alert name and sensitivity, inference snoozing windows.
![image](https://user-images.githubusercontent.com/36343326/176591239-1aab9a06-0d90-4d13-8f2c-37edab1b1d92.png)

Select hooks for alert.


![image](https://user-images.githubusercontent.com/36343326/176591270-7127defa-46d1-4b03-8c02-819f14358be9.png)
             


## 2. Set alert configuration

| Parameter             | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| Snoozing window       | If there is an alert has been triggered, for the selecting snoozing time, alert will not be triggered no matter whether there is an anomaly. |
| Detection sensitivity | From 1 ~ 100, to define detector's sensitivity. The bigger the more sensitive to anomalies. |



### 3. inferernce parametrers

Specify the name for the inference and the time period that your model performs inference on the data coming from your pipeline.
For the dataset, select or create an inference dataset.


## 4. Managing inference schedules

- **Setting inference as inactive**

This will halt the inference process.

From the Model details, under inference tab, choose **inactive.**

- **Setting inference as active**

This will resume a stopped inference schedule.
From the Model details, under inference tab, choose **active**.

- **Deleting an inactive inference**

From the Model details, under inference tab, choose **Delete**.



## 5. Understanding the inference process      
Metrics-Advisor-for-Equipment looks for the component name (which can be the name of an asset or a sensor).Once the component name is found in the file name, Metrics-Advisor-for-Equipment looks at the time stamp in the timestamps column. The timestamp in the file name must be within the range of time that your scheduler is running. For example, if the scheduler is running every 5 minutes, then at 9:05, Metrics-Advisor-for-Equipment will look for any files that have a timestamp from 9:00 to 9:05. Any files with timestamps outside this range will be ignored for the inference run.

![image](https://user-images.githubusercontent.com/36343326/176591345-dbb3ad25-a2cc-4be1-b8e7-1a3b1e7bb66c.png)

![image](https://user-images.githubusercontent.com/36343326/176591367-fe6aa6e0-11a7-4854-aa98-74e79bc13c41.png)

![image](https://user-images.githubusercontent.com/36343326/176591416-600ab496-fa7d-4423-bb55-a577512b9bcb.png)
![image](https://user-images.githubusercontent.com/36343326/176591438-dfbad83b-c300-41c1-a692-de23ce6c99b3.png)
![image](https://user-images.githubusercontent.com/36343326/176591452-52f98c0e-2f93-44c7-b0f2-e7bc32a0163c.png)



