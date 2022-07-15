---
title: "Cleanup"
chapter: false
weight: 140
pre: "<b>8. </b>"
---

### Clean up your Environment

Now that you have successfully completed this lab, to avoid charges please follow the documentation steps to remove resources deployed during this workshop.

- Delete all objects in the data-migration-workshop S3 bucket in the in-cloud region. The bucket must be empty before it can be deleted by CloudFormation in the next step.

- Go to the CloudFormation page in the in-cloud region and delete the stack named ```DataMigrationWorkshop-inCloudResources```.

- Go to the CloudFormation page in the on-premises region and delete the stack named ```DataMigrationWorkshop-onPremResources```.


------

### Thank you for joining our workshop! We hope you enjoyed this and learned new things! :clap: :clap: