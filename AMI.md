Amazon Machine Images (AMI)

An Amazon Machine Image (AMI) provides the information required to launch an instance, which is a virtual server in the cloud. You specify an AMI when you launch an instance, and you can launch as many instances from the AMI as you need. You can also launch instances from as many different AMIs as you need.

An AMI includes the following:

A template for the root volume for the instance (for example, an operating system, an application server, and applications)
Launch permissions that control which AWS accounts can use the AMI to launch instances
A block device mapping that specifies the volumes to attach to the instance when it's launched
Using an AMI

The following diagram summarizes the AMI lifecycle. After you create and register an AMI, you can use it to launch new instances. (You can also launch instances from an AMI if the AMI owner grants you launch permissions.) You can copy an AMI to the same region or to different regions. When you are finished launching instance from an AMI, you can deregister the AMI.


					The AMI lifecycle (create, register, launch, copy, deregister).
				
You can search for an AMI that meets the criteria for your instance. You can search for AMIs provided by AWS or AMIs provided by the community. For more information, see AMI Types and Finding a Linux AMI.

When you are connected to an instance, you can use it just like you use any other server. For information about launching, connecting, and using your instance, see Amazon EC2 Instances.

Creating Your Own AMI

You can customize the instance that you launch from a public AMI and then save that configuration as a custom AMI for your own use. Instances that you launch from your AMI use all the customizations that you've made.

The root storage device of the instance determines the process you follow to create an AMI. The root volume of an instance is either an Amazon EBS volume or an instance store volume. For information, see Amazon EC2 Root Device Volume.

To create an Amazon EBS-backed AMI, see Creating an Amazon EBS-Backed Linux AMI. To create an instance store-backed AMI, see Creating an Instance Store-Backed Linux AMI.

To help categorize and manage your AMIs, you can assign custom tags to them. For more information, see Tagging Your Amazon EC2 Resources.

Buying, Sharing, and Selling AMIs

After you create an AMI, you can keep it private so that only you can use it, or you can share it with a specified list of AWS accounts. You can also make your custom AMI public so that the community can use it. Building a safe, secure, usable AMI for public consumption is a fairly straightforward process, if you follow a few simple guidelines. For information about how to create and use shared AMIs, see Shared AMIs.

You can purchase an AMIs from a third party, including AMIs that come with service contracts from organizations such as Red Hat. You can also create an AMI and sell it to other Amazon EC2 users. For more information about buying or selling AMIs, see Paid AMIs.

Deregistering Your AMI

You can deregister an AMI when you have finished with it. After you deregister an AMI, you can't use it to launch new instances. For more information, see Deregistering Your AMI.

Amazon Linux

The Amazon Linux AMI is a supported and maintained Linux image provided by AWS. The following are some of the features of Amazon Linux:

A stable, secure, and high-performance execution environment for applications running on Amazon EC2.
Provided at no additional charge to Amazon EC2 users.
Repository access to multiple versions of MySQL, PostgreSQL, Python, Ruby, Tomcat, and many more common packages.
Updated on a regular basis to include the latest components, and these updates are also made available in the yum repositories for installation on running instances.
Includes packages that enable easy integration with AWS services, such as the AWS CLI, Amazon EC2 API and AMI tools, the Boto library for Python, and the Elastic Load Balancing tools.
For more information, see Amazon Linux.

AMI Types

You can select an AMI to use based on the following characteristics:

Region (see Regions and Availability Zones)
Operating system
Architecture (32-bit or 64-bit)
Launch Permissions
Storage for the Root Device
Launch Permissions

The owner of an AMI determines its availability by specifying launch permissions. Launch permissions fall into the following categories.

Launch Permission	Description
public	The owner grants launch permissions to all AWS accounts.
explicit	The owner grants launch permissions to specific AWS accounts.
implicit	The owner has implicit launch permissions for an AMI.
Amazon and the Amazon EC2 community provide a large selection of public AMIs. For more information, see Shared AMIs. Developers can charge for their AMIs. For more information, see Paid AMIs.

Storage for the Root Device

All AMIs are categorized as either backed by Amazon EBS or backed by instance store. The former means that the root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot. The latter means that the root device for an instance launched from	the AMI is an instance store volume created from a template stored in Amazon S3. For more information, see Amazon EC2 Root Device Volume.

This section summarizes the important differences between the two types of AMIs. The following table provides a quick summary of these differences.

Characteristic	Amazon EBS-Backed	Amazon Instance Store-Backed
Boot time
Usually less than 1 minute
Usually less than 5 minutes
Size limit
16 TiB
10 GiB
Root device volume
Amazon EBS volume
Instance store volume
Data persistence
By default, the root volume is deleted when the instance terminates.* Data on any other Amazon EBS volumes persists after instance termination by default. Data on any instance store volumes persists only during the life of the instance.
Data on any instance store volumes persists only during the life of the instance. Data on any Amazon EBS volumes persists after instance termination by default.
Upgrading
The instance type, kernel, RAM disk, and user data can be changed while the instance is stopped.
Instance attributes are fixed for the life of an instance.
Charges
You're charged for instance usage, Amazon EBS volume usage, and storing your AMI as an Amazon EBS snapshot.
You're charged for instance usage and storing your AMI in Amazon S3.
AMI creation/bundling
Uses a single command/call
Requires installation and use of AMI tools
Stopped state
Can be placed in stopped state where instance is not running, but the root volume is persisted in Amazon EBS
Cannot be in stopped state; instances are running or terminated
* By default, Amazon EBS-backed instance root volumes have the DeleteOnTermination flag set to true. For information about how to change this flag so that the volume persists after termination, see Changing the Root Device Volume to Persist.

Determining the Root Device Type of Your AMI

To determine the root device type of an AMI using the console

Open the Amazon EC2 console.

In the navigation pane, click AMIs, and select the AMI.

Check the value of Root Device Type in the Details tab as follows:

If the value is ebs, this is an Amazon EBS-backed AMI.
If the value is instance store, this is an instance store-backed AMI.
To determine the root device type of an AMI using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-images (AWS CLI)
Get-EC2Image (AWS Tools for Windows PowerShell)
Stopped State

You can stop an Amazon EBS-backed instance, but not an Amazon EC2 instance store-backed instance. Stopping causes the instance to stop running (its status goes from running to stopping to stopped). A stopped instance persists in Amazon EBS, which allows it to be restarted. Stopping is different from terminating; you can't restart a terminated instance. Because Amazon EC2 instance store-backed AMIs can't be stopped, they're either running or terminated. For more information about what happens and what you can do while an instance is stopped, see Stop and Start Your Instance.

Default Data Storage and Persistence

Instances that use an instance store volume for the root device automatically have instance store available (the root volume contains the root partition and you can store additional data). You can add persistent storage to your instance by attaching one or more Amazon EBS volumes. Any data on an instance store volume is deleted when the instance fails or terminates. For more information, see Instance Store Lifetime.

Instances that use Amazon EBS for the root device automatically have an Amazon EBS volume attached. The volume appears in your list of volumes like any other. With most instance types, Amazon EBS-backed instances don't have instance store volumes by default. You can add instance store volumes or additional Amazon EBS volumes using a block device mapping. For more information, see Block Device Mapping.

Boot Times

Amazon EBS-backed AMIs launch faster than Amazon EC2 instance store-backed AMIs. When you launch an Amazon EC2 instance store-backed AMI, all the parts have to be retrieved from Amazon S3 before the instance is available. With an Amazon EBS-backed AMI, only the parts required to boot the instance need to be retrieved from the snapshot before the instance is available. However, the performance of an instance that uses an Amazon EBS volume for its root device is slower for a short time while the remaining parts are retrieved from the snapshot and loaded into the volume. When you stop and restart the instance, it launches quickly, because the state is stored in an Amazon EBS volume.

AMI Creation

To create Linux AMIs backed by instance store, you must create an AMI from your instance on the instance itself using the Amazon EC2 AMI tools.

AMI creation is much easier for AMIs backed by Amazon EBS. The CreateImage API action creates your Amazon EBS-backed AMI and registers it. There's also a button in the AWS Management Console that lets you create an AMI from a running instance. For more information, see Creating an Amazon EBS-Backed Linux AMI.

How You're Charged

With AMIs backed by instance store, you're charged for AMI storage and instance usage. With AMIs backed by Amazon EBS, you're charged for volume storage and usage in addition to the AMI and instance usage charges.

With Amazon EC2 instance store-backed AMIs, each time you customize an AMI and create a new one, all of the parts are stored in Amazon S3 for each AMI. So, the storage footprint for each customized AMI is the full size of the AMI. For Amazon EBS-backed AMIs, each time you customize an AMI and create a new one, only the changes are stored. So the storage footprint for subsequent AMIs you customize after the first is much smaller, resulting in lower AMI storage charges.

When an Amazon EBS-backed instance is stopped, you're not charged for instance usage; however, you're still charged for volume storage. We charge a full instance hour for every transition from a stopped state to a running state, even if you transition the instance multiple times within a single hour. For example, let's say the hourly instance charge for your instance is $0.10. If you were to run that instance for one hour without stopping it, you would be charged $0.10. If you stopped and restarted that instance twice during that hour, you would be charged $0.30 for that hour of usage (the initial $0.10, plus 2 x $0.10 for each restart).

Linux AMI Virtualization Types

Linux Amazon Machine Images use one of two types of virtualization: paravirtual (PV) or hardware virtual machine (HVM). The main difference between PV and HVM AMIs is the way in which they boot and whether they can take advantage of special hardware extensions (CPU, network, and storage) for better performance.

For the best performance, we recommend that you use current generation instance types and HVM AMIs when you launch your instances. For more information about current generation instance types, see the Amazon EC2 Instances detail page. If you are using previous generation instance types and would like to upgrade, see Upgrade Paths.

For information about the types of the Amazon Linux AMI recommended for each instance type, see the Amazon Linux AMI Instance Types detail page.

HVM AMIs

HVM AMIs are presented with a fully virtualized set of hardware and boot by executing the master boot record of the root block device of your image. This virtualization type provides the ability to run an operating system directly on top of a virtual machine without any modification, as if it were run on the bare-metal hardware. The Amazon EC2 host system emulates some or all of the underlying hardware that is presented to the guest.

Unlike PV guests, HVM guests can take advantage of hardware extensions that provide fast access to the underlying hardware on the host system. For more information on CPU virtualization extensions available in Amazon EC2, see Intel Virtualization Technology on the Intel website. HVM AMIs are required to take advantage of enhanced networking and GPU processing. In order to pass through instructions to specialized network and GPU devices, the OS needs to be able to have access to the native hardware platform; HVM virtualization provides this access. For more information, see Enhanced Networking and Linux Accelerated Computing Instances.

All current generation instance types support HVM AMIs. The CC2, CR1, HI1, and HS1 previous generation instance types support HVM AMIs.

To find an HVM AMI, verify that the virtualization type of the AMI is set to hvm, using the console or the describe-images command.

PV AMIs

PV AMIs boot with a special boot loader called PV-GRUB, which starts the boot cycle and then chain loads the kernel specified in the menu.lst file on your image. Paravirtual guests can run on host hardware that does not have explicit support for virtualization, but they cannot take advantage of special hardware extensions such as enhanced networking or GPU processing. Historically, PV guests had better performance than HVM guests in many cases, but because of enhancements in HVM virtualization and the availability of PV drivers for HVM AMIs, this is no longer true. For more information about PV-GRUB and its use in Amazon EC2, see Enabling Your Own Linux Kernels.

The C3 and M3 current generation instance types support PV AMIs. The C1, HI1, HS1, M1, M2, and T1 previous generation instance types support PV AMIs.

To find a PV AMI, verify that the virtualization type of the AMI is set to paravirtual, using the console or the describe-images command.

PV on HVM

Paravirtual guests traditionally performed better with storage and network operations than HVM guests because they could leverage special drivers for I/O that avoided the overhead of emulating network and disk hardware, whereas HVM guests had to translate these instructions to emulated hardware. Now these PV drivers are available for HVM guests, so operating systems that cannot be ported to run in a paravirtualized environment (such as Windows) can still see performance advantages in storage and network I/O by using them. With these PV on HVM drivers, HVM guests can get the same, or better, performance than paravirtual guests.

Finding a Linux AMI

Before you can launch an instance, you must select an AMI to use. As you select an AMI, consider the following requirements you might have for the instances that you'll launch:

The region
The operating system
The architecture: 32-bit (i386) or 64-bit (x86_64)
The root device type: Amazon EBS or instance store
The provider: Amazon Web Services, Oracle, IBM, Microsoft, or the community
If you need to find a Windows AMI, see Finding a Windows AMI in the Amazon EC2 User Guide for Windows Instances.

Contents

Finding a Linux AMI Using the Amazon EC2 Console
Finding an AMI Using the AWS CLI
Finding a Linux AMI Using the Amazon EC2 Console

You can find Linux AMIs using the Amazon EC2 console. You can search through all available AMIs using the Images page, or select from commonly used AMIs on the Quick Launch tab when you use the console to launch an instance.

To find a Linux AMI using the Images page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select a region. You can select any region that's available to you, regardless of your location. This is the region in which you'll launch your instance.

In the navigation pane, choose AMIs.

(Optional) Use the Filter options to scope the list of displayed AMIs to see only the AMIs that interest you. For example, to list all Linux AMIs provided by AWS, select Public images. Choose the Search bar and select Owner from the menu, then select Amazon images. Choose the Search bar again to select Platform and then the operating system from the list provided.

(Optional) Choose the Show/Hide Columns icon to select which image attributes to display, such as the root device type. Alternatively, you can select an AMI from the list and view its properties in the Details tab.

Before you select an AMI, it's important that you check whether it's backed by instance store or by Amazon EBS and that you are aware of the effects of this difference. For more information, see Storage for the Root Device.

To launch an instance from this AMI, select it and then choose Launch. For more information about launching an instance using the console, see Launching Your Instance from an AMI. If you're not ready to launch the instance now, write down the AMI ID (ami-xxxxxxxx) for later.

To find a Linux AMI when you launch an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the console dashboard, choose Launch Instance.

On the Choose an Amazon Machine Image (AMI) page, on the Quick Start tab, select from one of the commonly used AMIs in the list. If you don't see the AMI that you need, select the AWS Marketplace or Community AMIs tab to find additional AMIs.

Finding an AMI Using the AWS CLI

You can use command line parameters to list only the types of AMIs that interest you. For example, you can use the describe-images command as follows to find public AMIs owned by you or Amazon.

Copy
aws ec2 describe-images --owners self amazon
Add the following filter to the previous command to display only AMIs backed by Amazon EBS:

Copy
--filters "Name=root-device-type,Values=ebs"
After locating an AMI that meets your needs, write down its ID (ami-xxxxxxxx). You can use this AMI to launch instances. For more information, see Launching an Instance Using the AWS CLI in the AWS Command Line Interface User Guide.

Shared AMIs

A shared AMI is an AMI that a developer created and made available for other developers to use. One of the easiest ways to get started with Amazon EC2 is to use a shared AMI that has the components you need and then add custom content. You can also create your own AMIs and share them with others.

You use a shared AMI at your own risk. Amazon can't vouch for the integrity or security of AMIs shared by other Amazon EC2 users. Therefore, you should treat shared AMIs as you would any foreign code that you might consider deploying in your own data center and perform the appropriate due diligence. We recommend that you get an AMI from a trusted source. If you have questions or observations about a shared AMI, use the AWS forums.

