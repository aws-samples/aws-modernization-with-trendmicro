---
title: "Monitor Migration"
chapter: true
weight: 51
pre: "<b>5.1 </b>"
---

# Monitor migration for important events.

Now that the DataSync task has completed successfully, check the Cloud One - File Storage Security console for scan details.

![Diagram](/images/login_2.png)

---

#### 1. From the left-hand menu, select scan activity.

![Diagram](/images/scan_activity.png)

---

#### 2. Curious on the scan errors?

- In the AWS console, in the AWS region where the File Storage stacks were deployed, navigate to **CloudWatch**.

- From the left-hand menu, select **Logs Insight**.

- Select from the drop down the **ScannerLambda** log stream.

- To identify scan errors, run the following query:

```
fields @timestamp, @message
| filter @message like "sqs_message_id"
| filter scanner_status != "0"
| display scanner_status, scanner_status_message, scanning_result.Error, file_url
```

![Diagram](/images/insight.png)

---

#### 3. Expand the details to understand more regarding the scan.

The amount of scan errors found in the File Storage Security Console should match the Log insights query result.

The reason for the scan error being produced has to do with how the DataSync task operates.

During the task, DataSync creates a temporary stage ```.../.aws-datasync/...``` in S3 to move objects to. These temporary stages are removed once the task is completed. The stage does not exist for the File Storage Security scanner to ingest and scan, thus an error is generated and links to a file that does not exist after the task completes.


![Diagram](/images/insight1.png)

#### 4. Validate scan error path does not exist in S3 buckets.

- In the s3 bucket try to locate the file that generated a scan error.

![Diagram](/images/insight3.png)

---
