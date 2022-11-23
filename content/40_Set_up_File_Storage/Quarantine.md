---
title: "Quarantine Malicious Files"
chapter: false
weight: 41
pre: "<b>4.1 </b>"
---

### Prerequisites

Continue to deploy S3 buckets and the File Storage Security quarantine plugin in the same AWS region used before. 

**1.** **For this workflow, we will need to create an Amazon S3 bucket**

- Create a 'Quarantine bucket' to receive quarantined files when detected. Example: `fss-quarantine`.

{{% notice warning %}}
<p style='text-align: left;'>
Remember that S3 buckets are a unique name globally for all AWS customers. If you try to use the same name from this workshop you will have issues with an existing S3 bucket name already created.
</p>
{{% /notice %}}


**2.** **Locate the 'ScanResultTopic' SNS topic ARN. This is needed to deploy the plugin**

- In the AWS console, go to **Services > CloudFormation** > your all-in-one stack > **Resources** > your storage stack > **Resources**.
- Scroll down to locate the  **ScanResultTopic** Logical ID.
- Copy the **ScanResultTopic** ARN to a temporary location. It will look like this: `arn:aws:sns:us-east-1:123445678901:FileStorageSecurity-All-In-One-Stack-StorageStack-1IDPU1PZ2W5RN-ScanResultTopic-N8DD2JH1GRKF`

![Diagram](/images/slack_2.png)

---

### Deploying Post Scan Action (Functions) - Promote and Quarantine

In this case, let's use the Serverless Application Repository

1. Visit [the app's page on the AWS Lambda Console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/create/app?applicationId=arn:aws:serverlessrepo:us-east-1:415485722356:applications/cloudone-filestorage-plugin-action-promote-or-quarantine).
2. Fill in the parameters:
    * ScanResultTopic
    * ScanningBucketName
    * **PromoteBucketName(Ignore and leave blank. We will not be using this for our workflow)**
    * QuarantineBucketName
    * Optionally, you can customize the name of the Cloud Formation stack that will be created
3. Check the `I acknowledge that this app creates custom IAM roles.` checkbox.
4. Click `Deploy`.

![Diagram](/images/scan_action_1.png)

![Diagram](/images/scan_action_3.png)

----

**5.** After a couple minutes you can click on the tab Deployments and expand the deployment to see if the status shows as complete. Then you can move to the next step to test it.

![Diagram](/images/scan_action_4.png)


---

<b>Awesome, You did it! :tada: </b>
        