Amazon's public images have an aliased owner, which appears as amazon in the account field. This enables you to find AMIs from Amazon easily. Other users can't alias their AMIs.

For information about creating an AMI, see Creating an Instance Store-Backed Linux AMI or Creating an Amazon EBS-Backed Linux AMI . For more information about building, delivering, and maintaining your applications on the AWS Marketplace, see the AWS Marketplace User Guide and AWS Marketplace Seller Guide.

Contents

Finding Shared AMIs
Making an AMI Public
Sharing an AMI with Specific AWS Accounts
Using Bookmarks
Guidelines for Shared Linux AMIs

Finding Shared AMIs

You can use the Amazon EC2 console or the command line to find shared AMIs.

Finding a Shared AMI (Console)

To find a shared private AMI using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose AMIs.

In the first filter, choose Private images. All AMIs that have been shared with you are listed. To granulate your search, choose the Search bar and use the filter options provided in the menu.

To find a shared public AMI using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose AMIs.

In the first filter, choose Public images. To granulate your search, choose the Search bar and use the filter options provided in the menu.

Use filters to list only the types of AMIs that interest you. For example, choose Owner : and then choose Amazon images to display only Amazon's public images.

Finding a Shared AMI (AWS CLI)

Use the describe-images command (AWS CLI) to list AMIs. You can scope the list to the types of AMIs that interest you, as shown in the following examples.

Example: List all public AMIs

The following command lists all public AMIs, including any public AMIs that you own.

Copy
aws ec2 describe-images --executable-users all
Example: List AMIs with explicit launch permissions

The following command lists the AMIs for which you have explicit launch permissions. This list does not include any AMIs that you own.

Copy
aws ec2 describe-images --executable-users self
Example: List AMIs owned by Amazon

The following command lists the AMIs owned by Amazon. Amazon's public AMIs have an aliased owner, which appears as amazon in the account field. This enables you to find AMIs from Amazon easily. Other users can't alias their AMIs.

Copy
aws ec2 describe-images --owners amazon
Example: List AMIs owned by an account

The following command lists the AMIs owned by the specified AWS account.

Copy
aws ec2 describe-images --owners 123456789012
Example: Scope AMIs using a filter

To reduce the number of displayed AMIs, use a filter to list only the types of AMIs that interest you. For example, use the following filter to display only EBS-backed AMIs.

Copy
--filters "Name=root-device-type,Values=ebs"
Using Shared AMIs

Before you use a shared AMI, take the following steps to confirm that there are no pre-installed credentials that would allow unwanted access to your instance by a third party and no pre-configured remote logging that could transmit sensitive data to a third party. Check the documentation for the Linux distribution used by the AMI for information about improving the security of the system.

To ensure that you don't accidentally lose access to your instance, we recommend that you initiate two SSH sessions and keep the second session open until you've removed credentials that you don't recognize and confirmed that you can still log into your instance using SSH.

Identify and disable any unauthorized public SSH keys. The only key in the file should be the key you used to launch the AMI. The following command locates authorized_keys files:

Copy
[ec2-user ~]$ sudo find / -name "authorized_keys" -print -exec cat {} \;
Disable password-based authentication for the root user. Open the ssh_config file and edit the PermitRootLogin line as follows:

PermitRootLogin without-password
Alternatively, you can disable the ability to log into the instance as root:

PermitRootLogin No
Restart the sshd service.

Check whether there are any other user accounts that are able to log in to your instance. Accounts with superuser privileges are particularly dangerous. Remove or lock the password of any unknown accounts.

Check for open ports that you aren't using and running network services listening for incoming connections.

To prevent preconfigured remote logging, you should delete the existing configuration file and restart the rsyslog service. For example:

Copy
[ec2-user ~]$ sudo rm /etc/rsyslog.config
[ec2-user ~]$ sudo service rsyslog restart
Verify that all cron jobs are legitimate.

If you discover a public AMI that you feel presents a security risk, contact the AWS security team. For more information, see the AWS Security Center.

Making an AMI Public

Amazon EC2 enables you to share your AMIs with other AWS accounts. You can allow all AWS accounts to launch the AMI (make the AMI public), or only allow a few specific accounts to launch the AMI (see Sharing an AMI with Specific AWS Accounts). You are not billed when your AMI is launched by other AWS accounts; only the accounts launching the AMI are billed.

AMIs are a regional resource. Therefore, sharing an AMI makes it available in that region. To make an AMI available in a different region, copy the AMI to the region and then share it. For more information, see Copying an AMI.

To avoid exposing sensitive data when you share an AMI, read the security considerations in Guidelines for Shared Linux AMIs and follow the recommended actions.

Note
If an AMI has a product code, you can't make it public. You must share the AMI with only specific AWS accounts.
Sharing an AMI with all AWS Accounts (Console)

After you make an AMI public, it is available in Community AMIs when you launch an instance in the same region using the console. Note that it can take a short while for an AMI to appear in Community AMIs after you make it public. It can also take a short while for an AMI to be removed from Community AMIs after you make it private again.

To share a public AMI using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose AMIs.

Select your AMI from the list, and then choose Actions, Modify Image Permissions.

Choose Public and choose Save.

Sharing an AMI with all AWS Accounts (AWS CLI)

Each AMI has a launchPermission property that controls which AWS accounts, besides the owner's, are allowed to use that AMI to launch instances. By modifying the launchPermission property of an AMI, you can make the AMI public (which grants launch permissions to all AWS accounts) or share it with only the AWS accounts that you specify.

You can add or remove account IDs from the list of accounts that have launch permissions for an AMI. To make the AMI public, specify the all group. You can specify both public and explicit launch permissions.

To make an AMI public

Use the modify-image-attribute command as follows to add the all group to the launchPermission list for the specified AMI.

Copy
aws ec2 modify-image-attribute --image-id ami-12345678 --launch-permission "{\"Add\":[{\"Group\":\"all\"}]}"
To verify the launch permissions of the AMI, use the following describe-image-attribute command.

Copy
aws ec2 describe-image-attribute --image-id ami-12345678 --attribute launchPermission
(Optional) To make the AMI private again, remove the all group from its launch permissions. Note that the owner of the AMI always has launch permissions and is therefore unaffected by this command.

Copy
aws ec2 modify-image-attribute --image-id ami-12345678 --launch-permission "{\"Remov

Sharing an AMI with Specific AWS Accounts

You can share an AMI with specific AWS accounts without making the AMI public. All you need are the AWS account IDs.

AMIs are a regional resource. Therefore, sharing an AMI makes it available in that region. To make an AMI available in a different region, copy the AMI to the region and then share it. For more information, see Copying an AMI.

Sharing an AMI (Console)

To grant explicit launch permissions using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose AMIs.

Select your AMI in the list, and then choose Actions, Modify Image Permissions.

Specify the AWS account number of the user with whom you want to share the AMI in the AWS Account Number field, then choose Add Permission.

To share this AMI with multiple users, repeat the above step until you have added all the required users.

To allow create volume permissions for snapshots, select Add "create volume" permissions to the following associated snapshots when creating permissions.

Note
You do not need to share the Amazon EBS snapshots that an AMI references in order to share the AMI. Only the AMI itself needs to be shared; the system automatically provides the instance access to the referenced Amazon EBS snapshots for the launch.
Choose Save when you are done.

Sharing an AMI (AWS CLI)

Use the modify-image-attribute command (AWS CLI) to share an AMI as shown in the following examples.

To grant explicit launch permissions

The following command grants launch permissions for the specified AMI to the specified AWS account.

Copy
aws ec2 modify-image-attribute --image-id ami-12345678 --launch-permission "{\"Add\":[{\"UserId\":\"123456789012\"}]}"
The following command grants create volume permission for a snapshot.

Copy
aws ec2 modify-snapshot-attribute --snapshot-id snap-1234567890abcdef0 --attribute createVolumePermission --operation-type add --user-ids 123456789012
To remove launch permissions for an account

The following command removes launch permissions for the specified AMI from the specified AWS account:

Copy
aws ec2 modify-image-attribute --image-id ami-12345678 --launch-permission "{\"Remove\":[{\"UserId\":\"123456789012\"}]}"
The following command removes create volume permission for a snapshot.

Copy
aws ec2 modify-snapshot-attribute --snapshot-id snap-1234567890abcdef0 --attribute createVolumePermission --operation-type remove --user-ids 123456789012
To remove all launch permissions

The following command removes all public and explicit launch permissions from the specified AMI. Note that the owner of the AMI always has launch permissions and is therefore unaffected by this command.

Copy
aws ec2 reset-image-attribute --image-id ami-12345678 --attribute launchPermission

Using Bookmarks

If you have created a public AMI, or shared an AMI with another AWS user, you can create a bookmark that allows a user to access your AMI and launch an instance in their own account immediately. This is an easy way to share AMI references, so users don't have to spend time finding your AMI in order to use it.

Note that your AMI must be public, or you must have shared it with the user to whom you want to send the bookmark.

To create a bookmark for your AMI

Type a URL with the following information, where region is the region in which your AMI resides:

Copy
https://console.aws.amazon.com/ec2/v2/home?region=region#LaunchInstanceWizard:ami=ami_id
For example, this URL launches an instance from the ami-12345678 AMI in the us-east-1 region:

https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstanceWizard:ami=ami-12345678
Distribute the link to users who want to use your AMI.

To use a bookmark, choose the link or copy and paste it into your browser. The launch wizard opens, with the AMI already selected.

Guidelines for Shared Linux AMIs

Use the following guidelines to reduce the attack surface and improve the reliability of the AMIs you create.

Note
No list of security guidelines can be exhaustive. Build your shared AMIs carefully and take time to consider where you might expose sensitive data.
Topics

Update the AMI Tools at Boot Time
Disable Password-Based Remote Logins for Root
Disable Local Root Access
Remove SSH Host Key Pairs
Install Public Key Credentials
Disabling sshd DNS Checks (Optional)
Identify Yourself
Protect Yourself
If you are building AMIs for AWS Marketplace, see Building AMIs for AWS Marketplace for guidelines, policies and best practices.

For additional information about sharing AMIs safely, see the following articles:

How To Share and Use Public AMIs in A Secure Manner
Public AMI Publishing: Hardening and Clean-up Requirements
Update the AMI Tools at Boot Time

For AMIs backed by instance store, we recommend that your AMIs download and upgrade the Amazon EC2 AMI creation tools during startup. This ensures that new AMIs based on your shared AMIs have the latest AMI tools.

For Amazon Linux, add the following to /etc/rc.local:

Copy
# Update the Amazon EC2 AMI tools
echo " + Updating EC2 AMI tools"
yum update -y aws-amitools-ec2
echo " + Updated EC2 AMI tools"
Use this method to automatically update other software on your image.

Note
When deciding which software to automatically update, consider the amount of WAN traffic that the update will generate (your users will be charged for it) and the risk of the update breaking other software on the AMI.
For other distributions, make sure you have the latest AMI tools.

Disable Password-Based Remote Logins for Root

Using a fixed root password for a public AMI is a security risk that can quickly become known. Even relying on users to change the password after the first login opens a small window of opportunity for potential abuse.

To solve this problem, disable password-based remote logins for the root user.

To disable password-based remote logins for root

Open the /etc/ssh/sshd_config file with a text editor and locate the following line:

#PermitRootLogin yes
Change the line to:

PermitRootLogin without-password
The location of this configuration file might differ for your distribution, or if you are not running OpenSSH. If this is the case, consult the relevant documentation.

Disable Local Root Access

When you work with shared AMIs, a best practice is to disable direct root logins. To do this, log into your running instance and issue the following command:

Copy
[ec2-user ~]$ sudo passwd -l root
Note
This command does not impact the use of sudo.
Remove SSH Host Key Pairs

If you plan to share an AMI derived from a public AMI, remove the existing SSH host key pairs located in /etc/ssh. This forces SSH to generate new unique SSH key pairs when someone launches an instance using your AMI, improving security and reducing the likelihood of "man-in-the-middle" attacks.

Remove all of the following key files that are present on your system.

ssh_host_dsa_key
ssh_host_dsa_key.pub
ssh_host_key
ssh_host_key.pub
ssh_host_rsa_key
ssh_host_rsa_key.pub
ssh_host_ecdsa_key
ssh_host_ecdsa_key.pub
ssh_host_ed25519_key
ssh_host_ed25519_key.pub
You can securely remove all of these files with the following command.

Copy
[ec2-user ~]$ sudo shred -u /etc/ssh/*_key /etc/ssh/*_key.pub
Warning
Secure deletion utilities such as shred may not remove all copies of a file from your storage media. Hidden copies of files may be created by journalling file systems (including Amazon Linux default ext4), snapshots, backups, RAID, and temporary caching. For more information see the shred documentation.
Important
If you forget to remove the existing SSH host key pairs from your public AMI, our routine auditing process notifies you and all customers running instances of your AMI of the potential security risk. After a short grace period, we mark the AMI private.
Install Public Key Credentials

After configuring the AMI to prevent logging in using a password, you must make sure users can log in using another mechanism.

Amazon EC2 allows users to specify a public-private key pair name when launching an instance. When a valid key pair name is provided to the RunInstances API call (or through the command line API tools), the public key (the portion of the key pair that Amazon EC2 retains on the server after a call to CreateKeyPair or ImportKeyPair) is made available to the instance through an HTTP query against the instance metadata.

To log in through SSH, your AMI must retrieve the key value at boot and append it to /root/.ssh/authorized_keys (or the equivalent for any other user account on the AMI). Users can launch instances of your AMI with a key pair and log in without requiring a root password.

Many distributions, including Amazon Linux and Ubuntu, use the cloud-init package to inject public key credentials for a configured user. If your distribution does not support cloud-init, you can add the following code to a system start-up script (such as /etc/rc.local) to pull in the public key you specified at launch for the root user.

Copy
if [ ! -d /root/.ssh ] ; then
        mkdir -p /root/.ssh
        chmod 700 /root/.ssh
fi
# Fetch public key using HTTP
curl http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key > /tmp/my-key
if [ $? -eq 0 ] ; then
        cat /tmp/my-key >> /root/.ssh/authorized_keys
        chmod 700 /root/.ssh/authorized_keys
        rm /tmp/my-key
fi
This can be applied to any user account; you do not need to restrict it to root.

Note
Rebundling an instance based on this AMI includes the key with which it was launched. To prevent the key's inclusion, you must clear out (or delete) the authorized_keys file or exclude this file from rebundling.
Disabling sshd DNS Checks (Optional)

Disabling sshd DNS checks slightly weakens your sshd security. However, if DNS resolution fails, SSH logins still work. If you do not disable sshd checks, DNS resolution failures prevent all logins.

To disable sshd DNS checks

Open the /etc/ssh/sshd_config file with a text editor and locate the following line:

#UseDNS yes
Change the line to:

UseDNS no
Note
The location of this configuration file can differ for your distribution or if you are not running OpenSSH. If this is the case, consult the relevant documentation.
Identify Yourself

Currently, there is no easy way to know who provided a shared AMI, because each AMI is represented by an account ID.

We recommend that you post a description of your AMI, and the AMI ID, in the Amazon EC2 forum. This provides a convenient central location for users who are interested in trying new shared AMIs. You can also post the AMI to the Amazon Machine Images (AMIs) page.

Protect Yourself

The previous sections described how to make your shared AMIs safe, secure, and usable for the users who launch them. This section describes guidelines to protect yourself from the users of your AMI.

We recommend against storing sensitive data or software on any AMI that you share. Users who launch a shared AMI might be able to rebundle it and register it as their own. Follow these guidelines to help you to avoid some easily overlooked security risks:

We recommend using the --exclude directory option on ec2-bundle-vol to skip any directories and subdirectories that contain secret information that you would not like to include in your bundle. In particular, exclude all user-owned SSH public/private key pairs and SSH authorized_keys files when bundling the image. The Amazon public AMIs store these in /root/.ssh for the root account, and /home/user_name/.ssh/ for regular user accounts. For more information, see ec2-bundle-vol.
Always delete the shell history before bundling. If you attempt more than one bundle upload in the same AMI, the shell history contains your secret access key. The following example should be the last command executed before bundling from within the instance.
Copy
[ec2-user ~]$ shred -u ~/.*history
Warning
The limitations of shred described in the warning above apply here as well.
Be aware that bash writes the history of the current session to the disk on exit. If you log out of your instance after deleting ~/.bash_history, and then log back in, you will find that ~/.bash_history has been re-created and contains all of the commands executed during your previous session.
Other programs besides bash also write histories to disk, Use caution and remove or exclude unnecessary dot-files and dot-directories.
Bundling a running instance requires your private key and X.509 certificate. Put these and other credentials in a location that is not bundled (such as the instance store).

Paid AMIs

A paid AMI is an AMI that you can purchase from a developer.

Amazon EC2 integrates with AWS Marketplace, enabling developers to charge other Amazon EC2 users for the use of their AMIs or to provide support for instances.

The AWS Marketplace is an online store where you can buy software that runs on AWS; including AMIs that you can use to launch your EC2 instance. The AWS Marketplace AMIs are organized into categories, such as Developer Tools, to enable you to find products to suit your requirements. For more information about AWS Marketplace, see the AWS Marketplace site.

Launching an instance from a paid AMI is the same as launching an instance from any other AMI. No additional parameters are required. The instance is charged according to the rates set by the owner of the AMI, as well as the standard usage fees for the related web services; for example, the hourly rate for running a m1.small instance type in Amazon EC2. Additional taxes may also apply. The owner of the paid AMI can confirm whether a specific instance was launched using that paid AMI.

Important
Amazon DevPay is no longer accepting new sellers or products. AWS Marketplace is now the single, unified e-commerce platform for selling software and services through AWS. For information about how to deploy and sell software from AWS Marketplace, see Selling on AWS Marketplace. AWS Marketplace supports AMIs backed by Amazon EBS.
Contents

Selling Your AMI
Finding a Paid AMI
Purchase a Paid AMI
Getting the Product Code for Your Instance
Using Paid Support
Bills for Paid and Supported AMIs
Managing Your AWS Marketplace Subscriptions
Selling Your AMI

You can sell your AMI using AWS Marketplace. AWS Marketplace offers an organized shopping experience. Additionally, AWS Marketplace also supports AWS features such as Amazon EBS-backed AMIs, Reserved Instances, and Spot instances.

For information about how to sell your AMI on AWS Marketplace, see Selling on AWS Marketplace.

Finding a Paid AMI

There are several ways that you can find AMIs that are available for you to purchase. For example, you can use AWS Marketplace, the Amazon EC2 console, or the command line. Alternatively, a developer might let you know about a paid AMI themselves.

Finding a Paid AMI Using the Console

To find a paid AMI using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose AMIs.

Choose Public images from the first Filter list. In the Search bar choose Product Code, then Marketplace. In the Search bar again, choose Platform and then select the operating system from the list.

Finding a Paid AMI Using AWS Marketplace

To find a paid AMI using AWS Marketplace

Open AWS Marketplace.

Enter the name of the operating system in the search box, and click Go.

To scope the results further, use one of the categories or filters.

Each product is labeled with its product type: either AMI or Software as a Service.

Finding a Paid AMI Using the AWS CLI

You can find a paid AMI using the following describe-images command (AWS CLI).

Copy
aws ec2 describe-images --owners aws-marketplace
This command returns numerous details that describe each AMI, including the product code for a paid AMI. The output from describe-images includes an entry for the product code like the following:

"ProductCodes": [
    {
        "ProductCodeId": "product_code",
        "ProductCodeType": "marketplace"
    }
],
Purchase a Paid AMI

You must sign up for (purchase) a paid AMI before you can launch an instance using the AMI.

Typically a seller of a paid AMI presents you with information about the AMI, including its price and a link where you can buy it. When you click the link, you're first asked to log into AWS, and then you can purchase the AMI.

Purchasing a Paid AMI Using the Console

You can purchase a paid AMI by using the Amazon EC2 launch wizard. For more information, see Launching an AWS Marketplace Instance.

Subscribing to a Product Using AWS Marketplace

To use the AWS Marketplace, you must have an AWS account. To launch instances from AWS Marketplace products, you must be signed up to use the Amazon EC2 service, and you must be subscribed to the product from which to launch the instance. There are two ways to subscribe to products in the AWS Marketplace:

AWS Marketplace website: You can launch preconfigured software quickly with the 1-Click deployment feature.
Amazon EC2 launch wizard: You can search for an AMI and launch an instance directly from the wizard. For more information, see Launching an AWS Marketplace Instance.
Purchasing a Paid AMI From a Developer

The developer of a paid AMI can enable you to purchase a paid AMI that isn't listed in AWS Marketplace. The developer provides you with a link that enables you to purchase the product through Amazon. You can sign in with your Amazon.com credentials and select a credit card that's stored in your Amazon.com account to use when purchasing the AMI.

Getting the Product Code for Your Instance

You can retrieve the AWS Marketplace product code for your instance using its instance metadata. For more information about retrieving metadata, see Instance Metadata and User Data.

To retrieve a product code, use the following command:

Copy
[ec2-user ~]$ GET http://169.254.169.254/latest/meta-data/product-codes
If the instance has a product code, Amazon EC2 returns it.

Using Paid Support

Amazon EC2 also enables developers to offer support for software (or derived AMIs). Developers can create support products that you can sign up to use. During sign-up for the support product, the developer gives you a product code, which you must then associate with your own AMI. This enables the developer to confirm that your instance is eligible for support. It also ensures that when you run instances of the product, you are charged according to the terms for the product specified by the developer.

Important
You can't use a support product with Reserved Instances. You always pay the price that's specified by the seller of the support product.
To associate a product code with your AMI, use one of the following commands, where ami_id is the ID of the AMI and product_code is the product code:

modify-image-attribute (AWS CLI)
Copy
aws ec2 modify-image-attribute --image-id ami_id --product-codes "product_code"
Edit-EC2ImageAttribute (AWS Tools for Windows PowerShell)
Copy
PS C:\> Edit-EC2ImageAttribute -ImageId ami_id -ProductCode product_code
After you set the product code attribute, it cannot be changed or removed.

Bills for Paid and Supported AMIs

At the end of each month, you receive an email with the amount your credit card has been charged for using any paid or supported AMIs during the month. This bill is separate from your regular Amazon EC2 bill. For more information, see Paying For AWS Marketplace Products.

Managing Your AWS Marketplace Subscriptions

On the AWS Marketplace website, you can check your subscription details, view the vendor's usage instructions, manage your subscriptions, and more.

To check your subscription details

Log in to the AWS Marketplace.

Click Your Account.

Click Manage Your Software Subscriptions.

All your current subscriptions are listed. Click Usage Instructions to view specific instructions for using the product, for example, a user name for connecting to your running instance.

To cancel an AWS Marketplace subscription

Ensure that you have terminated any instances running from the subscription.

Open the Amazon EC2 console.

In the navigation pane, click Instances.

Select the instance, click Actions, select Instance State, and select Terminate. When prompted, click Yes, Terminate.

Log in to the AWS Marketplace, and click Your Account, then Manage Your Software Subscriptions.

Click Cancel subscription. You are prompted to confirm your cancellation.

Note
After you've canceled your subscription, you are no longer able to launch any instances from that AMI. To use that AMI again, you need to resubscribe to it, either on the AWS Marketplace website, or through the launch wizard in the Amazon EC2 console.

Creating an Amazon EBS-Backed Linux AMI

To create an Amazon EBS-backed Linux AMI, start from an instance that you've launched from an existing Amazon EBS-backed Linux AMI. This can be an AMI you have obtained from the AWS Marketplace, an AMI you have created using the AWS Server Migration Service or VM Import/Export, or any other AMI you can access. After you customized the instance to suit your needs, create and register a new AMI, which you can use to launch new instances with these customizations.

The procedures described below work for Amazon EC2 instances backed by encrypted Amazon EBS volumes (including the root volume) as well as for unencrypted volumes.

The AMI creation process is different for instance store-backed AMIs. For more information about the differences between Amazon EBS-backed and instance store-backed instances, and how to determine the root device type for your instance, see Storage for the Root Device. For more information about creating an instance store-backed Linux AMI, see Creating an Instance Store-Backed Linux AMI.

For more information about creating an Amazon EBS-backed Windows AMI, see Creating an Amazon EBS-Backed Windows AMI in the Amazon EC2 User Guide for Windows Instances.

Overview of Creating Amazon EBS-Backed AMIs

First, launch an instance from an AMI that's similar to the AMI that you'd like to create. You can connect to your instance and customize it. When the instance is configured correctly, ensure data integrity by stopping the instance before you create an AMI, then create the image. When you create an Amazon EBS-backed AMI, we automatically register it for you.

Amazon EC2 powers down the instance before creating the AMI to ensure that everything on the instance is stopped and in a consistent state during the creation process. If you're confident that your instance is in a consistent state appropriate for AMI creation, you can tell Amazon EC2 not to power down and reboot the instance. Some file systems, such as XFS, can freeze and unfreeze activity, making it safe to create the image without rebooting the instance.

During the AMI-creation process, Amazon EC2 creates snapshots of your instance's root volume and any other EBS volumes attached to your instance. If any volumes attached to the instance are encrypted, the new AMI only launches successfully on instances that support Amazon EBS encryption. For more information, see Amazon EBS Encryption.

Depending on the size of the volumes, it can take several minutes for the AMI-creation process to complete (sometimes up to 24 hours).You may find it more efficient to create snapshots of your volumes prior to creating your AMI. This way, only small, incremental snapshots need to be created when the AMI is created, and the process completes more quickly (the total time for snapshot creation remains the same). For more information, see Creating an Amazon EBS Snapshot.

After the process completes, you have a new AMI and snapshot created from the root volume of the instance. When you launch an instance using the new AMI, we create a new EBS volume for its root volume using the snapshot. Both the AMI and the snapshot incur charges to your account until you delete them. For more information, see Deregistering Your AMI.

If you add instance-store volumes or EBS volumes to your instance in addition to the root device volume, the block device mapping for the new AMI contains information for these volumes, and the block device mappings for instances that you launch from the new AMI automatically contain information for these volumes. The instance-store volumes specified in the block device mapping for the new instance are new and don't contain any data from the instance store volumes of the instance you used to create the AMI. The data on EBS volumes persists. For more information, see Block Device Mapping.

Creating a Linux AMI from an Instance

You can create an AMI using the AWS Management Console or the command line. The following diagram summarizes the process for creating an Amazon EBS-backed AMI from a running EC2 instance. Start with an existing AMI, launch an instance, customize it, create a new AMI from it, and finally launch an instance of your new AMI. The steps in the following diagram match the steps in the procedure below.


				Workflow for creating an AMI from an instance
			
To create an AMI from an instance using the console

Select an appropriate EBS-backed AMI to serve as a starting point for your new AMI, and configure it as needed prior to launch. For more information, see Launching an Instance.

Choose Launch to launch an instance of the EBS-backed AMI that you've selected. Accept the default values as you step through the wizard. For more information, see Launching an Instance.

While the instance is running, connect to it.

You can perform any of the following actions on your instance to customize it for your needs:

Install software and applications
Copy data
Reduce start time by deleting temporary files, defragmenting your hard drive, and zeroing out free space
Attach additional Amazon EBS volumes
(Optional) Create snapshots of all the volumes attached to your instance. For more information about creating snapshots, see Creating an Amazon EBS Snapshot.

In the navigation pane, choose Instances and select your instance. Choose Actions, Image, and Create Image.

Tip
If this option is disabled, your instance isn't an Amazon EBS-backed instance.
In the Create Image dialog box, specify values for the following fields, and then choose Create Image.

Name
A unique name for the image.

Description
(Optional) A description of the image, up to 255 characters.

By default, Amazon EC2 shuts down the instance, takes snapshots of any attached volumes, creates and registers the AMI, and then reboots the instance. Choose No reboot if you don't want your instance to be shut down.

Warning
If you choose No reboot, we can't guarantee the file system integrity of the created image.
You can modify the root volume, Amazon EBS volumes, and instance store volumes as follows:

To change the size of the root volume, locate the Root volume in the Type column, and fill in the Size field.
To suppress an Amazon EBS volume specified by the block device mapping of the AMI used to launch the instance, locate the EBS volume in the list and choose Delete.
To add an Amazon EBS volume, choose Add New Volume, Type, and EBS, and fill in the fields. When you then launch an instance from your new AMI, these additional volumes are automatically attached to the instance. Empty volumes must be formatted and mounted. Volumes based on a snapshot must be mounted.
To suppress an instance store volume specified by the block device mapping of the AMI used to launch the instance, locate the volume in the list and choose Delete.
To add an instance store volume, choose Add New Volume, Type, and Instance Store, and select a device name from the Device list. When you launch an instance from your new AMI, these additional volumes are automatically initialized and mounted. These volumes don't contain data from the instance store volumes of the running instance from which you based your AMI.
While your AMI is being created, you can choose AMIs in the navigation pane to view its status. Initially this will be pending. After a few minutes the status should change to available.

(Optional) Choose Snapshots in the navigation pane to view the snapshot that was created for the new AMI. When you launch an instance from this AMI, we use this snapshot to create its root device volume.

Launch an instance from your new AMI. For more information, see Launching an Instance.

The new running instance contains all of the customizations you applied in previous steps.

To create an AMI from an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-image (AWS CLI)
New-EC2Image (AWS Tools for Windows PowerShell)
Creating a Linux AMI from a Snapshot

If you have a snapshot of the root device volume of an instance, you can create an AMI from this snapshot using the AWS Management Console or the command line.

Important
Some Linux distributions, such as Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise Server (SLES), use the Amazon EC2 billingProduct code associated with an AMI to verify subscription status for package updates. Creating an AMI from an EBS snapshot does not maintain this billing code, and subsequent instances launched from such an AMI will not be able to connect to package update infrastructure.
Similarly, although you can create a Windows AMI from a snapshot, you can't successfully launch an instance from the AMI.
In general, AWS advises against manually creating AMIs from snapshots.
For more information about creating Windows AMIs or AMIs for Linux operating systems that must retain AMI billing codes to work properly, see Creating a Linux AMI from an Instance.
To create an AMI from a snapshot using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under Elastic Block Store, choose Snapshots.

Choose the snapshot and choose Actions, Create Image.

In the Create Image from EBS Snapshot dialog box, complete the fields to create your AMI, then choose Create. If you're re-creating a parent instance, then choose the same options as the parent instance.

Architecture: Choose i386 for 32-bit or x86_64 for 64-bit.
Root device name: Enter the appropriate name for the root volume. For more information, see Device Naming on Linux Instances.
Virtualization type: Choose whether instances launched from this AMI use paravirtual (PV) or hardware virtual machine (HVM) virtualization. For more information, see Linux AMI Virtualization Types.
(PV virtualization type only) Kernel ID and RAM disk ID: Choose the AKI and ARI from the lists. If you choose the default AKI or don't choose an AKI, you'll be required to specify an AKI every time you launch an instance using this AMI. In addition, your instance may fail the health checks if the default AKI is incompatible with the instance.
(Optional) Block Device Mappings: Add volumes or expand the default size of the root volume for the AMI. For more information about resizing the file system on your instance for a larger volume, see Extending a Linux File System after Resizing the Volume.
To create an AMI from a snapshot using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

register-image (AWS CLI)
Register-EC2Image (AWS Tools for Windows PowerShell)

Creating an Instance Store-Backed Linux AMI

To create an instance store-backed Linux AMI, start from an instance that you've launched from an existing instance store-backed Linux AMI. After you've customized the instance to suit your needs, bundle the volume and register a new AMI, which you can use to launch new instances with these customizations.

If you need to create an instance store-backed Windows AMI, see Creating an Instance Store-Backed Windows AMI in the Amazon EC2 User Guide for Windows Instances.

The AMI creation process is different for instance store-backed AMIs. For more information about the differences between Amazon EBS-backed and instance store-backed instances, and how to determine the root device type for your instance, see Storage for the Root Device. If you need to create an Amazon EBS-backed Linux AMI, see Creating an Amazon EBS-Backed Linux AMI.

Overview of the Creation Process for Instance Store-Backed AMIs

The following diagram summarizes the process of creating an AMI from an instance store-backed instance.


				Creating an instance store-backed AMI
			
First, launch an instance from an AMI that's similar to the AMI that you'd like to create. You can connect to your instance and customize it. When the instance is set up the way you want it, you can bundle it. It takes several minutes for the bundling process to complete. After the process completes, you have a bundle, which consists of an image manifest (image.manifest.xml) and files (image.part.xx) that contain a template for the root volume. Next you upload the bundle to your Amazon S3 bucket and then register your AMI.

When you launch an instance using the new AMI, we create the root volume for the instance using the bundle that you uploaded to Amazon S3. The storage space used by the bundle in Amazon S3 incurs charges to your account until you delete it. For more information, see Deregistering Your AMI.

If you add instance store volumes to your instance in addition to the root device volume, the block device mapping for the new AMI contains information for these volumes, and the block device mappings for instances that you launch from the new AMI automatically contain information for these volumes. For more information, see Block Device Mapping.

Prerequisites

Before you can create an AMI, you must complete the following tasks:

Install the AMI tools. For more information, see Setting Up the AMI Tools.
Install the AWS CLI. For more information, see Getting Set Up with the AWS Command Line Interface.
Ensure that you have an Amazon S3 bucket for the bundle. To create an Amazon S3 bucket, open the Amazon S3 console and click Create Bucket. Alternatively, you can use the AWS CLI mb command.
Ensure that you have your AWS account ID. For more information, see AWS Account Identifiers in the AWS General Reference.
Ensure that you have your access key ID and secret access key. For more information, see Access Keys in the AWS General Reference.
Ensure that you have an X.509 certificate and corresponding private key.
If you need to create an X.509 certificate, see Managing Signing Certificates. The X.509 certificate and private key are used to encrypt and decrypt your AMI.
[China (Beijing)] Use the $EC2_AMITOOL_HOME/etc/ec2/amitools/cert-ec2-cn-north-1.pem certificate.
[AWS GovCloud (US)] Use the $EC2_AMITOOL_HOME/etc/ec2/amitools/cert-ec2-gov.pem certificate.
Connect to your instance and customize it. For example, you can install software and applications, copy data, delete temporary files, and modify the Linux configuration.
Tasks

Setting Up the AMI Tools
Creating an AMI from an Instance Store-Backed Amazon Linux Instance
Creating an AMI from an Instance Store-Backed Ubuntu Instance
Converting your Instance Store-Backed AMI to an Amazon EBS-Backed AMI

Setting Up the AMI Tools

You can use the AMI tools to create and manage instance store-backed Linux AMIs. To use the tools, you must install them on your Linux instance. The AMI tools are available as both an RPM and as a .zip file for Linux distributions that don't support RPM.

To set up the AMI tools using the RPM

Install Ruby using the package manager for your Linux distribution, such as yum. For example:

Copy
[ec2-user ~]$ sudo yum install -y ruby
Download the RPM file using a tool such as wget or curl. For example:

Copy
[ec2-user ~]$ sudo wget https://s3.amazonaws.com/ec2-downloads/ec2-ami-tools.noarch.rpm
Install the RPM using the following command.

Copy
[ec2-user ~]$ sudo yum install ec2-ami-tools.noarch.rpm
Verify your AMI tools installation using the ec2-ami-tools-version command.

Copy
[ec2-user ~]$ ec2-ami-tools-version
Note
If you receive a load error such as "cannot load such file -- ec2/amitools/version (LoadError)", complete the next step to add the location of your AMI tools installation to your RUBYLIB path.
(Optional) If you received an error in the previous step, add the location of your AMI tools installation to your RUBYLIB path.

Run the following command to determine the paths to add.

Copy
[ec2-user ~]$ rpm -qil ec2-ami-tools | grep ec2/amitools/version
/usr/lib/ruby/site_ruby/ec2/amitools/version.rb
/usr/lib64/ruby/site_ruby/ec2/amitools/version.rb
In the above example, the missing file from the previous load error is located at /usr/lib/ruby/site_ruby and /usr/lib64/ruby/site_ruby.

Add the locations from the previous step to your RUBYLIB path.

Copy
[ec2-user ~]$ export RUBYLIB=$RUBYLIB:/usr/lib/ruby/site_ruby:/usr/lib64/ruby/site_ruby
Verify your AMI tools installation using the ec2-ami-tools-version command.

Copy
[ec2-user ~]$ ec2-ami-tools-version
To set up the AMI tools using the .zip file

Install Ruby and unzip using the package manager for your Linux distribution, such as apt-get. For example:

Copy
[ec2-user ~]$ sudo apt-get update -y && sudo apt-get install -y ruby unzip
Download the .zip file using a tool such as wget or curl. For example:

Copy
[ec2-user ~]$ wget https://s3.amazonaws.com/ec2-downloads/ec2-ami-tools.zip
Unzip the files into a suitable installation directory, such as /usr/local/ec2.

Copy
[ec2-user ~]$ sudo mkdir -p /usr/local/ec2
$ sudo unzip ec2-ami-tools.zip -d /usr/local/ec2
Notice that the .zip file contains a folder ec2-ami-tools-x.x.x, where x.x.x is the version number of the tools (for example, ec2-ami-tools-1.5.7).

Set the EC2_AMITOOL_HOME environment variable to the installation directory for the tools. For example:

Copy
[ec2-user ~]$ export EC2_AMITOOL_HOME=/usr/local/ec2/ec2-ami-tools-x.x.x
Add the tools to your PATH environment variable. For example:

Copy
[ec2-user ~]$ export PATH=$EC2_AMITOOL_HOME/bin:$PATH
You can verify your AMI tools installation using the ec2-ami-tools-version command.

Copy
[ec2-user ~]$ ec2-ami-tools-version
Managing Signing Certificates

Certain commands in the AMI tools require a signing certificate (also known as X.509 certificate). You must create the certificate and then upload it to AWS. For example, you can use a third-party tool such as OpenSSL to create the certificate.

To create a signing certificate

Install and configure OpenSSL.

Create a private key using the openssl genrsa command and save the output to a .pem file. We recommend that you create a 2048- or 4096-bit RSA key.

Copy
openssl genrsa 2048 > private-key.pem
Generate a certificate using the openssl req command.

Copy
openssl req -new -x509 -nodes -sha256 -days 365 -key private-key.pem -outform PEM -out certificate.pem
To upload the certificate to AWS, use the upload-signing-certificate command.

Copy
aws iam upload-signing-certificate --user-name user-name --certificate-body file://path/to/certificate.pem
To list the certificates for a user, use the list-signing-certificates command:

Copy
aws iam list-signing-certificates --user-name user-name
To disable or re-enable a signing certificate for a user, use the update-signing-certificate command. The following command disables the certificate:

Copy
aws iam update-signing-certificate --certificate-id OFHPLP4ZULTHYPMSYEX7O4BEXAMPLE --status Inactive --user-name user-name
To delete a certificate, use the delete-signing-certificate command:

Copy
aws iam delete-signing-certificate --user-name user-name --certificate-id OFHPLP4ZULT

Creating an AMI from an Instance Store-Backed Instance

The following procedures are for creating an instance store-backed AMI from an instance store-backed instance. Before you begin, ensure that you've read the Prerequisites.

Topics

Creating an AMI from an Instance Store-Backed Amazon Linux Instance
Creating an AMI from an Instance Store-Backed Ubuntu Instance
Creating an AMI from an Instance Store-Backed Amazon Linux Instance

This section describes the creation of an AMI from an Amazon Linux instance. The following procedures may not work for instances running other Linux distributions. For Ubuntu-specific procedures, see Creating an AMI from an Instance Store-Backed Ubuntu Instance.

To prepare to use the AMI tools (HVM instances only)

The AMI tools require GRUB Legacy to boot properly. Use the following command to install GRUB:

Copy
[ec2-user ~]$ sudo yum install -y grub
Install the partition management packages with the following command:

Copy
[ec2-user ~]$ sudo yum install -y gdisk kpartx parted
To create an AMI from an instance store-backed Amazon Linux instance

This procedure assumes that you have satisfied the prerequisites in Prerequisites.

Upload your credentials to your instance. We use these credentials to ensure that only you and Amazon EC2 can access your AMI.

Create a temporary directory on your instance for your credentials as follows:

Copy
[ec2-user ~]$ mkdir /tmp/cert
This enables you to exclude your credentials from the created image.

Copy your X.509 certificate and corresponding private key from your computer to the /tmp/cert directory on your instance using a secure copy tool such as scp. The -i my-private-key.pem option in the following scp command is the private key you use to connect to your instance with SSH, not the X.509 private key. For example:

Copy
you@your_computer:~ $ scp -i my-private-key.pem /path/to/pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem /path/to/cert-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem ec2-user@ec2-203-0-113-25.compute-1.amazonaws.com:/tmp/cert/
pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem  100%  717     0.7KB/s   00:00
cert-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem  100%  685     0.7KB/s   00:00
Alternatively, because these are plain text files, you can open the certificate and key in a text editor and copy their contents into new files in /tmp/cert.

Prepare the bundle to upload to Amazon S3 by running the ec2-bundle-vol command from inside your instance. Be sure to specify the -e option to exclude the directory where your credentials are stored. By default, the bundle process excludes files that might contain sensitive information. These files include *.sw, *.swo, *.swp, *.pem, *.priv, *id_rsa*, *id_dsa* *.gpg, *.jks, */.ssh/authorized_keys, and */.bash_history. To include all of these files, use the --no-filter option. To include some of these files, use the --include option.

Important
By default, the AMI bundling process creates a compressed, encrypted collection of files in the /tmp directory that represents your root volume. If you do not have enough free disk space in /tmp to store the bundle, you need to specify a different location for the bundle to be stored with the -d /path/to/bundle/storage option. Some instances have ephemeral storage mounted at /mnt or /media/ephemeral0 that you can use, or you can also create, attach, and mount a new Amazon EBS volume to store the bundle.
You must run the ec2-bundle-vol command as root. For most commands, you can use sudo to gain elevated permissions, but in this case, you should run sudo -E su to keep your environment variables.

Copy
[ec2-user ~]$ sudo -E su
Note that bash prompt now identifies you as the root user, and that the dollar sign has been replaced by a hash tag, signalling that you are in a root shell:

[root ec2-user]#
To create the AMI bundle, run the ec2-bundle-vol command as follows:

Copy
[root ec2-user]# ec2-bundle-vol -k /tmp/cert/pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem -c /tmp/cert/cert-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem -u 123456789012 -r x86_64 -e /tmp/cert --partition gpt
It can take a few minutes to create the image. When this command completes, your /tmp (or non-default) directory contains the bundle (image.manifest.xml, plus multiple image.part.xx files).

Exit from the root shell.

Copy
[root ec2-user]# exit
(Optional) To add more instance store volumes, edit the block device mappings in the image.manifest.xml file for your AMI. For more information, see Block Device Mapping.

Create a backup of your image.manifest.xml file.

Copy
[ec2-user ~]$ sudo cp /tmp/image.manifest.xml /tmp/image.manifest.xml.bak
Reformat the image.manifest.xml file so that it is easier to read and edit.

Copy
[ec2-user ~]$ sudo xmllint --format /tmp/image.manifest.xml.bak > sudo /tmp/image.manifest.xml
Edit the block device mappings in image.manifest.xml with a text editor. The example below shows a new entry for the ephemeral1 instance store volume.

    <block_device_mapping>
      <mapping>
        <virtual>ami</virtual>
        <device>sda</device>
      </mapping>
      <mapping>
        <virtual>ephemeral0</virtual>
        <device>sdb</device>
      </mapping>
      <mapping>
        <virtual>ephemeral1</virtual>
        <device>sdc</device>
      </mapping>
      <mapping>
        <virtual>root</virtual>
        <device>/dev/sda1</device>
      </mapping>
    </block_device_mapping>
Save the image.manifest.xml file and exit your text editor.

To upload your bundle to Amazon S3, run the ec2-upload-bundle command as follows.

Copy
[ec2-user ~]$ ec2-upload-bundle -b my-s3-bucket/bundle_folder/bundle_name -m /tmp/image.manifest.xml -a your_access_key_id -s your_secret_access_key
Important
To register your AMI in a region other than US East (N. Virginia), you must specify both the target region with the --region option and a bucket path that already exists in the target region or a unique bucket path that can be created in the target region.
(Optional) After the bundle is uploaded to Amazon S3, you can remove the bundle from the /tmp directory on the instance using the following rm command:

Copy
[ec2-user ~]$ sudo rm /tmp/image.manifest.xml /tmp/image.part.* /tmp/image
Important
If you specified a path with the -d /path/to/bundle/storage option in Step 2, use that path instead of /tmp.
To register your AMI, run the register-image command as follows.

Copy
[ec2-user ~]$ aws ec2 register-image --image-location my-s3-bucket/bundle_folder/bundle_name/image.manifest.xml --name AMI_name --virtualization-type hvm
Important
If you previously specified a region for the ec2-upload-bundle command, specify that region again for this command.
Creating an AMI from an Instance Store-Backed Ubuntu Instance

This section describes the creation of an AMI from an Ubuntu Linux instance. The following procedures may not work for instances running other Linux distributions. For procedures specific to Amazon Linux, see Creating an AMI from an Instance Store-Backed Amazon Linux Instance.

To prepare to use the AMI Tools (HVM instances only)

The AMI tools require GRUB Legacy to boot properly. However, Ubuntu is configured to use GRUB 2. You must check to see that your instance uses GRUB Legacy, and if not, you need to install and configure it.

HVM instances also require partitioning tools to be installed for the AMI tools to work properly.

GRUB Legacy (version 0.9x or less) must be installed on your instance. Check to see if GRUB Legacy is present and install it if necessary.

Check the version of your GRUB installation.

Copy
ubuntu:~$ grub-install --version
grub-install (GRUB) 1.99-21ubuntu3.10
In this example, the GRUB version is greater than 0.9x, so GRUB Legacy must be installed. Proceed to Step 2. If GRUB Legacy is already present, you can skip to Step 2.

Install the grub package using the following command.

Copy
ubuntu:~$ sudo apt-get install -y grub
Verify that your instance is using GRUB Legacy.

Copy
ubuntu:~$ grub --version
grub (GNU GRUB 0.97)
Install the following partition management packages using the package manager for your distribution.

