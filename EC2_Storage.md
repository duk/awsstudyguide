Storage

Amazon EC2 provides you with flexible, cost effective, and easy-to-use data storage options for your instances. Each option has a unique combination of performance and durability. These storage options can be used independently or in combination to suit your requirements.

After reading this section, you should have a good understanding about how you can use the data storage options supported by Amazon EC2 to meet your specific requirements. These storage options include the following:

Amazon Elastic Block Store
Amazon EC2 Instance Store
Amazon Elastic File System (Amazon EFS)
Amazon Simple Storage Service (Amazon S3)
The following figure shows the relationship between these types of storage.


      Storage options for Amazon EC2
    
Amazon EBS

Amazon EBS provides durable, block-level storage volumes that you can attach to a running instance. You can use Amazon EBS as a primary storage device for data that requires frequent and granular updates. For example, Amazon EBS is the recommended storage option when you run a database on an instance.

An EBS volume behaves like a raw, unformatted, external block device that you can attach to a single instance. The volume persists independently from the running life of an instance. After an EBS volume is attached to an instance, you can use it like any other physical hard drive. As illustrated in the previous figure, multiple volumes can be attached to an instance. You can also detach an EBS volume from one instance and attach it to another instance. You can dynamically change the configuration of a volume attached to an instance. EBS volumes can also be created as encrypted volumes using the Amazon EBS encryption feature. For more information, see Amazon EBS Encryption.

To keep a backup copy of your data, you can create a snapshot of an EBS volume, which is stored in Amazon S3. You can create an EBS volume from a snapshot, and attach it to another instance. For more information, see Amazon Elastic Block Store.

Amazon EC2 Instance Store

Many instances can access storage from disks that are physically attached to the host computer. This disk storage is referred to as instance store. Instance store provides temporary block-level storage for instances. The data on an instance store volume persists only during the life of the associated instance; if you stop or terminate an instance, any data on instance store volumes is lost. For more information, see Amazon EC2 Instance Store.

Amazon EFS File System

Amazon EFS provides scalable file storage for use with Amazon EC2. You can create an EFS file system and configure your instances to mount the file system. You can use an EFS file system as a common data source for workloads and applications running on multiple instances. For more information, see Amazon Elastic File System (Amazon EFS).

Amazon S3

Amazon S3 provides access to reliable and inexpensive data storage infrastructure. It is designed to make web-scale computing easier by enabling you to store and retrieve any amount of data, at any time, from within Amazon EC2 or anywhere on the web. For example, you can use Amazon S3 to store backup copies of your data and applications. Amazon EC2 uses Amazon S3 to store EBS snapshots and instance store-backed AMIs. For more information, see Amazon Simple Storage Service (Amazon S3).

Adding Storage

Every time you launch an instance from an AMI, a root storage device is created for that instance. The root storage device contains all the information necessary to boot the instance. You can specify storage volumes in addition to the root device volume when you create an AMI or launch an instance using block device mapping. For more information, see Block Device Mapping.

You can also attach EBS volumes to a running instance. For more information, see Attaching an Amazon EBS Volume to an Instance.

Amazon Elastic Block Store (Amazon EBS)

Amazon Elastic Block Store (Amazon EBS) provides block level storage volumes for use with EC2 instances. EBS volumes are highly available and reliable storage volumes that can be attached to any running instance that is in the same Availability Zone. EBS volumes that are attached to an EC2 instance are exposed as storage volumes that persist independently from the life of the instance. With Amazon EBS, you pay only for what you use. For more information about Amazon EBS pricing, see the Projecting Costs section of the Amazon Elastic Block Store page.

Amazon EBS is recommended when data must be quickly accessible and requires long-term persistence. EBS volumes are particularly well-suited for use as the primary storage for file systems, databases, or for any applications that require fine granular updates and access to raw, unformatted, block-level storage. Amazon EBS is well suited to both database-style applications that rely on random reads and writes, and to throughput-intensive applications that perform long, continuous reads and writes.

For simplified data encryption, you can launch your EBS volumes as encrypted volumes. Amazon EBS encryption offers you a simple encryption solution for your EBS volumes without the need for you to build, manage, and secure your own key management infrastructure. When you create an encrypted EBS volume and attach it to a supported instance type, data stored at rest on the volume, disk I/O, and snapshots created from the volume are all encrypted. The encryption occurs on the servers that hosts EC2 instances, providing encryption of data-in-transit from EC2 instances to EBS storage. For more information, see Amazon EBS Encryption.

Amazon EBS encryption uses AWS Key Management Service (AWS KMS) master keys when creating encrypted volumes and any snapshots created from your encrypted volumes. The first time you create an encrypted EBS volume in a region, a default master key is created for you automatically. This key is used for Amazon EBS encryption unless you select a Customer Master Key (CMK) that you created separately using the AWS Key Management Service. Creating your own CMK gives you more flexibility, including the ability to create, rotate, disable, define access controls, and audit the encryption keys used to protect your data. For more information, see the AWS Key Management Service Developer Guide.

You can attach multiple volumes to the same instance within the limits specified by your AWS account. Your account has a limit on the number of EBS volumes that you can use, and the total storage available to you. For more information about these limits, and how to request an increase in your limits, see Request to Increase the Amazon EBS Volume Limit.

Contents

Features of Amazon EBS
Amazon EBS Volumes
Amazon EBS Snapshots
Amazon EBS–Optimized Instances
Amazon EBS Encryption
Amazon EBS Volume Performance on Linux Instances
Amazon CloudWatch Events for Amazon EBS
Features of Amazon EBS

You can create EBS General Purpose SSD (gp2), Provisioned IOPS SSD (io1), Throughput Optimized HDD (st1), and Cold HDD (sc1) volumes up to 16 TiB in size. You can mount these volumes as devices on your Amazon EC2 instances. You can mount multiple volumes on the same instance, but each volume can be attached to only one instance at a time. You can dynamically change the configuration of a volume attached to an instance. For more information, see Creating an Amazon EBS Volume.
With General Purpose SSD (gp2) volumes, you can expect base performance of 3 IOPS/GiB, with the ability to burst to 3,000 IOPS for extended periods of time. Gp2 volumes are ideal for a broad range of use cases such as boot volumes, small and medium-size databases, and development and test environments. Gp2 volumes support up to 10,000 IOPS and 160 MB/s of throughput. For more information, see General Purpose SSD (gp2) Volumes.
With Provisioned IOPS SSD (io1) volumes, you can provision a specific level of I/O performance. Io1 volumes support up to 20,000 IOPS and 320 MB/s of throughput. This allows you to predictably scale to tens of thousands of IOPS per EC2 instance. For more information, see Provisioned IOPS SSD (io1) Volumes.
Throughput Optimized HDD (st1) volumes provide low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. With throughput of up to 500 MiB/s, this volume type is a good fit for large, sequential workloads such as Amazon EMR, ETL, data warehouses, and log processing. For more information, see Throughput Optimized HDD (st1) Volumes.
Cold HDD (sc1) volumes provide low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. With throughput of up to 250 MiB/s, sc1 is a good fit ideal for large, sequential, cold-data workloads. If you require infrequent access to your data and are looking to save costs, sc1 provides inexpensive block storage. For more information, see Cold HDD (sc1) Volumes.
EBS volumes behave like raw, unformatted block devices. You can create a file system on top of these volumes, or use them in any other way you would use a block device (like a hard drive). For more information on creating file systems and mounting volumes, see Making an Amazon EBS Volume Available for Use.
You can use encrypted EBS volumes to meet a wide range of data-at-rest encryption requirements for regulated/audited data and applications. For more information, see Amazon EBS Encryption.
You can create point-in-time snapshots of EBS volumes, which are persisted to Amazon S3. Snapshots protect data for long-term durability, and they can be used as the starting point for new EBS volumes. The same snapshot can be used to instantiate as many volumes as you wish. These snapshots can be copied across AWS regions. For more information, see Amazon EBS Snapshots.
EBS volumes are created in a specific Availability Zone, and can then be attached to any instances in that same Availability Zone. To make a volume available outside of the Availability Zone, you can create a snapshot and restore that snapshot to a new volume anywhere in that region. You can copy snapshots to other regions and then restore them to new volumes there, making it easier to leverage multiple AWS regions for geographical expansion, data center migration, and disaster recovery. For more information, see Creating an Amazon EBS Snapshot, Restoring an Amazon EBS Volume from a Snapshot, and Copying an Amazon EBS Snapshot.
A large repository of public data set snapshots can be restored to EBS volumes and seamlessly integrated into AWS cloud-based applications. For more information, see Using Public Data Sets.
Performance metrics, such as bandwidth, throughput, latency, and average queue length, are available through the AWS Management Console. These metrics, provided by Amazon CloudWatch, allow you to monitor the performance of your volumes to make sure that you are providing enough performance for your applications without paying for resources you don't need. For more information, see Amazon EBS Volume Performance on Linux Instances.

Amazon EBS Volumes

An Amazon EBS volume is a durable, block-level storage device that you can attach to a single EC2 instance. You can use EBS volumes as primary storage for data that requires frequent updates, such as the system drive for an instance or storage for a database application, or for throughput-intensive applications that perform continuous disk scans . EBS volumes persist independently from the running life of an EC2 instance. After a volume is attached to an instance, you can use it like any other physical hard drive. EBS volumes are flexible. You can dynamically grow volumes, modify provisioned IOPS capacity, and change volume types on live production volumes. Amazon EBS provides the following volume types: General Purpose SSD (gp2), Provisioned IOPS SSD (io1), Throughput Optimized HDD (st1), Cold HDD (sc1), and Magnetic (standard). They differ in performance characteristics and price, allowing you to tailor your storage performance and cost to the needs of your applications. For more information, see Amazon EBS Volume Types.

Contents

Benefits of Using EBS Volumes
Amazon EBS Volume Types
Creating an Amazon EBS Volume
Restoring an Amazon EBS Volume from a Snapshot
Attaching an Amazon EBS Volume to an Instance
Making an Amazon EBS Volume Available for Use
Viewing Volume Information
Monitoring the Status of Your Volumes
Detaching an Amazon EBS Volume from an Instance
Deleting an Amazon EBS Volume
Modifying the Size, IOPS, or Type of an EBS Volume on Linux
Expanding a Linux Partition
Benefits of Using EBS Volumes

EBS volumes provide several benefits that are not supported by instance store volumes.

Data availability
When you create an EBS volume in an Availability Zone, it is automatically replicated within that zone to prevent data loss due to failure of any single hardware component. After you create a volume, you can attach it to any EC2 instance in the same Availability Zone. After you attach a volume, it appears as a native block device similar to a hard drive or other physical device. At that point, the instance can interact with the volume just as it would with a local drive; the instance can format the EBS volume with a file system, such as ext3, and then install applications.
An EBS volume can be attached to only one instance at a time within the same Availability Zone. However, multiple volumes can be attached to a single instance. If you attach multiple volumes to a device that you have named, you can stripe data across the volumes for increased I/O and throughput performance.
You can get monitoring data for your EBS volumes at no additional charge (this includes data for the root device volumes for EBS-backed instances). For more information, see Monitoring Volumes with CloudWatch.
Data persistence
An EBS volume is off-instance storage that can persist independently from the life of an instance. You continue to pay for the volume usage as long as the data persists.
By default, EBS volumes that are attached to a running instance automatically detach from the instance with their data intact when that instance is terminated. The volume can then be reattached to a new instance, enabling quick recovery. If you are using an EBS-backed instance, you can stop and restart that instance without affecting the data stored in the attached volume. The volume remains attached throughout the stop-start cycle. This enables you to process and store the data on your volume indefinitely, only using the processing and storage resources when required. The data persists on the volume until the volume is deleted explicitly. The physical block storage used by deleted EBS volumes is overwritten with zeroes before it is allocated to another account. If you are dealing with sensitive data, you should consider encrypting your data manually or storing the data on a volume protected by Amazon EBS encryption. For more information, see Amazon EBS Encryption.
By default, EBS volumes that are created and attached to an instance at launch are deleted when that instance is terminated. You can modify this behavior by changing the value of the flag DeleteOnTermination to false when you launch the instance. This modified value causes the volume to persist even after the instance is terminated, and enables you to attach the volume to another instance.
Data encryption
For simplified data encryption, you can create encrypted EBS volumes with the Amazon EBS encryption feature. All EBS volume types support encryption. You can use encrypted EBS volumes to meet a wide range of data-at-rest encryption requirements for regulated/audited data and applications. Amazon EBS encryption uses 256-bit Advanced Encryption Standard algorithms (AES-256) and an Amazon-managed key infrastructure. The encryption occurs on the server that hosts the EC2 instance, providing encryption of data-in-transit from the EC2 instance to Amazon EBS storage. For more information, see Amazon EBS Encryption.
Amazon EBS encryption uses AWS Key Management Service (AWS KMS) master keys when creating encrypted volumes and any snapshots created from your encrypted volumes. The first time you create an encrypted EBS volume in a region, a default master key is created for you automatically. This key is used for Amazon EBS encryption unless you select a customer master key (CMK) that you created separately using AWS KMS. Creating your own CMK gives you more flexibility, including the ability to create, rotate, disable, define access controls, and audit the encryption keys used to protect your data. For more information, see the AWS Key Management Service Developer Guide.
Snapshots
Amazon EBS provides the ability to create snapshots (backups) of any EBS volume and write a copy of the data in the volume to Amazon S3, where it is stored redundantly in multiple Availability Zones. The volume does not need be attached to a running instance in order to take a snapshot. As you continue to write data to a volume, you can periodically create a snapshot of the volume to use as a baseline for new volumes. These snapshots can be used to create multiple new EBS volumes or move volumes across Availability Zones. Snapshots of encrypted EBS volumes are automatically encrypted.
When you create a new volume from a snapshot, it's an exact copy of the original volume at the time the snapshot was taken. EBS volumes that are restored from encrypted snapshots are automatically encrypted. By optionally specifying a different Availability Zone, you can use this functionality to create duplicate a volume in that zone. The snapshots can be shared with specific AWS accounts or made public. When you create snapshots, you incur charges in Amazon S3 based on the volume's total size. For a successive snapshot of the volume, you are only charged for any additional data beyond the volume's original size.
Snapshots are incremental backups, meaning that only the blocks on the volume that have changed after your most recent snapshot are saved. If you have a volume with 100 GiB of data, but only 5 GiB of data have changed since your last snapshot, only the 5 GiB of modified data is written to Amazon S3. Even though snapshots are saved incrementally, the snapshot deletion process is designed so that you need to retain only the most recent snapshot in order to restore the volume.
To help categorize and manage your volumes and snapshots, you can tag them with metadata of your choice. For more information, see Tagging Your Amazon EC2 Resources.
Flexibility
EBS volumes support live configuration changes while in production. You can modify volume type, volume size, and IOPS capacity without service interruptions.

Amazon EBS Volume Types

Amazon EBS provides the following volume types, which differ in performance characteristics and price, so that you can tailor your storage performance and cost to the needs of your applications. The volumes types fall into two categories:

SSD-backed volumes optimized for transactional workloads involving frequent read/write operations with small I/O size, where the dominant performance attribute is IOPS
HDD-backed volumes optimized for large streaming workloads where throughput (measured in MiB/s) is a better performance measure than IOPS
The following table describes the use cases and performance characteristics for each volume type:

Solid-State Drives (SSD)	Hard disk Drives (HDD)
Volume Type	General Purpose SSD (gp2)*	Provisioned IOPS SSD (io1)	Throughput Optimized HDD (st1)	Cold HDD (sc1)
Description	General purpose SSD volume that balances price and performance for a wide variety of transactional workloads	Highest-performance SSD volume designed for mission-critical applications	Low cost HDD volume designed for frequently accessed, throughput-intensive workloads	Lowest cost HDD volume designed for less frequently accessed workloads
Use Cases	
Recommended for most workloads
System boot volumes
Virtual desktops
Low-latency interactive apps
Development and test environments
Critical business applications that require sustained IOPS performance, or more than 10,000 IOPS or 160 MiB/s of throughput per volume
Large database workloads, such as:
MongoDB
Cassandra
Microsoft SQL Server
MySQL
PostgreSQL
Oracle
Streaming workloads requiring consistent, fast throughput at a low price
Big data
Data warehouses
Log processing
Cannot be a boot volume
Throughput-oriented storage for large volumes of data that is infrequently accessed
Scenarios where the lowest storage cost is important
Cannot be a boot volume
API Name	gp2	io1	st1	sc1
Volume Size	1 GiB - 16 TiB	4 GiB - 16 TiB	500 GiB - 16 TiB	500 GiB - 16 TiB
Max. IOPS**/Volume	10,000	20,000	500	250
Max. Throughput/Volume†	160 MiB/s	320 MiB/s	500 MiB/s	250 MiB/s
Max. IOPS/Instance	75,000	75,000	75,000	75,000
Max. Throughput/Instance	1,750 MB/s	1,750 MB/s	1,750 MB/s	1,750 MB/s
Dominant Performance Attribute	IOPS	IOPS	MiB/s	MiB/s
*Default volume type

**gp2/io1 based on 16KiB I/O size, st1/sc1 based on 1 MiB I/O size

† To achieve this throughput, you must have an instance that supports it, such as r3.8xlarge or x1.32xlarge.

The following table describes previous-generation EBS volume types. If you need higher performance or performance consistency than previous-generation volumes can provide, we recommend that you consider using General Purpose SSD (gp2) or other current volume types. For more information, see Previous Generation Volumes.

Previous Generation Volumes
Volume Type	EBS Magnetic
Description	Previous generation HDD
Use Cases	Workloads where data is infrequently accessed
API Name	standard
Volume Size	1 GiB-1 TiB
Max. IOPS/Volume	40-200
Max. Throughput/Volume	40-90 MiB/s
Max. IOPS/Instance	48,000
Max. Throughput/Instance	1,250 MiB/s
Dominant Performance Attribute	IOPS
Note
Linux AMIs require GPT partition tables and GRUB 2 for boot volumes 2 TiB (2048 GiB) or larger. Many Linux AMIs today use the MBR partitioning scheme, which only supports up to 2047 GiB boot volumes. If your instance does not boot with a boot volume that is 2 TiB or larger, the AMI you are using may be limited to a 2047 GiB boot volume size. Non-boot volumes do not have this limitation on Linux instances.
There are several factors that can affect the performance of EBS volumes, such as instance configuration, I/O characteristics, and workload demand. For more information about getting the most out of your EBS volumes, see Amazon EBS Volume Performance on Linux Instances.

For more information about pricing for these volume types, see Amazon EBS Pricing.

General Purpose SSD (gp2) Volumes

