## Scheduling inference
After you create a model, you can use it to monitor your asset in real-time. To use your model to monitor your asset, you do the following.

Create an new real time inference.

![image](https://user-images.githubusercontent.com/36343326/175054446-79c3977d-6e18-498f-8622-3ec436c14b8c.png)


Specify the frequency that data is uploaded.

![image](https://user-images.githubusercontent.com/36343326/175054891-c5311013-94c0-4762-b9b3-5353cb442711.png)


![image](https://user-images.githubusercontent.com/36343326/175054762-521ef174-d2ae-4ba5-8c3e-a249c5431cd3.png)

Schedule the time period that your model performs inference on the data coming from your pipeline.



To create an inference schedule on the data that your model outputs to Amazon S3, use one of the following procedures.

Schedule inference (console)
To schedule an inference (console)

To schedule inference, you specify the model, the schedule, the S3 location of where the model is reading the data, and where it outputs the results of the inference.

Sign in to AWS Management Console and open the Amazon Lookout for Equipment console at Amazon Lookout for Equipment console.

Choose Models. Then choose the model that monitors your asset.

Choose Schedule inference.

For Inference schedule name, specify the name for the inference schedule.

For Model, choose the model that is monitoring the data coming from your asset.

For S3 location under Input data, specify the Amazon S3 location of the input data coming from the asset.

For Data upload frequency, specify how often your asset sends the data to the S3 bucket.

For S3 location under Output data, specify the S3 location to store the output of the inference results.

For IAM role under Access Permissions, specify the IAM role that provides Amazon Lookout for Equipment with access to your data in Amazon S3.

Choose Schedule inference.

If you believe you have found a security vulnerability in any Microsoft-owned repository that meets [Microsoft's definition of a security vulnerability](https://aka.ms/opensource/security/definition), please report it to us as described below.

## Reporting Security Issues

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, please report them to the Microsoft Security Response Center (MSRC) at [https://msrc.microsoft.com/create-report](https://aka.ms/opensource/security/create-report).

If you prefer to submit without logging in, send email to [secure@microsoft.com](mailto:secure@microsoft.com).  If possible, encrypt your message with our PGP key; please download it from the [Microsoft Security Response Center PGP Key page](https://aka.ms/opensource/security/pgpkey).

You should receive a response within 24 hours. If for some reason you do not, please follow up via email to ensure we received your original message. Additional information can be found at [microsoft.com/msrc](https://aka.ms/opensource/security/msrc). 

Please include the requested information listed below (as much as you can provide) to help us better understand the nature and scope of the possible issue:

  * Type of issue (e.g. buffer overflow, SQL injection, cross-site scripting, etc.)
  * Full paths of source file(s) related to the manifestation of the issue
  * The location of the affected source code (tag/branch/commit or direct URL)
  * Any special configuration required to reproduce the issue
  * Step-by-step instructions to reproduce the issue
  * Proof-of-concept or exploit code (if possible)
  * Impact of the issue, including how an attacker might exploit the issue

This information will help us triage your report more quickly.

If you are reporting for a bug bounty, more complete reports can contribute to a higher bounty award. Please visit our [Microsoft Bug Bounty Program](https://aka.ms/opensource/security/bounty) page for more details about our active programs.

## Preferred Languages

We prefer all communications to be in English.

## Policy

Microsoft follows the principle of [Coordinated Vulnerability Disclosure](https://aka.ms/opensource/security/cvd).

<!-- END MICROSOFT SECURITY.MD BLOCK -->
