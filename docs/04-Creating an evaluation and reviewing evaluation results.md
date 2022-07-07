# ⭐Creating an evaluation and reviewing evaluation results

One of the most important and subtle parts of anomaly detection happens at the intersection between predicting how a metric should behave, and comparing observed values to those expectations.

## 1. Before Evaluating

After a model is trained, Metrics Advisor for Equipment evaluates its performance on a subset of the dataset that you've specified for evaluation purposes. It displays results that provide an overview of the performance and detailed information about the abnormal equipment behavior events and how well the model performed when detecting those.

**We strongly recommend that you use labels for evaluating the model**, Metrics Advisor for Equipment reports how many times the model's predictions were true positives (how often the model found the equipment anomaly that was noted within the ranges shown in the labels).

Metrics Advisor for Equipment also displays this information graphically on a chart that shows the days and events.

Metrics Advisor for Equipment provides detailed information about the anomalous events that it detects. It displays a list of sensors that provided the data to indicate an anomalous event. This might help you determine which part of your asset is behaving abnormally.

Metrics Advisor for Equipment identifies patterns in the dataset that help to detect critical issues, but it's the responsibility of a technician or subject matter expert (SME) to diagnose the problem and take corrective action, if needed. **To ensure that you are getting the right output, we highly recommend that you work with a SME. The SME should help you make sure that you are using the right input data and that your output results are actionable and relevant.**

## 2. Create an evaluation

If you've used part of your dataset for training and the other part for evaluation, you can start to evaluate the model's performance after finishing the training. You can also select a different dataset for model evaluations.

You can use the following procedure and example code to view the models you've created. They also show you how to get information about a model, such as how well it performed.

To view a model:

Go to **Models** and Choose a model and click the model name.

Navigate to **Model details** page and choose **create a evaluation**.

![image](https://user-images.githubusercontent.com/36343326/175050952-b3a5036e-2a48-48f2-92e1-070d54d8e886.png)

## 3.**Evaluation parameters**

In the following image, you need to fill evaluation parameters:

![image](https://user-images.githubusercontent.com/36343326/175051021-6633e3fd-61af-45b1-bcb3-f3c645efa388.png)

## 4. Evaluation Summary

Starting the evaluation process. Click the **model name**, then the **Evaluation result** tab gives you a chance to review evaluation details such as the evaluation name, the dataset, and evaluation time range.

On the evaluation results tab page you'll find your list of evaluations.
Click **Evaluation summary**, you'll find details about the evaluation summaries.

There are three kinds of evaluation status.

| Status    | Description                                  |
| --------- | -------------------------------------------- |
| Running   | Evaluation is in processing.                 |
| Completed | Evaluation is done, you can start inference. |
| Failed    | Evaluation is failed for some reason.        |

You can click the **View details** button for the error messages when you find the Evaluation status gets to **Failed**.

In the example below, equipment anomalies and health trend represents the results from the chosen evaluation run. These results provide information about anomalous behavior that occurred over the evaluation time range.

Use the slider to zoom in on a particular event.

Click on a particular event (red bar) to view details about it.

After you click on a particular event, the Event details tab indicates which sensors contributed the most to that event.

![image](https://user-images.githubusercontent.com/36343326/175233341-e8eda33b-84e8-4e1a-8440-a635cacde7fd.png)

## 5. Upload the label

If you've provided Metrics-Advisor-for-Equipment with label data, you can see how the model's predictions compare to the label data.
![image](https://user-images.githubusercontent.com/36343326/175234568-54d77e0b-926b-4a3a-9f48-01c8d6f3a8fa.png)

Metrics-Advisor-for-Equipment also reports the results where it incorrectly identified an abnormal behavior event in the label data. The label data that you provide when you create a dataset has a time range for abnormal equipment events. You specify the duration of the abnormal events in the label data. In the evaluation data, the model used by Metrics-Advisor-for-Equipment could incorrectly identify abnormal events outside of the equipment range. You can see how often the model identifies these events when you evaluate the model's performance.

**After clicking on “Upload label”, upload ONE csv file with label data.**

**Format requirement:**

Event_start_time (timestamp format MUST be the same as your evaluation data)-Event_end_time (timestamp format MUST be the same as your evaluation data)

File size limit: 1MB

**Advanced settings:**

Users should modify the detection configuration to let Metric Advisor for Equipment's predicted anomalies match with their labels as much as possible
When users try different numbers for sensitivity, the anomaly red points on the anomaly score trend visuals will change accordingly.

- `Data granularity`: automatically detected on the backend;
- `Sensitivity`: choose an integer between 1-100, higher sensitivity means more anomalies will show up
- `Snoozing window`: “Do not send out alerts if an alert was already sent in the last ____ min”，different numbers for Snoozing window, the anomaly score trend visuals will change accordingly.

## 6. Anomaly score

Equipment anomalies and health trend means the results from the most recent evaluation run. These results provide information about anomalous behavior that occurred over the past 300 points.

Use the slider to zoom in on a particular event.

Click on a particular event (red bar) to view details about it.

-  `Anomaly score` is the raw output of the model on which the model makes a decision.  `Anomaly score` will have a value from 0-1.78.  `Anomaly score` usually will indicate a anomaly rise or decline respectively.

-  `Anomaly` indicates an anomaly at the current timestamp.

-  `Not Anomaly` indicates the current timestamp is not an anomaly.

![image](https://user-images.githubusercontent.com/36343326/175235792-55d6f4df-5111-4739-8556-e6d46349df43.png)

## 7. Top 5 contributors

After you click on a particular event, the Event details tab indicates which sensors contributed the most to that event. Users can select top 5/10/15 contributors at one time from the dropdown.

- `contributors` is a list containing the contribution score of each variable. Higher contribution scores indicate higher possibility of the root cause. This list is often used for interpreting anomalies as well as diagnosing the root causes.

For contribution score color scale:

1. 0<x<=25%: lightest

2. 25%<x<=75%: medium

3. 75%<x<=100%: darkest

   > **_NOTE:_**  Metrics Advisor for Equipment will pull 300 data points for each variable when users clicked on an anomalous point, and show the top 5 contributors by default.

![image](https://user-images.githubusercontent.com/36343326/175237217-cc591970-c8a5-4c16-8eb4-dbd5ef9cf651.png)

## 7. Download results

Users can download the raw model output. The downloaded file will have the following information:

- Timestamp: timestamps within the evaluation start and end time users defined during evaluation set up.
- is Anomaly: True if an anomaly is detected at the current timestamp
- Score: Raw score from the model
- Severity: Indicates the significance of the anomaly. The higher the severity, the more significant the anomaly)