General Purpose SSD (gp2) volumes offer cost-effective storage that is ideal for a broad range of workloads. These volumes deliver single-digit millisecond latencies and the ability to burst to 3,000 IOPS for extended periods of time. Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 10,000 IOPS (at 3,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. AWS designs gp2 volumes to deliver the provisioned performance 99% of the time. A gp2 volume can range in size from 1 GiB to 16 TiB.

I/O Credits and Burst Performance

The performance of gp2 volumes is tied to volume size, which determines the baseline performance level of the volume and how quickly it accumulates I/O credits; larger volumes have higher baseline performance levels and accumulate I/O credits faster. I/O credits represent the available bandwidth that your gp2 volume can use to burst large amounts of I/O when more than the baseline performance is needed. The more credits your volume has for I/O, the more time it can burst beyond its baseline performance level and the better it performs when more performance is needed. The following diagram shows the burst-bucket behavior for gp2.


              gp2 burst bucket
            
Each volume receives an initial I/O credit balance of 5.4 million I/O credits, which is enough to sustain the maximum burst performance of 3,000 IOPS for 30 minutes. This initial credit balance is designed to provide a fast initial boot cycle for boot volumes and to provide a good bootstrapping experience for other applications. Volumes earn I/O credits at the baseline performance rate of 3 IOPS per GiB of volume size. For example, a 100 GiB gp2 volume has a baseline performance of 300 IOPS.


              Comparing baseline performance and burst IOPS
            
When your volume requires more than the baseline performance I/O level, it draws on I/O credits in the credit balance to burst to the required performance level, up to a maximum of 3,000 IOPS. Volumes larger than 1,000 GiB have a baseline performance that is equal or greater than the maximum burst performance, and their I/O credit balance never depletes. When your volume uses fewer I/O credits than it earns in a second, unused I/O credits are added to the I/O credit balance. The maximum I/O credit balance for a volume is equal to the initial credit balance (5.4 million I/O credits).

The following table lists several volume sizes and the associated baseline performance of the volume (which is also the rate at which it accumulates I/O credits), the burst duration at the 3,000 IOPS maximum (when starting with a full credit balance), and the time in seconds that the volume would take to refill an empty credit balance.

Volume size (GiB)

Baseline performance (IOPS)

Maximum burst duration @ 3,000 IOPS (seconds)

Seconds to fill empty credit balance

1
100
1862
54,000
100
300
2,000
18,000
214 (Min. size for max. throughput)
642
2,290
8,412
250
750
2,400	7,200
500
1,500
3,600
3,600
750
2,250
7,200
2,400
1,000
3,000
N/A*
N/A*
3,334 (Min. size for max. IOPS)
10,000
N/A*
N/A*
16,384 (16 TiB, max. volume size)
10,000
N/A*
N/A*
* Bursting and I/O credits are only relevant to volumes under 1,000 GiB, where burst performance exceeds baseline performance.

The burst duration of a volume is dependent on the size of the volume, the burst IOPS required, and the credit balance when the burst begins. This is shown in the following equation:

                             (Credit balance)
Burst duration  =  ------------------------------------
                   (Burst IOPS) - 3(Volume size in GiB)
What happens if I empty my I/O credit balance?

If your gp2 volume uses all of its I/O credit balance, the maximum IOPS performance of the volume will remain at the baseline IOPS performance level (the rate at which your volume earns credits) and the volume's maximum throughput is reduced to the baseline IOPS multiplied by the maximum I/O size. Throughput can never exceed 160 MiB/s. When I/O demand drops below the baseline level and unused credits are added to the I/O credit balance, the maximum IOPS performance of the volume will again exceed the baseline. For example, a 100 GiB gp2 volume with an empty credit balance has a baseline performance of 300 IOPS and a throughput limit of 75 MiB/s (300 I/O operations per second * 256 KiB per I/O operation = 75 MiB/s). The larger a volume is, the greater the baseline performance is and the faster it replenishes the credit balance. For more information about how IOPS are measured, see I/O Characteristics.

If you notice that your volume performance is frequently limited to the baseline level (due to an empty I/O credit balance), you should consider using a larger gp2 volume (with a higher baseline performance level) or switching to an io1 volume for workloads that require sustained IOPS performance greater than 10,000 IOPS.

For information about using CloudWatch metrics and alarms to monitor your burst bucket balance, see Monitoring the Burst Bucket Balance for gp2, st1, and sc1 Volumes.

Throughput Performance

The throughput limit for gp2 volumes is 128 MiB/s for volumes less than or equal to 170 GiB and 160 MiB/s for volumes over 170 GiB.

Provisioned IOPS SSD (io1) Volumes

Provisioned IOPS SSD (io1) volumes are designed to meet the needs of I/O-intensive workloads, particularly database workloads, that are sensitive to storage performance and consistency. Unlike gp2, which uses a bucket and credit model to calculate performance, an io1 volume allows you to specify a consistent IOPS rate when you create the volume, and Amazon EBS delivers within 10 percent of the provisioned IOPS performance 99.9 percent of the time over a given year.

An io1 volume can range in size from 4 GiB to 16 TiB and you can provision 100 up to 20,000 IOPS per volume. The maximum ratio of provisioned IOPS to requested volume size (in GiB) is 50:1. For example, a 100 GiB volume can be provisioned with up to 5,000 IOPS. Any volume 400 GiB in size or greater allows provisioning up to the 20,000 IOPS maximum.

The throughput limit of io1 volumes is 256 KiB for each IOPS provisioned, up to a maximum of 320 MiB/s (at 1,280 IOPS).


            Throughput limits for io1 volumes
          
Your per-I/O latency experience depends on the IOPS provisioned and your workload pattern. For the best per-I/O latency experience, we recommend that you provision an IOPS-to-GiB ratio greater than 2:1. For example, a 2,000 IOPS volume should be smaller than 1,000 GiB.

Note
Some AWS accounts created before 2012 might have access to Availability Zones in us-west-1 or ap-northeast-1 that do not support Provisioned IOPS SSD (io1) volumes. If you are unable to create an io1 volume (or launch an instance with an io1 volume in its block device mapping) in one of these regions, try a different Availability Zone in the region. You can verify that an Availability Zone supports io1 volumes by creating a 4 GiB io1 volume in that zone.
Throughput Optimized HDD (st1) Volumes

Throughput Optimized HDD (st1) volumes provide low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. This volume type is a good fit for large, sequential workloads such as Amazon EMR, ETL, data warehouses, and log processing. Bootable st1 volumes are not supported.

Note
This volume type is optimized for workloads involving large, sequential I/O, and we recommend that customers with workloads performing small, random I/O use gp2. For more information, see Inefficiency of Small Read/Writes on HDD.
Throughput Credits and Burst Performance

Like gp2, st1 uses a burst-bucket model for performance. Volume size determines the baseline throughput of your volume, which is the rate at which the volume accumulates throughput credits. Volume size also determines the burst throughput of your volume, which is the rate at which you can spend credits when they are available. Larger volumes have higher baseline and burst throughput. The more credits your volume has, the longer it will be able to drive I/O at the burst level.

The following diagram shows the burst-bucket behavior for st1.


              st1 burst bucket
            
Subject to throughput and throughput-credit caps, the available throughput of an st1 volume is expressed by the following formula:

(Volume size) x (Credit accumulation rate per TiB) = Throughput
For a 1 TiB st1 volume, burst throughput is limited to 250 MiB/s, the bucket fills with credits at 40 MiB/s, and it can hold up to 1 TiB-worth of credits.

Larger volumes scale these limits linearly, with throughput capped at a maximum of 500 MiB/s. After the bucket is depleted, throughput is limited to the baseline rate of 40 MiB/s per TiB.

On volume sizes ranging from 0.5 to 16 TiB, baseline throughput varies from 20 to a cap of 500 MiB/s, which is reached at 12.5 TiB as follows:

            40 MiB/s
12.5 TiB x ---------- = 500 MiB/s
             1 TiB                                                                 
Burst throughput varies from 125 MiB/s to a cap of 500 MiB/s, which is reached at 2 TiB as follows:

         250 MiB/s
2 TiB x ---------- = 500 MiB/s
          1 TiB                                                                 
The following table states the full range of base and burst throughput values for st1:

Volume Size (TiB)	ST1 Base Throughput (MiB/s)	ST1 Burst Throughput (MiB/s)
0.5	20	125
1	40	250
2	80	500
3	120	500
4	160	500
5	200	500
6	240	500
7	280	500
8	320	500
9	360	500
10	400	500
11	440	500
12	480	500
12.5	500	500
13	500	500
14	500	500
15	500	500
16	500	500
The following diagram plots the table values:


              Comparing st1 base and burst throughput
            
Note
When you create a snapshot of a Throughput Optimized HDD (st1) volume, performance may drop as far as the volume's baseline value while the snapshot is in progress.
For information about using CloudWatch metrics and alarms to monitor your burst bucket balance, see Monitoring the Burst Bucket Balance for gp2, st1, and sc1 Volumes.

Cold HDD (sc1) Volumes

Cold HDD (sc1) volumes provide low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. With a lower throughput limit than st1, sc1 is a good fit ideal for large, sequential cold-data workloads. If you require infrequent access to your data and are looking to save costs, sc1 provides inexpensive block storage. Bootable sc1 volumes are not supported.

Note
This volume type is optimized for workloads involving large, sequential I/O, and we recommend that customers with workloads performing small, random I/O use gp2. For more information, see Inefficiency of Small Read/Writes on HDD.
Throughput Credits and Burst Performance

Like gp2, sc1 uses a burst-bucket model for performance. Volume size determines the baseline throughput of your volume, which is the rate at which the volume accumulates throughput credits. Volume size also determines the burst throughput of your volume, which is the rate at which you can spend credits when they are available. Larger volumes have higher baseline and burst throughput. The more credits your volume has, the longer it will be able to drive I/O at the burst level.


              sc1 burst bucket
            
Subject to throughput and throughput-credit caps, the available throughput of an sc1 volume is expressed by the following formula:

(Volume size) x (Credit accumulation rate per TiB) = Throughput
For a 1 TiB sc1 volume, burst throughput is limited to 80 MiB/s, the bucket fills with credits at 12 MiB/s, and it can hold up to 1 TiB-worth of credits.

Larger volumes scale these limits linearly, with throughput capped at a maximum of 250 MiB/s. After the bucket is depleted, throughput is limited to the baseline rate of 12 MiB/s per TiB.

On volume sizes ranging from 0.5 to 16 TiB, baseline throughput varies from 6 MiB/s to a maximum of 192 MiB/s, which is reached at 16 TiB as follows:

           12 MiB/s
16 TiB x ---------- = 192 MiB/s
            1 TiB                                                                 
Burst throughput varies from 40 MiB/s to a cap of 250 MiB/s, which is reached at 3.125 TiB as follows:

             80 MiB/s
3.125 TiB x ----------- = 250 MiB/s
              1 TiB                                                                 
The following table states the full range of base and burst throughput values for sc1:

Volume Size (TiB)	SC1 Base Throughput (MiB/s)	SC1 Burst Throughput (MiB/s)
0.5	6	40
1	12	80
2	24	160
3	36	240
3.125	37.5	250
4	48	250
5	60	250
6	72	250
7	84	250
8	96	250
9	108	250
10	120	250
11	132	250
12	144	250
13	156	250
14	168	250
15	180	250
16	192	250
The following diagram plots the table values:


              Comparing sc1 base and burst throughput
            
Note
When you create a snapshot of a Cold HDD (sc1) volume, performance may drop as far as the volume's baseline value while the snapshot is in progress.
For information about using CloudWatch metrics and alarms to monitor your burst bucket balance, see Monitoring the Burst Bucket Balance for gp2, st1, and sc1 Volumes.

Magnetic (standard)

Magnetic volumes are backed by magnetic drives and are suited for workloads where data is accessed infrequently, and scenarios where low-cost storage for small volume sizes is important. These volumes deliver approximately 100 IOPS on average, with burst capability of up to hundreds of IOPS, and they can range in size from 1 GiB to 1 TiB.

Note
Magnetic is a Previous Generation Volume. For new applications, we recommend using one of the newer volume types. For more information, see Previous Generation Volumes.
For information about using CloudWatch metrics and alarms to monitor your burst bucket balance, see Monitoring the Burst Bucket Balance for gp2, st1, and sc1 Volumes.

Performance Considerations When Using HDD Volumes

For optimal throughput results using HDD volumes, plan your workloads with the following considerations in mind.

Throughput Optimized HDD vs. Cold HDD

The st1 and sc1 bucket sizes vary according to volume size, and a full bucket contains enough tokens for a full volume scan. However, larger st1 and sc1 volumes take longer for the volume scan to complete due to per-instance and per-volume throughput limits. Volumes attached to smaller instances are limited to the per-instance throughput rather than the st1 or sc1 throughput limits.

Both st1 and sc1 are designed for performance consistency of 90% of burst throughput 99% of the time. Non-compliant periods are approximately uniformly distributed, targeting 99% of expected total throughput each hour.

The following table shows ideal scan times for volumes of various size, assuming full buckets and sufficient instance throughput.

In general, scan times are expressed by this formula:

 Volume size
------------- = Scan time
 Throughput
For example, taking the performance consistency guarantees and other optimizations into account, an st1 customer with a 5 TiB volume can expect to complete a full volume scan in 2.91 to 3.27 hours.

   5 TiB            5 TiB
----------- = ------------------- = 10,486 s = 2.91 hours (optimal) 
 500 MiB/s     0.00047684 TiB/s


               2.91 hours
2.91 hours + -------------- = 3.27 hours (minimum expected)
              (0.90)(0.99) <-- From expected performance of 90% of burst 99% of the time
Similarly, an sc1 customer with a 5 TiB volume can expect to complete a full volume scan in 5.83 to 6.54 hours.

      5 TiB
------------------- = 20972 s = 5.83 hours (optimal) 
 0.000238418 TiB/s


  5.83 hours
-------------- = 6.54 hours (minimum expected)
 (0.90)(0.99)
Volume Size (TiB)	ST1 Scan Time with Burst (Hours)*	SC1 Scan Time with Burst (Hours)*
1	1.17	3.64
2	1.17	3.64
3	1.75	3.64
4	2.33	4.66
5	2.91	5.83
6	3.50	6.99
7	4.08	8.16
8	4.66	9.32
9	5.24	10.49
10	5.83	11.65
11	6.41	12.82
12	6.99	13.98
13	7.57	15.15
14	8.16	16.31
15	8.74	17.48
16	9.32	18.64
* These scan times assume an average queue depth (rounded to the nearest whole number) of four or more when performing 1 MiB of sequential I/O.

Therefore if you have a throughput-oriented workload that needs to complete scans quickly (up to 500 MiB/s), or requires several full volume scans a day, use st1. If you are optimizing for cost, your data is relatively infrequently accessed, and you don’t need more than 250 MiB/s of scanning performance, then use sc1.

Inefficiency of Small Read/Writes on HDD

The performance model for st1 and sc1 volumes is optimized for sequential I/Os, favoring high-throughput workloads, offering acceptable performance on workloads with mixed IOPS and throughput, and discouraging workloads with small, random I/O.

For example, an I/O request of 1 MiB or less counts as a 1 MiB I/O credit. However, if the I/Os are sequential, they are merged into 1 MiB I/O blocks and count only as a 1 MiB I/O credit.

Limitations on per-Instance Throughput

Throughput for st1 and sc1 volumes will always be the determined by the smaller of the following:

Throughput limits of the volume
Throughput limits of the instance
As for all Amazon EBS volumes, we recommend that you select an appropriate EBS-optimized EC2 instance in order to avoid network bottlenecks. For more information, see Amazon EBS-Optimized Instances.

Monitoring the Burst Bucket Balance for gp2, st1, and sc1 Volumes

You can monitor the burst-bucket level for for gp2, st1, and sc1 volumes using the EBS BurstBalance metric available in Amazon CloudWatch. This metric shows the percentage of I/O credits (for gp2) or throughput credits (for st1 and sc1) remaining in the burst bucket. For more information about the BurstBalance metric and other metrics related to I/O, see I/O Characteristics and Monitoring. CloudWatch also allows you to set an alarm that notifies you when the BurstBalance value falls to a certain level. For more information about CloudWatch alarms, see Creating Amazon CloudWatch Alarms.

Creating an Amazon EBS Volume

You can create an Amazon EBS volume that you can then attach to any EC2 instance within the same Availability Zone. You can choose to create an encrypted EBS volume, but encrypted volumes can only be attached to selected instance types. For more information, see Supported Instance Types. You can use IAM policies to enforce encryption on new volumes. For more information, see the example IAM policies in 4. Working with Volumes and 5: Launching Instances (RunInstances).

You can also create and attach EBS volumes when you launch instances by specifying a block device mapping. For more information, see Launching an Instance and Block Device Mapping. You can restore volumes from previously created snapshots. For more information, see Restoring an Amazon EBS Volume from a Snapshot.

You can apply tags to EBS volumes at the time of creation. With tagging you can simplify tracking of your Amazon EC2 resource inventory. Tagging on creation can be combined with an IAM policy to enforce tagging on new volumes. For more information, see Tagging Your Resources.

If you are creating a volume for a high-performance storage scenario, you should make sure to use a Provisioned IOPS SSD (io1) volume and attach it to an instance with enough bandwidth to support your application, such as an EBS-optimized instance or an instance with 10 Gigabit network connectivity. The same advice holds for Throughput Optimized HDD (st1) and Cold HDD (sc1) volumes. For more information, see Amazon EC2 Instance Configuration.

New EBS volumes receive their maximum performance the moment that they are available and do not require initialization (formerly known as pre-warming). However, storage blocks on volumes that were restored from snapshots must be initialized (pulled down from Amazon S3 and written to the volume) before you can access the block. This preliminary action takes time and can cause a significant increase in the latency of an I/O operation the first time each block is accessed. For most applications, amortizing this cost over the lifetime of the volume is acceptable. Performance is restored after the data is accessed once. For more information, see Initializing Amazon EBS Volumes.

To create an EBS volume using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region in which you would like to create your volume. This choice is important because some Amazon EC2 resources can be shared between regions, while others can't. For more information, see Resource Locations.

In the navigation pane, choose ELASTIC BLOCK STORE, Volumes.

Choose Create Volume.

For Volume Type, choose a volume type. For more information, see Amazon EBS Volume Types.

Note
Some AWS accounts created before 2012 might have access to Availability Zones in us-west-1 or ap-northeast-1 that do not support Provisioned IOPS SSD (io1) volumes. If you are unable to create an io1 volume (or launch an instance with an io1 volume in its block device mapping) in one of these regions, try a different Availability Zone in the region. You can verify that an Availability Zone supports io1 volumes by creating a 4 GiB io1 volume in that zone.
For Size (GiB), type the size of the volume.

With a Provisioned IOPS SSD volume, for IOPS, type the maximum number of input/output operations per second (IOPS) that the volume should support.

For Availability Zone, choose the Availability Zone in which to create the volume. EBS volumes can only be attached to EC2 instances within the same Availability Zone.

(Optional) To create an encrypted volume, select the Encrypted box and choose the master key you want to use when encrypting the volume. You can choose the default master key for your account, or you can choose any customer master key (CMK) that you have previously created using the AWS Key Management Service. Available keys are visible in the Master Key menu, or you can paste the full ARN of any key that you have access to. For more information, see the AWS Key Management Service Developer Guide.

Note
Encrypted volumes can only be attached to selected instance types. For more information, see Supported Instance Types.
(Optional) Choose Create additional tags to add tags to the volume. For each tag, provide a tag key and a tag value.

Choose Create Volume.

To create an EBS volume using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-volume (AWS CLI)
New-EC2Volume (AWS Tools for Windows PowerShell)

Restoring an Amazon EBS Volume from a Snapshot

You can restore an Amazon EBS volume with data from a snapshot stored in Amazon S3. You need to know the ID of the snapshot you wish to restore your volume from and you need to have access permissions for the snapshot. For more information on snapshots, see Amazon EBS Snapshots.

New volumes created from existing EBS snapshots load lazily in the background. This means that after a volume is created from a snapshot, there is no need to wait for all of the data to transfer from Amazon S3 to your EBS volume before your attached instance can start accessing the volume and all its data. If your instance accesses data that hasn't yet been loaded, the volume immediately downloads the requested data from Amazon S3, and continues loading the rest of the data in the background.

EBS volumes that are restored from encrypted snapshots are automatically encrypted. Encrypted volumes can only be attached to selected instance types. For more information, see Supported Instance Types.

Because of security constraints, you cannot directly restore an EBS volume from a shared encrypted snapshot that you do not own. You must first create a copy of the snapshot, which you will own. You can then restore a volume from that copy. For more information, see Amazon EBS Encryption.

New EBS volumes receive their maximum performance the moment that they are available and do not require initialization (formerly known as pre-warming). However, storage blocks on volumes that were restored from snapshots must be initialized (pulled down from Amazon S3 and written to the volume) before you can access the block. This preliminary action takes time and can cause a significant increase in the latency of an I/O operation the first time each block is accessed. Performance is restored after the data is accessed once.

For most applications, amortizing the initialization cost over the lifetime of the volume is acceptable. If you need to ensure that your restored volume always functions at peak capacity in production, you can force the immediate initialization of the entire volume using dd or fio. For more information, see Initializing Amazon EBS Volumes.

To restore an EBS volume from a snapshot using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region that your snapshot is located in.

If you need to restore the snapshot to a volume in a different region, you can copy your snapshot to the new region and then restore it to a volume in that region. For more information, see Copying an Amazon EBS Snapshot.

In the navigation pane, choose ELASTIC BLOCK STORE, Volumes.

Choose Create Volume.

For Volume Type, choose a volume type. For more information, see Amazon EBS Volume Types.

Note
Some AWS accounts created before 2012 might have access to Availability Zones in us-west-1 or ap-northeast-1 that do not support Provisioned IOPS SSD (io1) volumes. If you are unable to create an io1 volume (or launch an instance with an io1 volume in its block device mapping) in one of these regions, try a different Availability Zone in the region. You can verify that an Availability Zone supports io1 volumes by creating a 4 GiB io1 volume in that zone.
For Snapshot, start typing the ID or description of the snapshot from which you are restoring the volume, and choose it from the list of suggested options.

Volumes that are restored from encrypted snapshots can only be attached to instances that support Amazon EBS encryption. For more information, see Supported Instance Types.

For Size (GiB), type the size of the volume, or verify that the default size of the snapshot is adequate.

Note
If you specify both a volume size and a snapshot, the size must be equal to or greater than the snapshot size. When you select a volume type and a snapshot, the minimum and maximum sizes for the volume are shown next to Size. Any AWS Marketplace product codes from the snapshot are propagated to the volume.
With a Provisioned IOPS SSD volume, for IOPS, type the maximum number of input/output operations per second (IOPS) that the volume should support.

For Availability Zone list, choose the Availability Zone in which to create the volume. EBS volumes can only be attached to EC2 instances in the same Availability Zone.

(Optional) Choose Create additional tags to add tags to the volume. For each tag, provide a tag key and a tag value.

Choose Create Volume.

After you've restored a volume from a snapshot, you can attach it to an instance to begin using it. For more information, see Attaching an Amazon EBS Volume to an Instance.

If you restored a snapshot to a larger volume than the default for that snapshot, you must extend the file system on the volume to take advantage of the extra space. For more information, see Modifying the Size, IOPS, or Type of an EBS Volume on Linux.

To restore an EBS volume using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-volume (AWS CLI)
New-EC2Volume (AWS Tools for Windows PowerShell)

Attaching an Amazon EBS Volume to an Instance

You can attach an EBS volume to one of your instances that is in the same Availability Zone as the volume.

Prerequisites

Determine the device names that you'll use. For more information, see Device Naming on Linux Instances.
Determine how many volumes you can attach to your instance. For more information, see Instance Volume Limits.
If a volume is encrypted, it can only be attached to an instance that supports Amazon EBS encryption. For more information, see Supported Instance Types.
If a volume has an AWS Marketplace product code:
The volume can only be attached to a stopped instance.
You must be subscribed to the AWS Marketplace code that is on the volume.
The configuration (instance type, operating system) of the instance must support that specific AWS Marketplace code. For example, you cannot take a volume from a Windows instance and attach it to a Linux instance.
AWS Marketplace product codes are copied from the volume to the instance.
To attach an EBS volume to an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

Select a volume and choose Actions, Attach Volume.

In the Attach Volume dialog box, start typing the name or ID of the instance to attach the volume to for Instance, and select it from the list of suggestion options (only instances that are in the same Availability Zone as the volume are displayed).

You can keep the suggested device name, or enter a different supported device name.

Important
The block device driver for the instance assigns the actual volume name when mounting the volume, and the name assigned can be different from the name that Amazon EC2 recommends.
Choose Attach.

Connect to your instance and make the volume available. For more information, see Making an Amazon EBS Volume Available for Use.

To attach an EBS volume to an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

attach-volume (AWS CLI)
Add-EC2Volume (AWS Tools for Windows PowerShell)

Making an Amazon EBS Volume Available for Use

After you attach an Amazon EBS volume to your instance, it is exposed as a block device. You can format the volume with any file system and then mount it. After you make the EBS volume available for use, you can access it in the same ways that you access any other volume. Any data written to this file system is written to the EBS volume and is transparent to applications using the device.

Note that you can take snapshots of your EBS volume for backup purposes or to use as a baseline when you create another volume. For more information, see Amazon EBS Snapshots.

Making the Volume Available on Linux

Use the following procedure to make the volume available. Note that you can get directions for volumes on a Windows instance from Making the Volume Available on Windows in the Amazon EC2 User Guide for Windows Instances.

To make an EBS volume available for use on Linux

Connect to your instance using SSH. For more information, see Step 2: Connect to Your Instance.

Depending on the block device driver of the kernel, the device might be attached with a different name than what you specify. For example, if you specify a device name of /dev/sdh, your device might be renamed /dev/xvdh or /dev/hdh by the kernel; in most cases, the trailing letter remains the same. In some versions of Red Hat Enterprise Linux (and its variants, such as CentOS), even the trailing letter might also change (where /dev/sda could become /dev/xvde). In these cases, each device name trailing letter is incremented the same number of times. For example, /dev/sdb would become /dev/xvdf and /dev/sdc would become /dev/xvdg. Amazon Linux AMIs create a symbolic link with the name you specify at launch that points to the renamed device path, but other AMIs might behave differently.

Use the lsblk command to view your available disk devices and their mount points (if applicable) to help you determine the correct device name to use.

Copy
[ec2-user ~]$ lsblk
NAME  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvdf  202:80   0  100G  0 disk
xvda1 202:1    0    8G  0 disk /
The output of lsblk removes the /dev/ prefix from full device paths. In this example, /dev/xvda1 is mounted as the root device (note that MOUNTPOINT is listed as /, the root of the Linux file system hierarchy), and /dev/xvdf is attached, but it has not been mounted yet.

Determine whether you need to create a file system on the volume. New volumes are raw block devices, and you need to create a file system on them before you can mount and use them. Volumes that have been restored from snapshots likely have a file system on them already; if you create a new file system on top of an existing file system, the operation overwrites your data. Use the sudo file -s device command to list special information, such as file system type.

Copy
[ec2-user ~]$ sudo file -s /dev/xvdf
/dev/xvdf: data
If the output of the previous command shows simply data for the device, then there is no file system on the device and you need to create one. You can go on to Step 4. If you run this command on a device that contains a file system, then your output will be different.

Copy
[ec2-user ~]$ sudo file -s /dev/xvda1
/dev/xvda1: Linux rev 1.0 ext4 filesystem data, UUID=1701d228-e1bd-4094-a14c-8c64d6819362 (needs journal recovery) (extents) (large files) (huge files)
In the previous example, the device contains Linux rev 1.0 ext4 filesystem data, so this volume does not need a file system created (you can skip Step 4 if your output shows file system data).

(Conditional) Use the following command to create an ext4 file system on the volume. Substitute the device name (such as /dev/xvdf) for device_name. Depending on the requirements of your application or the limitations of your operating system, you can choose a different file system type, such as ext3 or XFS.

Warning
This step assumes that you're mounting an empty volume. If you're mounting a volume that already has data on it (for example, a volume that was restored from a snapshot), don't use mkfs before mounting the volume (skip to the next step instead). Otherwise, you'll format the volume and delete the existing data.
Copy
[ec2-user ~]$ sudo mkfs -t ext4 device_name
Use the following command to create a mount point directory for the volume. The mount point is where the volume is located in the file system tree and where you read and write files to after you mount the volume. Substitute a location for mount_point, such as /data.

Copy
[ec2-user ~]$ sudo mkdir mount_point
Use the following command to mount the volume at the location you just created.

Copy
[ec2-user ~]$ sudo mount device_name mount_point
(Optional) To mount this EBS volume on every system reboot, add an entry for the device to the /etc/fstab file.

Create a backup of your /etc/fstab file that you can use if you accidentally destroy or delete this file while you are editing it.

Copy
[ec2-user ~]$ sudo cp /etc/fstab /etc/fstab.orig
Open the /etc/fstab file using any text editor, such as nano or vim.

Note
You need to open the file as root or by using the sudo command.
Add a new line to the end of the file for your volume using the following format:

device_name  mount_point  file_system_type  fs_mntops  fs_freq  fs_passno  
The last three fields on this line are the file system mount options, the dump frequency of the file system, and the order of file system checks done at boot time. If you don't know what these values should be, then use the values in the following example for them (defaults,nofail 0 2). For more information on /etc/fstab entries, see the fstab manual page (by entering man fstab on the command line).

You can use the system's current device name (/dev/sda1, /dev/xvda1, etc.) in /etc/fstab, but we recommend using the device's 128-bit universally unique identifier (UUID) instead. System-declared block-device names may change under a variety of circumstances, but the UUID is assigned to a volume partition when it is formatted and persists throughout the partition's service life. By using the UUID, you reduce the chances of the block-device mapping in /etc/fstab leaving the system unbootable after a hardware reconfiguration.

To find the UUID of a device, first display the available devices:

Copy
[ec2-user ~]$ df
The following is example output:

Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/xvda1       8123812 1876888   6146676  24% /
devtmpfs          500712      56    500656   1% /dev
tmpfs             509724       0    509724   0% /dev/shm
Next, continuing this example, examine the output of either of two commands to find the UUID of /dev/xvda1:

sudo file -s /dev/xvda1
ls -al /dev/disk/by-uuid/
Assuming that you find /dev/xvda1 to have UUID de9a1ccd-a2dd-44f1-8be8-0123456abcdef, you would add the following entry to /etc/fstab to mount an ext4 file system at mount point /data:

Copy
UUID=de9a1ccd-a2dd-44f1-8be8-0123456abcdef       /data   ext4    defaults,nofail        0       2
Note
If you ever intend to boot your instance without this volume attached (for example, so this volume could move back and forth between different instances), you should add the nofail mount option that allows the instance to boot even if there are errors in mounting the volume. Debian derivatives, including Ubuntu versions earlier than 16.04, must also add the nobootwait mount option.
After you've added the new entry to /etc/fstab, you need to check that your entry works. Run the sudo mount -a command to mount all file systems in /etc/fstab.

Copy
[ec2-user ~]$ sudo mount -a
If the previous command does not produce an error, then your /etc/fstab file is OK and your file system will mount automatically at the next boot. If the command does produce any errors, examine the errors and try to correct your /etc/fstab.

Warning
Errors in the /etc/fstab file can render a system unbootable. Do not shut down a system that has errors in the /etc/fstab file.
(Optional) If you are unsure how to correct /etc/fstab errors, you can always restore your backup /etc/fstab file with the following command.

Copy
[ec2-user ~]$ sudo mv /etc/fstab.orig /etc/fstab
Review the file permissions of your new volume mount to make sure that your users and applications can write to the volume. For more information about file permissions, see File security at The Linux Documentation Project.

Viewing Volume Information

You can view descriptive information for your Amazon EBS volumes in a selected region at a time in the AWS Management Console. You can also view detailed information about a single volume, including the size, volume type, whether or not the volume is encrypted, which master key was used to encrypt the volume, and the specific instance to which the volume is attached.

View information about an EBS volume using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

To view more information about a volume, select it. In the details pane, you can inspect the information provided about the volume.

Learn what EBS (or other) volumes are attached to an Amazon EC2 instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

To view more information about an instance, select it.

In the details pane, you can inspect the information provided about root and block devices.

To view information about an EBS volume using the command line

You can use one of the following commands to view volume attributes. For more information, see Accessing Amazon EC2.

describe-volumes (AWS CLI)
Get-EC2Volume (AWS Tools for Windows PowerShell)

Monitoring the Status of Your Volumes

Amazon Web Services (AWS) automatically provides data, such as Amazon CloudWatch metrics and volume status checks, that you can use to monitor your Amazon Elastic Block Store (Amazon EBS) volumes.

Contents

Monitoring Volumes with CloudWatch
Monitoring Volumes with Status Checks
Monitoring Volume Events
Working with an Impaired Volume
Working with the AutoEnableIO Volume Attribute
Monitoring Volumes with CloudWatch

CloudWatch metrics are statistical data that you can use to view, analyze, and set alarms on the operational behavior of your volumes.

The following table describes the types of monitoring data available for your Amazon EBS volumes.

Type	Description
Basic
Data is available automatically in 5-minute periods at no charge. This includes data for the root device volumes for EBS-backed instances.
Detailed
Provisioned IOPS SSD (io1) volumes automatically send one-minute metrics to CloudWatch.
When you get data from CloudWatch, you can include a Period request parameter to specify the granularity of the returned data. This is different than the period that we use when we collect the data (5-minute periods). We recommend that you specify a period in your request that is equal to or larger than the collection period to ensure that the returned data is valid.

You can get the data using either the CloudWatch API or the Amazon EC2 console. The console takes the raw data from the CloudWatch API and displays a series of graphs based on the data. Depending on your needs, you might prefer to use either the data from the API or the graphs in the console.

Amazon EBS Metrics

Amazon Elastic Block Store (Amazon EBS) sends data points to CloudWatch for several metrics. Amazon EBS General Purpose SSD (gp2), Throughput Optimized HDD (st1), Cold HDD (sc1), and Magnetic (standard) volumes automatically send five-minute metrics to CloudWatch. Provisioned IOPS SSD (io1) volumes automatically send one-minute metrics to CloudWatch. For more information about how to monitor Amazon EBS, see Monitoring the Status of Your Volumes in the Amazon EC2 User Guide for Linux Instances.

Data is reported to CloudWatch only when the volume is active. If the volume is not attached, no data is reported.

The AWS/EBS namespace includes the following metrics.

Metric	Description
VolumeReadBytes

VolumeWriteBytes
Provides information on the I/O operations in a specified period of time. The Sum statistic reports the total number of bytes transferred during the period. The Average statistic reports the average size of each I/O operation during the period. The SampleCount statistic reports the total number of I/O operations during the period. The Minimum and Maximum statistics are not relevant for this metric. Data is only reported to Amazon CloudWatch when the volume is active. If the volume is idle, no data is reported to Amazon CloudWatch.

Units: Bytes
VolumeReadOps

VolumeWriteOps
The total number of I/O operations in a specified period of time.

Note
To calculate the average I/O operations per second (IOPS) for the period, divide the total operations in the period by the number of seconds in that period.
Units: Count
VolumeTotalReadTime

VolumeTotalWriteTime
The total number of seconds spent by all operations that completed in a specified period of time. If multiple requests are submitted at the same time, this total could be greater than the length of the period. For example, for a period of 5 minutes (300 seconds): if 700 operations completed during that period, and each operation took 1 second, the value would be 700 seconds.

Units: Seconds
VolumeIdleTime
The total number of seconds in a specified period of time when no read or write operations were submitted.

Units: Seconds
VolumeQueueLength
The number of read and write operation requests waiting to be completed in a specified period of time.

Units: Count
VolumeThroughputPercentage
Used with Provisioned IOPS SSD volumes only. The percentage of I/O operations per second (IOPS) delivered of the total IOPS provisioned for an Amazon EBS volume. Provisioned IOPS SSD volumes deliver within 10 percent of the provisioned IOPS performance 99.9 percent of the time over a given year.

Note
During a write, if there are no other pending I/O requests in a minute, the metric value will be 100 percent. Also, a volume's I/O performance may become degraded temporarily due to an action you have taken (e.g., creating a snapshot of a volume during peak usage, running the volume on a non-EBS-optimized instance, accessing data on the volume for the first time).
Units: Percent
VolumeConsumedReadWriteOps
Used with Provisioned IOPS SSD volumes only. The total amount of read and write operations (normalized to 256K capacity units) consumed in a specified period of time.

I/O operations that are smaller than 256K each count as 1 consumed IOPS. I/O operations that are larger than 256K are counted in 256K capacity units. For example, a 1024K I/O would count as 4 consumed IOPS.

Units: Count
BurstBalance
Used with General Purpose SSD (gp2), Throughput Optimized HDD (st1), and Cold HDD (sc1) volumes only. Provides information about the percentage of I/O credits (for gp2) or throughput credits (for st1 and sc1) remaining in the burst bucket.

Units: Percent
Dimensions for Amazon EBS Metrics

The only dimension that Amazon EBS sends to CloudWatch is the volume ID. This means that all available statistics are filtered by volume ID.

Graphs in the Amazon EC2 Console

After you create a volume, you can view the volume's monitoring graphs in the Amazon EC2 console. Select a volume on the Volumes page in the console and choose Monitoring. The following table lists the graphs that are displayed. The column on the right describes how the raw data metrics from the CloudWatch API are used to produce each graph. The period for all the graphs is 5 minutes.

Graph	Description using raw metrics
Read Bandwidth (KiB/s)
Sum(VolumeReadBytes) / Period / 1024
Write Bandwidth (KiB/s)
Sum(VolumeWriteBytes) / Period / 1024
Read Throughput (Ops/s)
Sum(VolumeReadOps) / Period
Write Throughput (Ops/s)
Sum(VolumeWriteOps) / Period
Avg Queue Length (ops)
Avg(VolumeQueueLength)
% Time Spent Idle
Sum(VolumeIdleTime) / Period * 100
Avg Read Size (KiB/op)
Avg(VolumeReadBytes) / 1024
Avg Write Size (KiB/op)
Avg(VolumeWriteBytes) / 1024
Avg Read Latency (ms/op)
Avg(VolumeTotalReadTime) * 1000
Avg Write Latency (ms/op)
Avg(VolumeTotalWriteTime) * 1000
For the average latency graphs and average size graphs, the average is calculated over the total number of operations (read or write, whichever is applicable to the graph) that completed during the period.

Monitoring Volumes with Status Checks

Volume status checks enable you to better understand, track, and manage potential inconsistencies in the data on an Amazon EBS volume. They are designed to provide you with the information that you need to determine whether your Amazon EBS volumes are impaired, and to help you control how a potentially inconsistent volume is handled.

Volume status checks are automated tests that run every 5 minutes and return a pass or fail status. If all checks pass, the status of the volume is ok. If a check fails, the status of the volume is impaired. If the status is insufficient-data, the checks may still be in progress on the volume. You can view the results of volume status checks to identify any impaired volumes and take any necessary actions.

When Amazon EBS determines that a volume's data is potentially inconsistent, the default is that it disables I/O to the volume from any attached EC2 instances, which helps to prevent data corruption. After I/O is disabled, the next volume status check fails, and the volume status is impaired. In addition, you'll see an event that lets you know that I/O is disabled, and that you can resolve the impaired status of the volume by enabling I/O to the volume. We wait until you enable I/O to give you the opportunity to decide whether to continue to let your instances use the volume, or to run a consistency check using a command, such as fsck (Linux) or chkdsk (Windows), before doing so.

Note
Volume status is based on the volume status checks, and does not reflect the volume state. Therefore, volume status does not indicate volumes in the error state (for example, when a volume is incapable of accepting I/O.)
If the consistency of a particular volume is not a concern for you, and you'd prefer that the volume be made available immediately if it's impaired, you can override the default behavior by configuring the volume to automatically enable I/O. If you enable the AutoEnableIO volume attribute, the volume status check continues to pass. In addition, you'll see an event that lets you know that the volume was determined to be potentially inconsistent, but that its I/O was automatically enabled. This enables you to check the volume's consistency or replace it at a later time.

The I/O performance status check compares actual volume performance to the expected performance of a volume and alerts you if the volume is performing below expectations. This status check is only available for io1 volumes that are attached to an instance and is not valid for General Purpose SSD (gp2), Throughput Optimized HDD (st1), Cold HDD (sc1), or Magnetic (standard) volumes. The I/O performance status check is performed once every minute and CloudWatch collects this data every 5 minutes, so it may take up to 5 minutes from the moment you attach a io1 volume to an instance for this check to report the I/O performance status.

Important
While initializing io1 volumes that were restored from snapshots, the performance of the volume may drop below 50 percent of its expected level, which causes the volume to display a warning state in the I/O Performance status check. This is expected, and you can ignore the warning state on io1 volumes while you are initializing them. For more information, see Initializing Amazon EBS Volumes.
The following table lists statuses for Amazon EBS volumes.

Volume status	I/O enabled status	I/O performance status (only available for Provisioned IOPS volumes)
ok
Enabled (I/O Enabled or I/O Auto-Enabled)
Normal (Volume performance is as expected)
warning
Enabled (I/O Enabled or I/O Auto-Enabled)
Degraded (Volume performance is below expectations)

Severely Degraded (Volume performance is well below expectations)
impaired
Enabled (I/O Enabled or I/O Auto-Enabled)

Disabled (Volume is offline and pending recovery, or is waiting for the user to enable I/O)
Stalled (Volume performance is severely impacted)

Not Available (Unable to determine I/O performance because I/O is disabled)
insufficient-data
Enabled (I/O Enabled or I/O Auto-Enabled)

Insufficient Data
Insufficient Data
To view and work with status checks, you can use the Amazon EC2 console, the API, or the command line interface.

To view status checks in the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

On the EBS Volumes page, use the Volume Status column lists the operational status of each volume.

To view an individual volume's status, select the volume, and choose Status Checks.


                        Viewing EBS volume status
                    
If you have a volume with a failed status check (status is impaired), see Working with an Impaired Volume.

Alternatively, you can use the Events pane to view all events for your instances and volumes in a single pane. For more information, see Monitoring Volume Events.

To view volume status information with the command line

You can use one of the following commands to view the status of your Amazon EBS volumes. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-volume-status (AWS CLI)
Get-EC2VolumeStatus (AWS Tools for Windows PowerShell)
Monitoring Volume Events

When Amazon EBS determines that a volume's data is potentially inconsistent, it disables I/O to the volume from any attached EC2 instances by default. This causes the volume status check to fail, and creates a volume status event that indicates the cause of the failure.

To automatically enable I/O on a volume with potential data inconsistencies, change the setting of the AutoEnableIO volume attribute. For more information about changing this attribute, see Working with an Impaired Volume.

Each event includes a start time that indicates the time at which the event occurred, and a duration that indicates how long I/O for the volume was disabled. The end time is added to the event when I/O for the volume is enabled.

Volume status events include one of the following descriptions:

Awaiting Action: Enable IO
Volume data is potentially inconsistent. I/O is disabled for the volume until you explicitly enable it. The event description changes to IO Enabled after you explicitly enable I/O.

IO Enabled
I/O operations were explicitly enabled for this volume.

IO Auto-Enabled
I/O operations were automatically enabled on this volume after an event occurred. We recommend that you check for data inconsistencies before continuing to use the data.

Normal
For io1 volumes only. Volume performance is as expected.

Degraded
For io1 volumes only. Volume performance is below expectations.

Severely Degraded
For io1 volumes only. Volume performance is well below expectations.

Stalled
For io1 volumes only. Volume performance is severely impacted.

You can view events for your volumes using the Amazon EC2 console, the API, or the command line interface.

To view events for your volumes in the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Events.

All instances and volumes that have events are listed. You can filter by volume to view only volume status. You can also filter on specific status types.

Select a volume to view its specific event.


                        Viewing volume events
                    
If you have a volume where I/O is disabled, see Working with an Impaired Volume. If you have a volume where I/O performance is below normal, this might be a temporary condition due to an action you have taken (e.g., creating a snapshot of a volume during peak usage, running the volume on an instance that cannot support the I/O bandwidth required, accessing data on the volume for the first time, etc.).

To view events for your volumes with the command line

You can use one of the following commands to view event information for your Amazon EBS volumes. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-volume-status (AWS CLI)
Get-EC2VolumeStatus (AWS Tools for Windows PowerShell)
Working with an Impaired Volume

This section discusses your options if a volume is impaired because the volume's data is potentially inconsistent.

Options

Option 1: Perform a Consistency Check on the Volume Attached to its Instance
Option 2: Perform a Consistency Check on the Volume Using Another Instance
Option 3: Delete the Volume If You No Longer Need It
Option 1: Perform a Consistency Check on the Volume Attached to its Instance

The simplest option is to enable I/O and then perform a data consistency check on the volume while the volume is still attached to its Amazon EC2 instance.

To perform a consistency check on an attached volume

Stop any applications from using the volume.

Enable I/O on the volume.

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

Select the volume on which to enable I/O operations.

In the details pane, choose Enable Volume IO.


                                    Enable IO
                                
In Enable Volume IO, choose Yes, Enable.

Check the data on the volume.

Run the fsck (Linux) or chkdsk (Windows) command.

(Optional) Review any available application or system logs for relevant error messages.

If the volume has been impaired for more than 20 minutes you can contact support. Choose Troubleshoot, and then on the Troubleshoot Status Checks dialog box, choose Contact Support to submit a support case.

To enable I/O for a volume with the command line

You can use one of the following commands to view event information for your Amazon EBS volumes. For more information about these command line interfaces, see Accessing Amazon EC2.

enable-volume-io (AWS CLI)
Enable-EC2VolumeIO (AWS Tools for Windows PowerShell)
Option 2: Perform a Consistency Check on the Volume Using Another Instance

Use the following procedure to check the volume outside your production environment.

Important
This procedure may cause the loss of write I/Os that were suspended when volume I/O was disabled.
To perform a consistency check on a volume in isolation

Stop any applications from using the volume.

Detach the volume from the instance.

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

Select the volume to detach.

Choose Actions, Force Detach Volume. You'll be prompted for confirmation.

Enable I/O on the volume.

In the navigation pane, choose Volumes.

Select the volume that you detached in the previous step.

In the details pane, choose Enable Volume IO.


                                    Enable IO
                                
In the Enable Volume IO dialog box, choose Yes, Enable.

Attach the volume to another instance. For information, see Launch Your Instance and Attaching an Amazon EBS Volume to an Instance.

Check the data on the volume.

Run the fsck (Linux) or chkdsk (Windows) command.

(Optional) Review any available application or system logs for relevant error messages.

If the volume has been impaired for more than 20 minutes, you can contact support. Choose Troubleshoot, and then in the troubleshooting dialog box, choose Contact Support to submit a support case.

To enable I/O for a volume with the command line

You can use one of the following commands to view event information for your Amazon EBS volumes. For more information about these command line interfaces, see Accessing Amazon EC2.

enable-volume-io (AWS CLI)
Enable-EC2VolumeIO (AWS Tools for Windows PowerShell)
Option 3: Delete the Volume If You No Longer Need It

If you want to remove the volume from your environment, simply delete it. For information about deleting a volume, see Deleting an Amazon EBS Volume.

If you have a recent snapshot that backs up the data on the volume, you can create a new volume from the snapshot. For information about creating a volume from a snapshot, see Restoring an Amazon EBS Volume from a Snapshot.

Working with the AutoEnableIO Volume Attribute

When Amazon EBS determines that a volume's data is potentially inconsistent, it disables I/O to the volume from any attached EC2 instances by default. This causes the volume status check to fail, and creates a volume status event that indicates the cause of the failure. If the consistency of a particular volume is not a concern, and you prefer that the volume be made available immediately if it's impaired, you can override the default behavior by configuring the volume to automatically enable I/O. If you enable the AutoEnableIO volume attribute, I/O between the volume and the instance is automatically re-enabled and the volume's status check will pass. In addition, you'll see an event that lets you know that the volume was in a potentially inconsistent state, but that its I/O was automatically enabled. When this event occurs, you should check the volume's consistency and replace it if necessary. For more information, see Monitoring Volume Events.

This section explains how to view and modify the AutoEnableIO attribute of a volume using the Amazon EC2 console, the command line interface, or the API.

To view the AutoEnableIO attribute of a volume in the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

Select the volume.

In the lower pane, choose Status Checks.

In the Status Checks tab, Auto-Enable IO displays the current setting for your volume, either Enabled or Disabled.


                        View Auto-Enable IO
                    
To modify the AutoEnableIO attribute of a volume in the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

Select the volume.

At the top of the Volumes page, choose Actions.

Choose Change Auto-Enable IO Setting.


                        Change Auto-Enable IO setting
                    
In the Change Auto-Enable IO Setting dialog box, select the Auto-Enable Volume IO option to automatically enable I/O for an impaired volume. To disable the feature, clear the option.


                        Modify Auto-Enable IO setting
                    
Choose Save.

Alternatively, instead of completing steps 4-6 in the previous procedure, choose Status Checks, Edit.

To view or modify the AutoEnableIO attribute of a volume with the command line

You can use one of the following commands to view the AutoEnableIO attribute of your Amazon EBS volumes. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-volume-attribute (AWS CLI)
Get-EC2VolumeAttribute (AWS Tools for Windows PowerShell)
To modify the AutoEnableIO attribute of a volume, you can use one of the commands below.

modify-volume-attribute (AWS CLI)
Edit-EC2VolumeAttribute (AWS Tools for Windows PowerShell)

Detaching an Amazon EBS Volume from an Instance

You can detach an Amazon EBS volume from an instance explicitly or by terminating the instance. However, if the instance is running, you must first unmount the volume from the instance.

If an EBS volume is the root device of an instance, you must stop the instance before you can detach the volume.

When a volume with an AWS Marketplace product code is detached from an instance, the product code is no longer associated with the instance.

Important
After you detach a volume, you are still charged for volume storage as long as the storage amount exceeds the limit of the AWS Free Tier. You must delete a volume to avoid incurring further charges. For more information, see Deleting an Amazon EBS Volume.
This example unmounts the volume and then explicitly detaches it from the instance. This is useful when you want to terminate an instance or attach a volume to a different instance. To verify that the volume is no longer attached to the instance, see Viewing Volume Information.

Note that you can reattach a volume that you detached (without unmounting it), but it might not get the same mount point and the data on the volume might be out of sync if there were writes to the volume in progress when it was detached.

To detach an EBS volume using the console

Use the following command to unmount the /dev/sdh device.

Copy
[ec2-user ~]$ umount -d /dev/sdh
Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

Select a volume and choose Actions, Detach Volume.

In the confirmation dialog box, choose Yes, Detach.

To detach an EBS volume from an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

detach-volume (AWS CLI)
Dismount-EC2Volume (AWS Tools for Windows PowerShell)
Troubleshooting

The following are common problems encountered when detaching volumes, and how to resolve them.

Note
To guard against the possibility of data loss, take a snapshot of your volume before attempting to unmount it. Forced detachment of a stuck volume can cause damage to the file system or the data it contains or an inability to attach a new volume using the same device name, unless you reboot the instance.
If you encounter problems while detaching a volume through the Amazon EC2 console, it may be helpful to use the describe-volumes CLI command to diagnose the issue. For more information, see describe-volumes>.
If your volume stays in the detaching state, you can force the detachment by choosing Force Detach. Use this option only as a last resort to detach a volume from a failed instance, or if you are detaching a volume with the intention of deleting it. The instance doesn't get an opportunity to flush file system caches or file system metadata. If you use this option, you must perform file system check and repair procedures.
If you've tried to force the volume to detach multiple times over several minutes and it stays in the detaching state, you can post a request for help to the Amazon EC2 forum. To help expedite a resolution, include the volume ID and describe the steps that you've already taken.
When you attempt to detach a volume that is still mounted, the volume can become stuck in the busy state while it is trying to detach. The following output from describe-volumes shows an example of this condition:
Copy
aws ec2 describe-volumes --region us-west-2 --volume-ids vol-1234abcd 
{
    "Volumes": [
        {
            "AvailabilityZone": "us-west-2b",
            "Attachments": [
                {
                    "AttachTime": "2016-07-21T23:44:52.000Z",
                    "InstanceId": "i-fedc9876",
                    "VolumeId": "vol-1234abcd",
                    "State": "busy",
                    "DeleteOnTermination": false,
                    "Device": "/dev/sdf"
                }
....
When you encounter this state, detachment can be delayed indefinitely until you unmount the volume, force detachment, reboot the instance, or all three.

Deleting an Amazon EBS Volume

After you no longer need an Amazon EBS volume, you can delete it. After deletion, its data is gone and the volume can't be attached to any instance. However, before deletion, you can store a snapshot of the volume, which you can use to re-create the volume later.

To delete a volume, it must be in the available state (not attached to an instance). For more information, see Detaching an Amazon EBS Volume from an Instance.

To delete an EBS volume using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Volumes.

Select a volume and choose Actions, Delete Volume.

In the confirmation dialog box, choose Yes, Delete.

To delete an EBS volume using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

delete-volume (AWS CLI)
Remove-EC2Volume (AWS Tools for Windows PowerShell)

Modifying the Size, IOPS, or Type of an EBS Volume on Linux

If your Amazon EBS volume is attached to a current generation EC2 instance type, you can increase its size, change its volume type, or (for an io1 volume) adjust its IOPS performance, all without detaching it. You can apply these changes to detached volumes as well. For more information about the current generation instance types, see Current Generation Instances.

If you are using a previous generation instance type, or if you encounter an error while attempting a volume modification, follow the procedures in Appendix: Starting and Stopping an Instance to Modify an EBS Volume.

In general, the following steps are involved in modifying a volume:

Issue the modification command. For more information, see Modifying an EBS Volume from the Console and Modifying an EBS Volume from the Command Line.

Monitor the progress of the modification. For more information, see Monitoring the Progress of Volume Modifications.

If the size of the volume was modified, extend the volume's file system to take advantage of the increased storage capacity. For more information, see Extending a Linux File System after Resizing the Volume .

Additionally, you can use Amazon CloudWatch Events and AWS CloudFormation to automate the actions associated with volume modification.

There is no charge to modify the configuration of a volume. You are charged at the new volume configuration price after a modification starts. For more information, see the Amazon Elastic Block Store section on the Amazon EBS Pricing page.

For more information, see Considerations for Modifying EBS Volumes.

Important
Before modifying a volume that contains valuable data, it is a best practice to create a snapshot of the volume in case you need to roll back your changes. For information about EBS snapshots, see Creating an Amazon EBS Snapshot.
Modifying an EBS Volume from the Console

The following procedure shows how to apply available volume modifications from the Amazon EC2 console.

To modify an EBS volume using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Volumes, select the volume to modify and then choose Actions, Modify Volume.

The Modify Volume window displays the volume ID and the volume's current configuration, including type, size, and IOPS. You can change any or all of these settings in a single action. Set new configuration values as follows:

To modify the type, choose a value for Volume Type.
To modify the size, enter an allowed integer value for Size.
If you chose Provisioned IOPS (IO1) as your volume type, enter an allowed integer value for IOPS.
After you have specified all of the modifications to apply, choose Modify, Yes.

Modifying volume size has no practical effect until you also extend the volume's file system to make use of the new storage capacity. For more information, see Extending a Linux File System after Resizing the Volume.

Modifying an EBS Volume from the Command Line

The following example demonstrates how an EBS volume can be modified from the command line using the AWS CLI. Depending on your default configuration, you may need to specify information such as region and availability zone. The ID of the source volume being modified is required, and you must have appropriate permissions to carry out the action. When an io1 volume is the modification target, you must specify its level of provisioned IOPS. Multiple modification actions (to change capacity, IOPS, or type) may be performed in a single command.

For example, an EBS volume is configured as follows:

Volume ID: vol-11111111111111111
Volume size: 100 GiB
Volume type: gp2
You can change the volume configuration to the following:

Volume size: 200 GiB
Volume type: io1
Provisioning level: 10,000 IOPS
Apply the above modifications with the following command:

Copy
aws ec2 modify-volume --region us-east-1 --volume-id vol-11111111111111111 --size 200 --volume-type io1 --iops 10000
The command yields output similar to the following:

{
    "VolumeModification": {
        "TargetSize": 200,
        "TargetVolumeType": "io1",
        "ModificationState": "modifying",
        "VolumeId": "vol-11111111111111111",
        "TargetIops": 10000,
        "StartTime": "2017-01-19T22:21:02.959Z",
        "Progress": 0,
        "OriginalVolumeType": "gp2",
        "OriginalIops": 300,
        "OriginalSize": 100
    }
}
Note
Modifying volume size has no practical effect until you also extend the volume's file system to make use of the new storage capacity. For more information, see Extending a Linux File System after Resizing the Volume.
Monitoring the Progress of Volume Modifications

An EBS volume being modified goes through a sequence of states. After you issue a ModifyVolume directive, whether from the console, CLI, API, or SDK, the volume enters first the Modifying state, then the Optimizing state, and finally the Complete state. At this point, the volume is ready to be further modified. Rarely, a transient AWS fault can result in the Failed state. If this occurs, retry the modification.

Size changes usually take a few seconds to complete and take effect after a volume is in the Optimizing state.

Performance (IOPS) changes can take from a few minutes to a few hours to complete and are dependent on the configuration change being made.

It may take up to 24 hours for a new configuration to take effect, and in some cases more, such as when the volume has not been fully initialized. Typically, a fully used 1 TiB volume takes about 6 hours to migrate to a new performance configuration.

While the volume is in the optimizing state, your volume performance will be in between the source and target configuration specifications. Transitional volume performance will be no less than the source volume performance. If you are downgrading IOPS, transitional volume performance will be no less than the target volume performance.

You can monitor the progress of a modification by inspecting the AWS Management Console, by querying the volume's state with the AWS EC2 API/CLI, or by accessing metrics sent to Amazon CloudWatch Events. The following procedures demonstrate these approaches.

To monitor progress of a modification from the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Volumes, and select the volume to inspect. The volume's status is displayed in the State column. In the example below, the modification state is completed. This state information is also displayed in the State field of the details pane.

Open the information icon next to the State field to display complete before and after information about the most recent modification action, as illustrated below.


Example To monitor progress of a modification from the command line

Use describe-volumes-modifications to view the progress of the modifications. In this example, volume vol-11111111111111111 from above and another volume, vol-22222222222222222, are called.

Copy
aws ec2 describe-volumes-modifications --region us-east-1 --volume-id vol-11111111111111111 vol-22222222222222222
The command returns one or more VolumesModification objects. The following is example output. The first object is nearly identical to the original modify-volume command output shown above. No additional modifications have been applied, however.

{
    "VolumesModifications": [
        {
            "TargetSize": 200,
            "TargetVolumeType": "io1",
            "ModificationState": "modifying",
            "VolumeId": "vol-11111111111111111",
            "TargetIops": 10000,
            "StartTime": "2017-01-19T22:21:02.959Z",
            "Progress": 0,
            "OriginalVolumeType": "gp2",
            "OriginalIops": 300,
            "OriginalSize": 100
        },
        {
            "TargetSize": 2000,
            "TargetVolumeType": "sc1",
            "ModificationState": "modifying",
            "VolumeId": "vol-22222222222222222",
            "StartTime": "2017-01-19T22:23:22.158Z",
            "Progress": 0,
            "OriginalVolumeType": "gp2",
            "OriginalIops": 300,
            "OriginalSize": 1000
        }
    ]
}
The next example queries for all volumes in a region with a modification state of either optimizing or completed, and then filters and formats the results to show only modifications that were initiated on or after February 1, 2017:

Copy
aws ec2 describe-volumes-modifications --filters Name=modification-state,Values="optimizing","completed" --region us-east-1 --query "VolumesModifications[?StartTime>='2017-02-01'].{ID:VolumeId,STATE:ModificationState}"
In this case the query returns information about two volumes:

[
    {
        "STATE": "optimizing",
        "ID": "vol-06397e7a0eEXAMPLE"
    },
    {
        "STATE": "completed",
        "ID": "vol-bEXAMPLE"
    }
]
To monitor progress of a modification with CloudWatch Events

With CloudWatch Events, you can create a notification rule for volume modification events to send a text message or execute a Lambda function.

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

Choose Events, Create rule.

For Build event pattern to match events by service, choose Custom event pattern.

For Build custom event pattern , replace the contents with the following code:

Copy
{
  "source": [
    "aws.ec2"
  ],
  "detail-type": [
    "EBS Volume Notification"
  ],
  "detail": {
    "event": [
      "modifyVolume"
    ]
  }
}
Choose Save when done.

Typical event output should look like the following:

Body:
{
   "version": "0",
   "id": "1ea2ace2-7790-46ed-99ab-d07a8bd68685",
   "detail-type": "EBS Volume Notification",
   "source": "aws.ec2",
   "account": "065441870323",
   "time": "2017-01-12T21:09:07Z",
   "region": "us-east-1",
   "resources": [
      "arn:aws:ec2:us-east-1:065441870323:volume/vol-03a55cf56513fa1b6"
   ],
   "detail": {
      "result": "optimizing",
      "cause": "",
      "event": "modifyVolume",
      "request-id": "auto-58c08bad-d90b-11e6-a309-b51ed35473f8"
   }
}
You can use your rule to generate a notification message with Amazon SNS or to invoke an AWS Lambda function in response to matching events.

Extending a Linux File System after Resizing the Volume

Use a file system–specific command to resize the file system to the larger size of the new volume. These commands work even if the volume to extend is the root volume. For ext2, ext3, and ext4 file systems, this command is resize2fs. For XFS file systems, this command is xfs_growfs. For other file systems, refer to the specific documentation for those file systems for instructions on extending them.

If you are unsure of which file system you are using, you can use the file -s command to list the file system data for a device. The following example shows a Linux ext4 file system and an SGI XFS file system.

Copy
[ec2-user ~]$ sudo file -s /dev/xvd*
/dev/xvda1: Linux rev 1.0 ext4 filesystem data ...
/dev/xvdf:  SGI XFS filesystem data ...
Note
If the volume you are extending has been partitioned, you need to increase the size of the partition before you can resize the file system. You can also allocate additional partitions at this time. For more information, see Expanding a Linux Partition.
You can begin resizing the file system as soon as the volume enters the Optimizing state.

Important
Before extending a file system that contains valuable data, it is a best practice to create a snapshot of the volume that contains it in case you need to roll back your changes. For information about EBS snapshots, see Creating an Amazon EBS Snapshot.
To check if your volume partition needs resizing

Use the lsblk command to list the block devices attached to your instance. The example below shows three volumes: /dev/xvda, /dev/xvdb, and /dev/xvdf.

Copy
[ec2-user ~]$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  30G  0 disk
└─xvda1 202:1    0  30G  0 part /
xvdb    202:16   0  30G  0 disk /mnt
xvdf    202:80   0  35G  0 disk
└─xvdf1 202:81   0   8G  0 part
The root volume, /dev/xvda1, is a partition on /dev/xvda. Notice that they are both 30 GiB in size. In this case, the partition occupies all of the room on the device, so it does not need resizing.

The volume /dev/xvdb is not partitioned at all, so it does not need resizing.

However, /dev/xvdf1 is an 8 GiB partition on a 35 GiB device and there are no other partitions on the volume. In this case, the partition must be resized in order to use the remaining space on the volume. For more information, see Expanding a Linux Partition. After you resize the partition, you can follow the next procedure to extend the file system to occupy all of the space on the partition.

To extend a Linux file system

Log in to your Linux instance using an SSH client. For more information about connecting to a Linux instance, see Connecting to Your Linux Instance Using SSH.

Use the df -h command to report the existing file system disk space usage. In this new example, /dev/xvda1 device has already been expanded to 35 GiB, but the operating system still sees only an original 8 GiB ext4 file system. Similarly, the /dev/xvdf device has been expanded to 35 GiB, but the operating system still only sees an original 1 GiB XFS file system.

Copy
[ec2-user ~]$ df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/xvda1            8.0G  943M  6.9G  12% /
tmpfs                 1.9G     0  1.9G   0% /dev/shm
/dev/xvdf            1014M   33M  982M   4% /mnt
Expand the modified partition using growpart:

Copy
$sudo growpart /dev/xvdf 1
CHANGED: disk=/dev/xvdf partition=1: start=4096 old: size=16773086,end=16777182 new: size=73396190,end=73400286
A look at the lsblk output confirms that the partition /dev/xvdf1 now fills the available space on the volume /dev/xvdf:

Copy
[ec2-user ~]$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
...
xvdf    202:80   0  35G  0 disk
└─xvdf1 202:81   0  35G  0 part
Use a file system-specific command to resize each file system to the new volume capacity.

For a Linux ext2, ext3, or ext4 file system, use the following command, substituting the device name to extend:

Copy
[ec2-user ~]$ sudo resize2fs /dev/xvdf1
resize2fs 1.42.3 (14-May-2012)
old_desc_blocks = 1, new_desc_blocks = 3
The filesystem on /dev/xvdf1 is now 9174523 blocks long.
For an XFS file system, first install the XFS userspace tools:

Copy
[ec2-user ~]$ sudo yum install xfsprogs
Then use the following command, substituting the mount point of the file system (XFS file systems must be mounted to resize them):

Copy
[ec2-user ~]$ sudo xfs_growfs -d /mnt
meta-data=/dev/xvdf              isize=256    agcount=4, agsize=65536 blks
         =                       sectsz=512   attr=2
data     =                       bsize=4096   blocks=262144, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0
log      =internal               bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 262144 to 26214400
Note
If you receive an xfsctl failed: Cannot allocate memory error, you may need to update the Linux kernel on your instance. For more information, refer to your specific operating system documentation.
If you receive a The filesystem is already nnnnnnn blocks long. Nothing to do! error, see Expanding a Linux Partition.
Use the df -h command to report the existing file system disk space usage, in this example showing 70 GiB on the ext4 file system and 100 GiB on the XFS file system:

Copy
# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/xvda1             70G  951M   69G   2% /
tmpfs                 1.9G     0  1.9G   0% /dev/shm
/dev/xvdf             100G   45M  100G   1% /mnt
Tip
If the increased available space on your volume remains invisible to the system, try re-initializing the volume as described in Initializing Amazon EBS Volumes.
Appendix: Starting and Stopping an Instance to Modify an EBS Volume

If you are using a previous generation Amazon EC2 instance and you need to modify the root (boot) volume, you must stop the instance, apply the modifications, and then restart the instance. The procedure described here can be used to modify any EBS volume on any instance type.

When you stop and start an instance, be aware of the following:

If your instance is running in a VPC and has a public IPv4 address, we release the address and give it a new public IPv4 address. The instance retains its private IPv4 addresses and any Elastic IP addresses.
If your instance is running in EC2-Classic, we give it new public and private IPv4 addresses, and disassociate any Elastic IP address that's associated with the instance. You must re-associate any Elastic IP address after you restart your instance.
If your instance is in an Auto Scaling group, Auto Scaling marks the stopped instance as unhealthy, and may terminate it and launch a replacement instance. To prevent this, you can temporarily suspend the Auto Scaling processes for the group. For more information, see Suspend and Resume Auto Scaling Processes in the Auto Scaling User Guide.
To modify the root volume of an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances and select the instance with the volume to expand.

Verify that Shutdown Behavior is set to Stop and not Terminate.

Select the instance.

From the context (right-click) menu, choose Instance Settings, Change Shutdown Behavior.

If Shutdown behavior is set to Terminate, choose Stop, Apply.

If Shutdown behavior is already set to Stop, choose Cancel.

Stop the instance. For more information, see Stopping and Starting Your Instances.

Warning
When you stop an instance, the data on any instance store volumes is erased. Therefore, if you have any data on instance store volumes that you want to keep, be sure to back it up to persistent storage.
Modify your EBS volume as described in Modifying an EBS Volume from the Console or Modifying an EBS Volume from the Command Line.

Restart the instance.

In the navigation pane, choose Instances and then select the instance to restart.

From the context (right-click) menu, choose Instance State, Start.

In the Start Instances dialog box, choose Yes, Start. If the instance fails to start, and the volume being expanded is a root volume, verify that you attached the expanded volume using the same device name as the original volume, for example /dev/sda1.

After the instance has started, you can check the file system size to see if your instance recognizes the larger volume space. On Linux, use the df -h command to check the file system size.

Copy
[ec2-user ~]$ df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/xvda1            7.9G  943M  6.9G  12% /
tmpfs                 1.9G     0  1.9G   0% /dev/shm
If the size does not reflect your newly expanded volume, you must extend the file system of your device so that your instance can use the new space. For more information, see Extending a Linux File System after Resizing the Volume.

Considerations for Modifying EBS Volumes

Be aware of the following limits and requirements when you modify an EBS volume:

In some cases, you must detach the volume or stop the instance for modification to proceed. If you encounter an error message while attempting to modify an EBS volume, or if you are modifying an EBS volume attached to a previous-generation instance type, take one of the following steps:
For a non-root volume, detach the volume from the instance, apply the modifications, and then re-attach the volume. For more information, see Detaching an Amazon EBS Volume from an Instance and Attaching an Amazon EBS Volume to an Instance.
For a root (boot) volume, stop the instance, apply the modifications, and then restart the instance. For more information, see Appendix: Starting and Stopping an Instance to Modify an EBS Volume.
The previous generation Magnetic volume type is not supported by the volume modification methods described in this topic. However, you can take a snapshot of a Magnetic volume and restore it to a differently configured EBS volume.
Decreasing the size of an EBS volume is not supported. However, you can create a smaller volume and then migrate your data to it using an application-level tool such as rsync.
After modifying a volume, wait at least six hours before applying further modifications to the same volume.
While m3.medium instances fully support volume modification, some m3.large, m3.xlarge, and m3.2xlarge instances might not support all volume modification features. If you encounter an error, see Appendix: Starting and Stopping an Instance to Modify an EBS Volume.
Linux AMIs require a GUID partition table (GPT) and GRUB 2 for boot volumes 2 TiB (2,048 GiB) or larger. Many Linux AMIs today still use the MBR partitioning scheme, which only supports boot-volume sizes up to 2,047 GiB. If your instance does not boot with a boot volume that is 2 TiB or larger, the AMI you are using may be limited to a 2,047 GiB boot volume size. Non-boot volumes do not have this limitation on Linux instances.
Before attempting to resize a boot volume beyond 2 TiB, you can determine whether the volume is using MBR or GPT partitioning by running the following command on your instance:
Copy
[ec2-user ~]$ sudo gdisk -l /dev/xvda
An Amazon Linux instance with GPT partitioning returns the following information:
GPT fdisk (gdisk) version 0.8.10

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.
A SUSE instance with MBR partitioning returns the following information:
GPT fdisk (gdisk) version 0.8.8

Partition table scan:
  MBR: MBR only
  BSD: not present
  APM: not present
  GPT: not present
Volume Modification Support on Older Volumes

Before you can modify a volume that was attached to an instance before November 1, 2016, you must initialize volume modification support using one of the following actions:

Detach and attach the volume
Restart the instance
To determine whether you must initialize volume modification support using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the navigation pane, choose Instances.

Choose the Show/Hide Columns icon (the gear). Select the Launch Time and Block Devices attributes and then choose Close.

Sort the list of instances by the Launch Time column. For instances that were started before the cutoff date, check when the devices were attached. In the following example, you must initialize volume modification for the first instance because it was started before the cutoff date and its root volume was attached before the cutoff date. The other instances are ready because they were started after the cutoff, regardless of when the volumes were attached.


              Check the Launch Time and Block Devices columns.
            
To determine whether you must initialize volume modification support using the CLI

To find an instance that was last started before the cutoff date with a volume that was attached before the cutoff date, use the following describe-instances command.

Copy
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,LaunchTime<=`2016-11-01`,BlockDeviceMappings[*][Ebs.AttachTime<=`20016-11-01`]]" --output text
The output for each instance shows its ID, whether it was started before the cutoff date (True or False), and whether its volumes were attached before the cutoff date (True or False). In the following example output, you must initialize volume modification for the first instance because it was started before the cutoff date and its root volume was attached before the cutoff date. The other instances are ready because they were started after the cutoff, regardless of when the volumes were attached.

i-e905622e              True
True
i-719f99a8              False
True
i-006b02c1b78381e57     False
False
False
i-e3d172ed              False
True

Expanding a Linux Partition

Some Amazon EC2 root volumes and volumes that are restored from snapshots contain a partition that actually holds the file system and the data. If you think of a volume as a container, a partition is another container inside the volume, and the data resides on the partition. Growing the volume size does not grow the partition; to take advantage of a larger volume, the partition must be expanded to the new size.

Note
Not all volumes restored from snapshots are partitioned, and this procedure may not apply to your volume. You may just need to resize the file system on your volume to make all of the space available. If you are not sure if your volume has a partition that needs resizing, see To check if your volume partition needs resizing for more information.
If the partition you want to expand is not the root partition, then you can simply unmount it and resize the partition from the instance itself. If the partition you need to resize is the root partition for an instance, the process becomes more complicated because you cannot unmount the root partition of a running instance. You have to perform the following procedures on another instance, which is referred to as a secondary instance.

Important
The following procedures were written for and tested on Amazon Linux. Other distributions with different tool sets and tool versions may behave differently.
Topics

Preparing a Linux Root Partition for Expansion
Expanding a Linux Partition Using parted
Expanding a Linux Partition Using gdisk
Returning an Expanded Partition to its Original Instance
Preparing a Linux Root Partition for Expansion

There are several steps that you need to take to expand the root partition of an instance. If the partition you need to expand is not the root partition, then this procedure is not necessary.

To prepare a Linux root partition for expansion

If your primary instance is running, stop it. You cannot perform the rest of this procedure on a running instance. For more information, see Stop and Start Your Instance.

Check the integrity of your volume. File-system corruption that is picked up by the snapshot may render a restored root volume unbootable.

Take a snapshot of your volume. It can be easy to corrupt or lose your data in the following procedures. If you have a fresh snapshot, you can always start over in case of a mistake and your data will still be safe. For more information, see Creating an Amazon EBS Snapshot.

Record the device name that the volume is attached to. You can find this information on the Root device field of the instance's details pane. The value is likely /dev/sda1 or /dev/xvda.

Detach the volume from the primary instance. For more information, see Detaching an Amazon EBS Volume from an Instance.

Attach the volume to another (secondary) instance in the same Availability Zone. For more information, see Attaching an Amazon EBS Volume to an Instance. If your EBS volume is encrypted, you must use a secondary instance that supports Amazon EBS encryption; otherwise, you can use a t2.micro instance for this procedure. For more information, see Supported Instance Types. If you do not already have a secondary instance, you will need to launch one. For more information, see Launching an Instance.

Important
The secondary instance must be running when you attach the volume, and you should not reboot the secondary instance while multiple root volumes are attached; booting an instance with multiple root volumes attached could cause the instance to boot to the wrong volume.
Log in to the secondary instance with SSH. For more information, see Connect to Your Linux Instance. Continue with the next procedure.

Expanding a Linux Partition Using parted

The parted utility is a partition editing tool that is available on most Linux distributions. It can create and edit both MBR partition tables and GPT partition tables. Some versions of parted (newer than version 2.1) have limited support for GPT partition tables and they may cause boot issues if their version of parted is used to modify boot volumes. You can check your version of parted with the parted --version command.

If you are expanding a partition that resides on a GPT partitioned device, you should choose to use the gdisk utility instead. If you're not sure which disk label type your volume uses, you can check it with the sudo fdisk -l command. For more information, see To expand a Linux partition using gdisk.

To expand a Linux partition using parted

If the partition you need to expand is the root partition, be sure to follow the steps in To prepare a Linux root partition for expansion first.

Identify the device that contains the partition that you want to expand. Use the lsblk command to list all devices and partitions attached to the instance.

Copy
[ec2-user ~]$ lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvdf    202:80   0  100G  0 disk
└─xvdf1 202:81   0    8G  0 part /mnt
xvda1   202:1    0   30G  0 disk /
In this example, the xvdf device has 100 GiB of available storage and it contains an 8 GiB partition.

Unmount the partition if it is mounted. Run the umount command with the value of MOUNTPOINT from the lsblk command. In this example, the MOUNTPOINT value for the partition is /mnt.

Copy
[ec2-user ~]$ sudo umount /mnt
Take a snapshot of your volume (unless you just took one in the previous procedure). It can be easy to corrupt or lose your data in the following procedures. If you have a fresh snapshot, you can always start over in case of a mistake and your data will still be safe. For more information, see Creating an Amazon EBS Snapshot.

Run the parted command on the device (and not the partition on the device). Remember to add the /dev/ prefix to the name that lsblk outputs.

Copy
[ec2-user ~]$ sudo parted /dev/xvdf
GNU Parted 2.1
Using /dev/xvdf
Welcome to GNU Parted! Type 'help' to view a list of commands.
Change the parted units of measure to sectors.

Copy
(parted) unit s
Run the print command to list the partitions on the device. For certain partition table types, you might be prompted to repair the partition table for the larger volume size. Answer 'Ignore' to any questions about fixing the existing partition table; you will create a new table later.

Copy
(parted) print
If you receive the following message, enter 'Ignore' to prevent the backup GPT location from changing.

Error: The backup GPT table is not at the end of the disk, as it should be.  This might mean that another operating
system believes the disk is smaller.  Fix, by moving the backup to the end (and removing the old backup)?
Fix/Ignore/Cancel? Ignore
If you receive the following message, enter 'Ignore' again to keep the space on the drive the same.

Warning: Not all of the space available to /dev/xvdf appears to be used, you can fix the GPT to use all of the
space (an extra 46137344 blocks) or continue with the current setting?
Fix/Ignore? Ignore
Examine the output for the total size of the disk, the partition table type, the number of the partition, the start point of the partition, and any flags, such as boot. For gpt partition tables, note the name of the partition; for msdos partition tables, note the Type field (primary or extended). These values are used in the upcoming steps.

The following is a gpt partition table example.

Model: Xen Virtual Block Device (xvd)
Disk /dev/xvdf: 209715200s
Sector size (logical/physical): 512B/512B
Partition Table: gpt

Number  Start  End        Size       File system  Name                 Flags
128     2048s  4095s      2048s                   BIOS Boot Partition  bios_grub
 1      4096s  16777182s  16773087s  ext4         Linux
The following is an msdos partition table example.

Model: Xen Virtual Block Device (xvd)
Disk /dev/xvdg: 104857600s
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start  End        Size       Type     File system  Flags
 1      2048s  35649535s  35647488s  primary  ext3
Delete the partition entry for the partition using the number (1) from the previous step.

Copy
(parted) rm 1
Create a new partition that extends to the end of the volume.

(For the gpt partition table example) Note the start point and name of partition 1 above. For the gpt example, there is a start point of 4096s, and the name Linux. Run the mkpart command with the start point of partition 1, the name, and 100% to use all of the available space.

Copy
(parted) mkpart Linux 4096s 100%
(For the msdos partition table example) Note the start point and the partition type of partition 1 above. For the msdos example, there is a start point of 2048s and a partition type of primary. Run the mkpart command with a primary partition type, the start point of partition 1, and 100% to use all of the available space.

Copy
(parted) mkpart primary 2048s 100%
Run the print command again to verify your partition.

(For the gpt partition table example)

Copy
(parted) print
Model: Xen Virtual Block Device (xvd)
Disk /dev/xvdf: 209715200s
Sector size (logical/physical): 512B/512B
Partition Table: gpt

Number  Start  End         Size        File system  Name                 Flags
128     2048s  4095s       2048s                    BIOS Boot Partition  bios_grub
 1      4096s  209713151s  209709056s  ext4         Linux
(For the msdos partition table example)

Copy
(parted) print
Model: Xen Virtual Block Device (xvd)
Disk /dev/xvdg: 104857600s
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start  End         Size        Type     File system  Flags
 1      2048s  104857599s  104855552s  primary  ext3
Check to see that any flags that were present earlier are still present for the partition that you expanded. In some cases the boot flag may be lost. If a flag was dropped from the partition when it was expanded, add the flag with the following command, substituting your partition number and the flag name. For example, the following command adds the boot flag to partition 1.

Copy
(parted) set 1 boot on
You can run the print command again to verify your change.

Run the quit command to exit parted.

Copy
(parted) quit
Note
Because you removed a partition and added a partition, parted may warn that you may need to update /etc/fstab. This is only required if the partition number changes.
Check the file system to make sure there are no errors (this is required before you may extend the file system). Note the file system type from the previous print commands. Choose one of the commands below based on your file system type; if you are using a different file system, consult the documentation for that file system to determine the correct check command.

(For ext3 or ext4 file systems)

Copy
[ec2-user ~]$ sudo e2fsck -f /dev/xvdf1
e2fsck 1.42.3 (14-May-2012)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/: 31568/524288 files (0.4% non-contiguous), 266685/2096635 blocks
(For xfs file systems)

Copy
[ec2-user ~]$ sudo xfs_repair /dev/xvdf1
Phase 1 - find and verify superblock...
Phase 2 - using internal log
        - zero log...
        - scan filesystem freespace and inode maps...
        - found root inode chunk
Phase 3 - for each AG...
        - scan and clear agi unlinked lists...
        - process known inodes and perform inode discovery...
        - agno = 0
        - agno = 1
        - agno = 2
        - agno = 3
        - process newly discovered inodes...
Phase 4 - check for duplicate blocks...
        - setting up duplicate extent list...
        - check for inodes claiming duplicate blocks...
        - agno = 0
        - agno = 1
        - agno = 2
        - agno = 3
Phase 5 - rebuild AG headers and trees...
        - reset superblock...
Phase 6 - check inode connectivity...
        - resetting contents of realtime bitmap and summary inodes
        - traversing filesystem ...
        - traversal finished ...
        - moving disconnected inodes to lost+found ...
Phase 7 - verify and correct link counts...
done
The next steps differ depending on whether the expanded partition belongs on the current instance or if it is the root partition for another instance.

If this partition belongs on the current instance, remount the partition at the MOUNTPOINT identified in Step 2.
Copy
[ec2-user ~]$ sudo mount /dev/xvdf1 /mnt
After you have mounted the partition, extend the file system to use the newly available space by following the procedures in Extending a Linux File System after Resizing the Volume.
If this volume is the root partition for another instance, proceed to the procedures in Returning an Expanded Partition to its Original Instance.
Expanding a Linux Partition Using gdisk

The gdisk utility (sometimes called GPT fdisk) is a text-based, menu-driven tool for creating and editing partition tables, and it has better support for GPT partition tables than parted in some distributions. Many common Linux distributions (such as Amazon Linux and Ubuntu) provide gdisk by default. If your distribution does not provide the gdisk command, you can find out how to get it by visiting Obtaining GPT fdisk; in many cases, it is much easier to launch an Amazon Linux instance to use as a secondary instance because the gdisk command is already available.

To expand a Linux partition using gdisk

If the partition you need to expand is the root partition, be sure to follow the steps in To prepare a Linux root partition for expansion first.

Identify the device that contains the partition that you want to expand. Use the lsblk command to list all devices and partitions attached to the instance.

Copy
[ec2-user ~]$ lsblk
NAME    MAJ:MIN RM  SIZE RO MOUNTPOINT
xvdf    202:80   0  100G  0
xvdf1   202:81   0  9.9G  0 /mnt
xvda1   202:1    0   30G  0 /
In this example, the xvdf device has 100 GiB of available storage and it contains a 9.9 GiB partition.

Unmount the partition if it is mounted. Run the umount command with the value of MOUNTPOINT from the lsblk command. In this example, the MOUNTPOINT value for the partition is /mnt.

Copy
[ec2-user ~]$ sudo umount /mnt
Take a snapshot of your volume (unless you just took one in the previous procedure). It can be easy to corrupt or lose your data in the following procedures. If you have a fresh snapshot, you can always start over in case of a mistake and your data will still be safe. For more information, see Creating an Amazon EBS Snapshot.

Run the gdisk command on the device (and not the partition on the device). Remember to add the /dev/ prefix to the name that lsblk outputs.

Copy
[ec2-user ~]$ sudo gdisk /dev/xvdf
gdisk /dev/xvdf
GPT fdisk (gdisk) version 0.8.10

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.
Run the p command to print the partition table for the device.

Examine the output for the disk identifier, partition number, starting sector, code for the partition, and name of the partition. If your volume has multiple partitions, take note of each one.

Command (? for help): p
Disk /dev/xvdf: 209715200 sectors, 100.0 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): 947F4655-F3BF-4A1F-8203-000000000000
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 20705246
Partitions will be aligned on 2048-sector boundaries
Total free space is 2108 sectors (1.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048        20705152   9.9 GiB     EF00  lxroot
In the above example the disk identifier is 947F4655-F3BF-4A1F-8203-000000000000, the partition number is 1, the starting sector is 2048, the code is EF00, and the name is lxroot. Your values will vary.

Because the existing partition table was originally created for a smaller volume, you need to create a new partition table for the larger volume. Run the o command to create a new, empty partition table.

Command (? for help): o
This option deletes all partitions and creates a new protective MBR.
Proceed? (Y/N): Y
Use the n command to create a new partition entry for each partition on the device.

If your volume has only one partition, at each prompt, enter the values that you recorded earlier. For the last sector value, use the default value to expand to the entire volume size.

Command (? for help): n
Partition number (1-128, default 1): 1
First sector (34-209715166, default = 2048) or {+-}size{KMGTP}: 2048
Last sector (2048-209715166, default = 209715166) or {+-}size{KMGTP}: 209715166
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300): EF00
Changed type of partition to 'EFI System'
If your volume has more than one partition, there is likely a BIOS boot partition, and a main data partition. Create a new partition entry for the BIOS boot partition using the values that you recorded earlier. Create another new partition entry for the main data partition using the values that you recorded earlier, but for the last sector value, use the default value to expand to the entire volume size.

Command (? for help): n
Partition number (1-128, default 1): 1
First sector (34-209715166, default = 2048) or {+-}size{KMGTP}:  2048
Last sector (2048-209715166, default = 209715166) or {+-}size{KMGTP}: 4095
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300): EF02
Changed type of partition to 'BIOS boot partition'

Command (? for help): n
Partition number (2-128, default 2): 2
First sector (34-209715166, default = 4096) or {+-}size{KMGTP}: 4096
Last sector (4096-209715166, default = 209715166) or {+-}size{KMGTP}: 209715166
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300): 0700
Changed type of partition to 'Microsoft basic data'
Use the c command to change the name of each partition to the name of the previous partition. If your partition did not have a name, simply type Enter.

Command (? for help): c
Using 1
Enter name: lxroot
Use the x command to enter the expert command menu.

Use the g command to change the disk identifier to the original value.

Expert command (? for help): g
Enter the disk's unique GUID ('R' to randomize): 947F4655-F3BF-4A1F-8203-A7B30C2A4425
The new disk GUID is 947F4655-F3BF-4A1F-8203-A7B30C2A4425
Use the w command to write the changes to the device and exit.

Expert command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): Y
OK; writing new GUID partition table (GPT) to /dev/xvdf.
The operation has completed successfully.
Check the file system to make sure there are no errors (this is required before you may extend the file system).

