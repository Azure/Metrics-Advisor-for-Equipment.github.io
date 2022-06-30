## Scheduling inference
After you create a model, you can use it to monitor your asset in real-time. To use your model to monitor your asset, you do the following.

## 1. Create an near real time inference

When the model status is completed, click the button to create a inference. 

![image](https://user-images.githubusercontent.com/36343326/175054446-79c3977d-6e18-498f-8622-3ec436c14b8c.png)

Set alert configuration, specify alert name and sensitivity, inference snoozing windows.

Select hooks for alert.

![image](https://user-images.githubusercontent.com/36343326/175054762-521ef174-d2ae-4ba5-8c3e-a249c5431cd3.png)

Specify the name for the inference and the time period that your model performs inference on the data coming from your pipeline.
For the dataset, select or create an inference dataset.

![image](https://user-images.githubusercontent.com/36343326/175054891-c5311013-94c0-4762-b9b3-5353cb442711.png)

## 2. Managing inference schedules

- **Setting inference as inactive**

This will halt the inference process.

From the Model details, under inference tab, choose **inactive.**

- **Setting inference as active**

This will resume a stopped inference schedule.
From the Model details, under inference tab, choose **active**.

- **Deleting an inactive inference**

From the Model details, under inference tab, choose **Delete**.



## 3. Understanding the inference process      
Metrics-Advisor-for-Equipment looks for the component name (which can be the name of an asset or a sensor).Once the component name is found in the file name, Metrics-Advisor-for-Equipment looks at the time stamp in the timestamps column. The timestamp in the file name must be within the range of time that your scheduler is running. For example, if the scheduler is running every 5 minutes, then at 9:05, Metrics-Advisor-for-Equipment will look for any files that have a timestamp from 9:00 to 9:05. Any files with timestamps outside this range will be ignored for the inference run.

