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