Find the file system type with the following command, substituting the partition you just expanded (this may be /dev/xvdf2 if your volume had multiple partitions).

Copy
[ec2-user ~]$ sudo file -sL /dev/xvdf1
Choose one of the commands below based on your file system type; if you are using a different file system, consult the documentation for that file system to determine the correct check command.

(For ext3 or ext4 file systems)

Copy
[ec2-user ~]$ sudo e2fsck -f /dev/xvdf1
e2fsck 1.42.3 (14-May-2012)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/: 31568/524288 files (0.4% non-contiguous), 266685/2096635 blocks
(For xfs file systems)

Note
You may need to install the xfsprogs package to work with XFS file systems. Use the following command to add XFS support to your Amazon Linux instance.
Copy
[ec2-user ~]$ sudo yum install -y xfsprogs
Copy
[ec2-user ~]$ sudo xfs_repair /dev/xvdf1
Phase 1 - find and verify superblock...
Phase 2 - using internal log
        - zero log...
        - scan filesystem freespace and inode maps...
        - found root inode chunk
Phase 3 - for each AG...
        - scan and clear agi unlinked lists...
        - process known inodes and perform inode discovery...
        - agno = 0
        - agno = 1
        - agno = 2
        - agno = 3
        - process newly discovered inodes...
Phase 4 - check for duplicate blocks...
        - setting up duplicate extent list...
        - check for inodes claiming duplicate blocks...
        - agno = 0
        - agno = 1
        - agno = 2
        - agno = 3
