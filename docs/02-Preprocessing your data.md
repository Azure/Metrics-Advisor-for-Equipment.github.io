# Preprocessing your data

Multivariate industrial time-series data can be challenging to deal with. This article will show you how to preprocess your data to Metrics Advisor for equipment.

## 1. Data format requirements 

Data format should be store all the sensor data in one file/table.

- One table/ file per asset.
- All sensors from that asset are represented in that one file/table.

## 2. Data schema requirements 

Metrics Advisor for equipment uses your data in the following steps:

- to train a model 
- to evaluate a model
- to conduct a near real time inference

Metrics Advisor for equipment accepts tables with only three columns:

- The first column headers of the file are a timestamp that indicates the date and time. 
- The second column headers contain the sensor name. 
- The third column headers show the data value from the sensor.

| Timestamp     | Sensor  name | Sensor  value |
| ------------- | ------------ | ------------- |
| 1/1/2020 0:00 | Sensor 1     | 2.0456        |
| 1/1/2020 0:00 | Sensor  2    | 6.4948        |
| 1/1/2020 0:05 | Sensor  1    | 4.2938        |
| 1/1/2020 0:05 | Sensor  2    | 4.3894        |
| 1/1/2020 0:10 | Sensor  1    | 5.4098        |

**_NOTE:_** Timestamp format : yyyy-MM-ddTHH:mm.

The easiest way to prevent problems with column headers is to take the following precautions:
o	Make sure your column headers don't include any invalid characters, such as spaces.
o	Valid characters are: 200 characters.
o	Valid characters are: 0-9, a-z, A-Z, and # $ . \ - (hyphen) _ (underscore)
o	Make sure that the timestamp column is the one furthest to the left in your CSV file.
o	Make sure that you don't have any duplicated column headers.

