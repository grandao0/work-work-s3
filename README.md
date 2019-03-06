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

## Amazon S3 Objects

The object consists of the following parts:
  - Key name (The name that you assign to an object e.g /mydocs/mydoc.doc)
  - Version ID (String that Amazon S3 generates when adding an object to a bucket. Utilized only when versioning enabled)
  - Value (This is the content you are storing. Objects can range in size from zero to 5 TB)
  - Metadata (Set of name-value pairs which can be system-defined metadata or user-defined metadata)
    - Creation time and date
    - Content type
    - Storage class
  - Access control information
    - Access Control Lists (ACL)
    - Resource-based policies
    - User-based policies

Objects are not partially update, when you change an object or upload a new copy to a bucket, a new object is created and overwrites the existing object, unless versioning is enabled, in which case a new object version is created.

Amazon S3 does not provide object locking, if you need this functionality, you must build it into your application layer.

System-defined metadata (aws s3api head-object --bucket mybucket --key myimage.png):
  - content type
  - object creation date (shown as last modified)
  - size in bytes (shown as content length)
  - version ID
  - etag (which can be used for file and object comparison)
  - storage class
  
User-defined metadata requires the prefix `x-amz-meta-` when uploading via the REST API to distinguish them from other HTTP headers or when adding metadata in the Amazon S3 management console, otherwise Amazon S3 will not set the key value pair as you define it.

Amazon S3 data model is a flat structure. There is no hierarchy of buckets and subbuckets or folders and subfolders.
You can use delimiters such as `/` in key names to organize your keys and create a logical hierarchy.

### Amazon S3 Storage Classes

Consider:
  - The type of data
  - Resiliency requirements
  - Usage pattern
  - All but one type stores data in at least 3 Availability Zones

Types:

- S3 Standard
  - Default option
  - Active data
  - Miliseconds access
  - Highest cost high-performance
  - Ideal for frequent retrieval (big data analysis, content distribution, website hosting)
- S3 Intelligent-Tiering
  - Automated tiering (after 30 days moves non frequent accesses objects from frequet tier to infrequent tier)
  - Active and infrequently accessed data
  - Miliseconds access
  - Designed to optimize storage costs
  - Ideal if access patterns are unkown or unpredictable
- S3 Standard Infrequent Access
  - Infrequently accessed data
  - Miliseconds access
  - Associated retrieval cost
  - Designed for colder or less frequently accessed data that still requires milisecond access
  - Ideal for data that ages and you access it less (detailed application logs that you analyze infrequently, backup storage, disaster recovery, data that does not change frequently)
- S3 One Zone Infrequent Access
  - Stored in only 1 Availability Zone
  - Infrequently accessed data
  - Miliseconds access
  - Associated retrieval cost
  - Ideal for secondary backup copies of on-premises data or easily re-creatable data, or for storage used as cross-region replication target from another AWS Region
- S3 Glacier
  - Not available for real-time access (
  - Archive data
  - Minutes to hours access
  - Designed for long-term archival storage and asynchronous retrieval
  - Ideal for long-term backup archives
  - Associated retrieval cost
  - Cost less than the other storage classes
