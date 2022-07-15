---
title: "Configure Storage Gateway"
chapter: true
weight: 60
pre: "<b>6. </b>"
---

# AWS Storage Gateway configuration.

The files from the NFS server have now been copied to the AWS S3 bucket defined in the DataSync task. However, the application still running in the On-Premises environment will need access to the S3 bucket to continue with operations. The File Gateway was already deployed by CloudFormation in the on-premises region. Next, you will connect your application to the S3 bucket and provide access to the objects through Storage Gateway NFS share.

You will mount the Storage Gateway share on the Application server to validate access to the files.

![Diagram](/images/sgw1.png)

---

#### 1. Activate the Storage Gateway in the same AWS region where the stack named ```DataMigrationWorkshop-inCloudResources``` was deployed.

Although the agent instance was created in the **DataMigrationWorkshop-onPremResources** template, before it can be used it needs to be activated. Follow the steps below to active the agent.

- Ensure you are in the AWS region ```us-east-2```.

- Go to the AWS Management console page navigate to **AWS Storage Gateway**.

- Click **Create gateway**.

- Gateway Name: <code>DataMigrationGateway</code>

- Gateway TimeZone: **Select your timezone**.

- Gateway Option Type: **Amazon S3 File Gateway**

- Host Platform: **Amazon EC2**  

- Check Box to confirm gateway set up.

- Click **Next**.

![Diagram](/images/sgw2.png)
![Diagram](/images/sgw3.png)

---

#### 2. Connect Gateway to AWS.

- Service Endpoint: **Publicly accessible**.
- Connection Option: **IP Address**.
- Enter the **fileGatewayPublicIP** found in the outputs of the DataMigrationWorkshop-onPremResources template.
- Click **Next**.
- Review and click **Next** again.

![Diagram](/images/sgw4.png)

#### 2.1 Configure Gateway.

- Accept all the defaults
- Click **Configure**.

![Diagram](/images/sgw5.png)
![Diagram](/images/sgw6.png)

---

#### 3. Create a Storage Gateway NFS share.

- From the left-hand menu, select **File Shares**.

- Click **Create File share**.

- Select the Gateway just created.

- Enter the S3 bucket's name used for migration. Leave the S3 prefix name field blank.

- Ensure NFS is selected under the Access objects using setting. 
- Leave Automated cache refresh from S3 set to none.
- Click **Next**.

![Diagram](/images/fgw1.png)
![Diagram](/images/fgw2.png)


Keep the default S3 storage settings, then click **Next**.

![Diagram](/images/fgw3.png)

Under the Access object section, click **Add client**. 

- Add the **appServerPrivateIP** address, followed by "/32". This will allow the Application server to access the NFS file share on the gateway.

- Click **Next**.

![Diagram](/images/fgw4.png)


---

#### 4. Review and Create.

- Click **Create**.

![Diagram](/images/fgw5.png)

---

#### 4.1 Example commands
- Copy down the AWS command on **Linux**.

![Diagram](/images/fgw7.png)

---

#### 5. Mount the NFS Gateway share on the Application Server.

- Return/Re-establish connection to the **Application server** and run the following command to create a new mount point for the Storage Gateway share:

```
sudo mkdir /mnt/fgw
```

- Next, paste the **Linux mount command** copied from the Storage Gateway file page. Be sure to replace "[MountPath]" with ```/mnt/fgw```. You must run the command as sudo.

```
[Example]
sudo mount -t nfs -o nolock,hard 1.1.1.1:/data-migration-workshop-12345678-2222-3333-4444-012345678910 /mnt/fgw
```

- You should now have two NFS mount points on your Application server: one for the on-premises NFS server (mounted at /mnt/data) and one for the Storage Gateway (mounted at /mnt/fgw).

```
mount | grep nfs4
```

![Diagram](/images/fgw6.png)

---

> Congratulations, you have successfully activated the Storage Gateway and created an NFS file share on the gateway. You then mounted the share on the Application server