gdisk (some distributions may call this package gptfdisk instead)
kpartx
parted
Use the following command.

Copy
ubuntu:~$ sudo apt-get install -y gdisk kpartx parted
Check the kernel parameters for your instance.

Copy
ubuntu:~$ cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-3.2.0-54-virtual root=UUID=4f392932-ed93-4f8f-aee7-72bc5bb6ca9d ro console=ttyS0 xen_emul_unplug=unnecessary
Note the options following the kernel and root device parameters: ro, console=ttyS0, and xen_emul_unplug=unnecessary. Your options may differ.

Check the kernel entries in /boot/grub/menu.lst.

Copy
ubuntu:~$ grep ^kernel /boot/grub/menu.lst
kernel		/boot/vmlinuz-3.2.0-54-virtual root=LABEL=cloudimg-rootfs ro console=hvc0
kernel		/boot/vmlinuz-3.2.0-54-virtual root=LABEL=cloudimg-rootfs ro single
kernel		/boot/memtest86+.bin
Note that the console parameter is pointing to hvc0 instead of ttyS0 and that the xen_emul_unplug=unnecessary parameter is missing. Again, your options may differ.

Edit the /boot/grub/menu.lst file with your favorite text editor (such as vim or nano) to change the console and add the parameters you identified earlier to the boot entries.

Copy
title           Ubuntu 12.04.3 LTS, kernel 3.2.0-54-virtual
root            (hd0)
kernel          /boot/vmlinuz-3.2.0-54-virtual root=LABEL=cloudimg-rootfs ro console=ttyS0 xen_emul_unplug=unnecessary
initrd          /boot/initrd.img-3.2.0-54-virtual

title           Ubuntu 12.04.3 LTS, kernel 3.2.0-54-virtual (recovery mode)
root            (hd0)
kernel          /boot/vmlinuz-3.2.0-54-virtual root=LABEL=cloudimg-rootfs ro single console=ttyS0 xen_emul_unplug=unnecessary
initrd          /boot/initrd.img-3.2.0-54-virtual

title           Ubuntu 12.04.3 LTS, memtest86+
root            (hd0)
kernel          /boot/memtest86+.bin
Verify that your kernel entries now contain the correct parameters.

Copy
ubuntu:~$ grep ^kernel /boot/grub/menu.lst
kernel		/boot/vmlinuz-3.2.0-54-virtual root=LABEL=cloudimg-rootfs ro console=ttyS0 xen_emul_unplug=unnecessary
kernel		/boot/vmlinuz-3.2.0-54-virtual root=LABEL=cloudimg-rootfs ro single console=ttyS0 xen_emul_unplug=unnecessary
kernel		/boot/memtest86+.bin
[For Ubuntu 14.04 and later only] Starting with Ubuntu 14.04, instance store backed Ubuntu AMIs use a GPT partition table and a separate EFI partition mounted at /boot/efi. The ec2-bundle-vol command will not bundle this boot partition, so you need to comment out the /etc/fstab entry for the EFI partition as shown in the following example.

LABEL=cloudimg-rootfs   /        ext4   defaults        0 0
#LABEL=UEFI     /boot/efi       vfat    defaults        0 0
/dev/xvdb       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2
To create an AMI from an instance store-backed Ubuntu instance

This procedure assumes that you have satisfied the prerequisites in Prerequisites.

Upload your credentials to your instance. We use these credentials to ensure that only you and Amazon EC2 can access your AMI.

Create a temporary directory on your instance for your credentials as follows:

Copy
ubuntu:~$ mkdir /tmp/cert
This enables you to exclude your credentials from the created image.

Copy your X.509 certificate and private key from your computer to the /tmp/cert directory on your instance, using a secure copy tool such as scp. The -i my-private-key.pem option in the following scp command is the private key you use to connect to your instance with SSH, not the X.509 private key. For example:

Copy
you@your_computer:~ $ scp -i my-private-key.pem /path/to/pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem /path/to/cert-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem ec2-user@ec2-203-0-113-25.compute-1.amazonaws.com:/tmp/cert/
pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem  100%  717     0.7KB/s   00:00
cert-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem  100%  685     0.7KB/s   00:00
Alternatively, because these are plain text files, you can open the certificate and key in a text editor and copy their contents into new files in /tmp/cert.

Prepare the bundle to upload to Amazon S3 by running the ec2-bundle-vol command from your instance. Be sure to specify the -e option to exclude the directory where your credentials are stored. By default, the bundle process excludes files that might contain sensitive information. These files include *.sw, *.swo, *.swp, *.pem, *.priv, *id_rsa*, *id_dsa* *.gpg, *.jks, */.ssh/authorized_keys, and */.bash_history. To include all of these files, use the --no-filter option. To include some of these files, use the --include option.

Important
By default, the AMI bundling process creates a compressed, encrypted collection of files in the /tmp directory that represents your root volume. If you do not have enough free disk space in /tmp to store the bundle, you need to specify a different location for the bundle to be stored with the -d /path/to/bundle/storage option. Some instances have ephemeral storage mounted at /mnt or /media/ephemeral0 that you can use, or you can also create, attach, and mount a new Amazon EBS volume to store the bundle.
You must run the ec2-bundle-vol command needs as root. For most commands, you can use sudo to gain elevated permissions, but in this case, you should run sudo -E su to keep your environment variables.

Copy
ubuntu:~$ sudo -E su
Note that bash prompt now identifies you as the root user, and that the dollar sign has been replaced by a hash tag, signalling that you are in a root shell:

root@ubuntu:#
To create the AMI bundle, run the ec2-bundle-vol command as follows.

Copy
root@ubuntu:# ec2-bundle-vol -k /tmp/cert/pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem -c /tmp/cert/cert-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem -u your_aws_account_id -r x86_64 -e /tmp/cert --partition gpt
Important
For Ubuntu 14.04 and later HVM instances, add the --partition mbr flag to bundle the boot instructions properly; otherwise, your newly-created AMI will not boot.
It can take a few minutes to create the image. When this command completes, your tmp directory contains the bundle (image.manifest.xml, plus multiple image.part.xx files).

Exit from the root shell.

Copy
root@ubuntu:# exit
(Optional) To add more instance store volumes, edit the block device mappings in the image.manifest.xml file for your AMI. For more information, see Block Device Mapping.

Create a backup of your image.manifest.xml file.

Copy
ubuntu:~$ sudo cp /tmp/image.manifest.xml /tmp/image.manifest.xml.bak
Reformat the image.manifest.xml file so that it is easier to read and edit.

Copy
ubuntu:~$ sudo xmllint --format /tmp/image.manifest.xml.bak > /tmp/image.manifest.xml
Edit the block device mappings in image.manifest.xml with a text editor. The example below shows a new entry for the ephemeral1 instance store volume.

    <block_device_mapping>
      <mapping>
        <virtual>ami</virtual>
        <device>sda</device>
      </mapping>
      <mapping>
        <virtual>ephemeral0</virtual>
        <device>sdb</device>
      </mapping>
      <mapping>
        <virtual>ephemeral1</virtual>
        <device>sdc</device>
      </mapping>
      <mapping>
        <virtual>root</virtual>
        <device>/dev/sda1</device>
      </mapping>
    </block_device_mapping>
Save the image.manifest.xml file and exit your text editor.

To upload your bundle to Amazon S3, run the ec2-upload-bundle command as follows.

Copy
ubuntu:~$ ec2-upload-bundle -b my-s3-bucket/bundle_folder/bundle_name -m /tmp/image.manifest.xml -a your_access_key_id -s your_secret_access_key
Important
If you intend to register your AMI in a region other than US East (N. Virginia), you must specify both the target region with the --region option and a bucket path that already exists in the target region or a unique bucket path that can be created in the target region.
(Optional) After the bundle is uploaded to Amazon S3, you can remove the bundle from the /tmp directory on the instance using the following rm command:

Copy
ubuntu:~$ sudo rm /tmp/image.manifest.xml /tmp/image.part.* /tmp/image
Important
If you specified a path with the -d /path/to/bundle/storage option in Step 2, use that same path below, instead of /tmp.
To register your AMI, run the register-image AWS CLI command as follows.

Copy
ubuntu:~$ aws ec2 register-image my-s3-bucket/bundle_folder/bundle_name/image.manifest.xml --name AMI_name --virtualization-type hvm
Important
If you previously specified a region for the ec2-upload-bundle command, specify that region again for this command.
[Ubuntu 14.04 and later] Uncomment the EFI entry in /etc/fstab; otherwise, your running instance will not be able to reboot.

Converting your Instance Store-Backed AMI to an Amazon EBS-Backed AMI

You can convert an instance store-backed Linux AMI that you own to an Amazon EBS-backed Linux AMI.

Important
You can't convert an instance store-backed Windows AMI to an Amazon EBS-backed Windows AMI and you cannot convert an AMI that you do not own.
To convert an instance store-backed AMI to an Amazon EBS-backed AMI

Launch an Amazon Linux instance from an Amazon EBS-backed AMI. For more information, see Launching an Instance. Amazon Linux instances have the AWS CLI and AMI tools pre-installed.

Upload the X.509 private key that you used to bundle your instance store-backed AMI to your instance. We use this key to ensure that only you and Amazon EC2 can access your AMI.

Create a temporary directory on your instance for your X.509 private key as follows:

Copy
[ec2-user ~]$ mkdir /tmp/cert
Copy your X.509 private key from your computer to the /tmp/cert directory on your instance, using a secure copy tool such as scp. The my-private-key parameter in the following command is the private key you use to connect to your instance with SSH. For example:

Copy
you@your_computer:~ $ scp -i my-private-key.pem /path/to/pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem ec2-user@ec2-203-0-113-25.compute-1.amazonaws.com:/tmp/cert/
pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem  100%  717     0.7KB/s   00:00
Set environment variables for your AWS access key and secret key.

Copy
[ec2-user ~]$ export AWS_ACCESS_KEY_ID=your_access_key_id
[ec2-user ~]$ export AWS_SECRET_ACCESS_KEY=your_secret_access_key
Prepare an Amazon EBS volume for your new AMI.

Create an empty Amazon EBS volume in the same Availability Zone as your instance using the create-volume command. Note the volume ID in the command output.

Important
This Amazon EBS volume must be the same size or larger than the original instance store root volume.
Copy
[ec2-user ~]$ aws ec2 create-volume --size 10 --region us-west-2 --availability-zone us-west-2b						
Attach the volume to your Amazon EBS-backed instance using the attach-volume command.

Copy
[ec2-user ~]$ aws ec2 attach-volume --volume-id volume_id --instance-id instance_id --device /dev/sdb --region us-west-2
Create a folder for your bundle.

Copy
[ec2-user ~]$ mkdir /tmp/bundle
Download the bundle for your instance store-based AMI to /tmp/bundle using the ec2-download-bundle command.

Copy
[ec2-user ~]$ ec2-download-bundle -b my-s3-bucket/bundle_folder/bundle_name -m image.manifest.xml -a $AWS_ACCESS_KEY -s $AWS_SECRET_KEY --privatekey /path/to/pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem -d /tmp/bundle
Reconstitute the image file from the bundle using the ec2-unbundle command.

Change directories to the bundle folder.

Copy
[ec2-user ~]$ cd /tmp/bundle/
Run the ec2-unbundle command.

Copy
[ec2-user bundle]$ ec2-unbundle -m image.manifest.xml --privatekey /path/to/pk-HKZYKTAIG2ECMXYIBH3HXV4ZBEXAMPLE.pem
Copy the files from the unbundled image to the new Amazon EBS volume.

Copy
[ec2-user bundle]$ sudo dd if=/tmp/bundle/image of=/dev/sdb bs=1M
Probe the volume for any new partitions that were unbundled.

Copy
[ec2-user bundle]$ sudo partprobe /dev/sdb1
List the block devices to find the device name to mount.

Copy
[ec2-user bundle]$ lsblk
NAME         MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
/dev/sda    202:0    0   8G  0 disk
└─/dev/sda1 202:1    0   8G  0 part /
/dev/sdb    202:80   0  10G  0 disk
└─/dev/sdb1 202:81   0  10G  0 part
In this example, the partition to mount is /dev/sdb1, but your device name will likely be different. If your volume is not partitioned, then the device to mount will be similar to /dev/sdb (without a device partition trailing digit).

Create a mount point for the new Amazon EBS volume and mount the volume.

Copy
[ec2-user bundle]$ sudo mkdir /mnt/ebs
[ec2-user bundle]$ sudo mount /dev/sdb1 /mnt/ebs
Open the /etc/fstab file on the EBS volume with your favorite text editor (such as vim or nano) and remove any entries for instance store (ephemeral) volumes. Because the Amazon EBS volume is mounted on /mnt/ebs, the fstab file is located at /mnt/ebs/etc/fstab.

Copy
[ec2-user bundle]$ sudo nano /mnt/ebs/etc/fstab
#
LABEL=/     /           ext4    defaults,noatime  1   1
tmpfs       /dev/shm    tmpfs   defaults        0   0
devpts      /dev/pts    devpts  gid=5,mode=620  0   0
sysfs       /sys        sysfs   defaults        0   0
proc        /proc       proc    defaults        0   0
/dev/sdb        /media/ephemeral0       auto    defaults,comment=cloudconfig    0       2
In this example, the last line should be removed.

Unmount the volume and detach it from the instance.

Copy
[ec2-user bundle]$ sudo umount /mnt/ebs
[ec2-user bundle]$ aws ec2 detach-volume --volume-id volume_id --region us-west-2
Create an AMI from the new Amazon EBS volume as follows.

Create a snapshot of the new Amazon EBS volume.

Copy
[ec2-user bundle]$ aws ec2 create-snapshot --region us-west-2 --description "your_snapshot_description" --volume-id volume_id
Check to see that your snapshot is complete.

Copy
[ec2-user bundle]$ aws ec2 describe-snapshots --region us-west-2 --snapshot-id snapshot_id
Identify the processor architecture, virtualization type, and the kernel image (aki) used on the original AMI with the describe-images command. You need the AMI ID of the original instance store-backed AMI for this step.

Copy
[ec2-user bundle]$ aws ec2 describe-images --region us-west-2 --image-id ami-id --output text
IMAGES	x86_64	amazon/amzn-ami-pv-2013.09.2.x86_64-s3	ami-8ef297be	amazon	available	public	machine	aki-fc8f11cc	instance-store	paravirtual	xen
In this example, the architecture is x86_64 and the kernel image ID is aki-fc8f11cc. Use these values in the following step. If the output of the above command also lists an ari ID, take note of that as well.

Register your new AMI with the snapshot ID of your new Amazon EBS volume and the values from the previous step. If the previous command output listed an ari ID, include that in the following command with --ramdisk-id ari_id.

Copy
[ec2-user bundle]$ aws ec2 register-image --region us-west-2 --name your_new_ami_name --block-device-mappings Ebs={SnapshotId=snapshot_id} --virtualization-type hvm --architecture x86_64 --kernel-id aki-fc8f11cc
(Optional) After you have tested that you can launch an instance from your new AMI, you can delete the Amazon EBS volume that you created for this procedure.

Copy
aws ec2 delete-volume --volume-id volume_id

AMIs with Encrypted Snapshots

AMIs that are backed by Amazon EBS snapshots can take advantage of Amazon EBS encryption. Snapshots of both data and root volumes can be encrypted and attached to an AMI.

EC2 instances with encrypted volumes are launched from AMIs in the same way as other instances.

