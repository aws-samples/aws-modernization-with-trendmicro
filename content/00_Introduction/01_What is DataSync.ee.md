---
title: "DataSync"
chapter: false
weight: 6
---


# What is AWS DataSync?

---

![datasync](/images/datasync.png)

[AWS DataSync](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/govcloud-dsy.html) is a data transfer service that makes it easy for you to automate moving data between on-premises storage systems and Amazon S3, Amazon Elastic File System (Amazon EFS), or Amazon FSx for Windows File Server. DataSync automatically handles many of the tasks related to data transfers that can slow down migrations or burden your IT operations, including running your own instances, handling encryption, managing scripts, network optimization, and data integrity validation. You can use DataSync to transfer data at speeds up to 10 times faster than open-source tools. You can use DataSync to copy data over AWS Direct Connect or internet links to AWS for one-time data migrations, recurring data processing workflows, and automated replication for data protection and recovery.


For the purposes of this workshop we will be leveraging S3.


---

#### Is the data encrypted while being transferred?

When leveraging AWS DataSync all the data transferred between source and destination is encrypted via Transport Layer Security (TLS). Data is never persisted in AWS DataSync itself. The service supports using default encryption for S3 buckets, Amazon EFS file system encryption of data at rest, and Amazon FSx For Windows File Server encryption at rest and in transit.

---

#### DataSync Components

##### 1. Deploy the DataSync Agent. 

Download the agent virtual machine image from the AWS Console and deploy to your on-premises VMware ESXi, Linux Kernel-based Virtual Machine (KVM), or Microsoft Hyper-V hypervisor.

##### 2. Create a data transfer task.

A task can be created by specifying the location of your data source and destination, and any options you want to use to configure the transfer, such as the desired task schedule.

##### 3. Start transferring.

Start the task and begin monitoring data movement in the AWS console.

---

#### Data Sync Task Execution Life Cycle


![datasync](/images/datasync_lifecycle.png)


### Learn More

To learn more about AWS DataSync, click <a href="https://aws.amazon.com/datasync/faqs/">here</a>
