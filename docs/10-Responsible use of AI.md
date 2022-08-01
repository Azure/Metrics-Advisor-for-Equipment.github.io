# ⭐Responsible Use of AI

## Use case of Metrics Advisor for Equipment

### 1. Recommended use case

**Monitoring IoT data from sensors and predictive maintenance**: Sensor data read from IoT sensors that are deployed on factory floors, production lines, oil rigs, and pipelines, or even cars and drones could be analyzed and monitored with Anomaly Detector. Anomalies detected from the data might indicate an anomalous state of the machinery. The application you build can inform human reviewers, allowing them to take potential maintenance actions before a bigger problem arises.

### 2. Considerations when choosing a use case

* In use cases with potential to impact the physical safety of human beings, include human review of outputs prior to any decision regarding operations. Examples of such use cases include monitoring and detecting an anomalous state in the performance of machinery on factory floors or in production lines.
* Don’t use Anomaly Detector for decisions that may have serious adverse impacts: Examples of such use cases include health care scenarios like monitoring heartbeat or blood glucose levels. Decisions based on incorrect output could have serious adverse impacts. Additionally, it is advisable to include human review of decisions that have the potential for serious impacts on individuals.
* Don't use Anomaly Detector in workspace monitoring on individuals. Because Anomaly Detector has no qualitative assessment capabilities, it is not suitable for monitoring or evaluating human activity, such as in the workplace. We do not recommend that it be used in such a way. In addition, workplace monitoring may not be legal within your jurisdiction.


## Characteristics and limitations of use

This section contains our recommendations intended for customers when they've started piloting or are planning to integrate the service into their solutions.

### 1. Subject matter expertise (SME) involvement throughout the process

This system does not accept labeled data from customers during model training, but you can use the model output (score, severity) to fine-tune detection results according to your specific needs. Humans can check the detection results, top contributing variables, and correlated variables to ensure the service is generating expected results. This human review is **required** for any decision being made. 

Our model only output data insights that aim at complementing human knowledge in decision making or situation diagnosing, so **the raw output should not be directly used for any automated decision-making process/pipeline** (i.e., without any human oversight or post-processing). 

Here is a high-level workflow that indicates when SMEs should be involved and their core responsibilities in those steps.  
![Subject Matter Expertises (SMEs) are highly recommended to be involved in feature selection, model evaluation, and ongoing alert monitoring processes.](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/High_level_workflow_RAI.jpg "Recommended pilot and production workflow")


### 2. Variable selection

Choosing the right input data is crucial to the success of using this AI system for predictive maintenance. It may take customers multiple trial and error iterations to find the right combination of inputs. Thus we make no claims to guarantee results, success is highly dependent on the relevancy of your data to the equipment issues.

Some of our successful customers even set up an experimentation pipeline to continuously iterate thru feature selection and feature engineering in order to improve the model performance


### 3. Data quality

As the model learns normal patterns from historical data, the training data should represent the overall normal state of the system. It's hard for the model to learn these types of patterns if the training data is full of anomalies. An empirical threshold of abnormal rate is 1% and below for good accuracy.

**In general, the missing value ratio of training data should be under 20%.** Too much missing data may end up with automatically filled values (usually linear values or constant values) being learned as normal patterns. That may result in real (not missing) data points being detected as anomalies.

For more details on data quality requirements, please refer to [Preprocessing your data](https://azure.github.io/Metrics-Advisor-for-Equipment/docs/02-Preprocessing%20your%20data.html).


### 4.  Streaming inference data volume

The underlying model of this AI system has millions of parameters. It needs a minimum number of data points to learn an optimal set of parameters. **The empirical rule is that you need to provide 15,000 or more data points (timestamps) per variable to train the model for good accuracy.** In general, the more the training data, better the accuracy. However, in cases when you're not able to accrue that much data, we still encourage you to experiment with less data and see if the compromised accuracy is still acceptable.

When setting up an inference schedule for continuous real-time monitoring, you need to ensure that the source data file contains just enough data points. The minimun data volume required in this case should be equal to or greater than (3 * `slidingWindow`) + (the number of timestamps to be detected). 
* `slidingWindow`: Control how many previous data points get used to determine if the next data point is an anomaly. The default value is 300, but you can choose an integer between 28 and 2,880. This is set for when you trigger a model training job. 

For example, during streaming inference if you'd like to on ONE new timestamp, the data file could contain only the leading slidingWindow plus ONE data point; then you could move on and create another zip file with the same number of data points (3 * `slidingWindow` + 1) but moving ONE step to the "right" side and submit for another inference job.

Any data at timestamps beyond or "earlier" the leading `slidingWindow` won't impact the inference result at all and may only cause performance downgrade. If the inference schedule cannot fetch the amount of data points required (e.g.., during to missing data), you may receive a `NotEnoughInput` error and detection results will not be returned. 


### 5. Data recency

Data drifting is a common pitfall that would impact the model’s anomaly detection results. **Thus, users are highly recommended to retrain their models regularly to ensure that model keep up with the recent data patterns.**

The optimal retraining frequency could differ by data granularity, equipment types, feature combinations, customers’ own success criteria, we’d recommend users to experiment different retraining cycles and have the SMEs evaluate the model performance.


### 6. Other limitations
* **Highly variable sensors/equipment**: Currently our model may not be suitable for cases where the sensor data pattern is highly variable because our model requires enough data to learn the pattern in order to make predictions.

* **High frequency data**: In the past, we have found that our model tends to perform better when the input data’s granularity is greater than 1 sec. When the raw data is at low granularity – like one data point per second or even sub-second – a common practice is to aggregate (sum/average/sample) it to a higher granularity. 
    * The benefits of aggregation:
        * Easier alignment to even distribution on time, which is a protocol of the API input.
        * Increased tolerance of random noise.
        * Fewer data points and fewer API transactions.
    * The downside of aggregation: subtle changes within lower granularity are not considered, which might lead to missing important anomalies.


## Other references
* [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)
* [Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)
* [Identify principles and practices for responsible AI](https://docs.microsoft.com/en-us/learn/paths/responsible-ai-business-principles/)
* [Microsoft principles for developing and deploying facial recognition technology](https://blogs.microsoft.com/wp-content/uploads/prod/sites/5/2018/12/MSFT-Principles-on-Facial-Recognition.pdf)