The CopyImage action can be used to create an AMI with encrypted snapshots from an AMI with unencrypted snapshots. By default, CopyImage preserves the encryption status of source snapshots when creating destination copies. However, you can configure the parameters of the copy process to also encrypt the destination snapshots.

Snapshots can be encrypted with either your default AWS Key Management Service customer master key (CMK), or with a custom key that you specify. You must in all cases have permission to use the selected key. If you have an AMI with encrypted snapshots, you can choose to re-encrypt them with a different encryption key as part of the CopyImage action. CopyImage accepts only one key at a time and encrypts all of an image's snapshots (whether root or data) to that key. However, it is possible to manually build an AMI with snapshots encrypted to multiple keys.

Support for creating AMIs with encrypted snapshots is accessible through the Amazon EC2 console, Amazon EC2 API, or the AWS CLI.

The encryption parameters of CopyImage are available in all regions where AWS KMS is available.

AMI Scenarios Involving Encrypted EBS Snapshots

You can copy an AMI and simultaneously encrypt its associated EBS snapshots using the AWS Management Console or the command line.

Copying an AMI with an Encrypted Data Snapshot

In this scenario, an EBS-backed AMI has an unencrypted root snapshot and an encrypted data snapshot, shown in step 1. The CopyImage action is invoked in step 2 without encryption parameters. As a result, the encryption status of each snapshot is preserved, so that the destination AMI, in step 3, is also backed by an unencrypted root snapshot and an encrypted data snapshot. Though the snapshots contain the same data, they are distinct from each other and you will incur storage costs for the snapshots in both AMIs, as well as charges for any instances you launch from either AMI.


						Copy an AMI with encrypted data snapshot
					
You can perform a simple copy such as this using either the Amazon EC2 console or the command line. For more information, see Copying an AMI.

Copying an AMI Backed by An Encrypted Root Snapshot

In this scenario, an Amazon EBS-backed AMI has an encrypted root snapshot, shown in step 1. The CopyImage action is invoked in step 2 without encryption parameters. As a result, the encryption status of the snapshot is preserved, so that the destination AMI, in step 3, is also backed by an encrypted root snapshot. Though the root snapshots contain identical system data, they are distinct from each other and you will incur storage costs for the snapshots in both AMIs, as well as charges for any instances you launch from either AMI.


						Copy an AMI backed by encrypted root snapshot
					
You can perform a simple copy such as this using either the Amazon EC2 console or the command line. For more information, see Copying an AMI.

Creating an AMI with Encrypted Root Snapshot from an Unencrypted AMI

In this scenario, an Amazon EBS-backed AMI has an unencrypted root snapshot, shown in step 1, and an AMI is created with an encrypted root snapshot, shown in step 3. The CopyImage action in step 2 is invoked with two encryption parameters, including the choice of a CMK. As a result, the encryption status of the root snapshot changes, so that the target AMI is backed by a root snapshot containing the same data as the source snapshot, but encrypted using the specified key. You will incur storage costs for the snapshots in both AMIs, as well as charges for any instances you launch from either AMI.


						Create an AMI from unencrypted AMI
					
You can perform a copy and encrypt operation such as this using either the Amazon EC2 console or the command line. For more information, see Copying an AMI.

Creating an AMI with an Encrypted Root Snapshot from a Running Instance

In this scenario, an AMI is created from a running EC2 instance. The running instance in step 1 has an encrypted root volume, and the created AMI in step 3 has a root snapshot encrypted to the same key as the source volume. The CreateImage action has exactly the same behavior whether or not encryption is present.


						Create an AMI from instance with encrypted root snapshot
					
You can create an AMI from a running Amazon EC2 instance (with or without encrypted volumes) using either the Amazon EC2 console or the command line. For more information, see Creating an Amazon EBS-Backed Linux AMI.

Creating an AMI with Unique CMKs for Each Encrypted Snapshot

This scenario starts with an AMI backed by a root-volume snapshot (encrypted to key #1), and finishes with an AMI that has two additional data-volume snapshots attached (encrypted to key #2 and key #3). The CopyImage action cannot apply more than one encryption key in a single operation. However, you can create an AMI from an instance that has multiple attached volumes encrypted to different keys. The resulting AMI has snapshots encrypted to those keys and any instance launched from this new AMI also has volumes encrypted to those keys.

The steps of this example procedure correspond to the following diagram.

Start with the source AMI backed by vol. #1 (root) snapshot, which is encrypted with key #1.

Launch an EC2 instance from the source AMI.

Create EBS volumes vol. #2 (data) and vol. #3 (data), encrypted to key #2 and key #3 respectively.

Attach the encrypted data volumes to the EC2 instance.

The EC2 instance now has an encrypted root volume as well as two encrypted data volumes, all using different keys.

Use the CreateImage action on the EC2 instance.

The resulting target AMI contains encrypted snapshots of the three EBS volumes, all using different keys.


						Create AMIs with unique CMKs
					
You can carry out this procedure using either the Amazon EC2 console or the command line. For more information, see the following topics:

Launch Your Instance
Creating an Amazon EBS-Backed Linux AMI.
Amazon EBS Volumes
AWS Key Management in the AWS Key Management Service Developer Guide

Copying an AMI

You can copy an Amazon Machine Image (AMI) within or across an AWS region using the AWS Management Console, the AWS command line tools or SDKs, or the Amazon EC2 API, all of which support the CopyImage action. You can copy both Amazon EBS-backed AMIs and instance store-backed AMIs. You can copy AMIs with encrypted snapshots and encrypted AMIs.

Copying a source AMI results in an identical but distinct target AMI with its own unique identifier. In the case of an Amazon EBS-backed AMI, each of its backing snapshots is, by default, copied to an identical but distinct target snapshot. (The one exception is when you choose to encrypt the snapshot.) You can change or deregister the source AMI with no effect on the target AMI. The reverse is also true.

There are no charges for copying an AMI. However, standard storage and data transfer rates apply.

AWS does not copy launch permissions, user-defined tags, or Amazon S3 bucket permissions from the source AMI to the new AMI. After the copy operation is complete, you can apply launch permissions, user-defined tags, and Amazon S3 bucket permissions to the new AMI.

Permissions

If you use an IAM user to copy an instance-store-backed AMI, the user must have the following Amazon S3 permissions: s3:CreateBucket, s3:GetBucketAcl, s3:ListAllMyBuckets, s3:GetObject, s3:PutObject, and s3:PutObjectAcl.

The following example policy allows the user to copy the AMI source in the specified bucket to the specified region.

Copy
{
    "Version": "2016-12-09",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": [
                "arn:aws:s3:::*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": [
                "arn:aws:s3:::ami-source-bucket/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
              "s3:CreateBucket",
              "s3:GetBucketAcl",
              "s3:PutObjectAcl",
              "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::amis-for-123456789012-in-us-east-1*"
            ]
        }
    ]
}
Cross-Region AMI Copy

Copying an AMI across geographically diverse regions provides the following benefits:

Consistent global deployment: Copying an AMI from one region to another enables you to launch consistent instances based from the same AMI into different regions.
Scalability: You can more easily design and build world-scale applications that meet the needs of your users, regardless of their location.
Performance: You can increase performance by distributing your application, as well as locating critical components of your application in closer proximity to your users. You can also take advantage of region-specific features, such as instance types or other AWS services.
High availability: You can design and deploy applications across AWS regions, to increase availability.
The following diagram shows the relations among a source AMI and two copied AMIs in different regions, as well as the EC2 instances launched from each. When you launch an instance from an AMI, it resides in the same region where the AMI resides. If you make changes to the source AMI and want those changes to be reflected in the AMIs in the target regions, you must recopy the source AMI to the target regions.


						AMIs copied in different regions
					
When you first copy an instance store-backed AMI to a region, we create an Amazon S3 bucket for the AMIs copied to that region. All instance store-backed AMIs that you copy to that region are stored in this bucket. The bucket names have the following format: amis-for-account-in-region-hash. For example: amis-for-123456789012-in-us-east-2-yhjmxvp6.

Prerequisite

Prior to copying an AMI, you must ensure that the contents of the source AMI are updated to support running in a different region. For example, you should update any database connection strings or similar application configuration data to point to the appropriate resources. Otherwise, instances launched from the new AMI in the destination region may still use the resources from the source region, which can impact performance and cost.

Limit

Destination regions are limited to 50 concurrent AMI copies at a time, with no more than 25 of those coming from a single source region. To request an increase to this limit, see Amazon EC2 Service Limits.

Cross-Account AMI Copy

You can share an AMI with another AWS account. Sharing an AMI does not affect the ownership of the AMI. The owning account is charged for the storage in the region. For more information, see Sharing an AMI with Specific AWS Accounts.

If you copy an AMI that has been shared with your account, you are the owner of the target AMI in your account. The owner of the source AMI is charged standard Amazon EBS or Amazon S3 transfer fees, and you are charged for the storage of the target AMI in the destination region.

Resource Permissions

To copy an AMI that was shared with you from another account, the owner of the source AMI must grant you read permissions for the storage that backs the AMI, either the associated EBS snapshot (for an Amazon EBS-backed AMI) or an associated S3 bucket (for an instance store-backed AMI).

Limits

You can't copy an encrypted AMI that was shared with you from another account. Instead, if the underlying snapshot and encryption key were shared with you, you can copy the snapshot while re-encrypting it with a key of your own. You own the copied snapshot, and can register it as a new AMI.
You can't copy an AMI with an associated billingProduct code that was shared with you from another account. This includes Windows AMIs and AMIs from the AWS Marketplace. To copy a shared AMI with a billingProduct code, launch an EC2 instance in your account using the shared AMI and then create an AMI from the instance. For more information, see Creating an Amazon EBS-Backed Linux AMI.
Encryption and AMI Copy

Encrypting during AMI copy applies only to Amazon EBS-backed AMIs. Because an instance-store-backed AMIs does not rely on snapshots, you cannot use AMI copy to change its encryption status.

You can use AMI copy to create a new AMI backed by encrypted Amazon EBS snapshots. If you invoke encryption while copying an AMI, each snapshot taken of its associated Amazon EBS volumes—including the root volume—is encrypted using a key that you specify. For more information about using AMIs with encrypted snapshots, see AMIs with Encrypted Snapshots.

By default, the backing snapshot of an AMI is copied with its original encryption status. Copying an AMI backed by an unencrypted snapshot results in an identical target snapshot that is also unencrypted. If the source AMI is backed by an encrypted snapshot, copying it results in a target snapshot encrypted to the specified key. Copying an AMI backed by multiple snapshots preserves the source encryption status in each target snapshot. For more information about copying AMIs with multiple snapshots, see AMIs with Encrypted Snapshots.

The following table shows encryption support for various scenarios. Note that while it is possible to copy an unencrypted snapshot to yield an encrypted snapshot, you cannot copy an encrypted snapshot to yield an unencrypted one.

Scenario	Description	Supported
1	Unencrypted-to-unencrypted	Yes
2	Encrypted-to-encrypted	Yes
3	Unencrypted-to-encrypted	Yes
4	Encrypted-to-unencrypted	No
Copy an unencrypted source AMI to an unencrypted target AMI

In this scenario, a copy of an AMI with an unencrypted single backing snapshot is created in the specified geographical region (not shown). Although this diagram shows an AMI with a single backing snapshot, you can also copy an AMI with multiple snapshots. The encryption status of each snapshot is preserved. Therefore, an unencrypted snapshot in the source AMI results in an unencrypted snapshot in the target AMI, and an encrypted shapshot in the source AMI results in an encrypted snapshot in the target AMI.


					Copy an unencrypted source AMI
				
Copy an encrypted source AMI to an encrypted target AMI

Although this scenario involves encrypted snapshots, it is functionally equivalent to the previous scenario. If you apply encryption while copying a multi-snapshot AMI, all of the target snapshots are encrypted using the specified key or the default key if none is specified.


					Copy an encrypted source AMI
				
Copy an unencrypted source AMI to an encrypted target AMI

In this scenario, copying an AMI changes the encryption status of the destination image, for instance, by encrypting an unencrypted snapshot, or re-encrypting an encrypted snapshot with a different key. To apply encryption during the copy, you must provide an encryption flag and key. Volumes created from the target snapshot are accessible only using this key.


					Copy an unencrypted source AMI to encrypted target AMI
				
Copying an AMI

You can copy an AMI as follows.

Prerequisite

Create or obtain an AMI backed by an Amazon EBS snapshot. Note that you can use the Amazon EC2 console to search a wide variety of AMIs provided by AWS. For more information, see Creating an Amazon EBS-Backed Linux AMI and Finding a Linux AMI.

To copy an AMI using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the console navigation bar, select the region that contains the AMI. In the navigation pane, choose Images, AMIs to display the list of AMIs available to you in the region.

Select the AMI to copy and choose Actions, Copy AMI.

On the AMI Copy page, specify the following information and then choose Copy AMI:

Destination region: The region into which to copy the AMI.
Name: A name for the new AMI. You can include operating system information in the name, as we do not provide this information when displaying details about the AMI.
Description: By default, the description includes information about the source AMI so that you can distinguish a copy from its original. You can change this description as needed.
Encryption: Select this field to encrypt the target snapshots, or to re-encrypt them using a different key.
Master Key: The KMS key to used to encrypt the target snapshots.
We display a confirmation page to let you know that the copy operation has been initiated and to provide you with the ID of the new AMI.

To check on the progress of the copy operation immediately, follow the provided link. To check on the progress later, choose Done, and then when you are ready, use the navigation bar to switch to the target region (if applicable) and locate your AMI in the list of AMIs.

The initial status of the target AMI is pending and the operation is complete when the status is available.

To copy an AMI using the AWS CLI

You can copy an AMI using the copy-image command. You must specify both the source and destination regions. You specify the source region using the --source-region parameter. You can specify the destination region using either the --region parameter or an environment variable. For more information, see Configuring the AWS Command Line Interface.

When you encrypt a target snapshot during copying, you must specify these additional parameters: --encrypted and --kms-key-id.

To copy an AMI using the Tools for Windows PowerShell

You can copy an AMI using the Copy-EC2Image command. You must specify both the source and destination regions. You specify the source region using the -SourceRegion parameter. You can specify the destination region using either the -Region parameter or the Set-AWSDefaultRegion command. For more information, see Specifying AWS Regions.

When you encrypt a target snapshot during copying, you must specify these additional parameters: -Encrypted and -KmsKeyId.

Stopping a Pending AMI Copy Operation

You can stop a pending AMI copy as follows.

To stop an AMI copy operation using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the destination region from the region selector.

In the navigation pane, choose AMIs.

Select the AMI to stop copying and choose Actions and Deregister.

When asked for confirmation, choose Continue.

To stop an AMI copy operation using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

deregister-image (AWS CLI)
Unregister-EC2Image (AWS Tools for Windows PowerShell)

Deregistering Your AMI

You can deregister an AMI when you have finished using it. After you deregister an AMI, you can't use it to launch new instances.

When you deregister an AMI, it doesn't affect any instances that you've already launched from the AMI. You'll continue to incur usage costs for these instances. Therefore, if you are finished with these instances, you should terminate them.

The procedure that you'll use to clean up your AMI depends on whether it is backed by Amazon EBS or instance store. (Note that the only Windows AMIs that can be backed by instance store are those for Windows Server 2003.)

Contents

Cleaning Up Your Amazon EBS-Backed AMI
Cleaning Up Your Instance Store-Backed AMI
Cleaning Up Your Amazon EBS-Backed AMI

