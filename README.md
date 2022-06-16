# Metrics Advisor for equipment(private preview)

The new Metrics Advisor for equipment feature on Metrics Advisor enables users by easily integrating advanced AI for detecting anomalies from groups of time series signals, without the need for machine learning knowledge or labeled data. This new capability helps you to proactively protect your complex systems such as pumps, Compressors, Motors and turbines from failures.

Imagine 20 sensors from an auto engine generating 20 different signals like rotation, fuel pressure, bearing etc. The readings of those signals individually may not tell you much about system level issues, but together they can represent the health of the engine. When the interaction of those signals deviates outside the usual range, the multivariate anomaly detection feature can sense the anomaly like a seasoned expert. The underlying AI models are trained and customized using your data such that it understands the unique needs of your business. With the new feature, developers can now easily integrate the multivariate time series anomaly detection capabilities into predictive maintenance solutions, AIOps monitoring solutions for complex enterprise software, or business intelligence tools.

## When to use **multivariate** anomaly detection

If your goal is to detect system level anomalies from a group of time series data, use multivariate anomaly detection. Particularly, when any individual time series won't tell you much, and you have to look at all signals (a group of time series) holistically to determine a system level issue. For example, you have an expensive physical asset like turbines, equipment on an oil rig, or a milk drier. Each of these assets has tens or hundreds of different types of sensors. You would have to look at all those time series signals from those sensors to decide whether there is system level issue. Also if your scenario has the keyword like is predicative maintenance, equipment health, then it is likely multivariate feature is a great fit.

## Value propositions

- Easy for use: No data science knowledge needed, users can leverage no code experience to create models and set up inferencing and alert with a few clicks, customers and partners to build this AI capability into their own solutions.
- Scalability: Multivariate Metrics Advisor can be used across 300 pieces of equipment and sensors located across the world.
- Cost Effectiveness: Compared with custom build model, significantly lower the model building cost and shorten the time to market. You don't need to have a few data scientists building and tuning models for a few weeks then go production. Instead, the whole process can be done in hours instead of days or weeks. Multivariate Metrics Advisor is priced based on usage, so training and inferencing can be set up and automated for cost-effective model deployment.
- Accuracy: State of the art AI model created by Microsoft research and AI platform data scientists. While not all equipment issues can be seen in the data, Multivariate Metrics Advisor can find key abnormal equipment behavior with best-in-class detection algorithms and multiple signals analyzed in a group as opposed to being watched individually, dependencies and inter-correlations between signals have now been accounted. 

## Get familiar with new multivariate detection flow

### Prerequisites

1. [Preprocessing your data](https://github.com/Azure/Metrics-Advisor-for-Equipment.github.io/blob/gh-pages/Preprocessing%20your%20data.md).
2. [Create an Azure resource for Metrics Advisor studio](https://go.microsoft.com/fwlink/?linkid=2142156).
3. Login to Metrics Advisor studio and clicked the Adel card to start trying out the service.
4. Create a model and onboard your data.
5. Start training and evaluate your model.
6. Start inferencing and get Inference result & contributor ranking visualization.
7. About alert


## Other references

* Reference architecture of building predictive maintenance with Metrics Advisor's MV feature
* Azure Metrics Advisor: [Azure Metrics Advisor Doc](https://docs.microsoft.com/en-us/azure/cognitive-services/metrics-advisor/)
* Anomaly Detector: [Anomaly Detector Doc](https://docs.microsoft.com/en-us/azure/cognitive-services/anomaly-detector/)
* MVAD Blog: [Introducing Multivariate Anomaly Detection](https://techcommunity.microsoft.com/t5/azure-ai/introducing-multivariate-anomaly-detection/ba-p/2260679)
* MVAD Paper: [Multivariate time series Anomaly Detection via Graph Attention Network](https://arxiv.org/abs/2009.02040)
