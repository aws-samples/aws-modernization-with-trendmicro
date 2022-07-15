---
title: "Configure AWS DataSync"
chapter: true
weight: 50
pre: "<b>5. </b>"
---

# AWS DataSync configuration.

The DataSync agent has already been deployed in the on-premises region via the CloudFormation template. The agent needs to be activated, DataSync locations need to be defined, and then finally a DataSync task needs to be created to copy data from the source location (On-Prem) to the destination location (AWS Cloud Account).

The created DataSync task handles the migration of data using the two locations defined. With DataSync, a location is an endpoint where files reside or will be subsequently moved. A location can range from an NFS export, an SMB share, an Amazon S3 bucket, HDFS, FSx for Windows, FSx for Lustre or an Amazon EFS file system. Location objects are independent of tasks. A location can be used with multiple different tasks

We will focus on migration to AWS S3.

![Diagram](/images/data1.png)

---

#### 1. Activate the DataSync agent in the same AWS region where the stack named ```DataMigrationWorkshop-inCloudResources``` was deployed.

Although the agent instance was created in the **DataMigrationWorkshop-onPremResources** template, before it can be used it needs to be activated. Follow the steps below to activate the agent.

- Ensure you are in the AWS region ```us-east-2```.

- Go to the AWS Management console page navigate to **AWS DataSync**.

- From the Left-hand menu select **Agents**.

- Click **Create agent**.

![Diagram](/images/sync2.png)

---

#### 1.1 Create agent.

- Deploy Agent: **Amazon EC2**

- Leave the Service endpoint as **Public service endpoints**.

- Activation key section: **Automatically get the activation key from your agent**. 

- Agent Address: **dataSyncAgentPublicIP** found in outputs tab of stack ```DataMigrationWorkshop-onPremResources```. 

- Click **Get key**.

![Diagram](/images/sync1.png)

---

Once the activation is successful, you will be shown the activation key and will be prompted for further information.

- For Agent name enter: <code>migration-agent</code>.
- Click **Create agent**.

![Diagram](/images/data3.png)

![Diagram](/images/sync3.png)



---

#### 2. Create location.

- On the left-hand side of the DataSync service page, click on **Locations** and then click on **Create location**.

![Diagram](/images/loco1.png)

---

#### 2.1 Create NFS server Location.

- Create a location for the on-premises NFS server. Select **Network File System (NFS)** from the Location type drop-down.

- From the Agents drop-down, select the DataSync agent that was created in the previous step.

- Enter the **nfsServerPrivateIP**, from the ```DataMigrationWorkshop-onPremResources``` CloudFormation outputs. 

- Under Mount path, enter ```/media/data```

- Click **Create location**.

![Diagram](/images/data4.png)

---

#### 3. Create another location.

- On the left-hand side of the DataSync service page, click on **Locations** and then click on **Create location**.

![Diagram](/images/loco2.png)

---

#### 3.1 Create S3 location.

- Create a location for the S3 bucket. Select **Amazon S3 bucket** from the Location type drop-down.

- From the S3 bucket drop-down, select the S3 bucket that starts with **data-migration-workshop** and is followed by a long GUID.

- Keep the S3 storage class as **Standard**.

- Under Folder, enter ``` / ``` This will copy all files to the top-level of the bucket.

- Under IAM role, select the S3 bucket IAM role, ```DataMigrationWorkshop-inCloudResou-s3BucketIamRole```. 

The full name of the role can be found in the outputs for the **DataMigrationWorkshop-inCloudResources** CloudFormation stack.

- Click **Create location**.

![Diagram](/images/data5.png)

---

#### 4. On the left-side of the page, click Locations again. You should now have two locations listed. One for the NFS server and one for the S3 bucket.

![Diagram](/images/data6.png)

---

#### 5. Create a DataSync task.

- On the left-hand side of the DataSync service page, click on **Tasks** and then click on **Create task**.

![Diagram](/images/task1.png)

---

#### 5.1 Configure source location.

- Under Source location options, select **Choose an existing location**.

- Under the Existing locations drop-down, select the **NFS server location** you created previously.

- Click **Next**.

![Diagram](/images/data7.png)

---

#### 5.2 Configure destination location.

- Under Destination location options, select **Choose an existing location**.

- Under the Existing locations drop-down, select the **S3 bucket location** you created previously.

- Click **Next**.

![Diagram](/images/data8.png)

---

- Name the task: <code>datasync-migration</code>.

- Task execution configuration: under verify data, select **Verify only the data transferred**. Keep all other options as-is.

- Select Autogenerate under Task logging to create a CloudWatch log group and Resource policy.

- Click **Next**.

![Diagram](/images/data14.png)
![Diagram](/images/data15.png)

- Review that task settings and Click **Create task**.

---

#### 6. Run the DataSync task.

- Wait for the Task status to report **"Available"**. (you may need to refresh the page)

![Diagram](/images/data9.png)

To run the task, click the **Start** button, and then click **Start with defaults**.

- The task will immediately go into the **"Running"** state.

- Under the History tab, click on the task execution object in the list.

![Diagram](/images/data10.png)

As the task runs, the execution status will progress from "Launching" to "Preparing" to "Transferring" to "Verifying" and finally to "Success". The task execution will report statistics on the job, as shown below. It will take a few minutes for the task to complete. Once the task has finished, notice that 202 files were transferred. This is the 200 files in the data set along with the two folders in the path that we specified.

![Diagram](/images/data11.png)
![Diagram](/images/data12.png)

---

#### Validate migration

Navigate to AWS S3. In the bucket list, click on the data-migration-workshop bucket. You should see a top-level folder named "images". Inside this folder should be the 200 .jpg files from the NFS server.

![Diagram](/images/data13.png)