Phase 5 - rebuild AG headers and trees...
        - reset superblock...
Phase 6 - check inode connectivity...
        - resetting contents of realtime bitmap and summary inodes
        - traversing filesystem ...
        - traversal finished ...
        - moving disconnected inodes to lost+found ...
Phase 7 - verify and correct link counts...
done
The next steps differ depending on whether the expanded partition belongs on the current instance or if it is the root partition for another instance.

If this partition belongs on the current instance, remount the partition at the MOUNTPOINT identified in Step 2.
Copy
[ec2-user ~]$ sudo mount /dev/xvdf1 /mnt
After you have mounted the partition, extend the file system to use the newly available space by following the procedures in Extending a Linux File System after Resizing the Volume.
If this volume is the root partition for another instance, proceed to the procedures in Returning an Expanded Partition to its Original Instance.
Returning an Expanded Partition to its Original Instance

If you expanded a root partition from another instance, follow this procedure to return the volume to its original instance.

To return an expanded root partition to its original instance

Detach the expanded partition from its secondary instance. For more information, see Detaching an Amazon EBS Volume from an Instance.

Reattach the volume to the primary instance using the device name that you identified in Step 4 of the preparation procedure. For more information, see Attaching an Amazon EBS Volume to an Instance.

Start the primary instance. For more information, see Stop and Start Your Instance.

(Optional) If you launched a secondary instance for the sole purpose of expanding the partition, you can terminate the instance to stop incurring charges. For more information, see Terminate Your Instance.

Connect to your primary instance and extend the file system to use the newly available space by following the procedures in Extending a Linux File System after Resizing the Volume.

After you are finished with this expanding the file system, you can create an AMI from the instance that you can use to launch new instances with the desired partition size. For more information, see Amazon Machine Images (AMI).

Amazon EBS Snapshots

You can back up the data on your Amazon EBS volumes to Amazon S3 by taking point-in-time snapshots. Snapshots are incremental backups, which means that only the blocks on the device that have changed after your most recent snapshot are saved. This minimizes the time required to create the snapshot and saves on storage costs by not duplicating data. When you delete a snapshot, only the data unique to that snapshot is removed. Each snapshot contains all of the information needed to restore your data (from the moment when the snapshot was taken) to a new EBS volume.

When you create an EBS volume based on a snapshot, the new volume begins as an exact replica of the original volume that was used to create the snapshot. The replicated volume loads data lazily in the background so that you can begin using it immediately. If you access data that hasn't been loaded yet, the volume immediately downloads the requested data from Amazon S3, and then continues loading the rest of the volume's data in the background. For more information, see Creating an Amazon EBS Snapshot.

Contents

How Incremental Snapshots Work
Copying and Sharing Snapshots
Encryption Support for Snapshots
Creating an Amazon EBS Snapshot
Deleting an Amazon EBS Snapshot
Copying an Amazon EBS Snapshot
Viewing Amazon EBS Snapshot Information
Sharing an Amazon EBS Snapshot
How Incremental Snapshots Work

This section provides illustrations of how an EBS snapshot captures the state of a volume at a point in time, and also how successive snapshots of a changing volume create a history of those changes.

In the diagram below, Volume 1 is shown at three points in time. A snapshot is taken of each of these three volume states.

In State 1, the volume has 10 GiB of data. Because Snap A is the first snapshot taken of the volume, the entire 10 GiB of data must be copied.
In State 2, the volume still contains 10 GiB of data, but 4 GiB have changed. Snap B needs to copy and store only the 4 GiB that changed after Snap A was taken. The other 6 GiB of unchanged data, which are already copied and stored in Snap A, are referenced by Snap B rather than (again) copied. This is indicated by the dashed arrow.
In State 3, 2 GiB of data have been added to the volume, for a total of 12 GiB. Snap C needs to copy the 2 GiB that were added after Snap B was taken. As shown by the dashed arrows, Snap C also references the 4 GiB of data stored in Snap B, and the 6 GiB of data stored in Snap A. The total storage required for the three snapshots is 16 GiB.
Relations among Multiple Snapshots of a Volume


        Snapshots capturing an initial volume state and two subsequent states after data has
          been changed.
      
For more information about how data is managed when you delete a snapshot, see Deleting an Amazon EBS Snapshot.

Copying and Sharing Snapshots

You can share a snapshot across AWS accounts by modifying its access permissions. You can make copies of your own snapshots as well as snapshots that have been shared with you. For more information, see Sharing an Amazon EBS Snapshot.

A snapshot is constrained to the region where it was created. After you create a snapshot of an EBS volume, you can use it to create new volumes in the same region. For more information, see Restoring an Amazon EBS Volume from a Snapshot. You can also copy snapshots across regions, making it possible to use multiple regions for geographical expansion, data center migration, and disaster recovery. You can copy any accessible snapshot that has a completed status. For more information, see Copying an Amazon EBS Snapshot.

Encryption Support for Snapshots

EBS snapshots broadly support EBS encryption.

Snapshots of encrypted volumes are automatically encrypted.
Volumes that are created from encrypted snapshots are automatically encrypted.
When you copy an unencrypted snapshot that you own, you can encrypt it during the copy process.
When you copy an encrypted snapshot that you own, you can reencrypt it with a different key during the copy process.
For more information, see Amazon EBS Encryption.

Creating an Amazon EBS Snapshot

A point-in-time snapshot of an EBS volume, can be used as a baseline for new volumes or for data backup. If you make periodic snapshots of a volume, the snapshots are incremental—only the blocks on the device that have changed after your last snapshot are saved in the new snapshot. Even though snapshots are saved incrementally, the snapshot deletion process is designed so that you need to retain only the most recent snapshot in order to restore the entire volume.

Snapshots occur asynchronously; the point-in-time snapshot is created immediately, but the status of the snapshot is pending until the snapshot is complete (when all of the modified blocks have been transferred to Amazon S3), which can take several hours for large initial snapshots or subsequent snapshots where many blocks have changed. While it is completing, an in-progress snapshot is not affected by ongoing reads and writes to the volume.

Important
Although you can take a snapshot of a volume while a previous snapshot of that volume is in the pending status, having multiple pending snapshots of a volume may result in reduced volume performance until the snapshots complete.
There is a limit of five pending snapshots for a single gp2, io1, or Magnetic volume, and one pending snapshot for a single st1 or sc1 volume. If you receive a ConcurrentSnapshotLimitExceeded error while trying to create multiple concurrent snapshots of the same volume, wait for one or more of the pending snapshots to complete before creating another snapshot of that volume.
Snapshots that are taken from encrypted volumes are automatically encrypted. Volumes that are created from encrypted snapshots are also automatically encrypted. The data in your encrypted volumes and any associated snapshots is protected both at rest and in motion. For more information, see Amazon EBS Encryption.

By default, only you can create volumes from snapshots that you own. However, you can share your unencrypted snapshots with specific AWS accounts, or you can share them with the entire AWS community by making them public. For more information, see Sharing an Amazon EBS Snapshot.

You can share an encrypted snapshot only with specific AWS accounts. For others to use your shared, encrypted snapshot, you must also share the CMK key that was used to encrypt it. Users with access to your encrypted snapshot must create their own personal copy of it and then use that copy to restore the volume. Your copy of a shared, encrypted snapshot can also be re-encrypted with a different key. For more information, see Sharing an Amazon EBS Snapshot.

When a snapshot is created from a volume with an AWS Marketplace product code, the product code is propagated to the snapshot.

You can take a snapshot of an attached volume that is in use. However, snapshots only capture data that has been written to your Amazon EBS volume at the time the snapshot command is issued. This might exclude any data that has been cached by any applications or the operating system. If you can pause any file writes to the volume long enough to take a snapshot, your snapshot should be complete. However, if you can't pause all file writes to the volume, you should unmount the volume from within the instance, issue the snapshot command, and then remount the volume to ensure a consistent and complete snapshot. You can remount and use your volume while the snapshot status is pending.

To create a snapshot for an Amazon EBS volume that serves as a root device, you should stop the instance before taking the snapshot.

To unmount the volume in Linux, use the following command, where device_name is the device name (for example, /dev/sdh):

Copy
umount -d device_name
After you've created a snapshot, you can tag it to help you manage it later. For example, you can add tags describing the original volume from which the snapshot was created, or the device name that was used to attach the original volume to an instance. For more information, see Tagging Your Amazon EC2 Resources.

To create a snapshot using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Snapshots in the navigation pane.

Choose Create Snapshot.

In the Create Snapshot dialog box, select the volume to create a snapshot for, and then choose Create.

To create a snapshot using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-snapshot (AWS CLI)
New-EC2Snapshot (AWS Tools for Windows PowerShell)

Deleting an Amazon EBS Snapshot

When you delete a snapshot, only the data referenced exclusively by that snapshot is removed. Deleting previous snapshots of a volume does not affect your ability to restore volumes from later snapshots of that volume.

Deleting a snapshot of a volume has no effect on the volume. Deleting a volume has no effect on the snapshots made from it.

If you make periodic snapshots of a volume, the snapshots are incremental, which means that only the blocks on the device that have changed after your last snapshot are saved in the new snapshot. Even though snapshots are saved incrementally, the snapshot deletion process is designed so that you need to retain only the most recent snapshot in order to restore the volume.

Deleting a snapshot might not reduce your organization's data storage costs. Other snapshots might reference that snapshot's data, and referenced data is always preserved. If you delete a snapshot containing data being used by a later snapshot, costs associated with the referenced data are allocated to the later snapshot. For more information about how snapshots store data, see How Incremental Snapshots Work and the example below.

In the following diagram, Volume 1 is shown at three points in time. A snapshot has captured each of the first two states, and in the third, a snapshot has been deleted.

In State 1, the volume has 10 GiB of data. Because Snap A is the first snapshot taken of the volume, the entire 10 GiB of data must be copied.
In State 2, the volume still contains 10 GiB of data, but 4 GiB have changed. Snap B needs to copy and store only the 4 GiB that changed after Snap A was taken. The other 6 GiB of unchanged data, which are already copied and stored in Snap A, are referenced by Snap B rather than (again) copied. This is indicated by the dashed arrow.
In state 3, the volume has not changed since State 2, but Snapshot A has been deleted. The 6 GiB of data stored in Snapshot A that were referenced by Snapshot B have now been moved to Snapshot B, as shown by the heavy arrow. As a result, you are still charged for storing 10 GiB of data—6 GiB of unchanged data preserved from Snap A, and 4 GiB of changed data from Snap B.
Example 1: Deleting a Snapshot with Some of its Data Referenced by Another Snapshot


        Snap A contains 6 GiB of referenced data. When Snap A is deleted, that data is
          merged into Snap B.
      
Note that you can't delete a snapshot of the root device of an EBS volume used by a registered AMI. You must first deregister the AMI before you can delete the snapshot. For more information, see Deregistering Your AMI.

To delete a snapshot using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Snapshots in the navigation pane.

Select a snapshot and then choose Delete from the Actions list.

Choose Yes, Delete.

To delete a snapshot using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

delete-snapshot (AWS CLI)
Remove-EC2Snapshot (AWS Tools for Windows PowerShell)
Note
Although you can delete a snapshot that is still in progress, the snapshot must complete before the deletion takes effect. This may take a long time. If you are also at your concurrent snapshot limit (five snapshots in progress), and you attempt to take an additional snapshot, you may get the ConcurrentSnapshotLimitExceeded error.

Copying an Amazon EBS Snapshot

With Amazon EBS, you can create point-in-time snapshots of volumes, which we store for you in Amazon S3. After you've created a snapshot and it has finished copying to Amazon S3 (when the snapshot status is completed), you can copy it from one AWS region to another, or within the same region. Amazon S3 server-side encryption (256-bit AES) protects a snapshot's data in-transit during a copy operation. The snapshot copy receives an ID that is different than the ID of the original snapshot.

For information about copying an Amazon RDS snapshot, see Copying a DB Snapshot in the Amazon Relational Database Service User Guide.

If you would like another account to be able to copy your snapshot, you must either modify the snapshot permissions to allow access to that account or make the snapshot public so that all AWS accounts may copy it. For more information, see Sharing an Amazon EBS Snapshot.

For pricing information about copying snapshots across regions and accounts, see Amazon EBS Pricing. Note that snapshot copy operations within a single account and region do not copy any data and are cost-free as long as the following conditions apply:

The encryption status of the snapshot copy does not change.
For encrypted snapshots, both the source snapshot and the copy are encrypted with the default EBS CMK.
Use Cases

Geographic expansion: Launch your applications in a new region.
Migration: Move an application to a new region, to enable better availability and to minimize cost.
Disaster recovery: Back up your data and logs across different geographical locations at regular intervals. In case of disaster, you can restore your applications using point-in-time backups stored in the secondary region. This minimizes data loss and recovery time.
Encryption: Encrypt a previously unencrypted snapshot, change the key with which the snapshot is encrypted, or, for encrypted snapshots that have been shared with you, create a copy that you own in order to restore a volume from it.
Data retention and auditing requirements: Copy your encrypted EBS snapshots from one AWS account to another to preserve data logs or other files for auditing or data retention. Using a different account helps prevent accidental snapshot deletions, and protects you if your main AWS account is compromised.
Prerequisites

You can copy any accessible snapshots that have a completed status, including shared snapshots and snapshots that you've created.
You can copy AWS Marketplace, VM Import/Export, and AWS Storage Gateway snapshots, but you must verify that the snapshot is supported in the destination region.
Limits

Each account can have up to 5 concurrent snapshot copy requests to a single destination region.
User-defined tags are not copied from the source snapshot to the new snapshot. After the copy operation is complete, you can apply user-defined tags to the new snapshot. For more information, see Tagging Your Amazon EC2 Resources.
Snapshots created by the CopySnapshot action have an arbitrary volume ID that should not be used for any purpose.
Incremental Copy

The first snapshot copy to another region is always a full copy. Each subsequent snapshot copy is incremental (which makes the copy process faster), meaning that only the blocks in the snapshot that have changed after your last snapshot copy to the same destination are transferred. Support for incremental snapshots is specific to a cross=region pair where a previous complete snapshot copy of the source volume is already available in the destination region, and it is limited to the default EBS CMK for encrypted snapshots. For example, if you copy an unencrypted snapshot from the US East (N. Virginia) region to the US West (Oregon) region, the first snapshot copy of the volume is a full copy and subsequent snapshot copies of the same volume transferred between the same regions are incremental.

Encrypted Snapshots

When you copy a snapshot, you can choose to encrypt the copy (if the original snapshot was not encrypted) or you can specify a CMK different from the original one, and the resulting copied snapshot uses the new CMK. However, changing the encryption status of a snapshot or using a non-default EBS CMK during a copy operation always results in a full (not incremental) copy, which may incur greater data transfer and storage charges.

To copy an encrypted snapshot from another account, you must have permissions to use the snapshot and you must have permissions to use the customer master key (CMK) that was used to encrypt the original snapshot. For more information, see Sharing an Amazon EBS Snapshot.

When copying an encrypted snapshot that was shared with you, you should consider re-encrypting the snapshot during the copy process with a different key that you control. This protects you if the original key is compromised, or if the owner revokes the key for any reason, which could cause you to lose access to the volume you created.

Copy a Snapshot

Use the following procedure to copy a snapshot using the Amazon EC2 console.

To copy a snapshot using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Snapshots.

Select the snapshot to copy, and then choose Copy from the Actions list.

In the Copy Snapshot dialog box, update the following as necessary:

Destination region: Select the region where you want to write the copy of the snapshot.
Description: By default, the description includes information about the source snapshot so that you can identify a copy from the original. You can change this description as necessary.
Encryption: If the source snapshot is not encrypted, you can choose to encrypt the copy. You cannot decrypt an encrypted snapshot.
Master Key: The customer master key (CMK) that to be used to encrypt this snapshot. You can select from master keys in your account or type/paste the ARN of a key from a different account. You can create a new master encryption key in the IAM console.
Choose Copy.

In the Copy Snapshot confirmation dialog box, choose Snapshots to go to the Snapshots page in the region specified, or choose Close.

To view the progress of the copy process, switch to the destination region, and then refresh the Snapshots page. Copies in progress are listed at the top of the page.

To check for failure

If you attempt to copy an encrypted snapshot without having permissions to use the encryption key, the operation fails silently. The error state is not displayed in the console until you refresh the page. You can also check the state of the snapshot from the command line. For example:

Copy
aws ec2 describe-snapshots --snapshot-id snap-0123abcd
If the copy failed because of insufficient key permissions, you see the following message: "StateMessage": "Given key ID is not accessible".

When copying an encrypted snapshot, you must have DescribeKey permissions on the default CMK. Explicitly denying these permissions results in copy failure. For information about managing CMK keys, see Controlling Access to Customer Master Keys.

To copy a snapshot using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

copy-snapshot (AWS CLI)
Copy-EC2Snapshot (AWS Tools for Windows PowerShell)

Viewing Amazon EBS Snapshot Information

You can view detailed information about your snapshots.

To view snapshot information using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Snapshots in the navigation pane.

To reduce the list, choose an option from the Filter list. For example, to view only your snapshots, choose Owned By Me. You can filter your snapshots further by using the advanced search options. Choose the search bar to view the filters available.

To view more information about a snapshot, select it.

To view snapshot information using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-snapshots (AWS CLI)
Get-EC2Snapshot (AWS Tools for Windows PowerShell)

Sharing an Amazon EBS Snapshot

By modifying the permissions of the snapshot,you can share your unencrypted snapshots with your co-workers or others in the AWS community Users that you have authorized can use your unencrypted shared snapshots as the basis for creating their own EBS volumes. If you choose, you can also make your unencrypted snapshots available publicly to all AWS users.

You can share an encrypted snapshot with specific AWS accounts, though you cannot make it public. For others to use the snapshot, you must also share the custom CMK key used to encrypt it. Cross-account permissions may be applied to a custom key either when it is created or at a later time. Users with access can copy your snapshot and create their own EBS volumes based on your snapshot while your original snapshot remains unaffected.

Important
When you share a snapshot (whether by sharing it with another AWS account or making it public to all), you are giving others access to all the data on the snapshot. Share snapshots only with people with whom you want to share all your snapshot data.
Several technical and policy restrictions apply to sharing snapshots:

Snapshots are constrained to the region in which they were created. To share a snapshot with another region, copy the snapshot to that region. For more information about copying snapshots, see Copying an Amazon EBS Snapshot.
If your snapshot uses the longer resource ID format, you can only share it with another account that also supports longer IDs. For more information, see Resource IDs.
AWS prevents you from sharing snapshots that were encrypted with your default CMK. Snapshots that you intend to share must instead be encrypted with a custom CMK. For information about creating keys, see Creating Keys.
Users of your shared CMK who are accessing encrypted snapshots must be granted DescribeKey and ReEncrypt permissions. For information about managing and sharing CMK keys, see Controlling Access to Customer Master Keys.
If you have access to a shared encrypted snapshot and you want to restore a volume from it, you must create a personal copy of the snapshot and then use that copy to restore the volume. We recommend that you re-encrypt the snapshot during the copy process with a different key that you control. This protects your access to the volume if the original key is compromised, or if the owner revokes the key for any reason.
To modify snapshot permissions using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Snapshots in the navigation pane.

Select a snapshot and then choose Modify Permissions from the Actions list.

Choose whether to make the snapshot public or to share it with specific AWS accounts:

To make the snapshot public, choose Public.

This is not a valid option for encrypted snapshots or snapshots with AWS Marketplace product codes.

To expose the snapshot to only specific AWS accounts, choose Private, enter the ID of the AWS account (without hyphens) in the AWS Account Number field, and choose Add Permission. Repeat until you've added all the required AWS accounts.

Important
If your snapshot is encrypted, you must ensure that the following are true:
The snapshot is encrypted with a custom CMK, not your default CMK. If you attempt to change the permissions of a snapshot encrypted with your default CMK, the console displays an error message.
You are sharing the custom CMK with the accounts that have access to your snapshot.
Choose Save.

To view and modify snapshot permissions using the command line

To view the createVolumePermission attribute of a snapshot, you can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-snapshot-attribute (AWS CLI)
Get-EC2SnapshotAttribute (AWS Tools for Windows PowerShell)
To modify the createVolumePermission attribute of a snapshot, you can use one of the following commands.

modify-snapshot-attribute (AWS CLI)
Edit-EC2SnapshotAttribute (AWS Tools for Windows PowerShell)

Amazon EBS–Optimized Instances

An Amazon EBS–optimized instance uses an optimized configuration stack and provides additional, dedicated capacity for Amazon EBS I/O. This optimization provides the best performance for your EBS volumes by minimizing contention between Amazon EBS I/O and other traffic from your instance.

EBS–optimized instances deliver dedicated bandwidth to Amazon EBS, with options between 500 Mbps and 12,000 Mbps, depending on the instance type you use. When attached to an EBS–optimized instance, General Purpose SSD (gp2) volumes are designed to deliver within 10% of their baseline and burst performance 99% of the time in a given year, and Provisioned IOPS SSD (io1) volumes are designed to deliver within 10% of their provisioned performance 99.9% of the time in a given year. Both Throughput Optimized HDD (st1) and Cold HDD (sc1) guarantee performance consistency of 90% of burst throughput 99% of the time in a given year. Non-compliant periods are approximately uniformly distributed, targeting 99% of expected total throughput each hour. For more information, see Amazon EBS Volume Types.

When you enable EBS optimization for an instance that is not EBS–optimized by default, you pay an additional low, hourly fee for the dedicated capacity. For pricing information, see EBS-optimized Instances on the Amazon EC2 On-Demand Pricing page.

Contents

Instance Types that Support EBS Optimization
Enabling EBS Optimization at Launch
Modifying EBS Optimization for a Running Instance
Instance Types that Support EBS Optimization

The following table shows which instance types support EBS optimization, the dedicated bandwidth to Amazon EBS, the maximum number of IOPS the instance can support if you are using a 16 KiB I/O size, and the typical maximum aggregate throughput that can be achieved on that connection in MiB/s with a streaming read workload and128 KiB I/O size . Choose an EBS–optimized instance that provides more dedicated EBS throughput than your application needs; otherwise, the connection between Amazon EBS and Amazon EC2 can become a performance bottleneck.

Note that some instance types are EBS–optimized by default. For instances that are EBS–optimized by default, there is no need to enable EBS optimization and there is no effect if you disable EBS optimization using the CLI or API. You can enable EBS optimization for the other instance types that support EBS optimization when you launch the instances, or enable EBS optimization after the instances are running.

Note
Note that some instances with 10-gigabit network interfaces, such as i2.8xlarge and r3.8xlarge do not offer EBS-optimization, and therefore do not have dedicated EBS bandwidth available and are not listed here. On these instances, network traffic and Amazon EBS traffic is shared on the same 10-gigabit network interface. Some other 10-gigabit network instances, such as c4.8xlarge and d2.8xlarge offer dedicated EBS bandwidth in addition to a 10-gigabit interface which is used exclusively for network traffic.
Instance type	EBS-optimized by default	Max. bandwidth (Mbps)*	Expected throughput (MB/s)**	Max. IOPS (16 KB I/O size)**
c1.xlarge		1,000	125	8,000
c3.xlarge		500	62.5	4,000
c3.2xlarge		1,000	125	8,000
c3.4xlarge		2,000	250	16,000
c4.large	Yes	500	62.5	4,000
c4.xlarge	Yes	750	93.75	6,000
c4.2xlarge	Yes	1,000	125	8,000
c4.4xlarge	Yes	2,000	250	16,000
c4.8xlarge	Yes	4,000	500	32,000
d2.xlarge	Yes	750	93.75	6,000
d2.2xlarge	Yes	1,000	125	8,000
d2.4xlarge	Yes	2,000	250	16,000
d2.8xlarge	Yes	4,000	500	32,000
f1.2xlarge	Yes	1,700	200	12,000
f1.16xlarge	Yes	14,000	1,750	75,000
g2.2xlarge		1,000	125	8,000
g3.4xlarge	Yes	3,500	437	20,000
g3.8xlarge	Yes	7,000	875	40,000
g3.16xlarge	Yes	14,000	1,750	80,000
i2.xlarge		500	62.5	4,000
i2.2xlarge		1,000	125	8,000
i2.4xlarge		2,000	250	16,000
i3.large	Yes	425	50	3000
i3.xlarge	Yes	850	100	6000
i3.2xlarge	Yes	1,700	200	12,000
i3.4xlarge	Yes	3,500	400	16,000
i3.8xlarge	Yes	7,000	850	32,500
i3.16xlarge	Yes	14,000	1,750	65,000
m1.large		500	62.5	4,000
m1.xlarge		1,000	125	8,000
m2.2xlarge		500	62.5	4,000
m2.4xlarge		1,000	125	8,000
m3.xlarge		500	62.5	4,000
m3.2xlarge		1,000	125	8,000
m4.large	Yes	450	56.25	3,600
m4.xlarge	Yes	750	93.75	6,000
m4.2xlarge	Yes	1,000	125	8,000
m4.4xlarge	Yes	2,000	250	16,000
m4.10xlarge	Yes	4,000	500	32,000
m4.16xlarge	Yes	10,000	1,250	65,000
p2.xlarge	Yes	750	93.75	6,000
p2.8xlarge	Yes	5,000	625	32,500
p2.16xlarge	Yes	10,000	1,250	65,000
r3.xlarge		500	62.5	4,000
r3.2xlarge		1,000	125	8,000
r3.4xlarge		2,000	250	16,000
r4.large	Yes	437	54	3,000
r4.xlarge	Yes	875	109	6,000
r4.2xlarge	Yes	1,750	218	12,000
r4.4xlarge	Yes	3,500	437	18,750
r4.8xlarge	Yes	7,000	875	37,500
r4.16xlarge	Yes	14,000	1,750	75,000
x1.16xlarge	Yes	7,000	875	40,000
x1.32xlarge	Yes	14,000	1,750	80,000
* These instance types must be launched as EBS-optimized to consistently achieve this level of performance.

** This value is a rounded approximation based on a 100% read-only workload and it is provided as a baseline configuration aid. EBS-optimized connections are full-duplex, and can drive more throughput and IOPS in a 50/50 read/write workload where both communication lanes are used. In some cases, network, file system, and Amazon EBS encryption overhead can reduce the maximum throughput and IOPS available.

Enabling EBS Optimization at Launch

You can enable EBS optimization for an instance by setting its EBS–optimized attribute.

To enable EBS optimization when launching an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Click Launch Instance. In Step 1: Choose an Amazon Machine Image (AMI), select an AMI.

In Step 2: Choose an Instance Type, select an instance type that is listed as supporting EBS optimization.

In Step 3: Configure Instance Details, complete the fields that you need and select Launch as EBS-optimized instance. If the instance type that you selected in the previous step doesn't support EBS optimization, this option is not present. If the instance type that you selected is EBS–optimized by default, this option is selected and you can't deselect it.

Follow the directions to complete the wizard and launch your instance.

To enable EBS optimization when launching an instance using the command line

You can use one of the following options with the corresponding command. For more information about these command line interfaces, see Accessing Amazon EC2.

--ebs-optimized with run-instances (AWS CLI)
-EbsOptimized with New-EC2Instance (AWS Tools for Windows PowerShell)
Modifying EBS Optimization for a Running Instance

You can enable or disable EBS optimization for a running instance by modifying its EBS–optimized instance attribute.

To enable EBS optimization for a running instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, click Instances, and select the instance.

Click Actions, select Instance State, and then click Stop.

Warning
When you stop an instance, the data on any instance store volumes is erased. Therefore, if you have any data on instance store volumes that you want to keep, be sure to back it up to persistent storage.
In the confirmation dialog box, click Yes, Stop. It can take a few minutes for the instance to stop.

With the instance still selected, click Actions, select Instance Settings, and then click Change Instance Type.

In the Change Instance Type dialog box, do one of the following:

If the instance type of your instance is EBS–optimized by default, EBS-optimized is selected and you can't deselect it. You can click Cancel, because EBS optimization is already enabled for the instance.
If the instance type of your instance supports EBS optimization, select EBS-optimized, and then click Apply.
If the instance type of your instance does not support EBS optimization, EBS-optimized is deselected and you can't select it. You can select an instance type from Instance Type that supports EBS optimization, select EBS-optimized, and then click Apply.
Click Actions, select Instance State, and then click Start.

To enable EBS optimization for a running instance using the command line

You can use one of the following options with the corresponding command. For more information about these command line interfaces, see Accessing Amazon EC2.

--ebs-optimized with modify-instance-attribute (AWS CLI)
-EbsOptimized with Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)

Amazon EBS Encryption

Amazon EBS encryption offers you a simple encryption solution for your EBS volumes without the need for you to build, maintain, and secure your own key management infrastructure. When you create an encrypted EBS volume and attach it to a supported instance type, the following types of data are encrypted:

Data at rest inside the volume
All data moving between the volume and the instance
All snapshots created from the volume
The encryption occurs on the servers that host EC2 instances, providing encryption of data-in-transit from EC2 instances to EBS storage.

Amazon EBS encryption uses AWS Key Management Service (AWS KMS) customer master keys (CMK) when creating encrypted volumes and any snapshots created from them. The first time you create an encrypted volume in a region, a default CMK is created for you automatically. This key is used for Amazon EBS encryption unless you select a CMK that you created separately using AWS KMS. Creating your own CMK gives you more flexibility, including the ability to create, rotate, and disable keys to define access controls, and to audit the encryption keys used to protect your data. For more information, see the AWS Key Management Service Developer Guide.

This feature is supported with all EBS volume types (General Purpose SSD [gp2], Provisioned IOPS SSD [io1], Throughput Optimized HDD [st1], Cold HDD [sc1], and Magnetic [standard]). You can expect the same IOPS performance on encrypted volumes as you would with unencrypted volumes, with a minimal effect on latency. You can access encrypted volumes the same way that you access unencrypted volumes. Encryption and decryption are handled transparently and they require no additional action from you, your EC2 instance, or your application.

Snapshots that are taken from encrypted volumes are automatically encrypted. Volumes that are created from encrypted snapshots are also automatically encrypted. Public snapshots of encrypted volumes are not supported, but you can share an encrypted snapshot with specific accounts if you take the following steps:

Use a custom CMK, not your default CMK, to encrypt your volume.

Give the specific accounts access to the custom CMK.

Create the snapshot.

Give the specific accounts access to the snapshot.

For more information, see Sharing an Amazon EBS Snapshot.

Amazon EBS encryption is only available on certain instance types. You can attach both encrypted and unencrypted volumes to a supported instance type. For more information, see Supported Instance Types.

Contents

Encryption Key Management
Supported Instance Types
Changing the Encryption State of Your Data
Amazon EBS Encryption and CloudWatch Events
Encryption Key Management

Amazon EBS encryption handles key management for you. Each newly created volume is encrypted with a unique 256-bit key. Any snapshots of this volume and any subsequent volumes created from those snapshots also share that key. These keys are protected by AWS key management infrastructure, which implements strong logical and physical security controls to prevent unauthorized access. Your data and associated keys are encrypted using the industry standard AES-256 algorithm.

You cannot change the CMK that is associated with an existing snapshot or encrypted volume. However, you can associate a different CMK during a snapshot copy operation (including encrypting a copy of an unencrypted snapshot) and the resulting copied snapshot use the new CMK.

The AWS overall key management infrastructure is consistent with National Institute of Standards and Technology (NIST) 800-57 recommendations and uses cryptographic algorithms approved by Federal Information Processing Standards (FIPS) 140-2.

Each AWS account has a unique master key that is stored separately from your data, on a system that is surrounded with strong physical and logical security controls. Each encrypted volume (and its subsequent snapshots) is encrypted with a unique volume encryption key that is then encrypted with a region-specific secure master key. The volume encryption keys are used in memory on the server that hosts your EC2 instance; they are never stored on disk in plaintext.

Supported Instance Types

Amazon EBS encryption is available on the instance types listed in the table below. These instance types leverage the Intel AES New Instructions (AES-NI) instruction set to provide faster and simpler data protection. You can attach both encrypted and unencrypted volumes to these instance types simultaneously.

Instance family	Instance types that support Amazon EBS encryption
General purpose
m3.medium | m3.large | m3.xlarge | m3.2xlarge | m4.large | m4.xlarge | m4.2xlarge | m4.4xlarge | m4.10xlarge | m4.16xlarge | t2.nano | t2.micro | t2.small | t2.medium | t2.large | t2.xlarge | t2.2xlarge
Compute optimized
c4.large | c4.xlarge | c4.2xlarge | c4.4xlarge | c4.8xlarge | c3.large | c3.xlarge | c3.2xlarge | c3.4xlarge | c3.8xlarge
Memory optimized
cr1.8xlarge | r3.large | r3.xlarge | r3.2xlarge | r3.4xlarge | r3.8xlarge | r4.large | r4.xlarge | r4.2xlarge | r4.4xlarge | r4.8xlarge | r4.16xlarge | x1.16xlarge | x1.32xlarge
Storage optimized
d2.xlarge | d2.2xlarge | d2.4xlarge | d2.8xlarge | i2.xlarge | i2.2xlarge | i2.4xlarge | i2.8xlarge | i3.large | i3.xlarge | i3.2xlarge | i3.4xlarge | i3.8xlarge | i3.16xlarge
Accelerated computing
f1.2xlarge | f1.16xlarge | g2.2xlarge | g2.8xlarge | g3.4xlarge | g3.8xlarge | g3.16xlarge | p2.xlarge | p2.8xlarge | p2.16xlarge
For more information about these instance types, see Instance Type Details.

Changing the Encryption State of Your Data

There is no direct way to encrypt an existing unencrypted volume, or to remove encryption from an encrypted volume. However, you can migrate data between encrypted and unencrypted volumes. You can also apply a new encryption status while copying a snapshot:

While copying an unencrypted snapshot of an unencrypted volume, you can encrypt the copy. Volumes restored from this encrypted copy are also encrypted.
While copying an encrypted snapshot of an encrypted volume, you can re-encrypt the copy using a different CMK. Volumes restored from the encrypted copy are only accessible using the newly applied CMK.
You cannot remove encryption from an encrypted snapshot.

Migrate Data between Encrypted and Unencrypted Volumes

When you have access to both an encrypted and unencrypted volume, you can freely transfer data between them. EC2 carries out the encryption or decryption operations transparently.

To migrate data between encrypted and unencrypted volumes

Create your destination volume (encrypted or unencrypted, depending on your need) by following the procedures in Creating an Amazon EBS Volume.

Attach the destination volume to the instance that hosts the data to migrate. For more information, see Attaching an Amazon EBS Volume to an Instance.

Make the destination volume available by following the procedures in Making an Amazon EBS Volume Available for Use. For Linux instances, you can create a mount point at /mnt/destination and mount the destination volume there.

Copy the data from your source directory to the destination volume. It may be most convenient to use a bulk-copy utility for this.

Linux

Use the rsync command as follows to copy the data from your source to the destination volume. In this example, the source data is located in /mnt/source and the destination volume is mounted at /mnt/destination.

Copy
[ec2-user ~]$ sudo rsync -avh --progress /mnt/source/ /mnt/destination/
Windows

At a command prompt, use the robocopy command to copy the data from your source to the destination volume. In this example, the source data is located in D:\ and the destination volume is mounted at E:\.

Copy
PS C:\> robocopy D:\ E:\ /e /copyall /eta
Apply Encryption While Copying a Snapshot

Because you can apply encryption to a snapshot while copying it, another path to encrypting your data is the following procedure.

To encrypt a volume's data by means of snapshot copying

Create a snapshot of your unencrypted EBS volume. This snapshot is also unencrypted.

Copy the snapshot while applying encryption parameters. The resulting target snapshot is encrypted.

Restore the encrypted snapshot to a new volume, which is also encrypted.

For more information, see Copying an Amazon EBS Snapshot.

Re-Encrypt a Snapshot with a New CMK

The ability to encrypt a snapshot during copying also allows you to re-encrypt an already-encrypted snapshot that you own. In this operation, the plaintext of your snapshot is encrypted using a new CMK that you provide. Volumes restored from the resulting copy are only accessible using the new CMK.

In a related scenario, you may choose to re-encrypt a snapshot that has been shared with you. Before you can restore a volume from a shared encrypted snapshot, you must create your own copy of it. By default, the copy is encrypted with the key shared by the snapshot's owner. However, we recommend that you re-encrypt the snapshot during the copy process with a different key that you control. This protects your access to the volume if the original key is compromised, or if the owner revokes the key for any reason.

The following procedure demonstrates how to re-encrypt a snapshot that you own.

To re-encrypt a snapshot using the console

Create a custom CMK. For more information, see AWS Key Management Service Developer Guide.

Create an EBS volume encrypted with (for this example) your default CMK.

Create a snapshot of your encrypted EBS volume. This snapshot is also encrypted with your default CMK.

On the Snapshots page, choose Actions, Copy.

In the Copy Snapshot window, supply the complete ARN for your custom CMK (in the form arn:aws:kms:us-east-1:012345678910:key/abcd1234-a123-456a-a12b-a123b4cd56ef) in the Master Key field, or choose it from the menu. Choose Copy.

The resulting copy of the snapshot—and all volumes restored from it—are encrypted with your custom CMK.

The following procedure demonstrates how to re-encrypt a shared encrypted snapshot as you copy it. For this to work, you need access permissions to both the shared encrypted snapshot and to the CMK that encrypted it.

To copy and re-encrypt a shared snapshot using the console

Select the shared encrypted snapshot on the Snapshots page and choose Actions, Copy.

In the Copy Snapshot window, supply the complete ARN for a CMK that you own (in the form arn:aws:kms:us-east-1:012345678910:key/abcd1234-a123-456a-a12b-a123b4cd56ef) in the Master Key field, or choose it from the menu. Choose Copy.

The resulting copy of the snapshot—and all volumes restored from it—are encrypted with the CMK that you supplied. Changes to the original shared snapshot, its encryption status, or the shared CMK have no effect on your copy.

For more information, see Copying an Amazon EBS Snapshot.

Amazon EBS Encryption and CloudWatch Events

Amazon EBS supports Amazon CloudWatch Events for certain encryption-related scenarios. For more information, see Amazon CloudWatch Events for Amazon EBS.

Amazon EBS Volume Performance on Linux Instances

Several factors, including I/O characteristics and the configuration of your instances and volumes, can affect the performance of Amazon EBS. Customers who follow the guidance on our Amazon EBS and Amazon EC2 product detail pages typically achieve good performance out of the box. However, there are some cases where you may need to do some tuning in order achieve peak performance on the platform. This topic discusses general best practices as well as performance tuning that is specific to certain use cases. We recommend that you tune performance with information from your actual workload, in addition to benchmarking, to determine your optimal configuration. After you learn the basics of working with EBS volumes, it's a good idea to look at the I/O performance you require and at your options for increasing Amazon EBS performance to meet those requirements.

Contents

Amazon EBS Performance Tips
Amazon EC2 Instance Configuration
I/O Characteristics and Monitoring
Initializing Amazon EBS Volumes
RAID Configuration on Linux
Benchmark EBS Volumes
Amazon EBS Performance Tips

These tips represent best practices for getting optimal performance from your EBS volumes in a variety of user scenarios.

Use EBS-Optimized Instances

On instances without support for EBS-optimized throughput, network traffic can contend with traffic between your instance and your EBS volumes; on EBS-optimized instances, the two types of traffic are kept separate. Some EBS-optimized instance configurations incur an extra cost (such as C3, R3, and M3), while others are always EBS-optimized at no extra cost (such as M4, C4, and D2). For more information, see Amazon EC2 Instance Configuration.

Understand How Performance is Calculated

When you measure the performance of your EBS volumes, it is important to understand the units of measure involved and how performance is calculated. For more information, see I/O Characteristics and Monitoring.

Understand Your Workload

There is a relationship between the maximum performance of your EBS volumes, the size and number of I/O operations, and the time it takes for each action to complete. Each of these factors (performance, I/O, and latency) affects the others, and different applications are more sensitive to one factor or another. For more information, see Benchmark EBS Volumes.

Be Aware of the Performance Penalty When Initializing Volumes from Snapshots

There is a significant increase in latency when you first access each block of data on a new EBS volume that was restored from a snapshot. You can avoid this performance hit by accessing each block prior to putting the volume into production. This process is called initialization (formerly known as pre-warming). For more information, see Initializing Amazon EBS Volumes.

Factors That Can Degrade HDD Performance

When you create a snapshot of a Throughput Optimized HDD (st1) or Cold HDD (sc1) volume, performance may drop as far as the volume's baseline value while the snapshot is in progress. This behavior is specific to these volume types. Other factors that can limit performance include driving more throughput than the instance can support, the performance penalty encountered while initializing volumes restored from a snapshot, and excessive amounts of small, random I/O on the volume. For more information about calculating throughput for HDD volumes, see Amazon EBS Volume Types .

Your performance can also be impacted if your application isn’t sending enough I/O requests. This can be monitored by looking at your volume’s queue length and I/O size. The queue length is the number of pending I/O requests from your application to your volume. For maximum consistency, HDD-backed volumes must maintain a queue length (rounded to the nearest whole number) of 4 or more when performing 1 MiB sequential I/O. For more information about ensuring consistent performance of your volumes, see I/O Characteristics and Monitoring

Increase Read-Ahead for High-Throughput, Read-Heavy Workloads on st1 and sc1

Some workloads are read-heavy and access the block device through the operating system page cache (for example, from a file system). In this case, to achieve the maximum throughput, we recommend that you configure the read-ahead setting to 1 MiB. This is a per-block-device setting that should only be applied to your HDD volumes. The following examples assume that you are on an Amazon Linux instance.

To examine the current value of read-ahead for your block devices, use the following command:

Copy
[ec2-user ~]$ sudo blockdev --report /dev/<device>
Block device information is returned in the following format:

RO    RA   SSZ   BSZ   StartSec            Size   Device
rw   256   512  4096       4096      8587820544   /dev/<device>
The device shown reports a read-ahead value of 256 (the default). Multiply this number by the sector size (512 bytes) to obtain the size of the read-ahead buffer, which in this case is 128 KiB. To set the buffer value to 1 MiB, use the following command:

Copy
[ec2-user ~]$ sudo blockdev --setra 2048 /dev/<device>
Verify that the read-ahead setting now displays 2,048 by running the first command again.

Only use this setting when your workload consists of large, sequential I/Os. If it consists mostly of small, random I/Os, this setting will actually degrade your performance. In general, if your workload consists mostly of small or random I/Os, you should consider using a General Purpose SSD (gp2) volume rather than st1 or sc1.

Use a Modern Linux Kernel

Use a modern Linux kernel with support for indirect descriptors. Any Linux kernel 3.11 and above has this support, as well as any current-generation EC2 instance. If your average I/O size is at or near 44 KiB, you may be using an instance or kernel without support for indirect descriptors. For information about deriving the average I/O size from Amazon CloudWatch metrics, see I/O Characteristics and Monitoring.

To achieve maximum throughput on st1 or sc1 volumes, we recommend applying a value of 256 to the xen_blkfront.max parameter (for Linux kernel versions below 4.6) or the xen_blkfront.max_indirect_segments parameter (for Linux kernel version 4.6 and above). The appropriate parameter can be set in your OS boot command line.

For example, in an Amazon Linux AMI with an earlier kernel, you can add it to the end of the kernel line in the GRUB configuration found in /boot/grub/menu.lst:

Copy
kernel /boot/vmlinuz-4.4.5-15.26.amzn1.x86_64 root=LABEL=/ console=ttyS0 xen_blkfront.max=256
For a later kernel, the command would be similar to the following:

Copy
kernel /boot/vmlinuz-4.9.20-11.31.amzn1.x86_64 root=LABEL=/ console=tty1 console=ttyS0 xen_blkfront.max_indirect_segments=256
Reboot your instance for this setting to take effect.

For more information, see Configuring GRUB. Other Linux distributions, especially those that do not use the GRUB boot loader, may require a different approach to adjusting the kernel parameters.

For more information about EBS I/O characteristics, see the Amazon EBS: Designing for Performance re:Invent presentation on this topic.

Use RAID 0 to Maximize Utilization of Instance Resources

Some instance types can drive more I/O throughput than what you can provision for a single EBS volume. You can join multiple gp2, io1, st1, or sc1 volumes together in a RAID 0 configuration to use the available bandwidth for these instances. For more information, see RAID Configuration on Linux.

Track Performance with Amazon CloudWatch

Amazon Web Services provides performance metrics for Amazon EBS that you can analyze and view with Amazon CloudWatch and status checks that you can use to monitor the health of your volumes. For more information, see Monitoring the Status of Your Volumes.

Amazon EC2 Instance Configuration

When you plan and configure EBS volumes for your application, it is important to consider the configuration of the instances that you will attach the volumes to. In order to get the most performance out of your EBS volumes, you should attach them to an instance with enough bandwidth to support your volumes, such as an EBS-optimized instance or an instance with 10 Gigabit network connectivity. This is especially important when you stripe multiple volumes together in a RAID configuration.

Use EBS-Optimized or 10 Gigabit Network Instances

Any performance-sensitive workloads that require minimal variability and dedicated Amazon EC2 to Amazon EBS traffic, such as production databases or business applications, should use volumes that are attached to an EBS-optimized instance or an instance with 10 Gigabit network connectivity. EC2 instances that do not meet this criteria offer no guarantee of network resources. The only way to ensure sustained reliable network bandwidth between your EC2 instance and your EBS volumes is to launch the EC2 instance as EBS-optimized or choose an instance type with 10 Gigabit network connectivity. To see which instance types include 10 Gigabit network connectivity, see Instance Type Details. For information about configuring EBS-optimized instances, see Amazon EBS–Optimized Instances.

Choose an EC2 Instance with Enough Bandwidth

Launching an instance that is EBS-optimized provides you with a dedicated connection between your EC2 instance and your EBS volume. However, it is still possible to provision EBS volumes that exceed the available bandwidth for certain instance types, especially when multiple volumes are striped in a RAID configuration. The following table shows which instance types are available to be launched as EBS-optimized, the dedicated throughput to instance types are available to be launched as EBS-optimized, the dedicated bandwidth to Amazon EBS, the maximum amount of IOPS the instance can support if you are using a 16 KB I/O size, and the approximate I/O bandwidth available on that connection in MB/s. Be sure to choose an EBS-optimized instance that provides more dedicated EBS throughput than your application needs; otherwise, the Amazon EBS to Amazon EC2 connection will become a performance bottleneck.

Note
The table below and the following examples use 16 KB as an I/O size for explanatory purposes only; your application I/O size may vary (Amazon EBS measures each I/O operation per second that is 256 KiB or smaller as one IOPS). For more information about IOPS and the relationship between I/O size and volume throughput limits, see I/O Characteristics and Monitoring.
Instance type	EBS-optimized by default	Max. bandwidth (Mbps)*	Expected throughput (MB/s)**	Max. IOPS (16 KB I/O size)**
c1.xlarge		1,000	125	8,000
c3.xlarge		500	62.5	4,000
c3.2xlarge		1,000	125	8,000
c3.4xlarge		2,000	250	16,000
c4.large	Yes	500	62.5	4,000
c4.xlarge	Yes	750	93.75	6,000
c4.2xlarge	Yes	1,000	125	8,000
c4.4xlarge	Yes	2,000	250	16,000
c4.8xlarge	Yes	4,000	500	32,000
d2.xlarge	Yes	750	93.75	6,000
d2.2xlarge	Yes	1,000	125	8,000
d2.4xlarge	Yes	2,000	250	16,000
d2.8xlarge	Yes	4,000	500	32,000
f1.2xlarge	Yes	1,700	200	12,000
f1.16xlarge	Yes	14,000	1,750	75,000
g2.2xlarge		1,000	125	8,000
g3.4xlarge	Yes	3,500	437	20,000
g3.8xlarge	Yes	7,000	875	40,000
g3.16xlarge	Yes	14,000	1,750	80,000
i2.xlarge		500	62.5	4,000
i2.2xlarge		1,000	125	8,000
i2.4xlarge		2,000	250	16,000
i3.large	Yes	425	50	3000
i3.xlarge	Yes	850	100	6000
i3.2xlarge	Yes	1,700	200	12,000
i3.4xlarge	Yes	3,500	400	16,000
i3.8xlarge	Yes	7,000	850	32,500
i3.16xlarge	Yes	14,000	1,750	65,000
m1.large		500	62.5	4,000
m1.xlarge		1,000	125	8,000
m2.2xlarge		500	62.5	4,000
m2.4xlarge		1,000	125	8,000
m3.xlarge		500	62.5	4,000
m3.2xlarge		1,000	125	8,000
m4.large	Yes	450	56.25	3,600
m4.xlarge	Yes	750	93.75	6,000
m4.2xlarge	Yes	1,000	125	8,000
m4.4xlarge	Yes	2,000	250	16,000
m4.10xlarge	Yes	4,000	500	32,000
m4.16xlarge	Yes	10,000	1,250	65,000
p2.xlarge	Yes	750	93.75	6,000
p2.8xlarge	Yes	5,000	625	32,500
p2.16xlarge	Yes	10,000	1,250	65,000
r3.xlarge		500	62.5	4,000
r3.2xlarge		1,000	125	8,000
r3.4xlarge		2,000	250	16,000
r4.large	Yes	437	54	3,000
r4.xlarge	Yes	875	109	6,000
r4.2xlarge	Yes	1,750	218	12,000
r4.4xlarge	Yes	3,500	437	18,750
r4.8xlarge	Yes	7,000	875	37,500
r4.16xlarge	Yes	14,000	1,750	75,000
x1.16xlarge	Yes	7,000	875	40,000
x1.32xlarge	Yes	14,000	1,750	80,000
* These instance types must be launched as EBS-optimized to consistently achieve this level of performance.

** This value is a rounded approximation based on a 100% read-only workload and it is provided as a baseline configuration aid. EBS-optimized connections are full-duplex, and can drive more throughput and IOPS in a 50/50 read/write workload where both communication lanes are used. In some cases, network, file system, and Amazon EBS encryption overhead can reduce the maximum throughput and IOPS available.

Note that some instances with 10-gigabit network interfaces, such as i2.8xlarge, c3.8xlarge, and r3.8xlarge, do not offer EBS-optimization, and therefore do not have dedicated EBS bandwidth available and are not listed here. However, you can use all of that bandwidth for traffic to Amazon EBS if your application isn’t pushing other network traffic that contends with Amazon EBS. Some other 10-gigabit network instances, such as c4.8xlarge and d2.8xlarge offer dedicated Amazon EBS bandwidth in addition to a 10-gigabit interface which is used exclusively for network traffic.

The m1.large instance has a maximum 16 KB IOPS value of 4,000, but unless this instance type is launched as EBS-optimized, that value is an absolute best-case scenario and is not guaranteed; to consistently achieve 4,000 16 KB IOPS, you must launch this instance as EBS-optimized. However, if a 4,000 IOPS io1 volume is attached to an EBS-optimized m1.large instance, the Amazon EC2 to Amazon EBS connection bandwidth limit prevents this volume from providing the 320 MB/s maximum aggregate throughput available to it. In this case, we must use an EBS-optimized EC2 instance that supports at least 320 MB/s of throughput, such as the c4.8xlarge instance type.

Volumes of type General Purpose SSD (gp2) have a throughput limit between 128 MB/s and 160 MB/s per volume (depending on volume size), which pairs well with a 1,000 Mbps EBS-optimized connection. Instance types that offer more than 1,000 Mbps of throughput to Amazon EBS can use more than one gp2 volume to take advantage of the available throughput. Volumes of type Provisioned IOPS SSD (io1) have a throughput limit range of 256 KiB for each IOPS provisioned, up to a maximum of 320 MiB/s (at 1,280 IOPS). For more information, see Amazon EBS Volume Types.

Instance types with 10 Gigabit network connectivity support up to 800 MB/s of throughput and 48,000 16K IOPS for unencrypted Amazon EBS volumes and up to 25,000 16K IOPS for encrypted Amazon EBS volumes. Because the maximum io1 value for EBS volumes is 20,000 for io1 volumes and 10,000 for gp2 volumes, you can use several EBS volumes simultaneously to reach the level of I/O performance available to these instance types. For more information about which instance types include 10 Gigabit network connectivity, see Instance Type Details.

You should use EBS-optimized instances when available to get the full performance benefits of Amazon EBS gp2 and io1 volumes. For more information, see Amazon EBS–Optimized Instances.

I/O Characteristics and Monitoring

On a given volume configuration, certain I/O characteristics drive the performance behavior for your EBS volumes. SSD-backed volumes—General Purpose SSD (gp2) and Provisioned IOPS SSD (io1)—deliver consistent performance whether an I/O operation is random or sequential. HDD-backed volumes—Throughput Optimized HDD (st1) and Cold HDD (sc1)—deliver optimal performance only when I/O operations are large and sequential. To understand how SSD and HDD volumes will perform in your application, it is important to know the connection between demand on the volume, the quantity of IOPS available to it, the time it takes for an I/O operation to complete, and the volume's throughput limits.

IOPS

IOPS are a unit of measure representing input/output operations per second. The operations are measured in KiB, and the underlying drive technology determines the maximum amount of data that a volume type counts as a single I/O. I/O size is capped at 256 KiB for SSD volumes and 1,024 KiB for HDD volumes because SSD volumes handle small or random I/O much more efficiently than HDD volumes.

When small I/O operations are physically contiguous, Amazon EBS attempts to merge them into a single I/O up to the maximum size. For example, for SSD volumes, a single 1,024 KiB I/O operation counts as 4 operations (1,024÷256=4), while 8 contiguous I/O operations at 32 KiB each count as 1operation (8×32=256). However, 8 random I/O operations at 32 KiB each count as 8 operations. Each I/O operation under 32 KiB counts as 1 operation.

Similarly, for HDD-backed volumes, both a single 1,024 KiB I/O operation and 8 sequential 128 KiB operations would count as one operation. However, 8 random 128 KiB I/O operations would count as 8 operations.

Consequently, when you create an SSD-backed volume supporting 3,000 IOPS (either by provisioning an io1 volume at 3,000 IOPS or by sizing a gp2 volume at 1000 GiB), and you attach it to an EBS-optimized instance that can provide sufficient bandwidth, you can transfer up to 3,000 I/Os of data per second, with throughput determined by I/O size.

Volume Queue Length and Latency

