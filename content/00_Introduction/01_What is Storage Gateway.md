---
title: "Storage Gateway"
chapter: false
weight: 7
---

# What is AWS StorageGateway?

---

![datasync](/images/sg1.png)

[AWS Storage Gateway](https://aws.amazon.com/storagegateway/) is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage. You can use Storage Gateway to simplify storage management and reduce costs for key hybrid cloud storage use cases. These include moving backups to the cloud, using on-premises file shares backed by cloud storage, and providing low-latency access to data in AWS for on-premises applications.

To support these use cases, the service provides four different types of gateways that seamlessly connect on-premises applications to cloud storage, caching data locally for low-latency access:

- Tape Gateway
- File Gateway
- File Gateway - FSx
- Volume Gateway

![datasync](/images/sg.png)

For the purposes of this workshop we will be leveraging File Gateway.

---

#### What encryption does AWS Storage Gateway use to protect my data?

All data transferred between any type of gateway appliance and AWS storage is encrypted using SSL. By default, all data stored by AWS Storage Gateway in S3 is encrypted server-side with Amazon S3-Managed Encryption Keys (SSE-S3).

---

#### Storage Gateway Components

#### 1. Deploy the file gateway. 

Download the virtual appliance gateway or purchase the hardware appliance. You can deploy a virtual machine containing the Storage Gateway software on VMware ESXi, Microsoft Hyper-V, or Linux KVM, or you can deploy Storage Gateway as a hardware appliance. The gateway connects your applications to AWS storage by providing standard storage interfaces. It provides transparent caching, efficient data transfer, and integration with AWS monitoring and security services.

#### 2. Activate.

After the deployment, you then activate the gateway from the AWS Management Console or through the Storage Gateway API.

#### 3. Associate.

After the S3 File Gateway is activated, you create and configure your file share and associate that share with your Amazon Simple Storage Service (Amazon S3) bucket. Doing this makes the share accessible by clients using either the Network File System (NFS) or Server Message Block (SMB) protocol. Files written to a file share become objects in Amazon S3, with the path as the key. There is a one-to-one mapping between files and objects, and the gateway asynchronously updates the objects in Amazon S3 as you change the files.

### Learn More

To learn more about AWS Storage Gateway, click <a href="https://aws.amazon.com/storagegateway/faqs/">here</a>