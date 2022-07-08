---
title: "Infrastructure Deployment"
chapter: true
weight: 30
pre: "<b>3. </b>"
---

# Infrastructure Setup

## On-premises

As shown in the architecture diagram below, the first template will create an NFS server, an Application server, and a DataSync agent, and a File Gateway appliance will be deployed in an AWS region simulating the on-premises environment.


---

#### 1. Launch the CloudFormation template provided below to create our Mock On-Premises infrastructure in a new browser tab.

[![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=DataMigrationWorkshop-onPremResources&templateURL=https://aws-workshop-c1as-cft-templates.s3.amazonaws.com/on-premise-datamigration-workshop.yaml)

- This will automatically redirect to the AWS CloudFormation create stack page.
- Ensure AWS region is ```us-east-1```.
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

This template will be deployed in an alternative region. It will create an S3 bucket to simulate the AWS cloud region to which the NFS server’s data will be migrated.

---

#### 1. Launch the CloudFormation template provided below to create our Cloud Infrastructure..
[![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=DataMigrationWorkshop-inCloudResources&templateURL=https://aws-workshop-c1as-cft-templates.s3.amazonaws.com/cloud-datamigration-workshop.yaml)

- Ensure AWS region is ```us-east-2```
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