## Quotas

| Description                                                  | Quota          |
| :----------------------------------------------------------- | :------------- |
| **Data ingestion**                                           |                |
| Maximum number of components per dataset                     | 3,000          |
| Maximum number of datasets per account                       | 15             |
| Maximum number of pending data ingestion jobs per account    | 5              |
| Maximum number of models per account                         | 15             |
| Maximum number of columns across components per dataset (excluding timestamp) | 3,000          |
| Maximum number of files per component (per dataset)          | 1,000          |
| Maximum length of component name                             | 200 characters |
| Maximum size per dataset                                     | 50 GB          |
| Maximum size per file                                        | 5 GB           |
| Maximum number of pending models per account                 | 5              |
| Maximum number of inference schedulers per model             | 1              |
| **Training and evaluation**                                  |                |
| Maximum number of rows in training data (after resampling)   | 1.5 million    |
| Maximum number of rows in evaluation data (after resampling) | 1.5 million    |
| Maximum number of components in training data                | 300            |
| Maximum number of columns across components in training data (excluding timestamp) | 300            |
| Minimum timespan of training data                            | 180 days       |
| **Inference**                                                |                |
| Maximum size of raw data in inference input data (5-min scheduling frequency) | 5 MB           |
| Maximum size of raw data in inference input data (10-min scheduling frequency) | 10 MB          |
| Maximum size of raw data in inference input data (15-min scheduling frequency) | 15 MB          |
| Maximum size of raw data in inference input data (30-min scheduling frequency) | 30 MB          |
| Maximum size of raw data in inference input data (1-hour scheduling frequency) | 60 MB          |
| Maximum number of rows in inference input data, after resampling (5-min scheduling frequency) | 300            |
| Maximum number of rows in inference input data, after resampling (10-min scheduling frequency) | 600            |
| Maximum number of rows in inference input data, after resampling (15-min scheduling frequency) | 900            |
| Maximum number of rows in inference input data, after resampling (30-min scheduling frequency) | 1,800          |
| Maximum number of rows in inference input data, after resampling (1-hour scheduling frequency) | 3,600          |
| Maximum number of files per component (per inference execution) | 60             |
