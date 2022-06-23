# Best practices with Metrics-Advisor-for-Equipment
Training a machine learning (ML) model can involve inputs from up to 300 sensors, and you can have up to 3000 sensors represented in a single dataset. 
We highly recommend that you consult a subject matter expert (SME) when setting up Metrics Advisor for Equipment to monitor your equipment. 

There are three key pillars essential to setting up Metrics Advisor for Equipment for the best possible results:
## Choosing the right data
Your dataset should contain time-series data that's generated from an industrial asset such as a pump, compressor, motor, and so on. Each asset should be generating data from one or more sensors. The data that Lookout for Equipment uses for training should be representative of the condition and operation of the asset. Making sure that you have the right data is crucial.
We recommend that you work with a SME. A SME can help you make sure that the data is relevant to the aspect of the asset that you're trying to analyze. We recommend that you remove unnecessary sensor data. With data from too few sensors, you might miss critical information. With data from too many sensors, your model might overfit the data and it might miss out on key patterns.


