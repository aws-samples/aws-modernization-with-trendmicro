---
title: "Introduction"
chapter: true
weight: 5
pre: "<b>1. </b>"
---

## Cloud Data Migration

---


Data can always be found at the center of strong application deployments and workflows. Understanding how to eloquently move data from Point-wherever to AWS with minimal overhead, can seem intimidating but can easily be achieved to meet business goals, whether to migrate application data, data archival, or building a data lake pipeline.

Cloud storage offers many advantages such as durability, scalability, cost, and performance. In addition, any critical applications stuck running in on-premises data centers can still achieve quick access to retrieve or upload their precious data. This hybrid cloud storage architecture can help reduce costs and management burden.

![Diagram](/images/migration.png)

---

### Considerations

- Understanding all types of data you are moving.
- Compliance needs.
- Which cloud storage services to use.

---

### Example Workshop Use Case

Company X owns and operates a data center but has decided to reduce the data center footprint and to free up resources. Within the data center is an NFS server that is starting to age out. Most of the data on the server is several years old and is only occasionally accessed for reading. There are new files being written to the server but not very often. The NFS server has been identified to migrate its data into the cloud. Company X must adhere to PCI compliance so scanning data residing in cloud storage is a must. Lastly, there is a legacy application running on-premises that still requires access to the NFS data.


### Planning

Company X has identified their data types and wants to use Amazon Simple Storage Service (S3). For migration services, Company X opted to use AWS DataSync to facilitate secure data transfer of the data from the on-premises NFS server to Amazon S3. To assist with PCI compliance with scanning the objects migrated to S3, Company X has selected Trend Micro - File Storage Security. Lastly, AWS Storage Gateway will be used to facilitate access on-premises to the data once it is in S3.

---