The volume queue length is the number of pending I/O requests for a device. Latency is the true end-to-end client time of an I/O operation, in other words, the time elapsed between sending an I/O to EBS and receiving an acknowledgement from EBS that the I/O read or write is complete. Queue length must be correctly calibrated with I/O size and latency to avoid creating bottlenecks either on the guest operating system or on the network link to EBS.

Optimal queue length varies for each workload, depending on your particular application's sensitivity to IOPS and latency. If your workload is not delivering enough I/O requests to fully use the performance available to your EBS volume, then your volume might not deliver the IOPS or throughput that you have provisioned.

Transaction-intensive applications are sensitive to increased I/O latency and are well-suited for SSD-backed io1 and gp2 volumes. You can maintain high IOPS while keeping latency down by maintaining a low queue length and a high number of IOPS available to the volume. Consistently driving more IOPS to a volume than it has available can cause increased I/O latency.

Throughput-intensive applications are less sensitive to increased I/O latency, and are well-suited for HDD-backed st1 and sc1 volumes. You can maintain high throughput to HDD-backed volumes by maintaining a high queue length when performing large, sequential I/O.

I/O size and volume throughput limits

For SSD-backed volumes, if your I/O size is very large, you may experience a smaller number of IOPS than you provisioned because you are hitting the throughput limit of the volume. For example, a gp2 volume under 1000 GiB with burst credits available has an IOPS limit of 3,000 and a volume throughput limit of 160 MiB/s. If you are using a 256 KiB I/O size, your volume reaches its throughput limit at 640 IOPS (640 x 256 KiB = 160 MiB). For smaller I/O sizes (such as 16 KiB), this same volume can sustain 3,000 IOPS because the throughput is well below 160 MiB/s. (These examples assume that your volume's I/O is not hitting the throughput limits of the instance.) For more information about the throughput limits for each EBS volume type, see Amazon EBS Volume Types.

For smaller I/O operations, you may see a higher-than-provisioned IOPS value as measured from inside your instance. This happens when the instance operating system merges small I/O operations into a larger operation before passing them to Amazon EBS.

If your workload uses sequential I/Os on HDD-backed st1 and sc1 volumes, you may experience a higher than expected number of IOPS as measured from inside your instance. This happens when the instance operating system merges sequential I/Os and counts them in 1,024 KiB-sized units. If your workload uses small or random I/Os, you may experience a lower throughput than you expect. This is because we count each random, non-sequential I/O toward the total IOPS count, which can cause you to hit the volume's IOPS limit sooner than expected.

Whatever your EBS volume type, if you are not experiencing the IOPS or throughput you expect in your configuration, ensure that your EC2 instance bandwidth is not the limiting factor. You should always use a current-generation, EBS-optimized instance (or one that includes 10 Gb/s network connectivity) for optimal performance. For more information, see Amazon EC2 Instance Configuration. Another possible cause for not experiencing the expected IOPS is that you are not driving enough I/O to the EBS volumes.

Monitor I/O Characteristics with CloudWatch

You can monitor these I/O characteristics with each volume's CloudWatch metrics. Important metrics to consider include:

BurstBalance
VolumeReadBytes
VolumeWriteBytes
VolumeReadOps
VolumeWriteOps
VolumeQueueLength
BurstBalance displays the burst bucket balance for gp2, st1, and sc1 volumes as a percentage of the remaining balance. When your burst bucket is depleted, volume I/O credits (for gp2 volumes) or volume throughput credits (for st1 and sc1 volumes) is throttled to the baseline. Check the BurstBalance value to determine whether your volume is being throttled for this reason.

HDD-backed st1 and sc1 volumes are designed to perform best with workloads that take advantage of the 1,024 KiB maximum I/O size. To determine your volume's average I/O size, divide VolumeWriteBytes by VolumeWriteOps. The same calculation applies to read operations. If average I/O size is below 64 KiB, increasing the size of the I/O operations sent to an st1 or sc1 volume should improve performance.

Note
If average I/O size is at or near 44 KiB, you may be using an instance or kernel without support for indirect descriptors. Any Linux kernel 3.8 and above has this support, as well as any current-generation instance.
If your I/O latency is higher than you require, check VolumeQueueLength to make sure your application is not trying to drive more IOPS than you have provisioned. If your application requires a greater number of IOPS than your volume can provide, you should consider using a larger gp2 volume with a higher base performance level or an io1 volume with more provisioned IOPS to achieve faster latencies.

For more information about Amazon EBS I/O characteristics, see the Amazon EBS: Designing for Performance re:Invent presentation on this topic.

Initializing Amazon EBS Volumes

New EBS volumes receive their maximum performance the moment that they are available and do not require initialization (formerly known as pre-warming). However, storage blocks on volumes that were restored from snapshots must be initialized (pulled down from Amazon S3 and written to the volume) before you can access the block. This preliminary action takes time and can cause a significant increase in the latency of an I/O operation the first time each block is accessed. For most applications, amortizing this cost over the lifetime of the volume is acceptable. Performance is restored after the data is accessed once.

You can avoid this performance hit in a production environment by reading from all of the blocks on your volume before you use it; this process is called initialization. For a new volume created from a snapshot, you should read all the blocks that have data before using the volume.

Important
While initializing io1 volumes that were restored from snapshots, the performance of the volume may drop below 50 percent of its expected level, which causes the volume to display a warning state in the I/O Performance status check. This is expected, and you can ignore the warning state on io1 volumes while you are initializing them. For more information, see Monitoring Volumes with Status Checks.
Initializing Amazon EBS Volumes on Linux

New EBS volumes receive their maximum performance the moment that they are available and do not require initialization (formerly known as pre-warming). For volumes that have been restored from snapshots, use the dd or fio utilities to read from all of the blocks on a volume. All existing data on the volume will be preserved.

To initialize a volume restored from a snapshot on Linux

Attach the newly-restored volume to your Linux instance.

Use the lsblk command to list the block devices on your instance.

Copy
[ec2-user ~]$ lsblk
NAME  MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvdf  202:80   0  30G  0 disk
xvda1 202:1    0   8G  0 disk /
Here you can see that the new volume, /dev/xvdf, is attached, but not mounted (because there is no path listed under the MOUNTPOINT column).

Use the dd or fio utilities to read all of the blocks on the device. The dd command is installed by default on Linux systems, but fio is considerably faster because it allows multi-threaded reads.

Note
This step may take several minutes up to several hours, depending on your EC2 instance bandwidth, the IOPS provisioned for the volume, and the size of the volume.
[dd] The if (input file) parameter should be set to the drive you wish to initialize. The of (output file) parameter should be set to the Linux null virtual device, /dev/null. The bs parameter sets the block size of the read operation; for optimal performance, this should be set to 1 MB.

Copy
[ec2-user ~]$ sudo dd if=/dev/xvdf of=/dev/null bs=1M
[fio] If you have fio installed on your system, use the following command initialize your volume. The --filename (input file) parameter should be set to the drive you wish to initialize.

Copy
[ec2-user ~]$ sudo fio --filename=/dev/xvdf --rw=read --bs=128k --iodepth=32 --ioengine=libaio --direct=1 --name=volume-initialize
To install fio on Amazon Linux, use the following command:

Copy
sudo yum install -y fio
To install fio on Ubuntu, use the following command:

Copy
sudo apt-get install -y fio
When the operation is finished, you will see a report of the read operation. Your volume is now ready for use. For more information, see Making an Amazon EBS Volume Available for Use.

RAID Configuration on Linux

With Amazon EBS, you can use any of the standard RAID configurations that you can use with a traditional bare metal server, as long as that particular RAID configuration is supported by the operating system for your instance. This is because all RAID is accomplished at the software level. For greater I/O performance than you can achieve with a single volume, RAID 0 can stripe multiple volumes together; for on-instance redundancy, RAID 1 can mirror two volumes together.

Amazon EBS volume data is replicated across multiple servers in an Availability Zone to prevent the loss of data from the failure of any single component. This replication makes Amazon EBS volumes ten times more reliable than typical commodity disk drives. For more information, see Amazon EBS Availability and Durability in the Amazon EBS product detail pages.

Note
You should avoid booting from a RAID volume. Grub is typically installed on only one device in a RAID array, and if one of the mirrored devices fails, you may be unable to boot the operating system.
If you need to create a RAID array on a Windows instance, see RAID Configuration on Windows in the Amazon EC2 User Guide for Windows Instances.

Contents

RAID Configuration Options
Creating a RAID Array on Linux
RAID Configuration Options

The following table compares the common RAID 0 and RAID 1 options.

Configuration	Use	Advantages	Disadvantages
RAID 0
When I/O performance is more important than fault tolerance; for example, as in a heavily used database (where data replication is already set up separately).
I/O is distributed across the volumes in a stripe. If you add a volume, you get the straight addition of throughput.
Performance of the stripe is limited to the worst performing volume in the set. Loss of a single volume results in a complete data loss for the array.
RAID 1
When fault tolerance is more important than I/O performance; for example, as in a critical application.
Safer from the standpoint of data durability.
Does not provide a write performance improvement; requires more Amazon EC2 to Amazon EBS bandwidth than non-RAID configurations because the data is written to multiple volumes simultaneously.
Important
RAID 5 and RAID 6 are not recommended for Amazon EBS because the parity write operations of these RAID modes consume some of the IOPS available to your volumes. Depending on the configuration of your RAID array, these RAID modes provide 20-30% fewer usable IOPS than a RAID 0 configuration. Increased cost is a factor with these RAID modes as well; when using identical volume sizes and speeds, a 2-volume RAID 0 array can outperform a 4-volume RAID 6 array that costs twice as much.
Creating a RAID 0 array allows you to achieve a higher level of performance for a file system than you can provision on a single Amazon EBS volume. A RAID 1 array offers a "mirror" of your data for extra redundancy. Before you perform this procedure, you need to decide how large your RAID array should be and how many IOPS you want to provision.

The resulting size of a RAID 0 array is the sum of the sizes of the volumes within it, and the bandwidth is the sum of the available bandwidth of the volumes within it. The resulting size and bandwidth of a RAID 1 array is equal to the size and bandwidth of the volumes in the array. For example, two 500 GiB Amazon EBS volumes with 4,000 provisioned IOPS each will create a 1000 GiB RAID 0 array with an available bandwidth of 8,000 IOPS and 640 MB/s of throughput or a 500 GiB RAID 1 array with an available bandwidth of 4,000 IOPS and 320 MB/s of throughput.

This documentation provides basic RAID setup examples. For more information about RAID configuration, performance, and recovery, see the Linux RAID Wiki at https://raid.wiki.kernel.org/index.php/Linux_Raid.

Creating a RAID Array on Linux

Use the following procedure to create the RAID array. Note that you can get directions for Windows instances from Creating a RAID Array on Windows in the Amazon EC2 User Guide for Windows Instances.

To create a RAID array on Linux

Create the Amazon EBS volumes for your array. For more information, see Creating an Amazon EBS Volume.

Important
Create volumes with identical size and IOPS performance values for your array. Make sure you do not create an array that exceeds the available bandwidth of your EC2 instance. For more information, see Amazon EC2 Instance Configuration.
Attach the Amazon EBS volumes to the instance that you want to host the array. For more information, see Attaching an Amazon EBS Volume to an Instance.

Use the mdadm command to create a logical RAID device from the newly attached Amazon EBS volumes. Substitute the number of volumes in your array for number_of_volumes and the device names for each volume in the array (such as /dev/xvdf) for device_name. You can also substitute MY_RAID with your own unique name for the array.

Note
You can list the devices on your instance with the lsblk command to find the device names.
(RAID 0 only) To create a RAID 0 array, execute the following command (note the --level=0 option to stripe the array):

Copy
[ec2-user ~]$ sudo mdadm --create --verbose /dev/md0 --level=0 --name=MY_RAID --raid-devices=number_of_volumes device_name1 device_name2
(RAID 1 only) To create a RAID 1 array, execute the following command (note the --level=1 option to mirror the array):

Copy
[ec2-user ~]$ sudo mdadm --create --verbose /dev/md0 --level=1 --name=MY_RAID --raid-devices=number_of_volumes device_name1 device_name2
Allow time for the RAID array to initialize and synchronize. You can track the progress of these operations with the following command:

Copy
[ec2-user ~]$ sudo cat /proc/mdstat
The following is example output:

Personalities : [raid1] 
md0 : active raid1 xvdg[1] xvdf[0]
      20955008 blocks super 1.2 [2/2] [UU]
      [=========>...........]  resync = 46.8% (9826112/20955008) finish=2.9min speed=63016K/sec
In general, you can display detailed information about your RAID array with the following command:

Copy
[ec2-user ~]$ sudo mdadm --detail /dev/md0
The following is example output:

/dev/md0:
        Version : 1.2
  Creation Time : Mon Jun 27 11:31:28 2016
     Raid Level : raid1
     Array Size : 20955008 (19.98 GiB 21.46 GB)
  Used Dev Size : 20955008 (19.98 GiB 21.46 GB)
   Raid Devices : 2
  Total Devices : 2
    Persistence : Superblock is persistent

    Update Time : Mon Jun 27 11:37:02 2016
          State : clean 
...
...
...

    Number   Major   Minor   RaidDevice State
       0     202       80        0      active sync   /dev/sdf
       1     202       96        1      active sync   /dev/sdg
Create a file system on your RAID array, and give that file system a label to use when you mount it later. For example, to create an ext4 file system with the label MY_RAID, execute the following command:

Copy
[ec2-user ~]$ sudo mkfs.ext4 -L MY_RAID /dev/md0
Depending on the requirements of your application or the limitations of your operating system, you can use a different file system type, such as ext3 or XFS (consult your file system documentation for the corresponding file system creation command).

Create a mount point for your RAID array.

Copy
[ec2-user ~]$ sudo mkdir -p /mnt/raid
Finally, mount the RAID device on the mount point that you created:

Copy
[ec2-user ~]$ sudo mount LABEL=MY_RAID /mnt/raid
Your RAID device is now ready for use.

(Optional) To mount this Amazon EBS volume on every system reboot, add an entry for the device to the /etc/fstab file.

Create a backup of your /etc/fstab file that you can use if you accidentally destroy or delete this file while you are editing it.

Copy
[ec2-user ~]$ sudo cp /etc/fstab /etc/fstab.orig
Open the /etc/fstab file using your favorite text editor, such as nano or vim.

Comment out any lines starting with "UUID=" and, at the end of the file, add a new line for your RAID volume using the following format:

device_label mount_point file_system_type fs_mntops fs_freq fs_passno
The last three fields on this line are the file system mount options, the dump frequency of the file system, and the order of file system checks done at boot time. If you don't know what these values should be, then use the values in the example below for them (defaults,nofail 0 2). For more information about /etc/fstab entries, see the fstab manual page (by entering man fstab on the command line). For example, to mount the ext4 file system on the device with the label MY_RAID at the mount point /mnt/raid, add the following entry to /etc/fstab.

Note
If you ever intend to boot your instance without this volume attached (for example, so this volume could move back and forth between different instances), you should add the nofail mount option that allows the instance to boot even if there are errors in mounting the volume. Debian derivatives, such as Ubuntu, must also add the nobootwait mount option.
Copy
LABEL=MY_RAID       /mnt/raid   ext4    defaults,nofail        0       2
After you've added the new entry to /etc/fstab, you need to check that your entry works. Run the sudo mount -a command to mount all file systems in /etc/fstab.

Copy
[ec2-user ~]$ sudo mount -a
If the previous command does not produce an error, then your /etc/fstab file is OK and your file system will mount automatically at the next boot. If the command does produce any errors, examine the errors and try to correct your /etc/fstab.

Warning
Errors in the /etc/fstab file can render a system unbootable. Do not shut down a system that has errors in the /etc/fstab file.
(Optional) If you are unsure how to correct /etc/fstab errors, you can always restore your backup /etc/fstab file with the following command.

Copy
[ec2-user ~]$ sudo mv /etc/fstab.orig /etc/fstab
Benchmark EBS Volumes

This section demonstrates how you can test the performance of Amazon EBS volumes by simulating I/O workloads. The process is as follows:

Launch an EBS-optimized instance.

Create new EBS volumes.

Attach the volumes to your EBS-optimized instance.

Configure and mount the block device.

Install a tool to benchmark I/O performance.

Benchmark the I/O performance of your volumes.

Delete your volumes and terminate your instance so that you don't continue to incur charges.

Important
Some of the procedures described in this topic will result in the destruction of existing data on the EBS volumes you benchmark. The benchmarking procedures are intended for use on volumes specially created for testing purposes, not production volumes.
Set Up Your Instance

To get optimal performance from EBS volumes, we recommend that you use an EBS-optimized instance. EBS-optimized instances deliver dedicated throughput between Amazon EC2 and Amazon EBS, with instance. EBS-optimized instances deliver dedicated bandwidth between Amazon EC2 and Amazon EBS, with options between 500 and 12,000 Mbps, depending on the instance type.

To create an EBS-optimized instance, choose Launch as an EBS-Optimized instance when launching the instance using the Amazon EC2 console, or specify --ebs-optimized when using the command line. Be sure that you launch a current-generation instance that supports this option. For the example tests in this topic, we recommend that you launch a c3.4xlarge instance. For more information, see Amazon EBS–Optimized Instances.

Setting up Provisioned IOPS SSD (io1) volumes

To create an io1 volume, choose Provisioned IOPS SSD when creating the volume using the Amazon EC2 console, or, at the command line, specify --type io1 --iops n where n is an integer between 100 and 20000. For information about creating EBS volumes, see Creating an Amazon EBS Volume. For information about attaching these volumes to your instance, see Attaching an Amazon EBS Volume to an Instance.

For the example tests, we recommend that you create a RAID array with 6 volumes, which offers a high level of performance. Because you are charged by gigabytes provisioned (and the number of provisioned IOPS for io1 volumes), not the number of volumes, there is no additional cost for creating multiple, smaller volumes and using them to create a stripe set. If you're using Oracle Orion to benchmark your volumes, it can simulate striping the same way that Oracle ASM does, so we recommend that you let Orion do the striping. If you are using a different benchmarking tool, you need to stripe the volumes yourself.

To create a six-volume stripe set on Amazon Linux, use a command such as the following:

Copy
[ec2-user ~]$ sudo mdadm --create /dev/md0 --level=0 --chunk=64 --raid-devices=6 /dev/sdf /dev/sdg /dev/sdh /dev/sdi /dev/sdj /dev/sdk
For this example, the file system is XFS. Use the file system that meets your requirements. Use the following command to install XFS file system support:

Copy
[ec2-user ~]$ sudo yum install -y xfsprogs
Then, use these commands to create, mount, and assign ownership to the XFS file system:

Copy
[ec2-user ~]$ sudo mkdir -p /mnt/p_iops_vol0 && sudo mkfs.xfs /dev/md0
[ec2-user ~]$ sudo mount -t xfs /dev/md0 /mnt/p_iops_vol0
[ec2-user ~]$ sudo chown ec2-user:ec2-user /mnt/p_iops_vol0/
Setting up Throughput Optimized HDD (st1) or Cold HDD (sc1) volumes

To create an st1 volume, choose Throughput Optimized HDD when creating the volume using the Amazon EC2 console, or specify --type st1 when using the command line. To create an sc1 volume, choose Cold HDD when creating the volume using the Amazon EC2 console, or specify --type sc1 when using the command line. For information about creating EBS volumes, see Creating an Amazon EBS Volume. For information about attaching these volumes to your instance, see Attaching an Amazon EBS Volume to an Instance.

AWS provides a JSON template for use with AWS CloudFormation that simplifies this setup procedure. Access the template and save it as a JSON file. AWS CloudFormation allows you to configure your own SSH keys and offers an easy way to set up a performance test environment to evaluate st1 volumes. The template creates a current-generation instance and a 2 TiB st1 volume, and attaches the volume to the instance at /dev/xvdf.

To create an HDD volume with the template

Open the AWS CloudFormation console at https://console.aws.amazon.com/cloudformation.

Choose Create Stack.

Choose Upload a Template to Amazon S3 and select the JSON template you previously obtained.

Give your stack a name like “ebs-perf-testing”, and select an instance type (the default is r3.8xlarge) and SSH key.

Choose Next twice, and then choose Create Stack.

After the status for your new stack moves from CREATE_IN_PROGRESS to COMPLETE, choose Outputs to get the public DNS entry for your new instance, which will have a 2 TiB st1 volume attached to it.

Connect using SSH to your new stack as user ec2-user, with the hostname obtained from the DNS entry in the previous step.

Proceed to Install Benchmark Tools.

Install Benchmark Tools

The following table lists some of the possible tools you can use to benchmark the performance of EBS volumes.

Tool	Description
fio
For benchmarking I/O performance. (Note that fio has a dependency on libaio-devel.)

To install fio on Amazon Linux, run the following command:

Copy
[ec2-user ~]$ sudo yum install -y fio
To install fio on Ubuntu, run the following command:

Copy
sudo apt-get install -y fio
Oracle Orion Calibration Tool
For calibrating the I/O performance of storage systems to be used with Oracle databases.
These benchmarking tools support a wide variety of test parameters. You should use commands that approximate the workloads your volumes will support. These commands provided below are intended as examples to help you get started.

Choosing the Volume Queue Length

Choosing the best volume queue length based on your workload and volume type.

Queue Length on SSD-backed Volumes

To determine the optimal queue length for your workload on SSD-backed volumes, we recommend that you target a queue length of 1 for every 500 IOPS available (baseline for gp2 volumes and the provisioned amount for io1 volumes). Then you can monitor your application performance and tune that value based on your application requirements.

Increasing the queue length is beneficial until you achieve the provisioned IOPS, throughput or optimal system queue length value, which is currently set to 32. For example, a volume with 1,000 provisioned IOPS should target a queue length of 2. You should experiment with tuning these values up or down to see what performs best for your application.

Queue Length on HDD-backed Volumes

To determine the optimal queue length for your workload on HDD-backed volumes, we recommend that you target a queue length of at least 4 while performing 1MiB sequential I/Os. Then you can monitor your application performance and tune that value based on your application requirements. For example, a 2 TiB st1 volume with burst throughput of 500 MiB/s and IOPS of 500 should target a queue length of 4, 8, or 16 while performing 1,024 KiB, 512 KiB, or 256 KiB sequential I/Os respectively. You should experiment with tuning these values value up or down to see what performs best for your application.

Perform Benchmarking

The following procedures describe benchmarking commands for various EBS volume types.

Run the following commands on an EBS-optimized instance with attached EBS volumes. If the EBS volumes were restored from snapshots, be sure to initialize them before benchmarking. For more information, see Initializing Amazon EBS Volumes.

When you are finished testing your volumes, see the following topics for help cleaning up: Deleting an Amazon EBS Volume and Terminate Your Instance.

Benchmarking io1 Volumes

Run fio on the stripe set that you created.

The following command performs 16 KB random write operations.

Copy
[ec2-user ~]$ sudo fio --directory=/mnt/p_iops_vol0 \
--name fio_test_file --direct=1 --rw=randwrite --bs=16k --size=1G \
--numjobs=16 --time_based --runtime=180 --group_reporting --norandommap
The following command performs 16 KB random read operations.

Copy
[ec2-user ~]$ sudo fio --directory=/mnt/p_iops_vol0 \
--name fio_test_file --direct=1 --rw=randread --bs=16k --size=1G \
--numjobs=16 --time_based --runtime=180 --group_reporting --norandommap 
For more information about interpreting the results, see this tutorial: Inspecting disk IO performance with fio.

Benchmarking st1 and sc1 Volumes

Run fio on your st1 or sc1 volume.

Note
Prior to running these tests, set buffered I/O on your instance as described in Increase Read-Ahead for High-Throughput, Read-Heavy Workloads on st1 and sc1.
The following command performs 1 MiB sequential read operations against an attached st1 block device (e.g., /dev/xvdf):

Copy
[ec2-user ~]$ sudo fio --filename=/dev/<device> --direct=1 --rw=read 
--randrepeat=0 --ioengine=libaio --bs=1024k --iodepth=8 --time_based=1 --runtime=180
--name=fio_direct_read_test
The following command performs 1 MiB sequential write operations against an attached st1 block device:

Copy
[ec2-user ~]$ sudo fio --filename=/dev/<device> --direct=1 --rw=write 
--randrepeat=0 --ioengine=libaio --bs=1024k --iodepth=8 --time_based=1 --runtime=180
--name=fio_direct_write_test 
Some workloads perform a mix of sequential reads and sequential writes to different parts of the block device. To benchmark such a workload, we recommend that you use separate, simultaneous fio jobs for reads and writes, and use the fio offset_increment option to target different block device locations for each job.

Running this workload is a bit more complicated than a sequential-write or sequential-read workload. Use a text editor to create a fio job file, called fio_rw_mix.cfg in this example, that contains the following:

Copy
[global] 
clocksource=clock_gettime
randrepeat=0
runtime=180
offset_increment=100g
 
[sequential-write]
bs=1M
ioengine=libaio
direct=1
iodepth=8
filename=/dev/<device>
do_verify=0
rw=write
rwmixread=0
rwmixwrite=100 

[sequential-read] 
bs=1M
ioengine=libaio
direct=1
iodepth=8
filename=/dev/<device>
do_verify=0
rw=read
rwmixread=100
rwmixwrite=0
Then run the following command:

Copy
[ec2-user ~]$ sudo fio fio_rw_mix.cfg
For more information about interpreting the results, see the Inspecting disk I/O performance with fio tutorial.

Multiple fio jobs for direct I/O, even though using sequential read or write operations, can result in lower than expected throughput for st1 and sc1 volumes. We recommend that you use one direct I/O job and use the iodepth parameter to control the number of concurrent I/O operations.

Amazon CloudWatch Events for Amazon EBS

Amazon EBS emits notifications based on Amazon CloudWatch Events for a variety of snapshot and encryption status changes. With CloudWatch Events, you can establish rules that trigger programmatic actions in response to a change in snapshot or encryption key state. For example, when a snapshot is created, you can trigger an AWS Lambda function to share the completed snapshot with another account or copy it to another region for disaster-recovery purposes.

For more information, see Using Events in the Amazon CloudWatch User Guide.

Event Definitions and Examples

This section defines the supported Amazon EBS events and provides examples of event output for specific scenarios. Events in CloudWatch are represented as JSON objects. For more information about the format and content of event objects, see Events and Event Patterns in the Amazon CloudWatch Events User Guide.

The fields that are unique to EBS events are contained in the "detail" section of the JSON objects shown below. The "event" field contains the event name. The "result" field contains the completed status of the action that triggered the event.

Create Snapshot (createSnapshot)

The createSnapshot event is sent to your AWS account when an action to create a snapshot completes. This event can have a result of either succeeded or failed.

Event Data

The listing below is an example of a JSON object emitted by EBS for a successful createSnapshot event. The source field contains the ARN of the source volume. The StartTime and EndTime fields indicate when creation of the snapshot started and completed.

Copy
{
  "version": "0",
  "id": "01234567-0123-0123-0123-012345678901",
  "detail-type": "EBS Snapshot Notification",
  "source": "aws.ec2",
  "account": "012345678901",
  "time": "yyyy-mm-ddThh:mm:ssZ",
  "region": "us-east-1",
  "resources": [
     "arn:aws:ec2::us-west-2:snapshot/snap-01234567"
  ],
  "detail": {
    "event": "createSnapshot",
    "result": "succeeded",
    "cause": "",
    "request-id": "",
    "snapshot_id": "arn:aws:ec2::us-west-2:snapshot/snap-01234567",
    "source": "arn:aws:ec2::us-west-2:volume/vol-01234567",
    "StartTime": "yyyy-mm-ddThh:mm:ssZ",
    "EndTime": "yyyy-mm-ddThh:mm:ssZ"  }
}
Copy Snapshot (copySnapshot)

The copySnapshot event is sent to your AWS account when an action to copy a snapshot completes. This event can have a result of either succeeded or failed.

Event Data

The listing below is an example of a JSON object emitted by EBS after a failed copySnapshot event. The cause for the failure was an invalid source snapshot ID. The value of snapshot_id is the ARN of the failed snapshot. The value of source is the ARN of the source snapshot. StartTime and EndTime represent when the copy-snapshot action started and ended.

Copy
{
  "version": "0",
  "id": "01234567-0123-0123-0123-012345678901",
  "detail-type": "EBS Snapshot Notification",
  "source": "aws.ec2",
  "account": "123456789012",
  "time": "yyyy-mm-ddThh:mm:ssZ",
  "region": "us-east-1",
  "resources": [
    "arn:aws:ec2::us-west-2:snapshot/snap-01234567"
  ],
  "detail": {
    "event": "copySnapshot",
    "result": "failed",
    "cause": "Source snapshot ID is not valid",
    "request-id": "",
    "snapshot_id": "arn:aws:ec2::us-west-2:snapshot/snap-01234567",
    "source": "arn:aws:ec2::eu-west-1:snapshot/snap-76543210",
    "StartTime": "yyyy-mm-ddThh:mm:ssZ",
    "EndTime": "yyyy-mm-ddThh:mm:ssZ"
  }
}
Share Snapshot (shareSnapshot)

The shareSnapshot event is sent to your AWS account when another account shares a snapshot with it. The result is always succeeded.

Event Data

The listing below is an example of a JSON object emitted by EBS after a completed shareSnapshot event. The value of source is the AWS account number of the user that shared the snapshot with you. StartTime and EndTime represent when the share-snapshot action started and ended. The shareSnapshot event is emitted only when a private snapshot is shared with another user. Sharing a public snapshot does not trigger the event.

Copy
{
  "version": "0",
  "id": "01234567-01234-0123-0123-012345678901",
  "detail-type": "EBS Snapshot Notification",
  "source": "aws.ec2",
  "account": "012345678901",
  "time": "yyyy-mm-ddThh:mm:ssZ",
  "region": "us-east-1",
  "resources": [
    "arn:aws:ec2::us-west-2:snapshot/snap-01234567"
  ],
  "detail": {
    "event": "shareSnapshot",
    "result": "succeeded",
    "cause": "",
    "request-id": "",
    "snapshot_id": "arn:aws:ec2::us-west-2:snapshot/snap-01234567",
    "source": 012345678901,
    "StartTime": "yyyy-mm-ddThh:mm:ssZ",
    "EndTime": ""yyyy-mm-ddThh:mm:ssZ""
  }
}
Invalid Encryption Key on Volume Attach or Reattach (attachVolume, reattachVolume)

The attachVolume event is sent to your AWS account when it fails to attach or reattach a volume to an instance due to an invalid KMS key.

Note
You can use a KMS key to encrypt an EBS volume. If the key used to encrypt the volume becomes invalid, EBS will emit an event if that key is later used to create, attach, or reattach to a volume.
Event Data

The listing below is an example of a JSON object emitted by EBS after a failed attachVolume event. The cause for the failure was a KMS key pending deletion.

Note
AWS may attempt to reattach to a volume following routine server maintenance.
Copy
{
  "version": "0",    
  "id": "01234567-0123-0123-0123-0123456789ab",
  "detail-type": "EBS Volume Notification",
  "source": "aws.ec2",
  "account": "012345678901",
  "time": "yyyy-mm-ddThh:mm:ssZ",
  "region": "us-east-1",
  "resources": [
  "arn:aws:ec2:us-east-1:0123456789ab:volume/vol-01234567",
  "arn:aws:kms:us-east-1:0123456789ab:key/01234567-0123-0123-0123-0123456789ab"
  ],
  "detail": {
    "event": "attachVolume",
    "result": "failed",
    "cause": "arn:aws:kms:us-east-1:0123456789ab:key/01234567-0123-0123-0123-0123456789ab is pending deletion.",
    "request-id": ""
  }
}
The listing below is an example of a JSON object emitted by EBS after a failed reattachVolume event. The cause for the failure was a KMS key pending deletion.

Copy
{
  "version": "0",    
  "id": "01234567-0123-0123-0123-0123456789ab",
  "detail-type": "EBS Volume Notification",
  "source": "aws.ec2",
  "account": "012345678901",
  "time": "yyyy-mm-ddThh:mm:ssZ",
  "region": "us-east-1",
  "resources": [
  "arn:aws:ec2:us-east-1:0123456789ab:volume/vol-01234567",
  "arn:aws:kms:us-east-1:0123456789ab:key/01234567-0123-0123-0123-0123456789ab"
  ],
  "detail": {
    "event": "reattachVolume",
    "result": "failed",
    "cause": "arn:aws:kms:us-east-1:0123456789ab:key/01234567-0123-0123-0123-0123456789ab is pending deletion.",
    "request-id": ""
  }
}
Invalid Encryption Key on Create Volume (createVolume)

The createVolume event is sent to your AWS account when it fails to create a volume due to an invalid KMS key.

You can use a KMS key to encrypt an EBS volume. If the key used to encrypt the volume becomes invalid, EBS will emit an event if that key is later used to create, attach, or reattach to a volume.

Event Data

The listing below is an example of a JSON object emitted by EBS after a failed createVolume event. The cause for the failure was a disabled KMS key.

Copy
{
  "version": "0",
  "id": "01234567-0123-0123-0123-0123456789ab",
  "detail-type": "EBS Volume Notification",
  "source": "aws.ec2",
  "account": "012345678901",
  "time": "yyyy-mm-ddThh:mm:ssZ",
  "region": "sa-east-1",
  "resources": [
    "arn:aws:ec2:sa-east-1:0123456789ab:volume/vol-01234567",
  ],
  "detail": {
    "event": "createVolume",
    "result": "failed",
    "cause": "arn:aws:kms:sa-east-1:0123456789ab:key/01234567-0123-0123-0123-0123456789ab is disabled.",
    "request-id": "01234567-0123-0123-0123-0123456789ab",
  }
}
The following is an example of a JSON object that is emitted by EBS after a failed createVolume event. The cause for the failure was a KMS key pending import.

Copy
{  
  "version": "0",  
  "id": "01234567-0123-0123-0123-0123456789ab",  
  "detail-type": "EBS Volume Notification",  
  "source": "aws.ec2",  
  "account": "012345678901",  
  "time": "yyyy-mm-ddThh:mm:ssZ",  
  "region": "sa-east-1",  
  "resources": [    
    "arn:aws:ec2:sa-east-1:0123456789ab:volume/vol-01234567",  
  ],  
  "detail": {    
    "event": "createVolume",    
    "result": "failed",    
    "cause": "arn:aws:kms:sa-east-1:0123456789ab:key/01234567-0123-0123-0123-0123456789ab is pending import.",    
    "request-id": "01234567-0123-0123-0123-0123456789ab",  
  }
}
Using Amazon Lambda To Handle CloudWatch Events

You can use Amazon EBS and CloudWatch Events to automate your data-backup workflow. This requires you to create an IAM policy, a AWS Lambda function to handle the event, and an Amazon CloudWatch Events rule that matches incoming events and routes them to the Lambda function.

The following procedure uses the createSnapshot event to automatically copy a completed snapshot to another region for disaster recovery.

To copy a completed snapshot to another region

Create an IAM policy, such as the one shown in the following example, to provide permissions to execute a CopySnapshot action and write to the CloudWatch Events log. Assign the policy to the IAM user that will handle the CloudWatch event.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:*:*:*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:CopySnapshot"
      ],
      "Resource": "*"
    }
  ]
}
Define a function in Lambda that will be available from the CloudWatch console. The sample Lambda function below, written in Node.js, is invoked by CloudWatch when a matching createSnapshot event is emitted by Amazon EBS (signifying that a snapshot was completed). When invoked, the function copies the snapshot from us-east-2 to us-east-1.

