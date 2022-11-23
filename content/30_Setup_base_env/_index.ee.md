---
title: "Infrastructure Deployment"
chapter: true
weight: 30
pre: "<b>3. </b>"
---

# Infrastructure Setup

## On-premises

As shown in the architecture diagram below, the first template will create an NFS server, an Application server, and a DataSync agent, and a File Gateway appliance will be deployed in an AWS region simulating the on-premises environment.

![TrendMicro](/images/on-prem-diag.png)

---


#### 1. Launch the CloudFormation template provided below to create our Mock On-Premises infrastructure in a new browser tab.

<a target="_blank" href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=DataMigrationWorkshop-onPremResources&amp;templateURL=https://aws-workshop-c1as-cft-templates.s3.amazonaws.com/on-premise-datamigration-workshop.yaml"><img alt="Launch Stack" src="https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg"></a>

- This will automatically redirect to the AWS CloudFormation create stack page.
- Click **Next** on the Create Stack page.

![TrendMicro](/images/op1.png)

---

#### 2. Specify stack details.
- Accept the default parameter values.
- Click **Next**.

![TrendMicro](/images/op2.png)

---

#### 3. Configure stack options.
- Optional - Configure tags.
- Click **Next**.

---

#### 4. Review stack details.
- On the Review page, scroll to the bottom and **check the box** to acknowledge that CloudFormation will create IAM resources.
- Click **Create stack**.

![TrendMicro](/images/op3.png)

Note: Instances that are launched as part of this CloudFormation template may be in the initializing state for few minutes.

While the CloudFormation deployment progresses in the on-premises region, you can proceed to deploy resources for the in-cloud region.

---

## Cloud Infrastructure

**This template will create an S3 bucket to simulate the AWS cloud region to which the NFS server’s data will be migrated.**

![TrendMicro](/images/bucket.png)

---

#### 1. Coming from the Conformity Immersion day? Use this Step, otherwise please use step 1*.

{{% notice warning %}}
The below template creates an UNENCRYPTED bucket. This is intentional. This template is to be scanned and remediated with the Conformity IaC Template Scanner VS code extension for misconfigurations. Any S3 bucket created should be encrypted at a minimum. Some exceptions include static S3 websites. **If you DO NOT have access to Conformity please skip this step and use the IaC under step 1.***
{{% /notice %}}

<details>
  <summary> -> <code>CLICK HERE</code> to see how to scan the Cloudformation template for misconfigurations</summary>

#### 1.1 Download IaC template
- Click [here to download](https://aws-workshop-c1as-cft-templates.s3.amazonaws.com/on-premise-datamigration-workshop.yaml) 

---

#### 1.2 Open IaC template in VS Code IDE.
- With the CloudFormation template above open in the VSCode IDE, open the Command Pallet with:
```
- MAC OS: ⇧ + ⌘ + P
- Windows/Linux: Ctrl+Shift+P

```
- Search for **Cloud One Conformity: Scan the Current Open Template** and hit enter to start automatically scanning your CloudFormation template:
![TrendMicro](/images/conformity2.png)

The result will appear in a second tab called Scan Result like the image below.

You can also check out the Conformity Knowledge Base, which can help you better understand more about any best practice check violations and how to remediate and fix them in your CloudFormation template or in production environments:

![TrendMicro](/images/conformity3.png)

---

#### 1.3 Encrypt the S3 bucket to reduce misconfigurations introduced inside AWS.
- Search for(Line 26): ```AWS::S3::Bucket```

![TrendMicro](/images/conformity4.png)

- Insert the following snippet to add S3 SSE encryption(On line 41).

```
      BucketEncryption:
        ServerSideEncryptionConfiguration:
        - ServerSideEncryptionByDefault:
            SSEAlgorithm: AES256
```
![TrendMicro](/images/conformity5.png)

- Save the template changes.

---

#### 1.4 Scan the updated template to validate. Then launch this stack in AWS.

![TrendMicro](/images/conformity6.png)

</details>
<br>

---
## 1.* Launch the CloudFormation template provided below to create our Cloud Infrastructure

{{% notice tip %}}
The below template creates an ENCRYPTED bucket using SSE-S3. **This template is for thse who do not have a Conformity account or IDE to edit code.**
{{% /notice %}}

<a target="_blank" href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=DataMigrationWorkshop-inCloudResources&amp;templateURL=https://aws-workshop-c1as-cft-templates.s3.amazonaws.com/encrytped-s3-datamigration-workshop.yaml"><img alt="Launch Stack" src="https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg"></a>

- Click **Next** on the Create Stack page.

![TrendMicro](/images/cc1.png)

---

#### 2. Specify stack details.
- Click **Next** (there are no stack parameters).

![TrendMicro](/images/cc2.png)

---

#### 3. Configure stack options.
- Optional - Configure tags.
- Click **Next**.

---

#### 4. Review.
- On the Review page, scroll to the bottom and **check the box** to acknowledge that CloudFormation will create IAM resources.
- Click **Create stack**.

![TrendMicro](/images/op3.png)

---

#### Wait for the CloudFormation stacks in each region to reach the CREATE_COMPLETE state before proceeding to the next steps. 
It should take about 10 minutes for both CloudFormation stacks to complete.

![TrendMicro](/images/cc3.png)

---