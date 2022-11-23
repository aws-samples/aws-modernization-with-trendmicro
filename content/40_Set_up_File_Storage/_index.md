---
title: "Deploy File Storage Security"
chapter: true
weight: 40
pre: "<b>4. </b>"
---

# Deploy File Storage Security

### Cloud One - File Storage Security Deployment

Let's deploy Cloud One - File Storage Security to our AWS Account.

**1.** Login to the [Cloud One platform](https://cloudone.trendmicro.com). It will request your login information. If you don’t have it, check the requirements page that has all the details that you will need to create your account. 

![Diagram](/images/login.png)

---

**2.** Select the **File Storage Security** tile
![Diagram](/images/login_2.png)

---

**3.** Click on **Stack management** on the left side
![Diagram](/images/login_3.png)

---

**4.** Click on **Deploy** 
![Diagram](/images/login_4.png)

---

**5.** Select the ```Scanner Stack and Storage Stack```, to deploy to your AWS account.

![Diagram](/images/fss-deploy-stacks-select.png)

---

**6.** Select the AWS region that the CloudFormation stack named ```DataMigrationWorkshop-inCloudResources```. 
- The default selection is AWS region ```us-east-1```.
- Click on **Launch Stack**.

This will redirect you to your AWS account in the region that you choose to deploy the stack. Make sure that you’re logged in and have the correct permissions – you can check the details of the permissions required in the Requirements section.

{{% notice tip %}}
Try to make sure the Cloud One console tab is in the same Window as your browser. This way, the Launch Stack will automatically use the AWS session that you have open already. 
{{% /notice %}}

You can validate the CloudFormation Template by clicking in ```Review Stack```. To make it easier, you can also verify the CloudFormation Template by clicking the buttons below:

{{% button href="https://github1s.com/trendmicro/cloudone-filestorage-cloudformation-templates/blob/master/aws/FSS-All-In-One.template" %}}All in One Template{{% /button %}}
{{% button href="https://github1s.com/trendmicro/cloudone-filestorage-cloudformation-templates/blob/master/aws/FSS-Scanner-Stack.template" %}}Scanner Stack{{% /button %}}
{{% button href="https://github1s.com/trendmicro/cloudone-filestorage-cloudformation-templates/blob/master/aws/FSS-Storage-Stack.template" %}}Storage Stack{{% /button %}}

![Diagram](/images/login_5.png)

---

**7.** In the CloudFormation page the <b>only required parameter</b> here is the <b>name of the bucket</b> that was created in the template stack named ```DataMigrationWorkshop-inCloudResources```. 

- To find the bucket name check the cloudformation template outputs section as shown below.

![Diagram](/images/output-cloud1.png)

- It also supports different parameters to customize your installation, like Resource prefixes and optional KMS integration. For more details about these configurations check our <a href="https://cloudone.trendmicro.com/docs/file-storage-security/gs-deploy-all-in-one-stack/">Documentation</a>.

- After adding the bucket name you will need to acknowledge and click on <b>"Create Stack"</b>

![Diagram](/images/cfdeploy.png)

---

**8.** After deploying the all-in-one stack in your AWS account, you must configure the scanner and storage stack Amazon Resource Names (ARNs) information in the Cloud One console. The ARNs map a scanner stack to a storage stack, allowing them to be aware of each other.

Go to **CloudFormation > Stacks > your all-in-one stack > Outputs** tab and copy the Values with these Key names here ```ScannerStackManagementRoleARN``` and ```StorageStackManagementRoleARN``` and paste the information into the Cloud One - File Storage Security console.

![Diagram](/images/fss-arn-aws-info.png)

![Diagram](/images/login_6.png)

---

**9.** Then Click <b>Submit</b>. You see a couple of success messages at the bottom and the stack will show in the Stack Management too. 

![Diagram](/images/login_7.png)

You have now completed the deployment of the All-in-One stack :tada:, so let’s test our deployment.

All the new objects that will be uploaded to your bucket that you define will now automatically be scanned against malware and tagged as either “malicious” or “no issues found”.


---

Here is a video with the steps to deploy All-in-One stack for File Storage Security:
{{< youtube id="_w1_k5W3tEQ" title="Deploying the File Storage Security All In One Stack" >}}
