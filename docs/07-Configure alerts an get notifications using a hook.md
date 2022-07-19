# ⭐Settings

After an anomaly is detected by Metrics Advisor for Equipment, an alert notification will be triggered based on alert setting using a hook. 

## 1. Create a hook

Currently, Metrics Advisor for Equipment supports only one type of hook: **Webhook.**

A Webhook is the entry point for all the information available from the Metrics Advisor service, and calls a user-provided API when an alert is triggered. All alerts can be sent through a Webhook.

![image](https://user-images.githubusercontent.com/36343326/176588851-4f6c3e5c-dfb7-4500-854b-07552cfb0689.png)

To create a Webhook, you will need to add the following information:
![image](https://user-images.githubusercontent.com/36343326/176589224-644b7bf0-565f-4c38-aa7d-53ae9929aa98.png)


| Parameter           | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| Endpoint            | The API address to be called when an alert is triggered.     |
| Username / Password | For authenticating to the API address. Leave this black if authentication isn't needed. |
| Header              | Custom headers in the API call.                              |

After creating, you get a hook list.

![image](https://user-images.githubusercontent.com/36343326/176588951-7211f100-dfca-4732-9080-2fea67ecf374.png)

## 2. Hook details





![image-20220719162828599](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/image-20220719162828599.png)



![image](https://user-images.githubusercontent.com/36343326/176591650-a9007c26-a009-4a30-8d06-d30a6f90bb47.png)
![image](https://user-images.githubusercontent.com/36343326/176591665-53329e17-851a-4ecd-bbe3-ab344d039561.png)

## 3. Edit hooks 

The attached hooks can be modified on the hook detail pages.

![image-20220719163016542](https://raw.githubusercontent.com/Azure/Metrics-Advisor-for-Equipment/main/image/image-20220719163016542.png)
