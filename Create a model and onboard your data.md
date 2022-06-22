# Create a model

**Models** is the place where you can create a new model.

Click **Create a new model** to create a model.

![image-20220622145048266](C:\Users\jinruishao\AppData\Roaming\Typora\typora-user-images\image-20220622145048266.png)

To create a model, you should fill a model name.

![image-20220622145141721](C:\Users\jinruishao\AppData\Roaming\Typora\typora-user-images\image-20220622145141721.png)









Several parameters should be filled for multivariate anomaly detection application.

| Parameter                    | Description                                                  |
| ---------------------------- | ------------------------------------------------------------ |
| Application name             | Name of the application instance.                            |
| Application instance name    | Display name of the application instance.                    |
| Hook                         | Name of the hook.                                            |
| Inference frequency          | Frequency for inference.                                     |
| Inference frequency interval | Custom frequency when inference frequency is **Custom**.     |
| Anomaly Detector API         | To use multivariate anomaly detector, you need to create an anomaly detector resource and fill its endpoint. https://azure.microsoft.com/en-us/services/cognitive-services/anomaly-detector/ |
| Align Policy                 | How to align multiple time-series on Timestamps.             |
| Sliding Window               | An optional field, indicates how many history points will be used to determine the anomaly score of one subsequent point. |
| Padding Value                | Optional field, only be useful if FillNAMethod is set to Pad. |
| Alert observation window     | If Anomaly Ratio in [current timestamp - Alert observation window, current timestamp] is >= Anomaly Ratio, alert will be trigger. |
| Anomaly Ratio                | Use with Alert observation window to decide whether to trigger an alert. if anomaly ratio in [current timestamp - Alert observation window, current timestamp] is >= Anomaly Ratio, alert will be trigger. |
| Snooze after alerting        | If there is an alert has been triggered in [current timestamp - snooze size, current timestamp] , current timestamp will not trigger alert no matter whether there is an anomaly. |
| Detection sensitivity        | From 1 ~ 100, to define detector's sensitivity. The bigger the more sensitive to anomalies. |
| Correlation Window           | Correlate near by anomalies whose time span will be correlateWindow * inference frequency. |

> [!Note]
>
> - Inference frequency should be set according to the align policy when the series in series set has difference granularity.
> - To access Multivariate anomaly detection(MAD) resource on Metrics advisor(MA), you need to assign MAD's managed identity to MA. [How to assign role to a resource](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/managed_identity.md)

Click **Create** to complete the creation, then you can find the created instance.

[![New application instance](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/raw/main/media/train.png)](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/media/train.png)

Four buttons below **Model** tab represent from four operations:

| Name           | Function                         |
| -------------- | -------------------------------- |
| State          | Refresh the instance state.      |
| Train          | Train the model.                 |
| Inference      | Inference when training is done. |
| Operation Logs | Instance logs.                   |

## Next steps

- [Training](https://github.com/MS-AI-Platform/MetricsAdvisorMultivariate/blob/main/training.md)
