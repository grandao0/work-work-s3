work-work-s3
==============

Do you need my counsel?

### Amazon types of storage

- Block Storage

  - Implemented on devices such as storage arrays
  - Multiple blocks comprise a file
  - Stores data organized as an array of unrelated blocks
  - Host file system places data on disk
  - Amazon EBS

- File Storage

  - Stores data in a hierarchy of files and folders
  - Managed by the operating system, e.g NTFS
  - Amazon EFS
  
- Object Storage

  - Flat storage system
  - Stores datas as objects
  - Objects consist of data, metadata, and unique identifier
  - Unique combination of performance, durability, cost and interface 
  - Amazon S3

### Amazon S3

- Pay only for what you use
- Designed for durability
- Highly scalable
- Stores data as object within buckets
- Objects consists of data and optionally any metadata that describes that file
- Access objects with SDKs, AWS CLI, AWS API, Management Console
- Storage classes and transition targets:
  - S3 Standard
  - Intelligent-Tiering
  - S3 Standard - Infrequent Access
  - S3 One Zone - Infrequent Access
  - Amazon S3 Glacier

### Use cases

- Backup Storage
- Media Hosting
- Application Assets
- Data Lake
- Content Delivery

## Amazon S3 Buckets

Before transfer data into Amazon S3, first create a bucket then the data will be stored as objects in the bucket.

When creating a bucket you need not set a predetermined size, you pay only for what you use.
Buckets are resources, and Amazon S3 provides APIs for managing these resources. You can create a bucket using the SKDs, the AWS CLI, or the console.

One factor to consider when creating a bucket is the region where the bucket will be created. Consider the location to help optimze latency, minimize costs or address regulatory requirements.

You can replicate the bucket to other regions using cross-region replication that enables you to configure a replication of objects from a bucket in one region to a bucket in another region.

Restriction and limitations:
  - The account that created the bucket owns it, and ownership is not transferable
  - There is no limit on number of objects
  - You cannot create a bucket within another bucket
  - By default you can create up to 100 buckets in each account, but it can be increased if needed
  - Bucket name must be globally unique and DNS-compliant
  - All names must be lowercase and can contain numbers and hyphens (at least 3 and no more than 63 characters long)
