# Best practices with Metrics-Advisor-for-Equipment
We highly recommend that you consult a subject matter expert (SME) when setting up Metrics Advisor for Equipment to monitor your equipment. 

There are three key pillars essential to setting up Metrics Advisor for Equipment for the best possible results:
## 1. Choosing the right data
Your dataset should contain time-series data that's generated from an industrial asset such as a pump, compressor, motor, and so on. Each asset should be generating data from one or more sensors. The data that Metrics Advisor for Equipment uses for training should be representative of the condition and operation of the asset. Making sure that you have the right data is crucial.
We recommend that you work with a SME. A SME can help you make sure that the data is relevant to the aspect of the asset that you're trying to analyze. We recommend that you remove unnecessary sensor data. With data from too few sensors, you might miss critical information. With data from too many sensors, your model might overfit the data and it might miss out on key patterns.

-Use these guidelines to choose the right data:

-Use only numerical data – Remove nonnumerical data. Metrics Advisor for Equipment can't use non-numerical data for analysis.

-Use only analog data – Use only analog data (that is, many values that vary over time). Using digital values (also known as categorical values, or values that can be only one of a limited number of options), such as valve positions or set points, can lead to inconsistent or misleading results.

-Use data for the relevant component or subcomponent – You can use Lookout for Equipment to monitor an entire asset (such as a pump) or just a subcomponent (such as a pump motor). Determine where your downtime issues occur and choose the component or subcomponent that has the greater effect on that.

When formatting a predictive maintenance problem, consider these guidelines:

-Data size – Although Metrics Advisor for Equipment can ingest more than 50 GB of data, it can use only 7 GB with a model. Factors such as the number of sensors used, how far back in history the dataset goes, and the sample rate of the sensors can all determine how many measurements this amount of data can include. This amount of data also includes the missing data imputed by Lookout for Equipment.

-Missing data – Metrics Advisor for Equipment automatically fills in missing data (known as imputing). It does this by forward filling previous sensor readings. However, if too much original data is missing, it might affect your results.

-Sample rate – Sample rate is the interval at which the sensor readings are recorded. Use the highest frequency sample rate possible without exceeding the data size limit. The sample rate and data size might also increase your ML model training time. Metrics Advisor for Equipment handles any timestamp misalignment.

-Number of sensors – Metrics Advisor for Equipment can train a model with data from up to 300 sensors. However, having the right data is more important than the quantity of data. More is not necessarily better.


## Evaluating the output

After a model is trained, Metrics Advisor for Equipment evaluates its performance on a subset of the dataset that you've specified for evaluation purposes. It displays results that provide an overview of the performance and detailed information about the abnormal equipment behavior events and how well the model performed when detecting those.

We strongly recommend that you use labels for evaluating the model, Metrics Advisor for Equipment reports how many times the model's predictions were true positives (how often the model found the equipment anomaly that was noted within the ranges shown in the labels). 

Metrics Advisor for Equipment also displays this information graphically on a chart that shows the days and events and in a table.

Metrics Advisor for Equipment provides detailed information about the anomalous events that it detects. It displays a list of sensors that provided the data to indicate an anomalous event. This might help you determine which part of your asset is behaving abnormally.

## Consulting subject matter experts
Metrics Advisor for Equipment identifies patterns in the dataset that help to detect critical issues, but it's the responsibility of a technician or subject matter expert (SME) to diagnose the problem and take corrective action, if needed. To ensure that you are getting the right output, we highly recommend that you work with a SME. The SME should help you make sure that you are using the right input data and that your output results are actionable and relevant.
