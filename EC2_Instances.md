Amazon EC2 Instances

If you're new to Amazon EC2, see the following topics to get started:

What Is Amazon EC2?
Setting Up with Amazon EC2
Getting Started with Amazon EC2 Linux Instances
Instance Lifecycle
Before you launch a production environment, you need to answer the following questions.

Q. What instance type best meets my needs?
Amazon EC2 provides different instance types to enable you to choose the CPU, memory, storage, and networking capacity that you need to run your applications. For more information, see Instance Types.

Q. What purchasing option best meets my needs?
Amazon EC2 supports On-Demand instances (the default), Spot instances, and Reserved Instances. For more information, see Instance Purchasing Options.

Q. Which type of root volume meets my needs?
Each instance is backed by Amazon EBS or backed by instance store. Select an AMI based on which type of root volume you need. For more information, see Storage for the Root Device.

Q. Would I benefit from using a virtual private cloud?
If you can launch instances in either EC2-Classic or EC2-VPC, you'll need to decide which platform meets your needs. For more information, see Supported Platforms and Amazon EC2 and Amazon Virtual Private Cloud.

Q. Can I remotely manage a fleet of EC2 instances and machines in my hybrid environment?
Amazon Elastic Compute Cloud (Amazon EC2) Run Command lets you remotely and securely manage the configuration of your Amazon EC2 instances, virtual machines (VMs) and servers in hybrid environments, or VMs from other cloud providers. For more information, see Systems Manager Remote Management (Run Command).

Instance Types

When you launch an instance, the instance type that you specify determines the hardware of the host computer used for your instance. Each instance type offers different compute, memory, and storage capabilities and are grouped in instance families based on these capabilities. Select an instance type based on the requirements of the application or software that you plan to run on your instance.

Amazon EC2 provides each instance with a consistent and predictable amount of CPU capacity, regardless of its underlying hardware.

Amazon EC2 dedicates some resources of the host computer, such as CPU, memory, and instance storage, to a particular instance. Amazon EC2 shares other resources of the host computer, such as the network and the disk subsystem, among instances. If each instance on a host computer tries to use as much of one of these shared resources as possible, each receives an equal share of that resource. However, when a resource is under-utilized, an instance can consume a higher share of that resource while it's available.

Each instance type provides higher or lower minimum performance from a shared resource. For example, instance types with high I/O performance have a larger allocation of shared resources. Allocating a larger share of shared resources also reduces the variance of I/O performance. For most applications, moderate I/O performance is more than enough. However, for applications that require greater or more consistent I/O performance, consider an instance type with higher I/O performance.

Contents

Available Instance Types
Hardware Specifications
Virtualization Types
Networking and Storage Features
Instance Limits
Available Instance Types

Amazon EC2 provides the instance types listed in the following tables.

Current Generation Instances

For the best performance, we recommend that you use the current generation instance types when you launch new instances.

For more information about the current generation instance types, see Amazon EC2 Instances.

Instance Family	Current Generation Instance Types
General purpose
t2.nano | t2.micro | t2.small | t2.medium | t2.large | t2.xlarge | t2.2xlarge | m4.large | m4.xlarge | m4.2xlarge | m4.4xlarge | m4.10xlarge | m4.16xlarge | m3.medium | m3.large | m3.xlarge | m3.2xlarge
Compute optimized
c4.large | c4.xlarge | c4.2xlarge | c4.4xlarge | c4.8xlarge | c3.large | c3.xlarge | c3.2xlarge | c3.4xlarge | c3.8xlarge
Memory optimized
r3.large | r3.xlarge | r3.2xlarge | r3.4xlarge | r3.8xlarge | r4.large | r4.xlarge | r4.2xlarge | r4.4xlarge | r4.8xlarge | r4.16xlarge | x1.16xlarge | x1.32xlarge
Storage optimized
d2.xlarge | d2.2xlarge | d2.4xlarge | d2.8xlarge | i2.xlarge | i2.2xlarge | i2.4xlarge | i2.8xlarge | i3.large | i3.xlarge | i3.2xlarge | i3.4xlarge | i3.8xlarge | i3.16xlarge
Accelerated computing
f1.2xlarge | f1.16xlarge | p2.xlarge | p2.8xlarge | p2.16xlarge | g2.2xlarge | g2.8xlarge | g3.4xlarge | g3.8xlarge | g3.16xlarge
Previous Generation Instances

Amazon Web Services offers previous generation instances for users who have optimized their applications around these instances and have yet to upgrade. We encourage you to use the latest generation of instances to get the best performance, but we will continue to support these previous generation instances. If you are currently using a previous generation instance, you can see which current generation instance would be a suitable upgrade. For more information, see Previous Generation Instances.

Instance Family	Previous Generation Instance Types
General purpose
m1.small | m1.medium | m1.large | m1.xlarge
Compute optimized
c1.medium | c1.xlarge | cc2.8xlarge
Memory optimized
m2.xlarge | m2.2xlarge | m2.4xlarge | cr1.8xlarge
Storage optimized
hi1.4xlarge | hs1.8xlarge
Accelerated computing
cg1.4xlarge
Micro instances
t1.micro
Hardware Specifications

For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

To determine which instance type best meets your needs, we recommend that you launch an instance and use your own benchmark application. Because you pay by the instance hour, it's convenient and inexpensive to test multiple instance types before making a decision.

Even after you make a decision, if your needs change, you can resize your instance later on. For more information, see Resizing Your Instance.

Note
Amazon EC2 instances run on 64-bit virtual Intel processors as specified in the instance type product pages. For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances. However, confusion may result from industry naming conventions for 64-bit CPUs. Chip manufacturer Advanced Micro Devices (AMD) introduced the first commercially successful 64-bit architecture based on the Intel x86 instruction set. Consequently, the architecture is widely referred to as AMD64 regardless of the chip manufacturer. Windows and several Linux distributions follow this practice. This explains why the internal system information on an Ubuntu or Windows EC2 instance displays the CPU architecture as AMD64 even though the instances are running on Intel hardware.
Virtualization Types

Each instance type supports one or both of the following types of virtualization: paravirtual (PV) or hardware virtual machine (HVM). The virtualization type of your instance is determined by the AMI that you use to launch it.

For best performance, we recommend that you use an HVM AMI. In addition, HVM AMIs are required to take advantage of enhanced networking. HVM virtualization uses hardware-assist technology provided by the AWS platform. With HVM virtualization, the guest VM runs as if it were on a native hardware platform, except that it still uses PV network and storage drivers for improved performance. For more information, see Linux AMI Virtualization Types.

Networking and Storage Features

When you select an instance type, this determines the networking and storage features that are available.

Networking features

Some instance types are not available in EC2-Classic, so you must launch them in a VPC. By launching an instance in a VPC, you can leverage features that are not available in EC2-Classic, such as enhanced networking, assigning multiple private IPv4 addresses to an instance, assigning IPv6 addresses to an instance, and changing the security groups assigned to an instance. For more information, see Instance Types Available Only in a VPC.
To maximize the networking and bandwidth performance of your instance type, you can do the following:
Launch supported instance types into a placement group to optimize your instances for high performance computing (HPC) applications. Instances in a common placement group can benefit from high-bandwidth (10 Gbps), low-latency networking. For more information, see Placement Groups. Instance types that support 10 Gbps network speeds can only take advantage of those network speeds when launched in a placement group.
Enable enhanced networking for supported current generation instance types to get significantly higher packet per second (PPS) performance, lower network jitter, and lower latencies. For more information, see Enhanced Networking on Linux.
The maximum supported MTU varies across instance types. All Amazon EC2 instance types support standard Ethernet V2 1500 MTU frames. All current generation instances support 9001 MTU, or jumbo frames, and some previous generation instances support them as well. For more information, see Network Maximum Transmission Unit (MTU) for Your EC2 Instance.
Storage features

Some instance types support EBS volumes and instance store volumes, while other instance types support only EBS volumes. Some instances that support instance store volumes use solid state drives (SSD) to deliver very high random I/O performance. For more information, see Storage.
To obtain additional, dedicated capacity for Amazon EBS I/O, you can launch some instance types as EBS–optimized instances. Some instance types are EBS–optimized by default. For more information, see Amazon EBS–Optimized Instances.
The following table summarizes the networking and storage features supported by the current generation instance types.

VPC only	EBS only	Instance store	Placement group	HVM only	Enhanced networking	IPv6 support (VPC only)
C3
SSD
Yes
Intel 82599 VF
Yes
C4
Yes
Yes
Yes
Yes
Intel 82599 VF
Yes
D2
HDD
Yes
Yes
Intel 82599 VF
Yes
F1
Yes
NVMe *
Yes
Yes
ENA
Yes
G2
SSD
Yes
Yes
G3
Yes	Yes		
Yes
Yes
ENA	Yes
I2
SSD
Yes
Yes
Intel 82599 VF
Yes
I3
Yes
NVMe *
Yes
Yes
ENA
Yes
M3
SSD
M4
Yes
Yes
Yes
Yes
m4.16xlarge: ENA

All other sizes: Intel 82599 VF
Yes
P2
Yes
Yes
Yes
Yes
ENA
Yes
R3
SSD
Yes
Yes
Intel 82599 VF
Yes
R4
Yes
Yes
Yes
Yes
ENA
Yes
T2
Yes
Yes
Yes
Yes
X1	Yes		SSD	Yes	Yes	ENA	Yes
* The root device volume must be an Amazon EBS volume.

Instance Limits

There is a limit on the total number of instances that you can launch in a region, and there are additional limits on some instance types.

For more information about the default limits, see How many instances can I run in Amazon EC2?

For more information about viewing your current limits or requesting an increase in your current limits, see Amazon EC2 Service Limits.

T2 Instances

T2 instances are designed to provide moderate baseline performance and the capability to burst to significantly higher performance as required by your workload. They are intended for workloads that don't use the full CPU often or consistently, but occasionally need to burst. T2 instances are well suited for general purpose workloads, such as web servers, developer environments, and small databases. For more information about T2 instance pricing and additional hardware details, see Amazon EC2 Instances.

If your account is less than 12 months old, you can use a t2.micro instance for free within certain usage limits. For more information, see AWS Free Tier.

Contents

Hardware Specifications
T2 Instance Requirements
CPU Credits
Monitoring Your CPU Credits
Hardware Specifications

For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

T2 Instance Requirements

The following are the requirements for T2 instances:

You must launch your T2 instances into a virtual private cloud (VPC); they are not supported on the EC2-Classic platform. Amazon VPC enables you to launch AWS resources into a virtual network that you've defined. You cannot change the instance type of an existing instance in EC2-Classic to a T2 instance type. For more information about EC2-Classic and EC2-VPC, see Supported Platforms For more information about launching a VPC-only instance, see Instance Types Available Only in a VPC.
You must launch a T2 instance using an HVM AMI. For more information, see Linux AMI Virtualization Types.
You must launch your T2 instances using an EBS volume as the root device. For more information, see Amazon EC2 Root Device Volume.
T2 instances are available as On-Demand instances and Reserved Instances, but they are not available as Spot instances, Scheduled Instances, or Dedicated instances. They are also not supported on a Dedicated Host. For more information about these options, see Instance Purchasing Options.
There is a limit on the total number of instances that you can launch in a region, and there are additional limits on some instance types. By default, you can run up to 20 T2 instances simultaneously. If you need more T2 instances, you can request them using the Amazon EC2 Instance Request Form.
Ensure that the T2 instance size you choose passes the minimum memory requirements of your operating system and applications. Operating systems with graphical user interfaces that consume significant memory and CPU resources (for example, Windows) may require a t2.micro, or larger, instance size for many use cases. As the memory and CPU requirements of your workload grows over time, you can scale to larger T2 instance sizes, or other EC2 instance types.
CPU Credits

A CPU Credit provides the performance of a full CPU core for one minute. Traditional Amazon EC2 instance types provide fixed performance, while T2 instances provide a baseline level of CPU performance with the ability to burst above that baseline level. The baseline performance and ability to burst are governed by CPU credits.

What is a CPU credit?

One CPU credit is equal to one vCPU running at 100% utilization for one minute. Other combinations of vCPUs, utilization, and time are also equal to one CPU credit; for example, one vCPU running at 50% utilization for two minutes or two vCPUs running at 25% utilization for two minutes.

How are CPU credits earned?

Each T2 instance starts with a healthy initial CPU credit balance and then continuously (at a millisecond-level resolution) receives a set rate of CPU credits per hour, depending on instance size. The accounting process for whether credits are accumulated or spent also happens at a millisecond-level resolution, so you don't have to worry about overspending CPU credits; a short burst of CPU takes a small fraction of a CPU credit.

When a T2 instance uses fewer CPU resources than its base performance level allows (such as when it is idle), the unused CPU credits (or the difference between what was earned and what was spent) are stored in the credit balance for up to 24 hours, building CPU credits for bursting. When your T2 instance requires more CPU resources than its base performance level allows, it uses credits from the CPU credit balance to burst up to 100% utilization. The more credits your T2 instance has for CPU resources, the more time it can burst beyond its base performance level when more performance is needed.

The following table lists the initial CPU credit allocation received at launch, the rate at which CPU credits are received, the baseline performance level as a percentage of a full core performance (utilizing a single vCPU), and the maximum earned CPU credit balance that an instance can accrue.

Instance type

Initial CPU credit*

CPU credits earned per hour

vCPUs	
Base performance (CPU utilization)

Maximum earned CPU credit balance***

t2.nano
30
3
1	
5%
72
t2.micro
30
6
1	
10%
144
t2.small
30
12
1	
20%
288
t2.medium
60
24
2	
40% (of 200% max)**
576
t2.large
60
36
2	
60% (of 200% max)**
864
t2.xlarge
120
54
4	
90% (of 400% max)**
1296
t2.2xlarge
240
81
8	
135% (of 800% max)**
1944

* There are limits to how many T2 instances will launch or start with the initial CPU credit, which by default is set to 100 launches or starts of any T2 instance per account, per 24-hour period, per region. If you'd like to increase this limit, you can file a customer support limit increase request by using the Amazon EC2 Credit Based Instances Launch Credits Form. If your account does not launch or start more than 100 T2 instances in 24 hours, this limit will not affect you.
New accounts may have a lower limit which increases over time based on your usage.
** t2.medium and larger instances have more than one vCPU. The base performance in the table is a percentage of utilizing a single vCPU (you could split performance over multiple vCPUs). To calculate the base CPU utilization for the instance, divide the combined vCPU percentages by the number of vCPUs. For example, the base performance for a t2.large is 60% of 1 vCPU. A t2.large instance has 2 vCPUs, therefore the CPU utilization for a t2.large instance operating at base performance is shown as 30% in CloudWatch CPU metrics.
*** This maximum does not include the initial CPU credits, which are used first and do not expire. For example, a t2.micro instance that was launched and then remained idle for over 24 hours could reach a credit balance of up to 174 (30 initial CPU credits + 144 earned credits). However, after the instance uses the initial 30 CPU credits, the credit balance can never exceed 144 unless a new initial CPU credit balance is issued by stopping and starting the instance.
The initial credit balance is designed to provide a good startup experience. The maximum earned credit balance for an instance is equal to the number of CPU credits received per hour times 24 hours. For example, a t2.micro instance earns 6 CPU credits per hour and can accumulate a maximum earned CPU credit balance of 144 CPU credits.

Do CPU credits expire?

Initial CPU credits do not expire, but they are used first when an instance uses CPU credits. Unused earned credits from a given 5 minute interval expire 24 hours after they are earned, and any expired credits are removed from the CPU credit balance at that time, before any newly earned credits are added. Additionally, the CPU credit balance for an instance does not persist between instance stops and starts; stopping an instance causes it to lose its credit balance entirely, but when it restarts it will receive its initial credit balance again.

For example, if a t2.small instance had a CPU utilization of 5% for the hour, it would have used 3 CPU credits (5% of 60 minutes), but it would have earned 12 CPU credits during the hour, so the difference of 9 CPU credits would be added to the CPU credit balance. Any CPU credits in the balance that reached their 24 hour expiration date during that time (which could be as many as 12 credits if the instance was completely idle 24 hours ago) would also be removed from the balance. If the number of credits expired is greater than those earned, the credit balance will go down; conversely, if the number of credits expired is fewer than those earned, the credit balance will go up.

What happens if I use all of my credits?

If your instance uses all of its CPU credit balance, performance remains at the baseline performance level. If your instance is running low on credits, your instance’s CPU credit consumption (and therefore CPU performance) is gradually lowered to the base performance level over a 15-minute interval, so you will not experience a sharp performance drop-off when your CPU credits are depleted. If your instance consistently uses all of its CPU credit balance, we recommend a larger T2 size or a fixed performance instance type such as M3 or C3.

Monitoring Your CPU Credits

You can see the credit balance for each T2 instance presented in the Amazon EC2 per-instance metrics of the CloudWatch console. T2 instances have two metrics, CPUCreditUsage and CPUCreditBalance. The CPUCreditUsage metric indicates the number of CPU credits used during the measurement period. The CPUCreditBalance metric indicates the number of unused CPU credits a T2 instance has earned. This balance is depleted during burst time as CPU credits are spent more quickly than they are earned.

The following table describes the new available CloudWatch metrics. For more information about using these metrics in CloudWatch, see List the Available CloudWatch Metrics for Your Instances.

Metric	Description
CPUCreditUsage
[T2 instances] The number of CPU credits consumed by the instance. One CPU credit equals one vCPU running at 100% utilization for one minute or an equivalent combination of vCPUs, utilization, and time (for example, one vCPU running at 50% utilization for two minutes or two vCPUs running at 25% utilization for two minutes).

CPU credit metrics are available only at a 5 minute frequency. If you specify a period greater than five minutes, use the Sum statistic instead of the Average statistic.

Units: Count
CPUCreditBalance
[T2 instances] The number of CPU credits available for the instance to burst beyond its base CPU utilization. Credits are stored in the credit balance after they are earned and removed from the credit balance after they expire. Credits expire 24 hours after they are earned.

CPU credit metrics are available only at a 5 minute frequency.

Units: Count

Compute Optimized Instances

Compute optimized instances are ideal for compute-bound applications that benefit from high performance processors. They are well suited for the following applications:

Batch processing workloads
Media transcoding
High-traffic web servers, massively multiplayer online (MMO) gaming servers, and ad serving engines
High performance computing (HPC) and other compute-intensive applications
Contents

Hardware Specifications
Compute Instance Performance
Compute Instance Features
Support for 36 vCPUs
Instance Limits
Hardware Specifications

For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

Compute Instance Performance

EBS-optimized instances enable you to get consistently high performance for your EBS volumes by eliminating contention between Amazon EBS I/O and other network traffic from your instance. C4 instances are EBS-optimized by default at no additional cost. You can enable EBS optimization for your C3 instances for an additional low, hourly fee. For more information, see Amazon EBS–Optimized Instances.

You can enable enhanced networking capabilities. Enhanced networking provides significantly higher packet per second (PPS) performance, lower network jitter, and lower latencies. For more information, see Enhanced Networking on Linux.

The c4.8xlarge instance type provides the ability to control processor C-states and P-states on Linux. C-states control the sleep levels that a core can enter when it is inactive, while P-states control the desired performance (in CPU frequency) from a core. For more information, see Processor State Control for Your EC2 Instance.

Compute Instance Features

The following is a summary of features for compute optimized instances:

VPC only	EBS only	SSD volumes	Placement group	HVM only	Enhanced networking
C3
Yes
Yes
Intel 82599 VF
C4
Yes
Yes
Yes
Yes
Intel 82599 VF
For more information, see the following:

Instance Types Available Only in a VPC
Amazon EBS–Optimized Instances
Amazon EC2 Instance Store
Placement Groups
Enhanced Networking on Linux
Support for 36 vCPUs

The c4.8xlarge instance type provides 36 vCPUs, which might cause launch issues in some Linux operating systems that have a vCPU limit of 32. We strongly recommend that you use the latest AMIs when you launch c4.8xlarge instances.

The following AMIs support launching c4.8xlarge instances with 36 vCPUs:

Amazon Linux AMI 2017.03 (HVM)
Ubuntu Server 14.04 LTS (HVM)
Red Hat Enterprise Linux 7.1 (HVM)
SUSE Linux Enterprise Server 12 (HVM)
If you must use a different AMI for your application, and your c4.8xlarge instance launch does not complete successfully (for example, if your instance status changes to stopped during launch with a Client.InstanceInitiatedShutdown state transition reason), modify your instance as described in the following procedure to support more than 32 vCPUs so that you can use the c4.8xlarge instance type.

To update an instance to support more than 32 vCPUs

Launch a C4 instance using your AMI, choosing any C4 instance type other than c4.8xlarge.

Update the kernel to the latest version by following your operating system-specific instructions. For example, for RHEL 6, use the following command.

Copy
sudo yum update -y kernel
Stop the instance.

(Optional) Create an AMI from the instance that you can use to launch any additional c4.8xlarge instances that you need in the future.

Change the instance type of your stopped instance to c4.8xlarge (choose Actions, Instance Settings, Change Instance Type, and then follow the directions).

Start the instance. If the instance launches properly, you are done. If the instance still does not boot properly, proceed to the next step.

(Optional) If the instance still does not boot properly, the kernel on your instance may not support more than 32 vCPUs. However, you may be able to boot the instance if you limit the vCPUs.

Change the instance type of your stopped instance to any C4 instance type other than c4.8xlarge (choose Actions, Instance Settings, Change Instance Type, and then follow the directions).

Add the maxcpus=32 option to your boot kernel parameters by following your operating system-specific instructions. For example, for RHEL 6, edit the /boot/grub/menu.lst file and add the following option to the most recent and active kernel entry:

Copy
default=0
timeout=1
splashimage=(hd0,0)/boot/grub/splash.xpm.gz
hiddenmenu
title Red Hat Enterprise Linux Server (2.6.32-504.3.3.el6.x86_64)
root (hd0,0)
kernel /boot/vmlinuz-2.6.32-504.3.3.el6.x86_64 maxcpus=32 console=ttyS0 ro root=UUID=9996863e-b964-47d3-a33b-3920974fdbd9 rd_NO_LUKS  KEYBOARDTYPE=pc KEYTABLE=us LANG=en_US.UTF-8 xen_blkfront.sda_is_xvda=1 console=ttyS0,115200n8 console=tty0 rd_NO_MD SYSFONT=latarcyrheb-sun16 crashkernel=auto rd_NO_LVM rd_NO_DM
initrd /boot/initramfs-2.6.32-504.3.3.el6.x86_64.img
Stop the instance.

(Optional) Create an AMI from the instance that you can use to launch any additional c4.8xlarge instances that you need in the future.

Change the instance type of your stopped instance to c4.8xlarge (choose Actions, Instance Settings, Change Instance Type, and then follow the directions).

Start the instance.

Instance Limits

C4 instances require 64-bit HVM AMIs. They have high-memory (up to 60 GiB of RAM), and require a 64-bit operating system to take advantage of that capacity. HVM AMIs provide superior performance in comparison to paravirtual (PV) AMIs on high-memory instance types. In addition, you must use an HVM AMI to take advantage of enhanced networking.
There is a limit on the total number of instances that you can launch in a region, and there are additional limits on some instance types. For more information, see How many instances can I run in Amazon EC2?. To request a limit increase, use the Amazon EC2 Instance Request Form.

Memory Optimized Instances

Memory optimized instances are designed to deliver fast performance for workloads that process large data sets in memory.

R4 Instances

R4 instances are well suited for the following applications:

High performance relational (MySQL) and NoSQL (MongoDB, Cassandra) databases.
Distributed web scale cache stores that provide in-memory caching of key-value type data (Memcached and Redis).
In-memory databases using optimized data storage formats and analytics for business intelligence (for example, SAP HANA).
Applications performing real-time processing of big unstructured data (financial services, Hadoop/Spark clusters).
High-performance computing (HPC) and Electronic Design Automation (EDA) applications.
X1 Instances

X1 instances are well suited for the following applications:

In-memory databases such SAP HANA, including SAP-certified support for Business Suite S/4HANA, Business Suite on HANA (SoH), Business Warehouse on HANA (BW), and Data Mart Solutions on HANA. For more information, see SAP HANA on the AWS Cloud.
Big-data processing engines such as Apache Spark or Presto.
High-performance computing (HPC) applications.
R3 Instances

R3 instances are well suited for the following applications:

High performance relational (MySQL) and NoSQL (MongoDB, Cassandra) databases.
In-memory analytics.
Genome assembly and analysis.
Enterprise applications (for example, Microsoft SharePoint).
Hardware Specifications

For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

Memory Performance

R4 instances enable up to 488 GiB of RAM.

X1 instances include Intel Scalable M​​emory Buffers, providing 300 GiB/s of sustainable memory-read bandwidth and 140 GiB/s of sustainable memory-write bandwidth.

R3 instances enable up to 244 GiB of RAM.

Memory optimized instances have high-memory and require 64-bit HVM AMIs to take advantage of that capacity. HVM AMIs provide superior performance in comparison to paravirtual (PV) AMIs on high-memory instance types. For more information, see Linux AMI Virtualization Types.

Compute Performance

R4 instances feature up to 64 vCPUs and are powered by two AWS-customized Intel XEON processors based on E5-2686v4 that feature high-memory bandwidth and larger L3 caches to boost the performance of in-memory applications.

X1 instances feature up to 128 vCPUs and are powered by four Intel Xeon E7-8880 v3 processors that feature high-memory bandwidth and larger L3 caches to boost the performance of in-memory applications.

Memory optimized instances enable increased cryptographic performance through the latest Intel AES-NI feature, support Intel Transactional Synchronization Extensions (TSX) to boost the performance of in-memory transactional data processing, and support Advanced Vector Extensions 2 (Intel AVX2) processor instructions to expand most integer commands to 256 bits.

Some memory optimized instances provide the ability to control processor C-states and P-states on Linux. C-states control the sleep levels that a core can enter when it is inactive, while P-states control the desired performance (measured by CPU frequency) from a core. For more information, see Processor State Control for Your EC2 Instance.

Network Performance

To increase network performance of your memory optimized instances, enable enhanced networking. For more information, see Enhanced Networking on Linux.

R4 instances deliver high packet per second performance with consistently low latencies using Elastic Network Adapter (ENA). Most applications do not consistently need a high level of network performance, but can benefit from having access to increased bandwidth when they send or receive data. The smaller R4 instance sizes offer peak throughput of 10 Gbps. These instances use a network I/O credit mechanism to allocate network bandwidth to instances based on average bandwidth utilization. These instances accrue credits when their network throughput is below their baseline limits, and can use these credits when they perform network data transfers. For workloads that require access to 10 Gbps or higher bandwidth on a sustained basis, we recommend using r4.8xlarge and r4.16xlarge instances, which can utilize up to 10 Gbps and 20 Gbps of network bandwidth, respectively.

Instance Features

The following is a summary of features for memory optimized instances.

VPC only	EBS only	SSD volumes	Placement group	Enhanced networking
R3
Yes
Yes
Intel 82599 VF
R4
Yes
Yes
Yes
ENA
X1	Yes		Yes	Yes	ENA
For more information, see the following:

Instance Types Available Only in a VPC
Amazon EBS–Optimized Instances
Amazon EC2 Instance Store
Placement Groups
Enhanced Networking on Linux
Support for vCPUs

Memory optimized instances provide a high number of vCPUs, which can cause launch issues with operating systems that have a lower vCPU limit. We strongly recommend that you use the latest AMIs when you launch memory optimized instances.

The following AMIs support launching memory optimized instances:

Amazon Linux AMI 2016.03 (HVM) or later
Ubuntu Server 14.04 LTS (HVM)
Red Hat Enterprise Linux 7.1 (HVM)
SUSE Linux Enterprise Server 12 SP1 (HVM)
Windows Server 2016
Windows Server 2012 R2
Windows Server 2012
Windows Server 2008 R2 64-bit
Windows Server 2008 SP2 64-bit
Windows Server 2003 R2 64-bit
Instance Limits

You can't launch X1 instances using a Windows Server 2008 SP2 64-bit AMI or a Windows Server 2003 R2 64-bit AMI, except for x1.16xlarge instances.
With earlier versions of the Windows Server 2008 R2 64-bit AMI, you can't launch r4.large and r4.4xlarge instances. If you experience this issue, update to the latest version of this AMI.
There is a limit on the total number of instances that you can launch in a region, and there are additional limits on some instance types. For more information, see How many instances can I run in Amazon EC2?. To request a limit increase, use the Amazon EC2 Instance Request Form.

Storage Optimized Instances

Storage optimized instances are designed for workloads that require high sequential read and write access to very large data sets on local storage. They are optimized to deliver tens of thousands of low-latency, random I/O operations per second (IOPS) to applications.

D2 Instances

D2 instances are well suited for the following applications:

Massive parallel processing (MPP) data warehouse
MapReduce and Hadoop distributed computing
Log or data processing applications
I2 Instances

I2 instances are well suited for the following applications:

NoSQL databases
Clustered databases
Online transaction processing (OLTP) systems
I3 Instances

I3 instances are well suited for the following applications:

High frequency online transaction processing (OLTP) systems
Relational databases
NoSQL databases
Cache for in-memory databases (for example, Redis)
Data warehousing applications
Low latency Ad-Tech serving applications
Contents

Hardware Specifications
Storage Performance
SSD I/O Performance
Storage Instance Features
Support for vCPUs
Instance Limits
Hardware Specifications

The primary data storage for D2 instances is HDD instance store volumes. The primary data storage for I2 instances is SATA SSD instance store volumes. The primary data storage for I3 instances is non-volatile memory express (NVMe) SSD instance store volumes.

Instance store volumes persist only for the life of the instance. When you stop or terminate an instance, the applications and data in its instance store volumes are erased. We recommend that you regularly back up or replicate important data in your instance store volumes. For more information, see Amazon EC2 Instance Store and SSD Instance Store Volumes.

For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

Storage Performance

To ensure the best disk throughput performance from your instance on Linux, we recommend that you use the most recent version of the Amazon Linux AMI.

For instances with NVMe instance store volumes, you must use a Linux AMI with kernel version 4.4 or later. Otherwise, your instance will not achieve the maximum IOPS performance available.

D2 instances provide the best disk performance when you use a Linux kernel that supports persistent grants, an extension to the Xen block ring protocol that significantly improves disk throughput and scalability. For more information about persistent grants, see this article in the Xen Project Blog.

EBS-optimized instances enable you to get consistently high performance for your EBS volumes by eliminating contention between Amazon EBS I/O and other network traffic from your instance. D2 instances are EBS-optimized by default at no additional cost. You can enable EBS optimization for your I2 instances for an additional low, hourly fee. For more information, see Amazon EBS–Optimized Instances.

You can enable enhanced networking capabilities. Enhanced networking provides significantly higher packet per second (PPS) performance, lower network jitter, and lower latencies. For more information, see Enhanced Networking on Linux.

The d2.8xlarge and i3.16xlarge instance types provides the ability to control processor C-states and P-states on Linux. C-states control the sleep levels that a core can enter when it is inactive, while P-states control the desired performance (in CPU frequency) from a core. For more information, see Processor State Control for Your EC2 Instance.

SSD I/O Performance

If you use a Linux AMI with kernel version 4.4 or later and utilize all the SSD-based instance store volumes available to your instance, you get the IOPS (4,096 byte block size) performance listed in the following table (at queue depth saturation). Otherwise, you'll get lower IOPS performance.

Instance Size	100% Random Read IOPS	Write IOPS
i2.xlarge
35,000
35,000
i2.2xlarge
75,000
75,000
i2.4xlarge
175,000
155,000
i2.8xlarge
365,000
315,000
i3.large *
100,125
9,375
i3.xlarge *
206,250
18,750
i3.2xlarge
412,500
37,500
i3.4xlarge
825,000
75,000
i3.8xlarge
1.65 million
150,000
i3.16xlarge
3.3 million
300,000
* For i3.large and i3.xlarge instances, you can get up to the specified performance.

As you fill the SSD-based instance store volumes for your instance, the number of write IOPS that you can achieve decreases. This is due to the extra work the SSD controller must do to find available space, rewrite existing data, and erase unused space so that it can be rewritten. This process of garbage collection results in internal write amplification to the SSD, expressed as the ratio of SSD write operations to user write operations. This decrease in performance is even larger if the write operations are not in multiples of 4,096 bytes or not aligned to a 4,096-byte boundary. If you write a smaller amount of bytes or bytes that are not aligned, the SSD controller must read the surrounding data and store the result in a new location. This pattern results in significantly increased write amplification, increased latency, and dramatically reduced I/O performance.

SSD controllers can use several strategies to reduce the impact of write amplification. One such strategy is to reserve space in the SSD instance storage so that the controller can more efficiently manage the space available for write operations. This is called over-provisioning. The SSD-based instance store volumes provided to an instance don't have any space reserved for over-provisioning. To reduce write amplification, we recommend that you leave 10% of the volume unpartitioned so that the SSD controller can use it for over-provisioning. This decreases the storage that you can use, but increases performance even if the disk is close to full capacity.

For instance store volumes that support TRIM, you can use the TRIM command to notify the SSD controller whenever you no longer need data that you've written. This provides the controller with more free space, which can reduce write amplification and increase performance. For more information, see Instance Store Volume TRIM Support.

Storage Instance Features

The following is a summary of features for storage optimized instances:

VPC only	SSD volumes	Placement group	Enhanced networking
D2
Yes
Intel 82599 VF
I2
SATA
Yes
Intel 82599 VF
I3
Yes
NVMe
Yes
ENA
For more information, see the following:

Instance Types Available Only in a VPC
Amazon EBS–Optimized Instances
Amazon EC2 Instance Store
Placement Groups
Enhanced Networking on Linux
Support for vCPUs

The d2.8xlarge instance type provides 36 vCPUs, which might cause launch issues in some Linux operating systems that have a vCPU limit of 32. We strongly recommend that you use the latest AMIs when you launch d2.8xlarge instances.

The following Linux AMIs support launching d2.8xlarge instances with 36 vCPUs:

Amazon Linux AMI 2017.03 (HVM)
Ubuntu Server 14.04 LTS (HVM)
Red Hat Enterprise Linux 7.1 (HVM)
SUSE Linux Enterprise Server 12 (HVM)
If you must use a different AMI for your application, and your d2.8xlarge instance launch does not complete successfully (for example, if your instance status changes to stopped during launch with a Client.InstanceInitiatedShutdown state transition reason), modify your instance as described in the following procedure to support more than 32 vCPUs so that you can use the d2.8xlarge instance type.

To update an instance to support more than 32 vCPUs

Launch a D2 instance using your AMI, choosing any D2 instance type other than d2.8xlarge.

Update the kernel to the latest version by following your operating system-specific instructions. For example, for RHEL 6, use the following command:

Copy
sudo yum update -y kernel
Stop the instance.

(Optional) Create an AMI from the instance that you can use to launch any additional d2.8xlarge instances that you need in the future.

Change the instance type of your stopped instance to d2.8xlarge (choose Actions, Instance Settings, Change Instance Type, and then follow the directions).

Start the instance. If the instance launches properly, you are done. If the instance still does not boot properly, proceed to the next step.

(Optional) If the instance still does not boot properly, the kernel on your instance may not support more than 32 vCPUs. However, you may be able to boot the instance if you limit the vCPUs.

Change the instance type of your stopped instance to any D2 instance type other than d2.8xlarge (choose Actions, Instance Settings, Change Instance Type, and then follow the directions).

Add the maxcpus=32 option to your boot kernel parameters by following your operating system-specific instructions. For example, for RHEL 6, edit the /boot/grub/menu.lst file and add the following option to the most recent and active kernel entry:

Copy
default=0
timeout=1
splashimage=(hd0,0)/boot/grub/splash.xpm.gz
hiddenmenu
title Red Hat Enterprise Linux Server (2.6.32-504.3.3.el6.x86_64)
root (hd0,0)
kernel /boot/vmlinuz-2.6.32-504.3.3.el6.x86_64 maxcpus=32 console=ttyS0 ro root=UUID=9996863e-b964-47d3-a33b-3920974fdbd9 rd_NO_LUKS  KEYBOARDTYPE=pc KEYTABLE=us LANG=en_US.UTF-8 xen_blkfront.sda_is_xvda=1 console=ttyS0,115200n8 console=tty0 rd_NO_MD SYSFONT=latarcyrheb-sun16 crashkernel=auto rd_NO_LVM rd_NO_DM
initrd /boot/initramfs-2.6.32-504.3.3.el6.x86_64.img
Stop the instance.

(Optional) Create an AMI from the instance that you can use to launch any additional d2.8xlarge instances that you need in the future.

Change the instance type of your stopped instance to d2.8xlarge (choose Actions, Instance Settings, Change Instance Type, and then follow the directions).

Start the instance.

Instance Limits

You must launch storage optimized instances using an HVM AMI. For more information, see Linux AMI Virtualization Types.
You must launch I3 instances using an Amazon EBS-backed AMI.
The d2.8xlarge instance type has 36 vCPUs, which might cause launch issues in some Linux operating systems that have a vCPU limit of 32. For more information, see Support for vCPUs.
There is a limit on the total number of instances that you can launch in a region, and there are additional limits on some instance types. For more information, see How many instances can I run in Amazon EC2?. To request a limit increase, use the Amazon EC2 Instance Request Form.

Linux Accelerated Computing Instances

If you require high processing capability, you'll benefit from using accelerated computing instances, which provide access to hardware-based compute accelerators such as Graphics Processing Units (GPUs) or Field Programmable Gate Arrays (FPGAs). Accelerated computing instances enable more parallelism for higher throughput on compute-intensive workloads.

GPU-based instances provide access to NVIDIA GPUs with thousands of compute cores. You can use GPU-based accelerated computing instances to accelerate scientific, engineering, and rendering applications by leveraging the CUDA or Open Computing Language (OpenCL) parallel computing frameworks. You can also use them for graphics applications, including game streaming, 3-D application streaming, and other graphics workloads.

FPGA-based instances provide access to large FPGAs with millions of parallel system logic cells. You can use FPGA-based accelerated computing instances to accelerate workloads such as genomics, financial analysis, real-time video processing, big data analysis, and security workloads by leveraging custom hardware accelerations. You can develop these accelerations using hardware description languages such as Verilog or VHDL, or by using higher-level languages such as OpenCL parallel computing frameworks. You can either develop your own hardware acceleration code or purchase hardware accelerations through the AWS Marketplace.

Important
FPGA-based instances do not support Microsoft Windows.
You can cluster accelerated computing instances into a placement group. Placement groups provide low latency and high-bandwidth connectivity between the instances within a single Availability Zone. For more information, see Placement Groups.

Contents

Accelerated Computing Instance Families
Hardware Specifications
Accelerated Computing Instance Limitations
AMIs for GPU-based Accelerated Computing Instances
Installing the NVIDIA Driver on Linux Instances
Activate GRID Workstation Features (G3 Instances Only)
Optimizing GPU Settings (P2 and G3 Instances Only)
Getting Started with FPGA Development
For information about Windows accelerated computing instances, see Windows Accelerated Computing Instances in the Amazon EC2 User Guide for Windows Instances.

Accelerated Computing Instance Families

Accelerated computing instance families use hardware accelerators, or co-processors, to perform some functions, such as floating point number calculations, graphics processing, or data pattern matching, more efficiently than is possible in software running on CPUs. The following accelerated computing instance families are available for you to launch in Amazon EC2.

F1 Instances

F1 instances use Xilinx UltraScale+ VU9P FPGAs and are designed to accelerate computationally intensive algorithms, such as data-flow or highly-parallel operations not suited to general purpose CPUs. Each FPGA in an F1 instance contains approximately 2.5 million logic elements and approximately 6,800 Digital Signal Processing (DSP) engines, along with 64 GiB of local DDR ECC protected memory, connected to the instance by a dedicated PCIe Gen3 x16 connection. F1 instances support enhanced networking with the Elastic Network Adapter (ENA), are EBS-optimized by default, and provide local NVMe SSD volumes.

Developers can use the FPGA Developer AMI and AWS Hardware Developer Kit to create custom hardware accelerations for use on F1 instances. The FPGA Developer AMI includes development tools for full-cycle FPGA development in the cloud. Using these tools, developers can create and share Amazon FPGA Images (AFIs) that can be loaded onto the FPGA of an F1 instance.

For more information, see Amazon EC2 F1 Instances.

P2 Instances

P2 instances use NVIDIA Tesla K80 GPUs and are designed for general purpose GPU computing using the CUDA or OpenCL programming models. P2 instances provide high bandwidth networking, powerful single and double precision floating-point capabilities, and 12 GiB of memory per GPU, which makes them ideal for deep learning, graph databases, high performance databases, computational fluid dynamics, computational finance, seismic analysis, molecular modeling, genomics, rendering, and other server-side GPU compute workloads.

P2 instances support enhanced networking with the Elastic Network Adapter. For more information, see Enabling Enhanced Networking with the Elastic Network Adapter (ENA) on Linux Instances in a VPC.
P2 instances are EBS-optimized by default. For more information, see Amazon EBS–Optimized Instances.
P2 instances support NVIDIA GPUDirect peer to peer transfers. For more information, see NVIDIA GPUDirect.
There are several GPU setting optimizations that you can perform to achieve the best performance on P2 instances. For more information, see Optimizing GPU Settings (P2 and G3 Instances Only) .
The p2.16xlarge instance type provides the ability for an operating system to control processor C-states and P-states. For more information, see Processor State Control for Your EC2 Instance.
G3 Instances

G3 instances use NVIDIA Tesla M60 GPUs and provide a cost-effective, high-performance platform for graphics applications using DirectX or OpenGL. G3 instances also provide NVIDIA GRID Virtual Workstation features, supporting 4 monitors with resolutions up to 4096x2160. Example applications include 3D visualizations, graphics-intensive remote workstations, 3D rendering, video encoding, virtual reality, and other server-side graphics workloads requiring massively parallel processing power.

G3 instances support enhanced networking with the Elastic Network Adapter. For more information, see Enabling Enhanced Networking with the Elastic Network Adapter (ENA) on Linux Instances in a VPC.
G3 instances are EBS-optimized by default. For more information, see Amazon EBS–Optimized Instances.
G3 instances support NVIDIA GRID workstation functionality, but you must activate it. For more information, see Activate GRID Workstation Features (G3 Instances Only).
There are several GPU setting optimizations that you can perform to achieve the best performance on G3 instances. For more information, see Optimizing GPU Settings (P2 and G3 Instances Only) .
The g3.16xlarge instance type provides the ability for an operating system to control processor C-states and P-states. For more information, see Processor State Control for Your EC2 Instance.
G2 Instances

G2 instances use NVIDIA GRID K520 GPUs and provide a cost-effective, high-performance platform for graphics applications using DirectX or OpenGL. NVIDIA GRID GPUs also support NVIDIA’s fast capture and encode API operations. Example applications include video creation services, 3D visualizations, streaming graphics-intensive applications, and other server-side graphics workloads.

CG1 Instances

CG1 instances use NVIDIA Tesla M2050 GPUs and are designed for general purpose GPU computing using the CUDA or OpenCL programming models. CG1 instances provide customers with high bandwidth networking, double precision floating-point capabilities, and error-correcting code (ECC) memory, making them ideal for high performance computing (HPC) applications.

Hardware Specifications

For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

Accelerated Computing Instance Limitations

Accelerated computing instances have the following limitations:

You must launch the instance using an HVM AMI.
GPU-based instances can't access the GPU unless the NVIDIA drivers are installed.
There is a limit of 100 AFIs per region.
There is a limit on the number of instances that you can run. For more information, see How many instances can I run in Amazon EC2? in the Amazon EC2 FAQ. To request an increase in these limits, use the following form: Request to Increase Amazon EC2 Instance Limit.
AMIs for GPU-based Accelerated Computing Instances

To help you get started, NVIDIA provides AMIs for GPU-based accelerated computing instances. These reference AMIs include the NVIDIA driver, which enables full functionality and performance of the NVIDIA GPUs.

For a list of AMIs with the NVIDIA driver, see AWS Marketplace (NVIDIA GRID).

You can launch accelerated computing instances using any HVM AMI.

Installing the NVIDIA Driver on Linux Instances

A GPU-based accelerated computing instance must have the appropriate NVIDIA driver. The NVIDIA driver that you install must be compiled against the kernel that you plan to run on your instance.

Amazon provides AMIs with updated and compatible builds of the NVIDIA kernel drivers for each official kernel upgrade in the AWS Marketplace. If you decide to use a different NVIDIA driver version than the one that Amazon provides, or decide to use a kernel that's not an official Amazon build, you must uninstall the Amazon-provided NVIDIA packages from your system to avoid conflicts with the versions of the drivers that you are trying to install.

Use this command to uninstall Amazon-provided NVIDIA packages:

Copy
sudo yum erase nvidia cuda
The Amazon-provided CUDA toolkit package has dependencies on the NVIDIA drivers. Uninstalling the NVIDIA packages erases the CUDA toolkit. You must reinstall the CUDA toolkit after installing the NVIDIA driver.

Obtaining the NVIDIA Driver

For G3 instances, you can download the driver from Amazon S3 using the AWS CLI or SDKs. To install the AWS CLI, see Installing the AWS Command Line Interface in the AWS Command Line Interface User Guide. Use the following AWS CLI command to download the driver:

Important
This download is available to AWS customers only. By downloading, you agree that you will only use the downloaded software to develop AMIs for use with the NVIDIA Tesla M60 hardware. Upon installation of the software, you will be bound by the terms of the NVIDIA GRID Cloud End User License Agreement.
Copy
aws s3 cp --recursive s3://ec2-linux-nvidia-drivers/ .
Note
If you receive an Unable to locate credentials error, see Configuring the AWS CLI to configure the AWS CLI to use your AWS credentials.
For P2, G2, and CG1 instances, you can download NVIDIA drivers from http://www.nvidia.com/Download/Find.aspx. Select the appropriate driver for your instance:

P2 Instances

Product Type	Tesla
Product Series	K-Series
Product	K-80
Operating System	Linux 64-bit
Recommended/Beta	Recommended/Certified
G2 Instances

Product Type	GRID
Product Series	GRID Series
Product	GRID K520
Operating System	Linux 64-bit
Recommended/Beta	Recommended/Certified
CG1 Instances

Product Type	Tesla
Product Series	M-Class
Product	M2050
Operating System	Linux 64-bit
Recommended/Beta	Recommended/Certified
For more information about installing and configuring the driver, choose the ADDITIONAL INFORMATION tab on the download page for the driver on the NVIDIA website and choose the README link.

Installing the NVIDIA Driver Manually

To install the driver on a Linux instance

Update your package cache and get necessary package updates for your instance.

For Amazon Linux, CentOS, and Red Hat Enterprise Linux:
Copy
sudo yum update -y
For Ubuntu and Debian:
Copy
sudo apt-get update -y
(Ubuntu 16.04 and later, with the linux-aws package) Upgrade the linux-aws package to receive the latest version.

Copy
sudo apt-get upgrade -y linux-aws
Reboot your instance to load the latest kernel version.

Copy
sudo reboot
Reconnect to your instance after it has rebooted.

Install the gcc compiler and the kernel headers package for the version of the kernel you are currently running.

For Amazon Linux, CentOS, and Red Hat Enterprise Linux:
Copy
sudo yum install -y gcc kernel-devel-$(uname -r)
For Ubuntu and Debian:
Copy
sudo apt-get install -y gcc linux-headers-$(uname -r)
(Graphical instances only) Disable the nouveau open source driver for NVIDIA graphics cards.

Add nouveau to the modprobe blacklist file. Copy the following code block and paste it into a terminal.

Copy
cat << EOF | sudo tee --append /etc/modprobe.d/blacklist.conf
blacklist vga16fb
blacklist nouveau
blacklist rivafb
blacklist nvidiafb
blacklist rivatv
EOF
Edit /etc/default/grub and add the following text to the GRUB_CMDLINE_LINUX line:

Copy
modprobe.blacklist=nouveau
Rebuild the Grub configuration.

CentOS and Red Hat Enterprise Linux:
Copy
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
For Ubuntu and Debian:
Copy
sudo update-grub
Download the driver package that you identified earlier. For P2 instances, the following command downloads the 375.66 version of the NVIDIA driver.

Copy
wget http://us.download.nvidia.com/XFree86/Linux-x86_64/375.66/NVIDIA-Linux-x86_64-375.66.run
For G3 instances, you can download the driver from Amazon S3 using the AWS CLI or SDKs. To install the AWS CLI, see Installing the AWS Command Line Interface in the AWS Command Line Interface User Guide. Use the following AWS CLI command to download the driver and the NVIDIA GRID Cloud End User License Agreement:

Important
This download is available to AWS customers only. By downloading, you agree that you will only use the downloaded software to develop AMIs for use with the NVIDIA Tesla M60 hardware. Upon installation of the software, you will be bound by the terms of the NVIDIA GRID Cloud End User License Agreement.
Copy
aws s3 cp --recursive s3://ec2-linux-nvidia-drivers/ .
Run the self-install script to install the NVIDIA driver that you downloaded in the previous step. For example:

Copy
sudo /bin/bash ./NVIDIA-Linux-x86_64-375.66.run
Reboot the instance.

Copy
sudo reboot
Confirm that the driver is functional. The response for the following command lists the installed NVIDIA driver version and details about the GPUs.

Note
This command may take several minutes to run.
Copy
nvidia-smi -q | head
(G3 instances only) If you are using a G3 instance, complete the GRID activation steps in Activate GRID Workstation Features (G3 Instances Only)

(P2 and G3 instances only) If you are using a P2 or G3 instance, complete the optimization steps in Optimizing GPU Settings (P2 and G3 Instances Only) to achieve the best performance from your GPU.

Activate GRID Workstation Features (G3 Instances Only)

To activate the GRID features on G3 instances, you must define the product type for the driver in the /etc/nvidia/gridd.conf file.

To activate GRID features on G3 Linux instances

Create the /etc/nvidia/gridd.conf file from the provided template file.

Copy
sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
Open the /etc/nvidia/gridd.conf file in your favorite text editor.

Find the FeatureType line, and set it equal to 2.

Copy
FeatureType=2
Save the file and exit.

Restart the nvidia-gridd licensing daemon to pick up the new configuration.

Copy
sudo service nvidia-gridd restart
Optimizing GPU Settings (P2 and G3 Instances Only)

There are several GPU setting optimizations that you can perform to achieve the best performance on P2 and G3 instances. By default, the NVIDIA driver uses an autoboost feature, which varies the GPU clock speeds. By disabling the autoboost feature and setting the GPU clock speeds to their maximum frequency, you can consistently achieve the maximum performance with your P2 and G3 instances. The following procedure helps you to configure the GPU settings to be persistent, disable the autoboost feature, and set the GPU clock speeds to their maximum frequency.

To optimize P2 or G3 GPU settings

Configure the GPU settings to be persistent.

Note
This command may take several minutes to run.
Copy
sudo nvidia-smi -pm 1
Disable the autoboost feature for all GPUs on the instance.

Copy
sudo nvidia-smi --auto-boost-default=0
Set all GPU clock speeds to their maximum frequency. Use the memory and graphics clock speeds listed below, based on your instance type.

For P2 instances: 2505,875
For G3 instances: 2505,1177
Copy
sudo nvidia-smi -ac 2505,1177
Getting Started with FPGA Development

The FPGA Developer AMI provides the tools you need to develop, test, and build AFIs. You can use the FPGA Developer AMI on any EC2 instance with at least 32 GB of system memory (for example, C4 instances).

For more information, see the documentation for the AWS FPGA Hardware Development Kit.

T1 Micro Instances

T1 Micro instances (t1.micro) provide a small amount of consistent CPU resources and allow you to increase CPU capacity in short bursts when additional cycles are available. They are well suited for lower throughput applications and websites that require additional compute cycles periodically.

Note
The t1.micro is a previous generation instance and it has been replaced by the t2.micro, which has a much better performance profile. We recommend using the t2.micro instance type instead of the t1.micro. For more information, see T2 Instances.
The t1.micro instance is available as an Amazon EBS-backed instance only.

This documentation describes how t1.micro instances work so that you can understand how to apply them. It's not our intent to specify exact behavior, but to give you visibility into the instance's behavior so you can understand its performance.

Topics

Hardware Specifications
Optimal Application of T1 Micro Instances
Available CPU Resources During Spikes
When the Instance Uses Its Allotted Resources
Comparison with the m1.small Instance Type
AMI Optimization for Micro Instances
Hardware Specifications

For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

Optimal Application of T1 Micro Instances

A t1.micro instance provides spiky CPU resources for workloads that have a CPU usage profile similar to what is shown in the following figure.


				Good fit
			
The instance is designed to operate with its CPU usage at essentially only two levels: the normal low background level, and then at brief spiked levels much higher than the background level. We allow the instance to operate at up to 2 EC2 compute units (ECUs) (one ECU provides the equivalent CPU capacity of a 1.0-1.2 GHz 2007 Opteron or 2007 Xeon processor). The ratio between the maximum level and the background level is designed to be large. We designed t1.micro instances to support tens of requests per minute on your application. However, actual performance can vary significantly depending on the amount of CPU resources required for each request on your application.

Your application might have a different CPU usage profile than that described in the preceding section. The following figure shows the profile for an application that isn't appropriate for a t1.micro instance. The application requires continuous data-crunching CPU resources for each request, resulting in plateaus of CPU usage that the t1.micro instance isn't designed to handle.


				Bad fit: Plateaus
			
The following figure shows another profile that isn't appropriate for a t1.micro instance. Here the spikes in CPU use are brief, but they occur too frequently to be serviced by a micro instance.


				Bad fit: Too frequent
			
The following figure shows another profile that isn't appropriate for a t1.micro instance. Here the spikes aren't too frequent, but the background level between spikes is too high to be serviced by a t1.micro instance.


				Bad fit: Background too high
			
In each of the preceding cases of workloads not appropriate for a t1.micro instance, we recommend that you consider using a different instance type. For more information about instance types, see Instance Types.

Available CPU Resources During Spikes

When your instance bursts to accommodate a spike in demand for compute resources, it uses unused resources on the host. The amount available depends on how much contention there is when the spike occurs. The instance is never left with zero CPU resources, whether other instances on the host are spiking or not.

When the Instance Uses Its Allotted Resources

We expect your application to consume only a certain amount of CPU resources in a period of time. If the application consumes more than your instance's allotted CPU resources, we temporarily limit the instance so it operates at a low CPU level. If your instance continues to use all of its allotted resources, its performance will degrade. We will increase the time that we limit its CPU level, thus increasing the time before the instance is allowed to burst again.

If you enable CloudWatch monitoring for your t1.micro instance, you can use the "Avg CPU Utilization" graph in the AWS Management Console to determine whether your instance is regularly using all its allotted CPU resources. We recommend that you look at the maximum value reached during each given period. If the maximum value is 100%, we recommend that you use Auto Scaling to scale out (with additional t1.micro instances and a load balancer), or move to a larger instance type. For more information, see the Auto Scaling User Guide.

Consider the three suboptimal profiles from the preceding section and what it might look like when the instance consumes its allotted resources and we limit its CPU level. If an instance consumes its allotted resources, we restrict it to the low background level. The following figure shows long plateaus of data-crunching CPU usage. The CPU hits the maximum allowed level and stays there until the instance's allotted resources are consumed for the period. At that point, we limit the instance to operate at the low background level, and it operates there until we allow it to burst above that level again. The instance again stays there until the allotted resources are consumed and we limit it again (not seen on the graph).


				Bad fit: Too wide; limited
			
The following figure shows requests that are too frequent. The instance uses its allotted resources after only a few requests and so we limit it. After we lift the restriction, the instance maxes out its CPU usage trying to keep up with the requests, and we limit it again.


				Bad fit: Too frequent; limited
			
The following figure shows a background level that is too high. Notice that the instance doesn't have to be operating at the maximum CPU level for us to limit it. We limit the instance when it's operating above the normal background level and has consumed its allotted resources for the given period. In this case (as in the preceding one), the instance can't keep up with the work, and we limit it again.


				Bad fit: Background too high; limited
			
Comparison with the m1.small Instance Type

The t1.micro instance provides different levels of CPU resources at different times (up to 2 ECUs). By comparison, the m1.small instance type provides 1 ECU at all times. The following figure illustrates the difference.


				General comparison with m1.small
			
Let's compare the CPU usage of a t1.micro instance with an m1.small instance for the various scenarios we've discussed in the preceding sections. The following figure that follows shows an optimal scenario for a t1.micro instance (the left graph) and how it might look for an m1.small instance (the right graph). In this case, we don't need to limit the t1.micro instance. The processing time on the m1.small instance would be longer for each spike in CPU demand compared to the t1.micro instance.


				Comparison with m1.small: optimal situation
			
The following figure shows the scenario with the data-crunching requests that used up the allotted resources on the t1.micro instance, and how they might look with the m1.small instance.


				Comparison with m1.small: too wide plateaus
			
The following figure shows the frequent requests that used up the allotted resources on the t1.micro instance, and how they might look on the m1.small instance.


				Comparison with m1.small: too frequent
			
The following figure shows the situation where the background level used up the allotted resources on the t1.micro instance, and how it might look on the m1.small instance.


				Comparison with m1.small: background too high
			
AMI Optimization for Micro Instances

We recommend that you follow these best practices when optimizing an AMI for the t1.micro instance type:

Design the AMI to run on 600 MB of RAM
Limit the number of recurring processes that use CPU time (for example, cron jobs, daemons)
You can optimize performance using swap space and virtual memory (for example, by setting up swap space in a separate partition from the root file system).

Resizing Your Instance

As your needs change, you might find that your instance is over-utilized (the instance type is too small) or under-utilized (the instance type is too large). If this is the case, you can change the size of your instance. For example, if your t2.micro instance is too small for its workload, you can change it to an m3.medium instance.

If the root device for your instance is an EBS volume, you can change the size of the instance simply by changing its instance type, which is known as resizing it. If the root device for your instance is an instance store volume, you must migrate your application to a new instance with the instance type that you need. For more information about root device volumes, see Storage for the Root Device.

When you resize an instance, you must select an instance type that is compatible with the configuration of the instance. If the instance type that you want is not compatible with the instance configuration you have, then you must migrate your application to a new instance with the instance type that you need.

Important
When you resize an instance, the resized instance usually has the same number of instance store volumes that you specified when you launched the original instance. If you want to add instance store volumes, you must migrate your application to a new instance with the instance type and instance store volumes that you need. An exception to this rule is when you resize to a storage-optimized instance type that by default contains a higher number of volumes. For more information about instance store volumes, see Amazon EC2 Instance Store.
Contents

Compatibility for Resizing Instances
Resizing an Amazon EBS–backed Instance
Migrating an Instance Store-backed Instance
Migrating to a New Instance Configuration
Compatibility for Resizing Instances

You can resize an instance only if its current instance type and the new instance type that you want are compatible in the following ways:

Virtualization type. Linux AMIs use one of two types of virtualization: paravirtual (PV) or hardware virtual machine (HVM). You can't resize an instance that was launched from a PV AMI to an instance type that is HVM only. For more information, see Linux AMI Virtualization Types. To check the virtualization type of your instance, see the Virtualization field on the details pane of the Instances screen in the Amazon EC2 console.
Network. Some instance types are not supported in EC2-Classic and must be launched in a VPC. Therefore, you can't resize an instance in EC2-Classic to a instance type that is available only in a VPC unless you have a nondefault VPC. For more information, see Instance Types Available Only in a VPC. To check if your instance is in a VPC, check the VPC ID value on the details pane of the Instances screen in the Amazon EC2 console.
Platform. All Amazon EC2 instance types support 64-bit AMIs, but only the following instance types support 32-bit AMIs: t2.nano, t2.micro, t2.small, t2.medium, c3.large, t1.micro, m1.small, m1.medium, and c1.medium. If you are resizing a 32-bit instance, you are limited to these instance types. To check the platform of your instance, go to the Instances screen in the Amazon EC2 console and choose Show/Hide Columns, Architecture.
For example, T2 instances are not supported in EC2-Classic and they are HVM only. On Linux, T1 instances do not support HVM and must be launched from PV AMIs. Therefore, you can't resize a T1 Linux instance to a T2 Linux instance.

Resizing an Amazon EBS–backed Instance

You must stop your Amazon EBS–backed instance before you can change its instance type. When you stop and start an instance, be aware of the following:

We move the instance to new hardware; however, the instance ID does not change.
If your instance is running in a VPC and has a public IPv4 address, we release the address and give it a new public IPv4 address. The instance retains its private IPv4 addresses, any Elastic IP addresses, and any IPv6 addresses.
If your instance is running in EC2-Classic, we give it new public and private IP addresses, and disassociate any Elastic IP address that's associated with the instance. Therefore, to ensure that your users can continue to use the applications that you're hosting on your instance uninterrupted, you must re-associate any Elastic IP address after you restart your instance.
If your instance is in an Auto Scaling group, the Auto Scaling service marks the stopped instance as unhealthy, and may terminate it and launch a replacement instance. To prevent this, you can suspend the Auto Scaling processes for the group while you're resizing your instance. For more information, see Suspend and Resume Auto Scaling Processes in the Auto Scaling User Guide.
Ensure that you plan for downtime while your instance is stopped. Stopping and resizing an instance may take a few minutes, and restarting your instance may take a variable amount of time depending on your application's startup scripts.
For more information, see Stop and Start Your Instance.

Use the following procedure to resize an Amazon EBS–backed instance using the AWS Management Console.

To resize an Amazon EBS–backed instance

Open the Amazon EC2 console.

In the navigation pane, choose Instances, and select the instance.

[EC2-Classic] If the instance has an associated Elastic IP address, write down the Elastic IP address and the instance ID shown in the details pane.

Choose Actions, select Instance State, and then choose Stop.

In the confirmation dialog box, choose Yes, Stop. It can take a few minutes for the instance to stop.

[EC2-Classic] When the instance state becomes stopped, the Elastic IP, Public DNS (IPv4), Private DNS, and Private IPs fields in the details pane are blank to indicate that the old values are no longer associated with the instance.

With the instance still selected, choose Actions, select Instance Settings, and then choose Change Instance Type. Note that this action is disabled if the instance state is not stopped.

In the Change Instance Type dialog box, do the following:

From Instance Type, select the instance type that you want. If the instance type that you want does not appear in the list, then it is not compatible with the configuration of your instance (for example, because of virtualization type).

(Optional) If the instance type that you selected supports EBS–optimization, select EBS-optimized to enable EBS–optimization or deselect EBS-optimized to disable EBS–optimization. Note that if the instance type that you selected is EBS–optimized by default, EBS-optimized is selected and you can't deselect it.

Choose Apply to accept the new settings.

To restart the stopped instance, select the instance, choose Actions, select Instance State, and then choose Start.

In the confirmation dialog box, choose Yes, Start. It can take a few minutes for the instance to enter the running state.

[EC2-Classic] When the instance state is running, the Public DNS (IPv4), Private DNS, and Private IPs fields in the details pane contain the new values that we assigned to the instance. If your instance had an associated Elastic IP address, you must reassociate it as follows:

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address that you wrote down before you stopped the instance.

Choose Actions and then choose Associate address.

From Instance, select the instance ID that you wrote down before you stopped the instance, and then choose Associate.

Migrating an Instance Store-backed Instance

When you want to move your application from one instance store-backed instance to an instance store-backed instance with a different instance type, you must migrate it by creating an image from your instance, and then launching a new instance from this image with the instance type that you need. To ensure that your users can continue to use the applications that you're hosting on your instance uninterrupted, you must take any Elastic IP address that you've associated with your original instance and associate it with the new instance. Then you can terminate the original instance.

To migrate an instance store-backed instance

[EC2-Classic] If the instance you are migrating has an associated Elastic IP address, record the Elastic IP address now so that you can associate it with the new instance later.

Back up any data on your instance store volumes that you need to keep to persistent storage. To migrate data on your EBS volumes that you need to keep, take a snapshot of the volumes (see Creating an Amazon EBS Snapshot) or detach the volume from the instance so that you can attach it to the new instance later (see Detaching an Amazon EBS Volume from an Instance).

Create an AMI from your instance store-backed instance by satisfying the prerequisites and following the procedures in Creating an Instance Store-Backed Linux AMI. When you are finished creating an AMI from your instance, return to this procedure.

Open the Amazon EC2 console and in the navigation pane, select AMIs. From the filter lists, select Owned by me, and select the image that you created in the previous step. Notice that AMI Name is the name that you specified when you registered the image and Source is your Amazon S3 bucket.

Note
If you do not see the AMI that you created in the previous step, make sure that you have selected the region in which you created your AMI.
Choose Launch. When you specify options for the instance, be sure to select the new instance type that you want. If the instance type that you want can't be selected, then it is not compatible with configuration of the AMI that you created (for example, because of virtualization type). You can also specify any EBS volumes that you detached from the original instance.

Note that it can take a few minutes for the instance to enter the running state.

[EC2-Classic] If the instance that you started with had an associated Elastic IP address, you must associate it with the new instance as follows:

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address that you recorded at the beginning of this procedure.

Choose Actions and then choose Associate Address.

From Instance, select the new instance, and then choose Associate.

(Optional) You can terminate the instance that you started with, if it's no longer needed. Select the instance and verify that you are about to terminate the original instance, not the new instance (for example, check the name or launch time). Choose Actions, select Instance State, and then choose Terminate.

Migrating to a New Instance Configuration

If the current configuration of your instance is incompatible with the new instance type that you want, then you can't resize the instance to that instance type. Instead, you can migrate your application to a new instance with a configuration that is compatible with the new instance type that you want.

If you want to move from an instance launched from a PV AMI to an instance type that is HVM only, the general process is as follows:

Back up any data on your instance store volumes that you need to keep to persistent storage. To migrate data on your EBS volumes that you need to keep, create a snapshot of the volumes (see Creating an Amazon EBS Snapshot) or detach the volume from the instance so that you can attach it to the new instance later (see Detaching an Amazon EBS Volume from an Instance).

Launch a new instance, selecting the following:

An HVM AMI.
The HVM only instance type.
[EC2-VPC] If you are using an Elastic IP address, select the VPC that the original instance is currently running in.
Any EBS volumes that you detached from the original instance and want to attach to the new instance, or new EBS volumes based on the snapshots that you created.
If you want to allow the same traffic to reach the new instance, select the security group that is associated with the original instance.
Install your application and any required software on the instance.

Restore any data that you backed up from the instance store volumes of the original instance.

If you are using an Elastic IP address, assign it to the newly launched instance as follows:

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address that is associated with the original instance, choose Actions, and then choose Disassociate address. When prompted for confirmation, choose Disassociate address.

With the Elastic IP address still selected, choose Actions, and then choose Associate address.

From Instance, select the new instance, and then choose Associate.

(Optional) You can terminate the original instance if it's no longer needed. Select the instance and verify that you are about to terminate the original instance, not the new instance (for example, check the name or launch time). Choose Actions, select Instance State, and then choose Terminate.

For information about migrating an application from an instance in EC2-Classic to an instance in a VPC, see Migrating from a Linux Instance in EC2-Classic to a Linux Instance in a VPC.

Instance Purchasing Options

Amazon EC2 provides the following purchasing options to enable you to optimize your costs based on your needs:

On-Demand instances — Pay, by the hour, for the instances that you launch.
Reserved Instances — Purchase, at a significant discount, instances that are always available, for a term from one to three years.
Scheduled Instances — Purchase instances that are always available on the specified recurring schedule, for a one-year term.
Spot instances — Bid on unused instances, which can run as long as they are available and your bid is above the Spot price, at a significant discount.
Dedicated hosts — Pay for a physical host that is fully dedicated to running your instances, and bring your existing per-socket, per-core, or per-VM software licenses to reduce costs.
Dedicated instances — Pay, by the hour, for instances that run on single-tenant hardware.
If you require a capacity reservation, purchase Reserved Instances for a specific Availability Zone or purchase Scheduled Instances. Spot instances are a cost-effective choice if you can be flexible about when your applications run and if they can be interrupted. Dedicated hosts can help you address compliance requirements and reduce costs by using your existing server-bound software licenses. For more information, see Amazon EC2 Instance Purchasing Options.

Contents

Determining the Instance Lifecycle
Reserved Instances
Scheduled Reserved Instances
Spot Instances
Dedicated Hosts
Dedicated Instances
Determining the Instance Lifecycle

The lifecycle of an instance starts when it is launched and ends when it is terminated. The purchasing option that you choose effects the lifecycle of the instance. For example, an On-Demand instance runs when you launch it and ends when you terminate it. A Spot instance runs as long as its capacity is available and your bid price is higher than the Spot price. You can launch a Scheduled Instance during its scheduled time period; Amazon EC2 launches the instances and then terminates them three minutes before the time period ends.

Use the following procedure to determine the lifecycle of an instance.

To determine the instance lifecycle using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance.

On the Description tab, find Tenancy. If the value is host, the instance is running on a Dedicated Host. If the value is dedicated, the instance is a Dedicated Instance.

On the Description tab, find Lifecycle. If the value is spot, the instance is a Spot instance. If the value is scheduled, the instance is a Scheduled Instance. If the value is normal, the instance is either an On-Demand instance or a Reserved Instance.

(Optional) If you have purchased a Reserved Instance and want to verify that it is being applied, you can check the usage reports for Amazon EC2. For more information, see Reserved Instance Utilization Reports.

To determine the instance lifecycle using the AWS CLI

Use the following describe-instances command:

Copy
aws ec2 describe-instances --instance-ids i-1234567890abcdef0
If the instance is running on a Dedicated host, the output contains the following information:

"Tenancy": "host"
If the instance is a Dedicated instance, the output contains the following information:

"Tenancy": "dedicated"
If the instance is a Spot instance, the output contains the following information:

"InstanceLifecycle": "spot"
If the instance is a Scheduled Instance, the output contains the following information:

"InstanceLifecycle": "scheduled"
Otherwise, the output contains the following information:

"InstanceLifecycle": "normal"

Reserved Instances

Reserved Instances provide you with a significant discount compared to On-Demand Instance pricing. Reserved Instances are not physical instances, but rather a billing discount applied to the use of On-Demand Instances in your account. These On-Demand Instances must match certain attributes in order to benefit from the billing discount.

The following diagram shows a basic overview of purchasing and using Reserved Instances.


			Purchasing Reserved Instances
		
In this scenario, you have a running On-Demand Instance (T2) in your account, for which you're currently paying On-Demand rates. You purchase a Reserved Instance that matches the attributes of your running instance, and the billing benefit is immediately applied. Next, you purchase a Reserved Instance for a C4 instance. You do not have any running instances in your account that match the attributes of this Reserved Instance. In the final step, you launch an instance that matches the attributes of the C4 Reserved Instance, and the billing benefit is immediately applied.

When you purchase a Reserved Instance, choose a combination of the following that suits yor needs:

Payment option: No Upfront, Partial Upfront, or All Upfront.
Term: One-year or three-year. A year is defined as 31536000 seconds (365 days). Three years is defined as 94608000 seconds (1095 days).
Offering class: Convertible or Standard.
In addition, a Reserved Instance has a number of attributes that determine how it is applied to a running instance in your account:

Instance type: For example, m4.large. This is composed of the instance family (m4) and the instance size (large).
Scope: Whether the Reserved Instance applies to a region or specific Availability Zone.
Tenancy: Whether your instance runs on shared (default) or single-tenant (dedicated) hardware. For more information, see Dedicated Instances.
Platform: The operating system; for example, Windows or Linux/Unix.
Reserved Instances do not renew automatically; when they expire, you can continue using the EC2 instance without interruption, but you are charged On-Demand rates. In the above example, when the Reserved Instances that cover the T2 and C4 instances expire, you go back to paying the On-Demand rates until you terminate the instances or purchase new Reserved Instances that match the instance attributes.

After you purchase a Reserved Instance, you cannot cancel your purchase. However, you may be able to modify, exchange, or sell your Reserved Instance if your needs change.

Payment Options

The following payment options are available for Reserved Instances.

No Upfront—You are billed a discounted hourly rate for every hour within the term, regardless of whether the Reserved Instance is being used. No upfront payment is required. This option is only available as a 1-year reservation for Standard Reserved Instances and a 3-year reservation for Convertible Reserved Instances.
Note
No Upfront Reserved Instances are based on a contractual obligation to pay monthly for the entire term of the reservation. For this reason, a successful billing history is required before you can purchase No Upfront Reserved Instances.
Partial Upfront—A portion of the cost must be paid upfront and the remaining hours in the term are billed at a discounted hourly rate, regardless of whether the Reserved Instance is being used.
All Upfront—Full payment is made at the start of the term, with no other costs or additional hourly charges incurred for the remainder of the term, regardless of hours used.
Generally speaking, you can save more money choosing Reserved Instances with a higher upfront payment. You can also find Reserved Instances offered by third-party sellers at lower prices and shorter term lengths on the Reserved Instance Marketplace. For more information, see Selling on the Reserved Instance Marketplace.

For more information about pricing, see Amazon EC2 Reserved Instances Pricing.

Using Reserved Instances in a VPC

If your account supports EC2-Classic, you can purchase Reserved Instances for use in either EC2-Classic or a VPC. You can purchase Reserved Instances to apply to instances launched into a VPC by selecting a platform that includes Amazon VPC in its name.

If you have an EC2-VPC-only account, the listed platforms available do not include Amazon VPC in its name because all instances must be launched into a VPC.

For more information, see Detecting Your Supported Platforms and Whether You Have a Default VPC.

Reserved Instance Limits

You are limited to purchasing 20 Reserved Instances per Availability Zone, per month, plus 20 regional Reserved Instances. Therefore, in a region that has three Availability Zones, you can purchase 80 Reserved Instances in total: 20 per Availability Zone (60) plus 20 regional Reserved Instances.

Reserved Instances that are purchased for a specific Availability Zone (zonal Reserved Instances) allow you to launch as many instances that are covered by the zonal Reserved Instances, even if this results in you exceeding your On-Demand Instance limit. For example, your running On-Demand Instance limit is 20, and you are currently running 18 On-Demand Instances. You have five unused zonal Reserved Instances. You can launch two more On-Demand Instances with any specifications, and you can launch five instances that exactly match the specifications of your zonal Reserved Instances; giving you a total of 25 instances.

Regional Reserved Instances do not increase your On-Demand Instance limit.

Types of Reserved Instances (Offering Classes)

When you purchase a Reserved Instance, you can choose between a Standard or Convertible offering class. The Reserved Instance applies to a single instance family, platform, scope, and tenancy over a term. If your computing needs change, you may be able to modify or exchange your Reserved Instance, depending on the offering class. Offering classes may also have additional restrictions or limitations.

The following are the differences between Standard and Convertible offering classes.


Standard Reserved Instance	Convertible Reserved Instance
Can be purchased for a one-year or three-year term.	Can be purchased for a three-year term only.
Some attributes, such as instance size, can be modified during the term; however, the instance type cannot be modified. You cannot exchange a Standard Reserved Instance, only modify it. For more information, see Modifying Standard Reserved Instances.	Can be exchanged during the term for another Convertible Reserved Instance with new attributes including instance family, instance type, platform, scope, or tenancy. You cannot modify the attributes of a Convertible Reserved Instance. You can only exchange it for a different one. For more information, see Exchanging Convertible Reserved Instances.
Can be sold in the Reserved Instance Marketplace.	Cannot be sold in the Reserved Instance Marketplace.
Standard and Convertible Reserved Instances can be purchased to apply to instances in a specific Availability Zone, or to instances in a region. When you purchase a Reserved Instance in a specific Availability Zone, it provides a capacity reservation. When you purchase a Reserved Instance for a region, it's referred to as a regional Reserved Instance. Regional Reserved Instances do not provide a capacity reservation.

Regional Reserved Instances have the following attributes:

Availability Zone flexibility: the Reserved Instance discount applies to instance usage in any Availability Zone in a region.
Instance size flexibility: the Reserved Instance discount applies to instance usage regardless of size, within that instance family. Only supported on Linux/Unix Reserved Instances with default tenancy.
For more information and examples, see How Reserved Instances Are Applied.

If you want to purchase capacity reservations that recur on a daily, weekly, or monthly basis, a Scheduled Reserved Instance may meet your needs. For more information, see Scheduled Reserved Instances.

How Reserved Instances Are Applied

If you purchase a Reserved Instance and you already have a running instance that matches the specifications of the Reserved Instance, the billing benefit is immediately applied. You do not have to restart your instances. If you do not have a suitable running instance, launch an instance and ensure that you match the same criteria that you specified for your Reserved Instance. For more information, see Using Your Reserved Instances.

Reserved Instances apply to usage in the same manner, irrespective of the offering type (Standard or Convertible), and are automatically applied to running On-Demand Instances with matching attributes.

How Zonal Reserved Instances Are Applied

Reserved Instances assigned to a specific Availability Zone provide the Reserved Instance discount to matching instance usage in that Availability Zone. For example, if you purchase two c4.xlarge default tenancy Linux/Unix Standard Reserved Instances in Availability Zone us-east-1a, then up to two c4.xlarge default tenancy Linux/Unix instances running in the Availability Zone us-east-1a can benefit from the Reserved Instance discount. The attributes (tenancy, platform, Availability Zone, instance type, and instance size) of the running instances must match that of the Reserved Instances.

How Regional Reserved Instances Are Applied

Reserved Instances purchased for a region (regional Reserved Instances) provide Availability Zone flexibility—the Reserved Instance discount applies to instance usage in any Availability Zone in that region.

Regional Reserved Instances on the Linux/Unix platform with default tenancy also provide instance size flexibility, where the Reserved Instance discount applies to instance usage within that instance type, regardless of size.

Note
Instance size flexibility does not apply to Reserved Instances that are purchased for a specific Availability Zone, and does not apply to Windows, Windows with SQL Standard, Windows with SQL Server Enterprise, Windows with SQL Server Web, RHEL, and SLES Reserved Instances.
Instance size flexibility is determined by the normalization factor of the instance size. The discount applies either fully or partially to running instances of the same instance type, depending on the instance size of the reservation, in any Availability Zone in the region. The only attributes that must be matched are the instance type, tenancy, and platform.

The table below describes the different sizes within an instance type, and corresponding normalization factor per hour. This scale is used to apply the discounted rate of Reserved Instances to the normalized usage of the instance type.


Instance size	Normalization factor
nano
0.25
micro
0.5
small
1
medium
2
large
4
xlarge
8
2xlarge
16
4xlarge
32
8xlarge
64
10xlarge
80
32xlarge
256
For example, a t2.medium instance has a normalization factor of 2. If you purchase a t2.medium default tenancy Amazon Linux/Unix Reserved Instance in the US East (N. Virginia) and you have two running t2.small instances in your account in that region, the billing benefit is applied in full to both instances.


					Applying a Regional Reserved Instance
				
Or, if you have one t2.large instance running in your account in the US East (N. Virginia) region, the billing benefit is applied to 50% of the usage of the instance.


					Applying a Regional Reserved Instance
				
Note
The normalization factor is also applied when modifying Standard Reserved Instances. For more information, see Modifying Standard Reserved Instances.
Examples of Applying Reserved Instances

The following scenarios cover the ways in which Reserved Instances are applied.

Example Scenario 1: Reserved Instances in a Single Account

You are running the following On-Demand Instances in account A:

4 x m3.large Linux, default tenancy instances in Availability Zone us-east-1a
2 x m4.xlarge Amazon Linux, default tenancy instances in Availability Zone us-east-1b
1 x c4.xlarge Amazon Linux, default tenancy instances in Availability Zone us-east-1c
You purchase the following Reserved Instances in account A:

4 x m3.large Linux, default tenancy Reserved Instances in Availability Zone us-east-1a (capacity is reserved)
4 x m4.large Amazon Linux, default tenancy Reserved Instances in us-east-1
1 x c4.large Amazon Linux, default tenancy Reserved Instances in us-east-1
The Reserved Instance benefits are applied in the following way:

The discount and capacity reservation of the four m3.large Reserved Instances is used by the four m3.large instances because the attributes (instance size, region, platform, tenancy) between them match.
The m4.large Reserved Instances provide Availability Zone and instance size flexibility, because they are regional Amazon Linux Reserved Instances with default tenancy.
An m4.large is equivalent to 4 normalized units/hour.
You've purchased four m4.large Reserved Instances, and in total, they are equal to 16 normalized units/hour (4x4). Account A has two m4.xlarge instances running, which is equivalent to 16 normalized units/hour (2x8). In this case, the four m4.large Reserved Instances provide the billing benefit to an entire hour of usage of the two m4.xlarge instances.
The c4.large Reserved Instance in us-east-1 provides Availability Zone and instance size flexibility, because it is an Amazon Linux Reserved Instance with default tenancy, and applies to the c4.xlarge instance. A c4.large instance is equivalent to 4 normalized units/hour and a c4.xlarge is equivalent to 8 normalized units/hour.
In this case, the c4.large Reserved Instance provides partial benefit to c4.xlarge usage. This is because the c4.large Reserved Instance is equivalent to 4 normalized units/hour of usage, but the c4.xlarge instance requires 8 normalized units/hour. Therefore, the c4.large Reserved Instance billing discount applies to 50% of c4.xlarge usage. The remaining c4.xlarge usage is charged at the On-Demand rate.
Example Scenario 2: Regional Reserved Instances in Linked Accounts

Reserved Instances are first applied to usage within the purchasing account, followed by qualifying usage in any other account in the organization. For more information, see Reserved Instances and Consolidated Billing. For regional Reserved Instances that offer instance size flexibility, there is no preference to the instance size within a family that the Reserved Instances apply. The Reserved Instance discount is applied to qualifying usage that is detected first by the AWS billing system. The following example may help explain this.

You're running the following On-Demand Instances in account A (the purchasing account):

2 x m4.xlarge Linux, default tenancy instances in Availability Zone us-east-1a
1 x m4.2xlarge Linux, default tenancy instances in Availability Zone us-east-1b
2 x c4.xlarge Linux, default tenancy instances in Availability Zone us-east-1a
1x c4.2xlarge Linux, default tenancy instances in Availability Zone us-east-1b
Another customer is running the following On-Demand Instances in account B—a linked account:

2 x m4.xlarge Linux, default tenancy instances in Availability Zone us-east-1a
You purchase the following Reserved Instances in account A:

4 x m4.xlarge Linux, default tenancy Reserved Instances in us-east-1
2 x c4.xlarge Linux, default tenancy Reserved Instances in us-east-1
The Reserved Instance benefits are applied in the following way:

The discount of the four m4.xlarge Reserved Instances is used by the two m4.xlarge instances in account A and the m4.2xlarge instance in account A. All three instances match the attributes (instance family, region, platform, tenancy). There is no capacity reservation.
The discount of the two c4.xlarge Reserved Instances can apply to either the two c4.xlarge instances or the c4.2xlarge instance, all of which match the attributes (instance family, region, platform, tenancy), depending on which usage is detected first by the billing system. There is no preference given to a particular instance size. There is no capacity reservation.
Example Scenario 3: Zonal Reserved Instances in a Linked Account

In general, Reserved Instances that are owned by an account are applied first to usage in that account. However, if there are qualifying, unused Reserved Instances for a specific Availability Zone (zonal Reserved Instances) in other accounts in the organization, they are applied to the account before regional Reserved Instances owned by the account. This is done to ensure maximum Reserved Instance utilization and a lower bill. For billing purposes, all the accounts in the organization are treated as one account. The following example may help explain this.

You're running the following On-Demand Instance in account A (the purchasing account):

1 x m4.xlarge Linux, default tenancy instance in Availability Zone us-east-1a
A customer is running the following On-Demand Instance in linked account B:

1 x m4.xlarge Linux, default tenancy instance in Availability Zone us-east-1b
You purchase the following Reserved Instances in account A:

1 x m4.xlarge Linux, default tenancy Reserved Instance in Availability Zone us-east-1
A customer also purchases the following Reserved Instances in linked account C:

1 x m4.xlarge Linux, default tenancy Reserved Instances in Availability Zone us-east-1a
The Reserved Instance benefits are applied in the following way:

The discount of the m4.xlarge Reserved Instance owned by account C is applied to the m4.xlarge usage in account A.
The discount of the m4.xlarge Reserved Instance owned by account A is applied to the m4.xlarge usage in account B.
If the Reserved Instance owned by account A was first applied to the usage in account A, the Reserved Instance owned by account C remains unused and usage in account B is charged at On-Demand rates.
For more information, see Reserved Instances in the Billing and Cost Management Report.

How You Are Billed

All Reserved Instances provide with you a discount compared to On-Demand pricing. With Reserved Instances, you pay for the entire term regardless of actual use. You can choose to pay for your Reserved Instance upfront, partially upfront, or monthly, depending on the payment option specified for the Reserved Instance.

Note
The AWS Free Tier is available for new AWS accounts. If you are using the AWS Free Tier to run Amazon EC2 instances, and you purchase a Reserved Instance, you are charged under standard pricing guidelines. For information, see AWS Free Tier.
Topics

Hourly Billing
Viewing Your Bill
Reserved Instances and Consolidated Billing
Reserved Instance Discount Pricing Tiers
Hourly Billing

Reserved Instances are billed for every clock-hour during the term that you select, regardless of whether an instance is running or not. For more information about instance states, see Instance Lifecycle.

Reserved Instance billing benefits only apply to one instance-hour per clock-hour. An instance-hour begins when an instance is started and continues for 60 minutes or until the instance is stopped or terminated—whichever happens first. A clock-hour is defined as the standard 24-hour clock that runs from midnight to midnight, and is divided into 24 hours (for example, 1:00:00 to 1:59:59 is one clock-hour).

A new instance-hour begins after an instance has run for 60 continuous minutes, or if an instance is stopped and then started. Rebooting an instance does not reset the running instance-hour.

For example, if an instance is stopped and then started again during a clock-hour and continues running for two more clock-hours, the first instance-hour (before the restart) is charged at the discounted Reserved Instance rate. The next instance-hour (after restart) is charged at the On-Demand rate and the next two instance-hours are charged at the discounted Reserved Instance rate.

The Reserved Instance Utilization Reports section includes sample reports that illustrate the savings against running On-Demand Instances. The Reserved Instances FAQ includes an example of a list value calculation.

If you close your AWS account, On-Demand billing for your resources stops. However, if you have any Reserved Instances in your account, you continue to receive a bill for these until they expire.

Viewing Your Bill

You can find out about the charges and fees to your account by viewing the Billing & Cost Management page in the AWS Management Console. To access your account, choose the arrow beside it.

The Dashboard page displays charges against your account—such as upfront and one-time fees, and recurring charges. You can get both a summary and detailed list of your charges.
The upfront charges from your purchase of third-party Reserved Instances in the Reserved Instance Marketplace are listed in the AWS Marketplace Charges section, with the name of the seller displayed beside it. All recurring or usage charges for these Reserved Instances are listed in the AWS Service Charges section.
On the Bills page, under Details expand the Elastic Compute Cloud section and the region to get billing information about your Reserved Instances.
You can view the charges online, or you can download a CSV file.

You can also track your Reserved Instance utilization using the AWS Cost and Usage Report. For more information, see Reserved Instances in the AWS Cost and Usage Report in the AWS Billing and Cost Management User Guide.

Reserved Instances and Consolidated Billing

The pricing benefits of Reserved Instances are shared when the purchasing account is part of a set of accounts billed under one consolidated billing payer account. The hourly usage across all member accounts is aggregated in the payer account every month. This is typically useful for companies in which there are different functional teams or groups; then, the normal Reserved Instance logic is applied to calculate the bill. For more information, see Consolidated Billing and AWS Organizations in the AWS Organizations User Guide.

If you close the payer account, any member accounts that benefit from Reserved Instances billing discounts continue to benefit from the discount until the Reserved Instances expire, or until the member account is removed.

Reserved Instance Discount Pricing Tiers

If your account qualifies for a discount pricing tier, it automatically receives discounts on upfront and hourly usage fees for Reserved Instance purchases that you make within that tier level from that point on. To qualify for a discount, the list value of your Reserved Instances in the region must be $500,000 USD or more.

The following rules apply:

Pricing tiers and related discounts apply only to purchases of Amazon EC2 Standard Reserved Instances.
Pricing tiers do not apply to Reserved Instances for Windows with SQL Server Standard or Windows with SQL Server Web.
Pricing tier discounts only apply to purchases made from AWS. They do not apply to purchases of third-party Reserved Instances.
Discount pricing tiers are currently not applicable to Convertible Reserved Instance purchases.
Topics

Calculating Reserved Instance Pricing Discounts
Buying with a Discount Tier
Crossing Pricing Tiers
Consolidated Billing for Pricing Tiers
Calculating Reserved Instance Pricing Discounts

You can determine the pricing tier for your account by calculating the list value for all of your Reserved Instances in a region. Multiply the hourly recurring price for each reservation by the hours left in each term and add the undiscounted upfront price (also known as the fixed price) listed on the Reserved Instances pricing page at the time of purchase. Because the list value is based on undiscounted (public) pricing, it is not affected if you qualify for a volume discount or if the price drops after you buy your Reserved Instances.

Copy
List value = fixed price + (undiscounted recurring hourly price * hours in term)
To view the fixed price values for Reserved Instances using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Display the Upfront Price column by choosing Show/Hide in the top right corner.

To view the fixed price values for Reserved Instances using the command line

describe-reserved-instances (AWS CLI)
Get-EC2ReservedInstance (AWS Tools for Windows PowerShell)
DescribeReservedInstances (Amazon EC2 API)
Buying with a Discount Tier

When you buy Reserved Instances, Amazon EC2 automatically applies any discounts to the part of your purchase that falls within a discount pricing tier. You don't need to do anything differently, and you can buy Reserved Instances using any of the Amazon EC2 tools. For more information, see Buying Reserved Instances.

After the list value of your active Reserved Instances in a region crosses into a discount pricing tier, any future purchase of Reserved Instances in that region are charged at a discounted rate. If a single purchase of Reserved Instances in a region takes you over the threshold of a discount tier, then the portion of the purchase that is above the price threshold is charged at the discounted rate. For more information about the temporary Reserved Instance IDs that are created during the purchase process, see Crossing Pricing Tiers.

If your list value falls below the price point for that discount pricing tier—for example, if some of your Reserved Instances expire—future purchases of Reserved Instances in the region are not discounted. However, you continue to get the discount applied against any Reserved Instances that were originally purchased within the discount pricing tier.

When you buy Reserved Instances, one of four possible scenarios occurs:

No discount—Your purchase within a region is still below the discount threshold.
Partial discount—Your purchase within a region crosses the threshold of the first discount tier. No discount is applied to one or more reservations and the discounted rate is applied to the remaining reservations.
Full discount—Your entire purchase within a region falls within one discount tier and is discounted appropriately.
Two discount rates—Your purchase within a region crosses from a lower discount tier to a higher discount tier. You are charged two different rates: one or more reservations at the lower discounted rate, and the remaining reservations at the higher discounted rate.
Crossing Pricing Tiers

If your purchase crosses into a discounted pricing tier, you see multiple entries for that purchase: one for that part of the purchase charged at the regular price, and another for that part of the purchase charged at the applicable discounted rate.

The Reserved Instance service generates several Reserved Instance IDs because your purchase crossed from an undiscounted tier, or from one discounted tier to another. There is an ID for each set of reservations in a tier. Consequently, the ID returned by your purchase CLI command or API action is different from the actual ID of the new Reserved Instances.

Consolidated Billing for Pricing Tiers

A consolidated billing account aggregates the list value of member accounts within a region. When the list value of all active Reserved Instances for the consolidated billing account reaches a discount pricing tier, any Reserved Instances purchased after this point by any member of the consolidated billing account are charged at the discounted rate (as long as the list value for that consolidated account stays above the discount pricing tier threshold). For more information, see Reserved Instances and Consolidated Billing.

Buying Reserved Instances

To purchase a Reserved Instance, search for Reserved Instance offerings from AWS and third-party sellers, adjusting your search parameters until you find the exact match that you're looking for.

When you search for Reserved Instances to buy, you receive a quote on the cost of the returned offerings. When you proceed with the purchase, AWS automatically places a limit price on the purchase price. The total cost of your Reserved Instances won't exceed the amount that you were quoted.

If the price rises or changes for any reason, the purchase is not completed. If, at the time of purchase, there are offerings similar to your choice but at a lower price, AWS sells you the offerings at the lower price.

Before you confirm your purchase, review the details of the Reserved Instance that you plan to buy, and make sure that all the parameters are accurate. After you purchase a Reserved Instance (either from a third-party seller in the Reserved Instance Marketplace or from AWS), you cannot cancel your purchase.

Note
To purchase and modify Reserved Instances, ensure that your IAM user account has the appropriate permissions, such as the ability to describe Availability Zones. For information, see Example Policies for Working With the AWS CLI or an AWS SDK and Example Policies for Working in the Amazon EC2 Console.
Topics

Buying Standard Reserved Instances
Buying Convertible Reserved Instances
Viewing Your Reserved Instances
Using Your Reserved Instances
Buying Standard Reserved Instances

You can buy Standard Reserved Instances in a specific Availability Zone and get a capacity reservation. Alternatively, you can forego the capacity reservation and purchase a regional Standard Reserved Instance.

To buy Standard Reserved Instances using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Reserved Instances, Purchase Reserved Instances.

For Offering Class, choose Standard to display Standard Reserved Instances.

To purchase a capacity reservation, choose Only show offerings that reserve capacity in the top-right corner of the purchase screen. To purchase a regional Reserved Instance, leave the check box unselected.

Select other configurations as needed and choose Search.

Note
To purchase a Standard Reserved Instance from the Reserved Instance Marketplace, look for 3rd Party in the Seller column in the search results. The Term column displays non-standard terms.
Select the Reserved Instances to purchase, enter the quantity, and choose Add to Cart.

To see a summary of the Reserved Instances that you selected, choose View Cart.

To complete the order, choose Purchase.

Note
If, at the time of purchase, there are offerings similar to your choice but with a lower price, AWS sells you the offerings at the lower price.
The status of your purchase is listed in the State column. When your order is complete, the State value changes from payment-pending to active. When the Reserved Instance is active, it is ready to use.

Note
If the status goes to retired, AWS may not have received your payment.
To buy a Standard Reserved Instance using the AWS CLI

Find available Reserved Instances using the describe-reserved-instances-offerings command. Specify standard for the --offering-class parameter to return only Standard Reserved Instances. You can apply additional parameters to narrow your results; for example, if you want to purchase a regional t2.large Reserved Instance with a default tenancy for Linux/UNIX for a 1-year term only:

Copy
aws ec2 describe-reserved-instances-offerings --instance-type t2.large --offering-class standard --product-description "Linux/UNIX" --instance-tenancy default --filters Name=duration,Values=31536000 Name=scope,Values=Region
{
    "ReservedInstancesOfferings": [
        {
            "OfferingClass": "standard", 
            "OfferingType": "No Upfront", 
            "ProductDescription": "Linux/UNIX", 
            "InstanceTenancy": "default", 
            "PricingDetails": [], 
            "UsagePrice": 0.0, 
            "RecurringCharges": [
                {
                    "Amount": 0.0672, 
                    "Frequency": "Hourly"
                }
            ], 
            "Marketplace": false, 
            "CurrencyCode": "USD", 
            "FixedPrice": 0.0, 
            "Duration": 31536000, 
            "Scope": "Region", 
            "ReservedInstancesOfferingId": "bec624df-a8cc-4aad-a72f-4f8abc34caf2", 
            "InstanceType": "t2.large"
        }, 
        {
            "OfferingClass": "standard", 
            "OfferingType": "Partial Upfront", 
            "ProductDescription": "Linux/UNIX", 
            "InstanceTenancy": "default", 
            "PricingDetails": [], 
            "UsagePrice": 0.0, 
            "RecurringCharges": [
                {
                    "Amount": 0.032, 
                    "Frequency": "Hourly"
                }
            ], 
            "Marketplace": false, 
            "CurrencyCode": "USD", 
            "FixedPrice": 280.0, 
            "Duration": 31536000, 
            "Scope": "Region", 
            "ReservedInstancesOfferingId": "6b15a842-3acb-4320-bd55-fa43a79f3fe3", 
            "InstanceType": "t2.large"
        }, 
        {
            "OfferingClass": "standard", 
            "OfferingType": "All Upfront", 
            "ProductDescription": "Linux/UNIX", 
            "InstanceTenancy": "default", 
            "PricingDetails": [], 
            "UsagePrice": 0.0, 
            "RecurringCharges": [], 
            "Marketplace": false, 
            "CurrencyCode": "USD", 
            "FixedPrice": 549.0, 
            "Duration": 31536000, 
            "Scope": "Region", 
            "ReservedInstancesOfferingId": "5062dc97-d284-417b-b09e-8abed1e5a183", 
            "InstanceType": "t2.large"
        }
    ]
}
To find Reserved Instances on the Reserved Instance Marketplace only, use the marketplace filter and do not specify a duration in the request, as the term may be shorter than a 1– or 3-year term.

Copy
aws ec2 describe-reserved-instances-offerings --instance-type t2.large --offering-class standard --product-description "Linux/UNIX" --instance-tenancy default --filters Name=marketplace,Values=true
When you find a Reserved Instance that meets your needs, take note of the ReservedInstancesOfferingId.

Use the purchase-reserved-instances-offering command to buy your Reserved Instance. You must specify the Reserved Instance offering ID you obtained the previous step and you must specify the number of instances for the reservation.

Copy
aws ec2 purchase-reserved-instances-offering --reserved-instances-offering-id ec06327e-dd07-46ee-9398-75b5fexample --instance-count 1
Use the describe-reserved-instances command to get the status of your Reserved Instance.

Copy
aws ec2 describe-reserved-instances
Alternatively, use the following AWS Tools for Windows PowerShell commands:

Get-EC2ReservedInstancesOffering
New-EC2ReservedInstance
Get-EC2ReservedInstance
If you already have a running instance that matches the specifications of the Reserved Instance, the billing benefit is immediately applied. You do not have to restart your instances. If you do not have a suitable running instance, launch an instance and ensure that you match the same criteria that you specified for your Reserved Instance. For more information, see Using Your Reserved Instances.

For examples of how Reserved Instances are applied to your running instances, see How Reserved Instances Are Applied.

Buying Convertible Reserved Instances

You can buy Convertible Reserved Instances in a specific Availability Zone and get a capacity reservation. Alternatively, you can forego the capacity reservation and purchase a regional Convertible Reserved Instance.

To buy Convertible Reserved Instances using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Reserved Instances, Purchase Reserved Instances.

For Offering Class, choose Convertible to display Convertible Reserved Instances.

To purchase a capacity reservation, choose Only show offerings that reserve capacity in the top-right corner of the purchase screen. To purchase a regional Reserved Instance, leave the check box unselected.

Select other configurations as needed and choose Search.

Select the Convertible Reserved Instances to purchase, enter the quantity, and choose Add to Cart.

To see a summary of your selection, choose View Cart.

To complete the order, choose Purchase.

Note
If, at the time of purchase, there are offerings similar to your choice but with a lower price, AWS sells you the offerings at the lower price.
The status of your purchase is listed in the State column. When your order is complete, the State value changes from payment-pending to active. When the Reserved Instance is active, it is ready to use.

Note
If the status goes to retired, AWS may not have received your payment.
To buy a Convertible Reserved Instance using the AWS CLI

Find available Reserved Instances using the describe-reserved-instances-offerings command. Specify convertible for the --offering-class parameter to return only Convertible Reserved Instances. You can apply additional parameters to narrow your results; for example, if you want to purchase a regional t2.large Reserved Instance with a default tenancy for Linux/UNIX:

Copy
aws ec2 describe-reserved-instances-offerings --instance-type t2.large --offering-class convertible --product-description "Linux/UNIX" --instance-tenancy default --filters Name=scope,Values=Region
{
    "ReservedInstancesOfferings": [
        {
            "OfferingClass": "convertible", 
            "OfferingType": "No Upfront", 
            "ProductDescription": "Linux/UNIX", 
            "InstanceTenancy": "default", 
            "PricingDetails": [], 
            "UsagePrice": 0.0, 
            "RecurringCharges": [
                {
                    "Amount": 0.0556, 
                    "Frequency": "Hourly"
                }
            ], 
            "Marketplace": false, 
            "CurrencyCode": "USD", 
            "FixedPrice": 0.0, 
            "Duration": 94608000, 
            "Scope": "Region", 
            "ReservedInstancesOfferingId": "e242e87b-b75c-4079-8e87-02d53f145204", 
            "InstanceType": "t2.large"
        }, 
        {
            "OfferingClass": "convertible", 
            "OfferingType": "Partial Upfront", 
            "ProductDescription": "Linux/UNIX", 
            "InstanceTenancy": "default", 
            "PricingDetails": [], 
            "UsagePrice": 0.0, 
            "RecurringCharges": [
                {
                    "Amount": 0.0258, 
                    "Frequency": "Hourly"
                }
            ], 
            "Marketplace": false, 
            "CurrencyCode": "USD", 
            "FixedPrice": 677.0, 
            "Duration": 94608000, 
            "Scope": "Region", 
            "ReservedInstancesOfferingId": "13486b92-bdd6-4b68-894c-509bcf239ccd", 
            "InstanceType": "t2.large"
        }, 
        {
            "OfferingClass": "convertible", 
            "OfferingType": "All Upfront", 
            "ProductDescription": "Linux/UNIX", 
            "InstanceTenancy": "default", 
            "PricingDetails": [], 
            "UsagePrice": 0.0, 
            "RecurringCharges": [], 
            "Marketplace": false, 
            "CurrencyCode": "USD", 
            "FixedPrice": 1327.0, 
            "Duration": 94608000, 
            "Scope": "Region", 
            "ReservedInstancesOfferingId": "e00ec34b-4674-4fb9-a0a9-213296ab93aa", 
            "InstanceType": "t2.large"
        }
    ]
}
When you find a Reserved Instance that meets your needs, take note of the ReservedInstancesOfferingId.

Use the purchase-reserved-instances-offering command to buy your Reserved Instance. You must specify the Reserved Instance offering ID you obtained the previous step and you must specify the number of instances for the reservation.

Copy
aws ec2 purchase-reserved-instances-offering --reserved-instances-offering-id ec06327e-dd07-46ee-9398-75b5fexample --instance-count 1
Use the describe-reserved-instances command to get the status of your Reserved Instance.

Copy
aws ec2 describe-reserved-instances
Alternatively, use the following AWS Tools for Windows PowerShell commands:

Get-EC2ReservedInstancesOffering
New-EC2ReservedInstance
Get-EC2ReservedInstance
If you already have a running instance that matches the specifications of the Reserved Instance, the billing benefit is immediately applied. You do not have to restart your instances. If you do not have a suitable running instance, launch an instance and ensure that you match the same criteria that you specified for your Reserved Instance. For more information, see Using Your Reserved Instances.

For examples of how Reserved Instances are applied to your running instances, see How Reserved Instances Are Applied.

Viewing Your Reserved Instances

You can view the Reserved Instances you've purchased using the Amazon EC2 console, or a command line tool.

To view your Reserved Instances in the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Reserved Instances.

Your active and retired Reserved Instances are listed. The State column displays the state.

If you are a seller in the Reserved Instance Marketplace the My Listings tab displays the status of a reservation that's listed in the Reserved Instance Marketplace. For more information, see Reserved Instance Listing States.

To view your Reserved Instances using the command line

describe-reserved-instances (AWS CLI)
Get-EC2ReservedInstance (Tools for Windows PowerShell)
Using Your Reserved Instances

Reserved Instances are automatically applied to running On-Demand Instances provided that the specifications match. If you have no running On-Demand Instances that match the specifications of your Reserved Instance, the Reserved Instance is unused until you launch an instance with the required specifications.

If you're launching an instance to take advantage of the billing benefit of a Reserved Instance, ensure that you specify the following information during launch:

Platform: You must choose an Amazon Machine Image (AMI) that matches the platform (product description) of your Reserved Instance. For example, if you specified Linux/UNIX, you can launch an instance from an Amazon Linux AMI.
Instance type: Specify the same instance type as your Reserved Instance; for example, t2.large.
Availability Zone: If you purchased a Reserved Instance for a specific Availability Zone, you must launch the instance into the same Availability Zone. If you purchased a regional Reserved Instance, you can launch your instance into any Availability Zone.
Tenancy: The tenancy of your instance must match the tenancy of the Reserved Instance; for example, dedicated or shared. For more information, see Dedicated Instances.
For more information, see Launching an Instance. For examples of how Reserved Instances are applied to your running instances, see How Reserved Instances Are Applied.

You can use Auto Scaling or other AWS services to launch the On-Demand Instances that use your Reserved Instance benefits. For more information, see the Auto Scaling User Guide.

Selling on the Reserved Instance Marketplace

The Reserved Instance Marketplace is a platform that supports the sale of third-party and AWS customers' unused Standard Reserved Instances, which vary in term lengths and pricing options. For example, you may want to sell Reserved Instances after moving instances to a new AWS region, changing to a new instance type, ending projects before the term expiration, when your business needs change, or if you have unneeded capacity.

If you want to sell your unused Reserved Instances on the Reserved Instance Marketplace, you must meet certain eligibility criteria.

Topics

Selling in the Reserved Instance Marketplace
Buying in the Reserved Instance Marketplace
Selling in the Reserved Instance Marketplace

As soon as you list your Reserved Instances in the Reserved Instance Marketplace, they are available for potential buyers to find. All Reserved Instances are grouped according to the duration of the term remaining and the hourly price.

To fulfill a buyer's request, AWS first sells the Reserved Instance with the lowest upfront price in the specified grouping. Then, we sell the Reserved Instance with the next lowest price, until the buyer's entire order is fulfilled. AWS then processes the transactions and transfers ownership of the Reserved Instances to the buyer.

You own your Reserved Instance until it's sold. After the sale, you've given up the capacity reservation and the discounted recurring fees. If you continue to use your instance, AWS charges you the On-Demand price starting from the time that your Reserved Instance was sold.

Topics

Restrictions and Limitations
Registering as a Seller
Pricing Your Reserved Instances
Listing Your Reserved Instances
Lifecycle of a Listing
After Your Reserved Instance Is Sold
Restrictions and Limitations

Before you can sell your unused reservation, be aware of the following limitations and restrictions.

Convertible Reserved Instances— Only Amazon EC2 Standard Reserved Instances can be sold in the Reserved Instance Marketplace. Convertible Reserved Instances cannot be sold.
Reserved Instances scope—Only Standard Reserved Instances purchased for an Availability Zone can be sold in the Reserved Instance Marketplace. Reserved Instances purchased for a region cannot be sold.
Seller requirement—To become a seller in the Reserved Instance Marketplace, you must register as a seller. For information, see Listing Your Reserved Instances.
Bank requirement—AWS must have your bank information in order to disburse funds collected when you sell your reservations. The bank you specify must have a US address. For more information, see Bank Accounts.
Tax requirement—Sellers who have 50 or more transactions or who plan to sell $20,000 or more in Standard Reserved Instances have to provide additional information about their business for tax reasons. For information, see Tax Information.
Minimum selling price—The minimum price allowed in the Reserved Instance Marketplace is $0.00.
When Standard Reserved Instances can be sold—Standard Reserved Instances can be sold only after AWS has received the upfront payment and the reservation has been active (you've owned it) for at least 30 days. In addition, there must be at least one month remaining in the term of the Standard Reserved Instance you are listing.
Modifying your listing—It is not possible to modify your listing in the Reserved Instance Marketplace directly. However, you can change your listing by first canceling it and then creating another listing with new parameters. For information, see Pricing Your Reserved Instances. You can also modify your Reserved Instances before listing them. For information, see Modifying Standard Reserved Instances.
Service fee—AWS charges a service fee of 12 percent of the total upfront price of each Standard Reserved Instance you sell in the Reserved Instance Marketplace. The upfront price is the price the seller is charging for the Standard Reserved Instance.
Other AWS Reserved Instances—Only Amazon EC2 Standard Reserved Instances can be sold in the Reserved Instance Marketplace. Other AWS Reserved Instances, such as Amazon RDS and Amazon ElastiCache Reserved Instances cannot be sold in the Reserved Instance Marketplace.
Registering as a Seller

To sell in the Reserved Instance Marketplace, you must first register as a seller. During registration, you provide the name of your business, information about your bank, and your business's tax identification number.

After AWS receives your completed seller registration, you receive an email confirming your registration and informing you that you can get started selling in the Reserved Instance Marketplace.

Topics

Bank Accounts
Tax Information
Sharing Information with the Buyer
Getting Paid
Bank Accounts

AWS must have your bank information in order to disburse funds collected when you sell your Reserved Instance. The bank you specify must have a US address.

To register a default bank account for disbursements

Open the Reserved Instance Marketplace Seller Registration page and sign in using your AWS credentials.

On the Manage Bank Account page, provide the following information about the bank through to receive payment:

Bank account holder name
Routing number
Account number
Bank account type
Note
If you are using a corporate bank account, you are prompted to send the information about the bank account via fax (1-206-765-3424).
After registration, the bank account provided is set as the default, pending verification with the bank. It can take up to two weeks to verify a new bank account, during which time you can't receive disbursements. For an established account, it usually takes about two days for disbursements to complete.

To change the default bank account for disbursement

On the Reserved Instance Marketplace Seller Registration page, sign in with the account that you used when you registered.

On the Manage Bank Account page, add a new bank account or modify the default bank account as needed.

Tax Information

Your sale of Reserved Instances might be subject to a transactional tax, such as sales tax or value-added tax. You should check with your business's tax, legal, finance, or accounting department to determine if transaction-based taxes are applicable. You are responsible for collecting and sending the transaction-based taxes to the appropriate tax authority.

As part of the seller registration process, you have the option of completing a tax interview. We encourage you to complete this process if any of the following apply:

You want AWS to generate a Form 1099-K.
You anticipate having either 50 or more transactions or $20,000 or more in sales of Reserved Instances in a calendar year. A transaction can involve one or more Reserved Instances. If you choose to skip this step during registration, and later you reach transaction 49, you get a message saying, "You have reached the transaction limit for pre-tax. Please complete the tax interview in the Seller Registration Portal." After the tax interview is completed, the account limit is automatically increased.
You are a non-US seller. In this case, you must electronically complete Form W-8BEN.
For more information about IRS requirements and the Form 1099-K, see the IRS website.

The tax information you enter as part of the tax interview differs depending on whether your business is a US or non-US legal entity. As you fill out the tax interview, keep in mind the following:

Information provided by AWS, including the information in this topic, does not constitute tax, legal, or other professional advice. To find out how the IRS reporting requirements might affect your business, or if you have other questions, please contact your tax, legal, or other professional advisor.
To fulfill the IRS reporting requirements as efficiently as possible, answer all questions and enter all information requested during the interview.
Check your answers. Avoid misspellings or entering incorrect tax identification numbers. They can result in an invalidated tax form.
After you complete the tax registration process, AWS files Form 1099-K. You will receive a copy of it through the US mail on or before January 31 in the year following the year that your tax account reaches the threshold levels. For example, if your tax account reaches the threshold in 2016, you receive the form in 2017.

Sharing Information with the Buyer

When you sell in the Reserved Instance Marketplace, AWS shares your company’s legal name on the buyer’s statement in accordance with US regulations. In addition, if the buyer calls AWS Support because the buyer needs to contact you for an invoice or for some other tax-related reason, AWS may need to provide the buyer with your email address so that the buyer can contact you directly.

For similar reasons, the buyer's ZIP code and country information are provided to the seller in the disbursement report. As a seller, you might need this information to accompany any necessary transaction taxes that you remit to the government (such as sales tax and value-added tax).

AWS cannot offer tax advice, but if your tax specialist determines that you need specific additional information, contact AWS Support.

Getting Paid

As soon as AWS receives funds from the buyer, a message is sent to the registered owner account email for the sold Reserved Instance.

AWS sends an Automated Clearing House (ACH) wire transfer to your specified bank account. Typically, this transfer occurs between one to three days after your Reserved Instance has been sold. You can view the state of this disbursement by viewing your Reserved Instance disbursement report. Disbursements take place once a day. Keep in mind that you can't receive disbursements until AWS has received verification from your bank. This period can take up to two weeks.

The Reserved Instance that you sold continues to appear when you describe your Reserved Instances.

You receive a cash disbursement for your Reserved Instances through a wire transfer directly into your bank account. AWS charges a service fee of 12 percent of the total upfront price of each Reserved Instance you sell in the Reserved Instance Marketplace.

Pricing Your Reserved Instances

The upfront fee is the only fee that you can specify for the Reserved Instance that you're selling. The upfront fee is the one-time fee that the buyer pays when they purchase a Reserved Instance. You cannot specify the usage fee or the recurring fee; The buyer pays the same usage or recurring fees that were set when the reservations were originally purchased.

The following are important limits to note:

You can sell up to $50,000 in Reserved Instances per year. To sell more, complete the Request to Raise Sales Limit on Amazon EC2 Reserved Instances form.
The minimum price is $0. The minimum allowed price in the Reserved Instance Marketplace is $0.00.
You cannot modify your listing directly. However, you can change your listing by first canceling it and then creating another listing with new parameters.

You can cancel your listing at any time, as long as it's in the activestate. You cannot cancel the listing if it's already matched or being processed for a sale. If some of the instances in your listing are matched and you cancel the listing, only the remaining unmatched instances are removed from the listing.

Setting a Pricing Schedule

Because the value of Reserved Instances decreases over time, by default, AWS can set prices to decrease in equal increments month over month. However, you can set different upfront prices based on when your reservation sells.

For example, if your Reserved Instance has nine months of its term remaining, you can specify the amount that you would accept if a customer were to purchase that Reserved Instance with nine months remaining. You could set another price with five months remaining, and yet another price with one month remaining.

Listing Your Reserved Instances

As a registered seller, you can choose to sell one or more of your Reserved Instances. You can choose to sell all of them in one listing or in portions. In addition, you can list Reserved Instances with any configuration of instance type, platform, and Availability Zone.

If you cancel your listing and a portion of that listing has already been sold, the cancellation is not effective on the portion that has been sold. Only the unsold portion of the listing is no longer available in the Reserved Instance Marketplace.

Topics

Listing Your Reserved Instance Using the AWS Management Console
Listing Your Reserved Instances Using the AWS CLI or Amazon EC2 API
Reserved Instance Listing States
Listing Your Reserved Instance Using the AWS Management Console

To list a Reserved Instance in the Reserved Instance Marketplace using the AWS Management Console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Reserved Instances.

Select the Reserved Instances to list, and choose Sell Reserved Instances.

On the Configure Your Reserved Instance Listing page, set the number of instances to sell and the upfront price for the remaining term in the relevant columns. See how the value of your reservation changes over the remainder of the term by selecting the arrow next to the Months Remaining column.

If you are an advanced user and you want to customize the pricing, you can enter different values for the subsequent months. To return to the default linear price drop, choose Reset.

Choose Continue when you are finished configuring your listing.

Confirm the details of your listing, on the Confirm Your Reserved Instance Listing page and if you're satisfied, choose List Reserved Instance.

To view your listings in the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Reserved Instances.

Select the Reserved Instance that you've listed and choose My Listings.

Listing Your Reserved Instances Using the AWS CLI or Amazon EC2 API

To list a Reserved Instance in the Reserved Instance Marketplace using the AWS CLI

Get a list of your Reserved Instances by using the describe-reserved-instances command.

Note the ID of the Reserved Instance you want to list and call create-reserved-instances-listing. You must specify the ID of the Reserved Instance, the number of instances, and the pricing schedule.

To view your listing, use the describe-reserved-instances-listings command.

To cancel your listing, use the cancel-reserved-instances-listings command.

To list a Reserved Instance in the Reserved Instance Marketplace using the Amazon EC2 API

DescribeReservedInstances
CreateReservedInstancesListing
DescribeReservedInstancesListings
CancelReservedInstancesListing
Reserved Instance Listing States

Listing State on the My Listings tab of the Reserved Instances page displays the current status of your listings:

The information displayed by Listing State is about the status of your listing in the Reserved Instance Marketplace. It is different from the status information that is displayed by the State column in the Reserved Instances page. This State information is about your reservation.

active—The listing is available for purchase.
canceled—The listing is canceled and isn't available for purchase in the Reserved Instance Marketplace.
closed—The Reserved Instance is not listed. A Reserved Instance might be closed because the sale of the listing was completed.
Lifecycle of a Listing

When all the instances in your listing are matched and sold, the My Listings tab shows that the Total instance count matches the count listed under Sold. Also, there are no Available instances left for your listing, and its Status is closed.

When only a portion of your listing is sold, AWS retires the Reserved Instances in the listing and creates the number of Reserved Instances equal to the Reserved Instances remaining in the count. So, the listing ID and the listing that it represents, which now has fewer reservations for sale, is still active.

Any future sales of Reserved Instances in this listing are processed this way. When all the Reserved Instances in the listing are sold, AWS marks the listing as closed.

For example, you create a listing Reserved Instances listing ID 5ec28771-05ff-4b9b-aa31-9e57dexample with a listing count of 5.

The My Listings tab in the Reserved Instance console page displays the listing this way:

Reserved Instance listing ID 5ec28771-05ff-4b9b-aa31-9e57dexample

Total reservation count = 5
Sold = 0
Available = 5
Status = active
A buyer purchases two of the reservations, which leaves a count of three reservations still available for sale. Because of this partial sale, AWS creates a new reservation with a count of three to represent the remaining reservations that are still for sale.

This is how your listing looks in the My Listings tab:

Reserved Instance listing ID 5ec28771-05ff-4b9b-aa31-9e57dexample

Total reservation count = 5
Sold = 2
Available = 3
Status = active
If you cancel your listing and a portion of that listing has already sold, the cancelation is not effective on the portion that has been sold. Only the unsold portion of the listing is no longer available in the Reserved Instance Marketplace.

After Your Reserved Instance Is Sold

When your Reserved Instance is sold, AWS sends you an email notification. Each day that there is any kind of activity, you receive one email notification capturing all the activities of the day. For example, you may create or sell a listing, or AWS may send funds to your account.

To track the status of a Reserved Instance listing in the console, choose Reserved Instance, My Listings. The My Listings tab contains the Listing State value. It also contains information about the term, listing price, and a breakdown of how many instances in the listing are available, pending, sold, and canceled. You can also use the describe-reserved-instances-listings command with the appropriate filter to obtain information about your listings.

Buying in the Reserved Instance Marketplace

You can purchase Reserved Instances from third-party sellers who own Reserved Instances that they no longer need from the Reserved Instance Marketplace. You can do this using the Amazon EC2 console or a command line tool. The process is similar to purchasing Reserved Instances from AWS. For more information, see Buying Reserved Instances.

There are a few differences between Reserved Instances purchased in the Reserved Instance Marketplace and Reserved Instances purchased directly from AWS:

Term—Reserved Instances that you purchase from third-party sellers have less than a full standard term remaining. Full standard terms from AWS run for one year or three years.
Upfront price—Third-party Reserved Instances can be sold at different upfront prices. The usage or recurring fees remain the same as the fees set when the Reserved Instances were originally purchased from AWS.
Types of Reserved Instances—Only Amazon EC2 Standard Reserved Instances can be purchased from the Reserved Instance Marketplace. Convertible Reserved Instances, Amazon RDS and Amazon ElastiCache Reserved Instances are not available for purchase on the Reserved Instance Marketplace.
Basic information about you is shared with the seller, for example, your ZIP code and country information.

This information enables sellers to calculate any necessary transaction taxes that they have to remit to the government (such as sales tax or value-added tax) and is provided as a disbursement report. In rare circumstances, AWS might have to provide the seller with your email address, so that they can contact you regarding questions related to the sale (for example, tax questions).

For similar reasons, AWS shares the legal entity name of the seller on the buyer's purchase invoice. If you need additional information about the seller for tax or related reasons, contact AWS Support.

Modifying Standard Reserved Instances

When your computing needs change, you can modify your Standard Reserved Instances and continue to benefit from the billing benefit. You can modify the Availability Zone, scope, network platform, or instance size (within the same instance type) of your Reserved Instance. To modify a Reserved Instance, you specify the Reserved Instances that you want to modify, and you specify one or more target configurations.

Note
You cannot modify a Convertible Reserved Instance. Instead, you can exchange it. For more information, see Exchanging Convertible Reserved Instances.
You can modify all or a subset of your Reserved Instances. You can separate your original Reserved Instances into two or more new Reserved Instances. For example, if you have a reservation for 10 instances in us-east-1a and decide to move 5 instances to us-east-1b, the modification request results in two new reservations: one for 5 instances in us-east-1a and the other for 5 instances in us-east-1b.

You can also merge two or more Reserved Instances into a single Reserved Instance. For example, if you have four t2.small Reserved Instances of one instance each, you can merge them to create one t2.large Reserved Instance. For more information, see Modifying the Instance Size of Your Reservations.

After modification, the benefit of the Reserved Instances is applied only to instances that match the new parameters. For example, if you change the Availability Zone of a reservation, the capacity reservation and pricing benefits are automatically applied to instance usage in the new Availability Zone. Instances that no longer match the new parameters are charged at the On-Demand rate unless your account has other applicable reservations.

If your modification request succeeds:

The modified reservation becomes effective immediately and the pricing benefit is applied to the new instances beginning at the hour of the modification request. For example, if you successfully modify your reservations at 9:15PM, the pricing benefit transfers to your new instance at 9:00PM. (You can get the effective date of the modified Reserved Instances by using the DescribeReservedInstances API action or the describe-reserved-instances command (AWS CLI).
The original reservation is retired. Its end date is the start date of the new reservation, and the end date of the new reservation is the same as the end date of the original Reserved Instance. If you modify a three-year reservation that had 16 months left in its term, the resulting modified reservation is a 16-month reservation with the same end date as the original one.
The modified reservation lists a $0 fixed price and not the fixed price of the original reservation.
Note
The fixed price of the modified reservation does not affect the discount pricing tier calculations applied to your account, which are based on the fixed price of the original reservation.
If your modification request fails, your Reserved Instances maintain their original configuration, and are immediately available for another modification request.

There is no fee for modification, and you do not receive any new bills or invoices. Modification is separate from purchasing and does not affect how you use, purchase, or sell Standard Reserved Instances.

You can modify your reservations as frequently as you like, but you cannot change or cancel a pending modification request after you submit it. After the modification has completed successfully, you can submit another modification request to roll back any changes you made, if needed.

Topics

Requirements and Restrictions for Modification
Modifying the Instance Size of Your Reservations
Submitting Modification Requests
Troubleshooting Modification Requests
Requirements and Restrictions for Modification

Not all attributes of a Reserved Instance can be modified, and restrictions may apply.


Modifiable attribute	Supported platforms	Limitations
Change Availability Zones within the same region
All Windows and Linux
-
Change the scope from Availability Zone to Region and vice versa
All Windows and Linux
If you change the scope from Availability Zone to region, you lose the capacity reservation benefit.

If you change the scope from region to Availability Zone, you lose Availability Zone flexibility and instance size flexibility (if applicable). For more information, see How Reserved Instances Are Applied.
Change the network platform between EC2-VPC and EC2-Classic
All Windows and Linux
Only applicable if your account supports EC2-Classic.
Change the instance size within the same instance type
Supported on Linux, except for RedHat and SUSE Linux due to licensing differences. For more information about RedHat and SUSE pricing, see Amazon EC2 Reserved Instance Pricing.

Not supported on Windows.
Some instance types are not supported, because there are no other sizes available. For more information, see Modifying the Instance Size of Your Reservations.
Amazon EC2 processes your modification request if there is sufficient capacity for your target configuration (if applicable), and if the following conditions are met.

The Reserved Instances that you want to modify must be:

Standard Reserved Instances
Active
Not pending another modification request
Not listed in the Reserved Instance Marketplace
Note
To modify your Reserved Instances that are listed in the Reserved Instance Marketplace, cancel the listing, request modification, and then list them again.
Terminating in the same hour (but not minutes or seconds)
Already purchased by you (you cannot modify an offering before or at the same time that you purchase it)
Your modification request must meet the following conditions:

Each target configuration in the request must be a unique combination of scope, instance type, instance size, offering class, and network platform attributes. For example, you cannot split a Reserved Instance for a single t2.medium instance into two identical Reserved Instances of one t2.small instance each. Instead, you can create one Reserved Instance with two t2.small instances.
There must be a match between the instance size footprint of the active reservation and the target configuration. For more information, see Modifying the Instance Size of Your Reservations.
Modifying the Instance Size of Your Reservations

If you have Amazon Linux reservations in an instance type with multiple sizes, you can adjust the instance size of your Standard Reserved Instances.

Note
Instances are grouped by family (based on storage, or CPU capacity); type (designed for specific use cases); and size. For example, the c4 instance type is in the Compute optimized instance family and is available in multiple sizes. While c3 instances are in the same family, you can't modify c4 instances into c3 instances because they have different hardware specifications. For more information, see Amazon EC2 Instance Types.
The following instances cannot be modified because there are no other sizes available.

t1.micro
cc1.4xlarge
cc2.8xlarge
cg1.8xlarge
cr1.8xlarge
hi1.4xlarge
hs1.8xlarge
g2.2xlarge
Each Reserved Instance has an instance size footprint, which is determined by the normalization factor of the instance type and the number of instances in the reservation. When you modify a Reserved Instance, the footprint of the target configuration must match that of the original configuration, otherwise the modification request is not processed.

The normalization factor is based on instance size within the instance type (for example, m1.xlarge instances within the m1 instance type). This is only meaningful within the same instance type. Instance types cannot be modified from one type to another. In the Amazon EC2 console, this is measured in units. The following table illustrates the normalization factor that applies within an instance type.


Instance size	Normalization factor
nano
0.25
micro
0.5
small
1
medium
2
large
4
xlarge
8
2xlarge
16
4xlarge
32
8xlarge
64
10xlarge
80
16xlarge
128
32xlarge
256
To calculate the instance size footprint of a Reserved Instance, multiply the number of instances by the normalization factor. For example, an t2.medium has a normalization factor of 2 so a reservation for four t2.medium instances has a footprint of 8 units.

You can allocate your reservations into different instance sizes across the same instance type as long as the instance size footprint of your reservation remains the same. For example, you can divide a reservation for one t2.large (1 x 4) instance into four t2.small (4 x 1) instances, or you can combine a reservation for four t2.small instances into one t2.large instance. However, you cannot change your reservation for two t2.small (2 x 1) instances into one t2.large (1 x 4) instance. This is because the existing instance size footprint of your current reservation is smaller than the proposed reservation.

In the following example, you have a reservation with two t2.micro instances (giving you a footprint of 1) and a reservation with one t2.small instance (giving you a footprint of 1). You merge both reservations to a single reservation with one t2.medium instance—the combined instance size footprint of the two original reservations equals the footprint of the modified reservation.


						Modifying Reserved Instances
					
You can also modify a reservation to divide it into two or more reservations. In the following example, you have a reservation with a t2.medium instance. You divide the reservation into a reservation with two t2.nano instances and a reservation with three t2.micro instances.


						Modifying Reserved Instances
					
Submitting Modification Requests

You can modify your Standard Reserved Instances using the Amazon EC2 console, the Amazon EC2 API, or a command line tool.

Amazon EC2 Console

Before you modify your Reserved Instances, ensure that you have read the applicable restrictions. If you are modifying instance size, ensure that you've calculated the total instance size footprint of the reservations that you want to modify and ensure that it matches the total instance size footprint of your target configurations.

To modify your Reserved Instances using the AWS Management Console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Reserved Instances page, select one or more Reserved Instances to modify, and choose Modify Reserved Instances.

Note
If your Reserved Instances are not in the active state or cannot be modified, Modify Reserved Instances is disabled.
The first entry in the modification table displays attributes of selected Reserved Instances, and at least one target configuration beneath it. The Units column displays the total instance size footprint. Choose Add for each new configuration to add. Modify the attributes as needed for each configuration, and choose Continue when you're done:

Network: Choose whether the Reserved Instance applies to EC2-Classic or EC2-VPC. This option is only available if your account supports EC2-Classic.
Scope: Choose whether the Reserved Instance applies to an Availability Zone or to the whole region.
Availability Zone: Choose the required Availability Zone. Not applicable for regional Reserved Instances.
Instance Type: Select the required instance type. Only available for supported platforms. For more information, see Requirements and Restrictions for Modification.
Count: Specify the number of instances to be covered by the reservation.
Note
If your combined target configurations are larger or smaller than the instance size footprint of your original Reserved Instances, the allocated total in the Units column displays in red.
To confirm your modification choices when you finish specifying your target configurations, choose Submit Modifications. If you change your mind at any point, choose Cancel to exit the wizard.

You can determine the status of your modification request by looking at the State column in the Reserved Instances screen. The following table illustrates the possible State values.


State	Description
active (pending modification)
Transition state for original Reserved Instances.
retired (pending modification)
Transition state for original Reserved Instances while new Reserved Instances are being created.
retired
Reserved Instances successfully modified and replaced.
active
New Reserved Instances created from a successful modification request.

-Or-

Original Reserved Instances after a failed modification request.
Amazon EC2 API or Command Line Tool

To modify your Standard Reserved Instances, you can use one of the following:

modify-reserved-instances (AWS CLI)
Edit-EC2ReservedInstance (AWS Tools for Windows PowerShell)
ModifyReservedInstances (Amazon EC2 API)
To get the status of your modification, use one of the following:

describe-reserved-instances-modifications (AWS CLI)
Get-EC2ReservedInstancesModifications (AWS Tools for Windows PowerShell)
DescribeReservedInstancesModifications (Amazon EC2 API)
The state returned shows your request as processing, fulfilled, or failed.

Troubleshooting Modification Requests

If the target configuration settings that you requested were unique, you receive a message that your request is being processed. At this point, Amazon EC2 has only determined that the parameters of your modification request are valid. Your modification request can still fail during processing due to unavailable capacity.

In some situations, you might get a message indicating incomplete or failed modification requests instead of a confirmation. Use the information in such messages as a starting point for resubmitting another modification request. Ensure that you have read the applicable restrictions before submitting the request.

Not all selected Reserved Instances can be processed for modification

Amazon EC2 identifies and lists the Reserved Instances that cannot be modified. If you receive a message like this, go to the Reserved Instances page in the Amazon EC2 console and check the information for the Reserved Instances.

Error in processing your modification request

You submitted one or more Reserved Instances for modification and none of your requests can be processed. Depending on the number of reservations you are modifying, you can get different versions of the message.

Amazon EC2 displays the reasons why your request cannot be processed. For example, you might have specified the same target configuration—a combination of Availability Zone and platform—for one or more subsets of the Reserved Instances you are modifying. Try submitting the modification requests again, but ensure that the instance details of the reservations match, and that the target configurations for all subsets being modified are unique.

Exchanging Convertible Reserved Instances

You can exchange a Convertible Reserved Instance for another Convertible Reserved Instance with a different configuration, including instance family. There are no limits to how many times you perform an exchange, as long as the target Convertible Reserved Instance is of an equal or higher value than the Convertible Reserved Instance that you are exchanging.

When you exchange your Convertible Reserved Instance, the number of instances for your current reservation is exchanged for a number of instances that cover the equal or higher value of the configuration of the target Convertible Reserved Instance. Amazon EC2 calculates the number of Reserved Instances that you can receive as a result of the exchange.

Topics

Requirements for Exchanging Convertible Reserved Instances
Calculating Convertible Reserved Instances Exchanges
Submitting Exchange Requests
Requirements for Exchanging Convertible Reserved Instances

Amazon EC2 processes your exchange request if the following conditions are met.

Your Convertible Reserved Instance must be:

Active
Not pending a previous exchange request
Limitations:

Convertible Reserved Instances can only be exchanged for other Convertible Reserved Instances currently offered by AWS.
You can exchange one Convertible Reserved Instance at a time for one Convertible Reserved Instance only.
Convertible Reserved Instances cannot be modified. To change the reservation's configuration, exchange it for another one.
A Convertible Reserved Instance can only be exchanged with the same or higher payment option. For example, a Partial Upfront Convertible Reserved Instance can be exchanged for another Partial Upfront Convertible Reserved Instance or an All Upfront Convertible Reserved Instance—but it cannot be exchanged for a No Upfront Convertible Reserved Instance.
Calculating Convertible Reserved Instances Exchanges

Exchanging Convertible Reserved Instances is free. However, you may be required to pay a true-up cost, which is a prorated upfront cost of the difference between the Convertible Reserved Instances that you had and the Convertible Reserved Instances that you receive from the exchange.

Each Convertible Reserved Instance has a list value. This list value is compared to the list value of the Convertible Reserved Instances that you want in order to determine how many instance reservations you can receive from the exchange.

For example: You have 1 x $35-list value Convertible Reserved Instance that you want to exchange for a new instance type with a list value of $10.

Copy
$35/$10 = 3.5
You can exchange your Convertible Reserved Instance for three $10 Convertible Reserved Instances. It's not possible to purchase half reservations; therefore you must purchase an additional Convertible Reserved Instance covers the remainder:

Copy
3.5 = 3 whole Convertible Reserved Instances + 1 additional Convertible Reserved Instance.
The fourth Convertible Reserved Instance has the same end date as the other three. If you are exchanging Partial or All Upfront Convertible Reserved Instances, you pay the true-up cost for the fourth reservation. If the remaining upfront cost of your Convertible Reserved Instances is $500, and the target reservation would normally cost $600 on a prorated basis, you are charged $100.

Copy
$600 prorated upfront cost of new reservations - $500 remaining upfront cost of original reservations = $100 difference.
Submitting Exchange Requests

You can exchange your Convertible Reserved Instances using the Amazon EC2 console or a command line tool.

Topics

Amazon EC2 Console
Command Line Interface
Amazon EC2 Console

You can search for Convertible Reserved Instances offerings and select your new configuration from the choices provided.

To exchange Convertible Reserved Instances using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Reserved Instances, select the Convertible Reserved Instance to exchange, and choose Actions, Exchange Reserved Instance.

Select the attributes of the desired configuration using the drop-down menus, and choose Find Offering.

Select a new Convertible Reserved Instance The Instance Count column displays the number of Reserved Instances that you receive for the exchange. When you have selected a Convertible Reserved Instance that meets your needs, choose Exchange.

The Reserved Instances that were exchanged are retired, and the new Reserved Instances are displayed in the Amazon EC2 console. This process can take a few minutes to propagate.

Command Line Interface

To exchange a Convertible Reserved Instance, first find a target Convertible Reserved Instance that meets your needs:

describe-reserved-instances-offerings (AWS CLI)
Get-EC2ReservedInstancesOffering (Tools for Windows PowerShell)
Get a quote for the exchange, which includes the number of Reserved Instances you get from the exchange, and the true-up cost for the exchange:

get-reserved-instances-exchange-quote (AWS CLI)
GetEC2-ReservedInstancesExchangeQuote (Tools for Windows PowerShell)
Finally, perform the exchange:

accept-reserved-instances-exchange-quote (AWS CLI)
Confirm-EC2ReservedInstancesExchangeQuote (Tools for Windows PowerShell)

Scheduled Reserved Instances

Scheduled Reserved Instances (Scheduled Instances) enable you to purchase capacity reservations that recur on a daily, weekly, or monthly basis, with a specified start time and duration, for a one-year term. You reserve the capacity in advance, so that you know it is available when you need it. You pay for the time that the instances are scheduled, even if you do not use them.

Scheduled Instances are a good choice for workloads that do not run continuously, but do run on a regular schedule. For example, you can use Scheduled Instances for an application that runs during business hours or for batch processing that runs at the end of the week.

If you require a capacity reservation on a continuous basis, Reserved Instances might meet your needs and decrease costs. For more information, see Reserved Instances. If you are flexible about when your instances run, Spot instances might meet your needs and decrease costs. For more information, see Spot Instances.

Contents

How Scheduled Instances Work
Purchasing a Scheduled Instance
Launching a Scheduled Instance
Scheduled Instance Limits
How Scheduled Instances Work

Amazon EC2 sets aside pools of EC2 instances in each Availability Zone for use as Scheduled Instances. Each pool supports a specific combination of instance type, operating system, and network (EC2-Classic or EC2-VPC).

To get started, you must search for an available schedule. You can search across multiple pools or a single pool. After you locate a suitable schedule, purchase it.

You must launch your Scheduled Instances during their scheduled time periods, using a launch configuration that matches the following attributes of the schedule that you purchased: instance type, Availability Zone, network, and platform. When you do so, Amazon EC2 launches EC2 instances on your behalf, based on the specified launch specification. Amazon EC2 must ensure that the EC2 instances have terminated by the end of the current scheduled time period so that the capacity is available for any other Scheduled Instances it is reserved for. Therefore, Amazon EC2 terminates the EC2 instances three minutes before the end of the current scheduled time period.

You can't stop or reboot Scheduled Instances, but you can terminate them manually as needed. If you terminate a Scheduled Instance before its current scheduled time period ends, you can launch it again after a few minutes. Otherwise, you must wait until the next scheduled time period.

The following diagram illustrates the lifecycle of a Scheduled Instance.


                    The Scheduled Instance life cycle
                
Purchasing a Scheduled Instance

To purchase a Scheduled Instance, you can use the Scheduled Reserved Instances Reservation Wizard.

Warning
After you purchase a Scheduled Instance, you can't cancel, modify, or resell your purchase.
To purchase a Scheduled Instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under INSTANCES, choose Scheduled Instances.

Choose Purchase Scheduled Instances.

On the Find available schedules page, do the following:

Under Create a schedule, select the starting date from Starting on, the schedule recurrence (daily, weekly, or monthly) from Recurring, and the minimum duration from for duration. Note that the console ensures that you specify a value for the minimum duration that meets the minimum required utilization for your Scheduled Instance (1,200 hours per year).


                                The schedule for a Scheduled Instance
                            
Under Instance details, select the operating system and network from Platform. To narrow the results, select one or more instance types from Instance type or one or more Availability Zones from Availability Zone.


                                Instance details for a Scheduled Instance
                            
Choose Find schedules.

Under Available schedules, select one or more schedules. For each schedule that you select, set the quantity of instances and choose Add to Cart.

Your cart is displayed at the bottom of the page. When you are finished adding and removing schedules from your cart, choose Review and purchase.

On the Review and purchase page, verify your selections and edit them as needed. When you are finished, choose Purchase.

To purchase a Scheduled Instance using the AWS CLI

Use the describe-scheduled-instance-availability command to list the available schedules that meet your needs, and then use the purchase-scheduled-instances command to complete the purchase.

Launching a Scheduled Instance

After you purchase a Scheduled Instance, it is available for you to launch during its scheduled time periods.

To launch a Scheduled Instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under INSTANCES, choose Scheduled Instances.

Select the Scheduled Instance and choose Launch Scheduled Instances.

On the Configure page, complete the launch specification for your Scheduled Instances and choose Review.

Important
The launch specification must match the instance type, Availability Zone, network, and platform of the schedule that you purchased.
On the Review page, verify the launch configuration and modify it as needed. When you are finished, choose Launch.

To launch a Scheduled Instance using the AWS CLI

Use the describe-scheduled-instances command to list your Scheduled Instances, and then use the run-scheduled-instances command to launch each Scheduled Instance during its scheduled time periods.

Scheduled Instance Limits

Scheduled Instances are subject to the following limits:

The following are the only supported instance types: C3, C4, M4, and R3.
The required term is 365 days (one year).
The minimum required utilization is 1,200 hours per year.
You can purchase a Scheduled Instance up to three months in advance.

Spot Instances

Spot instances enable you to bid on unused EC2 instances, which can lower your Amazon EC2 costs significantly. The hourly price for a Spot instance (of each instance type in each Availability Zone) is set by Amazon EC2, and fluctuates depending on the supply of and demand for Spot instances. Your Spot instance runs whenever your bid exceeds the current market price.

Spot instances are a cost-effective choice if you can be flexible about when your applications run and if your applications can be interrupted. For example, Spot instances are well-suited for data analysis, batch jobs, background processing, and optional tasks. For more information, see Amazon EC2 Spot Instances.

The key differences between Spot instances and On-Demand instances are that Spot instances might not start immediately, the hourly price for Spot instances varies based on demand, and Amazon EC2 can terminate an individual Spot instance as the hourly price for, or availability of, Spot instances changes. One strategy is to launch a core group of On-Demand instances to maintain a minimum level of guaranteed compute resources for your applications, and supplement them with Spot instances when the opportunity arises.


				Compare On-Demand and Spot instances
			
Another strategy is to launch Spot instances with a required duration (also known as Spot blocks), which are not interrupted due to changes in the Spot price. For more information, see Specifying a Duration for Your Spot Instances.

Concepts

Before you get started with Spot instances, you should be familiar with the following concepts:

Spot instance pool—A set of unused EC2 instances with the same instance type, operating system, Availability Zone, and network platform (EC2-Classic or EC2-VPC).
Spot price—The current market price of a Spot instance per hour, which is set by Amazon EC2 based on the last fulfilled bid. You can also retrieve the Spot price history.
Spot instance request (or Spot bid)—Provides the maximum price (bid price) that you are willing to pay per hour for a Spot instance. When your bid price exceeds the Spot price, Amazon EC2 fulfills your request. Note that a Spot instance request is either one-time or persistent. Amazon EC2 automatically resubmits a persistent Spot request after the Spot instance associated with the request is terminated. Your Spot instance request can optionally specify a duration for the Spot instances.
Spot fleet—A set of Spot instances that is launched based on criteria that you specify. The Spot fleet selects the Spot instance pools that meet your needs and launches Spot instances to meet the target capacity for the fleet. By default Spot fleets are set to maintain target capacity by launching replacement instances after Spot instances in the fleet are terminated. They can also be submitted as a one-time request which does not persist once instances have been terminated.
Spot instance interruption—Amazon EC2 terminates your Spot instance when the Spot price exceeds your bid price or there are no longer any unused EC2 instances. Amazon EC2 marks the Spot instance for termination and provides a Spot instance termination notice, which gives the instance a two-minute warning before it terminates.
Bid status—Provides detailed information about the current state of your Spot bid.
How to Get Started

The first thing you need to do is get set up to use Amazon EC2. It can also be helpful to have experience launching On-Demand instances before launching Spot instances.

Get Up and Running

Setting Up with Amazon EC2
Getting Started with Amazon EC2 Linux Instances
Spot Basics

How Spot Instances Work
How Spot Fleet Works
Working with Spot Instances

Preparing for Interruptions
Creating a Spot Instance Request
Getting Bid Status Information
Working with Spot Fleets

Spot Fleet Prerequisites
Creating a Spot Fleet Request
Related Services

You can provision Spot instances directly using Amazon EC2. You can also provision Spot instances using other services in AWS. For more information, see the following documentation.

Auto Scaling and Spot instances
You can create launch configurations with a bid price so that Auto Scaling can launch Spot instances. For more information, see Launching Spot instances in Your Auto Scaling Group in the Auto Scaling User Guide.

Amazon EMR and Spot instances
There are scenarios where it can be useful to run Spot instances in an Amazon EMR cluster. For more information, see Lower Costs with Spot Instances in the Amazon EMR Developer Guide.

AWS CloudFormation Templates
AWS CloudFormation enables you to create and manage a collection of AWS resources using a template in JSON format. AWS CloudFormation templates can include a Spot price. For more information, see EC2 Spot Instance Updates - Auto Scaling and CloudFormation Integration.

AWS SDK for Java
You can use the Java programming language to manage your Spot instances. For more information, see Tutorial: Amazon EC2 Spot Instances and Tutorial: Advanced Amazon EC2 Spot Request Management.

AWS SDK for .NET
You can use the .NET programming environment to manage your Spot instances. For more information, see Tutorial: Amazon EC2 Spot instances.

Pricing

You pay the Spot price for Spot instances, which is set by Amazon EC2 and fluctuates periodically depending on the supply of and demand for Spot instances. If your bid price exceeds the current Spot price, Amazon EC2 fulfills your request and your Spot instances run until either you terminate them or the Spot price increases above your bid price.

Everyone pays that same Spot price for that period, regardless of whether their bid price was higher. You never pay more than your bid price per hour, and often pay less per hour. For example, if you bid $0.25 per hour, and the Spot price is $0.20 per hour, you only pay $0.20 per hour. If the Spot price drops, you pay the new, lower price. If the Spot price rises, you pay the new price if it is equal to or less than your bid price. If the Spot price rises above your bid price, then your Spot instance is interrupted.

At the start of each instance hour, you are charged based on the Spot price. If your Spot instance is interrupted in the middle of an instance hour because the Spot price exceeded your bid, you are not charged for the hour of use that was interrupted. However, if you terminate your Spot instance in the middle of an instance hour, you are charged for the hour.

Note that Spot instances with a predefined duration use a fixed hourly price that remains in effect for the Spot instance while it runs.

View Prices

To view the current (updated every five minutes) lowest Spot price per region and instance type, see the Spot Instances Pricing page.

To view the Spot price history for the past three months, use the Amazon EC2 console or the describe-spot-price-history command (AWS CLI). For more information, see Spot Instance Pricing History.

Note that we independently map Availability Zones to codes for each AWS account. Therefore, you can get different results for the same Availability Zone code (for example, us-west-2a) between different accounts.

View Billing

To review your bill, go to your AWS Account Activity page. Your bill contains links to usage reports that provide details about your bill. For more information, see AWS Account Billing.

If you have questions concerning AWS billing, accounts, and events, contact AWS Support.

How Spot Instances Work

To use Spot instances, create a Spot instance request or a Spot fleet request. The request includes the maximum price that you are willing to pay per hour per instance (your bid price), and other constraints such as the instance type and Availability Zone. If your bid price is greater than the current Spot price for the specified instance, and the specified instance is available, your request is fulfilled immediately. Otherwise, the request is fulfilled whenever the Spot price falls below your bid price or the specified instance becomes available. Spot instances run until you terminate them or until Amazon EC2 must terminate them (also known as a Spot instance interruption).

When you use Spot instances, you must be prepared for interruptions. Amazon EC2 can interrupt your Spot instance when the Spot price rises above your bid price, when the demand for Spot instances rises, or when the supply of Spot instances decreases. When Amazon EC2 marks a Spot instance for termination, it provides a Spot instance termination notice, which gives the instance a two-minute warning before it terminates. Note that you can't enable termination protection for Spot instances. For more information, see Spot Instance Interruptions.

Note that you can't stop and start an Amazon EBS-backed instance if it is a Spot instance, but you can reboot or terminate it.

Shutting down a Spot instance on OS-level results in the Spot instance being terminated. It is not possible to change this behavior.

Contents

Supply and Demand in the Spot Market
Launching Spot Instances in a Launch Group
Launching Spot Instances in an Availability Zone Group
Launching Spot Instances in a VPC
Supply and Demand in the Spot Market

AWS continuously evaluates how many Spot instances are available in each Spot instance pool, monitors the bids that have been made for each pool, and provisions the available Spot instances to the highest bidders. The Spot price for a pool is set to the lowest fulfilled bid for that pool. Therefore, the Spot price is the price above which you must bid to fulfill a Spot request for a single Spot instance immediately.

For example, suppose that you create a Spot instance request, and that the corresponding Spot instance pool has only five Spot instances for sale. Your bid price is $0.10, which is also the current Spot price. The following table shows the current bids, ranked in descending order. Bids 1-5 are fulfilled. Bid 5, being the last fulfilled bid, sets the Spot price at $0.10. Bid 6 is unfulfilled. Bids 3-5, which share the same bid price of $0.10, are ranked in random order.

Bid	Bid price	Current Spot price	Notes
1
$1.00
$0.10
2
$1.00
$0.10
3
$0.10
$0.10
4
$0.10
$0.10	
Your bid
5
$0.10
$0.10	
Last fulfilled bid, which sets the Spot price. Everyone pays the same Spot price for the period.
— — —
— — —
Spot capacity cutoff
6
$0.05
Now, let's say that the size of this pool drops to 3. Bids 1-3 are fulfilled. Bid 3, the last fulfilled bid, sets the Spot price at $0.10. Bids 4-5, which also are $0.10, are unfulfilled. As you can see, even though the Spot price didn't change, two of the bids, including your bid, are no longer fulfilled because the Spot supply decreased.

Bid	Bid price	Current Spot price	Notes
1
$1.00
$0.10
2
$1.00
$0.10
3
$0.10
$0.10	
Last fulfilled bid, which sets the Spot price. Everyone pays the same Spot price for the period.
— — —
— — —
Spot capacity cutoff
4
$0.10
Your bid
5
$0.10
6
$0.05
To fulfill a Spot request for a single instance from this pool, you must bid above the current Spot price of $0.10. If you bid $0.101, your request will be fulfilled, the Spot instance for bid 3 would be interrupted, and the Spot price would become $0.101. If you bid $2.00, the Spot instance for bid 3 would be interrupted and the Spot price would become $1.00 (the price for bid 2).

Keep in mind that no matter how high you bid, you can never get more than the available number of Spot instances in a Spot instance pool. If the size of the pool drops to zero, then all the Spot instances from that pool would be interrupted.

Launching Spot Instances in a Launch Group

Specify a launch group in your Spot instance request to tell Amazon EC2 to launch a set of Spot instances only if it can launch them all. In addition, if the Spot service must terminate one of the instances in a launch group (for example, if the Spot price rises above your bid price), it must terminate them all. However, if you terminate one or more of the instances in a launch group, Amazon EC2 does not terminate the remaining instances in the launch group.

Note that although this option can be useful, adding this constraint can lower the chances that your Spot instance request is fulfilled. It can also increase the chance that your Spot instances will be terminated.

If you create another successful Spot instance request that specifies the same (existing) launch group as an earlier successful request, then the new instances are added to the launch group. Subsequently, if an instance in this launch group is terminated, all instances in the launch group are terminated, which includes instances launched by the first and second requests.

Launching Spot Instances in an Availability Zone Group

Specify an Availability Zone group in your Spot instance request to tell the Spot service to launch a set of Spot instances in the same Availability Zone. Note that Amazon EC2 need not terminate all instances in an Availability Zone group at the same time. If Amazon EC2 must terminate one of the instances in an Availability Zone group, the others remain running.

Note that although this option can be useful, adding this constraint can lower the chances that your Spot instance request is fulfilled.

If you specify an Availability Zone group but don't specify an Availability Zone in the Spot instance request, the result depends on whether you specified the EC2-Classic network, a default VPC, or a nondefault VPC. For more information about EC2-Classic and EC2-VPC, see Supported Platforms.

EC2-Classic

Amazon EC2 finds the lowest-priced Availability Zone in the region and launches your Spot instances in that Availability Zone if the lowest bid for the group is higher than the current Spot price in that Availability Zone. Amazon EC2 waits until there is enough capacity to launch your Spot instances together, as long as the Spot price remains lower than the lowest bid for the group.

Default VPC

Amazon EC2 uses the Availability Zone for the specified subnet, or if you don't specify a subnet, it selects an Availability Zone and its default subnet, but it might not be the lowest-priced Availability Zone. If you deleted the default subnet for an Availability Zone, then you must specify a different subnet.

Nondefault VPC

Amazon EC2 uses the Availability Zone for the specified subnet.

Launching Spot Instances in a VPC

To take advantage of the features of EC2-VPC when you use Spot instances, specify in your Spot request that your Spot instances are to be launched in a VPC. You specify a subnet for your Spot instances the same way that you specify a subnet for your On-Demand instances.

The process for making a Spot instance request that launches Spot instances in a VPC is the same as the process for making a Spot instance request that launches Spot instances in EC2-Classic—except for the following differences:

You should base your bid on the Spot price history of Spot instances in a VPC.
[Default VPC] If you want your Spot instance launched in a specific low-priced Availability Zone, you must specify the corresponding subnet in your Spot instance request. If you do not specify a subnet, Amazon EC2 selects one for you, and the Availability Zone for this subnet might not have the lowest Spot price.
[Nondefault VPC] You must specify the subnet for your Spot instance.

How Spot Fleet Works

A Spot fleet is a collection, or fleet, of Spot instances. The Spot fleet attempts to launch the number of Spot instances that are required to meet the target capacity that you specified in the Spot fleet request. The Spot fleet also attempts to maintain its target capacity fleet if your Spot instances are interrupted due to a change in Spot prices or available capacity.

A Spot instance pool is a set of unused EC2 instances with the same instance type, operating system, Availability Zone, and network platform (EC2-Classic or EC2-VPC). When you make a Spot fleet request, you can include multiple launch specifications, that vary by instance type, AMI, Availability Zone, or subnet. The Spot fleet selects the Spot instance pools that are used to fulfill the request, based on the launch specifications included in your Spot fleet request, and the configuration of the Spot fleet request. The Spot instances come from the selected pools.

Contents

Spot Fleet Allocation Strategy
Spot Price Overrides
Spot Fleet Instance Weighting
Walkthrough: Using Spot Fleet with Instance Weighting
Spot Fleet Allocation Strategy

The allocation strategy for your Spot fleet determines how it fulfills your Spot fleet request from the possible Spot instance pools represented by its launch specifications. The following are the allocation strategies that you can specify in your Spot fleet request:

lowestPrice
The Spot instances come from the pool with the lowest price. This is the default strategy.

diversified
The Spot instances are distributed across all pools.

Choosing an Allocation Strategy

You can optimize your Spot fleets based on your use case.

If your fleet is small or runs for a short time, the probability that your Spot instances will be interrupted is low, even with all the instances in a single Spot instance pool. Therefore, the lowestPrice strategy is likely to meet your needs while providing the lowest cost.

If your fleet is large or runs for a long time, you can improve the availability of your fleet by distributing the Spot instances across multiple pools. For example, if your Spot fleet request specifies 10 pools and a target capacity of 100 instances, the Spot fleet launches 10 Spot instances in each pool. If the Spot price for one pool increases above your bid price for this pool, only 10% of your fleet is affected. Using this strategy also makes your fleet less sensitive to increases in the Spot price in any one pool over time.

Note that with the diversified strategy, the Spot fleet does not launch Spot instances into any pools with a Spot price that is equal to or higher than the On-Demand price.

Maintaining Target Capacity

After Spot instances are terminated due to a change in the Spot price or available capacity of a Spot instance pool, the Spot fleet launches replacement Spot instances. If the allocation strategy is lowestPrice, the Spot fleet launches replacement instances in the pool where the Spot price is currently the lowest. If the allocation strategy is diversified, the Spot fleet distributes the replacement Spot instances across the remaining pools.

Spot Price Overrides

Each Spot fleet request must include a global Spot price. By default, the Spot fleet uses this price as the bid price for each of its launch specifications.

You can optionally specify a Spot price in one or more launch specifications. This bid price is specific to the launch specification. If a launch specification includes a specific Spot price, the Spot fleet uses this price as the bid price for that launch specification, overriding the global Spot price. Note that any other launch specifications that do not include a specific Spot price still use the global Spot price.

Spot Fleet Instance Weighting

When you request a fleet of Spot instances, you can define the capacity units that each instance type would contribute to your application's performance, and adjust your bid price for each Spot instance pool accordingly using instance weighting.

By default, the Spot price that you specify represents your bid price per instance hour. When you use the instance weighting feature, the Spot price that you specify represents your bid price per unit hour. You can calculate your bid price per unit hour by dividing your bid price for an instance type by the number of units that it represents. The Spot fleet calculates the number of Spot instances to launch by dividing the target capacity by the instance weight. If the result isn't an integer, the Spot fleet rounds it up to the next integer, so that the size of your fleet is not below its target capacity. Note that Spot fleet can select any pool that you specify in your launch specification, even if the capacity of the instances launched exceeds the requested target capacity.

The following table includes examples of calculations to determine the bid price per unit for a Spot fleet request with a target capacity of 10.


Instance type	Instance weight	Spot price per instance hour	Spot price per unit hour	Number of instances launched
r3.xlarge
2
$0.05
.025

(.05 divided by 2)
5

(10 divided by 2)
r3.8xlarge
8
$0.10
.0125

(.10 divided by 8)
2

(10 divided by 8, result rounded up)
Use Spot fleet instance weighting as follows to provision the target capacity you want in the pools with the lowest price per unit at the time of fulfillment:

Set the target capacity for your Spot fleet either in instances (the default) or in the units of your choice, such as virtual CPUs, memory, storage, or throughput.

Set the bid price per unit.

For each launch configuration, specify the weight, which is the number of units that the instance type represents toward the target capacity.

Instance Weighting Example

Consider a Spot fleet request with the following configuration:

A target capacity of 24
A launch specification with an instance type r3.2xlarge and a weight of 6
A launch specification with an instance type c3.xlarge and a weight of 5
The weights represent the number of units that instance type represents toward the target capacity. If the first launch specification provides the lowest Spot price per unit (Spot price for r3.2xlarge per instance hour divided by 6), the Spot fleet would launch four of these instances (24 divided by 6).

If the second launch specification provides the lowest Spot price per unit (Spot price for c3.xlarge per instance hour divided by 5), the Spot fleet would launch five of these instances (24 divided by 5, result rounded up).

Instance Weighting and Allocation Strategy

Consider a Spot fleet request with the following configuration:

A target capacity of 30
A launch specification with an instance type c3.2xlarge and a weight of 8
A launch specification with an instance type m3.xlarge and a weight of 8
A launch specification with an instance type r3.xlarge and a weight of 8
The Spot fleet would launch four instances (30 divided by 8, result rounded up). With the lowestPrice strategy, all four instances come from the pool that provides the lowest Spot price per unit. With the diversified strategy, the Spot fleet launches 1 instance in each of the three pools, and the fourth instance in whichever of the three pools provides the lowest Spot price per unit.

Walkthrough: Using Spot Fleet with Instance Weighting

This walkthrough uses a fictitious company called Example Corp to illustrate the process of bidding for a Spot fleet using instance weighting.

Objective

Example Corp, a pharmaceutical company, wants to leverage the computational power of Amazon EC2 for screening chemical compounds that might be used to fight cancer.

Planning

Example Corp first reviews Spot Best Practices. Next, Example Corp determines the following requirements for their Spot fleet.

Instance Types

Example Corp has a compute- and memory-intensive application that performs best with at least 60 GB of memory and eight virtual CPUs (vCPUs). They want to maximize these resources for the application at the lowest possible price. Example Corp decides that any of the following EC2 instance types would meet their needs:

Instance type	Memory (GiB)	vCPUs
r3.2xlarge
61
8
r3.4xlarge
122
16
r3.8xlarge
244
32
Target Capacity in Units

With instance weighting, target capacity can equal a number of instances (the default) or a combination of factors such as cores (vCPUs), memory (GiBs), and storage (GBs). By considering the base for their application (60 GB of RAM and eight vCPUs) as 1 unit, Example Corp decides that 20 times this amount would meet their needs. So the company sets the target capacity of their Spot fleet request to 20.

Instance Weights

After determining the target capacity, Example Corp calculates instance weights. To calculate the instance weight for each instance type, they determine the units of each instance type that are required to reach the target capacity as follows:

r3.2xlarge (61.0 GB, 8 vCPUs) = 1 unit of 20
r3.4xlarge (122.0 GB, 16 vCPUs) = 2 units of 20
r3.8xlarge (244.0 GB, 32 vCPUs) = 4 units of 20
Therefore, Example Corp assigns instance weights of 1, 2, and 4 to the respective launch configurations in their Spot fleet request.

Bid Price Per Unit Hour

Example Corp uses the On-Demand price per instance hour as a starting point for their bid price. They could also use recent Spot prices, or a combination of the two. To calculate bid price per unit hour, they divide their starting bid price per instance hour by the weight. For example:

Instance type	On-Demand price	Instance weight	Price per unit hour
r3.2xLarge
$0.7
1
$0.7
r3.4xLarge
$1.4
2
$0.7
r3.8xLarge
$2.8
4
$0.7
Example Corp could enter a global bid price per unit hour of $0.7 and be competitive for all three instance types. They could also enter a global bid price per unit hour of $0.7 and a specific bid price per unit hour of $0.9 in the r3.8xlarge launch specification. Depending on the strategy for provisioning their Spot fleet, Example Corp could bid lower to further reduce costs, or bid higher to reduce the probability of interruption.

Verifying Permissions

Before creating a Spot fleet request, Example Corp verifies that it has an IAM role with the required permissions. For more information, see Spot Fleet Prerequisites.

Creating the Request

Example Corp creates a file, config.json, with the following configuration for its Spot fleet request:

Copy
{
  "SpotPrice": "0.70",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
    {
      "ImageId": "ami-1a2b3c4d",
      "InstanceType": "r3.2xlarge",
      "SubnetId": "subnet-482e4972",
      "WeightedCapacity": 1
    },
    {
      "ImageId": "ami-1a2b3c4d",
      "InstanceType": "r3.4xlarge",
      "SubnetId": "subnet-482e4972",
      "WeightedCapacity": 2
    }
    {
      "ImageId": "ami-1a2b3c4d",
      "InstanceType": "r3.8xlarge",
      "SubnetId": "subnet-482e4972",
      "SpotPrice": "0.90",
      "WeightedCapacity": 4
    }
  ]
}
Example Corp creates the Spot fleet request using the following request-spot-fleet command:

Copy
aws ec2 request-spot-fleet --spot-fleet-request-config file://config.json
For more information, see Spot Fleet Requests.

Fulfillment

The allocation strategy determines which Spot instance pools your Spot instances come from.

With the lowestPrice strategy (which is the default strategy), the Spot instances come from the pool with the lowest Spot price per unit at the time of fulfillment. To provide 20 units of capacity, the Spot fleet launches either 20 r3.2xlarge instances (20 divided by 1), 10 r3.4xlarge instances (20 divided by 2), or 5 r3.8xlarge instances (20 divided by 4).

If Example Corp used the diversified strategy, the Spot instances would come from all three pools. The Spot fleet would launch 6 r3.2xlarge instances (which provide 6 units), 3 r3.4xlarge instances (which provide 6 units), and 2 r3.8xlarge instances (which provide 8 units), for a total of 20 units.

Spot Instance Pricing History

The Spot price represents the price above which you have to bid to guarantee that a single Spot request is fulfilled. When your bid price is above the Spot price, Amazon EC2 launches your Spot instance, and when the Spot price rises above your bid price, Amazon EC2 terminates your Spot instance. You can bid above the current Spot price so that your Spot request is fulfilled quickly. However, before you specify a bid price for your Spot instance, we recommend that you review the Spot price history. You can view the Spot price history for the last 90 days, filtering by instance type, operating system, and Availability Zone.

Using the Spot price history as a guide, you can select a bid price that would have met your needs in the past. For example, you can determine which bid price that would have provided 75 percent uptime in the time range you viewed. However, keep in mind that the historical trends are not a guarantee of future results. Spot prices vary based on real-time supply and demand, and the conditions that generated certain patterns in the Spot price might not occur in the future.

To view the Spot price history using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the navigation pane, choose Spot Requests.

If you are new to Spot instances, you see a welcome page; choose Get started, scroll to the bottom of the screen, and then choose Cancel.

Choose Pricing History. By default, the page displays a graph of the data for Linux t1.micro instances in all Availability Zones over the past day. Move your mouse over the graph to display the prices at specific times in the table below the graph.


							The Spot Instance Pricing History tool in
								the Amazon EC2 console.
						
(Optional) To review the Spot price history for a specific Availability Zone, select an Availability Zone from the list. You can also select a different product, instance type, or date range.

To view the Spot price history using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-spot-price-history (AWS CLI)
Get-EC2SpotPriceHistory (AWS Tools for Windows PowerShell)

Spot Instance Requests

To use Spot instances, you create a Spot instance request that includes the number of instances, the instance type, the Availability Zone, and the maximum price that you are willing to pay per instance hour (your bid). If your bid exceeds the current Spot price, Amazon EC2 fulfills your request immediately. Otherwise, Amazon EC2 waits until your request can be fulfilled or until you cancel the request.

The following illustration shows how Spot requests work. Notice that the action taken for a Spot instance interruption depends on the request type (one-time or persistent). If the request is a persistent request, the request is opened again after your Spot instance is terminated.


					The Spot life cycle
				
Contents

Spot Instance Request States
Specifying a Duration for Your Spot Instances
Specifying a Tenancy for Your Spot Instances
Creating a Spot Instance Request
Finding Running Spot Instances
Tagging Spot Instance Requests
Cancelling a Spot Instance Request
Spot Request Example Launch Specifications
Spot Instance Request States

A Spot instance request can be in one of the following states:

open—The request is waiting to be fulfilled.
active—The request is fulfilled and has an associated Spot instance.
failed—The request has one or more bad parameters.
closed—The Spot instance was interrupted or terminated.
cancelled—You cancelled the request, or the request expired.
The following illustration represents the transitions between the request states. Notice that the transitions depend on the request type (one-time or persistent).


						Spot request states
					
A one-time Spot instance request remains active until Amazon EC2 launches the Spot instance, the request expires, or you cancel the request. If the Spot price rises above your bid price, your Spot instance is terminated and the Spot instance request is closed.

A persistent Spot instance request remains active until it expires or you cancel it, even if the request is fulfilled. For example, if you create a persistent Spot instance request for one instance when the Spot price is $0.25, Amazon EC2 launches your Spot instance if your bid price is above $0.25. If the Spot price rises above your bid price, your Spot instance is terminated; however, the Spot instance request is open again and Amazon EC2 launches a new Spot instance when the Spot price falls below your bid price.

You can track the status of your Spot instance requests, as well as the status of the Spot instances launched, through the bid status. For more information, see Spot Bid Status.

Specifying a Duration for Your Spot Instances

Amazon EC2 does not terminate Spot instances with a specified duration (also known as Spot blocks) when the Spot price changes. This makes them ideal for jobs that take a finite time to complete, such as batch processing, encoding and rendering, modeling and analysis, and continuous integration.

You can specify a duration of 1, 2, 3, 4, 5, or 6 hours. The price that you pay depends on the specified duration. To view the current prices for a 1 hour duration or a 6 hour duration, see Spot Instance Prices. You can use these prices to estimate the cost of the 2, 3, 4, and 5 hour durations. When a request with a duration is fulfilled, the price for your Spot instance is fixed, and this price remains in effect until the instance terminates. You are billed at this price for each hour or partial hour that the instance is running. Note that a partial instance hour is billed as a full hour.

When you specify a duration in your Spot request, the duration period for each Spot instance starts as soon as the instance receives its instance ID. The Spot instance runs until you terminate it or the duration period ends. At the end of the duration period, Amazon EC2 marks the Spot instance for termination and provides a Spot instance termination notice, which gives the instance a two-minute warning before it terminates.

To launch Spot instances with a specified duration using the console

Select the appropriate request type. For more information, see Creating a Spot Instance Request.

To launch Spot instances with a specified duration using the AWS CLI

To specify a duration for your Spot instances, include the --block-duration-minutes option with the request-spot-instances command. For example, the following command creates a Spot request that launches Spot instances that run for two hours:

Copy
aws ec2 request-spot-instances --spot-price "0.050" --instance-count 5 --block-duration-minutes 120 --type "one-time" --launch-specification file://specification.json
To retrieve the cost for Spot instances with a specified duration using the AWS CLI

Use the describe-spot-instance-requests command to retrieve the fixed cost for your Spot instances with a specified duration. The information is in the actualBlockHourlyPrice field.

Specifying a Tenancy for Your Spot Instances

You can run a Spot instance on single-tenant hardware. Dedicated Spot instances are physically isolated from instances that belong to other AWS accounts. For more information, see Dedicated Instances and the Amazon EC2 Dedicated Instances product page.

To run a Dedicated Spot instance, do one of the following:

Specify a tenancy of dedicated when you create the Spot instance request. For more information, see Creating a Spot Instance Request.
Request a Spot instance in a VPC with an instance tenancy of dedicated. For more information, see Creating a VPC with an Instance Tenancy of Dedicated. Note that you cannot request a Spot instance with a tenancy of default if you request it in a VPC with an instance tenancy of dedicated.
The following instance types support Dedicated Spot instances.

Current Generation

c3.8xlarge
c4.8xlarge
d2.8xlarge
g2.8xlarge
i2.8xlarge
m4.10xlarge
m4.16xlarge
p2.16xlarge
r3.8xlarge
r4.16xlarge
x1.32xlarge
Previous Generation

cc2.8xlarge
cg1.4xlarge
cr1.8xlarge
hi1.4xlarge
Creating a Spot Instance Request

The process for requesting a Spot instance is similar to the process for launching an On-Demand instance. Note that you can't change the parameters of your Spot request, including the bid price, after you've submitted the request.

If you request multiple Spot instances at one time, Amazon EC2 creates separate Spot instance requests so that you can track the status of each request separately. For more information about tracking Spot requests, see Spot Bid Status.

Prerequisites

Before you begin, decide on your bid price, how many Spot instances you'd like, and what instance type to use. To review Spot price trends, see Spot Instance Pricing History.

To create a Spot instance request using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the navigation pane, choose Spot Requests.

If you are new to Spot instances, you see a welcome page; choose Get started. Otherwise, choose Request Spot Instances.

On the Find instance types page, do the following:

For Request type, the default is a one-time Spot request created using a Spot fleet. For more information, see Spot Fleet Requests. To use Spot blocks instead, select Reserve for duration.

For Target capacity, enter the number of units to request. You can choose instances or performance characteristics that are important to your application workload, such as vCPUs, memory, and storage.

[Spot block] For Reserved duration, select the number of hours for the job to complete.

For AMI, choose one of the basic Amazon Machine Images (AMI) provided by AWS, or choose Use custom AMI to specify your own AMI.

For Instance type(s), choose Select. Select the instance types that have the minimum hardware specifications that you need (vCPUs, memory, and storage).

[Spot fleet] For Allocation strategy, choose the strategy that meets your needs. For more information, see Spot Fleet Allocation Strategy.

For Network, your account supports either the EC2-Classic and EC2-VPC platforms, or the EC2-VPC platform only. To find out which platforms your account supports, see Supported Platforms.

[Existing VPC] Select the VPC.

[New VPC] Select Create new VPC to go the Amazon VPC console. When you are done, return to the wizard and refresh the list.

[EC2-Classic] Select EC2-Classic.

(Optional) For Availability Zones, the default is to let AWS choose the Availability Zones for your Spot instances. If you prefer, you can specify specific Availability Zones.

[EC2-VPC] Select one or more Availability Zones. If you have more than one subnet in an Availability Zone, select the appropriate subnet from Subnet. To add subnets, select Create new subnet to go to the Amazon VPC console. When you are done, return to the wizard and refresh the list.

[EC2-Classic] Select Select specific zone/subnet, and then select one or more Availability Zones.

[Spot fleet] For Maximum price, you can use automated bidding or specify a bid price. Your Spot instances are not launched if your bid price is lower than the Spot price for the instance types that you selected.

Choose Next.

On the Configure page, do the following:

(Optional) To add storage, specify additional instance store volumes or EBS volumes, depending on the instance type. You can also enable EBS optimization.

(Optional) By default, basic monitoring is enabled for your instances. To enable detailed monitoring, select Enable CloudWatch detailed monitoring.

(Optional) To run a Dedicated Spot instance, choose Dedicated - run a dedicated instance for Tenancy.

(Optional) To run a start-up script, copy it to User data.

[Spot fleet] To add a tag, choose Add new tag and type the key and value for the tag. Repeat for each tag.

(Optional) If you need to connect to your instances, specify your key pair using Key pair name.

(Optional) To launch your Spot instances with an IAM role, specify it using IAM instance profile.

For Security groups, select one or more security groups.

[EC2-VPC] If you need to connect to your instances in a VPC, you can enable Auto-assign IPv4 Public IP.

By default, the request remains in effect until it is fulfilled or you cancel it. To create a request that is valid only during a specific time period, edit Request valid from and Request valid to.

[Spot fleet] By default, we terminate your Spot instances when the request expires. To keep them running after your request expires, clear Terminate instances at expiration.

Choose Review.

On the Review page, verify the launch configuration. To make changes, choose Previous. To download a copy of the launch configuration for use with the AWS CLI, choose JSON config. When you are ready, choose Launch.

On the confirmation page, choose OK.

[Spot fleet] The request type is fleet. When the request is fulfilled, requests of type instance are added, where the state is active and the status is fulfilled.

[Spot block] The request type is block and the initial state is open. When the request is fulfilled, the state is active and the status is fulfilled.

To create a Spot instance request using the AWS CLI

Use the following request-spot-instances command to create a one-time request:

Copy
aws ec2 request-spot-instances --spot-price "0.05" --instance-count 5 --type "one-time" --launch-specification file://specification.json
Use the following request-spot-instances command to create a persistent request:

Copy
aws ec2 request-spot-instances --spot-price "0.05" --instance-count 5 --type "persistent" --launch-specification file://specification.json
For example launch specification files, see Spot Request Example Launch Specifications.

Amazon EC2 launches your Spot instance when the Spot price is below your bid. The Spot instance runs until either it is interrupted, or you terminate it yourself. Use the following describe-spot-instance-requests command to monitor your Spot instance request:

Copy
aws ec2 describe-spot-instance-requests --spot-instance-request-ids sir-08b93456
Finding Running Spot Instances

Amazon EC2 launches a Spot instance when the Spot price is below your bid. A Spot instance runs until either its bid price is no longer higher than the Spot price, or you terminate it yourself. (If your bid price is exactly equal to the Spot price, there is a chance that your Spot instance will remain running, depending on demand.)

To find running Spot instances using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Spot Requests.

You can see both Spot instance requests and Spot fleet requests. If a Spot instance request has been fulfilled, Capacity is the ID of the Spot instance. For a Spot fleet, Capacity indicates how much of the requested capacity has been fulfilled. To view the IDs of the instances in a Spot fleet, choose the expand arrow, or select the fleet and then select the Instances tab.

Alternatively, in the navigation pane, choose Instances. In the top right corner, choose the Show/Hide icon, and then select Lifecycle. For each instance, Lifecycle is either normal, spot, or scheduled.

To find running Spot instances using the AWS CLI

To enumerate your Spot instances, use the describe-spot-instance-requests command with the --query option as follows:

Copy
aws ec2 describe-spot-instance-requests --query SpotInstanceRequests[*].{ID:InstanceId}
The following is example output:

[
    {
        "ID": "i-1234567890abcdef0"
    },
    {
        "ID": "i-0598c7d356eba48d7"
    }
]
Alternatively, you can enumerate your Spot instances using the describe-instances command with the --filters option as follows:

Copy
aws ec2 describe-instances --filters "Name=instance-lifecycle,Values=spot"
Tagging Spot Instance Requests

To help categorize and manage your Spot instance requests, you can tag them with metadata of your choice. For more information, see Tagging Your Amazon EC2 Resources.

You can assign a tag to a Spot instance request after you create it. The tags that you create for your Spot instance requests only apply to the requests. These tags are not added automatically to the Spot instance that the Spot service launches to fulfill the request. You must add tags to a Spot instance yourself after the Spot instance is launched.

To add a tag to your Spot instance request or Spot instance using the AWS CLI

Use the following create-tags command to tag your resources:

Copy
aws ec2 create-tags --resources sir-08b93456 i-1234567890abcdef0 --tags Key=purpose,Value=test
Cancelling a Spot Instance Request

If you no longer want your Spot request, you can cancel it. You can only cancel Spot instance requests that are open or active. Your Spot request is open when your request has not yet been fulfilled and no instances have been launched. Your Spot request is active when your request has been fulfilled, and Spot instances have launched as a result. If your Spot request is active and has an associated running Spot instance, cancelling the request does not terminate the instance; you must terminate the running Spot instance manually.

If the Spot request is a persistent Spot request, it returns to the open state so that a new Spot instance can be launched. To cancel a persistent Spot request and terminate its Spot instances, you must cancel the Spot request first and then terminate the Spot instances. Otherwise, the Spot request can launch a new instance.

To cancel a Spot instance request using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Spot Requests, and then select the Spot request.

Choose Actions, and then choose Cancel spot request.

(Optional) If you are finished with the associated Spot instances, you can terminate them. In the navigation pane, choose Instances, select the instance, choose Actions, choose Instance State, and then choose Terminate.

To cancel a Spot instance request using the AWS CLI

Use the following cancel-spot-instance-requests command to cancel the specified Spot request:

Copy
aws ec2 cancel-spot-instance-requests --spot-instance-request-ids sir-08b93456
If you are finished with the associated Spot instances, you can terminate them manually using the following terminate-instances command:

Copy
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0 i-0598c7d356eba48d7

Spot Request Example Launch Specifications

The following examples show launch configurations that you can use with the request-spot-instances command to create a Spot instance request. For more information, see Creating a Spot Instance Request.

Launch Spot instances

Launch Spot instances in the specified Availability Zone

Launch Spot instances in the specified subnet

Launch a Dedicated Spot instance

Example 1: Launch Spot Instances

The following example does not include an Availability Zone or subnet. Amazon EC2 selects an Availability Zone for you. If your account supports EC2-VPC only, Amazon EC2 launches the instances in the default subnet of the selected Availability Zone. If your account supports EC2-Classic, Amazon EC2 launches the instances in EC2-Classic in the selected Availability Zone.

Copy
{
  "ImageId": "ami-1a2b3c4d",
  "KeyName": "my-key-pair",
  "SecurityGroupIds": [ "sg-1a2b3c4d" ],
  "InstanceType": "m3.medium",
  "IamInstanceProfile": {
      "Arn": "arn:aws:iam::123456789012:instance-profile/my-iam-role"
  }
}
Note that you can specify security groups for EC2-Classic either by ID or by name (using the SecurityGroups field). You must specify security groups for EC2-VPC by ID.

Example 2: Launch Spot Instances in the Specified Availability Zone

The following example includes an Availability Zone. If your account supports EC2-VPC only, Amazon EC2 launches the instances in the default subnet of the specified Availability Zone. If your account supports EC2-Classic, Amazon EC2 launches the instances in EC2-Classic in the specified Availability Zone.

Copy
{
  "ImageId": "ami-1a2b3c4d",
  "KeyName": "my-key-pair",
  "SecurityGroupIds": [ "sg-1a2b3c4d" ],
  "InstanceType": "m3.medium",
  "Placement": {
    "AvailabilityZone": "us-west-2a"
  },
  "IamInstanceProfile": {
      "Arn": "arn:aws:iam::123456789012:instance-profile/my-iam-role"
  }
}
Example 3: Launch Spot Instances in the Specified Subnet

The following example includes a subnet. Amazon EC2 launches the instances in the specified subnet. If the VPC is a nondefault VPC, the instance does not receive a public IPv4 address by default.

Copy
{
  "ImageId": "ami-1a2b3c4d",
  "SecurityGroupIds": [ "sg-1a2b3c4d" ],
  "InstanceType": "m3.medium",
  "SubnetId": "subnet-1a2b3c4d",
  "IamInstanceProfile": {
      "Arn": "arn:aws:iam::123456789012:instance-profile/my-iam-role"
  }
}
To assign a public IPv4 address to an instance in a nondefault VPC, specify the AssociatePublicIpAddress field as shown in the following example. Note that when you specify a network interface, you must include the subnet ID and security group ID using the network interface, rather than using the SubnetId and SecurityGroupIds fields shown in example 3.

Copy
{
  "ImageId": "ami-1a2b3c4d",
  "KeyName": "my-key-pair",
  "InstanceType": "m3.medium",
  "NetworkInterfaces": [
    {
      "DeviceIndex": 0,
      "SubnetId": "subnet-1a2b3c4d",
      "Groups": [ "sg-1a2b3c4d" ],
      "AssociatePublicIpAddress": true
    }
  ],
  "IamInstanceProfile": {
      "Arn": "arn:aws:iam::123456789012:instance-profile/my-iam-role"
  }
}
Example 4: Launch a Dedicated Spot Instance

The following example requests Spot instance with a tenancy of dedicated. A Dedicated Spot instance must be launched in a VPC.

Copy
{
  "ImageId": "ami-1a2b3c4d",
  "KeyName": "my-key-pair",
  "SecurityGroupIds": [ "sg-1a2b3c4d" ],
  "InstanceType": "c3.8xlarge",
  "SubnetId": "subnet-1a2b3c4d",
  "Placement": {
    "Tenancy": "dedicated"
  }
}

Spot Fleet Requests

To use a Spot fleet, you create a Spot fleet request that includes the target capacity, one or more launch specifications for the instances, and the bid price that you are willing to pay. Amazon EC2 attempts to maintain your Spot fleet's target capacity as Spot prices change. For more information, see How Spot Fleet Works.

You can create a Spot fleet to submit a one-time request for your desired capacity, or require it to maintain a target capacity over time. Both types of requests benefit from Spot fleet's allocation strategy.

When you request a target capacity, Spot fleet places the required bids but will not attempt to replenish Spot instances if capacity is diminished. If capacity is not available, Spot fleet will not submit bids in alternative Spot pools.

When you want to maintain a target capacity, Spot fleet will place the required bids to meet this target capacity and automatically replenish any interrupted instances. By default, Spot fleets are set to maintain the requested target capacity.

It is not possible to modify the target capacity of a one-time request once it's been submitted. To change the target capacity, cancel the request and submit a new one.

A Spot fleet request remains active until it expires or you cancel it. When you cancel a Spot fleet request, you may specify whether cancelling your Spot fleet request terminates the Spot instances in your Spot fleet.

Each launch specification includes the information that Amazon EC2 needs to launch an instance—such as an AMI, an instance type, a subnet or Availability Zone, and one or more security groups.

Contents

Spot Fleet Request States
Spot Fleet Prerequisites
Spot Fleet and IAM Users
Spot Fleet Health Checks
Planning a Spot Fleet Request
Creating a Spot Fleet Request
Monitoring Your Spot Fleet
Modifying a Spot Fleet Request
Cancelling a Spot Fleet Request
Spot Fleet Example Configurations
Spot Fleet Request States

A Spot fleet request can be in one of the following states:

submitted—The Spot fleet request is being evaluated and Amazon EC2 is preparing to launch the target number of Spot instances.
active—The Spot fleet has been validated and Amazon EC2 is attempting to maintain the target number of running Spot instances. The request remains in this state until it is modified or cancelled.
modifying—The Spot fleet request is being modified. The request remains in this state until the modification is fully processed or the Spot fleet is cancelled. A one-time request cannot be modified, and this state does not apply to such Spot requests.
cancelled_running—The Spot fleet is cancelled and will not launch additional Spot instances, but its existing Spot instances continue to run until they are interrupted or terminated. The request remains in this state until all instances are interrupted or terminated.
cancelled_terminating—The Spot fleet is cancelled and its Spot instances are terminating. The request remains in this state until all instances are terminated.
cancelled—The Spot fleet is cancelled and has no running Spot instances. The Spot fleet request is deleted two days after its instances were terminated.
The following illustration represents the transitions between the request states. Note that if you exceed your Spot fleet limits, the request is cancelled immediately.


						Spot fleet request states
					
Spot Fleet Prerequisites

If you use the Amazon EC2 console to create a Spot fleet, it creates a role named aws-ec2-spot-fleet-tagging-role that grants the Spot fleet permission to bid on, launch, terminate, and tag instances on your behalf. This role is selected when you create your Spot fleet request. If you use the AWS CLI or an API instead, you must ensure that this role exists. You can either use the Request Spot Instances wizard (the role is created when you advance to the second page of the wizard) or use the IAM console as follows.

To create the IAM role for Spot fleet

Open the IAM console at https://console.aws.amazon.com/iam/.

In the navigation pane, choose Roles.

Choose Create new role.

On the Select role type page, choose Select next to Amazon EC2 Spot Fleet Role.

On the Attach Policy page, select the AmazonEC2SpotFleetRole policy, and then choose Next Step.

On the Set role name and review page, type a name for the role (for example, aws-ec2-spot-fleet-tagging-role) and then choose Create role.

To grant the Spot fleet permission to automatically tag the instances it launches, click the row for the new role, choose Attach Policy, select the AmazonEC2SpotFleetTaggingRole policy, and then choose Attach Policy. Choose Detach Policy next to the AmazonEC2SpotFleetRole policy.

Spot Fleet and IAM Users

If your IAM users will create or manage a Spot fleet, be sure to grant them the required permissions as follows.

To grant an IAM user permissions for Spot fleet

Open the IAM console at https://console.aws.amazon.com/iam/.

In the navigation pane, choose Policies, and then choose Create policy.

On the Create Policy page, choose Select next to Create Your Own Policy.

On the Review Policy page, type a policy name and add the following text to Policy Document.

Copy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
              "iam:ListRoles",
              "iam:PassRole",
              "iam:ListInstanceProfiles"
            ],
            "Resource": "*"
        }
    ]
}
The ec2:* grants an IAM user permission to call all Amazon EC2 API actions. To limit the user to specific Amazon EC2 API actions, specify those actions instead.

An IAM user must have permission to call the iam:ListRoles action to enumerate existing IAM roles, the iam:PassRole action to specify the Spot fleet role, and the iam:ListInstanceProfiles action to enumerate existing instance profiles.

(Optional) To enable an IAM user to create roles or instance profiles using the IAM console, you must also add the following actions to the policy:

iam:AddRoleToInstanceProfile
iam:AttachRolePolicy
iam:CreateInstanceProfile
iam:CreateRole
iam:ListPolicies
Choose Create Policy.

In the navigation pane, choose Users, and then choose the user who will submit the Spot fleet request.

On the Permissions tab, choose Add permissions.

Choose Attach existing policies directly. Select the policy you created above, choose Next: Review, then Add permissions.

Spot Fleet Health Checks

Spot fleet checks the health status of the Spot instances in the fleet every two minutes. The health status of an instance is either healthy or unhealthy. Spot fleet determines the health status of an instance using the status checks provided by Amazon EC2. If the status of either the instance status check or the system status check is impaired for three consecutive health checks, the health status of the instance is unhealthy. Otherwise, the health status is healthy. For more information, see Status Checks for Your Instances.

You can configure your Spot fleet to replace unhealthy instances. After enabling health check replacement, an instance is replaced after its health status is reported as unhealthy. Note that the Spot fleet could go below its target capacity for up to a few minutes while an unhealthy instance is being replaced.

Requirements

Health check replacement is supported only with Spot fleets that maintain a target capacity, not with one-time Spot fleets.
You can configure your Spot fleet to replace unhealthy instances only when you create it.
IAM users can use health check replacement only if they have permission to call the ec2:DescribeInstanceStatus action.
Planning a Spot Fleet Request

Before you create a Spot fleet request, review Spot Best Practices. Use these best practices when you plan your Spot fleet request so that you can provision the type of instances you want at the lowest possible price. We also recommend that you do the following:

Determine whether you want to create a Spot fleet that submits a one-time request for the desired target capacity, or one that will maintain a target capacity over time.
Determine the instance types that meet your application requirements.
Determine the target capacity for your Spot fleet request. You can set target capacity in instances or in custom units. For more information, see Spot Fleet Instance Weighting.
Determine your bid price per instance hour. Bidding lower can further reduce costs, while bidding higher can reduce the probability of interruption.
Determine your bid price per unit, if you are using instance weighting. To calculate the bid price per unit, divide the bid price per instance hour by the number of units (or weight) that this instance represents. (If you are not using instance weighting, the default bid price per unit is the bid price per instance hour.)
Review the possible options for your Spot fleet request. For more information, see the request-spot-fleet command in the AWS Command Line Interface Reference. For additional examples, see Spot Fleet Example Configurations.
Creating a Spot Fleet Request

When you create a Spot fleet request, you must specify information about the Spot instances to launch, such as the instance type and the Spot price.

To create a Spot fleet request using the console

Open the Spot console at https://console.aws.amazon.com/ec2spot.

If you are new to Spot, you see a welcome page; choose Get started. Otherwise, choose Request Spot Instances.

On the Find instance types page, do the following:

For Request type, select either Request or Request and Maintain.

For Target capacity, enter the number of units to request. You can choose instances or performance characteristics that are important to your application workload, such as vCPUs, memory, and storage.

For AMI, choose one of the basic Amazon Machine Images (AMI) provided by AWS, or choose Use custom AMI to use an AMI from our user community, the AWS Marketplace, or one of your own.

For Instance type(s), choose Select. Select the instance types that have the minimum hardware specifications that you need (vCPUs, memory, and storage).

For Allocation strategy, choose the strategy that meets your needs. For more information, see Spot Fleet Allocation Strategy.

For Network, your account supports either the EC2-Classic and EC2-VPC platforms, or the EC2-VPC platform only. To find out which platforms your account supports, see Supported Platforms.

[Existing VPC] Select the VPC.

[New VPC] Select Create new VPC to go the Amazon VPC console. When you are done, return to the wizard and refresh the list.

[EC2-Classic] Select EC2-Classic.

(Optional) For Availability Zones, the default is to let AWS choose the Availability Zones for your Spot instances. If you prefer, you can specify specific Availability Zones.

[EC2-VPC] Select one or more Availability Zones. If you have more than one subnet in an Availability Zone, select the appropriate subnet from Subnet. To add subnets, select Create new subnet to go to the Amazon VPC console. When you are done, return to the wizard and refresh the list.

[EC2-Classic] Select Select specific zone/subnet, and then select one or more Availability Zones.

For Maximum price, you can use automated bidding or specify a bid price. Your Spot instances are not launched if your bid price is lower than the Spot price for the instance types that you selected.

Choose Next.

On the Configure page, do the following:

(Optional) To add storage, specify additional instance store volumes or EBS volumes, depending on the instance type. You can also enable EBS optimization.

(Optional) By default, basic monitoring is enabled for your instances. To enable detailed monitoring, select Enable CloudWatch detailed monitoring.

(Optional) To replace unhealthy instances in a Request and Maintain Spot fleet, select Replace unhealthy instances.

(Optional) To run a Dedicated Spot instance, choose Dedicated - run a dedicated instance for Tenancy.

(Optional) To run a start-up script, copy it to User data.

(Optional) To add a tag, choose Add new tag and type the key and value for the tag. Repeat for each tag.

(Optional) If you need to connect to your instances, specify your key pair using Key pair name.

(Optional) To launch your Spot instances with an IAM role, specify it using IAM instance profile.

For Security groups, select one or more security groups.

[EC2-VPC] If you need to connect to your instances in a VPC, you can enable Auto-assign IPv4 Public IP.

By default, the request remains in effect until it is fulfilled or you cancel it. To create a request that is valid only during a specific time period, edit Request valid from and Request valid to.

(Optional) By default, we terminate your Spot instances when the request expires. To keep them running after your request expires, clear Terminate instances at expiration.

Choose Review.

On the Review page, verify the launch configuration. To make changes, choose Previous. To download a copy of the launch configuration for use with the AWS CLI, choose JSON config. When you are ready, choose Launch.

On the confirmation page, choose OK. The request type is fleet. When the request is fulfilled, requests of type instance are added, where the state is active and the status is fulfilled.

To create a Spot fleet request using the AWS CLI

Use the following request-spot-fleet command to create a Spot fleet request:

Copy
aws ec2 request-spot-fleet --spot-fleet-request-config file://config.json
For example configuration files, see Spot Fleet Example Configurations.

The following is example output:

{
    "SpotFleetRequestId": "sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE"
} 
Monitoring Your Spot Fleet

The Spot fleet launches Spot instances when the Spot price is below your bid. The Spot instances run until either the bid price is no longer higher than the Spot price, or you terminate them yourself.

To monitor your Spot fleet using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Spot Requests.

Select your Spot fleet request. The configuration details are available in the Description tab.

To list the Spot instances for the Spot fleet, choose the Instances tab.

To view the history for the Spot fleet, choose the History tab.

To monitor your Spot fleet using the AWS CLI

Use the following describe-spot-fleet-requests command to describe your Spot fleet requests:

Copy
aws ec2 describe-spot-fleet-requests
Use the following describe-spot-fleet-instances command to describe the Spot instances for the specified Spot fleet:

Copy
aws ec2 describe-spot-fleet-instances --spot-fleet-request-id sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE
Use the following describe-spot-fleet-request-history command to describe the history for the specified Spot fleet request:

Copy
aws ec2 describe-spot-fleet-request-history --spot-fleet-request-id sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE --start-time 2015-05-18T00:00:00Z
Modifying a Spot Fleet Request

You can modify an active Spot fleet request to complete the following tasks:

Increase the target capacity
Decrease the target capacity
Note
It is not possible to modify a one-time Spot fleet request.
When you increase the target capacity, the Spot fleet launches the additional Spot instances according to the allocation strategy for its Spot fleet request. If the allocation strategy is lowestPrice, the Spot fleet launches the instances from the lowest-priced Spot instance pool in the Spot fleet request. If the allocation strategy is diversified, the Spot fleet distributes the instances across the pools in the Spot fleet request.

When you decrease the target capacity, the Spot fleet cancels any open bids that exceed the new target capacity. You can request that the Spot fleet terminate Spot instances until the size of the fleet reaches the new target capacity. If the allocation strategy is lowestPrice, the Spot fleet terminates the instances with the highest price per unit. If the allocation strategy is diversified, the Spot fleet terminates instances across the pools. Alternatively, you can request that the Spot fleet keep the fleet at its current size, but not replace any Spot instances that are interrupted or that you terminate manually.

Note that when a Spot fleet terminates an instance because the target capacity was decreased, the instance receives a Spot instance termination notice.

To modify a Spot fleet request using the console

Open the Spot console at https://console.aws.amazon.com/ec2spot/home/fleet.

Select your Spot fleet request.

Choose Actions, and then choose Modify target capacity.

In Modify target capacity, do the following:

Enter the new target capacity.

(Optional) If you are decreasing the target capacity but want to keep the fleet at its current size, deselect Terminate instances.

Choose Submit.

To modify a Spot fleet request using the AWS CLI

Use the following modify-spot-fleet-request command to update the target capacity of the specified Spot fleet request:

Copy
aws ec2 modify-spot-fleet-request --spot-fleet-request-id sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE --target-capacity 20
You can modify the previous command as follows to decrease the target capacity of the specified Spot fleet without terminating any Spot instances as a result:

Copy
aws ec2 modify-spot-fleet-request --spot-fleet-request-id sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE --target-capacity 10 --excess-capacity-termination-policy NoTermination
Cancelling a Spot Fleet Request

When you are finished using your Spot fleet, you can cancel the Spot fleet request. This cancels all Spot requests associated with the Spot fleet, so that no new Spot instances are launched for your Spot fleet. You must specify whether the Spot fleet should terminate its Spot instances. If you terminate the instances, the Spot fleet request enters the cancelled_terminating state. Otherwise, the Spot fleet request enters the cancelled_running state and the instances continue to run until they are interrupted or you terminate them manually.

To cancel a Spot fleet request using the console

Open the Spot console at https://console.aws.amazon.com/ec2spot/home/fleet.

Select your Spot fleet request.

Choose Actions, and then choose Cancel spot request.

In Cancel spot request, verify that you want to cancel the Spot fleet. To keep the fleet at its current size, deselect Terminate instances. When you are ready, choose Confirm.

To cancel a Spot fleet request using the AWS CLI

Use the following cancel-spot-fleet-requests command to cancel the specified Spot fleet request and terminate the instances:

Copy
aws ec2 cancel-spot-fleet-requests --spot-fleet-request-ids sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE --terminate-instances
The following is example output:

{
    "SuccessfulFleetRequests": [
        {
            "SpotFleetRequestId": "sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE",
            "CurrentSpotFleetRequestState": "cancelled_terminating",
            "PreviousSpotFleetRequestState": "active"
        }
    ],
    "UnsuccessfulFleetRequests": []
}
You can modify the previous command as follows to cancel the specified Spot fleet request without terminating the instances:

Copy
aws ec2 cancel-spot-fleet-requests --spot-fleet-request-ids sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE --no-terminate-instances
The following is example output:

{
    "SuccessfulFleetRequests": [
        {
            "SpotFleetRequestId": "sfr-73fbd2ce-aa30-494c-8788-1cee4EXAMPLE",
            "CurrentSpotFleetRequestState": "cancelled_running",
            "PreviousSpotFleetRequestState": "active"
        }
    ],
    "UnsuccessfulFleetRequests": []
}

Spot Fleet Example Configurations

The following examples show launch configurations that you can use with the request-spot-fleet command to create a Spot fleet request. For more information, see Creating a Spot Fleet Request.

Launch Spot instances using the lowest-priced Availability Zone or subnet in the region

Launch Spot instances using the lowest-priced Availability Zone or subnet in a specified list

Launch Spot instances using the lowest-priced instance type in a specified list

Override the Spot price for the request

Launch a Spot fleet using the diversified allocation strategy

Launch a Spot fleet using instance weighting

Example 1: Launch Spot Instances Using the Lowest-priced Availability Zone or Subnet in the Region

The following example specifies a single launch specification without an Availability Zone or subnet. If your account supports EC2-VPC only, the Spot fleet launches the instances in the lowest-priced Availability Zone that has a default subnet. If your account supports EC2-Classic, the Spot fleet launches the instances in EC2-Classic in the lowest-priced Availability Zone. Note that the price you pay will not exceed the specified Spot price for the request.

Copy
{
  "SpotPrice": "0.07",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "KeyName": "my-key-pair",
          "SecurityGroups": [
              {
                  "GroupId": "sg-1a2b3c4d"
              }
          ],
          "InstanceType": "m3.medium",
          "IamInstanceProfile": {
              "Arn": "arn:aws:iam::123456789012:instance-profile/my-iam-role"
          }
      }
  ]
}
Example 2: Launch Spot Instances Using the Lowest-priced Availability Zone or Subnet in a Specified List

The following examples specify two launch specifications with different Availability Zones or subnets, but the same instance type and AMI.

Availability Zones

If your account supports EC2-VPC only, the Spot fleet launches the instances in the default subnet of the lowest-priced Availability Zone that you specified. If your account supports EC2-Classic, the Spot fleet launches the instances in the lowest-priced Availability Zone that you specified.

Copy
{
  "SpotPrice": "0.07",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "KeyName": "my-key-pair",
          "SecurityGroups": [
              {
                  "GroupId": "sg-1a2b3c4d"
              }
          ],
          "InstanceType": "m3.medium",
          "Placement": {
              "AvailabilityZone": "us-west-2a, us-west-2b"
          },
          "IamInstanceProfile": {
              "Arn": "arn:aws:iam::123456789012:instance-profile/my-iam-role"
          }
      }
  ]
}
Subnets

You can specify default subnets or nondefault subnets, and the nondefault subnets can be from a default VPC or a nondefault VPC. The Spot service launches the instances in whichever subnet is in the lowest-priced Availability Zone.

Note that you can't specify different subnets from the same Availability Zone in a Spot fleet request.

Copy
{
  "SpotPrice": "0.07",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "KeyName": "my-key-pair",
          "SecurityGroups": [
              {
                  "GroupId": "sg-1a2b3c4d"
              }
          ],
          "InstanceType": "m3.medium",
          "SubnetId": "subnet-a61dafcf, subnet-65ea5f08",
          "IamInstanceProfile": {
              "Arn": "arn:aws:iam::123456789012:instance-profile/my-iam-role"
          }
      }
  ]
}
If the instances are launched in a default VPC, they receive a public IPv4 address by default. If the instances are launched in a nondefault VPC, they do not receive a public IPv4 address by default. Use a network interface in the launch specification to assign a public IPv4 address to instances launched in a nondefault VPC. Note that when you specify a network interface, you must include the subnet ID and security group ID using the network interface.

Copy
  ...       
      {
          "ImageId": "ami-1a2b3c4d",
          "KeyName": "my-key-pair",
          "InstanceType": "m3.medium",
          "NetworkInterfaces": [
              {
                  "DeviceIndex": 0,
                  "SubnetId": "subnet-1a2b3c4d",
                  "Groups": [ "sg-1a2b3c4d" ],
                  "AssociatePublicIpAddress": true
              }
          ],
          "IamInstanceProfile": {
              "Arn": "arn:aws:iam::880185128111:instance-profile/my-iam-role"
          }
      }
  ...
Example 3: Launch Spot Instances Using the Lowest-priced Instance Type in a Specified List

The following examples specify two launch configurations with different instance types, but the same AMI and Availability Zone or subnet. The Spot fleet launches the instances using the specified instance type with the lowest price.

Availability Zone

Copy
{
  "SpotPrice": "1.00",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "SecurityGroups": [
              {
                  "GroupId": "sg-1a2b3c4d"
              }
          ],
          "InstanceType": "cc2.8xlarge",
          "Placement": {
            "AvailabilityZone": "us-west-2b"
          }
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "SecurityGroups": [
              {
                  "GroupId": "sg-1a2b3c4d"
              }
          ],
          "InstanceType": "r3.8xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          }
      }
  ]
}
Subnet

Copy
{
  "SpotPrice": "1.00",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "SecurityGroups": [
              {
                  "GroupId": "sg-1a2b3c4d"
              }
          ],
          "InstanceType": "cc2.8xlarge",
          "SubnetId": "subnet-1a2b3c4d"
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "SecurityGroups": [
              {
                  "GroupId": "sg-1a2b3c4d"
              }
          ],
          "InstanceType": "r3.8xlarge",
          "SubnetId": "subnet-1a2b3c4d"
      }
  ]
}
Example 4. Override the Spot Price for the Request

The ability to specify Spot prices for individual launch specifications provides you with additional control over the bidding process. The following examples override the Spot price for the request with individual Spot prices for two of the three launch specifications. Note that the Spot price for the request is used for any launch specification that does not specify an individual Spot price. The Spot fleet launches the instances using the instance type with the lowest price.

Availability Zone

Copy
{
  "SpotPrice": "1.00",
  "TargetCapacity": 30,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.2xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          },
          "SpotPrice": "0.10"
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.4xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          },
          "SpotPrice": "0.20"
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.8xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          }
      }
    ]
}
Subnet

Copy
{
  "SpotPrice": "1.00",
  "TargetCapacity": 30,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.2xlarge",
          "SubnetId": "subnet-1a2b3c4d",
          "SpotPrice": "0.10"
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.4xlarge",
          "SubnetId": "subnet-1a2b3c4d",
          "SpotPrice": "0.20"
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.8xlarge",
          "SubnetId": "subnet-1a2b3c4d"
      }
  ]
}
Example 5: Launch a Spot Fleet Using the Diversified Allocation Strategy

The following example uses the diversified allocation strategy. The launch specifications have different instance types but the same AMI and Availability Zone or subnet. The Spot fleet distributes the 30 instances across the 3 launch specifications, such that there are 10 instances of each type. For more information, see Spot Fleet Allocation Strategy.

Availability Zone

Copy
{
  "SpotPrice": "0.70", 
  "TargetCapacity": 30,
  "AllocationStrategy": "diversified",
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c4.2xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          }
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "m3.2xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          }
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "r3.2xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          }
      }
  ]
}
Subnet

Copy
{
    "SpotPrice": "0.70", 
    "TargetCapacity": 30,
    "AllocationStrategy": "diversified",
    "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
    "LaunchSpecifications": [
        {
            "ImageId": "ami-1a2b3c4d",
            "InstanceType": "c4.2xlarge",
            "SubnetId": "subnet-1a2b3c4d"
        },
        {
            "ImageId": "ami-1a2b3c4d",
            "InstanceType": "m3.2xlarge",
            "SubnetId": "subnet-1a2b3c4d"
        },
        {
            "ImageId": "ami-1a2b3c4d",
            "InstanceType": "r3.2xlarge",
            "SubnetId": "subnet-1a2b3c4d"
        }
    ]
}
Example 6: Launch a Spot Fleet Using Instance Weighting

The following examples use instance weighting, which means that the bid price is per unit hour instead of per instance hour. Each launch configuration lists a different instance type and a different weight. The Spot fleet selects the instance type with the lowest price per unit hour. The Spot fleet calculates the number of Spot instances to launch by dividing the target capacity by the instance weight. If the result isn't an integer, the Spot fleet rounds it up to the next integer, so that the size of your fleet is not below its target capacity.

If the r3.2xlarge bid is successful, Spot provisions 4 of these instances. (Divide 20 by 6 for a total of 3.33 instances, then round up to 4 instances.)

If the c3.xlarge bid is successful, Spot provisions 7 of these instances. (Divide 20 by 3 for a total of 6.66 instances, then round up to 7 instances.)

For more information, see Spot Fleet Instance Weighting.

Availability Zone

Copy
{
  "SpotPrice": "0.70",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "r3.2xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          },
          "WeightedCapacity": 6
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.xlarge",
          "Placement": {
              "AvailabilityZone": "us-west-2b"
          },
          "WeightedCapacity": 3
      }
    ]
}
Subnet

Copy
{
  "SpotPrice": "0.70",
  "TargetCapacity": 20,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "r3.2xlarge",
          "SubnetId": "subnet-1a2b3c4d",
          "WeightedCapacity": 6
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.xlarge",
          "SubnetId": "subnet-1a2b3c4d",
          "WeightedCapacity": 3
      }
  ]
}
Priority

You can also use instance weighting to give priority to an Availability Zone or subnet. For example, the following launch specifications are nearly identical, except that they specify different subnets and weights. The Spot fleet finds the specification with the highest value for WeightedCapacity, and attempts to provision the request in the least expensive Spot instance pool in that subnet. (Note that the second launch specification does not include a weight, so it defaults to 1.)

Copy
{
  "SpotPrice": "0.42",
  "TargetCapacity": 40,
  "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-tagging-role",
  "LaunchSpecifications": [
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.2xlarge",
          "SubnetId": "subnet-482e4972",
          "WeightedCapacity": 2
      },
      {
          "ImageId": "ami-1a2b3c4d",
          "InstanceType": "c3.2xlarge",
          "SubnetId": "subnet-bb3337d"
      }
    ]
}

CloudWatch Metrics for Spot Fleet

Amazon EC2 provides Amazon CloudWatch metrics that you can use to monitor your Spot fleet.

Important
To ensure accuracy, we recommend that you enable detailed monitoring when using these metrics. For more information, see Enable or Disable Detailed Monitoring for Your Instances.
For more information about CloudWatch metrics provided by Amazon EC2, see Monitoring Your Instances Using CloudWatch.

Spot Fleet Metrics

The AWS/EC2Spot namespace includes the following metrics, plus the CloudWatch metrics for the Spot instances in your fleet. For more information, see Instance Metrics.

The AWS/EC2Spot namespace includes the following metrics.

Metric	Description
AvailableInstancePoolsCount
The Spot Instance pools specified in the Spot Fleet request.

Units: Count
BidsSubmittedForCapacity
The capacity for which Amazon EC2 has submitted bids.

Units: Count
EligibleInstancePoolCount
The Spot Instance pools specified in the Spot Fleet request where Amazon EC2 can fulfill bids. Amazon EC2 will not fulfill bids in pools where your bid price is less than the Spot price or the Spot price is greater than the price for On-Demand instances.

Units: Count
FulfilledCapacity
The capacity that Amazon EC2 has fulfilled.

Units: Count
MaxPercentCapacityAllocation
The maximum value of PercentCapacityAllocation across all Spot Instance pools specified in the Spot Fleet request.

Units: Percent
PendingCapacity
The difference between TargetCapacity and FulfilledCapacity.

Units: Count
PercentCapacityAllocation
The capacity allocated for the Spot Instance pool for the specified dimensions. To get the maximum value recorded across all Spot Instance pools, use MaxPercentCapacityAllocation.

Units: Percent
TargetCapacity
The target capacity of the Spot Fleet request.

Units: Count
TerminatingCapacity
The capacity that is being terminated due to Spot Instance interruptions.

Units: Count
If the unit of measure for a metric is Count, the most useful statistic is Average.

Spot Fleet Dimensions

To filter the data for your Spot fleet, you can use the following dimensions.

Dimensions	Description
AvailabilityZone
Filter the data by Availability Zone.
FleetRequestId
Filter the data by Spot Fleet request.
InstanceType
Filter the data by instance type.
View the CloudWatch Metrics for Your Spot Fleet

You can view the CloudWatch metrics for your Spot fleet using the Amazon CloudWatch console. These metrics are displayed as monitoring graphs. These graphs show data points if the Spot fleet is active.

Metrics are grouped first by namespace, and then by the various combinations of dimensions within each namespace. For example, you can view all Spot fleet metrics, or Spot fleet metrics groups by Spot fleet request ID, instance type, or Availability Zone.

To view Spot fleet metrics

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, under Metrics, choose the EC2 Spot namespace.

(Optional) To filter the metrics by dimension, select one of the following:

Fleet Request Metrics — Group by Spot fleet request
By Availability Zone — Group by Spot fleet request and Availability Zone
By Instance Type — Group by Spot fleet request and instance type
By Availability Zone/Instance Type — Group by Spot fleet request, Availability Zone, and instance type
To view the data for a metric, select the check box next to the metric.

Automatic Scaling for Spot Fleet

Automatic scaling is the ability to increase or decrease the target capacity of your Spot fleet automatically based on demand. A Spot fleet can either launch instances (scale out) or terminate instances (scale in), within the range that you choose, in response to one or more scaling policies. We recommend that you create two policies, one for scaling out and one for scaling in.

A scaling policy uses CloudWatch alarms to trigger the scaling process. For example, if you want to scale out when CPU utilization reaches a certain level, create an alarm using the CPUUtilization metric provided by Amazon EC2.

When you create a scaling policy, you must specify one of the following scaling adjustment types:

Add — Increase the target capacity of the fleet by a specified number of capacity units or a specified percentage of the current capacity.
Remove — Decrease the target capacity of the fleet by a specified number of capacity units or a specified percentage of the current capacity.
Set to — Set the target capacity of the fleet to the specified number of capacity units.
When an alarm is triggered, the auto scaling process calculates the new target capacity using the fulfilled capacity and the scaling policy, and then updates the target capacity accordingly. For example, suppose that the target capacity and fulfilled capacity are 10 and the scaling policy adds 1. When the alarm is triggered, the auto scaling process adds 1 to 10 to get 11, so Spot fleet launches 1 instance.

If you are using instance weighting, keep in mind that Spot fleet can exceed the target capacity as needed, and that fulfilled capacity can be a floating-point number but target capacity must be an integer, so Spot fleet rounds up to the next integer. You must take these behaviors into account when you look at the outcome of a scaling policy when an alarm is triggered. For example, suppose that the target capacity is 30, the fulfilled capacity is 30.1, and the scaling policy subtracts 1. When the alarm is triggered, the auto scaling process subtracts 1 from 30.1 to get 29.1 and then rounds it up to 30, so no scaling action is taken. As another example, suppose that you selected instance weights of 2, 4, and 8, and a target capacity of 10, but no weight 2 instances were available so Spot fleet provisioned instances of weights 4 and 8 for a fulfilled capacity of 12. If the scaling policy decreases target capacity by 20% and an alarm is triggered, the auto scaling process subtracts 12*0.2 from 12 to get 9.6 and then rounds it up to 10, so no scaling action is taken.

You can also configure the cooldown period for a scaling policy. This is the number of seconds after a scaling activity completes where previous trigger-related scaling activities can influence future scaling events. For scale out policies, while the cooldown period is in effect, the capacity that has been added by the previous scale out event that initiated the cooldown is calculated as part of the desired capacity for the next scale out. The intention is to continuously (but not excessively) scale out. For scale in policies, the cooldown period is used to block subsequent scale in requests until it has expired. The intention is to scale in conservatively to protect your application's availability. However, if another alarm triggers a scale out policy during the cooldown period after a scale-in, auto scaling scales out your scalable target immediately.

Note that when a Spot fleet terminates an instance because the target capacity was decreased, the instance receives a Spot instance termination notice.

Limits

The Spot fleet request must have a request type of maintain. Automatic scaling is not supported for one-time requests or Spot blocks.
Prerequisites

Consider which CloudWatch metrics are important to your application. You can create CloudWatch alarms based on metrics provided by AWS or your own custom metrics.
For the AWS metrics that you will use in your scaling policies, enable CloudWatch metrics collection if the service that provides the metrics does not enable it by default.
If you use the AWS Management Console to enable automatic scaling for your Spot fleet, it creates a role named aws-ec2-spot-fleet-autoscale-role that grants Auto Scaling permission to describe the alarms for your policies, monitor the current capacity of the fleet, and modify the capacity of the fleet. If you configure automatic scaling using the AWS CLI or an API, you can use this role if it exists, or manually create your own role for this purpose as follows.
Open the IAM console at https://console.aws.amazon.com/iam/.
In the navigation pane, choose Roles.
Choose Create New Role.
On the Set Role Name page, type a name for the role and then choose Next Step.
On the Select Role Type page, choose Select next to Amazon EC2.
On the Attach Policy page, select the AmazonEC2SpotFleetAutoscaleRole policy and then choose Next Step.
On the Review page, choose Create Role.
Select the role that you just created.
On the Trust Relationships tab, choose Edit Trust Relationship.
Change ec2.amazonaws.com to application-autoscaling.amazonaws.com and then choose Update Trust Policy.
To create a CloudWatch alarm

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, choose Alarms.

Choose Create Alarm.

For CloudWatch Metrics by Category, choose a category. For example, choose EC2 Spot Metrics, Fleet Request Metrics.

Select a metric, and then choose Next.

For Alarm Threshold, type a name and description for the alarm, and set the threshold value and number of time periods for the alarm.

(Optional) To receive notification of a scaling event, for Actions, choose New list and type your email address. Otherwise, you can delete the notification now and add one later if needed.

Choose Create Alarm.

To configure automatic scaling for your Spot fleet using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Spot Requests.

Select your Spot fleet request, and then choose the Auto Scaling tab.

If automatic scaling is not configured, choose Configure.

Use Scale capacity between to set the minimum and maximum capacity for your fleet. Automatic scaling will not scale your fleet below the minimum capacity or above the maximum capacity.

Initially, Scaling policies contains policies named ScaleUp and ScaleDown. You can complete these policies, or choose Remove policy to delete them. You can also choose Add policy to add a policy.

To define a policy, do the following:

For Policy name, type a name for the policy.

For Policy trigger, select an existing alarm or choose Create new alarm to open the Amazon CloudWatch console and create an alarm.

For Modify capacity, select a scaling adjustment type, select a number, and select a unit.

(Optional) To perform step scaling, choose Define steps. By default, an add policy has a lower bound of -infinity and an upper bound of the alarm threshold. By default, a remove policy has a lower bound of the alarm threshold and an upper bound of +infinity. To add another step, choose Add step.

(Optional) To modify the default value for the cooldown period, select a number from Cooldown period.

Choose Save.

To configure automatic scaling for your Spot fleet using the AWS CLI

Register the Spot fleet request as a scalable target using the register-scalable-target command.

Create a scaling policy using the put-scaling-policy command.

Create an alarm that will trigger the scaling policy using the put-metric-alarm command.

Spot Bid Status

To help you track your Spot instance requests, plan your use of Spot instances, and bid strategically, Amazon EC2 provides a bid status. For example, a bid status can tell you the reason why your Spot request isn't fulfilled yet, or list the constraints that are preventing the fulfillment of your Spot request.

At each step of the process—also called the Spot request life cycle, specific events determine successive request states.

Contents

Life Cycle of a Spot Request
Getting Bid Status Information
Spot Bid Status Codes
Life Cycle of a Spot Request

The following diagram shows you the paths that your Spot request can follow throughout its life cycle, from submission to termination. Each step is depicted as a node, and the status code for each node describes the status of the Spot request and Spot instance.


						Life cycle of a Spot request
					
Pending evaluation

As soon as you make a Spot instance request, it goes into the pending-evaluation state unless one or more request parameters is not valid (bad-parameters).

Status Code	Request State	Instance State
pending-evaluation
open
n/a
bad-parameters
closed
n/a
Holding

If one or more request constraints are valid but can't be met yet, or if there is not enough capacity, the request goes into a holding state waiting for the constraints to be met. The request options affect the likelihood of the request being fulfilled. For example, if you specify a bid price below the current Spot price, your request stays in a holding state until the Spot price goes below your bid price. If you specify an Availability Zone group, the request stays in a holding state until the Availability Zone constraint is met.

Status Code	Request State	Instance State
capacity-not-available
open
n/a
capacity-oversubscribed
open
n/a
price-too-low
open
n/a
not-scheduled-yet
open
n/a
launch-group-constraint
open
n/a
az-group-constraint
open
n/a
placement-group-constraint
open
n/a
constraint-not-fulfillable
open
n/a
Pending evaluation/fulfillment-terminal

Your Spot instance request can go to a terminal state if you create a request that is valid only during a specific time period and this time period expires before your request reaches the pending fulfillment phase, you cancel the request, or a system error occurs.

Status Code	Request State	Instance State
schedule-expired
closed
n/a
canceled-before-fulfillment*
cancelled
n/a
bad-parameters
failed
n/a
system-error
closed
n/a
* If you cancel the request.

Pending fulfillment

When the constraints you specified (if any) are met and your bid price is equal to or higher than the current Spot price, your Spot request goes into the pending-fulfillment state.

At this point, Amazon EC2 is getting ready to provision the instances that you requested. If the process stops at this point, it is likely to be because it was cancelled by the user before a Spot instance was launched, or because an unexpected system error occurred.

Status Code	Request State	Instance State
pending-fulfillment
open
n/a
Fulfilled

When all the specifications for your Spot instances are met, your Spot request is fulfilled. Amazon EC2 launches the Spot instances, which can take a few minutes.

Status Code	Request State	Instance State
fulfilled
active
pending → running
Fulfilled-terminal

Your Spot instances continue to run as long as your bid price is at or above the Spot price, there is spare Spot capacity for your instance type, and you don't terminate the instance. If a change in Spot price or available capacity requires Amazon EC2 to terminate your Spot instances, the Spot request goes into a terminal state. For example, if your bid equals the Spot price but Spot instances are oversubscribed at that price, the status code is instance-terminated-capacity-oversubscribed. A request also goes into the terminal state if you cancel the Spot request or terminate the Spot instances.

Status Code	Request State	Instance State
request-canceled-and-instance-running
cancelled
running
marked-for-termination
closed
running
instance-terminated-by-price
closed (one-time), open (persistent)
terminated
instance-terminated-by-user
closed or cancelled *
terminated
instance-terminated-no-capacity
closed (one-time), open (persistent)
terminated
instance-terminated-capacity-oversubscribed
closed (one-time), open (persistent)
terminated
instance-terminated-launch-group-constraint
closed (one-time), open (persistent)
terminated
* The request state is closed if you terminate the instance but do not cancel the bid. The request state is cancelled if you terminate the instance and cancel the bid. Note that even if you terminate a Spot instance before you cancel its request, there might be a delay before Amazon EC2 detects that your Spot instance was terminated. In this case, the request state can either be closed or cancelled.

Persistent requests

When your Spot instances are terminated (either by you or Amazon EC2), if the Spot request is a persistent request, it returns to the pending-evaluation state and then Amazon EC2 can launch a new Spot instance when the constraints are met.

Getting Bid Status Information

You can get bid status information using the AWS Management Console or a command line tool.

To get bid status information using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Spot Requests, and then select the Spot request.

Check the value of Status in the Description tab.

To get bid status information using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-spot-instance-requests (AWS CLI)
Get-EC2SpotInstanceRequest (AWS Tools for Windows PowerShell)
Spot Bid Status Codes

Spot bid status information is composed of a bid status code, the update time, and a status message. Together, they help you determine the disposition of your Spot request.

The following are the Spot bid status codes:

az-group-constraint
Amazon EC2 cannot launch all the instances you requested in the same Availability Zone.

bad-parameters
One or more parameters for your Spot request are not valid (for example, the AMI you specified does not exist). The bid status message indicates which parameter is not valid.

cancelled-before-fulfillment
The user cancelled the Spot request before it was fulfilled.

capacity-not-available
There is not enough capacity available for the instances that you requested.

capacity-oversubscribed
The number of Spot requests with bid prices equal to or higher than your bid price exceeds the available capacity in this Spot instance pool.

constraint-not-fulfillable
The Spot request can't be fulfilled because one or more constraints are not valid (for example, the Availability Zone does not exist). The bid status message indicates which constraint is not valid.

fulfilled
The Spot request is active, and Amazon EC2 is launching your Spot instances.

instance-terminated-by-price
The Spot price rose above your bid price. If your request is a persistent bid, the process restarts, so your bid is pending evaluation.

instance-terminated-by-user or spot-instance-terminated-by-user
You terminated a Spot instance that had been fulfilled, so the bid state is closed (unless it's a persistent bid) and the instance state is terminated.

instance-terminated-capacity-oversubscribed
Your instance is terminated because the number of Spot requests with bid prices equal to or higher than your bid price exceeded the available capacity in this Spot instance pool. (Note that the Spot price might not have changed.) The Spot service randomly selects instances to be terminated.

instance-terminated-launch-group-constraint
One or more of the instances in your launch group was terminated, so the launch group constraint is no longer fulfilled.

instance-terminated-no-capacity
There is no longer enough Spot capacity available for the instance.

launch-group-constraint
Amazon EC2 cannot launch all the instances that you requested at the same time. All instances in a launch group are started and terminated together.

limit-exceeded
The limit on the number of EBS volumes or total volume storage was exceeded. For more information about these limits and how to request an increase, see Amazon EBS Limits in the Amazon Web Services General Reference.

marked-for-termination
The Spot instance is marked for termination.

not-scheduled-yet
The Spot request will not be evaluated until the scheduled date.

pending-evaluation
After you make a Spot instance request, it goes into the pending-evaluation state while the system evaluates the parameters of your request.

pending-fulfillment
Amazon EC2 is trying to provision your Spot instances.

placement-group-constraint
The Spot request can't be fulfilled yet because a Spot instance can't be added to the placement group at this time.

price-too-low
The bid request can't be fulfilled yet because the bid price is below the Spot price. In this case, no instance is launched and your bid remains open.

request-cancelled-and-instance-running
You canceled the Spot request while the Spot instances are still running. The request is cancelled, but the instances remain running.

schedule-expired
The Spot request expired because it was not fulfilled before the specified date.

system-error
There was an unexpected system error. If this is a recurring issue, please contact customer support for assistance.

Spot Instance Interruptions

Demand for Spot instances can vary significantly from moment to moment, and the availability of Spot instances can also vary significantly depending on how many unused EC2 instances are available. In addition, no matter how high you bid, it is still possible that your Spot instance will be interrupted. Therefore, you must ensure that your application is prepared for a Spot instance interruption. We strongly recommend that you do not use Spot instances for applications that can't be interrupted.

The following are the possible reasons that Amazon EC2 will terminate your Spot instances:

Price—The Spot price is greater than your bid price.
Capacity—If there are not enough unused EC2 instances to meet the demand for Spot instances, Amazon EC2 terminates Spot instances, starting with those instances with the lowest bid prices. If there are several Spot instances with the same bid price, the order in which the instances are terminated is determined at random.
Constraints—If your request includes a constraint such as a launch group or an Availability Zone group, these Spot instances are terminated as a group when the constraint can no longer be met.
Preparing for Interruptions

Here are some best practices to follow when you use Spot instances:

Choose a reasonable bid price. Your bid price should be high enough to make it likely that your request will be fulfilled, but not higher than you are willing to pay. This is important because if the supply is low for an extended period of time, the Spot price can remain high during that period because it is based on the highest bid prices. We strongly recommend against bidding above the price for On-Demand instances.
Ensure that your instance is ready to go as soon as the request is fulfilled by using an Amazon Machine Image (AMI) that contains the required software configuration. You can also use user data to run commands at start-up.
Store important data regularly in a place that won't be affected when the Spot instance terminates. For example, you can use Amazon S3, Amazon EBS, or DynamoDB.
Divide the work into small tasks (using a Grid, Hadoop, or queue-based architecture) or use checkpoints so that you can save your work frequently.
Use Spot instance termination notices to monitor the status of your Spot instances.
Test your application to ensure that it handles an unexpected instance termination gracefully. You can do so by running the application using an On-Demand instance and then terminating the On-Demand instance yourself.
Spot Instance Termination Notices

The best way to protect against Spot instance interruption is to architect your application to be fault tolerant. In addition, you can take advantage of Spot instance termination notices, which provide a two-minute warning before Amazon EC2 must terminate your Spot instance.

This warning is made available to the applications on your Spot instance using an item in the instance metadata. For example, you can check for this warning in the instance metadata periodically (we recommend every 5 seconds) using the following query:

Copy
[ec2-user ~]$ if curl -s http://169.254.169.254/latest/meta-data/spot/termination-time | grep -q .*T.*Z; then echo terminated; fi
For information about other ways to retrieve instance metadata, see Retrieving Instance Metadata.

If your Spot instance is marked for termination by Amazon EC2, the termination-time item is present and it specifies the approximate time in UTC when the instance will receive the shutdown signal. For example:

2015-01-05T18:02:00Z
If Amazon EC2 is not preparing to terminate the instance, or if you terminated the Spot instance yourself, the termination-time item is either not present (so you receive an HTTP 404 error) or contains a value that is not a time value.

Note that while we make every effort to provide this warning the moment that your Spot instance is marked for termination by Amazon EC2, it is possible that your Spot instance will be terminated before Amazon EC2 can make the warning available. Therefore, you must ensure that your application is prepared to handle an unexpected Spot instance interruption even if you are checking for Spot instance termination notices.

If Amazon EC2 fails to terminate the instance, the Spot bid status is set to fulfilled. Note that termination-time remains in the instance metadata with the original approximate time, which is now in the past.

Spot Instance Data Feed

To help you understand the charges for your Spot instances, Amazon EC2 provides a data feed that describes your Spot instance usage and pricing. This data feed is sent to an Amazon S3 bucket that you specify when you subscribe to the data feed.

Data feed files arrive in your bucket typically once an hour, and each hour of usage is typically covered in a single data file. These files are compressed (gzip) before they are delivered to your bucket. Amazon EC2 can write multiple files for a given hour of usage where files are very large (for example, when file contents for the hour exceed 50 MB before compression).

Note
If you don't have a Spot instance running during a certain hour, you won't receive a data feed file for that hour.
Contents

Data Feed File Name and Format
Amazon S3 Bucket Requirements
Subscribing to Your Spot instance Data Feed
Deleting Your Spot Instance Data Feed
Data Feed File Name and Format

The Spot instance data feed file name uses the following format (with the date and hour in UTC):

bucket-name.s3.amazonaws.com/{optional prefix}/aws-account-id.YYYY-MM-DD-HH.n.unique-id.gz
For example, if your bucket name is myawsbucket and your prefix is myprefix, your file names are similar to the following:

myawsbucket.s3.amazonaws.com/myprefix/111122223333.2014-03-17-20.001.pwBdGTJG.gz
The Spot instance data feed files are tab-delimited. Each line in the data file corresponds to one instance hour and contains the fields listed in the following table.

Field	Description
Timestamp
The timestamp used to determine the price charged for this instance hour.
UsageType
The type of usage and instance type being charged for. For m1.small Spot instances, this field is set to SpotUsage. For all other instance types, this field is set to SpotUsage:{instance-type}. For example, SpotUsage:c1.medium.
Operation
The product being charged for. For Linux Spot instances, this field is set to RunInstances. For Windows Spot instances, this field is set to RunInstances:0002. Spot usage is grouped according to Availability Zone.
InstanceID
The ID of the Spot instance that generated this instance hour.
MyBidID
The ID for the Spot instance request that generated this instance hour.
MyMaxPrice
The maximum price specified for this Spot instance request.
MarketPrice
The Spot price at the time specified in the Timestamp field.
Charge
The price charged for this instance hour.
Version
The version included in the data feed file name for this record.
Amazon S3 Bucket Requirements

When you subscribe to the data feed, you must specify an Amazon S3 bucket to store the data feed files. Before you choose an Amazon S3 bucket for the data feed, consider the following:

You must use a bucket from the US East (N. Virginia) region (also known as us-east-1 or the US Standard region).
You must have FULL_CONTROL permission to the bucket.
If you're the bucket owner, you have this permission by default. Otherwise, the bucket owner must grant your AWS account this permission.
When you create your data feed subscription, Amazon S3 updates the ACL of the specified bucket to allow the AWS data feed account read and write permissions.
Removing the permissions for the data feed account does not disable the data feed. If you remove those permissions but don't disable the data feed, we restore those permissions the next time that the data feed account needs to write to the bucket.
Each data feed file has its own ACL (separate from the ACL for the bucket). The bucket owner has FULL_CONTROL permission to the data files. The data feed account has read and write permissions.
If you delete your data feed subscription, Amazon EC2 doesn't remove the read and write permissions for the data feed account on either the bucket or the data files. You must remove these permissions yourself.
Subscribing to Your Spot instance Data Feed

To subscribe to your data feed, use the following create-spot-datafeed-subscription command:

Copy
aws ec2 create-spot-datafeed-subscription --bucket myawsbucket [--prefix myprefix]
The following is example output:

{
    "SpotDatafeedSubscription": {
        "OwnerId": "111122223333",
        "Prefix": "myprefix",
        "Bucket": "myawsbucket",
        "State": "Active"
    }
}
Deleting Your Spot Instance Data Feed

To delete your data feed, use the following delete-spot-datafeed-subscription command:

Copy
aws ec2 delete-spot-datafeed-subscription

Spot Instance Limits

Spot instance requests are subject to the following limits:

Limits

Unsupported Instance Types
Spot Request Limits
Spot Bid Price Limit
Spot Fleet Limits
Unsupported Instance Types

The following instance types are not supported for Spot:

T2
HS1
Some Spot instance types aren't available in every region. To view the supported instance types for a region, go to Spot Instance Pricing and select the region.

Spot Request Limits

By default, there is an account limit of 20 Spot instances per region. If you terminate your Spot instance but do not cancel the request, the request counts against this limit until Amazon EC2 detects the termination and closes the request.

Spot instance limits are dynamic. When your account is new, your limit might be lower than 20 to start, but increase over time. In addition, your account might have limits on specific Spot instance types. If you submit a Spot instance request and you receive the error Max spot instance count exceeded, you can go to AWS Support Center and submit a limit increase request form. For Use Case Description, indicate that you need an increase in your limits for Spot instance requests.

Spot Bid Price Limit

The bid price limit for Spot instances is ten times the On-Demand price. This limit is designed to help you control costs.

Spot Fleet Limits

The usual Amazon EC2 limits apply to instances launched by a Spot fleet, such as Spot bid price limits, instance limits, and volume limits. In addition, the following limits apply:

The number of active Spot fleets per region: 1,000
The number of launch specifications per fleet: 50
The size of the user data in a launch specification: 16 KB
The target capacity per Spot fleet: 3,000
The target capacity across all Spot fleets in a region: 5,000
A Spot fleet request can't span regions.
A Spot fleet request can't span different subnets from the same Availability Zone.

Dedicated Hosts

An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts allow you to use your existing per-socket, per-core, or per-VM software licenses, including Windows Server, Microsoft SQL Server, SUSE, Linux Enterprise Server, and so on.

Contents

Differences between Dedicated Hosts and Dedicated Instances
Pricing and Billing
Dedicated Hosts Limitations and Restrictions
Dedicated Host Configurations
Using Dedicated Hosts
Monitoring Dedicated Hosts
Differences between Dedicated Hosts and Dedicated Instances

Dedicated Hosts and Dedicated Instances can both be used to launch Amazon EC2 instances onto physical servers that are dedicated for your use.

There are no performance, security, or physical differences between Dedicated Instances and instances on Dedicated Hosts. However, Dedicated Hosts give you additional visibility and control over how instances are placed on a physical server.

When you use Dedicated Hosts, you have control over instance placement on the host using the Host Affinity and Instance Auto-placement settings. With Dedicated Instances, you don't have control over which host your instance launches and runs on. If your organization wants to use AWS, but has an existing software license with hardware compliance requirements, this allows visibility into the host's hardware so you can meet those requirements.

For more information about the differences between Dedicated Hosts and Dedicated Instances, see Amazon EC2 Dedicated Hosts.

For more information about working with Dedicated Hosts and Dedicated Instances, see Modifying Instance Tenancies.

Pricing and Billing

On-Demand Dedicated Hosts

On-Demand billing is automatically activated when you allocate a Dedicated Host to your account.

You are billed an hourly On-Demand rate. Rates vary based on the instance type that the Dedicated Host supports and the region in which the Dedicated Host is running. The instance type size or the number of instances that are running on the Dedicated Host do not have an impact on the cost of the host.

To terminate On-Demand billing, you must first stop instances running on the Dedicated Host and then release it. For more information, see Managing and Releasing Dedicated Hosts.

Dedicated Host Reservations

Dedicated Host Reservations provide a billing discount compared to running On-Demand Dedicated Hosts. Reservations are available in three payment options:

No Upfront—No Upfront Reservations provide you with a discount on your Dedicated Host usage over a term and do not require an upfront payment. Available for a one-year term only.
Partial Upfront—A portion of the reservation must be paid upfront and the remaining hours in the term are billed at a discounted rate. Available in one-year and three-year terms.
All Upfront—Provides the lowest effective price. Available in one-year and three-year terms and covers the entire cost of the term upfront, with no additional charges going forward.
You must have active Dedicated Hosts in your account before you can purchase reservations. Each reservation covers a single, specific Dedicated Host in your account. Reservations are applied to the instance family on the host, not the instance size. If you have three Dedicated Hosts with different instances sizes (m4.xlarge, m4.medium, and m4.large) you can associate a single m4 reservation with all those Dedicated Hosts. The instance family and region of the reservation must match that of the Dedicated Hosts you want to associate it with.

Note
When a reservation is associated with a Dedicated Host, the Dedicated Host can't be released until the reservation's term is over.
Purchasing Dedicated Host Reservations

You can purchase Dedicated Host Reservations using the console or the API.

To purchase Dedicated Host Reservations using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Dedicated Hosts page choose Dedicated Host Reservations.

Choose Purchase Dedicated Host Reservation.

On the Purchase Dedicated Host Reservation screen, you can search for offerings using the default settings or you can specify a configuration for the offering.

Host instance family—The options listed correspond with the Dedicated Hosts in your account that are not assigned to a reservation.
Availability Zone—The Availability Zone of the Dedicated Hosts in your account that aren't assigned to a reservation.
Payment Option—The payment option for the offering.
Term—The term of the reservation. Can be one or three years.
Choose Find offering.

Select an offering.

Choose the Dedicated Hosts to associate with the Dedicated Host Reservation.

Choose Review.

Review your order and choose Purchase to complete the transaction.

Viewing Dedicated Host Reservations

You can view information about the Dedicated Hosts associated with your reservation, the term of the reservation, the payment option selected, and the start and end dates of the reservation.

View details of Dedicated Host Reservations

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Dedicated Hosts page, choose Dedicated Host Reservations.

Choose the reservation from the list provided.

Select Details for information about the reservation.

Select Hosts for information about the Dedicated Hosts the reservation is associated with.

Dedicated Hosts Limitations and Restrictions

Before you allocate Dedicated Hosts, take note of the following limitations and restrictions.

RHEL, SUSE Linux, and Windows AMIs offered by AWS or on the AWS Marketplace cannot be used with Dedicated Hosts
Amazon EC2 instance auto recovery is not supported.
Up to two On-Demand Dedicated Hosts per instance family, per region can be allocated. It is possible to request a limit increase: Request to Raise Allocation Limit on Amazon EC2 Dedicated Hosts.
The instances that run on a Dedicated Host can only be launched in a VPC.
Host limits are independent from instance limits. Instances that you are running on Dedicated Hosts do not count towards your instance limits.
Auto Scaling groups are not supported.
Amazon RDS instances are not supported.
The AWS Free Usage tier is not available for Dedicated Hosts.
Instance placement control refers to managing instance launches onto Dedicated Hosts. Placement groups are not supported for Dedicated Hosts.
Dedicated Host Configurations

Dedicated Hosts are configured to support a single instance type and size capacity. The number of instances you can launch onto a Dedicated Host depends on the instance type that the Dedicated Host is configured to support. For example, if you allocated a c3.xlarge Dedicated Host, you'd have the right to launch up to 8 c3.xlarge instances on the Dedicated Host. To determine the number of instance type sizes that you can run on a particular Dedicated Host, see Amazon EC2 Dedicated Hosts Pricing.

Using Dedicated Hosts

To use a Dedicated Host, you first allocate hosts for use in your account. You then launch instances onto the hosts by specifying host tenancy for the instance. The instance auto-placement setting allows you to control whether an instance can launch onto a particular host. When an instance is stopped and restarted, the Host affinity setting determines whether it's restarted on the same, or a different, host. If you no longer need an On-Demand host, you can stop the instances running on the host, direct them to launch on a different host, and then release the Dedicated Host.

Contents

Bring Your Own License
Allocating Dedicated Hosts
Launching Instances onto Dedicated Hosts
Understanding Instance Placement and Host Affinity
Modifying Instance Tenancies
Managing and Releasing Dedicated Hosts
API and CLI Command Overview
Tracking Configuration Changes with AWS Config
Bring Your Own License

You can use your own software licenses on Dedicated Hosts. These are the general steps you need to follow in order to bring your own volume licensed machine image into Amazon EC2.

Verify that the license terms controlling the use of your machine images (AMIs) allow the usage of a machine image in a virtualized cloud environment. For more information about Microsoft Licensing, see Amazon Web Services and Microsoft Licensing.

After you have verified that your machine image can be used within Amazon EC2, import your machine images using the ImportImage API operation made available by the VM Import/Export tools. For information about restrictions and limitations, see VM Import/Export Prerequisites. For information about how to import your VM using ImportImage, see Importing a VM into Amazon EC2 Using ImportImage.

If you need a mechanism to track how your images were used in AWS, enable host recording in the AWS Config service. You can use AWS Config to record configuration changes to a Dedicated Host and use the output as a data source for license reporting. For more information, see Tracking Configuration Changes with AWS Config.

After you've imported your machine image, you can launch instances from this image onto active Dedicated Hosts in your account.

When you run these instances, depending on the operating system, you may be required to activate these instances against your own KMS server (for example, Windows Server or Windows SQL Server). You cannot activate your imported Windows AMI against the Amazon Windows KMS server.

Allocating Dedicated Hosts

To begin using Dedicated Hosts, they need to be allocated to your account. You can use the AWS Management Console, interact directly with the API, or use the command line interface to perform these tasks. Follow these steps every time you allocate a Dedicated Host.

To allocate Dedicated Hosts to your account

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Dedicated Hosts page, choose Allocate Dedicated Host.

Configure your host using the options provided:

Instance type—Instance type that will be available on the Dedicated Host.

Availability Zone—The Availability Zone for the Dedicated Host.

Allow instance auto-placement—The default setting is Off. The Dedicated Host accepts host tenancy instance launches only (provided capacity is available). When instance auto-placement is On, any instances with the tenancy of host, and matching the Dedicated Host's configuration, can be launched onto the host.

Quantity—The number of hosts to allocate with these settings.

Choose Allocate host.

The Dedicated Host capacity is made available in your account immediately.

If you launch instances with tenancy host but do not have any active Dedicated Hosts in your account, you receive an error and the instance launch fails.

Launching Instances onto Dedicated Hosts

After you have allocated a Dedicated Host, you can launch instances onto it. Instances with the tenancy host can be launched onto a specific Dedicated Host or Amazon EC2 can select the appropriate Dedicated Hosts for you (auto-placement). You cannot launch instances with the tenancy host if you do not have active Dedicated Hosts in your account with available capacity matching the instance type configuration of the instances you are launching.

Note
The instances launched onto Dedicated Hosts can only be launched in a VPC. For more information, see Introduction to VPC.
Before you launch your instances, take note of the limitations. For more information, see Dedicated Hosts Limitations and Restrictions.

Launching instances onto a Dedicated Host from the Dedicated Hosts page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Dedicated Hosts page, select a host, choose Actions and then choose Launch Instance(s) onto Host.

Select the AMI to use. If you have imported your own AMI, choose My AMIs on the left sidebar and select the relevant AMI.

Choose the instance type for the Dedicated Host; this is the only instance type you can launch onto the host.

On the Configure Instance Details page, the Tenancy and Host options are pre-selected. You can toggle the Affinity setting to On or Off.

On—If stopped, the instance always restarts on that specific host.
Off—The instance launches onto the specified Dedicated Host, but is not guaranteed to restart on it if stopped.
Complete the rest of the steps and choose Launch Instances.

The instance is automatically launched onto the Dedicated Host that you specified. To view the instances on a Dedicated Host, go to the Dedicated Hosts page, and select the Dedicated Host that you specified when you launched the instance.

Launching instances onto a specific Dedicated Host from the Instances page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Instances page, choose Launch Instance.

Select an AMI from the list. If you have imported your own AMI, choose My AMIs and select the imported image. Not all AMIs can be used with Dedicated Hosts.

Select the type of instance to launch.

On the Configure Instance Details page, the Dedicated Host settings are:

Tenancy—Dedicated host — Launch this instance on a Dedicated host. If you're not able to choose this, check whether you have selected an incompatible AMI or instance type.
Host—Select a host. If you are unable to select a Dedicated Host, check:
Whether the selected subnet is in a different Availability Zone to the host.
That the instance type you've selected matches the instance type that the Dedicated Host supports. If you don't have matching, running hosts, the only option available is Use auto-placement but the instance launch fails unless there is available, matching Dedicated Host capacity in your account.
Affinity—The default setting for this is Off. The instance launches onto the specified Dedicated Host, but is not guaranteed to restart on it if stopped.
Note
If you are unable to see these settings, check that you have selected a VPC in the Network menu.
Complete the rest of the configuration steps. Choose Review and Launch.

Choose Launch to launch your instance.

Select an existing key pair, or create a new one. Choose Launch Instances.

Launching instances onto any Dedicated Host from the Instances page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Instances page, choose Launch Instance.

Select an AMI from the list. If you have imported your own AMI, choose My AMIs and select the imported image. Not all AMIs can be used with Dedicated Hosts.

Select the type of instance to launch.

On the Configure Instance Details page, the Dedicated Host settings are:

Tenancy—Dedicated host — Launch this instance on a Dedicated host If you're not able to choose this, check whether you have selected an incompatible AMI or instance type.
Host—For this type of launch, keep the setting as Use auto-placement.
Affinity—The default setting for this is Off. The instance launches onto any available Dedicated Host in your account, but is not guaranteed to restart on that host if stopped.
If you are unable to see these settings, check that you have selected a VPC in the Network menu.

Complete the rest of the configuration steps. Choose Review and Launch.

Choose Launch to launch your instance.

Select an existing key pair, or create a new one. Choose Launch Instances.

Modifying Instance Tenancies

You can modify the tenancy of a Dedicated Instance from dedicated to host, and vice-versa if it is not using a Windows, SUSE, or RHEL AMI provided by Amazon EC2. You need to stop your Dedicated Instance in order to do this. Instances with shared tenancy cannot be modified to host tenancy.

Modify instance tenancy from dedicated to host

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Instances, then select the Dedicated Instances to modify.

Choose Actions, Instance State, and Stop.

Open the context (right-click) menu on the instance and choose Instance Settings, Modify Instance Placement.

On the Modify Instance Placement page, do the following:

Tenancy—Choose Launch this instance on a Dedicated host.
Affinity—Choose either This instance can run on any one of my Hosts or This instance can only run on the selected Host.
If you choose This instance can run on any one of my Hosts, the instance launches onto any available, compatible Dedicated Hosts in your account.
If you choose This instance can only run on the selected Host, select a value for Target Host. If no target host is listed, you may not have available, compatible Dedicated Hosts in your account.
Choose Save.

When you restart your instance Amazon EC2 places your instance on an available Dedicated Host in your account, provided it supports the instance type that you're launching.

Managing and Releasing Dedicated Hosts

You can use the console, interact directly with the API, or use the command line interface to view details about individual instances on a host and release an On-Demand Dedicated Host.

To view details of instances on a Dedicated Host

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Dedicated Hosts page, select the host to view more information about.

Choose the Description tab for information about the host. Choose the Instances tab for information about instances running on your host.

To release a Dedicated Host

Any running instances on the Dedicated Host need to be stopped before you can release the host. These instances can be migrated to other Dedicated Hosts in your account so that you can continue to use them. For more information, see Modifying Instance Auto-Placement and Host Affinity. These steps apply only to On-Demand Dedicated Hosts.

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Dedicated Hosts page, select the Dedicated Host to release.

Choose Actions, Release Hosts.

Confirm your choice by choosing Release.

After you release a Dedicated Host, you cannot reuse the same host or host ID again.

When the Dedicated Host is released you are no longer charged On-Demand billing rates for it. The Dedicated Host status is changed to released and you are not able to launch any instances onto that host.

If you've recently released Dedicated Hosts, it may take some time for them to stop counting towards your limit. During this time, you may experience LimitExceeded errors when trying to allocate new Dedicated Hosts. If this is the case, try allocating new hosts again after a few minutes.

The instances that were stopped are still available for use and are listed on the Instances page. They retain their host tenancy setting.

API and CLI Command Overview

You can perform the tasks described in this section using an API or the command line.

To allocate Dedicated Hosts to your account

allocate-hosts (AWS CLI)
AllocateHosts (Amazon EC2 Query API)
New-EC2Hosts (AWS Tools for Windows PowerShell)
To describe your Dedicated Hosts

describe-hosts (AWS CLI)
DescribeHosts (Amazon EC2 Query API)
Get-EC2Hosts (AWS Tools for Windows PowerShell)
To modify your Dedicated Hosts

modify-hosts (AWS CLI)
ModifyHosts (Amazon EC2 Query API)
Edit-EC2Hosts (AWS Tools for Windows PowerShell)
To modify instance auto-placement

modify-instance-placement (AWS CLI)
ModifyInstancePlacement (Amazon EC2 Query API)
Edit-EC2InstancePlacement (AWS Tools for Windows PowerShell)
To release your Dedicated Hosts

release-hosts (AWS CLI)
ReleaseHosts (Amazon EC2 Query API)
Remove-EC2Hosts (AWS Tools for Windows PowerShell)
Tracking Configuration Changes with AWS Config

You can use AWS Config to record configuration changes for Dedicated Hosts, and instances that are launched, stopped, or terminated on them. You can then use the information captured by AWS Config as a data source for license reporting.

AWS Config records configuration information for Dedicated Hosts and instances individually and pairs this information through relationships. There are three reporting conditions.

AWS Config recording status—When On, AWS Config is recording one or more AWS resource types, which can include Dedicated Hosts and Dedicated Instances. To capture the information required for license reporting, verify that hosts and instances are being recorded with the following fields.
Host recording status—When Enabled, the configuration information for Dedicated Hosts is recorded.
Instance recording status—When Enabled, the configuration information for Dedicated Instances is recorded.
If any of these three conditions are disabled, the icon in the Edit Config Recording button is red. To derive the full benefit of this tool, ensure that all three recording methods are enabled. When all three are enabled, the icon is green. To edit the settings, choose Edit Config Recording. You are directed to the Set up AWS Config page in the AWS Config console, where you can set up AWS Config and start recording for your hosts, instances, and other supported resource types. For more information, see Setting up AWS Config using the Console in the AWS Config Developer Guide.

Note
AWS Config records your resources after it discovers them, which might take several minutes.
After AWS Config starts recording configuration changes to your hosts and instances, you can get the configuration history of any host that you have allocated or released and any instance that you have launched, stopped, or terminated. For example, at any point in the configuration history of a Dedicated Host, you can look up how many instances are launched on that host alongside the number of sockets and cores on the host. For any of those instances, you can also look up the ID of its Amazon Machine Image (AMI). You can use this information to report on licensing for your own server-bound software that is licensed per-socket or per-core.

You can view configuration histories in any of the following ways.

By using the AWS Config console. For each recorded resource, you can view a timeline page, which provides a history of configuration details. To view this page, choose the grey icon in the Config Timeline column of the Dedicated Hosts page. For more information, see Viewing Configuration Details in the AWS Config Console in the AWS Config Developer Guide.
By running AWS CLI commands. First, you can use the list-discovered-resources command to get a list of all hosts and instances. Then, you can use the get-resource-config-history command to get the configuration details of a host or instance for a specific time interval. For more information, see View Configuration Details Using the CLI in the AWS Config Developer Guide.
By using the AWS Config API in your applications. First, you can use the ListDiscoveredResources action to get a list of all hosts and instances. Then, you can use the GetResourceConfigHistory action to get the configuration details of a host or instance for a specific time interval.
For example, to get a list of all of your Dedicated Hosts from AWS Config, run a CLI command such as the following:

Copy
aws configservice list-discovered-resources --resource-type AWS::EC2::Host
To obtain the configuration history of a Dedicated Host from AWS Config, run a CLI command such as the following:

Copy
aws configservice get-resource-config-history --resource type AWS::EC2::Instance --resource-id i-36a47fdf
To manage AWS Config settings using the AWS Management Console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Dedicated Hosts page, choose Edit Config Recording.

In the AWS Config console, follow the steps provided to turn on recording. For more information, see Setting up AWS Config using the Console.

For more information, see Viewing Configuration Details in the AWS Config Console.

To activate AWS Config using the command line or API

Using the AWS CLI, see Viewing Configuration Details in the AWS Config Console in the AWS Config Developer Guide.
Using the Amazon EC2 API, see GetResourceConfigHistory.

Understanding Instance Placement and Host Affinity

Placement control happens on both the instance level and host level.

Contents

Instance Auto-Placement
Host Affinity
Modifying Instance Auto-Placement and Host Affinity
Modifying Instance Host Affinity
Instance Auto-Placement

Auto-placement allows you to manage whether instances that you launch are launched onto a specific host, or onto any host that has matching configurations. The default setting for this is Off. This means that the Dedicated Host you are allocating only accepts host tenancy instances launches that specify the unique host ID. Instances launched without a host ID specified are not able to launch onto a host that have instance auto-placement set to Off.

Host Affinity

Host Affinity establishes a launch relationship between an instance and a Dedicated Host. When affinity is set to host, an instance launched onto a specific host always restarts on the same host if stopped. This applies to both targeted and untargeted launches.

If affinity is set to default, and you stop and restart the instance, it can be restarted on any available host but tries to launch back onto the last Dedicated Host it ran on (on a best-effort basis).

You can modify the relationship between an instance and a Dedicated Host by changing the affinity from host to default and vice-versa. For more information, see Modifying Instance Tenancies.

Modifying Instance Auto-Placement and Host Affinity

You can manage instance placement controls using the Amazon EC2 console, the API, or CLI.

To modify the instance placement settings of your instances, first stop the instances and then edit the instance placement settings.

Note
If the instance is stopped and restarted, it is not guaranteed to restart on the same Dedicated Host.
To edit an instance's placement settings (any available hosts)

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Instances page, select the instance to edit.

Choose Actions, Instance State, and Stop.

Choose Actions, Instance Settings, and Modify Instance Placement.

Change the instance tenancy to Launch this instance on a Dedicated host.

Choose This instance can run on any one of my Hosts. The instance launches onto any Dedicated Host that has auto-placement enabled.

Choose Save to continue.

Open the context (right-click) menu on the instance and choose Instance State, Start.

To edit an instance's placement settings (specific Dedicated Host)

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the Instances page, select the instance to edit.

Choose Actions, Instance State, and Stop.

Choose Actions, Instance Settings, and Modify Instance Placement.

Change the instance tenancy to Launch this instance on a Dedicated host.

Choose This instance can only run on the selected Host. Then select a value for Target Host and choose whether you want the instance to be placed on any available host, or a specific host.

Choose Save to continue.

Open the context (right-click) menu on the instance and choose Instance State, Start.

Modifying Instance Host Affinity

If you no longer want an instance to have affinity with a host, you can stop the instance and change its affinity to default. This removes the persistence between the instance and the host. However, when you restart the instance, it may launch back onto the same Dedicated Host (depending on Dedicated Host availability in your account, and on a best-effort basis). However, if it is stopped again, it will not restart on the same host.

Monitoring Dedicated Hosts

Amazon EC2 constantly monitors the state of your Dedicated Hosts; updates are communicated on the Amazon EC2 console. You can also obtain information about your Dedicated Hosts using the API or CLI.

The following table illustrates the possible State values in the console.

State	Description
available	AWS hasn't detected an issue with the Dedicated Host; no maintenance or repairs are scheduled. Instances can be launched onto this Dedicated Host.
released	The Dedicated Host has been released. The host ID is no longer in use. Released hosts cannot be reused.
under-assessment	AWS is exploring a possible issue with the Dedicated Host. If action needs to be taken, you will be notified via the AWS Management Console or email. Instances cannot be launched onto a Dedicated Host in this state.
permanent-failure	An unrecoverable failure has been detected. You will receive an eviction notice through your instances and by email. Your instances may continue to run. If you stop or terminate all instances on a Dedicated Host with this state, AWS retires the host. Instances cannot be launched onto Dedicated Hosts in this state.
released-permanent-failure	AWS permanently releases Dedicated Hosts that have failed and no longer have running instances on them. The Dedicated Host ID is no longer available for use.

Dedicated Instances

Dedicated instances are Amazon EC2 instances that run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. Your Dedicated instances are physically isolated at the host hardware level from instances that belong to other AWS accounts. Dedicated instances may share hardware with other instances from the same AWS account that are not Dedicated instances.

Note
A Dedicated Host is also a physical server that's dedicated for your use. With a Dedicated Host, you have visibility and control over how instances are placed on the server. For more information, see Dedicated Hosts.
Topics

Dedicated Instance Basics
Working with Dedicated Instances
API and Command Overview
Dedicated Instance Basics

Each instance that you launch into a VPC has a tenancy attribute. This attribute has the following values.

Value	Description
default
Your instance runs on shared hardware.
dedicated
Your instance runs on single-tenant hardware.
host
Your instance runs on a Dedicated Host, which is an isolated server with configurations that you can control.
You cannot change the tenancy of a default instance after you've launched it. You can change the tenancy of an instance from dedicated to host after you've launched it, and vice versa. For more information, see Changing the Tenancy of an Instance.

Each VPC has a related instance tenancy attribute. You can't change the instance tenancy of a VPC after you create it. This attribute has the following values.

Value	Description
default
An instance launched into the VPC runs on shared hardware by default, unless you explicitly specify a different tenancy during instance launch.
dedicated
An instance launched into the VPC is a Dedicated instance by default, unless you explicitly specify a tenancy of host during instance launch. You cannot specify a tenancy of default during instance launch.
To create Dedicated instances, you can do the following:

Create the VPC with the instance tenancy set to dedicated (all instances launched into this VPC are Dedicated instances).
Create the VPC with the instance tenancy set to default, and specify a tenancy of dedicated for any instances when you launch them.
Dedicated Instances Limitations

Some AWS services or their features won't work with a VPC with the instance tenancy set to dedicated. Check the service's documentation to confirm if there are any limitations.

Some instance types cannot be launched into a VPC with the instance tenancy set to dedicated. For more information about supported instances types, see Amazon EC2 Dedicated Instances.

Amazon EBS with Dedicated Instances

When you launch an Amazon EBS-backed Dedicated instance, the EBS volume doesn't run on single-tenant hardware.

Reserved Instances with Dedicated Tenancy

To guarantee that sufficient capacity will be available to launch Dedicated instances, you can purchase Dedicated Reserved Instances. For more information, see Reserved Instances.

When you purchase a Dedicated Reserved Instance, you are purchasing the capacity to launch a Dedicated instance into a VPC at a much reduced usage fee; the price break in the hourly charge applies only if you launch an instance with dedicated tenancy. However, if you purchase a Reserved Instance with a default tenancy value, you won't get a Dedicated Reserved Instance if you launch an instance with dedicated instance tenancy.

In addition, you can't change the tenancy of a Reserved Instance after you've purchased it.

Auto Scaling of Dedicated Instances

For information about using Auto Scaling to launch Dedicated instances, see Auto Scaling in Amazon Virtual Private Cloud in the Auto Scaling User Guide.

Dedicated Spot Instances

You can run a Dedicated Spot instance by specifying a tenancy of dedicated when you create a Spot instance request. For more information, see Specifying a Tenancy for Your Spot Instances.

Pricing for Dedicated Instances

Pricing for Dedicated instances is different to pricing for On-Demand instances. For more information, see the Amazon EC2 Dedicated Instances product page.

Working with Dedicated Instances

You can create a VPC with an instance tenancy of dedicated to ensure that all instances launched into the VPC are Dedicated instances. Alternatively, you can specify the tenancy of the instance during launch.

Topics

Creating a VPC with an Instance Tenancy of Dedicated
Launching Dedicated Instances into a VPC
Displaying Tenancy Information
Changing the Tenancy of an Instance
Creating a VPC with an Instance Tenancy of Dedicated

When you create a VPC, you have the option of specifying its instance tenancy. You can create a VPC using the VPC wizard or the Your VPCs page in the Amazon VPC console.

To create a VPC with an instance tenancy of dedicated (VPC Wizard)

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

From the dashboard, choose Start VPC Wizard.

Select a VPC configuration, and then choose Select.

On the next page of the wizard, choose Dedicated from the Hardware tenancy list.

Choose Create VPC.

To create a VPC with an instance tenancy of dedicated (Create VPC dialog box)

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs, and then Create VPC.

For Tenancy, choose Dedicated. Specify the CIDR block, and choose Yes, Create.

If you launch an instance into a VPC that has an instance tenancy of dedicated, your instance is automatically a Dedicated instance, regardless of the tenancy of the instance.

Launching Dedicated Instances into a VPC

You can launch a Dedicated instance using the Amazon EC2 launch instance wizard.

To launch an instance with a tenancy of dedicated into a VPC with a tenancy of default

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Launch Instance.

On the Choose an Amazon Machine Image (AMI) page, select an AMI and choose Select.

On the Choose an Instance Type page, select the instance type and choose Next: Configure Instance Details.

Note
Ensure that you choose an instance type that's supported as a Dedicated instance. For more information, see Amazon EC2 Dedicated Instances.
On the Configure Instance Details page, select a VPC and subnet. Choose Dedicated - Run a dedicated instance from the Tenancy list, and then Next: Add Storage.

Continue as prompted by the wizard. When you've finished reviewing your options on the Review Instance Launch page, choose Launch to choose a key pair and launch the Dedicated instance.

For more information about launching an instance with a tenancy of host, see Launching Instances onto Dedicated Hosts.

Displaying Tenancy Information

To display tenancy information for your VPC

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs.

Check the instance tenancy of your VPC in the Tenancy column.

If the Tenancy column is not displayed, choose Edit Table Columns (the gear-shaped icon), Tenancy in the Show/Hide Columns dialog box, and then Close.

To display tenancy information for your instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Check the tenancy of your instance in the Tenancy column.

If the Tenancy column is not displayed, do one of the following:

Choose Edit Table Columns (the gear-shaped icon), Tenancy in the Show/Hide Columns dialog box, and then Close.
Select the instance. The Description tab in the details pane displays information about the instance, including its tenancy.
Changing the Tenancy of an Instance

Depending on your instance type and platform, you can change the tenancy of a stopped Dedicated instance to host after launching it. The next time the instance starts, it's started on a Dedicated Host that's allocated to your account. For more information about allocating and working with Dedicated hosts, and the instance types that can be used with Dedicated hosts, see Using Dedicated Hosts. Similarly, you can change the tenancy of a stopped Dedicated Host instance to dedicated after launching it. The next time the instance starts, it's started on single-tenant hardware that we control.

To change the tenancy of an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances, and then select your instance.

Choose Actions, then Instance State, and then choose Stop.

Choose Actions, then Instance Settings, and then choose Modify Instance Placement.

In the Tenancy list, choose whether to run your instance on dedicated hardware or on a Dedicated Host. Choose Save.

API and Command Overview

You can perform the tasks described on this page using the command line or an API.

Set the tenancy option when you create a VPC

create-vpc (AWS CLI)
New-EC2Vpc (AWS Tools for Windows PowerShell)
Describe the supported tenancy options for instances launched into the VPC

describe-vpcs (AWS CLI)
Get-EC2Vpc (AWS Tools for Windows PowerShell)
Set the tenancy option for an instance during launch

run-instances (AWS CLI)
New-EC2Instance (AWS Tools for Windows PowerShell)
Describe the tenancy value of an instance

describe-instances (AWS CLI)
Get-EC2Instance (AWS Tools for Windows PowerShell)
Describe the tenancy value of a Reserved Instance

describe-reserved-instances (AWS CLI)
Get-EC2ReservedInstance (AWS Tools for Windows PowerShell)
Describe the tenancy value of a Reserved Instance offering

describe-reserved-instances-offerings (AWS CLI)
Get-EC2ReservedInstancesOffering (AWS Tools for Windows PowerShell)
Modify the tenancy value of an instance

modify-instance-placement (AWS CLI)
Edit-EC2InstancePlacement (AWS Tools for Windows PowerShell)

Instance Lifecycle

By working with Amazon EC2 to manage your instances from the moment you launch them through their termination, you ensure that your customers have the best possible experience with the applications or sites that you host on your instances.

The following illustration represents the transitions between instance states. Notice that you can't stop and start an instance store-backed instance. For more information about instance store-backed instances, see Storage for the Root Device.


        The instance lifecycle
      
Instance Launch

When you launch an instance, it enters the pending state. The instance type that you specified at launch determines the hardware of the host computer for your instance. We use the Amazon Machine Image (AMI) you specified at launch to boot the instance. After the instance is ready for you, it enters the running state. You can connect to your running instance and use it the way that you'd use a computer sitting in front of you.

As soon as your instance transitions to the running state, you're billed for each hour or partial hour that you keep the instance running; even if the instance remains idle and you don't connect to it.

For more information, see Launch Your Instance and Connect to Your Linux Instance.

Instance Stop and Start (Amazon EBS-backed instances only)

If your instance fails a status check or is not running your applications as expected, and if the root volume of your instance is an Amazon EBS volume, you can stop and start your instance to try to fix the problem.

When you stop your instance, it enters the stopping state, and then the stopped state. We don't charge hourly usage or data transfer fees for your instance after you stop it, but we do charge for the storage for any Amazon EBS volumes. While your instance is in the stopped state, you can modify certain attributes of the instance, including the instance type.

When you start your instance, it enters the pending state, and in most cases, we move the instance to a new host computer. (Your instance may stay on the same host computer if there are no problems with the host computer.) When you stop and start your instance, you'll lose any data on the instance store volumes on the previous host computer.

If your instance is running in EC2-Classic, it receives a new private IPv4 address, which means that an Elastic IP address (EIP) associated with the private IPv4 address is no longer associated with your instance. If your instance is running in EC2-VPC, it retains its private IPv4 address, which means that an EIP associated with the private IPv4 address or network interface is still associated with your instance. If your instance has an IPv6 address, it retains its IPv6 address.

Each time you transition an instance from stopped to running, we charge a full instance hour, even if these transitions happen multiple times within a single hour.

For more information, see Stop and Start Your Instance.

Instance Reboot

You can reboot your instance using the Amazon EC2 console, a command line tool, and the Amazon EC2 API. We recommend that you use Amazon EC2 to reboot your instance instead of running the operating system reboot command from your instance.

Rebooting an instance is equivalent to rebooting an operating system; the instance remains on the same host computer and maintains its public DNS name, private IP address, and any data on its instance store volumes. It typically takes a few minutes for the reboot to complete, but the time it takes to reboot depends on the instance configuration.

Rebooting an instance doesn't start a new instance billing hour.

For more information, see Reboot Your Instance.

Instance Retirement

An instance is scheduled to be retired when AWS detects irreparable failure of the underlying hardware hosting the instance. When an instance reaches its scheduled retirement date, it is stopped or terminated by AWS. If your instance root device is an Amazon EBS volume, the instance is stopped, and you can start it again at any time. If your instance root device is an instance store volume, the instance is terminated, and cannot be used again.

For more information, see Instance Retirement.

Instance Termination

When you've decided that you no longer need an instance, you can terminate it. As soon as the status of an instance changes to shutting-down or terminated, you stop incurring charges for that instance.

Note that if you enable termination protection, you can't terminate the instance using the console, CLI, or API.

After you terminate an instance, it remains visible in the console for a short while, and then the entry is automatically deleted. You can also describe a terminated instance using the CLI and API. Resources (such as tags) are gradually disassociated from the terminated instance, therefore may no longer be visible on the terminated instance after a short while. You can't connect to or recover a terminated instance.

Each Amazon EBS-backed instance supports the InstanceInitiatedShutdownBehavior attribute, which controls whether the instance stops or terminates when you initiate a shutdown from within the instance itself (for example, by using the shutdown command on Linux). The default behavior is to stop the instance. You can modify the setting of this attribute while the instance is running or stopped.

Each Amazon EBS volume supports the DeleteOnTermination attribute, which controls whether the volume is deleted or preserved when you terminate the instance it is attached to. The default is to delete the root device volume and preserve any other EBS volumes.

For more information, see Terminate Your Instance.

Differences Between Reboot, Stop, and Terminate

The following table summarizes the key differences between rebooting, stopping, and terminating your instance.

Characteristic	Reboot	Stop/start (Amazon EBS-backed instances only)	Terminate
Host computer
The instance stays on the same host computer
The instance runs on a new host computer
None
Private and public IPv4 addresses
These addresses stay the same
EC2-Classic: The instance gets new private and public IPv4 addresses

EC2-VPC: The instance keeps its private IPv4 address. The instance gets a new public IPv4 address, unless it has an Elastic IP address (EIP), which doesn't change during a stop/start.
None
Elastic IP addresses (IPv4)
The Elastic IP remains associated with the instance
EC2-Classic: The Elastic IP is disassociated from the instance

EC2-VPC: The Elastic IP remains associated with the instance
The Elastic IP is disassociated from the instance
IPv6 address (EC2-VPC only)	The address stays the same	The instance keeps its IPv6 address	None
Instance store volumes
The data is preserved
The data is erased
The data is erased
Root device volume
The volume is preserved
The volume is preserved
The volume is deleted by default
Billing
The instance billing hour doesn't change.
You stop incurring charges for an instance as soon as its state changes to stopping. Each time an instance transitions from stopped to running, we start a new instance billing hour.
You stop incurring charges for an instance as soon as its state changes to shutting-down.
Note that operating system shutdown commands always terminate an instance store-backed instance. You can control whether operating system shutdown commands stop or terminate an Amazon EBS-backed instance. For more information, see Changing the Instance Initiated Shutdown Behavior.

Launch Your Instance

An instance is a virtual server in the AWS cloud. You launch an instance from an Amazon Machine Image (AMI). The AMI provides the operating system, application server, and applications for your instance.

When you sign up for AWS, you can get started with Amazon EC2 for free using the AWS Free Tier. You can either leverage the free tier to launch and use a micro instance for free for 12 months. If you launch an instance that is not within the free tier, you incur the standard Amazon EC2 usage fees for the instance. For more information, see the Amazon EC2 Pricing.

You can launch an instance using the following methods.

Method	Documentation
[Amazon EC2 console] Use an AMI that you select
Launching an Instance
[Amazon EC2 console] Use an existing instance as a template	
Launching an Instance Using an Existing Instance as a Template
[Amazon EC2 console] Use an Amazon EBS snapshot that you created
Launching a Linux Instance from a Backup
[Amazon EC2 console] Use an AMI that you purchased from the AWS Marketplace
Launching an AWS Marketplace Instance
[AWS CLI] Use an AMI that you select
Using Amazon EC2 through the AWS CLI
[AWS Tools for Windows PowerShell] Use an AMI that you select
Amazon EC2 from the AWS Tools for Windows PowerShell
After you launch your instance, you can connect to it and use it. To begin, the instance state is pending. When the instance state is running, the instance has started booting. There might be a short time before you can connect to the instance. The instance receives a public DNS name that you can use to contact the instance from the Internet. The instance also receives a private DNS name that other instances within the same Amazon EC2 network (EC2-Classic or EC2-VPC) can use to contact the instance. For more information about connecting to your instance, see Connect to Your Linux Instance.

When you are finished with an instance, be sure to terminate it. For more information, see Terminate Your Instance.

Launching an Instance

Before you launch your instance, be sure that you are set up. For more information, see Setting Up with Amazon EC2.

Your AWS account might support both the EC2-Classic and EC2-VPC platforms, depending on when you created your account and which regions you've used. To find out which platform your account supports, see Supported Platforms. If your account supports EC2-Classic, you can launch an instance into either platform. If your account supports EC2-VPC only, you can launch an instance into a VPC only.

Important
When you launch an instance that's not within the AWS Free Tier, you are charged for the time that the instance is running, even if it remains idle.
Launching Your Instance from an AMI

When you launch an instance, you must select a configuration, known as an Amazon Machine Image (AMI). An AMI contains the information required to create a new instance. For example, an AMI might contain the software required to act as a web server: for example, Linux, Apache, and your web	site.

Tip
To ensure faster instance launches, break up large requests into smaller batches. For example, create five separate launch requests for 100 instances each instead of one launch request for 500 instances.
To launch an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation bar at the top of the screen, the current region is displayed. Select the region for the instance. This choice is important because some Amazon EC2 resources can be shared between regions, while others can't. Select the region that meets your needs. For more information, see Resource Locations.


            				Launch instance start
            			
From the Amazon EC2 console dashboard, choose Launch Instance.

On the Choose an Amazon Machine Image (AMI) page, choose an AMI as follows:

Select the type of AMI to use in the left pane:

Quick Start
A selection of popular AMIs to help you get started quickly. To ensure that you select an AMI that is eligible for the free tier, choose Free tier only in the left pane. (Notice that these AMIs are marked Free tier eligible.)

My AMIs
The private AMIs that you own, or private AMIs that have been shared with you.

AWS Marketplace
An online store where you can buy software that runs on AWS, including AMIs. For more information about launching an instance from the AWS Marketplace, see Launching an AWS Marketplace Instance.

Community AMIs
The AMIs that AWS community member have made available for others to use. To filter the list of AMIs by operating system, choose the appropriate check box under Operating system. You can also filter by architecture and root device type.

Check the Root device type listed for each AMI. Notice which AMIs are the type that you need, either ebs (backed by Amazon EBS) or instance-store (backed by instance store). For more information, see Storage for the Root Device.

Check the Virtualization type listed for each AMI. Notice which AMIs are the type that you need, either hvm or paravirtual. For example, some instance types require HVM. For more information, see Linux AMI Virtualization Types.

Choose an AMI that meets your needs, and then choose Select.

On the Choose an Instance Type page, select the hardware configuration and size of the instance to launch. Larger instance types have more CPU and memory. For more information, see Instance Types.

To remain eligible for the free tier, choose the t2.micro instance type. For more information, see T2 Instances.

By default, the wizard displays current generation instance types, and selects the first available instance type based on the AMI that you selected. To view previous generation instance types, choose All generations from the filter list.

Note
If you are new to AWS and would like to set up an instance quickly for testing purposes, you can choose Review and Launch at this point to accept default configuration settings, and launch your instance. Otherwise, to configure your instance further, choose Next: Configure Instance Details.
On the Configure Instance Details page, change the following settings as necessary (expand Advanced Details to see all the settings), and then choose Next: Add Storage:

Number of instances: Enter the number of instances to launch.
Note
To help ensure that you maintain the correct number of instances to handle your application, you can choose Launch into Auto Scaling Group to create a launch configuration and an Auto Scaling group. Auto Scaling scales the number of instances in the group according to your specifications. For more information, see the Auto Scaling User Guide.
Purchasing option: Select Request Spot instances to launch a Spot instance. For more information, see Spot Instances.
Your account may support the EC2-Classic and EC2-VPC platforms, or EC2-VPC only. To find out which platform your account supports, see Supported Platforms. If your account supports EC2-VPC only, you can launch your instance into your default VPC or a nondefault VPC. Otherwise, you can launch your instance into EC2-Classic or a nondefault VPC.
Note
Some instance types must be launched into a VPC. If you don't have a VPC, you can let the wizard create one for you.
To launch into EC2-Classic:
Network: Select Launch into EC2-Classic.
Availability Zone: Select the Availability Zone to use. To let AWS choose an Availability Zone for you, select No preference.
To launch into a VPC:
Network: Select the VPC, or to create a new VPC, choose Create new VPC to go the Amazon VPC console. When you have finished, return to the wizard and choose Refresh to load your VPC in the list.
Subnet: Select the subnet into which to launch your instance. If your account is EC2-VPC only, select No preference to let AWS choose a default subnet in any Availability Zone. To create a new subnet, choose Create new subnet to go to the Amazon VPC console. When you are done, return to the wizard and choose Refresh to load your subnet in the list.
Auto-assign Public IP: Specify whether your instance receives a public IPv4 address. By default, instances in a default subnet receive a public IPv4 address and instances in a nondefault subnet do not. You can select Enable or Disable to override the subnet's default setting. For more information, see Public IPv4 Addresses and External DNS Hostnames.
Auto-assign IPv6 IP: Specify whether your instance receives an IPv6 address from the range of the subnet. Select Enable or Disable to override the subnet's default setting. This option is only available if you've associated an IPv6 CIDR block with your VPC and subnet. For more information, see Your VPC and Subnets in the Amazon VPC User Guide.
IAM role: Select an AWS Identity and Access Management (IAM) role to associate with the instance. For more information, see IAM Roles for Amazon EC2.
Shutdown behavior: Select whether the instance should stop or terminate when shut down. For more information, see Changing the Instance Initiated Shutdown Behavior.
Enable termination protection: Select this check box to prevent accidental termination. For more information, see Enabling Termination Protection for an Instance.
Monitoring: Select this check box to enable detailed monitoring of your instance using Amazon CloudWatch. Additional charges apply. For more information, see Monitoring Your Instances Using CloudWatch.
EBS-Optimized instance: An Amazon EBS-optimized instance uses an optimized configuration stack and provides additional, dedicated capacity for Amazon EBS I/O. If the instance type supports this feature, select this check box to enable it. Additional charges apply. For more information, see Amazon EBS–Optimized Instances.
Tenancy: If you are launching your instance into a VPC, you can choose to run your instance on isolated, dedicated hardware (Dedicated) or on a Dedicated host (Dedicated host). Additional charges may apply. For more information, see Dedicated Instances and Dedicated Hosts.
Network interfaces: If you selected a specific subnet, you can specify up to two network interfaces for your instance:
For Network Interface, select New network interface to let AWS create a new interface, or select an existing, available network interface.
For Primary IP, enter a private IPv4 address from the range of your subnet, or leave Auto-assign to let AWS choose a private IPv4 address for you.
For Secondary IP addresses, choose Add IP to assign more than one private IPv4 address to the selected network interface.
(IPv6-only) For IPv6 IPs, choose Add IP, and enter an IPv6 address from the range of the subnet, or leave Auto-assign to let AWS choose one for you.
Choose Add Device to add a secondary network interface. A secondary network interface can reside in a different subnet of the VPC, provided it's in the same Availability Zone as your instance.
For more information, see Elastic Network Interfaces. If you specify more than one network interface, your instance cannot receive a public IPv4 address. Additionally, you cannot override the subnet's public IPv4 setting using Auto-assign Public IP if you specify an existing network interface for eth0. For more information, see Assigning a Public IPv4 Address During Instance Launch.
Kernel ID: (Only valid for paravirtual (PV) AMIs) Select Use default unless you want to use a specific kernel.
RAM disk ID: (Only valid for paravirtual (PV) AMIs) Select Use default unless you want to use a specific RAM disk. If you have selected a kernel, you may need to select a specific RAM disk with the drivers to support it.
Placement group: A placement group is a logical grouping for your cluster instances. Select an existing placement group, or create a new one. This option is only available if you've selected an instance type that supports placement groups. For more information, see Placement Groups.
User data: You can specify user data to configure an instance during launch, or to run a configuration script. To attach a file, select the As file option and browse for the file to attach.
On the Add Storage page, you can specify volumes to attach to the instance besides the volumes specified by the AMI (such as the root device volume). You can change the following options, then choose Next: Add Tags when you have finished:

Type: Select instance store or Amazon EBS volumes to associate with your instance. The type of volume available in the list depends on the instance type you've chosen. For more information, see Amazon EC2 Instance Store and Amazon EBS Volumes.
Device: Select from the list of available device names for the volume.
Snapshot: Enter the name or ID of the snapshot from which to restore a volume. You can also search for public snapshots by typing text into the Snapshot field. Snapshot descriptions are case-sensitive.
Size: For Amazon EBS-backed volumes, you can specify a storage size. Note that even if you have selected an AMI and instance that are eligible for the free tier, you need to keep under 30 GiB of total storage to stay within the free tier.
Note
Linux AMIs require GPT partition tables and GRUB 2 for boot volumes 2 TiB (2048 GiB) or larger. Many Linux AMIs today use the MBR partitioning scheme, which only supports up to 2047 GiB boot volumes. If your instance does not boot with a boot volume that is 2 TiB or larger, the AMI you are using may be limited to a 2047 GiB boot volume size. Non-boot volumes do not have this limitation on Linux instances.
Note
If you increase the size of your root volume at this point (or any other volume created from a snapshot), you need to extend the file system on that volume in order to use the extra space. For more information about extending your file system after your instance has launched, see Modifying the Size, IOPS, or Type of an EBS Volume on Linux.
Volume Type: For Amazon EBS volumes, select either a General Purpose SSD, Provisioned IOPS SSD, or Magnetic volume. For more information, see Amazon EBS Volume Types.
Note
If you select a Magnetic boot volume, you'll be prompted when you complete the wizard to make General Purpose SSD volumes the default boot volume for this instance and future console launches. (This preference persists in the browser session, and does not affect AMIs with Provisioned IOPS SSD boot volumes.) We recommended that you make General Purpose SSD volumes the default because they provide a much faster boot experience and they are the optimal volume type for most workloads. For more information, see Amazon EBS Volume Types.
Note
Some AWS accounts created before 2012 might have access to Availability Zones in us-west-1 or ap-northeast-1 that do not support Provisioned IOPS SSD (io1) volumes. If you are unable to create an io1 volume (or launch an instance with an io1 volume in its block device mapping) in one of these regions, try a different Availability Zone in the region. You can verify that an Availability Zone supports io1 volumes by creating a 4 GiB io1 volume in that zone.
IOPS: If you have selected a Provisioned IOPS SSD volume type, then you can enter the number of I/O operations per second (IOPS) that the volume can support.
Delete on Termination: For Amazon EBS volumes, select this check box to delete the volume when the instance is terminated. For more information, see Preserving Amazon EBS Volumes on Instance Termination.
Encrypted: Select this check box to encrypt new Amazon EBS volumes. Amazon EBS volumes that are restored from encrypted snapshots are automatically encrypted. Encrypted volumes may only be attached to supported instance types.
On the Add Tags page, specify tags by providing key and value combinations. You can tag the instance, the volumes, or both. Choose Add another tag to add more than one tag to your resources. Choose Next: Configure Security Group when you are done.

On the Configure Security Group page, use a security group to define firewall rules for your instance. These rules specify which incoming network traffic is delivered to your instance. All other traffic is ignored. (For more information about security groups, see Amazon EC2 Security Groups for Linux Instances.) Select or create a security group as follows, and then choose Review and Launch.

To select an existing security group:

Choose Select an existing security group. Your security groups are displayed. (If you are launching into EC2-Classic, these are security groups for EC2-Classic. If you are launching into a VPC, these are security group for that VPC.)

Select a security group from the list.

(Optional) You can't edit the rules of an existing security group, but you can copy them to a new group by choosing Copy to new. Then you can add rules as described in the next procedure.

To create a new security group:

Choose Create a new security group. The wizard automatically defines the launch-wizard-x security group.

(Optional) You can edit the name and description of the security group.

The wizard automatically defines an inbound rule to allow you to connect to your instance over SSH (port 22) for Linux or RDP (port 3389) for Windows.

Warning
This rule enables all IP addresses (0.0.0.0/0) to access your instance over the specified port. This is acceptable for this short exercise, but it's unsafe for production environments. You should authorize only a specific IP address or range of addresses to access your instance.
You can add rules to suit your needs. For example, if your instance is a web server, open ports 80 (HTTP) and 443 (HTTPS) to allow Internet traffic.

To add a rule, choose Add Rule, select the protocol to open to network traffic, and then specify the source. Choose My IP from the Source list to let the wizard add your computer's public IP address. However, if you are connecting through an ISP or from behind your firewall without a static IP address, you need to find out the range of IP addresses used by client computers.

On the Review Instance Launch page, check the details of your instance, and make any necessary changes by choosing the appropriate Edit link.

When you are ready, choose Launch.

In the Select an existing key pair or create a new key pair dialog box, you can choose an existing key pair, or create a new one. For example, choose Choose an existing key pair, then select the key pair you created when getting set up.

To launch your instance, select the acknowledgment check box, then choose Launch Instances.

Important
If you choose the Proceed without key pair option, you won't be able to connect to the instance unless you choose an AMI that is configured to allow users another way to log in.
(Optional) You can create a status check alarm for the instance (additional fees may apply). (If you're not sure, you can always add one later.) On the confirmation screen, choose Create status check alarms and follow the directions. For more information, see Creating and Editing Status Check Alarms.

If the instance state immediately goes to terminated instead of running, you can get information about why the instance didn't launch. For more information, see What To Do If An Instance Immediately Terminates.

Launching an Instance Using an Existing Instance as a Template

The Amazon EC2 console provides a Launch More Like This wizard option that enables you to use a current instance as a template for launching other instances. This option automatically populates the Amazon EC2 launch wizard with certain configuration details from the selected instance.

Note
The Launch More Like This wizard option does not clone your selected instance; it only replicates some configuration details. To create a copy of your instance, first create an AMI from it, then launch more instances from the AMI.
The following configuration details are copied from the selected instance into the launch wizard:

AMI ID
Instance type
Availability Zone, or the VPC and subnet in which the selected instance is located
Public IPv4 address. If the selected instance currently has a public IPv4 address, the new instance receives a public IPv4 address - regardless of the selected instance's default public IPv4 address setting. For more information about public IPv4 addresses, see Public IPv4 Addresses and External DNS Hostnames.
Placement group, if applicable
IAM role associated with the instance, if applicable
Shutdown behavior setting (stop or terminate)
Termination protection setting (true or false)
CloudWatch monitoring (enabled or disabled)
Amazon EBS-optimization setting (true or false)
Tenancy setting, if launching into a VPC (shared or dedicated)
Kernel ID and RAM disk ID, if applicable
User data, if specified
Tags associated with the instance, if applicable
Security groups associated with the instance
The following configuration details are not copied from your selected instance; instead, the wizard applies their default settings or behavior:

(VPC only) Number of network interfaces: The default is one network interface, which is the primary network interface (eth0).
Storage: The default storage configuration is determined by the AMI and the instance type.
To use your current instance as a template

On the Instances page, select the instance you want to use.

Choose Actions, and then Launch More Like This.

The launch wizard opens on the Review Instance Launch page. You can check the details of your instance, and make any necessary changes by clicking the appropriate Edit link.

When you are ready, choose Launch to select a key pair and launch your instance.

Launching a Linux Instance from a Backup

With an Amazon EBS-backed Linux instance, you can back up the root device volume of the instance by creating a snapshot. When you have a snapshot of the root device volume of an instance, you can terminate that instance and then later launch a new instance from the snapshot. This can be useful if you don't have the original AMI that you launched an instance from, but you need to be able to launch an instance using the same image.

Important
Although you can create a Windows AMI from a snapshot, you can't successfully launch an instance from that AMI.
Note that some Linux distributions, such as Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise Server (SLES), use the billing product code associated with an AMI to verify subscription status for package updates. Creating an AMI from an EBS snapshot does not maintain this billing code, and subsequent instances launched from such an AMI will not be able to connect to package update infrastructure. To retain the billing product codes, create the AMI from the instance not from a snapshot. For more information, see Creating an Amazon EBS-Backed Linux AMI or Creating an Instance Store-Backed Linux AMI.

Use the following procedure to create an AMI from the root volume of your instance using the console. If you prefer, you can use one of the following commands instead: register-image (AWS CLI) or Register-EC2Image (AWS Tools for Windows PowerShell). You specify the snapshot using the block device mapping.

To create an AMI from your root volume using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic Block Store, Snapshots.

Choose Create Snapshot.

For Volumes, start typing the name or ID of the root volume, and then select it from the list of options.

Choose the snapshot that you just created, and then choose Actions, Create Image.

In the Create Image from EBS Snapshot dialog box, provide the following information and then choose Create. If you're re-creating a parent instance, then choose the same options as the parent instance.

Architecture: Choose i386 for 32-bit or x86_64 for 64-bit.
Root device name: Enter the appropriate name for the root volume. For more information, see Device Naming on Linux Instances.
Virtualization type: Choose whether instances launched from this AMI use paravirtual (PV) or hardware virtual machine (HVM) virtualization. For more information, see Linux AMI Virtualization Types.
(PV virtualization type only) Kernel ID and RAM disk ID: Choose the AKI and ARI from the lists. If you choose the default AKI or don't choose an AKI, you'll be required to specify an AKI every time you launch an instance using this AMI. In addition, your instance may fail the health checks if the default AKI is incompatible with the instance.
(Optional) Block Device Mappings: Add volumes or expand the default size of the root volume for the AMI. For more information about resizing the file system on your instance for a larger volume, see Extending a Linux File System after Resizing the Volume.
In the navigation pane, choose AMIs.

Choose the AMI that you just created, and then choose Launch. Follow the wizard to launch your instance. For more information about how to configure each step in the wizard, see Launching an Instance.

Launching an AWS Marketplace Instance

You can subscribe to an AWS Marketplace product and launch an instance from the product's AMI using the Amazon EC2 launch wizard. For more information about paid AMIs, see Paid AMIs. To cancel your subscription after launch, you first have to terminate all instances running from it. For more information, see Managing Your AWS Marketplace Subscriptions.

To launch an instance from the AWS Marketplace using the launch wizard

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the Amazon EC2 dashboard, choose Launch Instance.

On the Choose an Amazon Machine Image (AMI) page, choose the AWS Marketplace category on the left. Find a suitable AMI by browsing the categories, or using the search functionality. Choose Select to choose your product.

A dialog displays an overview of the product you've selected. You can view the pricing information, as well as any other information that the vendor has provided. When you're ready, choose Continue.

Note
You are not charged for using the product until you have launched an instance with the AMI. Take note of the pricing for each supported instance type, as you will be prompted to select an instance type on the next page of the wizard. Additional taxes may also apply to the product.
On the Choose an Instance Type page, select the hardware configuration and size of the instance to launch. When you're done, choose Next: Configure Instance Details.

On the next pages of the wizard, you can configure your instance, add storage, and add tags. For more information about the different options you can configure, see Launching an Instance. Choose Next until you reach the Configure Security Group page.

The wizard creates a new security group according to the vendor's specifications for the product. The security group may include rules that allow all IPv4 addresses (0.0.0.0/0) access on SSH (port 22) on Linux or RDP (port 3389) on Windows. We recommend that you adjust these rules to allow only a specific address or range of addresses to access your instance over those ports.

When you are ready, choose Review and Launch.

On the Review Instance Launch page, check the details of the AMI from which you're about to launch the instance, as well as the other configuration details you set up in the wizard. When you're ready, choose Launch to select or create a key pair, and launch your instance.

Depending on the product you've subscribed to, the instance may take a few minutes or more to launch. You are first subscribed to the product before your instance can launch. If there are any problems with your credit card details, you will be asked to update your account details. When the launch confirmation page displays, choose View Instances to go to the Instances page.

Note
You are charged the subscription price as long as your instance is running, even if it is idle. If your instance is stopped, you may still be charged for storage.
When your instance is in the running state, you can connect to it. To do this, select your instance in the list and choose Connect. Follow the instructions in the dialog. For more information about connecting to your instance, see Connect to Your Linux Instance.

Important
Check the vendor's usage instructions carefully, as you may need to use a specific user name to log in to the instance. For more information about accessing your subscription details, see Managing Your AWS Marketplace Subscriptions.
Launching an AWS Marketplace AMI Instance Using the API and CLI

To launch instances from AWS Marketplace products using the API or command line tools, first ensure that you are subscribed to the product. You can then launch an instance with the product's AMI ID using the following methods:

Method	Documentation
AWS CLI
Use the run-instances command, or see the following topic for more information: Launching an Instance.
AWS Tools for Windows PowerShell
Use the New-EC2Instance command, or see the following topic for more information: Launch an Amazon EC2 Instance Using Windows PowerShell
Query API	Use the RunInstances request.

Connect to Your Linux Instance

Learn how to connect to the Linux instances that you launched and transfer files between your local computer and your instance.

If you need to connect to a Windows instance, see Connecting to Your Windows Instance in the Amazon EC2 User Guide for Windows Instances.

Your Computer	Topic
Linux
Connecting to Your Linux Instance Using SSH
Windows
Connecting to Your Linux Instance from Windows Using PuTTY
All
Connecting to Your Linux Instance Using MindTerm
After you connect to your instance, you can try one of our tutorials, such as Tutorial: Installing a LAMP Web Server on Amazon Linux or Tutorial: Hosting a WordPress Blog with Amazon Linux.

Connecting to Your Linux Instance Using SSH

After you launch your instance, you can connect to it and use it the way that you'd use a computer sitting in front of you.

Note
After you launch an instance, it can take a few minutes for the instance to be ready so that you can connect to it. Check that your instance has passed its status checks - you can view this information in the Status Checks column on the Instances page.
The following instructions explain how to connect to your instance using an SSH client. If you receive an error while attempting to connect to your instance, see Troubleshooting Connecting to Your Instance.

Prerequisites

Before you connect to your Linux instance, complete the following prerequisites:

Install an SSH client
Your Linux computer most likely includes an SSH client by default. You can check for an SSH client by typing ssh at the command line. If your computer doesn't recognize the command, the OpenSSH project provides a free implementation of the full suite of SSH tools. For more information, see http://www.openssh.com.
Install the AWS CLI Tools
(Optional) If you're using a public AMI from a third party, you can use the command line tools to verify the fingerprint. For more information about installing the AWS CLI, see Getting Set Up in the AWS Command Line Interface User Guide.
Get the ID of the instance
You can get the ID of your instance using the Amazon EC2 console (from the Instance ID column). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command.
Get the public DNS name of the instance
You can get the public DNS for your instance using the Amazon EC2 console (check the Public DNS (IPv4) column; if this column is hidden, choose the Show/Hide icon and select Public DNS (IPv4)). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command.
(IPv6 only) Get the IPv6 address of the instance
If you've assigned an IPv6 address to your instance, you can optionally connect to the instance using its IPv6 address instead of a public IPv4 address or public IPv4 DNS hostname. Your local computer must have an IPv6 address and must be configured to use IPv6. You can get the IPv6 address of your instance using the Amazon EC2 console (check the IPv6 IPs field). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command. For more information about IPv6, see IPv6 Addresses.
Locate the private key
Get the fully qualified path to the location on your computer of the .pem file for the key pair that you specified when you launched the instance.
Enable inbound SSH traffic from your IP address to your instance
Ensure that the security group associated with your instance allows incoming SSH traffic from your IP address. The default security group does not allow incoming SSH traffic by default. For more information, see Authorizing Inbound Traffic for Your Linux Instances.
Connecting to Your Linux Instance

Use the following procedure to connect to your Linux instance using an SSH client. If you receive an error while attempting to connect to your instance, see Troubleshooting Connecting to Your Instance.

To connect to your instance using SSH

(Optional) You can verify the RSA key fingerprint on your running instance by using one of the following commands on your local system (not on the instance). This is useful if you've launched your instance from a public AMI from a third party. Locate the SSH HOST KEY FINGERPRINTS section, and note the RSA fingerprint (for example, 1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f) and compare it to the fingerprint of the instance.

get-console-output (AWS CLI)
Copy
aws ec2 get-console-output --instance-id instance_id
Ensure that the instance is in the running state, not the pending state. The SSH HOST KEY FINGERPRINTS section is only available after the first boot of the instance.

In a command-line shell, change directories to the location of the private key file that you created when you launched the instance.

Use the chmod command to make sure that your private key file isn't publicly viewable. For example, if the name of your private key file is my-key-pair.pem, use the following command:

Copy
chmod 400 /path/my-key-pair.pem
Use the ssh command to connect to the instance. You specify the private key (.pem) file and user_name@public_dns_name. For Amazon Linux, the user name is ec2-user. For RHEL, the user name is ec2-user or root. For Ubuntu, the user name is ubuntu or root. For Centos, the user name is centos. For Fedora, the user name is ec2-user. For SUSE, the user name is ec2-user or root. Otherwise, if ec2-user and root don't work, check with your AMI provider.

Copy
ssh -i /path/my-key-pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com
You see a response like the following.

The authenticity of host 'ec2-198-51-100-1.compute-1.amazonaws.com (10.254.142.33)'
can't be established.
RSA key fingerprint is 1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f.
Are you sure you want to continue connecting (yes/no)?
(IPv6 only) Alternatively, you can connect to the instance using its IPv6 address. Specify the ssh command with the path to the private key (.pem) file and the appropriate user name. For Amazon Linux, the user name is ec2-user. For RHEL, the user name is ec2-user or root. For Ubuntu, the user name is ubuntu or root. For Centos, the user name is centos. For Fedora, the user name is ec2-user. For SUSE, the user name is ec2-user or root. Otherwise, if ec2-user and root don't work, check with your AMI provider.

Copy
ssh -i /path/my-key-pair.pem ec2-user@2001:db8:1234:1a00:9691:9503:25ad:1761
(Optional) Verify that the fingerprint in the security alert matches the fingerprint that you obtained in step 1. If these fingerprints don't match, someone might be attempting a "man-in-the-middle" attack. If they match, continue to the next step.

Enter yes.

You see a response like the following.

Warning: Permanently added 'ec2-198-51-100-1.compute-1.amazonaws.com' (RSA) 
to the list of known hosts.
Transferring Files to Linux Instances from Linux Using SCP

One way to transfer files between your local computer and a Linux instance is to use Secure Copy (SCP). This section describes how to transfer files with SCP. The procedure is very similar to the procedure for connecting to an instance with SSH.

Prerequisites

Install an SCP client
Most Linux, Unix, and Apple computers include an SCP client by default. If yours doesn't, the OpenSSH project provides a free implementation of the full suite of SSH tools, including an SCP client. For more information, go to http://www.openssh.org.
Get the ID of the instance
You can get the ID of your instance using the Amazon EC2 console (from the Instance ID column). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command.
Get the public DNS name of the instance
You can get the public DNS for your instance using the Amazon EC2 console (check the Public DNS (IPv4) column; if this column is hidden, choose the Show/Hide icon and select Public DNS (IPv4)). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command.
(IPv6 only) Get the IPv6 address of the instance
If you've assigned an IPv6 address to your instance, you can optionally connect to the instance using its IPv6 address instead of a public IPv4 address or public IPv4 DNS hostname. Your local computer must have an IPv6 address and must be configured to use IPv6. You can get the IPv6 address of your instance using the Amazon EC2 console (check the IPv6 IPs field). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command. For more information about IPv6, see IPv6 Addresses.
Locate the private key
Get the fully qualified path to the location on your computer of the .pem file for the key pair that you specified when you launched the instance.
Enable inbound SSH traffic from your IP address to your instance
Ensure that the security group associated with your instance allows incoming SSH traffic from your IP address. The default security group does not allow incoming SSH traffic by default. For more information, see Authorizing Inbound Traffic for Your Linux Instances.
The following procedure steps you through using SCP to transfer a file. If you've already connected to the instance with SSH and have verified its fingerprints, you can start with the step that contains the SCP command (step 4).

To use SCP to transfer a file

(Optional) You can verify the RSA key fingerprint on your instance by using one of the following commands on your local system (not on the instance). This is useful if you've launched your instance from a public AMI from a third party. Locate the SSH HOST KEY FINGERPRINTS section, and note the RSA fingerprint (for example, 1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f) and compare it to the fingerprint of the instance.

get-console-output (AWS CLI)
Copy
aws ec2 get-console-output --instance-id instance_id
The SSH HOST KEY FINGERPRINTS section is only available after the first boot of the instance.

In a command shell, change directories to the location of the private key file that you specified when you launched the instance.

Use the chmod command to make sure that your private key file isn't publicly viewable. For example, if the name of your private key file is my-key-pair.pem, use the following command:

Copy
chmod 400 /path/my-key-pair.pem
Transfer a file to your instance using the instance's public DNS name. For example, if the name of the private key file is my-key-pair, the file to transfer is SampleFile.txt, and the public DNS name of the instance is ec2-198-51-100-1.compute-1.amazonaws.com, use the following command to copy the file to the ec2-user home directory.

Copy
scp -i /path/my-key-pair.pem /path/SampleFile.txt ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com:~
Tip
For Amazon Linux, the user name is ec2-user. For RHEL, the user name is ec2-user or root. For Ubuntu, the user name is ubuntu or root. For Centos, the user name is centos. For Fedora, the user name is ec2-user. For SUSE, the user name is ec2-user or root. Otherwise, if ec2-user and root don't work, check with your AMI provider.
You see a response like the following.

The authenticity of host 'ec2-198-51-100-1.compute-1.amazonaws.com (10.254.142.33)'
can't be established.
RSA key fingerprint is 1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f.
Are you sure you want to continue connecting (yes/no)?
(IPv6 only) Alternatively, you can transfer a file using the IPv6 address for the instance. The IPv6 address must be enclosed in square brackets ([]), which must be escaped (\).

Copy
scp -i /path/my-key-pair.pem /path/SampleFile.txt ec2-user@\[2001:db8:1234:1a00:9691:9503:25ad:1761\]:~
(Optional) Verify that the fingerprint in the security alert matches the fingerprint that you obtained in step 1. If these fingerprints don't match, someone might be attempting a "man-in-the-middle" attack. If they match, continue to the next step.

Enter yes.

You see a response like the following.

Warning: Permanently added 'ec2-198-51-100-1.compute-1.amazonaws.com' (RSA) 
to the list of known hosts.
Sending file modes: C0644 20 SampleFile.txt
Sink: C0644 20 SampleFile.txt
SampleFile.txt                                100%   20     0.0KB/s   00:00
If you receive a "bash: scp: command not found" error, you must first install scp on your Linux instance. For some operating systems, this is located in the openssh-clients package. For Amazon Linux variants, such as the Amazon ECS-optimized AMI, use the following command to install scp.

Copy
[ec2-user ~]$ sudo yum install -y openssh-clients
To transfer files in the other direction (from your Amazon EC2 instance to your local computer), simply reverse the order of the host parameters. For example, to transfer the SampleFile.txt file from your EC2 instance back to the home directory on your local computer as SampleFile2.txt, use the following command on your local computer.

Copy
scp -i /path/my-key-pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com:~/SampleFile.txt ~/SampleFile2.txt
(IPv6 only) Alternatively, you can transfer files in the other direction using the instance's IPv6 address.

Copy
scp -i /path/my-key-pair.pem ec2-user@\[2001:db8:1234:1a00:9691:9503:25ad:1761\]:~/SampleFile.txt ~/SampleFile2.txt

Connecting to Your Linux Instance from Windows Using PuTTY

After you launch your instance, you can connect to it and use it the way that you'd use a computer sitting in front of you.

Note
After you launch an instance, it can take a few minutes for the instance to be ready so that you can connect to it. Check that your instance has passed its status checks - you can view this information in the Status Checks column on the Instances page.
The following instructions explain how to connect to your instance using PuTTY, a free SSH client for Windows. If you receive an error while attempting to connect to your instance, see Troubleshooting Connecting to Your Instance.

Prerequisites

Before you connect to your Linux instance using PuTTY, complete the following prerequisites:

Install PuTTY
Download and install PuTTY from the PuTTY download page. If you already have an older version of PuTTY installed, we recommend that you download the latest version. Be sure to install the entire suite.
Get the ID of the instance
You can get the ID of your instance using the Amazon EC2 console (from the Instance ID column). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command.
Get the public DNS name of the instance
You can get the public DNS for your instance using the Amazon EC2 console (check the Public DNS (IPv4) column; if this column is hidden, choose the Show/Hide icon and select Public DNS (IPv4)). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command.
(IPv6 only) Get the IPv6 address of the instance
If you've assigned an IPv6 address to your instance, you can optionally connect to the instance using its IPv6 address instead of a public IPv4 address or public IPv4 DNS hostname. Your local computer must have an IPv6 address and must be configured to use IPv6. You can get the IPv6 address of your instance using the Amazon EC2 console (check the IPv6 IPs field). If you prefer, you can use the describe-instances (AWS CLI) or Get-EC2Instance (AWS Tools for Windows PowerShell) command. For more information about IPv6, see IPv6 Addresses.
Locate the private key
Get the fully qualified path to the location on your computer of the .pem file for the key pair that you specified when you launched the instance.
Enable inbound SSH traffic from your IP address to your instance
Ensure that the security group associated with your instance allows incoming SSH traffic from your IP address. The default security group does not allow incoming SSH traffic by default. For more information, see Authorizing Inbound Traffic for Your Linux Instances.
Converting Your Private Key Using PuTTYgen

PuTTY does not natively support the private key format (.pem) generated by Amazon EC2. PuTTY has a tool named PuTTYgen, which can convert keys to the required PuTTY format (.ppk). You must convert your private key into this format (.ppk) before attempting to connect to your instance using PuTTY.

To convert your private key

Start PuTTYgen (for example, from the Start menu, choose All Programs > PuTTY > PuTTYgen).

Under Type of key to generate, choose RSA.


							RSA key in PuTTYgen
						
If you're using an older version of PuTTYgen, choose SSH-2 RSA.

Choose Load. By default, PuTTYgen displays only files with the extension .ppk. To locate your .pem file, select the option to display files of all types.


							Select all file types
						
Select your .pem file for the key pair that you specified when you launch your instance, and then choose Open. Choose OK to dismiss the confirmation dialog box.

Choose Save private key to save the key in the format that PuTTY can use. PuTTYgen displays a warning about saving the key without a passphrase. Choose Yes.

Note
A passphrase on a private key is an extra layer of protection, so even if your private key is discovered, it can't be used without the passphrase. The downside to using a passphrase is that it makes automation harder because human intervention is needed to log on to an instance, or copy files to an instance.
Specify the same name for the key that you used for the key pair (for example, my-key-pair). PuTTY automatically adds the .ppk file extension.

Your private key is now in the correct format for use with PuTTY. You can now connect to your instance using PuTTY's SSH client.

Starting a PuTTY Session

Use the following procedure to connect to your Linux instance using PuTTY. You need the .ppk file that you created for your private key. If you receive an error while attempting to connect to your instance, see Troubleshooting Connecting to Your Instance.

To start a PuTTY session

(Optional) You can verify the RSA key fingerprint on your instance using the get-console-output (AWS CLI) command on your local system (not on the instance). This is useful if you've launched your instance from a public AMI from a third party. Locate the SSH HOST KEY FINGERPRINTS section, and note the RSA fingerprint (for example, 1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f) and compare it to the fingerprint of the instance.

Copy
aws ec2 get-console-output --instance-id instance_id
Here is an example of what you should look for:

-----BEGIN SSH HOST KEY FINGERPRINTS-----
... 1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f ...
-----END SSH HOST KEY FINGERPRINTS-----
Note that the SSH HOST KEY FINGERPRINTS section is only available after the first boot of the instance.

Start PuTTY (from the Start menu, choose All Programs > PuTTY > PuTTY).

In the Category pane, select Session and complete the following fields:

In the Host Name box, enter user_name@public_dns_name. Be sure to specify the appropriate user name for your AMI. For example:

For an Amazon Linux AMI, the user name is ec2-user.
For a RHEL AMI, the user name is ec2-user or root.
For an Ubuntu AMI, the user name is ubuntu or root.
For a Centos AMI, the user name is centos.
For a Fedora AMI, the user name is ec2-user.
For SUSE, the user name is ec2-user or root.
Otherwise, if ec2-user and root don't work, check with the AMI provider.
(IPv6 only) To connect using your instance's IPv6 address, enter user_name@ipv6_address. Be sure to specify the appropriate user name for your AMI. For example:

For an Amazon Linux AMI, the user name is ec2-user.
For a RHEL AMI, the user name is ec2-user or root.
For an Ubuntu AMI, the user name is ubuntu or root.
For a Centos AMI, the user name is centos.
For a Fedora AMI, the user name is ec2-user.
For SUSE, the user name is ec2-user or root.
Otherwise, if ec2-user and root don't work, check with the AMI provider.
Under Connection type, select SSH.

Ensure that Port is 22.


							PuTTY configuration - Session
						
In the Category pane, expand Connection, expand SSH, and then select Auth. Complete the following:

Choose Browse.

Select the .ppk file that you generated for your key pair, and then choose Open.

(Optional) If you plan to start this session again later, you can save the session information for future use. Select Session in the Category tree, enter a name for the session in Saved Sessions, and then choose Save.

Choose Open to start the PuTTY session.


							PuTTY configuration - Auth
						
If this is the first time you have connected to this instance, PuTTY displays a security alert dialog box that asks whether you trust the host you are connecting to.

(Optional) Verify that the fingerprint in the security alert dialog box matches the fingerprint that you previously obtained in step 1. If these fingerprints don't match, someone might be attempting a "man-in-the-middle" attack. If they match, continue to the next step.

Choose Yes. A window opens and you are connected to your instance.

Note
If you specified a passphrase when you converted your private key to PuTTY's format, you must provide that passphrase when you log in to the instance.
If you receive an error while attempting to connect to your instance, see Troubleshooting Connecting to Your Instance.

Transferring Files to Your Linux Instance Using the PuTTY Secure Copy Client

The PuTTY Secure Copy client (PSCP) is a command-line tool that you can use to transfer files between your Windows computer and your Linux instance. If you prefer a graphical user interface (GUI), you can use an open source GUI tool named WinSCP. For more information, see Transferring Files to Your Linux Instance Using WinSCP.

To use PSCP, you need the private key you generated in Converting Your Private Key Using PuTTYgen. You also need the public DNS address of your Linux instance.

The following example transfers the file Sample_file.txt from the C:\ drive on a Windows computer to the ec2-user home directory on a Amazon Linux instance:

Copy
pscp -i C:\path\my-key-pair.ppk C:\path\Sample_file.txt ec2-user@public_dns:/home/ec2-user/Sample_file.txt
(IPv6 only) The following example transfers the file Sample_file.txt using the instance's IPv6 address. The IPv6 address must be enclosed in square brackets ([]).

Copy
pscp -i C:\path\my-key-pair.ppk C:\path\Sample_file.txt ec2-user@[ipv6-address]:/home/ec2-user/Sample_file.txt
Transferring Files to Your Linux Instance Using WinSCP

WinSCP is a GUI-based file manager for Windows that allows you to upload and transfer files to a remote computer using the SFTP, SCP, FTP, and FTPS protocols. WinSCP allows you to drag and drop files from your Windows machine to your Linux instance or synchronize entire directory structures between the two systems.

To use WinSCP, you need the private key you generated in Converting Your Private Key Using PuTTYgen. You also need the public DNS address of your Linux instance.

Download and install WinSCP from http://winscp.net/eng/download.php. For most users, the default installation options are OK.

Start WinSCP.

At the WinSCP login screen, for Host name, enter the public DNS hostname or public IPv4 address for your instance.

(IPv6 only) To log in using your instance's IPv6 address, enter the IPv6 address for your instance.

For User name, enter the default user name for your AMI. For Amazon Linux AMIs, the user name is ec2-user. For Red Hat AMIs, the user name is root, and for Ubuntu AMIs, the user name is ubuntu.

Specify the private key for your instance. For Private key, enter the path to your private key, or choose the "..." button to browse for the file. For newer versions of WinSCP, you need to choose Advanced to open the advanced site settings and then under SSH, choose Authentication to find the Private key file setting.

Here is a screenshot from WinSCP version 5.9.4:


							WinSCP Advanced screen
						
WinSCP requires a PuTTY private key file (.ppk). You can convert a .pem security key file to the .ppk format using PuTTYgen. For more information, see Converting Your Private Key Using PuTTYgen.

(Optional) In the left panel, choose Directories, and then, for Remote directory, enter the path for the directory you want to add files to. For newer versions of WinSCP, you need to choose Advanced to open the advanced site settings and then under Environment, choose Directories to find the Remote directory setting.

Choose Login to connect, and choose Yes to add the host fingerprint to the host cache.


							WinSCP screen
						
After the connection is established, in the connection window your Linux instance is on the right and your local machine is on the left. You can drag and drop files directly into the remote file system from your local machine. For more information on WinSCP, see the project documentation at http://winscp.net/eng/docs/start.

If you receive a "Cannot execute SCP to start transfer" error, you must first install scp on your Linux instance. For some operating systems, this is located in the openssh-clients package. For Amazon Linux variants, such as the Amazon ECS-optimized AMI, use the following command to install scp.

Copy
[ec2-user ~]$ sudo yum install -y openssh-clients

Connecting to Your Linux Instance Using MindTerm

After you launch your instance, you can connect to it and use it the way that you'd use a computer sitting in front of you.

Note
After you launch an instance, it can take a few minutes for the instance to be ready so that you can connect to it. Check that your instance has passed its status checks - you can view this information in the Status Checks column on the Instances page.
The following instructions explain how to connect to your instance using MindTerm through the Amazon EC2 console. If you receive an error while attempting to connect to your instance, see Troubleshooting Connecting to Your Instance.

Important
The Chrome browser does not support the NPAPI plugin, and therefore cannot run the MindTerm client. For more information, go to the Chromium NPAPI deprecation article. You can use Firefox, Safari, or Internet Explorer 9 or higher instead.
Prerequisites

Install Java
Your Linux computer most likely includes Java. If not, see How do I enable Java in my web browser? On a Windows or Mac client, you must run your browser using administrator credentials. For Linux, additional steps may be required if you are not logged in as root.
Enable Java in your browser
For instructions, see https://java.com/en/download/help/enable_browser.xml.
Locate the private key
Get the fully qualified path to the location on your computer of the .pem file for the key pair that you specified when you launched the instance.
Enable inbound SSH traffic from your IP address to your instance
Ensure that the security group associated with your instance allows incoming SSH traffic from your IP address. The default security group does not allow incoming SSH traffic by default. For more information, see Authorizing Inbound Traffic for Your Linux Instances.
Starting MindTerm

To connect to your instance using a web browser with MindTerm

In the Amazon EC2 console, choose Instances in the navigation pane.

Select the instance, and then choose Connect.

Choose A Java SSH client directly from my browser (Java required).

Amazon EC2 automatically detects the public DNS name of your instance and then populates Public DNS for you. It also detects the name of the key pair that you specified when you launched the instance. Complete the following, and then choose Launch SSH Client.

In User name, enter the user name to log in to your instance.

Tip
For Amazon Linux, the user name is ec2-user. For RHEL, the user name is ec2-user or root. For Ubuntu, the user name is ubuntu or root. For Centos, the user name is centos. For Fedora, the user name is ec2-user. For SUSE, the user name is ec2-user or root. Otherwise, if ec2-user and root don't work, check with your AMI provider.
In Private key path, enter the fully qualified path to your private key (.pem) file, including the key pair name; for example:

C:\KeyPairs\my-key-pair.pem

(Optional) Choose Store in browser cache to store the location of the private key in your browser cache. This enables Amazon EC2 to detect the location of the private key in subsequent browser sessions, until you clear your browser's cache.

If necessary, choose Yes to trust the certificate, and choose Run to run the MindTerm client.

If this is your first time running MindTerm, a series of dialog boxes asks you to accept the license agreement, to confirm setup for your home directory, and to confirm setup of the known hosts directory. Confirm these settings.

A dialog prompts you to add the host to your set of known hosts. If you do not want to store the host key information on your local computer, choose No.

A window opens and you are connected to your instance.

If you chose No in the previous step, you see the following message, which is expected:

Verification of server key disabled in this session.

Stop and Start Your Instance

You can stop and restart your instance if it has an Amazon EBS volume as its root device. The instance retains its instance ID, but can change as described in the Overview section.

When you stop an instance, we shut it down. We don't charge hourly usage for a stopped instance, or data transfer fees, but we do charge for the storage for any Amazon EBS volumes. Each time you start a stopped instance we charge a full instance hour, even if you make this transition multiple times within a single hour.

While the instance is stopped, you can treat its root volume like any other volume, and modify it (for example, repair file system problems or update software). You just detach the volume from the stopped instance, attach it to a running instance, make your changes, detach it from the running instance, and then reattach it to the stopped instance. Make sure that you reattach it using the storage device name that's specified as the root device in the block device mapping for the instance.

If you decide that you no longer need an instance, you can terminate it. As soon as the state of an instance changes to shutting-down or terminated, we stop charging for that instance. For more information, see Terminate Your Instance.

Contents

Overview
Stopping and Starting Your Instances
Modifying a Stopped Instance
Troubleshooting
Overview

You can only stop an Amazon EBS-backed instance. To verify the root device type of your instance, describe the instance and check whether the device type of its root volume is ebs (Amazon EBS-backed instance) or instance store (instance store-backed instance). For more information, see Determining the Root Device Type of Your AMI.

When you stop a running instance, the following happens:

The instance performs a normal shutdown and stops running; its status changes to stopping and then stopped.
Any Amazon EBS volumes remain attached to the instance, and their data persists.
Any data stored in the RAM of the host computer or the instance store volumes of the host computer is gone.
In most cases, the instance is migrated to a new underlying host computer when it's started.
EC2-Classic: We release the public and private IPv4 addresses for the instance when you stop the instance, and assign new ones when you restart it.
EC2-VPC: The instance retains its private IPv4 addresses and any IPv6 addresses when stopped and restarted. We release the public IPv4 address and assign a new one when you restart it.
EC2-Classic: We disassociate any Elastic IP address that's associated with the instance. You're charged for Elastic IP addresses that aren't associated with an instance. When you restart the instance, you must associate the Elastic IP address with the instance; we don't do this automatically.
EC2-VPC: The instance retains its associated Elastic IP addresses. You're charged for any Elastic IP addresses associated with a stopped instance.
When you stop and start a Windows instance, the EC2Config service performs tasks on the instance such as changing the drive letters for any attached Amazon EBS volumes. For more information about these defaults and how you can change them, see Configuring a Windows Instance Using the EC2Config Service in the Amazon EC2 User Guide for Windows Instances.
If you've registered the instance with a load balancer, it's likely that the load balancer won't be able to route traffic to your instance after you've stopped and restarted it. You must de-register the instance from the load balancer after stopping the instance, and then re-register after starting the instance. For more information, see Register or Deregister EC2 Instances for Your Classic Load Balancer in the Classic Load Balancer Guide.
If your instance is in an Auto Scaling group, the Auto Scaling service marks the stopped instance as unhealthy, and may terminate it and launch a replacement instance. For more information, see Health Checks for Auto Scaling Instances in the Auto Scaling User Guide.
When you stop a ClassicLink instance, it's unlinked from the VPC to which it was linked. You must link the instance to the VPC again after restarting it. For more information about ClassicLink, see ClassicLink.
For more information, see Differences Between Reboot, Stop, and Terminate.

You can modify the following attributes of an instance only when it is stopped:

Instance type
User data
Kernel
RAM disk
If you try to modify these attributes while the instance is running, Amazon EC2 returns the IncorrectInstanceState error.

Stopping and Starting Your Instances

You can start and stop your Amazon EBS-backed instance using the console or the command line.

By default, when you initiate a shutdown from an Amazon EBS-backed instance (using the shutdown, halt, or poweroff command), the instance stops. You can change this behavior so that it terminates instead. For more information, see Changing the Instance Initiated Shutdown Behavior.

To stop and start an Amazon EBS-backed instance using the console

In the navigation pane, choose Instances, and select the instance.

[EC2-Classic] If the instance has an associated Elastic IP address, write down the Elastic IP address and the instance ID shown in the details pane.

Choose Actions, select Instance State, and then choose Stop. If Stop is disabled, either the instance is already stopped or its root device is an instance store volume.

Warning
When you stop an instance, the data on any instance store volumes is erased. Therefore, if you have any data on instance store volumes that you want to keep, be sure to back it up to persistent storage.
In the confirmation dialog box, choose Yes, Stop. It can take a few minutes for the instance to stop.

[EC2-Classic] When the instance state becomes stopped, the Elastic IP, Public DNS (IPv4), Private DNS, and Private IPs fields in the details pane are blank to indicate that the old values are no longer associated with the instance.

While your instance is stopped, you can modify certain instance attributes. For more information, see Modifying a Stopped Instance.

To restart the stopped instance, select the instance, choose Actions, select Instance State, and then choose Start.

In the confirmation dialog box, choose Yes, Start. It can take a few minutes for the instance to enter the running state.

[EC2-Classic] When the instance state becomes running, the Public DNS (IPv4), Private DNS, and Private IPs fields in the details pane contain the new values that we assigned to the instance.

[EC2-Classic] If your instance had an associated Elastic IP address, you must reassociate it as follows:

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address that you wrote down before you stopped the instance.

Choose Actions, and then select Associate address.

Select the instance ID that you wrote down before you stopped the instance, and then choose Associate.

To stop and start an Amazon EBS-backed instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

stop-instances and start-instances (AWS CLI)
Stop-EC2Instance and Start-EC2Instance (AWS Tools for Windows PowerShell)
Modifying a Stopped Instance

You can change the instance type, user data, and EBS-optimization attributes of a stopped instance using the AWS Management Console or the command line interface. You can't use the AWS Management Console to modify the DeleteOnTermination, kernel, or RAM disk attributes.

To modify an instance attribute

To change the instance type, see Resizing Your Instance.
To change the user data for your instance, see Configuring Instances with User Data.
To enable or disable EBS–optimization for your instance, see Modifying EBS–Optimization.
To change the DeleteOnTermination attribute of the root volume for your instance, see Updating the Block Device Mapping of a Running Instance.
To modify an instance attribute using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-instance-attribute (AWS CLI)
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Troubleshooting

If you have stopped your Amazon EBS-backed instance and it appears "stuck" in the stopping state, you can forcibly stop it. For more information, see Troubleshooting Stopping Your Instance.

Reboot Your Instance

An instance reboot is equivalent to an operating system reboot. In most cases, it takes only a few minutes to reboot your instance. When you reboot an instance, it remains on the same physical host, so your instance keeps its public DNS name (IPv4), private IPv4 address, IPv6 address (if applicable), and any data on its instance store volumes.

Rebooting an instance doesn't start a new instance billing hour, unlike stopping and restarting your instance.

We might schedule your instance for a reboot for necessary maintenance, such as to apply updates that require a reboot. No action is required on your part; we recommend that you wait for the reboot to occur within its scheduled window. For more information, see Scheduled Events for Your Instances.

We recommend that you use Amazon EC2 to reboot your instance instead of running the operating system reboot command from your instance. If you use Amazon EC2 to reboot your instance, we perform a hard reboot if the instance does not cleanly shut down within four minutes. If you use AWS CloudTrail, then using Amazon EC2 to reboot your instance also creates an API record of when your instance was rebooted.

To reboot an instance using the console

Open the Amazon EC2 console.

In the navigation pane, choose Instances.

Select the instance, choose Actions, select Instance State, and then select Reboot.

Choose Yes, Reboot when prompted for confirmation.

To reboot an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

reboot-instances (AWS CLI)
Restart-EC2Instance (AWS Tools for Windows PowerShell)

Instance Retirement

An instance is scheduled to be retired when AWS detects irreparable failure of the underlying hardware hosting the instance. When an instance reaches its scheduled retirement date, it is stopped or terminated by AWS. If your instance root device is an Amazon EBS volume, the instance is stopped, and you can start it again at any time. Starting the stopped instance migrates it to new hardware. If your instance root device is an instance store volume, the instance is terminated, and cannot be used again.

Topics

Identifying Instances Scheduled for Retirement
Working with Instances Scheduled for Retirement
For more information about types of instance events, see Scheduled Events for Your Instances.

Identifying Instances Scheduled for Retirement

If your instance is scheduled for retirement, you'll receive an email prior to the event with the instance ID and retirement date. This email is sent to the address that's associated with your account; the same email address that you use to log in to the AWS Management Console. If you use an email account that you do not check regularly, then you can use the Amazon EC2 console or the command line to determine if any of your instances are scheduled for retirement. To update the contact information for your account, go to the Account Settings page.

To identify instances scheduled for retirement using the console

Open the Amazon EC2 console.

In the navigation pane, choose EC2 Dashboard. Under Scheduled Events, you can see the events associated with your Amazon EC2 instances and volumes, organized by region.


                        Scheduled events
                    
If you have an instance with a scheduled event listed, select its link below the region name to go to the Events page.

The Events page lists all resources with events associated with them. To view instances that are scheduled for retirement, select Instance resources from the first filter list, and then Instance stop or retirement from the second filter list.

If the filter results show that an instance is scheduled for retirement, select it, and note the date and time in the Start time field in the details pane. This is your instance retirement date.

To identify instances scheduled for retirement using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-instance-status (AWS CLI)
Get-EC2InstanceStatus (AWS Tools for Windows PowerShell)
Working with Instances Scheduled for Retirement

There are a number of actions available to you when your instance is scheduled for retirement. The action you take depends on whether your instance root device is an Amazon EBS volume, or an instance store volume. If you do not know what your instance root device type is, you can find out using the Amazon EC2 console or the command line.

Determining Your Instance Root Device Type

To determine your instance root device type using the console

In the navigation pane, select Events. Use the filter lists to identify retiring instances, as demonstrated in the procedure above, Identifying instances scheduled for retirement.

In the Resource Id column, select the instance ID to go to the Instances page.

Select the instance and locate the Root device type field in the Description tab. If the value is ebs, then your instance is EBS-backed. If the value is instance-store, then your instance is instance store-backed.

To determine your instance root device type using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-instances (AWS CLI)
Get-EC2Instance (AWS Tools for Windows PowerShell)
Managing Instances Scheduled for Retirement

You can perform one of the actions listed below in order to preserve the data on your retiring instance. It's important that you take this action before the instance retirement date, to prevent unforeseen downtime and data loss.

Warning
If your instance store-backed instance passes its retirement date, it's terminated and you cannot recover the instance or any data that was stored on it. Regardless of the root device of your instance, the data on instance store volumes is lost when the instance is retired, even if they are attached to an EBS-backed instance.
Instance Root Device Type	Action
EBS	Wait for the scheduled retirement date - when the instance is stopped - or stop the instance yourself before the retirement date. You can start the instance again at any time. For more information about stopping and starting your instance, and what to expect when your instance is stopped, such as the effect on public, private and Elastic IP addresses associated with your instance, see Stop and Start Your Instance.
EBS	Create an EBS-backed AMI from your instance, and launch a replacement instance. For more information, see Creating an Amazon EBS-Backed Linux AMI.
Instance store	Create an instance store-backed AMI from your instance using the AMI tools, and launch a replacement instance. For more information, see Creating an Instance Store-Backed Linux AMI.
Instance store	Convert your instance to an EBS-backed instance by transferring your data to an EBS volume, taking a snapshot of the volume, and then creating an AMI from the snapshot. You can launch a replacement instance from your new AMI. For more information, see Converting your Instance Store-Backed AMI to an Amazon EBS-Backed AMI.

Terminate Your Instance

You can delete your instance when you no longer need it. This is referred to as terminating your instance. As soon as the state of an instance changes to shutting-down or terminated, you stop incurring charges for that instance.

You can't connect to or restart an instance after you've terminated it. However, you can launch additional instances using the same AMI. If you'd rather stop and restart your instance, see Stop and Start Your Instance. For more information, see Differences Between Reboot, Stop, and Terminate.

Contents

Instance Termination
Terminating an Instance
Enabling Termination Protection for an Instance
Changing the Instance Initiated Shutdown Behavior
Preserving Amazon EBS Volumes on Instance Termination
Troubleshooting
Instance Termination

After you terminate an instance, it remains visible in the console for a short while, and then the entry is automatically deleted. You cannot delete the terminated instance entry yourself. After an instance is terminated, resources such as tags and volumes are gradually disassociated from the instance, therefore may no longer be visible on the terminated instance after a short while.

When an instance terminates, the data on any instance store volumes associated with that instance is deleted.

By default, Amazon EBS root device volumes are automatically deleted when the instance terminates. However, by default, any additional EBS volumes that you attach at launch, or any EBS volumes that you attach to an existing instance persist even after the instance terminates. This behavior is controlled by the volume's DeleteOnTermination attribute, which you can modify. For more information, see Preserving Amazon EBS Volumes on Instance Termination.

You can prevent an instance from being terminated accidentally by someone using the AWS Management Console, the CLI, and the API. This feature is available for both Amazon EC2 instance store-backed and Amazon EBS-backed instances. Each instance has a DisableApiTermination attribute with the default value of false (the instance can be terminated through Amazon EC2). You can modify this instance attribute while the instance is running or stopped (in the case of Amazon EBS-backed instances). For more information, see Enabling Termination Protection for an Instance.

You can control whether an instance should stop or terminate when shutdown is initiated from the instance using an operating system command for system shutdown. For more information, see Changing the Instance Initiated Shutdown Behavior.

If you run a script on instance termination, your instance might have an abnormal termination, because we have no way to ensure that shutdown scripts run. Amazon EC2 attempts to shut an instance down cleanly and run any system shutdown scripts; however, certain events (such as hardware failure) may prevent these system shutdown scripts from running.

Terminating an Instance

You can terminate an instance using the AWS Management Console or the command line.

To terminate an instance using the console

Before you terminate the instance, verify that you won't lose any data by checking that your Amazon EBS volumes won't be deleted on termination and that you've copied any data that you need from your instance store volumes to Amazon EBS or Amazon S3.

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, select Instances.

Select the instance, choose Actions, select Instance State, and then select Terminate.

Select Yes, Terminate when prompted for confirmation.

To terminate an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

terminate-instances (AWS CLI)
Stop-EC2Instance (AWS Tools for Windows PowerShell)
Enabling Termination Protection for an Instance

By default, you can terminate your instance using the Amazon EC2 console, command line interface, or API. If you want to prevent your instance from being accidentally terminated using Amazon EC2, you can enable termination protection for the instance. The DisableApiTermination attribute controls whether the instance can be terminated using the console, CLI, or API. By default, termination protection is disabled for your instance. You can set the value of this attribute when you launch the instance, while the instance is running, or while the instance is stopped (for Amazon EBS-backed instances).

The DisableApiTermination attribute does not prevent you from terminating an instance by initiating shutdown from the instance (using an operating system command for system shutdown) when the InstanceInitiatedShutdownBehavior attribute is set. For more information, see Changing the Instance Initiated Shutdown Behavior.

Limits

You can't enable termination protection for Spot instances — a Spot instance is terminated when the Spot price exceeds your bid price. However, you can prepare your application to handle Spot instance interruptions. For more information, see Spot Instance Interruptions.

The DisableApiTermination attribute does not prevent Auto Scaling from terminating an instance. For instances in an Auto Scaling group, use the following Auto Scaling features instead of Amazon EC2 termination protection:

To prevent instances that are part of an Auto Scaling group from terminating on scale in, use instance protection. For more information, see Instance Protection in the Auto Scaling User Guide.
To prevent Auto Scaling from terminating unhealthy instances, suspend the ReplaceUnhealthy process. For more information, see Suspending and Resuming Auto Scaling Processes in the Auto Scaling User Guide.
To specify which instances Auto Scaling should terminate first, choose a termination policy. For more information, see Customizing the Termination Policy in the Auto Scaling User Guide.
To enable termination protection for an instance at launch time

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the dashboard, choose Launch Instance and follow the directions in the wizard.

On the Configure Instance Details page, select the Enable termination protection check box.

To enable termination protection for a running or stopped instance

Select the instance, choose Actions, Instance Settings, and then choose Change Termination Protection.

Select Yes, Enable.

To disable termination protection for a running or stopped instance

Select the instance, choose Actions, Instance Settings, and then choose Change Termination Protection.

Select Yes, Disable.

To enable or disable termination protection using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-instance-attribute (AWS CLI)
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Changing the Instance Initiated Shutdown Behavior

By default, when you initiate a shutdown from an Amazon EBS-backed instance (using a command such as shutdown, halt, or poweroff), the instance stops. You can change this behavior using the InstanceInitiatedShutdownBehavior attribute for the instance so that it terminates instead. You can update this attribute while the instance is running or stopped.

Note that instance store-backed instances can be terminated but they can't be stopped.

You can update the InstanceInitiatedShutdownBehavior attribute using the Amazon EC2 console or the command line. The InstanceInitiatedShutdownBehavior attribute only applies when you perform a shutdown from the operating system of the instance itself; it does not apply when you stop an instance using the StopInstances API or the Amazon EC2 console.

To change the shutdown behavior of an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance, select Actions, Instance Settings, and then choose Change Shutdown Behavior. The current behavior is already selected.

To change the behavior, select an option from the Shutdown behavior list, and then select Apply.


						The Change Shutdown Behavior dialog box
					
To change the shutdown behavior of an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-instance-attribute (AWS CLI)
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Preserving Amazon EBS Volumes on Instance Termination

When an instance terminates, Amazon EC2 uses the value of the DeleteOnTermination attribute for each attached Amazon EBS volume to determine whether to preserve or delete the volume.

By default, the DeletionOnTermination attribute for the root volume of an instance is set to true. Therefore, the default is to delete the root volume of an instance when the instance terminates.

By default, when you attach an EBS volume to an instance, its DeleteOnTermination attribute is set to false. Therefore, the default is to preserve these volumes. After the instance terminates, you can take a snapshot of the preserved volume or attach it to another instance.

To verify the value of the DeleteOnTermination attribute for an EBS volume that is in-use, look at the instance's block device mapping. For more information, see Viewing the EBS Volumes in an Instance Block Device Mapping.

You can change value of the DeleteOnTermination attribute for a volume when you launch the instance or while the instance is running.

Examples

Changing the Root Volume to Persist at Launch Using the Console
Changing the Root Volume to Persist at Launch Using the Command Line
Changing the Root Volume of a Running Instance to Persist Using the Command Line
Changing the Root Volume to Persist at Launch Using the Console

Using the console, you can change the DeleteOnTermination attribute when you launch an instance. To change this attribute for a running instance, you must use the command line.

To change the root volume of an instance to persist at launch using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the console dashboard, select Launch Instance.

On the Choose an Amazon Machine Image (AMI) page, choose an AMI and choose Select.

Follow the wizard to complete the Choose an Instance Type and Configure Instance Details pages.

On the Add Storage page, deselect the Delete On Termination check box for the root volume.

Complete the remaining wizard pages, and then choose Launch.

You can verify the setting by viewing details for the root device volume on the instance's details pane. Next to Block devices, click the entry for the root device volume. By default, Delete on termination is True. If you change the default behavior, Delete on termination is False.

Changing the Root Volume to Persist at Launch Using the Command Line

When you launch an EBS-backed instance, you can use one of the following commands to change the root device volume to persist. For more information about these command line interfaces, see Accessing Amazon EC2.

run-instances (AWS CLI)
New-EC2Instance (AWS Tools for Windows PowerShell)
For example, add the following option to your run-instances command:

Copy
--block-device-mappings file://mapping.json
Specify the following in mapping.json:

Copy
[
  {
    "DeviceName": "/dev/sda1",
    "Ebs": {
      "DeleteOnTermination": false,
      "SnapshotId": "snap-1234567890abcdef0",
      "VolumeType": "gp2"
    }
  }
]
Changing the Root Volume of a Running Instance to Persist Using the Command Line

You can use one of the following commands to change the root device volume of a running EBS-backed instance to persist. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-instance-attribute (AWS CLI)
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
For example, use the following command:

Copy
aws ec2 modify-instance-attribute --instance-id i-1234567890abcdef0 --block-device-mappings file://mapping.json
Specify the following in mapping.json:

Copy
[
  {
    "DeviceName": "/dev/sda1",
    "Ebs": {
      "DeleteOnTermination": false
    }
  }
]
Troubleshooting

If your instance is in the shutting-down state for longer than usual, it will eventually be cleaned up (terminated) by automated processes within the Amazon EC2 service. For more information, see Troubleshooting Terminating (Shutting Down) Your Instance.

Recover Your Instance

You can create an Amazon CloudWatch alarm that monitors an Amazon EC2 instance and automatically recovers the instance if it becomes impaired due to an underlying hardware failure or a problem that requires AWS involvement to repair. Terminated instances cannot be recovered. A recovered instance is identical to the original instance, including the instance ID, private IP addresses, Elastic IP addresses, and all instance metadata. For more information about using Amazon CloudWatch alarms to recover an instance, see Create Alarms That Stop, Terminate, Reboot, or Recover an Instance. To troubleshoot issues with instance recovery failures, see Troubleshooting Instance Recovery Failures in the Amazon EC2 User Guide for Linux Instances.

When the StatusCheckFailed_System alarm is triggered, and the recover action is initiated, you will be notified by the Amazon SNS topic that you selected when you created the alarm and associated the recover action. During instance recovery, the instance is migrated during an instance reboot, and any data that is in-memory is lost. When the process is complete, information is published to the SNS topic you've configured for the alarm. Anyone who is subscribed to this SNS topic will receive an email notification that includes the status of the recovery attempt and any further instructions. You will notice an instance reboot on the recovered instance.

Examples of problems that cause system status checks to fail include:

Loss of network connectivity
Loss of system power
Software issues on the physical host
Hardware issues on the physical host that impact network reachability
The recover action can also be triggered when an instance is scheduled by AWS to stop or retire due to degradation of the underlying hardware. For more information about scheduled events, see Scheduled Events for Your Instances.

The recover action is supported only on instances with the following characteristics:

Use a C3, C4, M3, M4, R3, R4, T2, or X1 instance type
Run in a VPC (not EC2-Classic)
Use shared tenancy (the tenancy attribute is set to default)
Use EBS volumes only (do not configure instance store volumes). For more information, see 'Recover this instance' is disabled.
If your instance has a public IPv4 address, it retains the public IPv4 address after recovery.

Configuring Your Amazon Linux Instance

After you have successfully launched and logged into your Amazon Linux instance, you can make changes to it. There are many different ways you can configure an instance to meet the needs of a specific application. The following are some common tasks to help get you started.

Contents

Common Configuration Scenarios
Managing Software on Your Linux Instance
Managing User Accounts on Your Linux Instance
Processor State Control for Your EC2 Instance
Setting the Time for Your Linux Instance
Changing the Hostname of Your Linux Instance
Setting Up Dynamic DNS on Your Linux Instance
Running Commands on Your Linux Instance at Launch
Instance Metadata and User Data
Common Configuration Scenarios

The base distribution of Amazon Linux contains many software packages and utilities that are required for basic server operations. However, many more software packages are available in various software repositories, and even more packages are available for you to build from source code. For more information on installing and building software from these locations, see Managing Software on Your Linux Instance.

Amazon Linux instances come pre-configured with an ec2-user account, but you may want to add other user accounts that do not have super-user privileges. For more information on adding and removing user accounts, see Managing User Accounts on Your Linux Instance.

The default time configuration for Amazon Linux instances uses Network Time Protocol to set the system time on an instance. The default time zone is UTC. For more information on setting the time zone for an instance or using your own time server, see Setting the Time for Your Linux Instance.

If you have your own network with a domain name registered to it, you can change the hostname of an instance to identify itself as part of that domain. You can also change the system prompt to show a more meaningful name without changing the hostname settings. For more information, see Changing the Hostname of Your Linux Instance. You can configure an instance to use a dynamic DNS service provider. For more information, see Setting Up Dynamic DNS on Your Linux Instance.

When you launch an instance in Amazon EC2, you have the option of passing user data to the instance that can be used to perform common configuration tasks and even run scripts after the instance starts. You can pass two types of user data to Amazon EC2, cloud-init directives, and shell scripts. For more information, see Running Commands on Your Linux Instance at Launch.

Managing Software on Your Linux Instance

The base distribution of Amazon Linux contains many software packages and utilities that are required for basic server operations. However, many more software packages are available in various software repositories, and even more packages are available for you to build from source code.

Contents

Updating Instance Software
Adding Repositories
Finding Software Packages
Installing Software Packages
Preparing to Compile Software
It is important to keep software up-to-date. Many packages in a Linux distribution are updated frequently to fix bugs, add features, and protect against security exploits. For more information, see Updating Instance Software.

By default, Amazon Linux instances launch with two repositories enabled: amzn-main and amzn-updates. While there are many packages available in these repositories that are updated by Amazon Web Services, there may be a package that you wish to install that is contained in another repository. For more information, see Adding Repositories. For help finding packages in enabled repositories, see Finding Software Packages. For information about installing software on an Amazon Linux instance, see Installing Software Packages.

Not all software is available in software packages stored in repositories; some software must be compiled on an instance from its source code. For more information, see Preparing to Compile Software.

Amazon Linux instances manage their software using the yum package manager. The yum package manager can install, remove, and update software, as well as manage all of the dependencies for each package. Debian-based Linux distributions, like Ubuntu, use the apt-get command and dpkg package manager, so the yum examples in the following sections do not work for those distributions.

Updating Instance Software

It is important to keep software up-to-date. Many packages in a Linux distribution are updated frequently to fix bugs, add features, and protect against security exploits. When you first launch and connect to an Amazon Linux instance, you may see a message asking you to update software packages for security purposes. This section shows how to update an entire system, or just a single package.

Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
       __|  __|_  )
       _|  (     /   Amazon Linux AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-ami/2013.03-release-notes/
There are 12 security update(s) out of 25 total update(s) available
Run "sudo yum update" to apply all updates.
[ec2-user ~]$
To update all packages on an Amazon Linux instance

(Optional) Start a screen session in your shell window. Sometimes you may experience a network interruption that can disconnect the SSH connection to your instance. If this happens during a long software update, it can leave the instance in a recoverable, although confused state. A screen session allows you to continue running the update even if your connection is interrupted, and you can reconnect to the session later without problems.

Execute the screen command to begin the session.

Copy
[ec2-user ~]$ screen
If your session is disconnected, log back into your instance and list the available screens.

Copy
[ec2-user ~]$ screen -ls
There is a screen on:
	17793.pts-0.ip-12-34-56-78	(Detached)
1 Socket in /var/run/screen/S-ec2-user.
Reconnect to the screen using the screen -r command and the process ID from the previous command.

Copy
[ec2-user ~]$ screen -r 17793
When you are finished using screen, use the exit command to close the session.

Copy
[ec2-user ~]$ exit
[screen is terminating]
Run the yum update command. Optionally, you can add the --security flag to apply only security updates.

Copy
[ec2-user ~]$ sudo yum update
Loaded plugins: priorities, security, update-motd, upgrade-helper
amzn-main                                                | 2.1 kB     00:00
amzn-updates                                             | 2.3 kB     00:00
Setting up Update Process
Resolving Dependencies
--> Running transaction check
---> Package aws-apitools-ec2.noarch 0:1.6.8.1-1.0.amzn1 will be updated
---> Package aws-apitools-ec2.noarch 0:1.6.10.0-1.0.amzn1 will be an update
---> Package gnupg2.x86_64 0:2.0.18-1.16.amzn1 will be updated
---> Package gnupg2.x86_64 0:2.0.19-8.21.amzn1 will be an update
---> Package libgcrypt.i686 0:1.4.5-9.10.amzn1 will be updated
---> Package libgcrypt.x86_64 0:1.4.5-9.10.amzn1 will be updated
---> Package libgcrypt.i686 0:1.4.5-9.12.amzn1 will be an update
---> Package libgcrypt.x86_64 0:1.4.5-9.12.amzn1 will be an update
---> Package openssl.x86_64 1:1.0.1e-4.53.amzn1 will be updated
---> Package openssl.x86_64 1:1.0.1e-4.54.amzn1 will be an update
---> Package python-boto.noarch 0:2.9.9-1.0.amzn1 will be updated
---> Package python-boto.noarch 0:2.13.3-1.0.amzn1 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package              Arch       Version                 Repository        Size
================================================================================
Updating:
 aws-apitools-ec2     noarch     1.6.10.0-1.0.amzn1      amzn-updates      14 M
 gnupg2               x86_64     2.0.19-8.21.amzn1       amzn-updates     2.4 M
 libgcrypt            i686       1.4.5-9.12.amzn1        amzn-updates     248 k
 libgcrypt            x86_64     1.4.5-9.12.amzn1        amzn-updates     262 k
 openssl              x86_64     1:1.0.1e-4.54.amzn1     amzn-updates     1.7 M
 python-boto          noarch     2.13.3-1.0.amzn1        amzn-updates     1.6 M

Transaction Summary
================================================================================
Upgrade       6 Package(s)

Total download size: 20 M
Is this ok [y/N]:
Review the packages listed, type y, and press Enter to accept the updates. Updating all of the packages on a system can take several minutes. The yum output shows the status of the update while it is running.

Downloading Packages:
(1/6): aws-apitools-ec2-1.6.10.0-1.0.amzn1.noarch.rpm    |  14 MB     00:00
(2/6): gnupg2-2.0.19-8.21.amzn1.x86_64.rpm               | 2.4 MB     00:00
(3/6): libgcrypt-1.4.5-9.12.amzn1.i686.rpm               | 248 kB     00:00
(4/6): libgcrypt-1.4.5-9.12.amzn1.x86_64.rpm             | 262 kB     00:00
(5/6): openssl-1.0.1e-4.54.amzn1.x86_64.rpm              | 1.7 MB     00:00
(6/6): python-boto-2.13.3-1.0.amzn1.noarch.rpm           | 1.6 MB     00:00
--------------------------------------------------------------------------------
Total                                            28 MB/s |  20 MB     00:00
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Updating   : libgcrypt-1.4.5-9.12.amzn1.x86_64                           1/12
  Updating   : gnupg2-2.0.19-8.21.amzn1.x86_64                             2/12
  Updating   : aws-apitools-ec2-1.6.10.0-1.0.amzn1.noarch                  3/12
  Updating   : 1:openssl-1.0.1e-4.54.amzn1.x86_64                          4/12
  ...

Complete!
(Optional) Reboot your instance to ensure that you are using the latest packages and libraries from your update; kernel updates are not loaded until a reboot occurs. Updates to any glibc libraries should also be followed by a reboot. For updates to packages that control services, it may be sufficient to restart the services to pick up the updates, but a system reboot ensures that all previous package and library updates are complete.

To update a single package on an Amazon Linux instance

Use this procedure to update a single package (and its dependencies) and not the entire system.

Run the yum update command with the name of the package you would like to update.

Copy
[ec2-user ~]$ sudo yum update openssl
Loaded plugins: priorities, security, update-motd, upgrade-helper
amzn-main                                                | 2.1 kB     00:00
amzn-updates                                             | 2.3 kB     00:00
Setting up Update Process
Resolving Dependencies
--> Running transaction check
---> Package openssl.x86_64 1:1.0.1e-4.53.amzn1 will be updated
---> Package openssl.x86_64 1:1.0.1e-4.54.amzn1 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package       Arch         Version                    Repository          Size
================================================================================
Updating:
 openssl       x86_64       1:1.0.1e-4.54.amzn1        amzn-updates       1.7 M

Transaction Summary
================================================================================
Upgrade       1 Package(s)

Total download size: 1.7 M
Is this ok [y/N]:
Review the package information listed, type y, and press Enter to accept the update or updates. Sometimes there will be more than one package listed if there are package dependencies that must be resolved. The yum output shows the status of the update while it is running.

Downloading Packages:
openssl-1.0.1e-4.54.amzn1.x86_64.rpm                     | 1.7 MB     00:00
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Updating   : 1:openssl-1.0.1e-4.54.amzn1.x86_64                           1/2
  Cleanup    : 1:openssl-1.0.1e-4.53.amzn1.x86_64                           2/2
  Verifying  : 1:openssl-1.0.1e-4.54.amzn1.x86_64                           1/2
  Verifying  : 1:openssl-1.0.1e-4.53.amzn1.x86_64                           2/2

Updated:
  openssl.x86_64 1:1.0.1e-4.54.amzn1

Complete!
(Optional) Reboot your instance to ensure that you are using the latest packages and libraries from your update; kernel updates are not loaded until a reboot occurs. Updates to any glibc libraries should also be followed by a reboot. For updates to packages that control services, it may be sufficient to restart the services to pick up the updates, but a system reboot ensures that all previous package and library updates are complete.

Adding Repositories

By default, Amazon Linux instances launch with two repositories enabled: amzn-main and amzn-updates. While there are many packages available in these repositories that are updated by Amazon Web Services, there may be a package that you wish to install that is contained in another repository.

Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
To install a package from a different repository with yum, you need to add the repository information to the /etc/yum.conf file or to its own repository.repo file in the /etc/yum.repos.d directory. You can do this manually, but most yum repositories provide their own repository.repo file at their repository URL.

To determine what yum repositories are already installed

List the installed yum repositories with the following command:

Copy
[ec2-user ~]$ yum repolist all
The resulting output lists the installed repositories and reports the status of each. Enabled repositories display the number of packages they contain.

repo id                             repo name                                                                status
!amzn-main/latest                   amzn-main-Base                                                           enabled: 5,612
amzn-main-debuginfo/latest          amzn-main-debuginfo                                                      disabled
amzn-main-source/latest             amzn-main-source                                                         disabled
amzn-nosrc/latest                   amzn-nosrc-Base                                                          disabled
amzn-preview/latest                 amzn-preview-Base                                                        disabled
amzn-preview-debuginfo/latest       amzn-preview-debuginfo                                                   disabled
amzn-preview-source/latest          amzn-preview-source                                                      disabled
!amzn-updates/latest                amzn-updates-Base                                                        enabled: 1,152
amzn-updates-debuginfo/latest       amzn-updates-debuginfo                                                   disabled
amzn-updates-source/latest          amzn-updates-source                                                      disabled
epel/x86_64                         Extra Packages for Enterprise Linux 6 - x86_64                           disabled
epel-debuginfo/x86_64               Extra Packages for Enterprise Linux 6 - x86_64 - Debug                   disabled
epel-source/x86_64                  Extra Packages for Enterprise Linux 6 - x86_64 - Source                  disabled
epel-testing/x86_64                 Extra Packages for Enterprise Linux 6 - Testing - x86_64                 disabled
epel-testing-debuginfo/x86_64       Extra Packages for Enterprise Linux 6 - Testing - x86_64 - Debug         disabled
epel-testing-source/x86_64          Extra Packages for Enterprise Linux 6 - Testing - x86_64 - Source        disabled 
To add a yum repository to /etc/yum.repos.d

Find the location of the .repo file. This will vary depending on the repository you are adding. In this example, the .repo file is at https://www.example.com/repository.repo.

Add the repository with the yum-config-manager command.

Copy
[ec2-user ~]$ sudo yum-config-manager --add-repo https://www.example.com/repository.repo
Loaded plugins: priorities, update-motd, upgrade-helper
adding repo from: https://www.example.com/repository.repo
grabbing file https://www.example.com/repository.repo to /etc/yum.repos.d/repository.repo
repository.repo                                      | 4.0 kB     00:00
repo saved to /etc/yum.repos.d/repository.repo
After you install a repository, you must enable it as described in the next procedure.

To enable a yum repository in /etc/yum.repos.d

Use the yum-config-manager command with the --enable repository flag. The following command enables the Extra Packages for Enterprise Linux (EPEL) repository from the Fedora project. By default, this repository is present in /etc/yum.repos.d on Amazon Linux instances, but it is not enabled.

Copy
[ec2-user ~]$ sudo yum-config-manager --enable epel
Note
For information on enabling the EPEL repository on other distributions, such as Red Hat and CentOS, see the EPEL documentation at https://fedoraproject.org/wiki/EPEL.

Finding Software Packages

You can use the yum search command to search the descriptions of packages that are available in your configured repositories. This is especially helpful if you don't know the exact name of the package you want to install. Simply append the keyword search to the command; for multiple word searches, wrap the search query with quotation marks.

Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
Multiple word search queries in quotation marks only return results that match the exact query. If you don't see the expected package, simplify your search to one keyword and then scan the results. You can also try keyword synonyms to broaden your search.

Copy
[ec2-user ~]$ sudo yum search "find"
Loaded plugins: priorities, security, update-motd, upgrade-helper
============================== N/S Matched: find ===============================
findutils.x86_64 : The GNU versions of find utilities (find and xargs)
perl-File-Find-Rule.noarch : Perl module implementing an alternative interface
                           : to File::Find
perl-Module-Find.noarch : Find and use installed modules in a (sub)category
libpuzzle.i686 : Library to quickly find visually similar images (gif, png, jpg)
libpuzzle.x86_64 : Library to quickly find visually similar images (gif, png,
                 : jpg)
mlocate.x86_64 : An utility for finding files by name
The yum package manager also combines several packages into groups that you can install with one command to perform a particular task, such as installing a web server or build tools for software compilation. To list the groups that are already installed on your system and the available groups that you can install, use the yum grouplist command.

Copy
[ec2-user ~]$ sudo yum grouplist
Loaded plugins: priorities, security, update-motd, upgrade-helper
Setting up Group Process
Installed Groups:
   Development Libraries
   Development tools
   Editors
   Legacy UNIX compatibility
   Mail Server
   MySQL Database
   Network Servers
   Networking Tools
   PHP Support
   Perl Support
   System Tools
   Web Server
Available Groups:
   Console internet tools
   DNS Name Server
   FTP Server
   Java Development
   MySQL Database client
   NFS file server
   Performance Tools
   PostgreSQL Database client (version 8)
   PostgreSQL Database server (version 8)
   Scientific support
   TeX support
   Technical Writing
   Web Servlet Engine
Done
You can see the different packages in a group by using the yum groupinfo "Group Name" command, replacing Group Name with the name of the group to get information about. This command lists all of the mandatory, default, and optional packages that can be installed with that group.

If you cannot find the software you need in the default amzn-main and amzn-updates repositories, you can add more repositories, such as the Extra Packages for Enterprise Linux (EPEL) repository. For more information, see Adding Repositories.

Installing Software Packages

The yum package manager is a great tool for installing software, because it can search all of your enabled repositories for different software packages and also handle any dependencies in the software installation process.

Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
To install a package from a repository, use the yum install package command, replacing package with the name of the software to install. For example, to install the links text-based web browser, enter the following command.

Copy
[ec2-user ~]$ sudo yum install links
To install a group of packages, use the yum groupinstall Group Name command, replacing Group Name with the name of the group you would like to install. For example, to install the "Performance Tools" group, enter the following command.

Copy
[ec2-user ~]$ sudo yum groupinstall "Performance Tools"
By default, yum will only install the mandatory and default packages in the group listing. If you would like to install the optional packages in the group also, you can set the group_package_types configuration parameter in the command when you execute it that adds the optional packages.

Copy
[ec2-user ~]$ sudo yum --setopt=group_package_types=mandatory,default,optional groupinstall "Performance Tools"
You can also use yum install to install RPM package files that you have downloaded from the Internet. To do this, simply append the path name of an RPM file to the installation command instead of a repository package name.

Copy
[ec2-user ~]$ sudo yum install my-package.rpm

Preparing to Compile Software

There is a wealth of open-source software available on the Internet that has not been pre-compiled and made available for download from a package repository. You may eventually discover a software package that you need to compile yourself, from its source code. For your system to be able to compile software, you need to install several development tools, such as make, gcc, and autoconf.

Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
Because software compilation is not a task that every Amazon EC2 instance requires, these tools are not installed by default, but they are available in a package group called "Development Tools" that is easily added to an instance with the yum groupinstall command.

Copy
[ec2-user ~]$ sudo yum groupinstall "Development Tools"
Software source code packages are often available for download (from web sites such as https://github.com/ and http://sourceforge.net/) as a compressed archive file, called a tarball. These tarballs will usually have the .tar.gz file extension. You can decompress these archives with the tar command.

Copy
[ec2-user ~]$ tar -xzf software.tar.gz
After you have decompressed and unarchived the source code package, you should look for a README or INSTALL file in the source code directory that can provide you with further instructions for compiling and installing the source code.

To retrieve source code for Amazon Linux packages

Amazon Web Services provides the source code for maintained packages. You can download the source code for any installed packages with the yumdownloader --source command.

Run the yumdownloader --source package command to download the source code for package. For example, to download the source code for the htop package, enter the following command.

Copy
[ec2-user ~]$ yumdownloader --source htop

Loaded plugins: priorities, update-motd, upgrade-helper
Enabling amzn-updates-source repository
Enabling amzn-main-source repository
amzn-main-source                                                                                              | 1.9 kB  00:00:00     
amzn-updates-source                                                                                           | 1.9 kB  00:00:00     
(1/2): amzn-updates-source/latest/primary_db                                                                  |  52 kB  00:00:00     
(2/2): amzn-main-source/latest/primary_db                                                                     | 734 kB  00:00:00     
htop-1.0.1-2.3.amzn1.src.rpm
The location of the source RPM is in the directory from which you ran the command.

Managing User Accounts on Your Linux Instance

Each Linux instance type launches with a default Linux system user account. For Amazon Linux, the user name is ec2-user. For RHEL, the user name is ec2-user or root. For Ubuntu, the user name is ubuntu or root. For Centos, the user name is centos. For Fedora, the user name is ec2-user. For SUSE, the user name is ec2-user or root. Otherwise, if ec2-user and root don't work, check with your AMI provider.

Note
Linux system users should not be confused with AWS Identity and Access Management (IAM) users. For more information, see IAM Users and Groups in the IAM User Guide.
Using the default user account is adequate for many applications, but you may choose to add user accounts so that individuals can have their own files and workspaces. Creating user accounts for new users is much more secure than granting multiple (possibly inexperienced) users access to the ec2-user account, because that account can cause a lot of damage to a system when used improperly.

After you add the user account, you must set up access keys that allow the user to log in.

Prerequisites

Create a key pair for the user or use an existing key pair. For more information, see Creating a Key Pair Using Amazon EC2. To retrieve a public key from an existing key pair, see Retrieving the Public Key for Your Key Pair on Linux.

To add a user account

Use the following adduser command to add the newuser account to the system (with an entry in the /etc/passwd file). This command also creates a group and a home directory for the account.

Copy
[ec2-user ~]$ sudo adduser newuser
[Ubuntu] When adding a user to an Ubuntu system, include the --disabled-password option with this command to avoid adding a password to the account.

Copy
[ubuntu ~]$ sudo adduser newuser --disabled-password
Switch to the new account so that newly created files have the proper ownership.

Copy
[ec2-user ~]$ sudo su - newuser
[newuser ~]$
Notice that the prompt changes from ec2-user to newuser to indicate that you have switched the shell session to the new account.

Create a .ssh directory in the newuser home directory and change its file permissions to 700 (only the owner can read, write, or open the directory).

Copy
[newuser ~]$ mkdir .ssh
[newuser ~]$ chmod 700 .ssh
Important
Without these exact file permissions, the user will not be able to log in.
Create a file named authorized_keys in the .ssh directory and change its file permissions to 600 (only the owner can read or write to the file).

Copy
[newuser ~]$ touch .ssh/authorized_keys
[newuser ~]$ chmod 600 .ssh/authorized_keys
Important
Without these exact file permissions, the user will not be able to log in.
Open the authorized_keys file using your favorite text editor. Paste the public key for your key pair into the file. For example:

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClKsfkNkuSevGj3eYhCe53pcjqP3maAhDFcvBS7O6V
hz2ItxCih+PnDSUaw+WNQn/mZphTk/a/gU8jEzoOWbkM4yxyb/wB96xbiFveSFJuOp/d6RJhJOI0iBXr
lsLnBItntckiJ7FbtxJMXLvvwJryDUilBMTjYtwB+QhYXUMOzce5Pjz5/i8SeJtjnV3iAoG/cQk+0FzZ
qaeJAAHco+CY/5WrUBkrHmFJr6HcXkvJdWPkYQS3xqC0+FmUZofz221CBt5IMucxXPkX4rWi+z7wB3Rb
BQoQzd8v7yeb7OzlPnWOyN0qFU0XA246RA8QFYiCNYwI3f05p6KLxEXAMPLE
The user should now be able to log into the newuser account on your instance using the private key that corresponds to the public key that you added to the authorized_keys file.

To remove a user from the system

If a user account is no longer needed, you can remove that account so that it may no longer be used. When you specify the -r option, the user's home directory and mail spool are deleted. To keep the user's home directory and mail spool, omit the -r option.

Copy
[ec2-user ~]$ sudo userdel -r olduser

Processor State Control for Your EC2 Instance

C-states control the sleep levels that a core can enter when it is idle. C-states are numbered starting with C0 (the shallowest state where the core is totally awake and executing instructions) and go to C6 (the deepest idle state where a core is powered off). P-states control the desired performance (in CPU frequency) from a core. P-states are numbered starting from P0 (the highest performance setting where the core is allowed to use Intel Turbo Boost Technology to increase frequency if possible), and they go from P1 (the P-state that requests the maximum baseline frequency) to P15 (the lowest possible frequency).

The following instance types provide the ability for an operating system to control processor C-states and P-states:

c4.8xlarge
d2.8xlarge
f1.16xlarge
g3.16xlarge
i3.16xlarge
m4.10xlarge
m4.16xlarge
p2.16xlarge
r4.8xlarge
r4.16xlarge
x1.16xlarge
x1.32xlarge
You might want to change the C-state or P-state settings to increase processor performance consistency, reduce latency, or tune your instance for a specific workload. The default C-state and P-state settings provide maximum performance, which is optimal for most workloads. However, if your application would benefit from reduced latency at the cost of higher single- or dual-core frequencies, or from consistent performance at lower frequencies as opposed to bursty Turbo Boost frequencies, consider experimenting with the C-state or P-state settings that are available to these instances.

The following sections describe the different processor state configurations and how to monitor the effects of your configuration. These procedures were written for, and apply to Amazon Linux; however, they may also work for other Linux distributions with a Linux kernel version of 3.9 or newer. For more information about other Linux distributions and processor state control, see your system-specific documentation.

Note
The examples on this page use the turbostat utility (which is available on Amazon Linux by default) to display processor frequency and C-state information, and the stress command (which can be installed by running sudo yum install -y stress) to simulate a workload.
Contents

Highest Performance with Maximum Turbo Boost Frequency
High Performance and Low Latency by Limiting Deeper C-states
Baseline Performance with the Lowest Variability
Highest Performance with Maximum Turbo Boost Frequency

This is the default processor state control configuration for the Amazon Linux AMI, and it is recommended for most workloads. This configuration provides the highest performance with lower variability. Allowing inactive cores to enter deeper sleep states provides the thermal headroom required for single or dual core processes to reach their maximum Turbo Boost potential.

The following example shows a c4.8xlarge instance with two cores actively performing work reaching their maximum processor Turbo Boost frequency.

Copy
[ec2-user ~]$ sudo turbostat stress -c 2 -t 10
stress: info: [30680] dispatching hogs: 2 cpu, 0 io, 0 vm, 0 hdd
stress: info: [30680] successful run completed in 10s
pk cor CPU    %c0  GHz  TSC SMI    %c1    %c3    %c6    %c7   %pc2   %pc3   %pc6   %pc7  Pkg_W RAM_W PKG_% RAM_%
             5.54 3.44 2.90   0   9.18   0.00  85.28   0.00   0.00   0.00   0.00   0.00  94.04 32.70 54.18  0.00
 0   0   0   0.12 3.26 2.90   0   3.61   0.00  96.27   0.00   0.00   0.00   0.00   0.00  48.12 18.88 26.02  0.00
 0   0  18   0.12 3.26 2.90   0   3.61
 0   1   1   0.12 3.26 2.90   0   4.11   0.00  95.77   0.00
 0   1  19   0.13 3.27 2.90   0   4.11
 0   2   2   0.13 3.28 2.90   0   4.45   0.00  95.42   0.00
 0   2  20   0.11 3.27 2.90   0   4.47
 0   3   3   0.05 3.42 2.90   0  99.91   0.00   0.05   0.00
 0   3  21  97.84 3.45 2.90   0   2.11
...
  1   1  10   0.06 3.33 2.90   0  99.88   0.01   0.06   0.00
 1   1  28  97.61 3.44 2.90   0   2.32
...
10.002556 sec
In this example, vCPUs 21 and 28 are running at their maximum Turbo Boost frequency because the other cores have entered the C6 sleep state to save power and provide both power and thermal headroom for the working cores. vCPUs 3 and 10 (each sharing a processor core with vCPUs 21 and 28) are in the C1 state, waiting for instruction.

In the following example, all 18 cores are actively performing work, so there is no headroom for maximum Turbo Boost, but they are all running at the "all core Turbo Boost" speed of 3.2 GHz.

Copy
[ec2-user ~]$ sudo turbostat stress -c 36 -t 10
stress: info: [30685] dispatching hogs: 36 cpu, 0 io, 0 vm, 0 hdd
stress: info: [30685] successful run completed in 10s
pk cor CPU    %c0  GHz  TSC SMI    %c1    %c3    %c6    %c7   %pc2   %pc3   %pc6   %pc7  Pkg_W RAM_W PKG_% RAM_%
            99.27 3.20 2.90   0   0.26   0.00   0.47   0.00   0.00   0.00   0.00   0.00 228.59 31.33 199.26  0.00
 0   0   0  99.08 3.20 2.90   0   0.27   0.01   0.64   0.00   0.00   0.00   0.00   0.00 114.69 18.55 99.32  0.00
 0   0  18  98.74 3.20 2.90   0   0.62
 0   1   1  99.14 3.20 2.90   0   0.09   0.00   0.76   0.00
 0   1  19  98.75 3.20 2.90   0   0.49
 0   2   2  99.07 3.20 2.90   0   0.10   0.02   0.81   0.00
 0   2  20  98.73 3.20 2.90   0   0.44
 0   3   3  99.02 3.20 2.90   0   0.24   0.00   0.74   0.00
 0   3  21  99.13 3.20 2.90   0   0.13
 0   4   4  99.26 3.20 2.90   0   0.09   0.00   0.65   0.00
 0   4  22  98.68 3.20 2.90   0   0.67
 0   5   5  99.19 3.20 2.90   0   0.08   0.00   0.73   0.00
 0   5  23  98.58 3.20 2.90   0   0.69
 0   6   6  99.01 3.20 2.90   0   0.11   0.00   0.89   0.00
 0   6  24  98.72 3.20 2.90   0   0.39
...
High Performance and Low Latency by Limiting Deeper C-states

C-states control the sleep levels that a core may enter when it is inactive. You may want to control C-states to tune your system for latency versus performance. Putting cores to sleep takes time, and although a sleeping core allows more headroom for another core to boost to a higher frequency, it takes time for that sleeping core to wake back up and perform work. For example, if a core that is assigned to handle network packet interrupts is asleep, there may be a delay in servicing that interrupt. You can configure the system to not use deeper C-states, which reduces the processor reaction latency, but that in turn also reduces the headroom available to other cores for Turbo Boost.

A common scenario for disabling deeper sleep states is a Redis database application, which stores the database in system memory for the fastest possible query response time.

To limit deeper sleep states on Amazon Linux

Open the /boot/grub/grub.conf file with your editor of choice.

Copy
[ec2-user ~]$ sudo vim /boot/grub/grub.conf
Edit the kernel line of the first entry and add the intel_idle.max_cstate=1 option to set C1 as the deepest C-state for idle cores.

# created by imagebuilder
default=0
timeout=1
hiddenmenu

title Amazon Linux 2014.09 (3.14.26-24.46.amzn1.x86_64)
root (hd0,0)
kernel /boot/vmlinuz-3.14.26-24.46.amzn1.x86_64 root=LABEL=/ console=ttyS0 intel_idle.max_cstate=1
initrd /boot/initramfs-3.14.26-24.46.amzn1.x86_64.img
Save the file and exit your editor.

Reboot your instance to enable the new kernel option.

Copy
[ec2-user ~]$ sudo reboot
The following example shows a c4.8xlarge instance with two cores actively performing work at the "all core Turbo Boost" core frequency.

Copy
[ec2-user ~]$ sudo turbostat stress -c 2 -t 10
stress: info: [5322] dispatching hogs: 2 cpu, 0 io, 0 vm, 0 hdd
stress: info: [5322] successful run completed in 10s
pk cor CPU    %c0  GHz  TSC SMI    %c1    %c3    %c6    %c7   %pc2   %pc3   %pc6   %pc7  Pkg_W RAM_W PKG_% RAM_%
             5.56 3.20 2.90   0  94.44   0.00   0.00   0.00   0.00   0.00   0.00   0.00 131.90 31.11 199.47  0.00
 0   0   0   0.03 2.08 2.90   0  99.97   0.00   0.00   0.00   0.00   0.00   0.00   0.00  67.23 17.11 99.76  0.00
 0   0  18   0.01 1.93 2.90   0  99.99
 0   1   1   0.02 1.96 2.90   0  99.98   0.00   0.00   0.00
 0   1  19  99.70 3.20 2.90   0   0.30
...
 1   1  10   0.02 1.97 2.90   0  99.98   0.00   0.00   0.00
 1   1  28  99.67 3.20 2.90   0   0.33
 1   2  11   0.04 2.63 2.90   0  99.96   0.00   0.00   0.00
 1   2  29   0.02 2.11 2.90   0  99.98
...
In this example, the cores for vCPUs 19 and 28 are running at 3.2 GHz, and the other cores are in the C1 C-state, awaiting instruction. Although the working cores are not reaching their maximum Turbo Boost frequency, the inactive cores will be much faster to respond to new requests than they would be in the deeper C6 C-state.

Baseline Performance with the Lowest Variability

You can reduce the variability of processor frequency with P-states. P-states control the desired performance (in CPU frequency) from a core. Most workloads perform better in P0, which requests Turbo Boost. But you may want to tune your system for consistent performance rather than bursty performance that can happen when Turbo Boost frequencies are enabled.

Intel Advanced Vector Extensions (AVX or AVX2) workloads can perform well at lower frequencies, and AVX instructions can use more power. Running the processor at a lower frequency, by disabling Turbo Boost, can reduce the amount of power used and keep the speed more consistent. For more information about optimizing your instance configuration and workload for AVX, see http://www.intel.com/content/dam/www/public/us/en/documents/white-papers/performance-xeon-e5-v3-advanced-vector-extensions-paper.pdf.

This section describes how to limit deeper sleep states and disable Turbo Boost (by requesting the P1 P-state) to provide low-latency and the lowest processor speed variability for these types of workloads.

To limit deeper sleep states and disable Turbo Boost on Amazon Linux

Open the /boot/grub/grub.conf file with your editor of choice.

Copy
[ec2-user ~]$ sudo vim /boot/grub/grub.conf
Edit the kernel line of the first entry and add the intel_idle.max_cstate=1 option to set C1 as the deepest C-state for idle cores.

# created by imagebuilder
default=0
timeout=1
hiddenmenu

title Amazon Linux 2014.09 (3.14.26-24.46.amzn1.x86_64)
root (hd0,0)
kernel /boot/vmlinuz-3.14.26-24.46.amzn1.x86_64 root=LABEL=/ console=ttyS0 intel_idle.max_cstate=1
initrd /boot/initramfs-3.14.26-24.46.amzn1.x86_64.img
Save the file and exit your editor.

Reboot your instance to enable the new kernel option.

Copy
[ec2-user ~]$ sudo reboot
When you need the low processor speed variability that the P1 P-state provides, execute the following command to disable Turbo Boost.

Copy
[ec2-user ~]$ sudo sh -c "echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo"
When your workload is finished, you can re-enable Turbo Boost with the following command.

Copy
[ec2-user ~]$ sudo sh -c "echo 0 > /sys/devices/system/cpu/intel_pstate/no_turbo"
The following example shows a c4.8xlarge instance with two vCPUs actively performing work at the baseline core frequency, with no Turbo Boost.

Copy
[ec2-user ~]$ sudo turbostat stress -c 2 -t 10
stress: info: [5389] dispatching hogs: 2 cpu, 0 io, 0 vm, 0 hdd
stress: info: [5389] successful run completed in 10s
pk cor CPU    %c0  GHz  TSC SMI    %c1    %c3    %c6    %c7   %pc2   %pc3   %pc6   %pc7  Pkg_W RAM_W PKG_% RAM_%
             5.59 2.90 2.90   0  94.41   0.00   0.00   0.00   0.00   0.00   0.00   0.00 128.48 33.54 200.00  0.00
 0   0   0   0.04 2.90 2.90   0  99.96   0.00   0.00   0.00   0.00   0.00   0.00   0.00  65.33 19.02 100.00  0.00
 0   0  18   0.04 2.90 2.90   0  99.96
 0   1   1   0.05 2.90 2.90   0  99.95   0.00   0.00   0.00
 0   1  19   0.04 2.90 2.90   0  99.96
 0   2   2   0.04 2.90 2.90   0  99.96   0.00   0.00   0.00
 0   2  20   0.04 2.90 2.90   0  99.96
 0   3   3   0.05 2.90 2.90   0  99.95   0.00   0.00   0.00
 0   3  21  99.95 2.90 2.90   0   0.05
...
 1   1  28  99.92 2.90 2.90   0   0.08
 1   2  11   0.06 2.90 2.90   0  99.94   0.00   0.00   0.00
 1   2  29   0.05 2.90 2.90   0  99.95
The cores for vCPUs 21 and 28 are actively performing work at the baseline processor speed of 2.9 GHz, and all inactive cores are also running at the baseline speed in the C1 C-state, ready to accept instructions.

Setting the Time for Your Linux Instance

A consistent and accurate time reference is crucial for many server tasks and processes. Most system logs include a time stamp that you can use to determine when problems occur and in what order the events take place. If you use the AWS CLI or an AWS SDK to make requests from your instance, these tools sign requests on your behalf. If your instance's date and time are not set correctly, the date in the signature may not match the date of the request, and AWS rejects the request. Network Time Protocol (NTP) is configured by default on Amazon Linux instances, and the system time is synchronized with a load-balanced pool of public servers on the Internet and set to the UTC time zone. For more information about NTP, go to http://www.ntp.org/.

Tasks

Changing the Time Zone
Configuring Network Time Protocol (NTP)
Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
Changing the Time Zone

Amazon Linux instances are set to the UTC (Coordinated Universal Time) time zone by default, but you may wish to change the time on an instance to the local time or to another time zone in your network.

To change the time zone on an instance

Identify the time zone to use on the instance. The /usr/share/zoneinfo directory contains a hierarchy of time zone data files. Browse the directory structure at that location to find a file for your time zone.

Copy
[ec2-user ~]$ ls /usr/share/zoneinfo
Africa      Chile    GB         Indian       Mideast   posixrules  US
America     CST6CDT  GB-Eire    Iran         MST       PRC         UTC
Antarctica  Cuba     GMT        iso3166.tab  MST7MDT   PST8PDT     WET
Arctic      EET      GMT0       Israel       Navajo    right       W-SU
...
Some of the entries at this location are directories (such as America), and these directories contain time zone files for specific cities. Find your city (or a city in your time zone) to use for the instance. In this example, you can use the time zone file for Los Angeles, /usr/share/zoneinfo/America/Los_Angeles.

Update the /etc/sysconfig/clock file with the new time zone.

Open the /etc/sysconfig/clock file with your favorite text editor (such as vim or nano). You need to use sudo with your editor command because /etc/sysconfig/clock is owned by root.

Locate the ZONE entry, and change it to the time zone file (omitting the /usr/share/zoneinfo section of the path). For example, to change to the Los Angeles time zone, change the ZONE entry to the following.

Copy
ZONE="America/Los_Angeles"
Note
Do not change the UTC=true entry to another value. This entry is for the hardware clock, and does not need to be adjusted when you're setting a different time zone on your instance.
Save the file and exit the text editor.

Create a symbolic link between /etc/localtime and your time zone file so that the instance finds the time zone file when it references local time information.

Copy
[ec2-user ~]$ sudo ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
Reboot the system to pick up the new time zone information in all services and applications.

Copy
[ec2-user ~]$ sudo reboot
Configuring Network Time Protocol (NTP)

Network Time Protocol (NTP) is configured by default on Amazon Linux instances; however, an instance needs access to the Internet for the standard NTP configuration to work. In addition, your instance's security group rules must allow outbound UDP traffic on port 123 (NTP), and your network ACL rules must allow both inbound and outbound UDP traffic on port 123. The procedures in this section show how to verify that the default NTP configuration is working correctly. If your instance does not have access to the Internet, you need to configure NTP to query a different server in your private network to keep accurate time.

To verify that NTP is working properly

Use the ntpstat command to view the status of the NTP service on the instance.

Copy
[ec2-user ~]$ ntpstat
If your output resembles the output below, then NTP is working properly on the instance.

synchronised to NTP server (12.34.56.78) at stratum 3
   time correct to within 399 ms
   polling server every 64 s
If your output states, "unsynchronised", wait a minute and try again. The first synchronization may take a minute to complete.

If your output states, "Unable to talk to NTP daemon. Is it running?", you probably need to start the NTP service and enable it to automatically start at boot time.

(Optional) You can use the ntpq -p command to see a list of peers known to the NTP server and a summary of their state.

Copy
[ec2-user ~]$ ntpq -p
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
+lttleman.deekay 204.9.54.119     2 u   15  128  377   88.649    5.946   6.876
-bittorrent.tomh 91.189.94.4      3 u  133  128  377  182.673    8.001   1.278
*ntp3.junkemailf 216.218.254.202  2 u   68  128  377   29.377    4.726  11.887
+tesla.selinc.co 149.20.64.28     2 u   31  128  377   28.586   -1.215   1.435
If the output of this command shows no activity, check whether your security groups, network ACLs, or firewalls block access to the NTP port.

To start and enable NTP

Start the NTP service with the following command.

Copy
[ec2-user ~]$ sudo service ntpd start
Starting ntpd:                                             [  OK  ]
Enable NTP to start at boot time with the chkconfig command.

Copy
[ec2-user ~]$ sudo chkconfig ntpd on
Verify that NTP is enabled using the following command.

Copy
[ec2-user ~]$ sudo chkconfig --list ntpd
ntpd           	0:off	1:off	2:on	3:on	4:on	5:on	6:off
Here ntpd is on in runlevels 2, 3, 4, and 5, which is correct.

To change NTP servers

You may decide not to use the standard NTP servers or you may need to use your own NTP server within your private network for instances that do not have Internet access.

Open the /etc/ntp.conf file in your favorite text editor (such as vim or nano). You need to use sudo with the editor command because /etc/ntp.conf is owned by root.

Find the server section, which defines the servers to poll for NTP configuration.

# Use public servers from the pool.ntp.org project.
# Please consider joining the pool (http://www.pool.ntp.org/join.html).
server 0.amazon.pool.ntp.org iburst
server 1.amazon.pool.ntp.org iburst
server 2.amazon.pool.ntp.org iburst
server 3.amazon.pool.ntp.org iburst
Note
The n.amazon.pool.ntp.org DNS records are intended to load balance NTP traffic from AWS. However, these are public NTP servers in the pool.ntp.org project, and they are not owned or managed by AWS. There is no guarantee that they are geographically located near your instances, or even within the AWS network. For more information, see http://www.pool.ntp.org/en/.
Comment out the servers you don't want to use by adding a "#" character to the beginning of those server definitions.

# Use public servers from the pool.ntp.org project.
# Please consider joining the pool (http://www.pool.ntp.org/join.html).
#server 0.amazon.pool.ntp.org iburst
#server 1.amazon.pool.ntp.org iburst
#server 2.amazon.pool.ntp.org iburst
#server 3.amazon.pool.ntp.org iburst
Add an entry for each server to poll for time synchronization. You can use a DNS name for this entry or a dotted quad IP address (such as 10.0.0.254).

Copy
server my-ntp-server.my-domain.com iburst
Restart the NTP service to pick up the new servers.

Copy
[ec2-user ~]$ sudo service ntpd start
Starting ntpd:                                             [  OK  ]
Verify that your new settings work and that NTP is functioning.

Copy
[ec2-user ~]$ ntpstat
synchronised to NTP server (64.246.132.14) at stratum 2
   time correct to within 99 ms

Changing the Hostname of Your Linux Instance

When you launch an instance, it is assigned a hostname that is a form of the private, internal IPv4 address. A typical Amazon EC2 private DNS name looks something like this: ip-12-34-56-78.us-west-2.compute.internal, where the name consists of the internal domain, the service (in this case, compute), the region, and a form of the private IPv4 address. Part of this hostname is displayed at the shell prompt when you log into your instance (for example, ip-12-34-56-78). Each time you stop and restart your Amazon EC2 instance (unless you are using an Elastic IP address), the public IPv4 address changes, and so does your public DNS name, system hostname, and shell prompt. Instances launched into EC2-Classic also receive a new private IPv4 address, private DNS hostname, and system hostname when they're stopped and restarted; instances launched into a VPC don't.

Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
Changing the System Hostname

If you have a public DNS name registered for the IP address of your instance (such as webserver.mydomain.com), you can set the system hostname so your instance identifies itself as a part of that domain. This also changes the shell prompt so that it displays the first portion of this name instead of the hostname supplied by AWS (for example, ip-12-34-56-78). If you do not have a public DNS name registered, you can still change the hostname, but the process is a little different.

To change the system hostname to a public DNS name

Follow this procedure if you already have a public DNS name registered.

On your instance, open the /etc/sysconfig/network configuration file in your favorite text editor and change the HOSTNAME entry to reflect the fully qualified domain name (such as webserver.mydomain.com).

Copy
HOSTNAME=webserver.mydomain.com
Reboot the instance to pick up the new hostname.

Copy
[ec2-user ~]$ sudo reboot
Alternatively, you can reboot using the Amazon EC2 console (on the Instances page, choose Actions, Instance State, Reboot).

Log into your instance and verify that the hostname has been updated. Your prompt should show the new hostname (up to the first ".") and the hostname command should show the fully-qualified domain name.

Copy
[ec2-user@webserver ~]$ hostname
webserver.mydomain.com
To change the system hostname without a public DNS name

Open the /etc/sysconfig/network configuration file in your favorite text editor and change the HOSTNAME entry to reflect the desired system hostname (such as webserver).

Copy
HOSTNAME=webserver.localdomain
Open the /etc/hosts file in your favorite text editor and change the entry beginning with 127.0.0.1 to match the example below, substituting your own hostname.

Copy
127.0.0.1 webserver.localdomain webserver localhost4 localhost4.localdomain4
Reboot the instance to pick up the new hostname.

Copy
[ec2-user ~]$ sudo reboot
Alternatively, you can reboot using the Amazon EC2 console (on the Instances page, choose Actions, Instance State, Reboot).

Log into your instance and verify that the hostname has been updated. Your prompt should show the new hostname (up to the first ".") and the hostname command should show the fully-qualified domain name.

Copy
[ec2-user@webserver ~]$ hostname
webserver.localdomain
Changing the Shell Prompt Without Affecting the Hostname

If you do not want to modify the hostname for your instance, but you would like to have a more useful system name (such as webserver) displayed than the private name supplied by AWS (for example, ip-12-34-56-78), you can edit the shell prompt configuration files to display your system nickname instead of the hostname.

To change the shell prompt to a host nickname

Create a file in /etc/profile.d that sets the environment variable called NICKNAME to the value you want in the shell prompt. For example, to set the system nickname to webserver, run the following command.

Copy
[ec2-user ~]$ sudo sh -c 'echo "export NICKNAME=webserver" > /etc/profile.d/prompt.sh'
Open the /etc/bashrc file in your favorite text editor (such as vim or nano). You need to use sudo with the editor command because /etc/bashrc is owned by root.

Edit the file and change the shell prompt variable (PS1) to display your nickname instead of the hostname. Find the following line that sets the shell prompt in /etc/bashrc (several surrounding lines are shown below for context; look for the line that starts with [ "$PS1"):

  # Turn on checkwinsize
  shopt -s checkwinsize
  [ "$PS1" = "\\s-\\v\\\$ " ] && PS1="[\u@\h \W]\\$ "
  # You might want to have e.g. tty in prompt (e.g. more virtual machines)
  # and console windows
Change the \h (the symbol for hostname) in that line to the value of the NICKNAME variable.

  # Turn on checkwinsize
  shopt -s checkwinsize
  [ "$PS1" = "\\s-\\v\\\$ " ] && PS1="[\u@$NICKNAME \W]\\$ "
  # You might want to have e.g. tty in prompt (e.g. more virtual machines)
  # and console windows
(Optional) To set the title on shell windows to the new nickname, complete the following steps.

Create a file named /etc/sysconfig/bash-prompt-xterm.

Copy
[ec2-user ~]$ sudo touch /etc/sysconfig/bash-prompt-xterm
Make the file executable using the following command.

Copy
[ec2-user ~]$ sudo chmod +x /etc/sysconfig/bash-prompt-xterm
Open the /etc/sysconfig/bash-prompt-xterm file in your favorite text editor (such as vim or nano). You need to use sudo with the editor command because /etc/sysconfig/bash-prompt-xterm is owned by root.

Add the following line to the file.

Copy
echo -ne "\033]0;${USER}@${NICKNAME}:${PWD/#$HOME/~}\007"
Log out and then log back in to pick up the new nickname value.

Changing the Hostname on Other Linux Distributions

The procedures on this page are intended for use with Amazon Linux only. For more information about other Linux distributions, see their specific documentation and the following articles:

How do I assign a static hostname to a private Amazon EC2 instance running RHEL 7 or Centos 7?
How do I assign a static hostname to a private Amazon EC2 instance running SuSe Linux?
How do I assign a static hostname to a private Amazon EC2 instance running Ubuntu Linux?

Setting Up Dynamic DNS on Your Linux Instance

When you launch an EC2 instance, it is assigned a public IP address and a public DNS (Domain Name System) name that you can use to reach it from the Internet. Because there are so many hosts in the Amazon Web Services domain, these public names must be quite long for each name to remain unique. A typical Amazon EC2 public DNS name looks something like this: ec2-12-34-56-78.us-west-2.compute.amazonaws.com, where the name consists of the Amazon Web Services domain, the service (in this case, compute), the region, and a form of the public IP address.

Dynamic DNS services provide custom DNS host names within their domain area that can be easy to remember and that can also be more relevant to your host's use case; some of these services are also free of charge. You can use a dynamic DNS provider with Amazon EC2 and configure the instance to update the IP address associated with a public DNS name each time the instance starts. There are many different providers to choose from, and the specific details of choosing a provider and registering a name with them are outside the scope of this guide.

Important
These procedures are intended for use with Amazon Linux. For more information about other distributions, see their specific documentation.
To use dynamic DNS with Amazon EC2

Sign up with a dynamic DNS service provider and register a public DNS name with their service. This procedure uses the free service from noip.com/free as an example.

Configure the dynamic DNS update client. After you have a dynamic DNS service provider and a public DNS name registered with their service, point the DNS name to the IP address for your instance. Many providers (including noip.com) allow you to do this manually from your account page on their website, but many also support software update clients. If an update client is running on your EC2 instance, your dynamic DNS record is updated each time the IP address changes, as after a shutdown and restart. In this example, you install the noip2 client, which works with the service provided by noip.com.

Enable the Extra Packages for Enterprise Linux (EPEL) repository to gain access to the noip2 client.

Note
Amazon Linux instances have the GPG keys and repository information for the EPEL repository installed by default; however, Red Hat and CentOS instances must first install the epel-release package before you can enable the EPEL repository. For more information and to download the latest version of this package, see https://fedoraproject.org/wiki/EPEL.
Copy
[ec2-user ~]$ sudo yum-config-manager --enable epel
Install the noip package.

Copy
[ec2-user ~]$ sudo yum install -y noip
Create the configuration file. Enter the login and password information when prompted and answer the subsequent questions to configure the client.

Copy
[ec2-user ~]$ sudo noip2 -C
Enable the noip service with the chkconfig command.

Copy
[ec2-user ~]$ sudo chkconfig noip on
You can verify that the service is enabled with the chkconfig --list command.

Copy
[ec2-user ~]$ chkconfig --list noip
noip           	0:off	1:off	2:on	3:on	4:on	5:on	6:off
Here, noip is on in runlevels 2, 3, 4, and 5 (which is correct). Now the update client starts at every boot and updates the public DNS record to point to the IP address of the instance.

Start the noip service.

Copy
[ec2-user ~]$ sudo service noip start
Starting noip2:                                            [  OK  ]
This command starts the client, which reads the configuration file (/etc/no-ip2.conf) that you created earlier and updates the IP address for the public DNS name that you chose.

Verify that the update client has set the correct IP address for your dynamic DNS name. Allow a few minutes for the DNS records to update, and then try to connect to your instance using SSH with the public DNS name that you configured in this procedure.

Running Commands on Your Linux Instance at Launch

When you launch an instance in Amazon EC2, you have the option of passing user data to the instance that can be used to perform common automated configuration tasks and even run scripts after the instance starts. You can pass two types of user data to Amazon EC2: shell scripts and cloud-init directives. You can also pass this data into the launch wizard as plain text, as a file (this is useful for launching instances using the command line tools), or as base64-encoded text (for API calls).

If you are interested in more complex automation scenarios, consider using AWS CloudFormation and AWS OpsWorks. For more information, see the AWS CloudFormation User Guide and the AWS OpsWorks User Guide.

For information about running commands on your Windows instance at launch, see Executing User Data and Managing Windows Instance Configuration in the Amazon EC2 User Guide for Windows Instances.

In the following examples, the commands from the Installing a LAMP Web Server tutorial are converted to a shell script and a set of cloud-init directives that executes when the instance launches. In each example, the following tasks are executed by the user data:

The distribution software packages are updated.
The necessary web server, php, and mysql packages are installed.
The httpd service is started and turned on via chkconfig.
The www group is added, and ec2-user is added to that group.
The appropriate ownership and file permissions are set for the web directory and the files contained within it.
A simple web page is created to test the web server and PHP engine.
By default, user data and cloud-init directives only run during the first boot cycle when you launch an instance. However, AWS Marketplace vendors and owners of third-party AMIs may have made their own customizations for how and when scripts run.

Contents

Prerequisites
User Data and Shell Scripts
User Data and cloud-init Directives
User Data and the AWS CLI
Prerequisites

The following examples assume that your instance has a public DNS name that is reachable from the Internet. For more information, see Step 1: Launch an Instance. You must also configure your security group to allow SSH (port 22), HTTP (port 80), and HTTPS (port 443) connections. For more information about these prerequisites, see Setting Up with Amazon EC2.

Also, these instructions are intended for use with Amazon Linux, and the commands and directives may not work for other Linux distributions. For more information about other distributions, such as their support for cloud-init, see their specific documentation.

User Data and Shell Scripts

If you are familiar with shell scripting, this is the easiest and most complete way to send instructions to an instance at launch, and the cloud-init output log file (/var/log/cloud-init-output.log) captures console output so it is easy to debug your scripts following a launch if the instance does not behave the way you intended.

Important
User data scripts and cloud-init directives only run during the first boot cycle when an instance is launched.
User data shell scripts must start with the #! characters and the path to the interpreter you want to read the script (commonly /bin/bash). For a great introduction on shell scripting, see the BASH Programming HOW-TO at the Linux Documentation Project (tldp.org).

Scripts entered as user data are executed as the root user, so do not use the sudo command in the script. Remember that any files you create will be owned by root; if you need non-root users to have file access, you should modify the permissions accordingly in the script. Also, because the script is not run interactively, you cannot include commands that require user feedback (such as yum update without the -y flag).

Adding these tasks at boot time adds to the amount of time it takes to boot the instance. You should allow a few minutes of extra time for the tasks to complete before you test that the user script has finished successfully.

To pass a shell script to an instance with user data

Follow the procedure for launching an instance at Launching Your Instance from an AMI, but when you get to Step 6, paste the user data script text into the User data field and then complete the launch procedure. For the example below, the script creates and configures our web server.

Copy
#!/bin/bash
yum update -y
yum install -y httpd24 php56 mysql55-server php56-mysqlnd
service httpd start
chkconfig httpd on
groupadd www
usermod -a -G www ec2-user
chown -R root:www /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} +
find /var/www -type f -exec chmod 0664 {} +
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
Allow enough time for the instance to launch and execute the commands in your script, and then check to see that your script has completed the tasks that you intended. For our example, in a web browser, enter the URL of the PHP test file the script created. This URL is the public DNS address of your instance followed by a forward slash and the file name.

http://my.public.dns.amazonaws.com/phpinfo.php
You should see the PHP information page. If you are unable to see the PHP information page, check that the security group you are using contains a rule to allow HTTP (port 80) traffic. For more information, see Adding Rules to a Security Group.

(Optional) If your script did not accomplish the tasks you were expecting it to, or if you just want to verify that your script completed without errors, examine the cloud-init output log file at /var/log/cloud-init-output.log and look for error messages in the output.

For additional debugging information, you can create a Mime multipart archive that includes a cloud-init data section with the following directive:

Copy
output : { all : '| tee -a /var/log/cloud-init-output.log' }
This directive sends command output from your script to /var/log/cloud-init-output.log. For more information about cloud-init data formats and creating Mime multi part archive, see cloud-init Formats.

User Data and cloud-init Directives

The cloud-init package configures specific aspects of a new Amazon Linux instance when it is launched; most notably, it configures the .ssh/authorized_keys file for the ec2-user so you can log in with your own private key. For more information, see cloud-init.

The cloud-init user directives can be passed to an instance at launch the same way that a script is passed, although the syntax is different. For more information about cloud-init, go to http://cloudinit.readthedocs.org/en/latest/index.html.

Important
User data scripts and cloud-init directives only run during the first boot cycle when an instance is launched.
The Amazon Linux version of cloud-init does not support all of the directives that are available in the base package, and some of the directives have been renamed (such as repo_update instead of apt-upgrade).

Adding these tasks at boot time adds to the amount of time it takes to boot an instance. You should allow a few minutes of extra time for the tasks to complete before you test that your user data directives have completed.

To pass cloud-init directives to an instance with user data

Follow the procedure for launching an instance at Launching Your Instance from an AMI, but when you get to Step 6, paste your cloud-init directive text into the User data field and then complete the launch procedure. For the example below, the directives create and configure a web server.

Copy
#cloud-config
repo_update: true
repo_upgrade: all

packages:
 - httpd24
 - php56
 - mysql55-server
 - php56-mysqlnd

runcmd:
 - service httpd start
 - chkconfig httpd on
 - groupadd www
 - [ sh, -c, "usermod -a -G www ec2-user" ]
 - [ sh, -c, "chown -R root:www /var/www" ]
 - chmod 2775 /var/www
 - [ find, /var/www, -type, d, -exec, chmod, 2775, {}, + ]
 - [ find, /var/www, -type, f, -exec, chmod, 0664, {}, + ]
 - [ sh, -c, 'echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php' ]
Allow enough time for the instance to launch and execute the directives in your user data, and then check to see that your directives have completed the tasks you intended. For our example, in a web browser, enter the URL of the PHP test file the directives created. This URL is the public DNS address of your instance followed by a forward slash and the file name.

http://my.public.dns.amazonaws.com/phpinfo.php
You should see the PHP information page. If you are unable to see the PHP information page, check that the security group you are using contains a rule to allow HTTP (port 80) traffic. For more information, see Adding Rules to a Security Group.

(Optional) If your directives did not accomplish the tasks you were expecting them to, or if you just want to verify that your directives completed without errors, examine the output log file at /var/log/cloud-init-output.log and look for error messages in the output. For additional debugging information, you can add the following line to your directives:

Copy
output : { all : '| tee -a /var/log/cloud-init-output.log' }
This directive sends runcmd output to /var/log/cloud-init-output.log.

User Data and the AWS CLI

You can use the AWS CLI to specify, modify, and view the user data for your instance. For information about viewing user data from your instance using instance metadata, see Retrieving User Data.

On Windows, you can use the AWS Tools for Windows PowerShell instead of using the AWS CLI. For more information, see User Data and the Tools for Windows PowerShell in the Amazon EC2 User Guide for Windows Instances.

Example: Specify User Data at Launch

To specify user data when you launch your instance, use the run-instances command with the --user-data parameter. With run-instances, the AWS CLI performs base64 encoding of the user data for you.

The following example shows how to specify a script as a string on the command line:

Copy
aws ec2 run-instances --image-id ami-abcd1234 --count 1 --instance-type m3.medium \
--key-name my-key-pair --subnet-id subnet-abcd1234 --security-group-ids sg-abcd1234 \
--user-data echo user data
The following example shows how to specify a script using a text file. Be sure to use the file:// prefix to specify the file.

Copy
aws ec2 run-instances --image-id ami-abcd1234 --count 1 --instance-type m3.medium \
--key-name my-key-pair --subnet-id subnet-abcd1234 --security-group-ids sg-abcd1234 \
--user-data file://my_script.txt
The following is an example text file with a shell script.

Copy
#!/bin/bash
yum update -y
service httpd start
chkconfig httpd on
Example: Modify the User Data of a Stopped Instance

You can modify the user data of a stopped instance using the modify-instance-attribute command. With modify-instance-attribute, the AWS CLI does not perform base64 encoding of the user data for you.

On Linux, use the base64 command to encode the user data.

Copy
base64 my_script.txt >my_script_base64.txt
On Windows, use the certutil command to encode the user data. Before you can use this file with the AWS CLI, you must remove the first (BEGIN CERTIFICATE) and last (END CERTIFICATE) lines.

Copy
certutil -encode my_script.txt my_script_base64.txt
notepad my_script_base64.txt
Use the --user-data and --value parameters to use the encoded text file to specify the user data. Be sure to use the file:// prefix to specify the file.

Copy
aws ec2 modify-instance-attribute --instance-id i-1234567890abcdef0 --attribute userData --value file://my_script_base64.txt
Example: View User Data

To retrieve the user data for an instance, use the describe-instance-attribute command. With describe-instance-attribute, the AWS CLI does not perform base64 decoding of the user data for you.

Copy
aws ec2 describe-instance-attribute --instance-id i-1234567890abcdef0 --attribute userData
The following is example output with the user data base64 encoded.

{
    "UserData": {
        "Value": "IyEvYmluL2Jhc2gKeXVtIHVwZGF0ZSAteQpzZXJ2aWNlIGh0dHBkIHN0YXJ0CmNoa2NvbmZpZyBodHRwZCBvbg=="
    },
    "InstanceId": "i-1234567890abcdef0"
}
On Linux, use the --query option to get the encoded user data and the base64 command to decode it.

Copy
aws ec2 describe-instance-attribute --instance-id i-1234567890abcdef0 --attribute userData --output text --query "UserData.Value" | base64 --decode
On Windows, use the --query option to get the coded user data and the certutil command to decode it. Note that the encoded output is stored in a file and the decoded output is stored in another file.

Copy
aws ec2 describe-instance-attribute --instance-id i-1234567890abcdef0 --attribute userData --output text --query "UserData.Value" >my_output.txt
certutil -decode my_output.txt my_output_decoded.txt
type my_output_decoded.txt
The following is example output.

#!/bin/bash
yum update -y
service httpd start
chkconfig httpd on

Instance Metadata and User Data

Instance metadata is data about your instance that you can use to configure or manage the running instance. Instance metadata is divided into categories. For more information, see Instance Metadata Categories.

Important
Although you can only access instance metadata and user data from within the instance itself, the data is not protected by cryptographic methods. Anyone who can access the instance can view its metadata. Therefore, you should take suitable precautions to protect sensitive data (such as long-lived encryption keys). You should not store sensitive data, such as passwords, as user data.
You can also use instance metadata to access user data that you specified when launching your instance. For example, you can specify parameters for configuring your instance, or attach a simple script. You can also use this data to build more generic AMIs that can be modified by configuration files supplied at launch time. For example, if you run web servers for various small businesses, they can all use the same AMI and retrieve their content from the Amazon S3 bucket you specify in the user data at launch. To add a new customer at any time, simply create a bucket for the customer, add their content, and launch your AMI. If you launch more than one instance at the same time, the user data is available to all instances in that reservation.

EC2 instances can also include dynamic data, such as an instance identity document that is generated when the instance is launched. For more information, see Dynamic Data Categories.

Contents

Retrieving Instance Metadata
Configuring Instances with User Data
Retrieving User Data
Retrieving Dynamic Data
Example: AMI Launch Index Value
Instance Metadata Categories
Instance Identity Documents
Retrieving Instance Metadata

Because your instance metadata is available from your running instance, you do not need to use the Amazon EC2 console or the AWS CLI. This can be helpful when you're writing scripts to run from your instance. For example, you can access the local IP address of your instance from instance metadata to manage a connection to an external application.

To view all categories of instance metadata from within a running instance, use the following URI:

http://169.254.169.254/latest/meta-data/
Note that you are not billed for HTTP requests used to retrieve instance metadata and user data.

You can use a tool such as cURL, or if your instance supports it, the GET command; for example:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/
Copy
[ec2-user ~]$ GET http://169.254.169.254/latest/meta-data/
You can also download the Instance Metadata Query tool, which allows you to query the instance metadata without having to type out the full URI or category names.

All instance metadata is returned as text (content type text/plain). A request for a specific metadata resource returns the appropriate value, or a 404 - Not Found HTTP error code if the resource is not available.

A request for a general metadata resource (the URI ends with a /) returns a list of available resources, or a 404 - Not Found HTTP error code if there is no such resource. The list items are on separate lines, terminated by line feeds (ASCII 10).

Examples of Retrieving Instance Metadata

This example gets the available versions of the instance metadata. These versions do not necessarily correlate with an Amazon EC2 API version. The earlier versions are available to you in case you have scripts that rely on the structure and information present in a previous version.

Copy
[ec2-user ~]$ curl http://169.254.169.254/
1.0
2007-01-19
2007-03-01
2007-08-29
2007-10-10
2007-12-15
2008-02-01
2008-09-01
2009-04-04
2011-01-01
2011-05-01
2012-01-12
2014-02-25
2014-11-05
2015-10-20
2016-04-19
2016-06-30
2016-09-02
latest
This example gets the top-level metadata items. Some items are only available for instances in a VPC. For more information about each of these items, see Instance Metadata Categories.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/    
ami-id
ami-launch-index
ami-manifest-path
block-device-mapping/
hostname
iam/
instance-action
instance-id
instance-type
local-hostname
local-ipv4
mac
metrics/
network/
placement/
profile
public-hostname
public-ipv4
public-keys/
reservation-id
security-groups
services/
These examples get the value of some of the metadata items from the preceding example.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/ami-id
ami-12345678
Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/reservation-id
r-fea54097
Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/local-hostname
ip-10-251-50-12.ec2.internal
Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/public-hostname
ec2-203-0-113-25.compute-1.amazonaws.com
This example gets the list of available public keys.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/public-keys/
0=my-public-key
This example shows the formats in which public key 0 is available.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/public-keys/0/
openssh-key
This example gets public key 0 (in the OpenSSH key format).

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key
ssh-rsa MIICiTCCAfICCQD6m7oRw0uXOjANBgkqhkiG9w0BAQUFADCBiDELMAkGA1UEBhMC
VVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdTZWF0dGxlMQ8wDQYDVQQKEwZBbWF6
b24xFDASBgNVBAsTC0lBTSBDb25zb2xlMRIwEAYDVQQDEwlUZXN0Q2lsYWMxHzAd
BgkqhkiG9w0BCQEWEG5vb25lQGFtYXpvbi5jb20wHhcNMTEwNDI1MjA0NTIxWhcN
MTIwNDI0MjA0NTIxWjCBiDELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAldBMRAwDgYD
VQQHEwdTZWF0dGxlMQ8wDQYDVQQKEwZBbWF6b24xFDASBgNVBAsTC0lBTSBDb25z
b2xlMRIwEAYDVQQDEwlUZXN0Q2lsYWMxHzAdBgkqhkiG9w0BCQEWEG5vb25lQGFt
YXpvbi5jb20wgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMaK0dn+a4GmWIWJ
21uUSfwfEvySWtC2XADZ4nB+BLYgVIk60CpiwsZ3G93vUEIO3IyNoH/f0wYK8m9T
rDHudUZg3qX4waLG5M43q7Wgc/MbQITxOUSQv7c7ugFFDzQGBzZswY6786m86gpE
Ibb3OhjZnzcvQAaRHhdlQWIMm2nrAgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAtCu4
nUhVVxYUntneD9+h8Mg9q6q+auNKyExzyLwaxlAoo7TJHidbtS4J5iNmZgXL0Fkb
FFBjvSfpJIlJ00zbhNYS5f6GuoEDmFJl0ZxBHjJnyp378OD8uTs7fLvjx79LjSTb
NYiytVbZPQUQ5Yaxu2jXnimvw3rrszlaEXAMPLE my-public-key
This example shows the information available for a specific network interface (indicated by the MAC address) on an NAT instance in the EC2-Classic platform.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/02:29:96:8f:6a:2d/
device-number
local-hostname
local-ipv4s
mac
owner-id
public-hostname
public-ipv4s
This example gets the subnet ID for an instance launched into a VPC.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/02:29:96:8f:6a:2d/subnet-id
subnet-be9b61d7
Throttling

We throttle queries to the instance metadata service on a per-instance basis, and we place limits on the number of simultaneous connections from an instance to the instance metadata service.

If you're using the instance metadata service to retrieve AWS security credentials, avoid querying for credentials during every transaction or concurrently from a high number of threads or processes, as this may lead to throttling. Instead, we recommend that you cache the credentials until they start approaching their expiry time.

If you're throttled while accessing the instance metadata service, retry your query with an exponential backoff strategy.

Configuring Instances with User Data

When you specify user data, note the following:

User data is treated as opaque data: what you give is what you get back. It is up to the instance to be able to interpret it.
User data is limited to 16 KB. This limit applies to the data in raw form, not base64-encoded form.
User data must be base64-encoded. The Amazon EC2 console can perform the base64 encoding for you or accept base64-encoded input.
User data must be decoded when you retrieve it. The data is decoded when you retrieve it using instance metadata and the console.
User data is executed only at launch. If you stop an instance, modify the user data, and start the instance, the new user data is not executed automatically.
Specify User Data at Launch

You can specify user data when you launch an instance. For more information, see Launching an Instance, cloud-init, and Running Commands on Your Linux Instance at Launch.

Modify User Data for a Running Instance

You can modify user data for an existing instance if the root volume is an EBS volume. If the instance is running, you must first stop the instance. The new user data is visible on your instance after you restart it; however, it is not executed.

Warning
When you stop an instance, the data on any instance store volumes is erased. Therefore, if you have any data on instance store volumes that you want to keep, be sure to back it up to persistent storage.
To modify the user data for an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances, and select the instance.

Choose Actions, Instance State, Stop.

In the confirmation dialog box, click Yes, Stop. It can take a few minutes for the instance to stop.

With the instance still selected, choose Actions, select Instance Settings, and then choose View/Change User Data. Note that you can't change the user data if the instance is running, but you can view it.

In the View/Change User Data dialog box, update the user data, and then choose Save.

To modify the user data for an instance using the command line

You can modify user data using the AWS CLI and the Tools for Windows PowerShell. For more information, see User Data and the AWS CLI and User Data and the Tools for Windows PowerShell.

Retrieving User Data

To retrieve user data from within a running instance, use the following URI:

http://169.254.169.254/latest/user-data
Requests for user data returns the data as it is (content type application/octet-stream).

This example returns comma-separated user data.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/user-data
1234,john,reboot,true | 4512,richard, | 173,,,
This example returns line-separated user data.

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/user-data
[general]
instances: 4

[instance-0]
s3-bucket: <user_name>

[instance-1]
reboot-on-error: yes
Retrieving Dynamic Data

To retrieve dynamic data from within a running instance, use the following URI:

http://169.254.169.254/latest/dynamic/
This example shows how to retrieve the high-level instance identity categories:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/dynamic/instance-identity/
rsa2048
pkcs7
document
signature
dsa2048
For more information about dynamic data and examples of how to retrieve it, see Instance Identity Documents.

Example: AMI Launch Index Value

This example demonstrates how you can use both user data and instance metadata to configure your instances.

Alice wants to launch four instances of her favorite database AMI, with the first acting as master and the remaining three acting as replicas. When she launches them, she wants to add user data about the replication strategy for each replicant. She is aware that this data will be available to all four instances, so she needs to structure the user data in a way that allows each instance to recognize which parts are applicable to it. She can do this using the ami-launch-index instance metadata value, which will be unique for each instance.

Here is the user data that Alice has constructed:

replicate-every=1min | replicate-every=5min | replicate-every=10min
The replicate-every=1min data defines the first replicant's configuration, replicate-every=5min defines the second replicant's configuration, and so on. Alice decides to provide this data as an ASCII string with a pipe symbol (|) delimiting the data for the separate instances.

Alice launches four instances using the run-instances command, specifying the user data:

Copy
aws ec2 run-instances --image-id ami-12345678 --count 4 --instance-type t2.micro --user-data "replicate-every=1min | replicate-every=5min | replicate-every=10min"
After they're launched, all instances have a copy of the user data and the common metadata shown here:

AMI id: ami-12345678
Reservation ID: r-1234567890abcabc0
Public keys: none
Security group name: default
Instance type: t2.micro
However, each instance has certain unique metadata.

Instance 1

Metadata	Value
instance-id	i-1234567890abcdef0
ami-launch-index	0
public-hostname	ec2-203-0-113-25.compute-1.amazonaws.com
public-ipv4	67.202.51.223
local-hostname	ip-10-251-50-12.ec2.internal
local-ipv4	10.251.50.35
Instance 2

Metadata	Value
instance-id	i-0598c7d356eba48d7
ami-launch-index	1
public-hostname	ec2-67-202-51-224.compute-1.amazonaws.com
public-ipv4	67.202.51.224
local-hostname	ip-10-251-50-36.ec2.internal
local-ipv4	10.251.50.36
Instance 3

Metadata	Value
instance-id	i-0ee992212549ce0e7
ami-launch-index	2
public-hostname	ec2-67-202-51-225.compute-1.amazonaws.com
public-ipv4	67.202.51.225
local-hostname	ip-10-251-50-37.ec2.internal
local-ipv4	10.251.50.37
Instance 4

Metadata	Value
instance-id	i-1234567890abcdef0
ami-launch-index	3
public-hostname	ec2-67-202-51-226.compute-1.amazonaws.com
public-ipv4	67.202.51.226
local-hostname	ip-10-251-50-38.ec2.internal
local-ipv4	10.251.50.38
Alice can use the ami-launch-index value to determine which portion of the user data is applicable to a particular instance.

She connects to one of the instances, and retrieves the ami-launch-index for that instance to ensure it is one of the replicants:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/ami-launch-index
2
She saves the ami-launch-index as a variable:

Copy
[ec2-user ~]$ ami_launch_index=`curl http://169.254.169.254/latest/meta-data/ami-launch-index`
She saves the user data as a variable:

Copy
[ec2-user ~]$ user_data=`curl http://169.254.169.254/latest/user-data/`
Finally, Alice uses the cut command to extract the portion of the user data that is applicable to that instance:

Copy
[ec2-user ~]$ echo $user_data | cut -d"|" -f"$ami_launch_index"
replicate-every=5min
Instance Metadata Categories

The following table lists the categories of instance metadata.

Important
Category names that are formatted in red text are placeholders for data that is unique to your instance; for example, mac represents the MAC address for the network interface. You must replace the placeholders with the actual values.
Data	Description	Version Introduced
ami-id	The AMI ID used to launch the instance.	1.0
ami-launch-index	If you started more than one instance at the same time, this value indicates the order in which the instance was launched. The value of the first instance launched is 0.	1.0
ami-manifest-path	The path to the AMI manifest file in Amazon S3. If you used an Amazon EBS-backed AMI to launch the instance, the returned result is unknown.	1.0
ancestor-ami-ids	The AMI IDs of any instances that were rebundled to create this AMI. This value will only exist if the AMI manifest file contained an ancestor-amis key.	2007-10-10
block-device-mapping/ami	The virtual device that contains the root/boot file system.	2007-12-15
block-device-mapping/ebsN	The virtual devices associated with Amazon EBS volumes, if any are present. Amazon EBS volumes are only available in metadata if they were present at launch time or when the instance was last started. The N indicates the index of the Amazon EBS volume (such as ebs1 or ebs2).	2007-12-15
block-device-mapping/ephemeralN	The virtual devices associated with ephemeral devices, if any are present. The N indicates the index of the ephemeral volume.	2007-12-15
block-device-mapping/root	The virtual devices or partitions associated with the root devices, or partitions on the virtual device, where the root (/ or C:) file system is associated with the given instance.	2007-12-15
block-device-mapping/swap	The virtual devices associated with swap. Not always present.	2007-12-15
elastic-gpus/associations/elastic-gpu-id	If there is an Elastic GPU attached to the instance, contains a JSON string with information about the Elastic GPU, including its ID and connection information.	2016-11-30
hostname	The private IPv4 DNS hostname of the instance. In cases where multiple network interfaces are present, this refers to the eth0 device (the device for which the device number is 0).	1.0
iam/info	If there is an IAM role associated with the instance, contains information about the last time the instance profile was updated, including the instance's LastUpdated date, InstanceProfileArn, and InstanceProfileId. Otherwise, not present.	2012-01-12
iam/security-credentials/role-name	If there is an IAM role associated with the instance, role-name is the name of the role, and role-name contains the temporary security credentials associated with the role (for more information, see Retrieving Security Credentials from Instance Metadata). Otherwise, not present.	2012-01-12
instance-action	Notifies the instance that it should reboot in preparation for bundling. Valid values: none | shutdown | bundle-pending.	2008-09-01
instance-id	The ID of this instance.	1.0
instance-type	The type of instance. For more information, see Instance Types.	2007-08-29
kernel-id	The ID of the kernel launched with this instance, if applicable.	2008-02-01
local-hostname	The private IPv4 DNS hostname of the instance. In cases where multiple network interfaces are present, this refers to the eth0 device (the device for which the device number is 0).	2007-01-19
local-ipv4	The private IPv4 address of the instance. In cases where multiple network interfaces are present, this refers to the eth0 device (the device for which the device number is 0).	1.0
mac	The instance's media access control (MAC) address. In cases where multiple network interfaces are present, this refers to the eth0 device (the device for which the device number is 0).	2011-01-01
network/interfaces/macs/mac/device-number	The unique device number associated with that interface. The device number corresponds to the device name; for example, a device-number of 2 is for the eth2 device. This category corresponds to the DeviceIndex and device-index fields that are used by the Amazon EC2 API and the EC2 commands for the AWS CLI.	2011-01-01
network/interfaces/macs/mac/ipv4-associations/public-ip	The private IPv4 addresses that are associated with each public-ip address and assigned to that interface.	2011-01-01
network/interfaces/macs/mac/ipv6s	The IPv6 addresses associated with the interface. Returned only for instances launched into a VPC.	2016-06-30
network/interfaces/macs/mac/local-hostname	The interface's local hostname.	2011-01-01
network/interfaces/macs/mac/local-ipv4s	The private IPv4 addresses associated with the interface.	2011-01-01
network/interfaces/macs/mac/mac	The instance's MAC address.	2011-01-01
network/interfaces/macs/mac/owner-id	The ID of the owner of the network interface. In multiple-interface environments, an interface can be attached by a third party, such as Elastic Load Balancing. Traffic on an interface is always billed to the interface owner.	2011-01-01
network/interfaces/macs/mac/public-hostname	The interface's public DNS (IPv4). If the instance is in a VPC, this category is only returned if the enableDnsHostnames attribute is set to true. For more information, see Using DNS with Your VPC.	2011-01-01
network/interfaces/macs/mac/public-ipv4s	The Elastic IP addresses associated with the interface. There may be multiple IPv4 addresses on an instance.	2011-01-01
network/interfaces/macs/mac/security-groups	Security groups to which the network interface belongs. Returned only for instances launched into a VPC.	2011-01-01
network/interfaces/macs/mac/security-group-ids	The IDs of the security groups to which the network interface belongs. Returned only for instances launched into a VPC. For more information on security groups in the EC2-VPC platform, see Security Groups for Your VPC.	2011-01-01
network/interfaces/macs/mac/subnet-id	The ID of the subnet in which the interface resides. Returned only for instances launched into a VPC.	2011-01-01
network/interfaces/macs/mac/subnet-ipv4-cidr-block	The IPv4 CIDR block of the subnet in which the interface resides. Returned only for instances launched into a VPC.	2011-01-01
network/interfaces/macs/mac/subnet-ipv6-cidr-blocks	The IPv6 CIDR block of the subnet in which the interface resides. Returned only for instances launched into a VPC.	2016-06-30
network/interfaces/macs/mac/vpc-id	The ID of the VPC in which the interface resides. Returned only for instances launched into a VPC.	2011-01-01
network/interfaces/macs/mac/vpc-ipv4-cidr-block	The primary IPv4 CIDR block of the VPC. Returned only for instances launched into a VPC.	2011-01-01
network/interfaces/macs/mac/vpc-ipv4-cidr-blocks	The IPv4 CIDR blocks for the VPC. Returned only for instances launched into a VPC.	2016-06-30
network/interfaces/macs/mac/vpc-ipv6-cidr-blocks	The IPv6 CIDR block of the VPC in which the interface resides. Returned only for instances launched into a VPC.	2016-06-30
placement/availability-zone	The Availability Zone in which the instance launched.	2008-02-01
product-codes	Product codes associated with the instance, if any.	2007-03-01
public-hostname	The instance's public DNS. If the instance is in a VPC, this category is only returned if the enableDnsHostnames attribute is set to true. For more information, see Using DNS with Your VPC.	2007-01-19
public-ipv4	The public IPv4 address. If an Elastic IP address is associated with the instance, the value returned is the Elastic IP address.	2007-01-19
public-keys/0/openssh-key	Public key. Only available if supplied at instance launch time.	1.0
ramdisk-id	The ID of the RAM disk specified at launch time, if applicable.	2007-10-10
reservation-id	The ID of the reservation.	1.0
security-groups	
The names of the security groups applied to the instance.

After launch, you can only change the security groups of instances running in a VPC. Such changes are reflected here and in network/interfaces/macs/mac/security-groups.
1.0
services/domain	
The domain for AWS resources for the region; for example, amazonaws.com for us-east-1.
2014-02-25
services/partition	
The partition that the resource is in. For standard AWS regions, the partition is aws. If you have resources in other partitions, the partition is aws-partitionname. For example, the partition for resources in the China (Beijing) region is aws-cn.
2015-10-20
spot/termination-time	
The approximate time, in UTC, that the operating system for your Spot instance will receive the shutdown signal. This item is present and contains a time value (for example, 2015-01-05T18:02:00Z) only if the Spot instance has been marked for termination by Amazon EC2. The termination-time item is not set to a time if you terminated the Spot instance yourself.
2014-11-05
Dynamic Data Categories

The following table lists the categories of dynamic data.

Data	Description	Version introduced
fws/instance-monitoring	Value showing whether the customer has enabled detailed one-minute monitoring in CloudWatch. Valid values: enabled | disabled	2009-04-04
instance-identity/document	JSON containing instance attributes, such as instance-id, private IP address, etc. See Instance Identity Documents.	2009-04-04
instance-identity/pkcs7	Used to verify the document's authenticity and content against the signature. See Instance Identity Documents.	2009-04-04
instance-identity/signature	Data that can be used by other parties to verify its origin and authenticity. See Instance Identity Documents.

Instance Identity Documents

An instance identity document is a JSON file that describes an instance. The instance identity document is accompanied by a signature and a PKCS7 signature which can be used to verify the accuracy, origin, and authenticity of the information provided in the document. For example, you may have downloaded free software with paid updates.

The instance identity document is generated when the instance is launched, and exposed to the instance through instance metadata. It validates the attributes of the instances, such as the subscribed software, instance size, instance type, operating system, and AMI.

Important
Due to the dynamic nature of instance identity documents and signatures, we recommend retrieving the instance identity document and signature regularly.
Obtaining the Instance Identity Document and Signatures

To retrieve the instance identity document, use the following command from your running instance:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/dynamic/instance-identity/document
The following is example output:

{
    "devpayProductCodes" : null,
    "availabilityZone" : "us-west-2b",
    "privateIp" : "10.158.112.84",
    "version" : "2010-08-31",
    "instanceId" : "i-1234567890abcdef0",
    "billingProducts" : null,
    "instanceType" : "t2.micro",
    "accountId" : "123456789012",
    "imageId" : "ami-5fb8c835",
    "pendingTime" : "2016-11-19T16:32:11Z",
    "architecture" : "x86_64",
    "kernelId" : null,
    "ramdiskId" : null,
    "region" : "us-west-2"
}
To retrieve the instance identity signature, use the following command from your running instance:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/dynamic/instance-identity/signature
The following is example output:

dExamplesjNQhhJan7pORLpLSr7lJEF4V2DhKGlyoYVBoUYrY9njyBCmhEayaGrhtS/AWY+LPx
lVSQURF5n0gwPNCuO6ICT0fNrm5IH7w9ydyaexamplejJw8XvWPxbuRkcN0TAA1p4RtCAqm4ms
x2oALjWSCBExample=
To retrieve the PKCS7 signature, use the following command from your running instance:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/dynamic/instance-identity/pkcs7
The following is example output:

MIICiTCCAfICCQD6m7oRw0uXOjANBgkqhkiG9w0BAQUFADCBiDELMAkGA1UEBhMC
VVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdTZWF0dGxlMQ8wDQYDVQQKEwZBbWF6
b24xFDASBgNVBAsTC0lBTSBDb25zb2xlMRIwEAYDVQQDEwlUZXN0Q2lsYWMxHzAd
BgkqhkiG9w0BCQEWEG5vb25lQGFtYXpvbi5jb20wHhcNMTEwNDI1MjA0NTIxWhcN
MTIwNDI0MjA0NTIxWjCBiDELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAldBMRAwDgYD
VQQHEwdTZWF0dGxlMQ8wDQYDVQQKEwZBbWF6b24xFDASBgNVBAsTC0lBTSBDb25z
b2xlMRIwEAYDVQQDEwlUZXN0Q2lsYWMxHzAdBgkqhkiG9w0BCQEWEG5vb25lQGFt
YXpvbi5jb20wgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMaK0dn+a4GmWIWJ
21uUSfwfEvySWtC2XADZ4nB+BLYgVIk60CpiwsZ3G93vUEIO3IyNoH/f0wYK8m9T
rDHudUZg3qX4waLG5M43q7Wgc/MbQITxOUSQv7c7ugFFDzQGBzZswY6786m86gpE
Ibb3OhjZnzcvQAaRHhdlQWIMm2nrAgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAtCu4
nUhVVxYUntneD9+h8Mg9q6q+auNKyExzyLwaxlAoo7TJHidbtS4J5iNmZgXL0Fkb
FFBjvSfpJIlJ00zbhNYS5f6GuoEDmFJl0ZxBHjJnyp378OD8uTs7fLvjx79LjSTb
NYiytVbZPQUQ5Yaxu2jXnimvw3rrszlaEXAMPLE
Verifying the PKCS7 Signature

You can use the PKCS7 signature to verify your instance by validating it against the appropriate AWS public certificate.

The AWS public certificate for the regions provided by an AWS account is as follows:

Copy
-----BEGIN CERTIFICATE-----
MIIC7TCCAq0CCQCWukjZ5V4aZzAJBgcqhkjOOAQDMFwxCzAJBgNVBAYTAlVTMRkw
FwYDVQQIExBXYXNoaW5ndG9uIFN0YXRlMRAwDgYDVQQHEwdTZWF0dGxlMSAwHgYD
VQQKExdBbWF6b24gV2ViIFNlcnZpY2VzIExMQzAeFw0xMjAxMDUxMjU2MTJaFw0z
ODAxMDUxMjU2MTJaMFwxCzAJBgNVBAYTAlVTMRkwFwYDVQQIExBXYXNoaW5ndG9u
IFN0YXRlMRAwDgYDVQQHEwdTZWF0dGxlMSAwHgYDVQQKExdBbWF6b24gV2ViIFNl
cnZpY2VzIExMQzCCAbcwggEsBgcqhkjOOAQBMIIBHwKBgQCjkvcS2bb1VQ4yt/5e
ih5OO6kK/n1Lzllr7D8ZwtQP8fOEpp5E2ng+D6Ud1Z1gYipr58Kj3nssSNpI6bX3
VyIQzK7wLclnd/YozqNNmgIyZecN7EglK9ITHJLP+x8FtUpt3QbyYXJdmVMegN6P
hviYt5JH/nYl4hh3Pa1HJdskgQIVALVJ3ER11+Ko4tP6nwvHwh6+ERYRAoGBAI1j
k+tkqMVHuAFcvAGKocTgsjJem6/5qomzJuKDmbJNu9Qxw3rAotXau8Qe+MBcJl/U
hhy1KHVpCGl9fueQ2s6IL0CaO/buycU1CiYQk40KNHCcHfNiZbdlx1E9rpUp7bnF
lRa2v1ntMX3caRVDdbtPEWmdxSCYsYFDk4mZrOLBA4GEAAKBgEbmeve5f8LIE/Gf
MNmP9CM5eovQOGx5ho8WqD+aTebs+k2tn92BBPqeZqpWRa5P/+jrdKml1qx4llHW
MXrs3IgIb6+hUIB+S8dz8/mmO0bpr76RoZVCXYab2CZedFut7qc3WUH9+EUAH5mw
vSeDCOUMYQR7R9LINYwouHIziqQYMAkGByqGSM44BAMDLwAwLAIUWXBlk40xTwSw
7HX32MxXYruse9ACFBNGmdX2ZBrVNGrN9N2f6ROk0k9K
-----END CERTIFICATE-----
The AWS public certificate for the AWS GovCloud (US) region is as follows:

Copy
-----BEGIN CERTIFICATE-----
MIIC7TCCAq0CCQCWukjZ5V4aZzAJBgcqhkjOOAQDMFwxCzAJBgNVBAYTAlVTMRkw
FwYDVQQIExBXYXNoaW5ndG9uIFN0YXRlMRAwDgYDVQQHEwdTZWF0dGxlMSAwHgYD
VQQKExdBbWF6b24gV2ViIFNlcnZpY2VzIExMQzAeFw0xMjAxMDUxMjU2MTJaFw0z
ODAxMDUxMjU2MTJaMFwxCzAJBgNVBAYTAlVTMRkwFwYDVQQIExBXYXNoaW5ndG9u
IFN0YXRlMRAwDgYDVQQHEwdTZWF0dGxlMSAwHgYDVQQKExdBbWF6b24gV2ViIFNl
cnZpY2VzIExMQzCCAbcwggEsBgcqhkjOOAQBMIIBHwKBgQCjkvcS2bb1VQ4yt/5e
ih5OO6kK/n1Lzllr7D8ZwtQP8fOEpp5E2ng+D6Ud1Z1gYipr58Kj3nssSNpI6bX3
VyIQzK7wLclnd/YozqNNmgIyZecN7EglK9ITHJLP+x8FtUpt3QbyYXJdmVMegN6P
hviYt5JH/nYl4hh3Pa1HJdskgQIVALVJ3ER11+Ko4tP6nwvHwh6+ERYRAoGBAI1j
k+tkqMVHuAFcvAGKocTgsjJem6/5qomzJuKDmbJNu9Qxw3rAotXau8Qe+MBcJl/U
hhy1KHVpCGl9fueQ2s6IL0CaO/buycU1CiYQk40KNHCcHfNiZbdlx1E9rpUp7bnF
lRa2v1ntMX3caRVDdbtPEWmdxSCYsYFDk4mZrOLBA4GEAAKBgEbmeve5f8LIE/Gf
MNmP9CM5eovQOGx5ho8WqD+aTebs+k2tn92BBPqeZqpWRa5P/+jrdKml1qx4llHW
MXrs3IgIb6+hUIB+S8dz8/mmO0bpr76RoZVCXYab2CZedFut7qc3WUH9+EUAH5mw
vSeDCOUMYQR7R9LINYwouHIziqQYMAkGByqGSM44BAMDLwAwLAIUWXBlk40xTwSw
7HX32MxXYruse9ACFBNGmdX2ZBrVNGrN9N2f6ROk0k9K
-----END CERTIFICATE-----
For other regions, contact AWS Support to get the AWS public certificate.

To verify the PKCS7 signature

From your instance, create a temporary file for the PKCS7 signature:

Copy
[ec2-user ~]$ PKCS7=$(mktemp)
Add the -----BEGIN PKCS7----- header to the temporary PKCS7 file:

Copy
[ec2-user ~]$ echo "-----BEGIN PKCS7-----" > $PKCS7
Append the contents of the PKCS7 signature from the instance metadata, plus a new line:

Copy
[ec2-user ~]$ curl -s http://169.254.169.254/latest/dynamic/instance-identity/pkcs7 >> $PKCS7
[ec2-user ~]$ echo "" >> $PKCS7
Append the -----END PKCS7----- footer:

Copy
[ec2-user ~]$ echo "-----END PKCS7-----" >> $PKCS7
Create a temporary file for the instance identity document:

Copy
[ec2-user ~]$ DOCUMENT=$(mktemp)
Add the contents of the document from your instance metadata to the temporary document file:

Copy
[ec2-user ~]$ curl -s http://169.254.169.254/latest/dynamic/instance-identity/document > $DOCUMENT
Open a text editor and create a file named AWSpubkey. Copy and paste the contents of the AWS public certificate above to the file and save it.

Use the OpenSSL tools to verify the signature as follows:

Copy
[ec2-user ~]$ openssl smime -verify -in $PKCS7 -inform PEM -content $DOCUMENT -certfile AWSpubkey -noverify > /dev/null
Verification successful

Identify EC2 Linux Instances

You may benefit from being able to determine whether a system is an EC2 instance. There are two methods that you can use to identify an EC2 instance.

For information about identifying Windows instances, see Identify EC2 Windows Instances in the Amazon EC2 User Guide for Windows Instances.

Inspecting the System UUID

You can get the system UUID and look for the presence of the characters "ec2" or "EC2" in the beginning octet of the UUID. This method to determine whether a system is an EC2 instance is quick but potentially inaccurate because there is a small chance that a system that is not an EC2 instance could have a UUID that starts with these characters. For a definitive approach, see Inspecting the Instance Identity Document.

Example : Get the UUID from the hypervisor

If /sys/hypervisor/uuid exists, you can use the following command:

Copy
[ec2-user ~]$ cat /sys/hypervisor/uuid
In the following example output, the UUID starts with "ec2", which indicates that the system is probably an EC2 instance.

ec2e1916-9099-7caf-fd21-012345abcdef
Example : Get the UUID from DMI (HVM instances only)

On HVM instances only, you can use the Desktop Management Interface (DMI).

You can use the dmidecode tool to return the UUID. On Amazon Linux, use the following command to install the dmidecode tool if it's not already installed on your instance:

Copy
[ec2-user ~]$ sudo yum install dmidecode -y
Then run the following command:

Copy
[ec2-user ~]$ sudo dmidecode --string system-uuid
Alternatively, use the following command:

Copy
[ec2-user ~]$ sudo cat /sys/devices/virtual/dmi/id/product_uuid
In the following example output, the UUID starts with "EC2", which indicates that the system is probably an EC2 instance.

EC2E1916-9099-7CAF-FD21-01234ABCDEF
Inspecting the Instance Identity Document

For a definitive and cryptographically verified method of identifying an EC2 instance, check the instance identity document, including its signature. These documents are available on every EC2 instance at the local, non-routable address http://169.254.169.254/latest/dynamic/instance-identity/. For more information, see Instance Identity Documents.





