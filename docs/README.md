# Metrics Advisor for Equipment (private preview)🌞

## ⭐Introduction

Metrics Advisor for Equipment is a new product feature under the Azure Metrics Advisor service. While the existing Metrics Advisor service targets AIOps use cases, Metrics Advisor for Equipment is designed to provide Predictive Maintenance for critical physical assets (e.g., oil rigs, automotive engines, aircraft) thru multivariate anomaly detection AI capabilities. After users train Metrics Advisor for Equipment models with their historical equipment sensor data, they can initiate real-time equipment health monitoring, receive alerts when the models detect anomalous patterns, and determine the best actions to prevent potential losses as early as possible. Specifically, Metrics Advisor for Equipment’s ability to scale, outstanding AI prediction accuracy, and low cost to implement and maintain are perceived as the core value drivers by our customers.


## ⭐Metrics Advisor for Equipment capabilities

If your goal is to detect system-level anomalies from a group of time series data, use multivariate anomaly detection. Particularly when any individual time series won't tell you much, and you have to look at all signals (a group of time series) holistically to determine a system-level issue. For example, you have an expensive physical asset like turbines, equipment on an oil rig, or milk drier. Each of these assets has tens or hundreds of different types of sensors. You would have to look at all those time series signals from those sensors to decide whether there is a system-level issue. Also, if your scenario has keywords like predictive maintenance and equipment health, then the multivariate feature will likely be a great fit.

![image-20220714175904958](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/image-20220714175904958.png)

## ⭐Value propositions

- Easy for use✔️: No data science knowledge is needed; users can leverage no code experience to create models and set up inferencing and alert with a few clicks; customers and partners can build this AI capability into their own solutions.
- Scalability✔️: Multivariate Metrics Advisor can be used across 300 pieces of equipment and sensors worldwide.
- Cost Effectiveness✔️: Compared with a custom build model, significantly lower the model building cost and shorten the time to market. You don't need to have a few data scientists building and tuning models for a few weeks and then go to production. Instead, the whole process can be done in hours instead of days or weeks. Multivariate Metrics Advisor is priced based on usage, so training and inferencing can be set up and automated for cost-effective model deployment.
- Accuracy✔️: State-of-the-art AI model created by Microsoft Research and AI platform data scientists. While not all equipment issues can be seen in the data, Multivariate Metrics Advisor can find critical abnormal equipment behavior with best-in-class detection algorithms and multiple signals analyzed in a group as opposed to being watched individually. Dependencies and inter-correlations between signals have now been accounted for.

## ⭐How does Metrics Advisor for Equipment work

To build and use an anomaly detection model with Metrics Advisor for Equipment, you need to go through the following steps:

1. [Setting up your Azure account and getting started with Metrics Advisor studio](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/01-Setting%20up%20your%20Azure%20account.md).
2. [Preprocessing your data](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/02-Preprocessing%20your%20data.md).
3. [Creating a model and dataset](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/03-Creating%20a%20model%20and%20dataset.md).
4. [Creating an evaluation and reviewing evaluation results](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/04-Creating%20an%20evaluation%20and%20reviewing%20evaluation%20results.md).
5. [Scheduling inference](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/05-Scheduling%20an%20inference.md).
6. [Reviewing inference results](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/06-Reviewing%20inference%20results.md).
7. [Configuring alerts and getting notifications using a hook](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/07-Configure%20alerts%20an%20get%20notifications%20using%20a%20hook.md).
8. [Quota](https://github.com/Azure/Metrics-Advisor-for-Equipment/blob/main/docs/08-Quota.md).
8. Best Practice.

The Metrics Advisor for Equipment will help you streamline steps 3 to 7. 

## ⭐Support

Product-related issues (e.g. bugs, feature requests) can be created in the [IcM]( https://portal.microsofticm.com/imp/v3/incidents/create?tmpl=72q3D3).

Maintainer: Jinruishao@microsoft.com



## Other references

* Reference architecture of building predictive maintenance with Metrics Advisor for Equipment
* Metrics Advisor for Equipment: [Metrics Advisor for Equipment](https://ma-adel-dev.azurewebsites.net/)
* Anomaly Detector: [Anomaly Detector Doc](https://docs.microsoft.com/en-us/azure/cognitive-services/anomaly-detector/)
* MVAD Blog: [Introducing Multivariate Anomaly Detection](https://techcommunity.microsoft.com/t5/azure-ai/introducing-multivariate-anomaly-detection/ba-p/2260679)
* MVAD Paper: [Multivariate time series Anomaly Detection via Graph Attention Network](https://arxiv.org/abs/2009.02040)
