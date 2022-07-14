# ⭐Preprocessing your data

Multivariate industrial time-series data can be challenging to deal with. This article will show you how to preprocess your data to Metrics Advisor for equipment.

## 1. Data Storage

**SQL Databases: **put metrics in a big table,have an index on timestamp.
**Cons:**

- Atomicity, consistency, isolation, durability (ACID) creates a large amount of overhead.

- Unless you create a new table periodically, inserts will become much slower.

**Pros:**

- Aggregations, groupings etc. can be useful.

## 2. Data format requirements

- One table/ file per asset.
- All sensors from that asset are represented in that one file/table.

## 3. Data schema requirements

Metrics Advisor for equipment uses your data following the steps below:

- to train a model
- to evaluate a model
- to conduct a near real time inference

Metrics Advisor for equipment accepts tables with only three columns:

- The first column headers of the file are a `Timestamp` that indicates the date and time. The timestamp column should contain datetime values in the yyyy-MM-ddTHH:mm:ss format and conform to ISO 8601. Make sure that the timestamp column is the one furthest to the left in your file. 
- The second column headers contain the `Variable name`.The variable name column should contain the name of the variable for each data point
- The third column headers show the  `Variable value`.The value column should contain numeric values.

| Timestamp     | Sensor  name | Sensor  value |
| ------------- | ------------ | ------------- |
| 1/1/2020 0:05 | Sensor 1     | 2.0456        |
| 1/1/2020 0:10 | Sensor  2    | 6.4948        |
| 1/1/2020 0:15 | Sensor  1    | 4.2938        |
| 1/1/2020 0:20 | Sensor  2    | 4.3894        |
| 1/1/2020 0:25 | Sensor  1    | 5.4098        |

The easiest way to prevent problems with column headers is to take the following precautions:
o	Make sure your column headers don't include any invalid characters, such as spaces.
o	Character length limit: 200 characters.
o	Valid characters are: 0-9, a-z, A-Z, and # $ . \ - (hyphen) _ (underscore)
o	Make sure that the timestamp column is the one furthest to the left in your CSV file.
o	Make sure that you don't have any duplicated column headers.

## 4. Data quality

Your dataset should contain time-series data that's generated from an industrial asset such as a pump, compressor, motor, and so on. Each asset should generate data from one or more sensors.The data that Metrics Advisor for Equipment uses for training should be representative of the condition and operation of the asset. Making sure that you have the right data is crucial.
We recommend that you work with a Subject Matter Expert (**SME**). A SME can help you make sure that the data is relevant to the aspect of the asset that you're trying to analyze. We recommend that you remove unnecessary sensor data. With data from too few sensors, you might miss critical information. With data from too many sensors, your model might overfit the data and it might miss out on key patterns.

#### Use these guidelines to choose the right data:

- **Missing data: **In general, the missing value ratio of training data should be under 20%. Too much missing data may end up with automatically filled values (usually linear values or constant values) being learned as normal patterns. That may result in real (not missing) data points being detected as anomalies. Metrics Advisor for Equipment automatically fills in missing data (known as imputing). It does this by forward filling previous sensor readings. However, if too much original data is missing, it might affect your results.
- **Data granularity**: Ensure each variable has at most one data point within each interval. For example, suppose that data from some sensors is being recorded every 1 minute and other sensors are recording every 5 minutes. In this case, set the data granularity to an interval of 1 minute. If your data granularity unit is minute, make sure that your data granularity is a multiple or factors of 60. 

## 5. Data quantity

- **Data size:** Although Metrics Advisor for Equipment can ingest more than 50 GB of data, it can use only 7 GB with a model. Factors such as the number of sensors used, how far back in history the dataset goes, and the sample rate of the sensors can all determine how many measurements this amount of data can include.
- **Minimum number of data points to train a model:** The empirical rule is that you need to provide **15,000 or more data points (timestamps) per variable** to train the model for good accuracy.  However, in cases when you're not able to collect that much data, we still encourage you to experiment with less data and see if the compromised accuracy is still acceptable.
- **Minimum number of data points to batch inference:** At most 20000, at least 12 sliding window length.
- **Minimum number of data points to near real time inference:** At most 2880, at least 1 sliding window length. Detecting timestamps: From 1 to 10.