Copy
// Sample Lambda function to copy an EBS snapshot to a different region
 
var AWS = require('aws-sdk');
var ec2 = new AWS.EC2();
 
// define variables
var destinationRegion = 'us-east-1';
var sourceRegion = 'us-east-2';
console.log ('Loading function');
 
//main function
exports.handler = (event, context, callback) => {
 
    // Get the EBS snapshot ID from the CloudWatch event details
    var snapshotArn = event.detail.snapshot_id.split('/');
    const snapshotId = snapshotArn[1];
    const description = `Snapshot copy from ${snapshotId} in ${sourceRegion}.`;
    console.log ("snapshotId:", snapshotId);

    // Load EC2 class and update the configuration to use destination region to initiate the snapshot.
    AWS.config.update({region: destinationRegion});
    var ec2 = new AWS.EC2();

    // Prepare variables for ec2.modifySnapshotAttribute call
    const copySnapshotParams = {
        Description: description,
        DestinationRegion: destinationRegion,
        SourceRegion: sourceRegion,
        SourceSnapshotId: snapshotId
    };
 
    // Execute the copy snapshot and log any errors
    ec2.copySnapshot(copySnapshotParams, (err, data) => {
        if (err) {
            const errorMessage = `Error copying snapshot ${snapshotId} to region ${destinationRegion}.`;
            console.log(errorMessage);
            console.log(err);
            callback(errorMessage);
        } else {
            const successMessage = `Successfully started copy of snapshot ${snapshotId} to region ${destinationRegion}.`;
            console.log(successMessage);
            console.log(data);
            callback(null, successMessage);
        }
    });
};                
To ensure that your Lambda function is available from the CloudWatch console, create it in the region where the CloudWatch event will occur. For more information, see the AWS Lambda Developer Guide.

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

Choose Events, Create rule, Select event source, and Amazon EBS Snapshots.

For Specific Event(s), choose createSnapshot and for Specific Result(s), choose succeeded.

For Rule target, find and choose the sample function that you previously created.

Choose Target, Add Target.

For Lambda function, select the Lambda function that you previously created and choose Configure details.

On the Configure rule details page, type values for Name and Description. Select the State check box to activate the function (setting it to Enabled).

Choose Create rule.

Your rule should now appear on the Rules tab. In the example shown, the event that you configured should be emitted by EBS the next time you copy a snapshot.

Amazon EC2 Instance Store

An instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

An instance store consists of one or more instance store volumes exposed as block devices. The size of an instance store as well as the number of devices available varies by instance type. While an instance store is dedicated to a particular instance, the disk subsystem is shared among instances on a host computer.

The virtual devices for instance store volumes are ephemeral[0-23]. Instance types that support one instance store volume have ephemeral0. Instance types that support two instance store volumes have ephemeral0 and ephemeral1, and so on.

The virtual devices for NVMe instance store volumes are /dev/nvme[0-7]n1. Instance types that support one NVMe instance store volume have /dev/nvme0n1. Instance types that support two NVMe instance store volume have /dev/nvme0n1 and /dev/nvme1n1, and so on.


      Amazon EC2 instance storage
    
Contents

Instance Store Lifetime
Instance Store Volumes
Add Instance Store Volumes to Your EC2 Instance
SSD Instance Store Volumes
Instance Store Swap Volumes
Optimizing Disk Performance for Instance Store Volumes
Instance Store Lifetime

You can specify instance store volumes for an instance only when you launch it. You can't detach an instance store volume from one instance and attach it to a different instance.

The data in an instance store persists only during the lifetime of its associated instance. If an instance reboots (intentionally or unintentionally), data in the instance store persists. However, data in the instance store is lost under the following circumstances:

The underlying disk drive fails
The instance stops
The instance terminates
Therefore, do not rely on instance store for valuable, long-term data. Instead, use more durable data storage, such as Amazon S3, Amazon EBS, or Amazon EFS.

When you stop or terminate an instance, every block of storage in the instance store is reset. Therefore, your data cannot be accessed through the instance store of another instance.

If you create an AMI from an instance, the data on its instance store volumes isn't preserved and isn't present on the instance store volumes of the instances that you launch from the AMI.

Instance Store Volumes

The instance type determines the size of the instance store available and the type of hardware used for the instance store volumes. Instance store volumes are included as part of the instance's hourly cost. You must specify the instance store volumes that you'd like to use when you launch the instance (except for NVMe instance store volumes, which are available by default), and then format and mount them before using them. You can't make an instance store volume available after you launch the instance. For more information, see Add Instance Store Volumes to Your EC2 Instance.

Some instance types use NVMe or SATA based solid state drives (SSD) to deliver very high random I/O performance. This is a good option when you need storage with very low latency, but you don't need the data to persist when the instance terminates or you can take advantage of fault-tolerant architectures. For more information, see SSD Instance Store Volumes.

The following table provides the quantity, size, type, and performance optimizations of instance store volumes available on each supported instance type. For a complete list of instance types, including EBS-only types, see Amazon EC2 Instance Types.

Instance Type	Instance Store Volumes	Type	Needs Initialization*	TRIM Support**
c1.medium
1 x 350 GB†
HDD	✔	
c1.xlarge
4 x 420 GB (1,680 GB)
HDD	✔	
c3.large
2 x 16 GB (32 GB)
SSD	✔	
c3.xlarge
2 x 40 GB (80 GB)
SSD	✔	
c3.2xlarge
2 x 80 GB (160 GB)
SSD	✔	
c3.4xlarge
2 x 160 GB (320 GB)
SSD	✔	
c3.8xlarge
2 x 320 GB (640 GB)
SSD	✔	
cc2.8xlarge
4 x 840 GB (3,360 GB)
HDD	✔	
cg1.4xlarge
2 x 840 GB (1,680 GB)
HDD	✔	
cr1.8xlarge
2 x 120 GB (240 GB)
SSD	✔	
d2.xlarge
3 x 2,000 GB (6 TB)
HDD		
d2.2xlarge
6 x 2,000 GB (12 TB)
HDD		
d2.4xlarge
12 x 2,000 GB (24 TB)
HDD		
d2.8xlarge
24 x 2,000 GB (48 TB)
HDD		
f1.2xlarge
1 x 470 GB
NVMe SSD		✔
f1.16xlarge
4 x 940 GB
NVMe SSD		✔
g2.2xlarge	1 x 60 GB	SSD	✔	
g2.8xlarge	2 x 120 GB (240 GB)	SSD	✔	
hi1.4xlarge
2 x 1,024 GB (2,048 GB)
SSD		
hs1.8xlarge
24 x 2,000 GB (48 TB)
HDD	✔	
i2.xlarge
1 x 800 GB
SSD		✔
i2.2xlarge
2 x 800 GB (1,600 GB)
SSD		✔
i2.4xlarge
4 x 800 GB (3,200 GB)
SSD		✔
i2.8xlarge
8 x 800 GB (6,400 GB)
SSD		✔
i3.large
1 x 475 GB
NVMe SSD		✔
i3.xlarge
1 x 950 GB
NVMe SSD		✔
i3.2xlarge
1 x 1,900 GB
NVMe SSD		✔
i3.4xlarge
2 x 1,900 GB (3.8 TB)
NVMe SSD		✔
i3.8xlarge
4 x 1,900 GB (7.6 TB)
NVMe SSD		✔
i3.16xlarge
8 x 1,900 GB (15.2 TB)
NVMe SSD		✔
m1.small
1 x 160 GB†
HDD	✔	
m1.medium
1 x 410 GB
HDD	✔	
m1.large
2 x 420 GB (840 GB)
HDD	✔	
m1.xlarge
4 x 420 GB (1,680 GB)
HDD	✔	
m2.xlarge
1 x 420 GB
HDD	✔	
m2.2xlarge
1 x 850 GB
HDD	✔	
m2.4xlarge
2 x 840 GB (1,680 GB)
HDD	✔	
m3.medium
1 x 4 GB
SSD	✔	
m3.large
1 x 32 GB
SSD	✔	
m3.xlarge
2 x 40 GB (80 GB)
SSD	✔	
m3.2xlarge
2 x 80 GB (160 GB)
SSD	✔	
r3.large
1 x 32 GB
SSD		✔
r3.xlarge
1 x 80 GB
SSD		✔
r3.2xlarge
1 x 160 GB
SSD		✔
r3.4xlarge
1 x 320 GB
SSD		✔
r3.8xlarge
2 x 320 GB (640 GB)
SSD		✔
x1.16xlarge
1 x 1,920 GB
SSD		
x1.32xlarge
2 x 1,920 GB (3,840 GB)
SSD		
* Volumes attached to certain instances will suffer a first-write penalty unless initialized. For more information, see Optimizing Disk Performance for Instance Store Volumes.

** For more information, see Instance Store Volume TRIM Support.

† The c1.medium and m1.small instance types also include a 900 MB instance store swap volume, which may not be automatically enabled at boot time. For more information, see Instance Store Swap Volumes.

Add Instance Store Volumes to Your EC2 Instance

You specify the EBS volumes and instance store volumes for your instance using a block device mapping. Each entry in a block device mapping includes a device name and the volume that it maps to. The default block device mapping is specified by the AMI you use. Alternatively, you can specify a block device mapping for the instance when you launch it. Note that all of the NVMe instance store volumes supported by an instance type are automatically added on instance launch; you do not need to add them to the block device mapping for the AMI or the instance. For more information, see Block Device Mapping.

A block device mapping always specifies the root volume for the instance. The root volume is either an Amazon EBS volume or an instance store volume. For more information, see Storage for the Root Device. The root volume is mounted automatically. For instances with an instance store volume for the root volume, the size of this volume varies by AMI, but the maximum size is 10 GB.

You can use a block device mapping to specify additional EBS volumes when you launch your instance, or you can attach additional EBS volumes after your instance is running. For more information, see Amazon EBS Volumes.

You can specify the instance store volumes for your instance only when you launch an instance. You can't attach instance store volumes to an instance after you've launched it.

The number and size of available instance store volumes for your instance varies by instance type. Some instance types do not support instance store volumes. For more information about the instance store volumes support by each instance type, see Instance Store Volumes. If the instance type you choose for your instance supports instance store volumes, you must add them to the block device mapping for the instance when you launch it. After you launch the instance, you must ensure that the instance store volumes for your instance are formatted and mounted before you can use them. Note that the root volume of an instance store-backed instance is mounted automatically.

Contents

Adding Instance Store Volumes to an AMI
Adding Instance Store Volumes to an Instance
Making Instance Store Volumes Available on Your Instance
Adding Instance Store Volumes to an AMI

You can create an AMI with a block device mapping that includes instance store volumes. After you add instance store volumes to an AMI, any instance that you launch from the AMI includes these instance store volumes. Note that when you launch an instance, you can omit volumes specified in the AMI block device mapping and add new volumes.

Important
For M3 instances, specify instance store volumes in the block device mapping of the instance, not the AMI. Amazon EC2 might ignore instance store volumes that are specified only in the block device mapping of the AMI.
To add instance store volumes to an Amazon EBS-backed AMI using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances and select the instance.

Choose Actions, Image, Create Image.

In the Create Image dialog, add a meaningful name and description for your image.

For each instance store volume to add, choose Add New Volume, select an instance store volume from Type, and select a device name from Device. (For more information, see Device Naming on Linux Instances.) The number of available instance store volumes depends on the instance type. Note that for instances with NVMe instance store volumes, the device mapping of these volumes depends on the order in which the operating system enumerates the volumes.


              Add instance store volumes when launching an instance
            
Choose Create Image.

To add instance store volumes to an AMI using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-image or register-image (AWS CLI)
New-EC2Image and Register-EC2Image (AWS Tools for Windows PowerShell)
Adding Instance Store Volumes to an Instance

When you launch an instance, the default block device mapping is provided by the specified AMI. If you need additional instance store volumes, you must add them to the instance as you launch it. Note that you can also omit devices specified in the AMI block device mapping.

Important
For M3 instances, you might receive instance store volumes even if you do not specify them in the block device mapping for the instance.
Important
For HS1 instances, no matter how many instance store volumes you specify in the block device mapping of an AMI, the block device mapping for an instance launched from the AMI automatically includes the maximum number of supported instance store volumes. You must explicitly remove the instance store volumes that you don't want from the block device mapping for the instance before you launch it.
To update the block device mapping for an instance using the console

Open the Amazon EC2 console.

From the dashboard, choose Launch Instance.

In Step 1: Choose an Amazon Machine Image (AMI), select the AMI to use and choose Select.

Follow the wizard to complete Step 1: Choose an Amazon Machine Image (AMI), Step 2: Choose an Instance Type, and Step 3: Configure Instance Details.

In Step 4: Add Storage, modify the existing entries as needed. For each instance store volume to add, click Add New Volume, select an instance store volume from Type, and select a device name from Device. The number of available instance store volumes depends on the instance type.


              Add instance store volumes when launching an instance
            
Complete the wizard to launch the instance.

To update the block device mapping for an instance using the command line

You can use one of the following options commands with the corresponding command. For more information about these command line interfaces, see Accessing Amazon EC2.

--block-device-mappings with run-instances (AWS CLI)
-BlockDeviceMapping with New-EC2Instance (AWS Tools for Windows PowerShell)
Making Instance Store Volumes Available on Your Instance

After you launch an instance, the instance store volumes are available to the instance, but you can't access them until they are mounted. For Linux instances, the instance type determines which instance store volumes are mounted for you and which are available for you to mount yourself. For Windows instances, the EC2Config service mounts the instance store volumes for an instance. The block device driver for the instance assigns the actual volume name when mounting the volume, and the name assigned can be different than the name that Amazon EC2 recommends.

Many instance store volumes are pre-formatted with the ext3 file system. SSD-based instance store volumes that support TRIM instruction are not pre-formatted with any file system. However, you can format volumes with the file system of your choice after you launch your instance. For more information, see Instance Store Volume TRIM Support. For Windows instances, the EC2Config service reformats the instance store volumes with the NTFS file system.

You can confirm that the instance store devices are available from within the instance itself using instance metadata. For more information, see Viewing the Instance Block Device Mapping for Instance Store Volumes.

For Windows instances, you can also view the instance store volumes using Windows Disk Management. For more information, see Listing the Disks Using Windows Disk Management.

For Linux instances, you can view and mount the instance store volumes as described in the following procedure.

To make an instance store volume available on Linux

Connect to the instance using an SSH client.

Use the df -h command to view the volumes that are formatted and mounted. Use the lsblk to view any volumes that were mapped at launch but not formatted and mounted.

To format and mount an instance store volume that was mapped only, do the following:

Create a file system on the device using the mkfs command.

Create a directory on which to mount the device using the mkdir command.

Mount the device on the newly created directory using the mount command.

SSD Instance Store Volumes

The following instances support instance store volumes that use solid state drives (SSD) to deliver very high random I/O performance: C3, F1, G2, HI1, I2, I3, M3, R3, and X1. For more information about the instance store volumes support by each instance type, see Instance Store Volumes.

To ensure the best IOPS performance from your SSD instance store volumes on Linux, we recommend that you use the most recent version of the Amazon Linux AMI, or another Linux AMI with a kernel version of 3.8 or later. If you do not use a Linux AMI with a kernel version of 3.8 or later, your instance will not achieve the maximum IOPS performance available for these instance types.

Like other instance store volumes, you must map the SSD instance store volumes for your instance when you launch it, and the data on an SSD instance volume persists only for the life of its associated instance. For more information, see Add Instance Store Volumes to Your EC2 Instance.

NVMe SSD Volumes

I3 and F1 instances offer non-volatile memory express (NVMe) SSD instance store volumes. To access the NVMe volumes, you must use an operating system that supports NVMe. The following are the recommended operating systems:

The current Amazon Linux AMI
Ubuntu version 16.10 provided by AWS. If you are using a different version, we recommend that you turn off memory hot add.
Windows Server 2016, Windows Server 2012 R2, or Windows Server 2008 R2. Note that Windows Server 2012 and Windows Server 2008 are not supported.
Red Hat Enterprise 7, CentOS 7, and SUSE Linux Enterprise Server 12 are not recommended at this time due to pending kernel updates.

After you connect to your instance, you can list the NVMe devices using the lspci command. The following is example output for an i3.8xlarge instance, which supports 4 NVMe devices.

Copy
[ec2-user ~]$ lspci
00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02)
00:01.0 ISA bridge: Intel Corporation 82371SB PIIX3 ISA [Natoma/Triton II]
00:01.1 IDE interface: Intel Corporation 82371SB PIIX3 IDE [Natoma/Triton II]
00:01.3 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 01)
00:02.0 VGA compatible controller: Cirrus Logic GD 5446
00:03.0 Ethernet controller: Device 1d0f:ec20
00:17.0 Non-Volatile memory controller: Device 1d0f:cd01
00:18.0 Non-Volatile memory controller: Device 1d0f:cd01
00:19.0 Non-Volatile memory controller: Device 1d0f:cd01
00:1a.0 Non-Volatile memory controller: Device 1d0f:cd01
00:1f.0 Unassigned class [ff80]: XenSource, Inc. Xen Platform Device (rev 01)
If you are using a supported operating system but you do not see the NVMe devices, verify that the NVMe module is loaded using the following lsmod command.

Copy
[ec2-user ~]$ lsmod | grep nvme
nvme          48813  0
The NVMe volumes are compliant with the NVMe 1.0a specification. You can use the NVMe commands with your NVMe volumes. With the Amazon Linux AMI, you can install the nvme-cli package from the repo using the yum install command. With other supported versions of Linux, you can download the nvme-cli package if it's not available in the image.

Instance Store Volume TRIM Support

The following instances support SSD volumes with TRIM: F1, I2, I3, and R3.

Instance store volumes that support TRIM are fully trimmed before they are allocated to your instance. These volumes are not formatted with a file system when an instance launches, so you must format them before they can be mounted and used. For faster access to these volumes, you should skip the TRIM operation when you format them.

With instance store volumes that support TRIM, you can use the TRIM command to notify the SSD controller when you no longer need data that you've written. This provides the controller with more free space, which can reduce write amplification and increase performance. On Linux, you can use the fstrim command to enable periodic TRIM. On Windows, you can use the fsutil behavior set DisableDeleteNotify 1 command. For more information, see the documentation for your operating system.

HI1 SSD Storage

With SSD storage on HI1 instances:

The primary data source is an instance store with SSD storage.
Read performance is consistent and write performance can vary.
Write amplification can occur.
The TRIM command is not currently supported.
Instance Store with SSD Storage

The hi1.4xlarge instances use an Amazon EBS-backed root device. However, their primary data storage is provided by the SSD volumes in the instance store. Like other instance store volumes, these instance store volumes persist only for the life of the instance. Because the root device of the hi1.4xlarge instance is Amazon EBS-backed, you can still start and stop your instance. When you stop an instance, your application persists, but your production data in the instance store does not persist. For more information about instance store volumes, see Amazon EC2 Instance Store.

Variable Write Performance

Write performance depends on how your applications utilize logical block addressing (LBA) space. If your applications use the total LBA space, write performance can degrade by about 90 percent. Benchmark your applications and monitor the queue length (the number of pending I/O requests for a volume) and I/O size.

Write Amplification

Write amplification refers to an undesirable condition associated with flash memory and SSDs, where the actual amount of physical information written is a multiple of the logical amount intended to be written. Because flash memory must be erased before it can be rewritten, the process to perform these operations results in moving (or rewriting) user data and metadata more than once. This multiplying effect increases the number of writes required over the life of the SSD, which shortens the time that it can reliably operate. The hi1.4xlarge instances are designed with a provisioning model intended to minimize write amplification.

Random writes have a much more severe impact on write amplification than serial writes. If you are concerned about write amplification, allocate less than the full tebibyte of storage for your application (also known as over provisioning).

The TRIM Command

The TRIM command enables the operating system to notify an SSD that blocks of previously saved data are considered no longer in use. TRIM limits the impact of write amplification.

TRIM support is not available for HI1 instances.

Instance Store Swap Volumes

Swap space in Linux can be used when a system requires more memory than it has been physically allocated. When swap space is enabled, Linux systems can swap infrequently used memory pages from physical memory to swap space (either a dedicated partition or a swap file in an existing file system) and free up that space for memory pages that require high speed access.

Note
Using swap space for memory paging is not as fast or efficient as using RAM. If your workload is regularly paging memory into swap space, you should consider migrating to a larger instance type with more RAM. For more information, see Resizing Your Instance.
The c1.medium and m1.small instance types have a limited amount of physical memory to work with, and they are given a 900 MiB swap volume at launch time to act as virtual memory for Linux AMIs. Although the Linux kernel sees this swap space as a partition on the root device, it is actually a separate instance store volume, regardless of your root device type.

Amazon Linux AMIs automatically enable and use this swap space, but your AMI may require some additional steps to recognize and use this swap space. To see if your instance is using swap space, you can use the swapon -s command.

Copy
[ec2-user ~]$ swapon -s
Filename                                Type            Size    Used    Priority
/dev/xvda3                              partition       917500  0       -1
The above instance has a 900 MiB swap volume attached and enabled. If you don't see a swap volume listed with this command, you may need to enable swap space for the device. Check your available disks using the lsblk command.

Copy
[ec2-user ~]$ lsblk
NAME  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda1 202:1    0    8G  0 disk /
xvda3 202:3    0  896M  0 disk
Here, the swap volume xvda3 is available to the instance, but it is not enabled (notice that the MOUNTPOINT field is empty). You can enable the swap volume with the swapon command.

Note
You need to prepend /dev/ to the device name listed by lsblk. Your device may be named differently, such as sda3, sde3, or xvde3. Use the device name for your system in the command below.
Copy
[ec2-user ~]$ sudo swapon /dev/xvda3
Now the swap space should show up in lsblk and swapon -s output.

Copy
[ec2-user ~]$ lsblk
NAME  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda1 202:1    0    8G  0 disk /
xvda3 202:3    0  896M  0 disk [SWAP]
[ec2-user ~]$ swapon -s
Filename                                Type            Size    Used    Priority
/dev/xvda3                              partition       917500  0       -1
You will also need to edit your /etc/fstab file so that this swap space is automatically enabled at every system boot.

Copy
[ec2-user ~]$ sudo vim /etc/fstab
Append the following line to your /etc/fstab file (using the swap device name for your system):

/dev/xvda3       none    swap    sw  0       0
To use an instance store volume as swap space

Any instance store volume can be used as swap space. For example, the m3.medium instance type includes a 4 GB SSD instance store volume that is appropriate for swap space. If your instance store volume is much larger (for example, 350 GB), you may consider partitioning the volume with a smaller swap partition of 4-8 GB and the rest for a data volume.

Note
This procedure applies only to instance types that support instance storage. For a list of supported instance types, see Instance Store Volumes.
List the block devices attached to your instance to get the device name for your instance store volume.

Copy
[ec2-user ~]$ lsblk -p
NAME       MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
/dev/xvdb  202:16   0   4G  0 disk /media/ephemeral0
/dev/xvda1 202:1    0   8G  0 disk /
In this example, the instance store volume is /dev/xdvb. Because this is an Amazon Linux instance, the instance store volume is formatted and mounted at /media/ephemeral0; not all Linux operating systems do this automatically.

(Optional) If your instance store volume is mounted (it will list a MOUNTPOINT in the lsblk command output), you need to unmount it with the following command.

Copy
[ec2-user ~]$ sudo umount /dev/xvdb
Set up a Linux swap area on the device with the mkswap command.

Copy
[ec2-user ~]$ sudo mkswap /dev/xvdb
mkswap: /dev/xvdb: warning: wiping old ext3 signature.
Setting up swapspace version 1, size = 4188668 KiB
no label, UUID=b4f63d28-67ed-46f0-b5e5-6928319e620b
Enable the new swap space.

Copy
[ec2-user ~]$ sudo swapon /dev/xvdb
Verify that the new swap space is being used.

Copy
[ec2-user ~]$ swapon -s
Filename				Type		Size	Used	Priority
/dev/xvdb                              	partition	4188668	0	-1
Edit your /etc/fstab file so that this swap space is automatically enabled at every system boot.

Copy
[ec2-user ~]$ sudo vim /etc/fstab
If your /etc/fstab file has an entry for /dev/xvdb (or /dev/sdb) change it to match the line below; if it does not have an entry for this device, append the following line to your /etc/fstab file (using the swap device name for your system):

/dev/xvdb       none    swap    sw  0       0
Important
Instance store volume data is lost when an instance is stopped; this includes the instance store swap space formatting created in Step 3. If you stop and restart an instance that has been configured to use instance store swap space, you must repeat Step 1 through Step 5 on the new instance store volume.

Optimizing Disk Performance for Instance Store Volumes

Because of the way that Amazon EC2 virtualizes disks, the first write to any location on most instance store volumes performs more slowly than subsequent writes. For most applications, amortizing this cost over the lifetime of the instance is acceptable. However, if you require high disk performance, we recommend that you initialize your drives by writing once to every drive location before production use.

Note
Some instance types with direct-attached solid state drives (SSD) and TRIM support provide maximum performance at launch time, without initialization. For information about the instance store for each instance type, see Instance Store Volumes.
If you require greater flexibility in latency or throughput, we recommend using Amazon EBS.

To initialize the instance store volumes, use the following dd commands, depending on which store you want to initialize (for example, /dev/sdb or /dev/name[0-7]n1).

Note
Make sure to unmount the drive before performing this command.
Initialization can take a long time (about 8 hours for an extra large instance).
To initialize the instance store volumes, use the following commands on the m1.large, m1.xlarge, c1.xlarge, m2.xlarge, m2.2xlarge, and m2.4xlarge instance types:

Copy
dd if=/dev/zero of=/dev/sdb bs=1M          
dd if=/dev/zero of=/dev/sdc bs=1M          
dd if=/dev/zero of=/dev/sdd bs=1M          
dd if=/dev/zero of=/dev/sde bs=1M
To perform initialization on all instance store volumes at the same time, use the following command:

Copy
dd if=/dev/zero bs=1M|tee /dev/sdb|tee /dev/sdc|tee /dev/sde > /dev/sdd
Configuring drives for RAID initializes them by writing to every drive location. When configuring software-based RAID, make sure to change the minimum reconstruction speed:

Copy
echo $((30*1024)) > /proc/sys/dev/raid/speed_limit_min

Amazon Elastic File System (Amazon EFS)

Amazon EFS provides scalable file storage for use with Amazon EC2. You can create an EFS file system and configure your instances to mount the file system. You can use an EFS file system as a common data source for workloads and applications running on multiple instances. For more information, see the Amazon Elastic File System product page.

In this tutorial, you create an EFS file system and two Linux instances that can share data using the file system.

Important
Amazon EFS is not supported on Windows instances.
Tasks

Prerequisites
Step 1: Create an EFS File System
Step 2: Mount the File System
Step 3: Test the File System
Step 4: Clean Up
Prerequisites

Create a security group (for example, efs-sg) and add the following rules:
Allow inbound SSH connections from your computer (the source is the CIDR block for your network)
Allow inbound NFS connections from EC2 instances associated with the group (the source is the security group itself)
Create a key pair. You must specify a key pair when you configure your instances or you can't connect to them. For more information, see Create a Key Pair.
Step 1: Create an EFS File System

Amazon EFS enables you to create a file system that multiple instances can mount and access at the same time. For more information, see Creating Resources for Amazon EFS in the Amazon Elastic File System User Guide.

To create a file system

Open the Amazon Elastic File System console at https://console.aws.amazon.com/efs/.

Choose Create file system.

On the Configure file system access page, do the following:

For VPC, select the VPC to use for your instances.

For Create mount targets, select all the Availability Zones.

For each Availability Zone, ensure that the value for Security group is the security group that you created in Prerequisites.

Choose Next Step.

On the Configure optional settings page, do the following:

For the tag with Key=Name, type a name for the file system in Value.

For Choose performance mode, keep the default option, General Purpose.

Choose Next Step.

On the Review and create page, choose Create File System.

After the file system is created, note the file system ID, as you'll use it later in this tutorial.

Step 2: Mount the File System

Use the following procedure to launch two t2.micro instances. The user data script mounts the file system to both instances during launch and updates /etc/fstab to ensure that the file system is remounted after an instance reboot. Note that T2 instances must be launched in a subnet. You can use a default VPC or a nondefault VPC.

Note
There are other ways that you can mount the volume (for example, on an already running instance). For more information, see Mounting File Systems in the Amazon Elastic File System User Guide.
To launch two instances and mount an EFS file system

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Launch Instance.

On the Choose an Amazon Machine Image page, select an Amazon Linux AMI with the HVM virtualization type.

On the Choose an Instance Type page, keep the default instance type, t2.micro and choose Next: Configure Instance Details.

On the Configure Instance Details page, do the following:

For Number of instances, type 2.

[Default VPC] If you have a default VPC, it is the default value for Network. Keep the default VPC and the default value for Subnet to use the default subnet in the Availability Zone that Amazon EC2 chooses for your instances.

[Nondefault VPC] Select your VPC for Network and a public subnet from Subnet.

[Nondefault VPC] For Auto-assign Public IP, choose Enable. Otherwise, your instances do not get public IP addresses or public DNS names.

Under Advanced Details, paste the following script into User data. Update EFS_ID with the ID of your file system and EFS_REGION with the region code for your file system. You can optionally update EFS_MOUNT_DIR with a directory for your mounted file system.