When you deregister an Amazon EBS-backed AMI, it doesn't affect the snapshot that was created for the root volume of the instance during the AMI creation process. You'll continue to incur storage costs for this snapshot. Therefore, if you are finished with the snapshot, you should delete it.

The following diagram illustrates the process for cleaning up your Amazon EBS-backed AMI.


          Process to clean up your Amazon EBS-backed AMI
        
To clean up your Amazon EBS-backed AMI

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose AMIs. Select the AMI, and take note of its ID — this can help you find the correct snapshot in the next step. Choose Actions, and then Deregister. When prompted for confirmation, choose Continue.

Note
It may take a few minutes before the console removes the AMI from the list. Choose Refresh to refresh the status.
In the navigation pane, choose Snapshots, and select the snapshot (look for the AMI ID in the Description column). Choose Actions, and then choose Delete Snapshot. When prompted for confirmation, choose Yes, Delete.

(Optional) If you are finished with an instance that you launched from the AMI, terminate it. In the navigation pane, choose Instances. Select the instance, choose Actions, then Instance State, and then Terminate. When prompted for confirmation, choose Yes, Terminate.

Cleaning Up Your Instance Store-Backed AMI

When you deregister an instance store-backed AMI, it doesn't affect the files that you uploaded to Amazon S3 when you created the AMI. You'll continue to incur usage costs for these files in Amazon S3. Therefore, if you are finished with these files, you should delete them.

The following diagram illustrates the process for cleaning up your instance store-backed AMI.


          Process to clean up your instance store-backed AMI
        
To clean up your instance store-backed AMI

Deregister the AMI using the deregister-image command as follows.

Copy
aws ec2 deregister-image --image-id ami_id
Delete the bundle in Amazon S3 using the ec2-delete-bundle (AMI tools) command as follows.

Copy
ec2-delete-bundle -b myawsbucket/myami -a your_access_key_id -s your_secret_access_key -p image
(Optional) If you are finished with an instance that you launched from the AMI, you can terminate it using the terminate-instances command as follows.

Copy
aws ec2 terminate-instances --instance-ids instance_id
(Optional) If you are finished with the Amazon S3 bucket that you uploaded the bundle to, you can delete the bucket. To delete an Amazon S3 bucket, open the Amazon S3 console, select the bucket, choose Actions, and then choose Delete.

Amazon Linux

Amazon Linux is provided by Amazon Web Services (AWS). It is designed to provide a stable, secure, and high-performance execution environment for applications running on Amazon EC2. It also includes packages that enable easy integration with AWS, including launch configuration tools and many popular AWS libraries and tools. AWS provides ongoing security and maintenance updates to all instances running Amazon Linux.

Note
The Amazon Linux AMI repository structure is configured to deliver a continuous flow of updates that allow you to roll from one version of the Amazon Linux AMI to the next. To lock existing instances to their current version, see Repository Configuration.
To launch an Amazon Linux instance, use an Amazon Linux AMI. AWS provides Amazon Linux AMIs to Amazon EC2 users at no additional cost.

Contents

Finding an Amazon Linux AMI
Subscribing to Amazon Linux AMI Notifications
Launching and Connecting to an Amazon Linux Instance
Identifying Amazon Linux AMI Images
Included AWS Command Line Tools
cloud-init
Repository Configuration
Adding Packages
Accessing Source Packages for Reference
Developing Applications
Instance Store Access
Product Life Cycle
Security Updates
Support
Finding an Amazon Linux AMI

For a list of the latest Amazon Linux AMIs, see Amazon Linux AMIs.

Subscribing to Amazon Linux AMI Notifications

If you want to be notified when new Amazon Linux AMIs are released, you can subscribe to these notifications using Amazon SNS.

To subscribe to Amazon Linux AMI notifications

Open the Amazon SNS console at https://console.aws.amazon.com/sns/v2/home.

In the navigation bar, change the region to US East (N. Virginia), if necessary. You must select this region because the SNS notification that you are subscribing to was created in this region.

In the navigation pane, choose Subscriptions.

Choose Create subscription.

For the Create subscription dialog box, do the following:

For Topic ARN, copy and paste the following Amazon Resource Name (ARN): arn:aws:sns:us-east-1:137112412989:amazon-linux-ami-updates.

For Protocol, choose Email.

For Endpoint, type an email address that you can use to receive the notifications.

Choose Create subscription.

You'll receive a confirmation email with the subject line AWS Notification - Subscription Confirmation. Open the email and click Confirm subscription to complete your subscription.

Whenever Amazon Linux AMIs are released, we send notifications to the subscribers of the amazon-linux-ami-updates topic. If you no longer want to receive these notifications, use the following procedure to unsubscribe.

To unsubscribe from Amazon Linux AMI notifications

Open the Amazon SNS console at https://console.aws.amazon.com/sns/v2/home.

In the navigation bar, change the region to US East (N. Virginia), if necessary. You must use this region because the SNS notification was created in this region.

In the navigation pane, choose Subscriptions.

Select the subscription and then choose Actions, Delete subscriptions When prompted for confirmation, choose Delete.

Launching and Connecting to an Amazon Linux Instance

After locating your desired AMI, note the AMI ID. You can use the AMI ID to launch and then connect to your instance.

Amazon Linux does not allow remote root SSH by default. Also, password authentication is disabled to prevent brute-force password attacks. To enable SSH logins to an Amazon Linux instance, you must provide your key pair to the instance at launch. You must also set the security group used to launch your instance to allow SSH access. By default, the only account that can log in remotely using SSH is ec2-user; this account also has sudo privileges. If you want to enable remote root log in, please be aware that it is less secure than relying on key pairs and a secondary user.

For information about launching and using your Amazon Linux instance, see Launch Your Instance. For information about connecting to your Amazon Linux instance, see Connecting to Your Linux Instance.

Identifying Amazon Linux AMI Images

Each image contains a unique /etc/image-id that identifies the AMI. This file contains information about the image.

The following is an example of the /etc/image-id file:

Copy
[ec2-user ~]$ cat /etc/image-id
image_name="amzn-ami-hvm"
image_version="2017.03"
image_arch="x86_64"
image_file="amzn-ami-hvm-2017.03.0.20170401-x86_64.ext4.gpt"
image_stamp="26a3-ed31"
image_date="20170402053945"
recipe_name="amzn ami"
recipe_id="47cfa924-413c-d460-f4f2-2af7-feb6-9e37-7c9f1d2b"
The image_name, image_version, and image_arch items come from the build recipe that Amazon used to construct the image. The image_stamp is simply a unique random hex value generated during image creation. The image_date item is in YYYYMMDDhhmmss format, and is the UTC time of image creation. The recipe_name and recipe_id refer to the name and ID of the build recipe Amazon used to construct the image, which identifies the current running version of Amazon Linux. This file will not change as you install updates from the yum repository.

Amazon Linux contains an /etc/system-release file that specifies the current release that is installed. This file is updated through yum and is part of the system-release RPM.

The following is an example of an /etc/system-release file:

Copy
[ec2-user ~]$ cat /etc/system-release
Amazon Linux AMI release 2017.03
Amazon Linux also contains a machine readable version of the /etc/system-release file found in /etc/system-release-cpe and follows the CPE specification from MITRE (CPE).

Included AWS Command Line Tools

The following popular command line tools for AWS integration and usage have been included in Amazon Linux or in the default repositories:

aws-amitools-ec2
aws-apitools-as
aws-apitools-cfn
aws-apitools-ec2
aws-apitools-elb
aws-apitools-iam
aws-apitools-mon
aws-apitools-rds
aws-cfn-bootstrap
aws-cli
aws-scripts-ses
The minimal versions of Amazon Linux (amzn-ami-minimal-*) do not contain the above packages; however, they are available in the default yum repositories, and you can install them with the following command:

Copy
[ec2-user ~]$ sudo yum install -y package_name
For instances launched using IAM roles, a simple script has been included to prepare AWS_CREDENTIAL_FILE, JAVA_HOME, AWS_PATH, PATH, and product-specific environment variables after a credential file has been installed to simplify the configuration of these tools.

Also, to allow the installation of multiple versions of the API and AMI tools, we have placed symbolic links to the desired versions of these tools in /opt/aws, as described here:

/opt/aws/bin
Symbolic links to /bin directories in each of the installed tools directories.

/opt/aws/{apitools|amitools}
Products are installed in directories of the form name-version and a symbolic link name that is attached to the most recently installed version.

/opt/aws/{apitools|amitools}/name/environment.sh
Used by /etc/profile.d/aws-apitools-common.sh to set product-specific environment variables, such as EC2_HOME.

cloud-init

The cloud-init package is an open source application built by Canonical that is used to bootstrap Linux images in a cloud computing environment, such as Amazon EC2. Amazon Linux contains a customized version of cloud-init. It enables you to specify actions that should happen to your instance at boot time. You can pass desired actions to cloud-init through the user data fields when launching an instance. This means you can use common AMIs for many use cases and configure them dynamically at startup. Amazon Linux also uses cloud-init to perform initial configuration of the ec2-user account.

For more information about cloud-init, see http://cloudinit.readthedocs.org/en/latest/.

Amazon Linux uses the cloud-init actions found in /etc/cloud/cloud.cfg.d and /etc/cloud/cloud.cfg. You can create your own cloud-init action files in /etc/cloud/cloud.cfg.d. All files in this directory are read by cloud-init. They are read in lexical order, and later files overwrite values in earlier files.

The cloud-init package performs these (and other) common configuration tasks for instances at boot:

Set the default locale
Set the hostname
Parse and handle user data
Generate host private SSH keys
Add a user's public SSH keys to .ssh/authorized_keys for easy login and administration
Prepare the yum repositories for package management
Handle package actions defined in user data
Execute user scripts found in user data
Mount instance store volumes if applicable
By default, the ephemeral0 instance store volume is mounted at /media/ephemeral0 if it is present and contains a valid file system; otherwise, it is not mounted.
By default, any swap volumes associated with the instance are mounted (only for m1.small and c1.medium instance types).
You can override the default instance store volume mount with the following cloud-init directive:
Copy
#cloud-config
mounts:
- [ ephemeral0 ]
For more control over mounts, see Mounts in the cloud-init documentation.
Instance store volumes that support TRIM are not formatted when an instance launches, so you must partition and format them before you can mount them. For more information, see Instance Store Volume TRIM Support. You can use the cloud-init disk_setup module to partition and format your instance store volumes at boot. For more information, see Disk Setup in the cloud-init documentation.
Supported User-Data Formats

The cloud-init package supports user-data handling of a variety of formats:

Gzip
If user-data is gzip compressed, cloud-init decompresses the data and handles it appropriately.
MIME multipart
Using a MIME multipart file, you can specify more than one type of data. For example, you could specify both a user-data script and a cloud-config type. Each part of the multipart file can be handled by cloud-init if it is one of the supported formats.
Base64 decoding
If user-data is base64-encoded, cloud-init determines if it can understand the decoded data as one of the supported types. If it understands the decoded data, it decodes the data and handles it appropriately. If not, it returns the base64 data intact.
User-Data script
Begins with #! or Content-Type: text/x-shellscript.
The script is executed by /etc/init.d/cloud-init-user-scripts during the first boot cycle. This occurs late in the boot process (after the initial configuration actions are performed).
Include file
Begins with #include or Content-Type: text/x-include-url.
This content is an include file. The file contains a list of URLs, one per line. Each of the URLs is read, and their content passed through this same set of rules. The content read from the URL can be gzipped, MIME-multi-part, or plain text.
Cloud Config Data
Begins with #cloud-config or Content-Type: text/cloud-config.
This content is cloud-config data. See the examples for a commented example of supported configuration formats.
Cloud Boothook
Begins with #cloud-boothook or Content-Type: text/cloud-boothook.
This content is boothook data. It is stored in a file under /var/lib/cloud and then executed immediately.
This is the earliest "hook" available. Note that there is no mechanism provided for running it only one time. The boothook must take care of this itself. It is provided with the instance ID in the environment variable INSTANCE_ID. Use this variable to provide a once-per-instance set of boothook data.
Repository Configuration

Beginning with the 2011.09 release of Amazon Linux, Amazon Linux AMIs are treated as snapshots in time, with a repository and update structure that always gives you the latest packages when you run yum update -y.

The repository structure is configured to deliver a continuous flow of updates that allow you to roll from one version of Amazon Linux to the next. For example, if you launch an instance from an older version of the Amazon Linux AMI (such as 2016.09 or earlier) and run yum update -y, you end up with the latest packages.

You can disable rolling updates for Amazon Linux by enabling the lock-on-launch feature. The lock-on-launch feature locks your newly launched instance to receive updates only from the specified release of the AMI. For example, you can launch a 2016.09 AMI and have it receive only the updates that were released prior to the 2017.03 AMI, until you are ready to migrate to the 2017.03 AMI. To enable lock-on-launch in new instances, launch it with the following user data passed to cloud-init, using either the Amazon EC2 console or the ec2-run-instances command with the -f flag.

Important
If you lock your AMI to a version of the repositories that is not latest, you will not receive any further updates. The only way to receive a continuous flow of updates for the Amazon Linux AMI is to be using the latest AMI, or to be consistently updating your old AMI with the repositories pointed to latest.
Copy
#cloud-config
repo_releasever: 2016.09
To lock existing instances to their current AMI release version

Edit /etc/yum.conf.

Comment out releasever=latest.

Run yum clean all to clear the cache.

Adding Packages

Amazon Linux is designed to be used with online package repositories hosted in each Amazon EC2 region. These repositories provide ongoing updates to packages in the Amazon Linux AMI, as well as access to hundreds of additional common open source server applications. The repositories are available in all regions and are accessed using yum update tools, as well as on the Amazon Linux AMI packages site. Hosting repositories in each region enables us to deploy updates quickly and without any data transfer charges. The packages can be installed by issuing yum commands, such as the following example:

Copy
[ec2-user ~]$ sudo yum install httpd
Access to the Extra Packages for Enterprise Linux (EPEL) repository is configured, but it is not enabled by default. EPEL provides third-party packages in addition to those that are in the Amazon Linux repositories. The third-party packages are not supported by AWS.

If you find that Amazon Linux does not contain an application you need, you can simply install the application directly on your Amazon Linux instance. Amazon Linux uses RPMs and yum for package management, and that is likely the simplest way to install new applications. You should always check to see if an application is available in our central Amazon Linux repository first, because many applications are available there. These applications can easily be added to your Amazon Linux instance.

To upload your applications onto a running Amazon Linux instance, use scp or sftp and then configure the application by logging on to your instance. Your applications can also be uploaded during the instance launch by using the PACKAGE_SETUP action from the built-in cloud-init package. For more information, see cloud-init.

Important
If your instance is running in a virtual private cloud (VPC), you must attach an Internet Gateway to the VPC in order to contact the yum repository. For more information, see Internet Gateways in the Amazon VPC User Guide.
Accessing Source Packages for Reference

You can view the source of packages you have installed on your instance for reference purposes by using tools provided in Amazon Linux. Source packages are available for all of the packages included in Amazon Linux and the online package repository. Simply determine the package name for the source package you want to install and use the get_reference_source command to view source within your running instance. For example:

Copy
[ec2-user ~]$ get_reference_source -p bash
The following is a sample response:

Requested package: bash
Found package from local RPM database: bash-4.2.46-20.36.amzn1.x86_64
Corresponding source RPM to found package : bash-4.2.46-20.36.amzn1.src.rpm

