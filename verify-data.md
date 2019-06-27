---

copyright:
  years:  2019
lastupdated: "2019-06-19"

keywords:

subcollection: mass-data-migration

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Verifying your data
{: #verify-data}

You can access and verify your migrated data by using {{site.data.keyword.cos_full}}.
{: shortdesc}

After the offload is complete, enjoy immediate access to your data in the cloud while {{site.data.keyword.cloud_notm}} securely wipes the device.

## Accessing your data in Cloud Object Storage
{: #access-data-cos}

Your migrated data is available in the Cloud Object Storage instance that you specified when you submitted your {{site.data.keyword.mdms_short}} request. Before you delete data from your source server, verify that the data was uploaded successfully to {{site.data.keyword.cloud_notm}}.

To access and verify your data: 

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of Cloud Object Storage.
4. From the list of available storage buckets, select the bucket name that you designated for data migration.
5. Verify that the objects that are associated with the bucket correspond with the data that you copied to the {{site.data.keyword.mdms_short}} device.

## Moving data to a different storage solution
{: #move-data}

Depending on your workload requirements, you might need to move your migrated data from Cloud Object Storage to a different cloud storage solution, such as [File Storage](https://{DomainName}/catalog/infrastructure/file-storage) or [Block Storage](https://{DomainName}/catalog/infrastructure/block-storage). 

To learn more about storage migration options, check out [Recipe: Moving data from COS to File or Block Storage](https://developer.ibm.com/recipes/tutorials/moving-data-from-cos-to-file-or-block-storage/){: external}.
