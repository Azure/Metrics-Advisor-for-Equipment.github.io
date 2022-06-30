# Configure alerts an get notifications using a hook
After an anomaly is detected by Metrics Advisor for equipment, an alert notification will be triggered based on alert settingusing a hook. An alert setting can be used with multiple detection configurations, various parameters are available to customize your alert rule. 

## Create a hook

Metrics Advisor for equipment supports one type of hooks: web hook. 

### Web hook

A web hook is the entry point for all the information available from the Metrics Advisor service, and calls a user-provided api when an alert is triggered. All alerts can be sent through a web hook.

To create a web hook, you will need to add the following information:

| Parameter           | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| Endpoint            | The API address to be called when an alert is triggered.     |
| Username / Password | For authenticating to the API address. Leave this black if authentication isn't needed. |
| Header              | Custom headers in the API call.                              |

## Add or edit alert setting

Alert setting can be modified as **Application Instance's** parameters.

| Parameter                | Description                                                  |
| ------------------------ | ------------------------------------------------------------ |
| Alert observation window | If Anomaly Ratio in [current timestamp - Alert observation window, current timestamp] is >= Anomaly Ratio, alert will be trigger. |
| Anomaly Ratio            | Use with Alert observation window to decide whether to trigger an alert. if anomaly ratio in [current timestamp - Alert observation window, current timestamp] is >= Anomaly Ratio, alert will be trigger. |
| Snooze after alerting    | If there is an alert has been triggered in [current timestamp - snooze size, current timestamp] , current timestamp will not trigger alert no matter whether there is an anomaly. |
| Detection sensitivity    | From 1 ~ 100, to define detector's sensitivity. The bigger the more sensitive to anomalies. |
| Correlation Window       | Correlate near by anomalies whose time span will be correlateWindow * inference frequency. |

## Understand the alert

When you receive an alert request, the request body shows the detail information as json script.

| Parameter         | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| alertId           | Globally Unique Identifier.                                  |
| correlationId     | The alertId of nearest alert in **Correlation Window**.      |
| groupName         | Name of the **Analysis Group**                               |
| groupId           | Globally Unique Identifier of the **Analysis Group**.        |
| instanceName      | Name of the **Instance Group**.                              |
| instanceId        | Globally Unique Identifier of the **Application Instance**.  |
| from              | Start time of the alert.                                     |
| end               | End time of the alert.                                       |
| hookIds           | Globally Unique Identifier for correlated hooks.             |
| isResolved        | Whether the alert has been resolved or not.                  |
| granularityString | Granularity.                                                 |
| customInSeconds   | Custom granularity when granularity is Custom.               |
| snoozeAlertCount  | If there is an alert has been triggered in [current timestamp - snooze size, current timestamp] , current timestamp will not trigger alert no matter whether there is an anomaly. |
| score             | Anomaly score.                                               |
| severity          | Severity value.                                              |
| variableRank      | Series Name, Serise Id, score, severity of each variable.    |