Are these parameters correct? Please type 'yes' to continue: yes
Source RPM downloaded to: /usr/src/srpm/debug/bash-4.2.46-20.36.amzn1.src.rpm
The source RPM is placed in the /usr/src/srpm/debug directory of your instance. From there, it can be unpacked, and, for reference, you can view the source tree using standard RPM tools. After you finish debugging, the package is available for use.

Important
If your instance is running in a virtual private cloud (VPC), you must attach an Internet Gateway to the VPC in order to contact the yum repository. For more information, see Internet Gateways in the Amazon VPC User Guide.
Developing Applications

A full set of Linux development tools is provided in the yum repository for Amazon Linux. To develop applications on Amazon Linux, select the development tools you need with yum. Alternatively, many applications developed on CentOS and other similar distributions should run on Amazon Linux.

Instance Store Access

The instance store drive ephemeral0 is mounted in /media/ephemeral0 only on Amazon instance store-backed AMIs. This is different than many other images that mount the instance store drive under /mnt.

Product Life Cycle

The Amazon Linux AMI is updated regularly with security and feature enhancements. If you do not need to preserve data or customizations on your Amazon Linux instances, you can simply relaunch new instances with the latest Amazon Linux AMI. If you need to preserve data or customizations for your Amazon Linux instances, you can maintain those instances through the Amazon Linux yum repositories. The yum repositories contain all the updated packages. You can choose to apply these updates to your running instances.

Older versions of the AMI and update packages will continue to be available for use, even as new versions are released. In some cases, if you're seeking support for an older version of Amazon Linux; through AWS Support, we might ask you to move to newer versions as part of the support process.

Security Updates

Security updates are provided via the Amazon Linux AMI yum repositories as well as via updated Amazon Linux AMIs. Security alerts are published in the Amazon Linux AMI Security Center. For more information on AWS security policies or to report a security problem, go to the AWS Security Center.

Amazon Linux AMIs are configured to download and install security updates at launch time. This is controlled via a cloud-init setting called repo_upgrade. The following snippet of cloud-init configuration shows how you can change the settings in the user data text you pass to your instance initialization:

Copy
#cloud-config
repo_upgrade: security
The possible values for the repo_upgrade setting are as follows:

security
Apply outstanding updates that Amazon marks as security updates.

bugfix
Apply updates that Amazon marks as bug fixes. Bug fixes are a larger set of updates, which include security updates and fixes for various other minor bugs.

all
Apply all applicable available updates, regardless of their classification.

none
Do not apply any updates to the instance on startup.

The default setting for repo_upgrade is security. That is, if you don't specify a different value in your user data, by default, the Amazon Linux AMI performs the security upgrades at launch for any packages installed at that time. The Amazon Linux AMI also notifies you of any updates to the installed packages by listing the number of available updates upon login using the /etc/motd file. To install these updates, you need to run sudo yum upgrade on the instance.

Important
If your instance is running in a virtual private cloud (VPC), you must attach an Internet Gateway to the VPC in order to contact the yum repository. For more information, see Internet Gateways in the Amazon VPC User Guide.
Support

Support for installation and use of the base Amazon Linux AMI is included through subscriptions to AWS Support. For more information, see AWS Support.

We encourage you to post any questions you have about Amazon Linux to the Amazon EC2 forum.

User Provided Kernels

If you have a need for a custom kernel on your Amazon EC2 instances, you can start with an AMI that is close to what you want, compile the custom kernel on your instance, and modify the menu.lst file to point to the new kernel. This process varies depending on the virtualization type that your AMI uses. For more information, see Linux AMI Virtualization Types.

Contents

HVM AMIs (GRUB)
Paravirtual AMIs (PV-GRUB)
HVM AMIs (GRUB)

HVM instance volumes are treated like actual physical disks. The boot process is similar to that of a bare metal operating system with a partitioned disk and bootloader, which allows it to work with all currently supported Linux distributions. The most common bootloader is GRUB, and the following section describes configuring GRUB to use a custom kernel.

Configuring GRUB for HVM AMIs

The following is an example of a menu.lst configuration file for an HVM AMI. In this example, there are two kernel entries to choose from: Amazon Linux 2017.03 (the original kernel for this AMI) and Vanilla Linux 4.7.4 (a newer version of the Vanilla Linux kernel from https://www.kernel.org/). The Vanilla entry was copied from the original entry for this AMI, and the kernel and initrd paths were updated to the new locations. The default 0 parameter points the bootloader to the first entry that it sees (in this case, the Vanilla entry), and the fallback 1 parameter points the bootloader to the next entry if there is a problem booting the first.

By default, GRUB does not send its output to the instance console because it creates an extra boot delay. For more information, see Instance Console Output. If you are installing a custom kernel, you should consider enabling GRUB output by deleting the hiddenmenu line and adding serial and terminal lines to /boot/grub/menu.lst as shown in the example below.

Important
Avoid printing large amounts of debug information during the boot process; the serial console does not support high rate data transfer.
default=0
fallback=1
timeout=5
serial --unit=0 --speed=9600
terminal --dumb --timeout=5 serial console

title Vanilla Linux 4.7.4
root (hd0)
kernel /boot/vmlinuz-4.7.4 root=LABEL=/ console=tty1 console=ttyS0
initrd /boot/initrd.img-4.7.4

title Amazon Linux 2017.03 (4.9.17-8.31.amzn1.x86_64)
root (hd0,0)
kernel /boot/vmlinuz-4.9.17-8.31.amzn1.x86_64 root=LABEL=/ console=tty1 console=ttyS0
initrd /boot/initramfs-4.9.17-8.31.amzn1.x86_64.img
You don't need to specify a fallback kernel in your menu.lst file, but we recommend that you have a fallback when you test a new kernel. GRUB can fall back to another kernel in the event that the new kernel fails. Having a fallback kernel allows the instance to boot even if the new kernel isn't found.

If your new Vanilla Linux kernel fails, the output will be similar to the example below.

^M Entry 0 will be booted automatically in 3 seconds. ^M Entry 0 will be booted automatically in 2 seconds. ^M Entry 0 will be booted automatically in 1 seconds.

Error 13: Invalid or unsupported executable format
[ 0.000000] Initializing cgroup subsys cpuset
Paravirtual AMIs (PV-GRUB)

Amazon Machine Images that use paravirtual (PV) virtualization use a system called PV-GRUB during the boot process. PV-GRUB is a paravirtual bootloader that runs a patched version of GNU GRUB 0.97. When you start an instance, PV-GRUB starts the boot process and then chain loads the kernel specified by your image's menu.lst file.

PV-GRUB understands standard grub.conf or menu.lst commands, which allows it to work with all currently supported Linux distributions. Older distributions such as Ubuntu 10.04 LTS, Oracle Enterprise Linux or CentOS 5.x require a special "ec2" or "xen" kernel package, while newer distributions include the required drivers in the default kernel package.

Most modern paravirtual AMIs use a PV-GRUB AKI by default (including all of the paravirtual Linux AMIs available in the Amazon EC2 Launch Wizard Quick Start menu), so there are no additional steps that you need to take to use a different kernel on your instance, provided that the kernel you want to use is compatible with your distribution. The best way to run a custom kernel on your instance is to start with an AMI that is close to what you want and then to compile the custom kernel on your instance and modify the menu.lst file as shown in Configuring GRUB to boot with that kernel.

You can verify that the kernel image for an AMI is a PV-GRUB AKI by executing the following describe-images command with the Amazon EC2 command line tools (substituting the kernel image ID you want to check:

Copy
aws ec2 describe-images --filters Name=image-id,Values=aki-880531cd
Check whether the Name field starts with pv-grub.

Topics

Limitations of PV-GRUB
Configuring GRUB for Paravirtual AMIs
Amazon PV-GRUB Kernel Image IDs
Updating PV-GRUB
Limitations of PV-GRUB

PV-GRUB has the following limitations:

You can't use the 64-bit version of PV-GRUB to start a 32-bit kernel or vice versa.
You can't specify an Amazon ramdisk image (ARI) when using a PV-GRUB AKI.
AWS has tested and verified that PV-GRUB works with these file system formats: EXT2, EXT3, EXT4, JFS, XFS, and ReiserFS. Other file system formats might not work.
PV-GRUB can boot kernels compressed using the gzip, bzip2, lzo, and xz compression formats.
Cluster AMIs don't support or need PV-GRUB, because they use full hardware virtualization (HVM). While paravirtual instances use PV-GRUB to boot, HVM instance volumes are treated like actual disks, and the boot process is similar to the boot process of a bare metal operating system with a partitioned disk and bootloader.
PV-GRUB versions 1.03 and earlier don't support GPT partitioning; they support MBR partitioning only.
If you plan to use a logical volume manager (LVM) with Amazon EBS volumes, you need a separate boot partition outside of the LVM. Then you can create logical volumes with the LVM.
Configuring GRUB for Paravirtual AMIs

To boot PV-GRUB, a GRUB menu.lst file must exist in the image; the most common location for this file is /boot/grub/menu.lst.

The following is an example of a menu.lst configuration file for booting an AMI with a PV-GRUB AKI. In this example, there are two kernel entries to choose from: Amazon Linux 2017.03 (the original kernel for this AMI), and Vanilla Linux 4.7.4 (a newer version of the Vanilla Linux kernel from https://www.kernel.org/). The Vanilla entry was copied from the original entry for this AMI, and the kernel and initrd paths were updated to the new locations. The default 0 parameter points the bootloader to the first entry it sees (in this case, the Vanilla entry), and the fallback 1 parameter points the bootloader to the next entry if there is a problem booting the first.

default 0
fallback 1
timeout 0
hiddenmenu

title Vanilla Linux 4.7.4
root (hd0)
kernel /boot/vmlinuz-4.7.4 root=LABEL=/ console=hvc0
initrd /boot/initrd.img-4.7.4

title Amazon Linux 2017.03 (4.9.17-8.31.amzn1.x86_64)
root (hd0)
kernel /boot/vmlinuz-4.9.17-8.31.amzn1.x86_64 root=LABEL=/ console=hvc0
initrd /boot/initramfs-4.9.17-8.31.amzn1.x86_64.img
You don't need to specify a fallback kernel in your menu.lst file, but we recommend that you have a fallback when you test a new kernel. PV-GRUB can fall back to another kernel in the event that the new kernel fails. Having a fallback kernel allows the instance to boot even if the new kernel isn't found.

PV-GRUB checks the following locations for menu.lst, using the first one it finds:

(hd0)/boot/grub
(hd0,0)/boot/grub
(hd0,0)/grub
(hd0,1)/boot/grub
(hd0,1)/grub
(hd0,2)/boot/grub
(hd0,2)/grub
(hd0,3)/boot/grub
(hd0,3)/grub
Note that PV-GRUB 1.03 and earlier only check one of the first two locations in this list.

Amazon PV-GRUB Kernel Image IDs

PV-GRUB AKIs are available in all Amazon EC2 regions. There are AKIs for both 32-bit and 64-bit architecture types. Most modern AMIs use a PV-GRUB AKI by default.

We recommend that you always use the latest version of the PV-GRUB AKI, as not all versions of the PV-GRUB AKI are compatible with all instance types. Use the following describe-images command to get a list of the PV-GRUB AKIs for the current region:

Copy
aws ec2 describe-images --owners amazon --filters Name=name,Values=pv-grub-*.gz
Note that PV-GRUB is the only AKI available in the ap-southeast-2 region. You should verify that any AMI you want to copy to this region is using a version of PV-GRUB that is available in this region.

The following are the current AKI IDs for each region. Register new AMIs using an hd0 AKI.

Note
We continue to provide hd00 AKIs for backward compatibility in regions where they were previously available.
ap-northeast-1, Asia Pacific (Tokyo)

Image ID	Image Name
aki-f975a998	pv-grub-hd0_1.05-i386.gz
aki-7077ab11	pv-grub-hd0_1.05-x86_64.gz
ap-southeast-1, Asia Pacific (Singapore) Region

Image ID	Image Name
aki-17a40074	pv-grub-hd0_1.05-i386.gz
aki-73a50110	pv-grub-hd0_1.05-x86_64.gz
ap-southeast-2, Asia Pacific (Sydney)

Image ID	Image Name
aki-ba5665d9	pv-grub-hd0_1.05-i386.gz
aki-66506305	pv-grub-hd0_1.05-x86_64.gz
eu-central-1, EU (Frankfurt)

Image ID	Image Name
aki-1419e57b	pv-grub-hd0_1.05-i386.gz
aki-931fe3fc	pv-grub-hd0_1.05-x86_64.gz
eu-west-1, EU (Ireland)

Image ID	Image Name
aki-1c9fd86f	pv-grub-hd0_1.05-i386.gz
aki-dc9ed9af	pv-grub-hd0_1.05-x86_64.gz
sa-east-1, South America (São Paulo)

Image ID	Image Name
aki-7cd34110	pv-grub-hd0_1.05-i386.gz
aki-912fbcfd	pv-grub-hd0_1.05-x86_64.gz
us-east-1, US East (N. Virginia)

Image ID	Image Name
aki-04206613	pv-grub-hd0_1.05-i386.gz
aki-5c21674b	pv-grub-hd0_1.05-x86_64.gz
us-gov-west-1, AWS GovCloud (US)

Image ID	Image Name
aki-5ee9573f	pv-grub-hd0_1.05-i386.gz
aki-9ee55bff	pv-grub-hd0_1.05-x86_64.gz
us-west-1, US West (N. California)

Image ID	Image Name
aki-43cf8123	pv-grub-hd0_1.05-i386.gz
aki-59cc8239	pv-grub-hd0_1.05-x86_64.gz
us-west-2, US West (Oregon)

Image ID	Image Name
aki-7a69931a	pv-grub-hd0_1.05-i386.gz
aki-70cb0e10	pv-grub-hd0_1.05-x86_64.gz
Updating PV-GRUB

We recommend that you always use the latest version of the PV-GRUB AKI, as not all versions of the PV-GRUB AKI are compatible with all instance types. Also, older versions of PV-GRUB are not available in all regions, so if you copy an AMI that uses an older version to a region that does not support that version, you will be unable to boot instances launched from that AMI until you update the kernel image. Use the following procedures to check your instance's version of PV-GRUB and update it if necessary.

To check your PV-GRUB version

Find the kernel ID for your instance.

Copy
aws ec2 describe-instance-attribute --instance-id instance_id --attribute kernel --region region

{
    "InstanceId": "instance_id", 
    "KernelId": "aki-70cb0e10"
}
The kernel ID for this instance is aki-70cb0e10.

View the version information of that kernel ID.

Copy
aws ec2 describe-images --image-ids aki-70cb0e10 --region region

{
    "Images": [
        {
            "VirtualizationType": "paravirtual", 
            "Name": "pv-grub-hd0_1.05-x86_64.gz", 
            ...
            "Description": "PV-GRUB release 1.05, 64-bit"
        }
    ]
}
This kernel image is PV-GRUB 1.05. If your PV-GRUB version is not the newest version (as shown in Amazon PV-GRUB Kernel Image IDs), you should update it using the following procedure.

To update your PV-GRUB version

If your instance is using an older version of PV-GRUB, you should update it to the latest version.

Identify the latest PV-GRUB AKI for your region and processor architecture from Amazon PV-GRUB Kernel Image IDs.

Stop your instance. Your instance must be stopped to modify the kernel image used.

Copy
aws ec2 stop-instances --instance-ids instance_id --region region
Modify the kernel image used for your instance.

Copy
aws ec2 modify-instance-attribute --instance-id instance_id --kernel kernel_id --region region
Restart your instance.

Copy
aws ec2 start-instances --instance-ids instance_id --region region 

