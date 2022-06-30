# Reviewing inference results

## 1. Using the visualization page

On the visualization main page you'll find your list of inference, both active and inactive. 

Click **view details**

![image](https://user-images.githubusercontent.com/36343326/175203452-7422b3d6-8cda-4df7-ba3c-22d0e4714260.png)

On the right panel detail page you'll find details about the inference summaries. You'll also find alert configurations about the inference itself.

At the top, Equipment anomalies and health trend means the results from the most recent inference run. These results provide information about anomalous behavior that occurred over the past week. 

In this page, anomaly region is colored in red. You can find the anomaly score of each series by putting your mouse on a specific time stamp.

![image](https://user-images.githubusercontent.com/36343326/175231102-13b8359d-4170-4c67-a62e-bf01c02171fb.png)


Use the slider to zoom in on a particular event (red bar). Click on a particular event (red bar) to view details about it.

After you click on a particular event, the event details tab indicates which sensors contributed the most to that event.

## 2. Make sense of inference results

### Score and severity

Multivariate anomaly detection provides “severity” and “score” as part of the output from inference. How should I read this? Score is the raw output from the algorithm, while severity is derived from the score. And users are expected to use one of them to filter out low impact anomalies. 

### 30,000-foot view on how multivariate anomaly detection works to help you interpret the results

Multivariate analysis assumes that there is hidden relationship between any two signals from the multivariate signal set, and statistically those relationships (correlation) are stable across time. If this stable correlation varies significantly, then there is high chance that some anomaly happens. Through the deep neural network, those hidden relationships are identified between signals and used as one of the inputs for the decision of anomaly judgement. The algorithm also considers the historical value pattern in time dimension, and automatically identify the value anomaly that does not conform to historical pattern.

To sum it up, the correlation between signals and value anomalies in time domain are both considered by the algorithm and multivariate anomalies are determined holistically with the above-mentioned considerations.
