# Creating an evaluation and reviewing evaluation results

If you've used part of your dataset for training and the other part for evaluation, you can start evaluate the model's performance after finishing the training. You can also select a different dataset for model evaluations.

You can use the following procedure and example code to view the models you've created. They also show you how to get information about a model, such as how well it performed.

To view a model:

Go to **Models** and Choose a model. You can see whether the model is ready to monitor the equipment.

Navigate to **Model deatils** page and choose **create a evaluation**.

![image](https://user-images.githubusercontent.com/36343326/175050952-b3a5036e-2a48-48f2-92e1-070d54d8e886.png)


In the following image, you can see 

![image](https://user-images.githubusercontent.com/36343326/175051021-6633e3fd-61af-45b1-bcb3-f3c645efa388.png)


# Reviewing evaluation results

## Using the evaluation tab

On the evaluation tab page you'll find your list of evaluations. 
Click evaluation summary, you'll find details about the evalution summarys.

![image](https://user-images.githubusercontent.com/36343326/175233341-e8eda33b-84e8-4e1a-8440-a635cacde7fd.png)

At the below, Equipment anomalies and health trend means the results from the chosen evaluation run.These results provide information about anomalous behavior that occurred over the evalution time range.
![image](https://user-images.githubusercontent.com/36343326/175233779-f04dbc0c-b49a-40ff-a49b-b057552ece29.png)

Use the slider to zoom in on a particular event.
Click on a particular event (red bar) to view details about it.
After you click on a particular event, the Event details tab indicates which sensors contributed the most to that event.

•	Data granularity: automatically detected on the backend; 
•	Sensitivity: choose an integer between 1-100
•	Snoozing window (based on time): “Do not send out alerts if an alert was already sent in the last ____ min”
severity = anomaly score / (e - 1)
sensitivity = (1- severity) *100

## Uploading the label
If you've provided Metrics-Advisor-for-Equipment with label data, you can see how the model's predictions compare to the label data. 
![image](https://user-images.githubusercontent.com/36343326/175234568-54d77e0b-926b-4a3a-9f48-01c8d6f3a8fa.png)

Metrics-Advisor-for-Equipment also reports the results where it incorrectly identified an abnormal behavior event in the label data. The label data that you provide when you create a dataset has a time range for abnormal equipment events. You specify the duration of the abnormal events in the label data. In the evaluation data, the model used by Metrics-Advisor-for-Equipment could incorrectly identify abnormal events outside of the equipment range. You can see how often the model identifies these events when you evaluate the model's performance.

After clicking on “Upload label”，	Upload ONE csv file with label data. 
Format requirement:
• Event_start_time (timestamp format MUST be the same as your evaluation data)	event_end_time (timestamp format MUST be the same as your evaluation data) 
•	File size limit: 1MB

If a label csv file was uploaded successfully, Users should see the labeled time periods on the visualization.
![image](https://user-images.githubusercontent.com/36343326/175235792-55d6f4df-5111-4739-8556-e6d46349df43.png)

Users should modify the detection configuration to let Adel's predicted anomalies match with their labels as much as possible
When users try different numbers for sensitivity, the anomaly red points on the anomaly score trend visuals will change accordingly
o	higher sensitivity have more anomalies will show up
•	When users try different numbers for Snoozing window, the anomaly score trend visuals (i.e., “equipment anomalies and health trend” on the right – name of this visual is TBD) will change accordingly. 
o	Larger Snoozing window have more anomalies will share the same Snoozing id



[Open question 2]: raw value time range? (if DS used 2 year of historical data for evaluation, then it's not realistic to pull all – March alignment – show 1 sliding window before and after)
Pull 300 data points for each variable, show top 5 contributors by default
When users clicked on an anomalous point:
•	Allow users to select an integer between 1-30 as the number of contributors to show (as test for optimal number) - UI to notify no more than 30; final alignment: show as drop down for top 5, 10, 15, 20, 25, 30 contributors
•	Show a list of top N contributors for the clicked anomaly point 
o	[Option 1] ranked – horizontal bar chart with bar length = contribution percentage à will not add up to 100%
o	[Option 2] ranked list with contribution percentage shown in numbers
•	Show top N contributor's raw sensor value 
o	Allow users to zoom in to view a smaller time range 
o	Each sensor to be in a separate line chart (x = timestamp, y = sensor raw value) and stack them (*each sensor may have a different data scale so suggest we do not combine them in one chart)
o	For each contributor, if there is a variable with significant Snoozing change AND this variable is not among the top 5 contributors, have a sentence at the bottom to suggest users to also check this variable but we will NOT show the raw value for this variable on UI.
	"Note: we also detected significant change in Feature E's Snoozing with Feature X. Please check Feature X as well. "
o	[future iteration] Plain English explanation for anomalies – similar to UVAD on PBI
o	[future iteration] more insights will be provided for a given sensor 
## Top 5 contributors
Users can select top 5 contributors at one time from dropdown. The top contributor raw value chart will hide/mask the unselected one.
![image](https://user-images.githubusercontent.com/36343326/175237217-cc591970-c8a5-4c16-8eb4-dbd5ef9cf651.png)

for contribution score color scale:
1.	0<x<=25%: lightest
2.	25%<x<=75%: medium
3.	75%<x<=100%: darkest


## Downloading results

Users could download raw model output. The downloaded file will have the following information: 
•	Timestamp: timestamps within the evaluation start and end time users defined during evaluation set up.
•	is Anomaly: True if an anomaly is detected at the current timestamp
•	Score: Raw score from the model
•	Severity: Indicates the significance of the anomaly. The higher the severity, the more significant the anomaly)
Anomaly_contributors_ranks_correlated_variables: contribution score, changedVariables, and SnoozingChanges for ALL variables




