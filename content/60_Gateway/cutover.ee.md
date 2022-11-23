---
title: "Access Cloud Storage"
chapter: true
weight: 61
pre: "<b>6.1 </b>"
---

# Continue access to data with Storage Gateway only

With the DataSync migration completed and the File Gateway mounted, activated, and validated, the NFS server can be shut down. File access can be achieved by using Storage Gateway. Finally, test files will be written through Storage Gateway, verifying they end up in the S3 bucket to be scanned.

![Diagram](/images/sgw1.png)

---

#### 1. Unmount the NFS server.

From the CLI for the Application server, run the following command to unmount the NFS server:

```
sudo umount /mnt/data
```

---


#### 2. Validate access to new storage.

Using the EC2 console connect to the **Application Server**.

From the CLI of the Application server, run the following command to write a new object to S3 through Storage Gateway:

```
sudo cp /mnt/fgw/images/00002.jpg /mnt/fgw/new-image2.jpg
sudo cp eicar.com.txt /mnt/fgw/new-data.txt
```
---

#### 3. Return to the AWS console.

- Select the data-migration-workshop bucket. You should see the one new object named ```new-image2.jpg`` in the bucket. 
- The other object was moved to quarantine as it was found to be malicious.

![Diagram](/images/sgw8.png)

---


#### 4. Refresh Storage Gateway Cache.

When initially configuring storage gateway, the cache refresh interval was set to none. This means files quarantined by File Storage Security will continue to appear in the application server mount path.

To verify this, run the following command on the Application Server:

```
ls /mnt/fgw
```

![Diagram](/images/sgw7.png)

---

#### 5. Navigate back to AWS Storage Gateway.

- From the left-hand menu, select **File Shares**.
- Check the box next to the file share name.
- Click **Actions**.
- From the drop down, select **Refresh Cache**.
- Click **Start**.

![Diagram](/images/sgw9.png)
![Diagram](/images/sgw10.png)

---

#### 6. Validate cache refresh.

Using the EC2 console connect to the **Application Server**.

From the CLI of the Application server, run the following command:

```
ls /mnt/fgw
```
![Diagram](/images/sgw11.png)

With the cache refreshed the file is no longer available to the Application Server to interact with.

---
