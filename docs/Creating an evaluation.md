# Creating an evaluation and reviewing evaluation results

If you've used part of your dataset for training and the other part for evaluation, you can start evaluate the model's performance after finishing the training. You can also select a different dataset for model evaluations.

If you've provided Metrics-Advisor-for-Equipment with label data, you can see how the model's predictions compare to the label data. 

Metrics-Advisor-for-Equipment also reports the results where it incorrectly identified an abnormal behavior event in the label data. The label data that you provide when you create a dataset has a time range for abnormal equipment events. You specify the duration of the abnormal events in the label data. In the evaluation data, the model used by Metrics-Advisor-for-Equipment could incorrectly identify abnormal events outside of the equipment range. You can see how often the model identifies these events when you evaluate the model's performance.

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