Copy
#!/bin/bash
yum update -y
yum install -y nfs-utils
EFS_ID=fs-xxxxxxxx
EFS_REGION=region-code
EFS_MOUNT_DIR=/mnt/efs
mkdir -p ${EFS_MOUNT_DIR}
chown ec2-user:ec2-user ${EFS_MOUNT_DIR}
echo $(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone).${EFS_ID}.efs.${EFS_REGION}.amazonaws.com:/ ${EFS_MOUNT_DIR} nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 >> /etc/fstab
mount -a
Advance to Step 6 of the wizard.

On the Configure Security Group page, choose Select an existing security group, select your security group, and then choose Review and Launch.

On the Review Instance Launch page, choose Launch.

In the Select an existing key pair or create a new key pair dialog box, select Choose an existing key pair and choose your key pair. Select the acknowledgment check box, and choose Launch Instances.

In the navigation pane, choose Instances to see the status of your instances. Initially, their status is pending. After the status changes to running, your instances are ready for use.

Step 3: Test the File System

You can connect to your instances and verify that the file system is mounted to the directory that you specified (for example, /mnt/efs).

To verify that the file system is mounted

Connect to your instances. For more information, see Connect to Your Linux Instance.

From the terminal window for each instance, run the df -T command to verify that the EFS file system is mounted.

Copy
$ df -T
Filesystem     Type              1K-blocks    Used          Available Use% Mounted on
/dev/xvda1     ext4                8123812 1949800            6073764  25% /
devtmpfs       devtmpfs            4078468      56            4078412   1% /dev
tmpfs          tmpfs               4089312       0            4089312   0% /dev/shm
efs-dns        nfs4       9007199254740992       0   9007199254740992   0% /mnt/efs
Note that the name of the file system, shown in the example output as efs-dns, has the following form:

availability-zone.filesystem-id.efs.region.amazonaws.com:/
(Optional) Create a file in the file system from one instance, and then verify that you can view the file from the other instance.

From the first instance, run the following command to create the file:

Copy
$ sudo touch /mnt/efs/test-file.txt
From the second instance, run the following command to view the file:

Copy
$ ls /mnt/efs
test-file.txt
Step 4: Clean Up

When you are finished with this tutorial, you can terminate the instances and delete the file system.

To terminate the instances

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instances to terminate.

Choose Actions, Instance State, Terminate.

Choose Yes, Terminate when prompted for confirmation.

To delete the file system

Open the Amazon Elastic File System console at https://console.aws.amazon.com/efs/.

Select the file system to delete.

Choose Actions, Delete file system.

When prompted for confirmation, type the ID of the file system and choose Delete File System.

Amazon Simple Storage Service (Amazon S3)

Amazon S3 is a repository for Internet data. Amazon S3 provides access to reliable, fast, and inexpensive data storage infrastructure. It is designed to make web-scale computing easy by enabling you to store and retrieve any amount of data, at any time, from within Amazon EC2 or anywhere on the web. Amazon S3 stores data objects redundantly on multiple devices across multiple facilities and allows concurrent read or write access to these data objects by many separate clients or application threads. You can use the redundant data stored in Amazon S3 to recover quickly and reliably from instance or application failures.

Amazon EC2 uses Amazon S3 for storing Amazon Machine Images (AMIs). You use AMIs for launching EC2 instances. In case of instance failure, you can use the stored AMI to immediately launch another instance, thereby allowing for fast recovery and business continuity.

Amazon EC2 also uses Amazon S3 to store snapshots (backup copies) of the data volumes. You can use snapshots for recovering data quickly and reliably in case of application or system failures. You can also use snapshots as a baseline to create multiple new data volumes, expand the size of an existing data volume, or move data volumes across multiple Availability Zones, thereby making your data usage highly scalable. For more information about using data volumes and snapshots, see Amazon Elastic Block Store.

Objects are the fundamental entities stored in Amazon S3. Every object stored in Amazon S3 is contained in a bucket. Buckets organize the Amazon S3 namespace at the highest level and identify the account responsible for that storage. Amazon S3 buckets are similar to Internet domain names. Objects stored in the buckets have a unique key value and are retrieved using a HTTP URL address. For example, if an object with a key value /photos/mygarden.jpg is stored in the myawsbucket bucket, then it is addressable using the URL http://myawsbucket.s3.amazonaws.com/photos/mygarden.jpg.

For more information about the features of Amazon S3, see the Amazon S3 product page.

Amazon S3 and Amazon EC2

Given the benefits of Amazon S3 for storage, you may decide to use this service to store files and data sets for use with EC2 instances. There are several ways to move data to and from Amazon S3 to your instances. In addition to the examples discussed below, there are a variety of tools that people have written that you can use to access your data in Amazon S3 from your computer or your instance. Some of the common ones are discussed in the AWS forums.

If you have permission, you can copy a file to or from Amazon S3 and your instance using one of the following methods.

GET or wget

The wget utility is an HTTP and FTP client that allows you to download public objects from Amazon S3. It is installed by default in Amazon Linux and most other distributions, and available for download on Windows. To download an Amazon S3 object, use the following command, substituting the URL of the object to download.

Copy
[ec2-user ~]$ wget https://my_bucket.s3.amazonaws.com/path-to-file
This method requires that the object you request is public; if the object is not public, you receive an "ERROR 403: Forbidden" message. If you receive this error, open the Amazon S3 console and change the permissions of the object to public. For more information, see the Amazon Simple Storage Service Developer Guide.

AWS Command Line Interface

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. The AWS CLI enables users to authenticate themselves and download restricted items from Amazon S3 and also to upload items. For more information, such as how to install and configure the tools, see the AWS Command Line Interface detail page.

The aws s3 cp command is similar to the Unix cp command. You can copy files from Amazon S3 to your instance, copy files from your instance to Amazon S3, and copy files from one Amazon S3 location to another.

Use the following command to copy an object from Amazon S3 to your instance.

Copy
[ec2-user ~]$ aws s3 cp s3://my_bucket/my_folder/my_file.ext my_copied_file.ext
Use the following command to copy an object from your instance back into Amazon S3.

Copy
[ec2-user ~]$ aws s3 cp my_copied_file.ext s3://my_bucket/my_folder/my_file.ext
The aws s3 sync command can synchronize an entire Amazon S3 bucket to a local directory location. This can be helpful for downloading a data set and keeping the local copy up-to-date with the remote set. If you have the proper permissions on the Amazon S3 bucket, you can push your local directory back up to the cloud when you are finished by reversing the source and destination locations in the command.

Use the following command to download an entire Amazon S3 bucket to a local directory on your instance.

Copy
[ec2-user ~]$ aws s3 sync s3://remote_S3_bucket local_directory
Amazon S3 API

If you are a developer, you can use an API to access data in Amazon S3. For more information, see the Amazon Simple Storage Service Developer Guide. You can use this API and its examples to help develop your application and integrate it with other APIs and SDKs, such as the boto Python interface.

Instance Volume Limits

The maximum number of volumes that your instance can have depends on the operating system. When considering how many volumes to add to your instance, you should consider whether you need increased I/O bandwidth or increased storage capacity.

Contents

Linux-Specific Volume Limits
Windows-Specific Volume Limits
Bandwidth versus Capacity
Linux-Specific Volume Limits

Attaching more than 40 volumes can cause boot failures. Note that this number includes the root volume, plus any attached instance store volumes and EBS volumes. If you experience boot problems on an instance with a large number of volumes, stop the instance, detach any volumes that are not essential to the boot process, and then reattach the volumes after the instance is running.

Important
Attaching more than 40 volumes to a Linux instance is supported on a best effort basis only and is not guaranteed.
Windows-Specific Volume Limits

The following table shows the volume limits for Windows instances based on the driver used. Note that these numbers include the root volume, plus any attached instance store volumes and EBS volumes.

Important
Attaching more than the following volumes to a Windows instance is supported on a best effort basis only and is not guaranteed.
Driver	Volume Limit
AWS PV
26
Citrix PV
26
Red Hat PV
17
We do not recommend that you give a Windows instance more than 26 volumes with AWS PV or Citrix PV drivers, as it is likely to cause performance issues.

To determine which PV drivers your instance is using, or to upgrade your Windows instance from Red Hat to Citrix PV drivers, see Upgrading PV Drivers on Your Windows Instance.

For more information about how device names related to volumes, see Mapping Disks to Volumes on Your Windows EC2 Instance in the Amazon EC2 User Guide for Windows Instances.

Bandwidth versus Capacity

For consistent and predictable bandwidth use cases, use EBS-optimized or 10 Gigabit network connectivity instances and General Purpose SSD or Provisioned IOPS SSD volumes. Follow the guidance in Amazon EC2 Instance Configuration to match the IOPS you have provisioned for your volumes to the bandwidth available from your instances for maximum performance. For RAID configurations, many administrators find that arrays larger than 8 volumes have diminished performance returns due to increased I/O overhead. Test your individual application performance and tune it as required.

Device Naming on Linux Instances

When you attach a volume to your instance, you include a device name for the volume. This device name is used by Amazon EC2. The block device driver for the instance assigns the actual volume name when mounting the volume, and the name assigned can be different from the name that Amazon EC2 uses.

Contents

Available Device Names
Device Name Considerations
For information about device names on Windows instances, see Device Naming on Windows Instances in the Amazon EC2 User Guide for Windows Instances.

Available Device Names

The following table lists the available device names for Linux instances. The number of volumes that you can attach to your instance is determined by the operating system. For more information, see Instance Volume Limits.

Virtualization Type	Available	Reserved for Root	Recommended for EBS Volumes	Used for Instance Store Volumes	Used for NVMe Instance Store Volumes
Paravirtual
/dev/sd[a-z]

/dev/sd[a-z][1-15]

/dev/hd[a-z]

/dev/hd[a-z][1-15]
/dev/sda1
/dev/sd[f-p]

/dev/sd[f-p][1-6]
/dev/sd[b-e]

/dev/sd[b-y] (hs1.8xlarge)
Not available
HVM	
/dev/sd[a-z]

/dev/xvd[b-c][a-z]
Differs by AMI

/dev/sda1 or /dev/xvda
/dev/sd[f-p]
/dev/sd[b-e]

/dev/sd[b-y] (d2.8xlarge)

/dev/sd[b-y] (hs1.8xlarge)

/dev/sd[b-i] (i2.8xlarge)
/dev/nvme[0-7]n1 *
* NVMe volumes are automatically enumerated and assigned a device name. There is no need to specify NVMe volumes in your block device mapping.

Note that you can determine the root device name for your particular AMI with the following AWS CLI command:

Copy
aws ec2 describe-images --image-ids image_id --query 'Images[].RootDeviceName'
For more information about instance store volumes, see Amazon EC2 Instance Store. For information about the root device storage, see Amazon EC2 Root Device Volume.

Device Name Considerations

Keep the following in mind when selecting a device name:

Although you can attach your EBS volumes using the device names used to attach instance store volumes, we strongly recommend that you don't because the behavior can be unpredictable.
Depending on the block device driver of the kernel, the device might be attached with a different name than what you specify. For example, if you specify a device name of /dev/sdh, your device might be renamed /dev/xvdh or /dev/hdh by the kernel; in most cases, the trailing letter remains the same. In some versions of Red Hat Enterprise Linux (and its variants, such as CentOS), even the trailing letter might also change (where /dev/sda could become /dev/xvde). In these cases, each device name trailing letter is incremented the same number of times. For example, /dev/sdb would become /dev/xvdf and /dev/sdc would become /dev/xvdg. Amazon Linux AMIs create a symbolic link with the name you specify at launch that points to the renamed device path, but other AMIs might behave differently.
The number of NVMe instance store volumes for an instance depends on the size of the instance. The device names are /dev/nvme0n1, /dev/nvme1n1, and so on.
There are two types of virtualization available for Linux instances: paravirtual (PV) and hardware virtual machine (HVM). The virtualization type of an instance is determined by the AMI used to launch the instance. Some instance types support both PV and HVM, some support HVM only, and others support PV only. Be sure to note the virtualization type of your AMI, because the recommended and available device names that you can use depend on the virtualization type of your instance. For more information, see Linux AMI Virtualization Types.
You cannot attach volumes that share the same device letters both with and without trailing digits. For example, if you attach a volume as /dev/sdc and another volume as /dev/sdc1, only /dev/sdc is visible to the instance. To use trailing digits in device names, you must use trailing digits on all device names that share the same base letters (such as /dev/sdc1, /dev/sdc2, /dev/sdc3).
Hardware virtual machine (HVM) AMIs don't support the use of trailing numbers on device names, except for the device name that's reserved for the root device.
Some custom kernels might have restrictions that limit use to /dev/sd[f-p] or /dev/sd[f-p][1-6]. If you're having trouble using /dev/sd[q-z] or /dev/sd[q-z][1-6], try switching to /dev/sd[f-p] or /dev/sd[f-p][1-6].

Block Device Mapping

Each instance that you launch has an associated root device volume, either an Amazon EBS volume or an instance store volume. You can use block device mapping to specify additional EBS volumes or instance store volumes to attach to an instance when it's launched. You can also attach additional EBS volumes to a running instance; see Attaching an Amazon EBS Volume to an Instance. However, the only way to attach instance store volumes to an instance is to use block device mapping to attach them as the instance is launched.

For more information about root device volumes, see Changing the Root Device Volume to Persist.

Contents

Block Device Mapping Concepts
AMI Block Device Mapping
Instance Block Device Mapping
Block Device Mapping Concepts

A block device is a storage device that moves data in sequences of bytes or bits (blocks). These devices support random access and generally use buffered I/O. Examples include hard disks, CD-ROM drives, and flash drives. A block device can be physically attached to a computer or accessed remotely as if it were physically attached to the computer. Amazon EC2 supports two types of block devices:

Instance store volumes (virtual devices whose underlying hardware is physically attached to the host computer for the instance)
EBS volumes (remote storage devices)
A block device mapping defines the block devices (instance store volumes and EBS volumes) to attach to an instance. You can specify a block device mapping as part of creating an AMI so that the mapping is used by all instances launched from the AMI. Alternatively, you can specify a block device mapping when you launch an instance, so this mapping overrides the one specified in the AMI from which you launched the instance. Note that all of the NVMe instance store volumes supported by an instance type are automatically added on instance launch; you do not need to add them to the block device mapping for the AMI or the instance.

Contents

Block Device Mapping Entries
Block Device Mapping Instance Store Caveats
Example Block Device Mapping
How Devices Are Made Available in the Operating System
Block Device Mapping Entries

When you create a block device mapping, you specify the following information for each block device that you need to attach to the instance:

The device name used within Amazon EC2. The block device driver for the instance assigns the actual volume name when mounting the volume, and the name assigned can be different from the name that Amazon EC2 recommends. For more information, see Device Naming on Linux Instances.
[Instance store volumes] The virtual device: ephemeral[0-23]. Note that the number and size of available instance store volumes for your instance varies by instance type.
[NVMe instance store volumes] These volumes are mapped automatically as /dev/nvme[0-7]n1. You do not need to specify the NVMe volumes supported by an instance type in a block device mapping.
[EBS volumes] The ID of the snapshot to use to create the block device (snap-xxxxxxxx). This value is optional as long as you specify a volume size.
[EBS volumes] The size of the volume, in GiB. The specified size must be greater than or equal to the size of the specified snapshot.
[EBS volumes] Whether to delete the volume on instance termination (true or false). The default value is true for the root device volume and false for attached volumes. When you create an AMI, its block device mapping inherits this setting from the instance. When you launch an instance, it inherits this setting from the AMI.
[EBS volumes] The volume type, which can be gp2 for General Purpose SSD, io1 for Provisioned IOPS SSD, st1 for Throughput Optimized HDD, sc1 for Cold HDD, or standard for Magnetic. The default value is gp2 in the Amazon EC2 console, and standard in the AWS SDKs and the AWS CLI.
[EBS volumes] The number of input/output operations per second (IOPS) that the volume supports. (Not used with gp2, st1, sc1, or standard volumes.)
Block Device Mapping Instance Store Caveats

There are several caveats to consider when launching instances with AMIs that have instance store volumes in their block device mappings.

Some instance types include more instance store volumes than others, and some instance types contain no instance store volumes at all. If your instance type supports one instance store volume, and your AMI has mappings for two instance store volumes, then the instance launches with one instance store volume.
Instance store volumes can only be mapped at launch time. You cannot stop an instance without instance store volumes (such as the t2.micro), change the instance to a type that supports instance store volumes, and then restart the instance with instance store volumes. However, you can create an AMI from the instance and launch it on an instance type that supports instance store volumes, and map those instance store volumes to the instance.
If you launch an instance with instance store volumes mapped, and then stop the instance and change it to an instance type with fewer instance store volumes and restart it, the instance store volume mappings from the initial launch still show up in the instance metadata. However, only the maximum number of supported instance store volumes for that instance type are available to the instance.
Note
When an instance is stopped, all data on the instance store volumes is lost.
Depending on instance store capacity at launch time, M3 instances may ignore AMI instance store block device mappings at launch unless they are specified at launch. You should specify instance store block device mappings at launch time, even if the AMI you are launching has the instance store volumes mapped in the AMI, to ensure that the instance store volumes are available when the instance launches.
Example Block Device Mapping

This figure shows an example block device mapping for an EBS-backed instance. It maps /dev/sdb to ephemeral0 and maps two EBS volumes, one to /dev/sdh and the other to /dev/sdj. It also shows the EBS volume that is the root device volume, /dev/sda1.


          Relationship between instance, instance store volumes, and EBS volumes.
        
Note that this example block device mapping is used in the example commands and APIs in this topic. You can find example commands and APIs that create block device mappings in Specifying a Block Device Mapping for an AMI and Updating the Block Device Mapping when Launching an Instance.

How Devices Are Made Available in the Operating System

Device names like /dev/sdh and xvdh are used by Amazon EC2 to describe block devices. The block device mapping is used by Amazon EC2 to specify the block devices to attach to an EC2 instance. After a block device is attached to an instance, it must be mounted by the operating system before you can access the storage device. When a block device is detached from an instance, it is unmounted by the operating system and you can no longer access the storage device.

With a Linux instance, the device names specified in the block device mapping are mapped to their corresponding block devices when the instance first boots. The instance type determines which instance store volumes are formatted and mounted by default. You can mount additional instance store volumes at launch, as long as you don't exceed the number of instance store volumes available for your instance type. For more information, see Amazon EC2 Instance Store. The block device driver for the instance determines which devices are used when the volumes are formatted and mounted. For more information, see Attaching an Amazon EBS Volume to an Instance.

AMI Block Device Mapping

Each AMI has a block device mapping that specifies the block devices to attach to an instance when it is launched from the AMI. An AMI that Amazon provides includes a root device only. To add more block devices to an AMI, you must create your own AMI.

Contents

Specifying a Block Device Mapping for an AMI
Viewing the EBS Volumes in an AMI Block Device Mapping
Specifying a Block Device Mapping for an AMI

There are two ways to specify volumes in addition to the root volume when you create an AMI. If you've already attached volumes to a running instance before you create an AMI from the instance, the block device mapping for the AMI includes those same volumes. For EBS volumes, the existing data is saved to a new snapshot, and it's this new snapshot that's specified in the block device mapping. For instance store volumes, the data is not preserved.

For an EBS-backed AMI, you can add EBS volumes and instance store volumes using a block device mapping. For an instance store-backed AMI, you can add instance store volumes only by modifying the block device mapping entries in the image manifest file when registering the image.

Note
For M3 instances, you must specify instance store volumes in the block device mapping for the instance when you launch it. When you launch an M3 instance, instance store volumes specified in the block device mapping for the AMI may be ignored if they are not specified as part of the instance block device mapping.
To add volumes to an AMI using the console

Open the Amazon EC2 console.

In the navigation pane, choose Instances.

Select an instance and choose Actions, Image, Create Image.

In the Create Image dialog box, choose Add New Volume.

Select a volume type from the Type list and a device name from the Device list. For an EBS volume, you can optionally specify a snapshot, volume size, and volume type.

Choose Create Image.

To add volumes to an AMI using the command line

Use the create-image AWS CLI command to specify a block device mapping for an EBS-backed AMI. Use the register-image AWS CLI command to specify a block device mapping for an instance store-backed AMI.

Specify the block device mapping using the following parameter:

--block-device-mappings [mapping, ...]
To add an instance store volume, use the following mapping:

Copy
{
    "DeviceName": "/dev/sdf",
    "VirtualName": "ephemeral0"
}
To add an empty 100 GiB Magnetic volume, use the following mapping:

Copy
{
    "DeviceName": "/dev/sdg",
    "Ebs": {
      "VolumeSize": 100
    }
}
To add an EBS volume based on a snapshot, use the following mapping:

Copy
{
    "DeviceName": "/dev/sdh",
    "Ebs": {
      "SnapshotId": "snap-xxxxxxxx"
    }
}
To omit a mapping for a device, use the following mapping:

Copy
{
    "DeviceName": "/dev/sdj",
    "NoDevice": ""
}
Alternatively, you can use the -BlockDeviceMapping parameter with the following commands (AWS Tools for Windows PowerShell):

New-EC2Image
Register-EC2Image
Viewing the EBS Volumes in an AMI Block Device Mapping

You can easily enumerate the EBS volumes in the block device mapping for an AMI.

To view the EBS volumes for an AMI using the console

Open the Amazon EC2 console.

In the navigation pane, choose AMIs.

Choose EBS images from the Filter list to get a list of EBS-backed AMIs.

Select the desired AMI, and look at the Details tab. At a minimum, the following information is available for the root device:

Root Device Type (ebs)
Root Device Name (for example, /dev/sda1)
Block Devices (for example, /dev/sda1=snap-1234567890abcdef0:8:true)
If the AMI was created with additional EBS volumes using a block device mapping, the Block Devices field displays the mapping for those additional volumes as well. (Recall that this screen doesn't display instance store volumes.)

To view the EBS volumes for an AMI using the command line

Use the describe-images (AWS CLI) command or Get-EC2Image (AWS Tools for Windows PowerShell) command to enumerate the EBS volumes in the block device mapping for an AMI.

Instance Block Device Mapping

By default, an instance that you launch includes any storage devices specified in the block device mapping of the AMI from which you launched the instance. You can specify changes to the block device mapping for an instance when you launch it, and these updates overwrite or merge with the block device mapping of the AMI.

Limits

For the root volume, you can only modify the following: volume size, volume type, and the Delete on Termination flag.
When you modify an EBS volume, you can't decrease its size. Therefore, you must specify a snapshot whose size is equal to or greater than the size of the snapshot specified in the block device mapping of the AMI.
Contents

Updating the Block Device Mapping when Launching an Instance
Updating the Block Device Mapping of a Running Instance
Viewing the EBS Volumes in an Instance Block Device Mapping
Viewing the Instance Block Device Mapping for Instance Store Volumes
Updating the Block Device Mapping when Launching an Instance

You can add EBS volumes and instance store volumes to an instance when you launch it. Note that updating the block device mapping for an instance doesn't make a permanent change to the block device mapping of the AMI from which it was launched.

To add volumes to an instance using the console

Open the Amazon EC2 console.

From the dashboard, choose Launch Instance.

On the Choose an Amazon Machine Image (AMI) page, select the AMI to use and choose Select.

Follow the wizard to complete the Choose an Instance Type and Configure Instance Details pages.

On the Add Storage page, you can modify the root volume, EBS volumes, and instance store volumes as follows:

To change the size of the root volume, locate the Root volume under the Type column, and change its Size field.
To suppress an EBS volume specified by the block device mapping of the AMI used to launch the instance, locate the volume and click its Delete icon.
To add an EBS volume, choose Add New Volume, choose EBS from the Type list, and fill in the fields (Device, Snapshot, and so on).
To suppress an instance store volume specified by the block device mapping of the AMI used to launch the instance, locate the volume, and choose its Delete icon.
To add an instance store volume, choose Add New Volume, select Instance Store from the Type list, and select a device name from Device.
Complete the remaining wizard pages, and choose Launch.

To add volumes to an instance using the command line

Use the run-instances AWS CLI command to specify a block device mapping for an instance.

Specify the block device mapping using the following parameter:

--block-device-mappings [mapping, ...]
For example, suppose that an EBS-backed AMI specifies the following block device mapping:

/dev/sdb=ephemeral0
/dev/sdh=snap-1234567890abcdef0
/dev/sdj=:100
To prevent /dev/sdj from attaching to an instance launched from this AMI, use the following mapping:

Copy
{
    "DeviceName": "/dev/sdj",
    "NoDevice": ""
}
To increase the size of /dev/sdh to 300 GiB, specify the following mapping. Notice that you don't need to specify the snapshot ID for /dev/sdh, because specifying the device name is enough to identify the volume.

Copy
{
    "DeviceName": "/dev/sdh",
    "Ebs": {
      "VolumeSize": 300
    }
}
To attach an additional instance store volume, /dev/sdc, specify the following mapping. If the instance type doesn't support multiple instance store volumes, this mapping has no effect.

Copy
{
    "DeviceName": "/dev/sdc",
    "VirtualName": "ephemeral1"
}
Alternatively, you can use the -BlockDeviceMapping parameter with the New-EC2Instance command (AWS Tools for Windows PowerShell).

Updating the Block Device Mapping of a Running Instance

You can use the following modify-instance-attribute AWS CLI command to update the block device mapping of a running instance. Note that you do not need to stop the instance before changing this attribute.

Copy
aws ec2 modify-instance-attribute --instance-id i-1a2b3c4d --block-device-mappings file://mapping.json
For example, to preserve the root volume at instance termination, specify the following in mapping.json:

Copy
[
  {
    "DeviceName": "/dev/sda1",
    "Ebs": {
      "DeleteOnTermination": false
    }
  }
]
Alternatively, you can use the -BlockDeviceMapping parameter with the Edit-EC2InstanceAttribute command (AWS Tools for Windows PowerShell).

Viewing the EBS Volumes in an Instance Block Device Mapping

You can easily enumerate the EBS volumes mapped to an instance.

Note
For instances launched before the release of the 2009-10-31 API, AWS can't display the block device mapping. You must detach and reattach the volumes so that AWS can display the block device mapping.
To view the EBS volumes for an instance using the console

Open the Amazon EC2 console.

In the navigation pane, choose Instances.

In the search bar, type Root Device Type, and then choose EBS. This displays a list of EBS-backed instances.

Select the desired instance and look at the details displayed in the Description tab. At a minimum, the following information is available for the root device:

Root device type (ebs)
Root device (for example, /dev/sda1)
Block devices (for example, /dev/sda1, /dev/sdh, and /dev/sdj)
If the instance was launched with additional EBS volumes using a block device mapping, the Block devices field displays those additional volumes as well as the root device. (Recall that this dialog box doesn't display instance store volumes.)


              Block devices for an instance.
            
To display additional information about a block device, select its entry next to Block devices. This displays the following information for the block device:

EBS ID (vol-xxxxxxxx)
Root device type (ebs)
Attachment time (yyyy-mmThh:mm:ss.ssTZD)
Block device status (attaching, attached, detaching, detached)
Delete on termination (Yes, No)
To view the EBS volumes for an instance using the command line

Use the describe-instances (AWS CLI) command or Get-EC2Instance (AWS Tools for Windows PowerShell) command to enumerate the EBS volumes in the block device mapping for an instance.

Viewing the Instance Block Device Mapping for Instance Store Volumes

When you view the block device mapping for your instance, you can see only the EBS volumes, not the instance store volumes. You can use instance metadata to query the complete block device mapping. The base URI for all requests for instance metadata is http://169.254.169.254/latest/.

First, connect to your running instance. From the instance, use this query to get its block device mapping.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/block-device-mapping/
The response includes the names of the block devices for the instance. For example, the output for an instance store–backed m1.small instance looks like this.

ami
ephemeral0
root
swap
The ami device is the root device as seen by the instance. The instance store volumes are named ephemeral[0-23]. The swap device is for the page file. If you've also mapped EBS volumes, they appear as ebs1, ebs2, and so on.

To get details about an individual block device in the block device mapping, append its name to the previous query, as shown here.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/block-device-mapping/ephemeral0
For more information, see Instance Metadata and User Data.

Using Public Data Sets

Amazon Web Services provides a repository of public data sets that can be seamlessly integrated into AWS cloud-based applications. Amazon stores the data sets at no charge to the community and, as with all AWS services, you pay only for the compute and storage you use for your own applications.

Contents

Public Data Set Concepts
Finding Public Data Sets
Creating a Public Data Set Volume from a Snapshot
Attaching and Mounting the Public Data Set Volume
Public Data Set Concepts

Previously, large data sets such as the mapping of the Human Genome and the US Census data required hours or days to locate, download, customize, and analyze. Now, anyone can access these data sets from an EC2 instance and start computing on the data within minutes. You can also leverage the entire AWS ecosystem and easily collaborate with other AWS users. For example, you can produce or use prebuilt server images with tools and applications to analyze the data sets. By hosting this important and useful data with cost-efficient services such as Amazon EC2, AWS hopes to provide researchers across a variety of disciplines and industries with tools to enable more innovation, more quickly.

For more information, go to the Public Data Sets on AWS Page.

Available Public Data Sets

Public data sets are currently available in the following categories:

Biology—Includes Human Genome Project, GenBank, and other content.
Chemistry—Includes multiple versions of PubChem and other content.
Economics—Includes census data, labor statistics, transportation statistics, and other content.
Encyclopedic—Includes Wikipedia content from multiple sources and other content.
Finding Public Data Sets

Before you can use a public data set, you must locate the data set and determine which format the data set is hosted in. The data sets are available in two possible formats: Amazon EBS snapshots or Amazon S3 buckets.

To find a public data set and determine its format

Go to the Public Data Sets Page to see a listing of all available public data sets. You can also enter a search phrase on this page to query the available public data set listings.

Click the name of a data set to see its detail page.

On the data set detail page, look for a snapshot ID listing to identify an Amazon EBS formatted data set or an Amazon S3 URL.

Data sets that are in snapshot format are used to create new EBS volumes that you attach to an EC2 instance. For more information, see Creating a Public Data Set Volume from a Snapshot.

For data sets that are in Amazon S3 format, you can use the AWS SDKs or the HTTP query API to access the information, or you can use the AWS CLI to copy or synchronize the data to and from your instance. For more information, see Amazon S3 and Amazon EC2.

You can also use Amazon EMR to analyze and work with public data sets. For more information, see What is Amazon EMR?.

Creating a Public Data Set Volume from a Snapshot

To use a public data set that is in snapshot format, you create a new volume, specifying the snapshot ID of the public data set. You can create your new volume using the AWS Management Console as follows. If you prefer, you can use the create-volume AWS CLI command instead.

To create a public data set volume from a snapshot

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region that your data set snapshot is located in.

If you need to create this volume in a different region, you can copy the snapshot to that region and then use it to create a volume in that region. For more information, see Copying an Amazon EBS Snapshot.

In the navigation pane, choose ELASTIC BLOCK STORE, Volumes.

Choose Create Volume.

For Volume Type, choose a volume type. For more information, see Amazon EBS Volume Types.

For Snapshot, start typing the ID or description of the snapshot that has the data set, and choose it from the list.

If the snapshot that you are expecting to see does not appear, you might not have selected the region it is in. If the data set you identified in Finding Public Data Sets does not specify a region on its detail page, it is likely contained in the us-east-1 US East (N. Virginia) region.

For Size (GiB), type the size of the volume, or verify the that the default size of the snapshot is adequate.

Note
If you specify both a volume size and a snapshot, the size must be equal to or greater than the snapshot size. When you select a volume type and a snapshot, the minimum and maximum sizes for the volume are shown next to Size.
With a Provisioned IOPS SSD volume, for IOPS, type the maximum number of input/output operations per second (IOPS) that the volume should support.

For Availability Zone, choose the Availability Zone in which to create the volume. EBS volumes can only be attached to instances in the same Availability Zone.

(Optional) Choose Create additional tags to add tags to the volume. For each tag, provide a tag key and a tag value.

Choose Create Volume.

Attaching and Mounting the Public Data Set Volume

After you have created your new data set volume, you need to attach it to an EC2 instance to access the data (this instance must also be in the same Availability Zone as the new volume). For more information, see Attaching an Amazon EBS Volume to an Instance.

After you have attached the volume to an instance, you need to mount the volume on the instance. For more information, see Making an Amazon EBS Volume Available for Use.

If you restored a snapshot to a larger volume than the default for that snapshot, you must extend the file system on the volume to take advantage of the extra space. For more information, see Modifying the Size, IOPS, or Type of an EBS Volume on Linux.



