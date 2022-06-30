# Reviewing inference results

## 1. Use the visualization page

On the visualization main page you'll find your list of inference, both active and inactive. 

Click **view details**

On the right panel detail page you'll find details about the inference summaries. You'll also find alert configurations about the inference itself.

![image](https://user-images.githubusercontent.com/36343326/175203452-7422b3d6-8cda-4df7-ba3c-22d0e4714260.png)

At the top, Equipment anomalies and health trend means the results from the most recent inference run. These results provide information about anomalous behavior that occurred over the past 300 points. 

Use the slider to zoom in on a particular event.

Click on a particular event (red bar) to view details about it.

After you click on a particular event, the Event details tab indicates which sensors contributed the most to that event.

In this page, anomaly region is colored in red. You can find the anomaly score of each series by putting your mouse on a specific time stamp.

![image](https://user-images.githubusercontent.com/36343326/175231102-13b8359d-4170-4c67-a62e-bf01c02171fb.png)





## 2. Top 5 contributors

Users can select top 5 contributors at one time from dropdown. The top contributor raw value chart will hide/mask the unselected one.

for contribution score color scale:

1. 0<x<=25%: lightest

2. 25%<x<=75%: medium

3. 75%<x<=100%: darkest

   

   > **_NOTE:_**  Metrics Advisor for Equipment will pull 300 data points for each variable when users clicked on an anomalous point, show top 5 contributors by default.
