Network and Security

Amazon EC2 provides the following network and security features.

Features

Amazon EC2 Key Pairs
Amazon EC2 Security Groups for Linux Instances
Controlling Access to Amazon EC2 Resources
Amazon EC2 and Amazon Virtual Private Cloud
Amazon EC2 Instance IP Addressing
Elastic IP Addresses
Elastic Network Interfaces
Placement Groups
Network Maximum Transmission Unit (MTU) for Your EC2 Instance
Enhanced Networking on Linux
If you access Amazon EC2 using the command line tools or an API, you'll need your access key ID and secret access key. For more information, see How Do I Get Security Credentials? in the Amazon Web Services General Reference.

You can launch an instance into one of two platforms: EC2-Classic or EC2-VPC. An instance that's launched into EC2-Classic or a default VPC is automatically assigned a public IP address. An instance that's launched into a nondefault VPC can be assigned a public IP address on launch. For more information about EC2-Classic and EC2-VPC, see Supported Platforms.

Instances can fail or terminate for reasons outside of your control. If an instance fails and you launch a replacement instance, the replacement has a different public IP address than the original. However, if your application needs a static IP address, you can use an Elastic IP address.

You can use security groups to control who can access your instances. These are analogous to an inbound network firewall that enables you to specify the protocols, ports, and source IP ranges that are allowed to reach your instances. You can create multiple security groups and assign different rules to each group. You can then assign each instance to one or more security groups, and we use the rules to determine which traffic is allowed to reach the instance. You can configure a security group so that only specific IP addresses or specific security groups have access to the instance.

Amazon EC2 Key Pairs

Amazon EC2 uses public–key cryptography to encrypt and decrypt login information. Public–key cryptography uses a public key to encrypt a piece of data, such as a password, then the recipient uses the private key to decrypt the data. The public and private keys are known as a key pair.

To log in to your instance, you must create a key pair, specify the name of the key pair when you launch the instance, and provide the private key when you connect to the instance. On a Linux instance, the public key content is placed in an entry within ~/.ssh/authorized_keys. This is done at boot time and enables you to securely access your instance using the private key instead of a password.

Creating a Key Pair

You can use Amazon EC2 to create your key pair. For more information, see Creating a Key Pair Using Amazon EC2.

Alternatively, you could use a third-party tool and then import the public key to Amazon EC2. For more information, see Importing Your Own Public Key to Amazon EC2.

Each key pair requires a name. Be sure to choose a name that is easy to remember. Amazon EC2 associates the public key with the name that you specify as the key name.

Amazon EC2 stores the public key only, and you store the private key. Anyone who possesses your private key can decrypt your login information, so it's important that you store your private keys in a secure place.

The keys that Amazon EC2 uses are 2048-bit SSH-2 RSA keys. You can have up to five thousand key pairs per region.

Launching and Connecting to Your Instance

When you launch an instance, you should specify the name of the key pair you plan to use to connect to the instance. If you don't specify the name of an existing key pair when you launch an instance, you won't be able to connect to the instance. When you connect to the instance, you must specify the private key that corresponds to the key pair you specified when you launched the instance.

Note
Amazon EC2 doesn't keep a copy of your private key; therefore, if you lose a private key, there is no way to recover it. If you lose the private key for an instance store-backed instance, you can't access the instance; you should terminate the instance and launch another instance using a new key pair. If you lose the private key for an EBS-backed Linux instance, you can regain access to your instance. For more information, see Connecting to Your Linux Instance if You Lose Your Private Key.
Key Pairs for Multiple Users

If you have several users that require access to a single instance, you can add user accounts to your instance. For more information, see Managing User Accounts on Your Linux Instance. You can create a key pair for each user, and add the public key information from each key pair to the .ssh/authorized_keys file for each user on your instance. You can then distribute the private key files to your users. That way, you do not have to distribute the same private key file that's used for the root account to multiple users.

Contents

Creating a Key Pair Using Amazon EC2
Importing Your Own Public Key to Amazon EC2
Retrieving the Public Key for Your Key Pair on Linux
Retrieving the Public Key for Your Key Pair on Windows
Retrieving the Public Key for Your Key Pair From Your Instance
Verifying Your Key Pair's Fingerprint
Deleting Your Key Pair
Adding or Replacing a Key Pair for Your Instance
Connecting to Your Linux Instance if You Lose Your Private Key
Creating a Key Pair Using Amazon EC2

You can create a key pair using the Amazon EC2 console or the command line. After you create a key pair, you can specify it when you launch your instance. You can also add the key pair to a running instance to enable another user to connect to the instance. For more information, see Adding or Replacing a Key Pair for Your Instance.

To create your key pair using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under NETWORK & SECURITY, choose Key Pairs.

Note
The navigation pane is on the left side of the Amazon EC2 console. If you do not see the pane, it might be minimized; choose the arrow to expand the pane.
Choose Create Key Pair.

Enter a name for the new key pair in the Key pair name field of the Create Key Pair dialog box, and then choose Create.

The private key file is automatically downloaded by your browser. The base file name is the name you specified as the name of your key pair, and the file name extension is .pem. Save the private key file in a safe place.

Important
This is the only chance for you to save the private key file. You'll need to provide the name of your key pair when you launch an instance and the corresponding private key each time you connect to the instance.
If you will use an SSH client on a Mac or Linux computer to connect to your Linux instance, use the following command to set the permissions of your private key file so that only you can read it.

Copy
chmod 400 my-key-pair.pem
To create your key pair using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-key-pair (AWS CLI)
New-EC2KeyPair (AWS Tools for Windows PowerShell)
Importing Your Own Public Key to Amazon EC2

Instead of using Amazon EC2 to create your key pair, you can create an RSA key pair using a third-party tool and then import the public key to Amazon EC2. For example, you can use ssh-keygen (a tool provided with the standard OpenSSH installation) to create a key pair. Alternatively, Java, Ruby, Python, and many other programming languages provide standard libraries that you can use to create an RSA key pair.

Amazon EC2 accepts the following formats:

OpenSSH public key format (the format in ~/.ssh/authorized_keys)
Base64 encoded DER format
SSH public key file format as specified in RFC4716
Amazon EC2 does not accept DSA keys. Make sure your key generator is set up to create RSA keys.

Supported lengths: 1024, 2048, and 4096.

To create a key pair using a third-party tool

Generate a key pair with a third-party tool of your choice.

Save the public key to a local file. For example, ~/.ssh/my-key-pair.pub (Linux) or C:\keys\my-key-pair.pub (Windows). The file name extension for this file is not important.

Save the private key to a different local file that has the .pem extension. For example, ~/.ssh/my-key-pair.pem (Linux) or C:\keys\my-key-pair.pem (Windows). Save the private key file in a safe place. You'll need to provide the name of your key pair when you launch an instance and the corresponding private key each time you connect to the instance.

Use the following steps to import your key pair using the Amazon EC2 console.

To import the public key

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under NETWORK & SECURITY, choose Key Pairs.

Choose Import Key Pair.

In the Import Key Pair dialog box, choose Browse, and select the public key file that you saved previously. Enter a name for the key pair in the Key pair name field, and choose Import.

To import the public key using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

import-key-pair (AWS CLI)
Import-EC2KeyPair (AWS Tools for Windows PowerShell)
After the public key file is imported, you can verify that the key pair was imported successfully using the Amazon EC2 console as follows.

To verify that your key pair was imported

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region in which you created the key pair.

In the navigation pane, under NETWORK & SECURITY, choose Key Pairs.

Verify that the key pair that you imported is in the displayed list of key pairs.

To view your key pair using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-key-pairs (AWS CLI)
Get-EC2KeyPair (AWS Tools for Windows PowerShell)
Retrieving the Public Key for Your Key Pair on Linux

On your local Linux or Mac computer, you can use the ssh-keygen command to retrieve the public key for your key pair.

To retrieve the public key from your computer

Use the ssh-keygen command on a computer to which you've downloaded your private key:

Copy
ssh-keygen -y
When prompted to enter the file in which the key is, specify the path to your .pem file; for example:

Copy
/path_to_key_pair/my-key-pair.pem
The command returns the public key:

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClKsfkNkuSevGj3eYhCe53pcjqP3maAhDFcvBS7O6V
hz2ItxCih+PnDSUaw+WNQn/mZphTk/a/gU8jEzoOWbkM4yxyb/wB96xbiFveSFJuOp/d6RJhJOI0iBXr
lsLnBItntckiJ7FbtxJMXLvvwJryDUilBMTjYtwB+QhYXUMOzce5Pjz5/i8SeJtjnV3iAoG/cQk+0FzZ
qaeJAAHco+CY/5WrUBkrHmFJr6HcXkvJdWPkYQS3xqC0+FmUZofz221CBt5IMucxXPkX4rWi+z7wB3Rb
BQoQzd8v7yeb7OzlPnWOyN0qFU0XA246RA8QFYiCNYwI3f05p6KLxEXAMPLE
If this command fails, ensure that you've changed the permissions on your key pair file so that only you can view it by running the following command:

Copy
chmod 400 my-key-pair.pem
Retrieving the Public Key for Your Key Pair on Windows

On your local Windows computer, you can use PuTTYgen to get the public key for your key pair.

Start PuTTYgen, choose Load, and select the .ppk or .pem file. PuTTYgen displays the public key.

Retrieving the Public Key for Your Key Pair From Your Instance

The public key that you specified when you launched an instance is also available to you through its instance metadata. To view the public key that you specified when launching the instance, use the following command from your instance:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClKsfkNkuSevGj3eYhCe53pcjqP3maAhDFcvBS7O6V
hz2ItxCih+PnDSUaw+WNQn/mZphTk/a/gU8jEzoOWbkM4yxyb/wB96xbiFveSFJuOp/d6RJhJOI0iBXr
lsLnBItntckiJ7FbtxJMXLvvwJryDUilBMTjYtwB+QhYXUMOzce5Pjz5/i8SeJtjnV3iAoG/cQk+0FzZ
qaeJAAHco+CY/5WrUBkrHmFJr6HcXkvJdWPkYQS3xqC0+FmUZofz221CBt5IMucxXPkX4rWi+z7wB3Rb
BQoQzd8v7yeb7OzlPnWOyN0qFU0XA246RA8QFYiCNYwI3f05p6KLxEXAMPLE my-key-pair
If you change the key pair that you use to connect to the instance, we don't update the instance metadata to show the new public key; you'll continue to see the public key for the key pair you specified when you launched the instance in the instance metadata.

For more information, see Retrieving Instance Metadata.

Alternatively, on a Linux instance, the public key content is placed in an entry within ~/.ssh/authorized_keys. You can open this file in an editor. The following is an example entry for the key pair named my-key-pair. It consists of the public key followed by the name of the key pair. For example:

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClKsfkNkuSevGj3eYhCe53pcjqP3maAhDFcvBS7O6V
hz2ItxCih+PnDSUaw+WNQn/mZphTk/a/gU8jEzoOWbkM4yxyb/wB96xbiFveSFJuOp/d6RJhJOI0iBXr
lsLnBItntckiJ7FbtxJMXLvvwJryDUilBMTjYtwB+QhYXUMOzce5Pjz5/i8SeJtjnV3iAoG/cQk+0FzZ
qaeJAAHco+CY/5WrUBkrHmFJr6HcXkvJdWPkYQS3xqC0+FmUZofz221CBt5IMucxXPkX4rWi+z7wB3Rb
BQoQzd8v7yeb7OzlPnWOyN0qFU0XA246RA8QFYiCNYwI3f05p6KLxEXAMPLE my-key-pair
Verifying Your Key Pair's Fingerprint

On the Key Pairs page in the Amazon EC2 console, the Fingerprint column displays the fingerprints generated from your key pairs. AWS calculates the fingerprint differently depending on whether the key pair was generated by AWS or a third-party tool. If you created the key pair using AWS, the fingerprint is calculated using an SHA-1 hash function. If you created the key pair with a third-party tool and uploaded the public key to AWS, or if you generated a new public key from an existing AWS-created private key and uploaded it to AWS, the fingerprint is calculated using an MD5 hash function.

You can use the fingerprint that's displayed on the Key Pairs page to verify that the private key you have on your local machine matches the public key that's stored in AWS.

If you created your key pair using AWS, you can use the OpenSSL tools to generate a fingerprint from the private key file:

Copy
$ openssl pkcs8 -in path_to_private_key -inform PEM -outform DER -topk8 -nocrypt | openssl sha1 -c
If you created your key pair using a third-party tool and uploaded the public key to AWS, you can use the OpenSSL tools to generate a fingerprint from the private key file on your local machine:

Copy
$ openssl rsa -in path_to_private_key -pubout -outform DER | openssl md5 -c
The output should match the fingerprint that's displayed in the console.

Deleting Your Key Pair

When you delete a key pair, you are only deleting Amazon EC2's copy of the public key. Deleting a key pair doesn't affect the private key on your computer or the public key on any instances already launched using that key pair. You can't launch a new instance using a deleted key pair, but you can continue to connect to any instances that you launched using a deleted key pair, as long as you still have the private key (.pem) file.

Note
If you're using an Auto Scaling group (for example, in an Elastic Beanstalk environment), ensure that the key pair you're deleting is not specified in your launch configuration. Auto Scaling launches a replacement instance if it detects an unhealthy instance; however, the instance launch fails if the key pair cannot be found.
You can delete a key pair using the Amazon EC2 console or the command line.

To delete your key pair using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under NETWORK & SECURITY, choose Key Pairs.

Select the key pair and choose Delete.

When prompted, choose Yes.

To delete your key pair using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

delete-key-pair (AWS CLI)
Remove-EC2KeyPair (AWS Tools for Windows PowerShell)
Note
If you create a Linux AMI from an instance, and then use the AMI to launch a new instance in a different region or account, the new instance includes the public key from the original instance. This enables you to connect to the new instance using the same private key file as your original instance. You can remove this public key from your instance by removing its entry from the .ssh/authorized_keys file using a text editor of your choice. For more information about managing users on your instance and providing remote access using a specific key pair, see Managing User Accounts on Your Linux Instance.
Adding or Replacing a Key Pair for Your Instance

You can change the key pair that is used to access the default system account of your instance. For example, if a user in your organization requires access to the system user account using a separate key pair, you can add that key pair to your instance. Or, if someone has a copy of the .pem file and you want to prevent them from connecting to your instance (for example, if they've left your organization), you can replace the key pair with a new one.

Note
These procedures are for modifying the key pair for the default user account, such as ec2-user. For more information about adding user accounts to your instance, see Managing User Accounts on Your Linux Instance.
Before you begin, create a new key pair using the Amazon EC2 console or a third-party tool.

To add or replace a key pair

Retrieve the public key from your new key pair. For more information, see Retrieving the Public Key for Your Key Pair on Linux or Retrieving the Public Key for Your Key Pair on Windows.

Connect to your instance using your existing private key file.

Using a text editor of your choice, open the .ssh/authorized_keys file on the instance. Paste the public key information from your new key pair underneath the existing public key information. Save the file.

Disconnect from your instance, and test that you can connect to your instance using the new private key file.

(Optional) If you're replacing an existing key pair, connect to your instance and delete the public key information for the original key pair from the .ssh/authorized_keys file.

Note
If you're using an Auto Scaling group (for example, in an Elastic Beanstalk environment), ensure that the key pair you're replacing is not specified in your launch configuration. Auto Scaling launches a replacement instance if it detects an unhealthy instance; however, the instance launch fails if the key pair cannot be found.
Connecting to Your Linux Instance if You Lose Your Private Key

If you lose the private key for an EBS-backed instance, you can regain access to your instance. You must stop the instance, detach its root volume and attach it to another instance as a data volume, modify the authorized_keys file, move the volume back to the original instance, and restart the instance. For more information about launching, connecting to, and stopping instances, see Instance Lifecycle.

This procedure isn't supported for instance store-backed instances. To determine the root device type of your instance, open the Amazon EC2 console, choose Instances, select the instance, and check the value of Root device type in the details pane. The value is either ebs or instance store. If the root device is an instance store volume, you must have the private key in order to connect to the instance.

Prerequisites

Create a new key pair using either the Amazon EC2 console or a third-party tool. If you want to name your new key pair exactly the same as the lost private key, you must first delete the existing key pair.

To connect to an EBS-backed instance with a different key pair

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Instances in the navigation pane, and then select the instance that you'd like to connect to. (We'll refer to this as the original instance.)

Save the following information that you'll need to complete this procedure.

Write down the instance ID, AMI ID, and Availability Zone of the original instance.
In the Root device field, take note of the device name for the root volume (for example, /dev/sda1 or /dev/xvda). Choose the link and write down the volume ID in the EBS ID field (vol-xxxxxxxxxxxxxxxxx).
[EC2-Classic] If the original instance has an associated Elastic IP address, write down the Elastic IP address shown in the Elastic IP field in the details pane.
Choose Actions, select Instance State, and then select Stop. If Stop is disabled, either the instance is already stopped or its root device is an instance store volume.

Warning
When you stop an instance, the data on any instance store volumes is erased. Therefore, if you have any data on instance store volumes that you want to keep, be sure to back it up to persistent storage.
Choose Launch Instance, and then use the launch wizard to launch a temporary instance with the following options:

On the Choose an AMI page, select the same AMI that you used to launch the original instance. If this AMI is unavailable, you can create an AMI that you can use from the stopped instance. For more information, see Creating an Amazon EBS-Backed Linux AMI .
On the Choose an Instance Type page, leave the default instance type that the wizard selects for you.
On the Configure Instance Details page, specify the same Availability Zone as the instance you'd like to connect to. If you're launching an instance in a VPC, select a subnet in this Availability Zone.
On the Add Tags page, add the tag Name=Temporary to the instance to indicate that this is a temporary instance.
On the Review page, choose Launch. Create a new key pair, download it to a safe location on your computer, and then choose Launch Instances.
In the navigation pane, choose Volumes and select the root device volume for the original instance (you wrote down its volume ID in a previous step). Choose Actions, and then select Detach Volume. Wait for the state of the volume to become available. (You might need to choose the Refresh icon.)

With the volume still selected, choose Actions, and then select Attach Volume. Select the instance ID of the temporary instance, write down the device name specified under Device (for example, /dev/sdf), and then choose Yes, Attach.

Note
If you launched your original instance from an AWS Marketplace AMI and your volume contains AWS Marketplace codes, you must first stop the temporary instance before you can attach the volume.
Connect to the temporary instance.

From the temporary instance, mount the volume that you attached to the instance so that you can access its file system. For example, if the device name is /dev/sdf, use the following commands to mount the volume as /mnt/tempvol.

Note
The device name may appear differently on your instance. For example, devices mounted as /dev/sdf may show up as /dev/xvdf on the instance. Some versions of Red Hat (or its variants, such as CentOS) may even increment the trailing letter by 4 characters, where /dev/sdf becomes /dev/xvdk.
Use the lsblk command to determine if the volume is partitioned.

Copy
[ec2-user ~]$ lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0    8G  0 disk
└─xvda1 202:1    0    8G  0 part /
xvdf    202:80   0  101G  0 disk
└─xvdf1 202:81   0  101G  0 part
xvdg    202:96   0   30G  0 disk
In the above example, /dev/xvda and /dev/xvdf are partitioned volumes, and /dev/xvdg is not. If your volume is partitioned, you mount the partition (/dev/xvdf1) instead of the raw device (/dev/xvdf) in the next steps.

Create a temporary directory to mount the volume.

Copy
[ec2-user ~]$ sudo mkdir /mnt/tempvol
Mount the volume (or partition) at the temporary mount point, using the volume name or device name you identified earlier.

Copy
[ec2-user ~]$ sudo mount /dev/xvdf1 /mnt/tempvol
From the temporary instance, use the following command to update authorized_keys on the mounted volume with the new public key from the authorized_keys for the temporary instance.

Important
The following examples use the Amazon Linux user name ec2-user. You may need to substitute a different user name, such as ubuntu for Ubuntu instances.
Copy
[ec2-user ~]$ cp .ssh/authorized_keys /mnt/tempvol/home/ec2-user/.ssh/authorized_keys
If this copy succeeded, you can go to the next step.

(Optional) Otherwise, if you don't have permission to edit files in /mnt/tempvol, you'll need to update the file using sudo and then check the permissions on the file to verify that you'll be able to log into the original instance. Use the following command to check the permissions on the file:

Copy
[ec2-user ~]$ sudo ls -l /mnt/tempvol/home/ec2-user/.ssh
total 4
-rw------- 1 222 500 398 Sep 13 22:54 authorized_keys
In this example output, 222 is the user ID and 500 is the group ID. Next, use sudo to re-run the copy command that failed:

Copy
[ec2-user ~]$ sudo cp .ssh/authorized_keys /mnt/tempvol/home/ec2-user/.ssh/authorized_keys
Run the following command again to determine whether the permissions changed:

Copy
[ec2-user ~]$ sudo ls -l /mnt/tempvol/home/ec2-user/.ssh
If the user ID and group ID have changed, use the following command to restore them:

Copy
[ec2-user ~]$ sudo chown 222:500 /mnt/tempvol/home/ec2-user/.ssh/authorized_keys
From the temporary instance, unmount the volume that you attached so that you can reattach it to the original instance. For example, use the following command to unmount the volume at /mnt/tempvol:

Copy
[ec2-user ~]$ sudo umount /mnt/tempvol
From the Amazon EC2 console, select the volume with the volume ID that you wrote down, choose Actions, and then select Detach Volume. Wait for the state of the volume to become available. (You might need to choose the Refresh icon.)

With the volume still selected, choose Actions, Attach Volume. Select the instance ID of the original instance, specify the device name you noted earlier for the original root device attachment (/dev/sda1 or /dev/xvda), and then choose Yes, Attach.

Important
If you don't specify the same device name as the original attachment, you cannot start the original instance. Amazon EC2 expects the root device volume at sda1 or /dev/xvda.
Select the original instance, choose Actions, select Instance State, and then choose Start. After the instance enters the running state, you can connect to it using the private key file for your new key pair.

Note
If the name of your new key pair and corresponding private key file is different to the name of the original key pair, ensure that you specify the name of the new private key file when you connect to your instance.
[EC2-Classic] If the original instance had an associated Elastic IP address before you stopped it, you must re-associate it with the instance as follows:

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address that you wrote down at the beginning of this procedure.

Choose Actions, and then select Associate address.

Select the ID of the original instance, and then choose Associate.

(Optional) You can terminate the temporary instance if you have no further use for it. Select the temporary instance, choose Actions, select Instance State, and then choose Terminate.

Amazon EC2 Security Groups for Linux Instances

A security group acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group. When we decide whether to allow traffic to reach an instance, we evaluate all the rules from all the security groups that are associated with the instance.

If you need to allow traffic to a Windows instance, see Amazon EC2 Security Groups for Windows Instances in the Amazon EC2 User Guide for Windows Instances.

Topics

Security Groups for EC2-Classic
Security Groups for EC2-VPC
Security Group Rules
Default Security Groups
Custom Security Groups
Working with Security Groups
Security Group Rules Reference
If you have requirements that aren't met by security groups, you can maintain your own firewall on any of your instances in addition to using security groups.

Your account may support EC2-Classic in some regions, depending on when you created it. For more information, see Supported Platforms. Security groups for EC2-Classic are separate to security groups for EC2-VPC.

Security Groups for EC2-Classic

If you're using EC2-Classic, you must use security groups created specifically for EC2-Classic. When you launch an instance in EC2-Classic, you must specify a security group in the same region as the instance. You can't specify a security group that you created for a VPC when you launch an instance in EC2-Classic.

After you launch an instance in EC2-Classic, you can't change its security groups. However, you can add rules to or remove rules from a security group, and those changes are automatically applied to all instances that are associated with the security group.

In EC2-Classic, you can have up to 500 security groups in each region for each account. You can associate an instance with up to 500 security groups and add up to 100 rules to a security group.

Security Groups for EC2-VPC

If you're using EC2-VPC, you must use security groups created specifically for your VPC. When you launch an instance in a VPC, you must specify a security group for that VPC. You can't specify a security group that you created for EC2-Classic when you launch an instance in a VPC. Security groups for EC2-VPC have additional capabilities that aren't supported by security groups for EC2-Classic. For more information, see Differences Between Security Groups for EC2-Classic and EC2-VPC in the Amazon VPC User Guide.

After you launch an instance in a VPC, you can change its security groups. Security groups are associated with network interfaces. Changing an instance's security groups changes the security groups associated with the primary network interface (eth0). For more information, see Changing an Instance's Security Groups in the Amazon VPC User Guide. You can also change the security groups associated with any other network interface. For more information, see Changing the Security Group.

Security groups for EC2-VPC have separate limits. For more information, see Amazon VPC Limits in the Amazon VPC User Guide. The security groups for EC2-Classic do not count against the security group limit for EC2-VPC.

Your VPC can be enabled for IPv6. For more information, see IP addressing in Your VPC in the Amazon VPC User Guide. You can add rules to your VPC security groups to enable inbound and outbound IPv6 traffic.

Security Group Rules

The rules of a security group control the inbound traffic that's allowed to reach the instances that are associated with the security group and the outbound traffic that's allowed to leave them.

The following are the characteristics of security group rules:

By default, security groups allow all outbound traffic.
You can't change the outbound rules for an EC2-Classic security group.
Security group rules are always permissive; you can't create rules that deny access.
Security groups are stateful — if you send a request from your instance, the response traffic for that request is allowed to flow in regardless of inbound security group rules. For VPC security groups, this also means that responses to allowed inbound traffic are allowed to flow out, regardless of outbound rules. For more information, see Connection Tracking.
You can add and remove rules at any time. Your changes are automatically applied to the instances associated with the security group after a short period.
Note
The effect of some rule changes may depend on how the traffic is tracked. For more information, see Connection Tracking.
When you associate multiple security groups with an instance, the rules from each security group are effectively aggregated to create one set of rules. We use this set of rules to determine whether to allow access.
Note
You can assign multiple security groups to an instance, therefore an instance can have hundreds of rules that apply. This might cause problems when you access the instance. We recommend that you condense your rules as much as possible.
For each rule, you specify the following:

Protocol: The protocol to allow. The most common protocols are 6 (TCP) 17 (UDP), and 1 (ICMP).
Port range : For TCP, UDP, or a custom protocol, the range of ports to allow. You can specify a single port number (for example, 22), or range of port numbers (for example, 7000-8000).
ICMP type and code: For ICMP, the ICMP type and code.
Source or destination: The source (inbound rules) or destination (outbound rules) for the traffic. Specify one of these options:
An individual IPv4 address. You must use the /32 prefix after the IPv4 address; for example, 203.0.113.1/32.
(VPC only) An individual IPv6 address. You must use the /128 prefix length; for example 2001:db8:1234:1a00::123/128.
A range of IPv4 addresses, in CIDR block notation, for example, 203.0.113.0/24.
(VPC only) A range of IPv6 addresses, in CIDR block notation, for example, 2001:db8:1234:1a00::/64.
Another security group. This allows instances associated with the specified security group to access instances associated with this security group. This does not add rules from the source security group to this security group. You can specify one of the following security groups:
The current security group.
EC2-Classic: A different security group for EC2-Classic in the same region.
EC2-Classic: A security group for another AWS account in the same region (add the AWS account ID as a prefix; for example, 111122223333/sg-edcd9784).
EC2-VPC: A different security group for the same VPC or a peer VPC in a VPC peering connection.
(Optional) Description: You can add a description for the rule; for example, to help you identify it later. A description can be up to 255 characters in length. Allowed characters are a-z, A-Z, 0-9, spaces, and ._-:/()#,@[]+=;{}!$*.
When you specify a security group as the source or destination for a rule, the rule affects all instances associated with the security group. Incoming traffic is allowed based on the private IP addresses of the instances that are associated with the source security group (and not the public IP or Elastic IP addresses). For more information about IP addresses, see Amazon EC2 Instance IP Addressing. If your security group rule references a security group in a peer VPC, and the referenced security group or VPC peering connection is deleted, the rule is marked as stale. For more information, see Working with Stale Security Group Rules in the Amazon VPC Peering Guide.

If there is more than one rule for a specific port, we apply the most permissive rule. For example, if you have a rule that allows access to TCP port 22 (SSH) from IP address 203.0.113.1 and another rule that allows access to TCP port 22 from everyone, everyone has access to TCP port 22.

Connection Tracking

Your security groups use connection tracking to track information about traffic to and from the instance. Rules are applied based on the connection state of the traffic to determine if the traffic is allowed or denied. This allows security groups to be stateful — responses to inbound traffic are allowed to flow out of the instance regardless of outbound security group rules, and vice versa. For example, if you initiate an ICMP ping command to your instance from your home computer, and your inbound security group rules allow ICMP traffic, information about the connection (including the port information) is tracked. Response traffic from the instance for the ping command is not tracked as a new request, but rather as an established connection and is allowed to flow out of the instance, even if your outbound security group rules restrict outbound ICMP traffic.

Not all flows of traffic are tracked. If a security group rule permits TCP or UDP flows for all traffic (0.0.0.0/0) and there is a corresponding rule in the other direction that permits all response traffic (0.0.0.0/0) for all ports (0-65535), then that flow of traffic is not tracked. The response traffic is therefore allowed to flow based on the inbound or outbound rule that permits the response traffic, and not on tracking information. In the following example, the security group has specific inbound rules for SSH, HTTP, and ICMP traffic, and an outbound rule that allows all outbound traffic.


Inbound rules
Protocol type	Port number	Source IP
TCP	22 (SSH)	203.0.113.1/32
TCP	80 (HTTP)	0.0.0.0/0
ICMP	All	0.0.0.0/0
Outbound rules
Protocol type	Port number	Destination IP
All	All	0.0.0.0/0
SSH traffic to and from the instance is tracked, because of the restrictive inbound rule. ICMP traffic is always tracked, regardless of rules. HTTP traffic to and from the instance is not tracked, because both the inbound and outbound rules allow all HTTP traffic.

An existing flow of traffic that is tracked may not be interrupted when you remove the security group rule that enables that flow. Instead, the flow is interrupted when it's stopped by you or the other host for at least a few minutes (or up to 5 days for established TCP connections). For UDP, this may require terminating actions on the remote side of the flow. An untracked flow of traffic is immediately interrupted if the rule that enables the flow is removed or modified. For example, if you remove a rule that allows all inbound SSH traffic to the instance, then your existing SSH connections to the instance are immediately dropped.

For protocols other than TCP, UDP, or ICMP, only the IP address and protocol number is tracked. If your instance sends traffic to another host (host B), and host B initiates the same type of traffic to your instance in a separate request within 600 seconds of the original request or response, your instance accepts it regardless of inbound security group rules, because it’s regarded as response traffic.

For VPC security groups, to ensure that traffic is immediately interrupted when you remove a security group rule, or to ensure that all inbound traffic is subject to firewall rules, you can use a network ACL for your subnet — network ACLs are stateless and therefore do not automatically allow response traffic. For more information, see Network ACLs in the Amazon VPC User Guide.

Default Security Groups

Your AWS account automatically has a default security group per VPC and per region for EC2-Classic. If you don't specify a security group when you launch an instance, the instance is automatically associated with the default security group.

A default security group is named default, and it has an ID assigned by AWS. The following are the default rules for each default security group:

Allows all inbound traffic from other instances associated with the default security group (the security group specifies itself as a source security group in its inbound rules)
Allows all outbound traffic from the instance.
You can add or remove the inbound rules for any default security group. You can add or remove outbound rules for any VPC default security group.

You can't delete a default security group. If you try to delete the EC2-Classic default security group, you'll get the following error: Client.InvalidGroup.Reserved: The security group 'default' is reserved. If you try to delete a VPC default security group, you'll get the following error: Client.CannotDelete: the specified group: "sg-51530134" name: "default" cannot be deleted by a user.

Custom Security Groups

If you don't want your instances to use the default security group, you can create your own security groups and specify them when you launch your instances. You can create multiple security groups to reflect the different roles that your instances play; for example, a web server or a database server.

When you create a security group, you must provide it with a name and a description. Security group names and descriptions can be up to 255 characters in length, and are limited to the following characters:

EC2-Classic: ASCII characters
EC2-VPC: a-z, A-Z, 0-9, spaces, and ._-:/()#,@[]+=&;{}!$*
The following are the default rules for a security group that you create:

Allows no inbound traffic
Allows all outbound traffic
After you've created a security group, you can change its inbound rules to reflect the type of inbound traffic that you want to reach the associated instances. In EC2-VPC, you can also change its outbound rules.

For more information about the types of rules you can add to security groups, see Security Group Rules Reference.

Working with Security Groups

You can create, view, update, and delete security groups and security group rules using the Amazon EC2 console.

Contents

Creating a Security Group
Describing Your Security Groups
Adding Rules to a Security Group
Updating Security Group Rules
Deleting Rules from a Security Group
Deleting a Security Group
Creating a Security Group

You can create a custom security group using the Amazon EC2 console. For EC2-VPC, you must specify the VPC for which you're creating the security group.

To create a new security group using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Choose Create Security Group.

Specify a name and description for the security group.

(EC2-Classic only) To create a security group for use in EC2-Classic, choose No VPC.

(EC2-VPC) For VPC, choose a VPC ID to create a security group for that VPC.

You can start adding rules, or you can choose Create to create the security group now (you can always add rules later). For more information about adding rules, see Adding Rules to a Security Group.

To create a security group using the command line

create-security-group (AWS CLI)
New-EC2SecurityGroup (AWS Tools for Windows PowerShell)
The Amazon EC2 console enables you to copy the rules from an existing security group to a new security group.

To copy a security group using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Select the security group you want to copy, choose Actions, Copy to new.

The Create Security Group dialog opens, and is populated with the rules from the existing security group. Specify a name and description for your new security group. In the VPC list, choose No VPC to create a security group for EC2-Classic, or choose a VPC ID to create a security group for that VPC. When you are done, choose Create.

You can assign a security group to an instance when you launch the instance. When you add or remove rules, those changes are automatically applied to all instances to which you've assigned the security group.

After you launch an instance in EC2-Classic, you can't change its security groups. After you launch an instance in a VPC, you can change its security groups. For more information, see Changing an Instance's Security Groups in the Amazon VPC User Guide.

[EC2-VPC] To modify the security groups for an instance using the command line

modify-instance-attribute (AWS CLI)
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Describing Your Security Groups

You can view information about your security groups using the Amazon EC2 console or the command line.

To describe your security groups for EC2-Classic using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Select Network Platforms from the filter list, then choose EC2-Classic.

Select a security group. The Description tab displays general information. The Inbound tab displays the inbound rules.

To describe your security groups for EC2-VPC using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Select Network Platforms from the filter list, then choose EC2-VPC.

Select a security group. We display general information in the Description tab, inbound rules on the Inbound tab, and outbound rules on the Outbound tab.

To describe one or more security groups using the command line

describe-security-groups (AWS CLI)
Get-EC2SecurityGroup (AWS Tools for Windows PowerShell)
Adding Rules to a Security Group

When you add a rule to a security group, the new rule is automatically applied to any instances associated with the security group.

For more information about choosing security group rules for specific types of access, see Security Group Rules Reference.

To add rules to a security group using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups and select the security group.

On the Inbound tab, choose Edit.

In the dialog, choose Add Rule and do the following:

For Type, select the protocol.
If you select a custom TCP or UDP protocol, specify the port range in Port Range.
If you select a custom ICMP protocol, choose the ICMP type name from Protocol, and, if applicable, the code name from Port Range.
For Source, choose one of the following:
Custom: in the provided field, you must specify an IP address in CIDR notation, a CIDR block, or another security group.
Anywhere: automatically adds the 0.0.0.0/0 IPv4 CIDR block. This option enables all traffic of the specified type to reach your instance. This is acceptable for a short time in a test environment, but it's unsafe for production environments. In production, authorize only a specific IP address or range of addresses to access your instance.
Note
If your security group is in a VPC that's enabled for IPv6, the Anywhere option creates two rules—one for IPv4 traffic (0.0.0.0/0) and one for IPv6 traffic (::/0).
My IP: automatically adds the public IPv4 address of your local computer.
For Description, you can optionally specify a description for the rule.
For more information about the types of rules that you can add, see Security Group Rules Reference.

Choose Save.

For a VPC security group, you can also specify outbound rules. On the Outbound tab, choose Edit, Add Rule, and do the following:

For Type, select the protocol.
If you select a custom TCP or UDP protocol, specify the port range in Port Range.
If you select a custom ICMP protocol, choose the ICMP type name from Protocol, and, if applicable, the code name from Port Range.
For Destination, choose one of the following:
Custom: in the provided field, you must specify an IP address in CIDR notation, a CIDR block, or another security group.
Anywhere: automatically adds the 0.0.0.0/0 IPv4 CIDR block. This option enables outbound traffic to all IP addresses.
Note
If your security group is in a VPC that's enabled for IPv6, the Anywhere option creates two rules—one for IPv4 traffic (0.0.0.0/0) and one for IPv6 traffic (::/0).
My IP: automatically adds the IP address of your local computer.
For Description, you can optionally specify a description for the rule.
Choose Save.

To add one or more ingress rules to a security group using the command line

authorize-security-group-ingress (AWS CLI)
Grant-EC2SecurityGroupIngress (AWS Tools for Windows PowerShell)
[EC2-VPC] To add one or more egress rules to a security group using the command line

authorize-security-group-egress (AWS CLI)
Grant-EC2SecurityGroupEgress (AWS Tools for Windows PowerShell)
Updating Security Group Rules

When you modify the protocol, port range, or source or destination of an existing security group rule using the console, the console deletes the existing rule and adds a new one for you.

To update a security group rule using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Select the security group to update, and choose Inbound Rules to update a rule for inbound traffic or Outbound Rules to update a rule for outbound traffic.

Choose Edit. Modify the rule entry as required and choose Save.

To update the protocol, port range, or source or destination of an existing rule using the Amazon EC2 API or a command line tool, you cannot modify the rule. Instead, you must delete the existing rule and add a new rule. To update the rule description only, you can use the update-security-group-rule-descriptions-ingress and update-security-group-rule-descriptions-egress commands.

To update the description for an ingress security group rule using the command line

update-security-group-rule-descriptions-ingress (AWS CLI)
[EC2-VPC] To update the description for an egress security group rule using the command line

update-security-group-rule-descriptions-egress (AWS CLI)
Deleting Rules from a Security Group

When you delete a rule from a security group, the change is automatically applied to any instances associated with the security group.

To delete a security group rule using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Select a security group.

On the Inbound tab (for inbound rules) or Outbound tab (for outbound rules), choose Edit. Choose Delete (a cross icon) next to each rule to delete.

Choose Save.

To remove one or more ingress rules from a security group using the command line

revoke-security-group-ingress (AWS CLI)
Revoke-EC2SecurityGroupIngress (AWS Tools for Windows PowerShell)
[EC2-VPC] To remove one or more egress rules from a security group using the command line

revoke-security-group-egress (AWS CLI)
Revoke-EC2SecurityGroupEgress (AWS Tools for Windows PowerShell)
Deleting a Security Group

You can't delete a security group that is associated with an instance. You can't delete the default security group. You can't delete a security group that is referenced by a rule in another security group in the same VPC. If your security group is referenced by one of its own rules, you must delete the rule before you can delete the security group.

To delete a security group using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Select a security group and choose Actions, Delete Security Group.

Choose Yes, Delete.

To delete a security group using the command line

delete-security-group (AWS CLI)
Remove-EC2SecurityGroup (AWS Tools for Windows PowerShell)

Security Group Rules Reference

You can create a security group and add rules that reflect the role of the instance that's associated with the security group. For example, an instance that's configured as a web server needs security group rules that allow inbound HTTP and HTTPS access, and a database instance needs rules that allow access for the type of database, such as access over port 3306 for MySQL.

The following are examples of the kinds of rules that you can add to security groups for specific kinds of access.

Topics

Web server
Database server
Access from another instance in the same group
Access from local computer
Path MTU Discovery
Ping your instance
DNS server
Amazon EFS file system
Elastic Load Balancing
Web server

The following inbound rules allow HTTP and HTTPS access from any IP address. If your VPC is enabled for IPv6, you can add rules to control inbound HTTP and HTTPS traffic from IPv6 addresses.

Protocol type	Protocol number	Port	Source IP	Notes
TCP	6	80 (HTTP)	0.0.0.0/0	Allows inbound HTTP access from any IPv4 address
TCP	6	443 (HTTPS)	0.0.0.0/0	Allows inbound HTTPS access from any IPv4 address
TCP	6	80 (HTTP)	::/0	(VPC only) Allows inbound HTTP access from any IPv6 address
TCP	6	443 (HTTPS)	::/0	(VPC only) Allows inbound HTTPS access from any IPv6 address
Database server

The following inbound rules are examples of rules you might add for database access, depending on what type of database you're running on your instance. For more information about Amazon RDS instances, see the Amazon Relational Database Service User Guide.

For the source IP, specify one of the following:

A specific IP address or range of IP addresses in your local network
A security group ID for a group of instances that access the database
Protocol type	Protocol number	Port	Notes
TCP	6	1433 (MS SQL)	The default port to access a Microsoft SQL Server database, for example, on an Amazon RDS instance
TCP	6	3306 (MYSQL/Aurora)	The default port to access a MySQL or Aurora database, for example, on an Amazon RDS instance
TCP	6	5439 (Redshift)	The default port to access an Amazon Redshift cluster database.
TCP	6	5432 (PostgreSQL)	The default port to access a PostgreSQL database, for example, on an Amazon RDS instance
TCP	6	1521 (Oracle)	The default port to access an Oracle database, for example, on an Amazon RDS instance
(VPC only) You can optionally restrict outbound traffic from your database servers, for example, if you want allow access to the Internet for software updates, but restrict all other kinds of traffic. You must first remove the default outbound rule that allows all outbound traffic.

Protocol type	Protocol number	Port	Destination IP	Notes
TCP	6	80 (HTTP)	0.0.0.0/0	Allows outbound HTTP access to any IPv4 address
TCP	6	443 (HTTPS)	0.0.0.0/0	Allows outbound HTTPS access to any IPv4 address
TCP	6	80 (HTTP)	::/0	(IPv6-enabled VPC only) Allows outbound HTTP access to any IPv6 address
TCP	6	443 (HTTPS)	::/0	(IPv6-enabled VPC only) Allows outbound HTTPS access to any IPv6 address
Access from another instance in the same group

To allow instances that are associated with the same security group to communicate with each other, you must explicitly add rules for this.

The following table describes the inbound rule for a VPC security group that enables associated instances to communicate with each other. The rule allows all types of traffic.

Protocol type	Protocol number	Ports	Source IP
-1 (All)	-1 (All)	-1 (All)	The ID of the security group
The following table describes inbound rules for an EC2-Classic security group that enable associated instances to communicate with each other. The rules allow all types of traffic.

Protocol type	Protocol number	Ports	Source IP
ICMP	1	-1 (All)	The ID of the security group
TCP	6	0 - 65535 (All)	The ID of the security group
UDP	17	0 - 65535 (All)	The ID of the security group
Access from local computer

To connect to your instance, your security group must have inbound rules that allow SSH access (for Linux instances) or RDP access (for Windows instances).

Protocol type	Protocol number	Port	Source IP
TCP	6	22 (SSH)	The public IPv4 address of your computer, or a range of IP addresses in your local network. If your VPC is enabled for IPv6 and your instance has an IPv6 address, you can enter an IPv6 address or range.
TCP	6	3389 (RDP)	The public IPv4 address of your computer, or a range of IP addresses in your local network. If your VPC is enabled for IPv6 and your instance has an IPv6 address, you can enter an IPv6 address or range.
Path MTU Discovery

The path MTU is the maximum packet size that's supported on the path between the originating host and the receiving host. If a host sends a packet that's larger than the MTU of the receiving host or that's larger than the MTU of a device along the path, the receiving host returns the following ICMP message:

Destination Unreachable: Fragmentation Needed and Don't Fragment was Set
To ensure that your instance can receive this message and the packet does not get dropped, you must add an ICMP rule to your inbound security group rules.

Protocol type	Protocol number	ICMP type	ICMP code	Source IP
ICMP	1	3 (Destination Unreachable)	4 (Fragmentation Needed and Don't Fragment was Set)	The IP addresses of the hosts that communicate with your instance
Ping your instance

The ping command is a type of ICMP traffic. To ping your instance, you must add the following inbound ICMP rule.

Protocol type	Protocol number	ICMP type	ICMP code	Source IP
ICMP	1	8 (Echo)	N/A	The public IPv4 address of your computer, or a range of IPv4 addresses in your local network
To use the ping6 command to ping the IPv6 address for your instance, you must add the following inbound ICMPv6 rule.

Protocol type	Protocol number	ICMP type	ICMP code	Source IP
ICMPv6	58	128 (Echo)	0	The IPv6 address of your computer, or a range of IPv6 addresses in your local network
DNS server

If you've set up your EC2 instance as a DNS server, you must ensure that TCP and UDP traffic can reach your DNS server over port 53.

For the source IP, specify one of the following:

A specific IP address or range of IP addresses in a network
A security group ID for a group of instances in your network that require access to the DNS server
Protocol type	Protocol number	Port
TCP	6	53
UDP	17	53
Amazon EFS file system

If you're using an Amazon EFS file system with your Amazon EC2 instances, the security group that you associate with your Amazon EFS mount targets must allow traffic over the NFS protocol.

Protocol type	Protocol number	Ports	Source IP	Notes
TCP	6	2049 (NFS)	The ID of the security group.	Allows inbound NFS access from resources (including the mount target) associated with this security group.
To mount an Amazon EFS file system on your Amazon EC2 instance, you must connect to your instance. Therefore, the security group associated with your instance must have rules that allow inbound SSH from your local computer or local network.

Protocol type	Protocol number	Ports	Source IP	Notes
TCP	6	22 (SSH)	The IP address range of your local computer, or the range of IP addresses for your network.	Allows inbound SSH access from your local computer.
Elastic Load Balancing

If you're using a load balancer, the security group associated with your load balancer must have rules that allow communication with your instances or targets.

Inbound
Protocol type	Protocol number	Port	Source IP	Notes
TCP	6	The listener port	
For an Internet-facing load-balancer: 0.0.0.0/0 (all IPv4 addresses)

For an internal load-balancer: the IPv4 CIDR block of the VPC
Allow inbound traffic on the load balancer listener port.
Outbound
Protocol type	Protocol number	Port	Destination IP	Notes
TCP	6	The instance listener port	The ID of the instance security group	Allow outbound traffic to instances on the instance listener port.
TCP	6	The health check port	The ID of the instance security group	Allow outbound traffic to instances on the health check port.
The security group rules for your instances must allow the load balancer to communicate with your instances on both the listener port and the health check port.

Inbound
Protocol type	Protocol number	Port	Source IP	Notes
TCP	6	The instance listener port	
The ID of the load balancer security group
Allow traffic from the load balancer on the instance listener port.
TCP	6	The health check port	The ID of the load balancer security group	Allow traffic from the load balancer on the health check port.
For more information, see Configure Security Groups for Your Classic Load Balancer in the Classic Load Balancer Guide, and Security Groups for Your Application Load Balancer in the Application Load Balancer Guide.

Controlling Access to Amazon EC2 Resources

Your security credentials identify you to services in AWS and grant you unlimited use of your AWS resources, such as your Amazon EC2 resources. You can use features of Amazon EC2 and AWS Identity and Access Management (IAM) to allow other users, services, and applications to use your Amazon EC2 resources without sharing your security credentials. You can use IAM to control how other users use resources in your AWS account, and you can use security groups to control access to your Amazon EC2 instances. You can choose to allow full use or limited use of your Amazon EC2 resources.

Contents

Network Access to Your Instance
Amazon EC2 Permission Attributes
IAM and Amazon EC2
IAM Policies for Amazon EC2
IAM Roles for Amazon EC2
Authorizing Inbound Traffic for Your Linux Instances
Network Access to Your Instance

A security group acts as a firewall that controls the traffic allowed to reach one or more instances. When you launch an instance, you assign it one or more security groups. You add rules to each security group that control traffic for the instance. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances to which the security group is assigned.

For more information, see Authorizing Inbound Traffic for Your Linux Instances.

Amazon EC2 Permission Attributes

Your organization might have multiple AWS accounts. Amazon EC2 enables you to specify additional AWS accounts that can use your Amazon Machine Images (AMIs) and Amazon EBS snapshots. These permissions work at the AWS account level only; you can't restrict permissions for specific users within the specified AWS account. All users in the AWS account that you've specified can use the AMI or snapshot.

Each AMI has a LaunchPermission attribute that controls which AWS accounts can access the AMI. For more information, see Making an AMI Public.

Each Amazon EBS snapshot has a createVolumePermission attribute that controls which AWS accounts can use the snapshot. For more information, see Sharing an Amazon EBS Snapshot.

IAM and Amazon EC2

IAM enables you to do the following:

Create users and groups under your AWS account
Assign unique security credentials to each user under your AWS account
Control each user's permissions to perform tasks using AWS resources
Allow the users in another AWS account to share your AWS resources
Create roles for your AWS account and define the users or services that can assume them
Use existing identities for your enterprise to grant permissions to perform tasks using AWS resources
By using IAM with Amazon EC2, you can control whether users in your organization can perform a task using specific Amazon EC2 API actions and whether they can use specific AWS resources.

This topic helps you answer the following questions:

How do I create groups and users in IAM?
How do I create a policy?
What IAM policies do I need to carry out tasks in Amazon EC2?
How do I grant permissions to perform actions in Amazon EC2?
How do I grant permissions to perform actions on specific resources in Amazon EC2?
Creating an IAM Group and Users

To create an IAM group

Open the IAM console at https://console.aws.amazon.com/iam/.

In the navigation pane, choose Groups and then choose Create New Group.

For Group Name, type a name for your group, and then choose Next Step.

On the Attach Policy page, select an AWS managed policy and then choose Next Step. For example, for Amazon EC2, one of the following AWS managed policies might meet your needs:

PowerUserAccess
ReadOnlyAccess
AmazonEC2FullAccess
AmazonEC2ReadOnlyAccess
Choose Create Group.

Your new group is listed under Group Name.

To create an IAM user, add the user to your group, and create a password for the user

In the navigation pane, choose Users, Add user.

For User name, type a user name.

For Access type, select both Programmatic access and AWS Management Console access.

For Console password, choose one of the following:

Autogenerated password. Each user gets a randomly generated password that meets the current password policy in effect (if any). You can view or download the passwords when you get to the Final page.
Custom password. Each user is assigned the password that you type in the box.
Choose Next: Permissions.

On the Set permissions page, choose Add user to group. Select the checkbox next to the group that you created earlier and choose Next: Review.

Choose Create user.

To view the users' access keys (access key IDs and secret access keys), choose Show next to each password and secret access key to see. To save the access keys, choose Download .csv and then save the file to a safe location.

Important
You cannot retrieve the secret access key after you complete this step; if you misplace it you must create a new one.
Choose Close.

Give each user his or her credentials (access keys and password); this enables them to use services based on the permissions you specified for the IAM group.

Related Topics

For more information about IAM, see the following:

IAM Policies for Amazon EC2
IAM Roles for Amazon EC2
AWS Identity and Access Management (IAM)
IAM User Guide

IAM Policies for Amazon EC2

By default, IAM users don't have permission to create or modify Amazon EC2 resources, or perform tasks using the Amazon EC2 API. (This means that they also can't do so using the Amazon EC2 console or CLI.) To allow IAM users to create or modify resources and perform tasks, you must create IAM policies that grant IAM users permission to use the specific resources and API actions they'll need, and then attach those policies to the IAM users or groups that require those permissions.

When you attach a policy to a user or group of users, it allows or denies the users permission to perform the specified tasks on the specified resources. For more general information about IAM policies, see Permissions and Policies in the IAM User Guide. For more information about managing and creating custom IAM policies, see Managing IAM Policies.

Getting Started

An IAM policy must grant or deny permission to use one or more Amazon EC2 actions. It must also specify the resources that can be used with the action, which can be all resources, or in some cases, specific resources. The policy can also include conditions that you apply to the resource.

Amazon EC2 partially supports resource-level permissions. This means that for some EC2 API actions, you cannot specify which resource a user is allowed to work with for that action; instead, you have to allow users to work with all resources for that action.

Task	Topic
Understand the basic structure of a policy	Policy Syntax
Define actions in your policy	Actions for Amazon EC2
Define specific resources in your policy	Amazon Resource Names for Amazon EC2
Apply conditions to the use of the resources	Condition Keys for Amazon EC2
Work with the available resource-level permissions for Amazon EC2	Supported Resource-Level Permissions for Amazon EC2 API Actions
Test your policy	
Checking that Users Have the Required Permissions
Example policies for a CLI or SDK	Example Policies for Working With the AWS CLI or an AWS SDK
Example policies for the Amazon EC2 console	Example Policies for Working in the Amazon EC2 Console

Policy Structure

The following topics explain the structure of an IAM policy.

Topics

Policy Syntax
Actions for Amazon EC2
Amazon Resource Names for Amazon EC2
Condition Keys for Amazon EC2
Checking that Users Have the Required Permissions
Policy Syntax

An IAM policy is a JSON document that consists of one or more statements. Each statement is structured as follows:

{
  "Statement":[{
    "Effect":"effect",
    "Action":"action",
    "Resource":"arn",
    "Condition":{
      "condition":{
        "key":"value"
        }
      }
    }
  ]
}
There are various elements that make up a statement:

Effect: The effect can be Allow or Deny. By default, IAM users don't have permission to use resources and API actions, so all requests are denied. An explicit allow overrides the default. An explicit deny overrides any allows.
Action: The action is the specific API action for which you are granting or denying permission. To learn about specifying action, see Actions for Amazon EC2.
Resource: The resource that's affected by the action. Some Amazon EC2 API actions allow you to include specific resources in your policy that can be created or modified by the action. To specify a resource in the statement, you need to use its Amazon Resource Name (ARN). For more information about specifying the ARN value, see Amazon Resource Names for Amazon EC2. For more information about which API actions support which ARNs, see Supported Resource-Level Permissions for Amazon EC2 API Actions. If the API action does not support ARNs, use the * wildcard to specify that all resources can be affected by the action.
Condition: Conditions are optional. They can be used to control when your policy is in effect. For more information about specifying conditions for Amazon EC2, see Condition Keys for Amazon EC2.
For more information about example IAM policy statements for Amazon EC2, see Example Policies for Working With the AWS CLI or an AWS SDK.

Actions for Amazon EC2

In an IAM policy statement, you can specify any API action from any service that supports IAM. For Amazon EC2, use the following prefix with the name of the API action: ec2:. For example: ec2:RunInstances and ec2:CreateImage.

To specify multiple actions in a single statement, separate them with commas as follows:

"Action": ["ec2:action1", "ec2:action2"]
You can also specify multiple actions using wildcards. For example, you can specify all actions whose name begins with the word "Describe" as follows:

"Action": "ec2:Describe*"
To specify all Amazon EC2 API actions, use the * wildcard as follows:

"Action": "ec2:*"
For a list of Amazon EC2 actions, see Actions in the Amazon EC2 API Reference.

Amazon Resource Names for Amazon EC2

Each IAM policy statement applies to the resources that you specify using their ARNs.

Important
Currently, not all API actions support individual ARNs; we'll add support for additional API actions and ARNs for additional Amazon EC2 resources later. For information about which ARNs you can use with which Amazon EC2 API actions, as well as supported condition keys for each ARN, see Supported Resource-Level Permissions for Amazon EC2 API Actions.
An ARN has the following general syntax:

arn:aws:[service]:[region]:[account]:resourceType/resourcePath
service
The service (for example, ec2).

region
The region for the resource (for example, us-east-1).

account
The AWS account ID, with no hyphens (for example, 123456789012).

resourceType
The type of resource (for example, instance).

resourcePath
A path that identifies the resource. You can use the * wildcard in your paths.

For example, you can indicate a specific instance (i-1234567890abcdef0) in your statement using its ARN as follows:

"Resource": "arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0"
You can also specify all instances that belong to a specific account by using the * wildcard as follows:

"Resource": "arn:aws:ec2:us-east-1:123456789012:instance/*"
To specify all resources, or if a specific API action does not support ARNs, use the * wildcard in the Resource element as follows:

"Resource": "*"
The following table describes the ARNs for each type of resource used by the Amazon EC2 API actions.

Resource Type	ARN
All Amazon EC2 resources
arn:aws:ec2:*
All Amazon EC2 resources owned by the specified account in the specified region
arn:aws:ec2:region:account:*
Customer gateway
arn:aws:ec2:region:account:customer-gateway/cgw-id

Where cgw-id is cgw-xxxxxxxx
DHCP options set
arn:aws:ec2:region:account:dhcp-options/dhcp-options-id

Where dhcp-options-id is dopt-xxxxxxxx
Image
arn:aws:ec2:region::image/image-id

Where image-id is the ID of the AMI, AKI, or ARI, and account isn't used
Instance
arn:aws:ec2:region:account:instance/instance-id

Where instance-id is i-xxxxxxxx or i-xxxxxxxxxxxxxxxxx
Instance profile
arn:aws:iam::account:instance-profile/instance-profile-name

Where instance-profile-name is the name of the instance profile, and region isn't used
Internet gateway
arn:aws:ec2:region:account:internet-gateway/igw-id

Where igw-id is igw-xxxxxxxx
Key pair
arn:aws:ec2:region:account:key-pair/key-pair-name

Where key-pair-name is the key pair name (for example, gsg-keypair)
Network ACL
arn:aws:ec2:region:account:network-acl/nacl-id

Where nacl-id is acl-xxxxxxxx
Network interface
arn:aws:ec2:region:account:network-interface/eni-id

Where eni-id is eni-xxxxxxxx
Placement group
arn:aws:ec2:region:account:placement-group/placement-group-name

Where placement-group-name is the placement group name (for example, my-cluster)
Reserved Instance
arn:aws:ec2:region:account:reserved-instance/reservation-id

Where reservation-id is xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
Route table
arn:aws:ec2:region:account:route-table/route-table-id

Where route-table-id is rtb-xxxxxxxx
Security group
arn:aws:ec2:region:account:security-group/security-group-id

Where security-group-id is sg-xxxxxxxx
Snapshot
arn:aws:ec2:region::snapshot/snapshot-id

Where snapshot-id is snap-xxxxxxxx or snap-xxxxxxxxxxxxxxxxx, and account isn't used
Spot instance request
arn:aws:ec2:region:account:spot-instance-request/spot-instance-request-id

Where spot-instance-request-id is sir-xxxxxxxx
Subnet
arn:aws:ec2:region:account:subnet/subnet-id

Where subnet-id is subnet-xxxxxxxx
Volume
arn:aws:ec2:region:account:volume/volume-id

Where volume-id is vol-xxxxxxxx or vol-xxxxxxxxxxxxxxxxx
VPC
arn:aws:ec2:region:account:vpc/vpc-id

Where vpc-id is vpc-xxxxxxxx
VPC peering connection
arn:aws:ec2:region:account:vpc-peering-connection/vpc-peering-connection-id

Where vpc-peering connection-id is pcx-xxxxxxxx
VPN connection
arn:aws:ec2:region:account:vpn-connection/vpn-connection-id

Where vpn-connection-id is vpn-xxxxxxxx
VPN gateway
arn:aws:ec2:region:account:vpn-gateway/vpn-gateway-id

Where vpn-gateway-id is vgw-xxxxxxxx
Many Amazon EC2 API actions involve multiple resources. For example, AttachVolume attaches an Amazon EBS volume to an instance, so an IAM user must have permission to use the volume and the instance. To specify multiple resources in a single statement, separate their ARNs with commas, as follows:

"Resource": ["arn1", "arn2"]
For more general information about ARNs, see Amazon Resource Names (ARN) and AWS Service Namespaces in the Amazon Web Services General Reference. For more information about the resources that are created or modified by the Amazon EC2 actions, and the ARNs that you can use in your IAM policy statements, see Granting IAM Users Required Permissions for Amazon EC2 Resources in the Amazon EC2 API Reference.

Condition Keys for Amazon EC2

In a policy statement, you can optionally specify conditions that control when it is in effect. Each condition contains one or more key-value pairs. Condition keys are not case sensitive. We've defined AWS-wide condition keys, plus additional service-specific condition keys.

If you specify multiple conditions, or multiple keys in a single condition, we evaluate them using a logical AND operation. If you specify a single condition with multiple values for one key, we evaluate the condition using a logical OR operation. For permission to be granted, all conditions must be met.

You can also use placeholders when you specify conditions. For example, you can grant an IAM user permission to use resources with a tag that specifies his or her IAM user name. For more information, see Policy Variables in the IAM User Guide.

Important
Many condition keys are specific to a resource, and some API actions use multiple resources. If you write a policy with a condition key, use the Resource element of the statement to specify the resource to which the condition key applies. If not, the policy may prevent users from performing the action at all, because the condition check fails for the resources to which the condition key does not apply. If you do not want to specify a resource, or if you've written the Action element of your policy to include multiple API actions, then you must use the ...IfExists condition type to ensure that the condition key is ignored for resources that do not use it. For more information, see ...IfExists Conditions in the IAM User Guide.
Amazon EC2 implements the following service-specific condition keys.

Condition Key	Key-Value Pair	Evaluation Types
ec2:AccepterVpc
"ec2:AccepterVpc":"vpc-arn"

Where vpc-arn is the VPC ARN for the accepter VPC in a VPC peering connection
ARN, Null
ec2:AvailabilityZone
"ec2:AvailabilityZone":"az-api-name"

Where az-api-name is the name of the Availability Zone (for example, us-east-2a)

To list your Availability Zones, use describe-availability-zones
String, Null
ec2:CreateAction	"ec2:CreateAction":"api-name"
Where api-name is the name of the resource-creating action (for example, RunInstances)
String, Null
ec2:EbsOptimized
"ec2:EbsOptimized":"optimized-flag"

Where optimized-flag is true | false (for an instance)
Boolean, Null
ec2:Encrypted	"ec2:Encrypted":"encrypted-flag"
Where encrypted-flag is true | false (for an EBS volume)
Boolean, Null
ec2:ImageType
"ec2:ImageType":"image-type-api-name"

Where image-type-api-name is ami | aki | ari
String, Null
ec2:InstanceProfile
"ec2:InstanceProfile":"instance-profile-arn"

Where instance-profile-arn is the instance profile ARN
ARN, Null
ec2:InstanceType
"ec2:InstanceType":"instance-type-api-name"

Where instance-type-api-name is the name of the instance type.
String, Null
ec2:Owner
"ec2:Owner":"account-id"

Where account-id is amazon | aws-marketplace | aws-account-id
String, Null
ec2:ParentSnapshot
"ec2:ParentSnapshot":"snapshot-arn"

Where snapshot-arn is the snapshot ARN
ARN, Null
ec2:ParentVolume
"ec2:ParentVolume":"volume-arn"

Where volume-arn is the volume ARN
ARN, Null
ec2:PlacementGroup
"ec2:PlacementGroup":"placement-group-arn"

Where placement-group-arn is the placement group ARN
ARN, Null
ec2:PlacementGroupStrategy	
"ec2:PlacementGroupStrategy":"placement-group-strategy"

Where placement-group-strategy is cluster
String, Null
ec2:ProductCode
"ec2:ProductCode":"product-code"

Where product-code is the product code
String, Null
ec2:Public
"ec2:Public":"public-flag"

Where public-flag is true | false (for an AMI)
Boolean, Null
ec2:Region
"ec2:Region":"region-name"

Where region-name is the name of the region (for example, us-east-2). To list your regions, use describe-regions. This condition key can be used with all Amazon EC2 actions.
String, Null
ec2:RequesterVpc
"ec2:RequesterVpc":"vpc-arn"

Where vpc-arn is the VPC ARN for the requester VPC in a VPC peering connection
ARN, Null
ec2:ResourceTag/tag-key
"ec2:ResourceTag/tag-key":"tag-value"

Where tag-key and tag-value are the tag-key pair
String, Null
ec2:RootDeviceType
"ec2:RootDeviceType":"root-device-type-name"

Where root-device-type-name is ebs | instance-store
String, Null
ec2:SnapshotTime
"ec2:SnapshotTime":"time"

Where time is the snapshot creation time (for example, 2013-06-01T00:00:00Z)
Date, Null
ec2:Subnet
"ec2:Subnet":"subnet-arn"

Where subnet-arn is the subnet ARN
ARN, Null
ec2:Tenancy
"ec2:Tenancy":"tenancy-attribute"

Where tenancy-attribute is default | dedicated | host
String, Null
ec2:VolumeIops
"ec2:VolumeIops":"volume-iops"

Where volume-iops is the input/output operations per second (IOPS); the range is 100 to 20,000
Numeric, Null
ec2:VolumeSize
"ec2:VolumeSize":"volume-size"

Where volume-size is the size of the volume, in GiB
Numeric, Null
ec2:VolumeType
"ec2:VolumeType":"volume-type-name"

Where volume-type-name is gp2 for General Purpose SSD volumes, io1 for Provisioned IOPS SSD volumes, st1 for Throughput Optimized HDD volumes, sc1 for Cold HDD volumes, or standard for Magnetic volumes.
String, Null
ec2:Vpc
"ec2:Vpc":"vpc-arn"

Where vpc-arn is the VPC ARN
ARN, Null
Amazon EC2 also implements the AWS-wide condition keys (see Available Keys). The following AWS condition keys were introduced for Amazon EC2 and are supported by a limited number of additional services.

Condition Key	Key/Value Pair	Evaluation Types
aws:RequestTag/tag-key
"aws:Request/tag-key":"tag-value"

Where tag-key and tag-value are the tag key-value pair
String, Null
aws:TagKeys
"aws:TagKeys":"tag-key"

Where tag-key is a list of tag keys (for example, ["A","B"])
String, Null
For information about which condition keys you can use with which Amazon EC2 resources, on an action-by-action basis, see Supported Resource-Level Permissions for Amazon EC2 API Actions. For example policy statements for Amazon EC2, see Example Policies for Working With the AWS CLI or an AWS SDK.

Checking that Users Have the Required Permissions

After you've created an IAM policy, we recommend that you check whether it grants users the permissions to use the particular API actions and resources they need before you put the policy into production.

First, create an IAM user for testing purposes, and then attach the IAM policy that you created to the test user. Then, make a request as the test user.

If the Amazon EC2 action that you are testing creates or modifies a resource, you should make the request using the DryRun parameter (or run the AWS CLI command with the --dry-run option). In this case, the call completes the authorization check, but does not complete the operation. For example, you can check whether the user can terminate a particular instance without actually terminating it. If the test user has the required permissions, the request returns DryRunOperation; otherwise, it returns UnauthorizedOperation.

If the policy doesn't grant the user the permissions that you expected, or is overly permissive, you can adjust the policy as needed and retest until you get the desired results.

Important
It can take several minutes for policy changes to propagate before they take effect. Therefore, we recommend that you allow five minutes to pass before you test your policy updates.
If an authorization check fails, the request returns an encoded message with diagnostic information. You can decode the message using the DecodeAuthorizationMessage action. For more information, see DecodeAuthorizationMessage in the AWS Security Token Service API Reference, and decode-authorization-message in the AWS Command Line Interface Reference.

Supported Resource-Level Permissions for Amazon EC2 API Actions

Resource-level permissions refers to the ability to specify which resources users are allowed to perform actions on. Amazon EC2 has partial support for resource-level permissions. This means that for certain Amazon EC2 actions, you can control when users are allowed to use those actions based on conditions that have to be fulfilled, or specific resources that users are allowed to use. For example, you can grant users permission to launch instances, but only of a specific type, and only using a specific AMI.

The following table describes the Amazon EC2 API actions that currently support resource-level permissions, as well as the supported resources (and their ARNs) and condition keys for each action. When specifying an ARN, you can use the * wildcard in your paths; for example, when you cannot or do not want to specify exact resource IDs. For examples of using wildcards, see Example Policies for Working With the AWS CLI or an AWS SDK.

Important
If an Amazon EC2 API action is not listed in this table, then it does not support resource-level permissions. If an Amazon EC2 API action does not support resource-level permissions, you can grant users permission to use the action, but you have to specify a * for the resource element of your policy statement. For an example, see 1: Read-Only Access. For a list of Amazon EC2 API actions that currently do not support resource-level permissions, see Unsupported Resource-Level Permissions in the Amazon EC2 API Reference.
All Amazon EC2 actions support the ec2:Region condition key. For an example, see 2: Restricting Access to a Specific Region.
API Action	Resources	Condition Keys
AcceptVpcPeeringConnection	
VPC peering connection

arn:aws:ec2:region:account:vpc-peering-connection/*

arn:aws:ec2:region:account:vpc-peering-connection/vpc-peering-connection-id
ec2:AccepterVpc

ec2:Region

ec2:ResourceTag/tag-key

ec2:RequesterVpc
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id

Where vpc-id is a VPC owned by the accepter.
ec2:ResourceTag/tag-key

ec2:Region

ec2:Tenancy
AssociateIamInstanceProfile	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
AttachClassicLinkVpc	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id

Where the security group is the security group for the VPC.
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Tenancy
AttachVolume	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
Volume

arn:aws:ec2:region:account:volume/*

arn:aws:ec2:region:account:volume/volume-id
ec2:AvailabilityZone

ec2:Encrypted

ec2:ParentSnapshot

ec2:Region

ec2:ResourceTag/tag-key

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
AuthorizeSecurityGroupEgress	
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
AuthorizeSecurityGroupIngress	
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
CreateTags	
DHCP options set

arn:aws:ec2:region:account:dhcp-options/*

arn:aws:ec2:region:account:dhcp-options/dhcp-options-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Image

arn:aws:ec2:region::image/*

arn:aws:ec2:region::image/image-id
ec2:CreateAction

ec2:ImageType

ec2:Owner

ec2:Public

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType
aws:RequestTag/tag-key

aws:TagKeys
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:CreateAction

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
aws:RequestTag/tag-key

aws:TagKeys
Internet gateway

arn:aws:ec2:region:account:internet-gateway/*

arn:aws:ec2:region:account:internet-gateway/igw-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Network ACL

arn:aws:ec2:region:account:network-acl/*

arn:aws:ec2:region:account:network-acl/nacl-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
aws:RequestTag/tag-key

aws:TagKeys
Network interface

arn:aws:ec2:region:account:network-interface/*

arn:aws:ec2:region:account:network-interface/eni-id
ec2:AvailabilityZone

ec2:CreateAction

ec2:Region

ec2:Subnet

ec2:ResourceTag/tag-key

ec2:Vpc
aws:RequestTag/tag-key

aws:TagKeys
Reserved Instance

arn:aws:ec2:region:account:reserved-instance/*

arn:aws:ec2:region:account:reserved-instance/reservation-id
ec2:AvailabilityZone

ec2:CreateAction

ec2:InstanceType

ec2:ReservedInstancesOfferingType

ec2:Region

ec2:ResourceTag/tag-key

ec2:Tenancy
aws:RequestTag/tag-key

aws:TagKeys
Route table

arn:aws:ec2:region:account:route-table/*

arn:aws:ec2:region:account:route-table/route-table-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
aws:RequestTag/tag-key

aws:TagKeys
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
aws:RequestTag/tag-key

aws:TagKeys
Snapshot

arn:aws:ec2:region::snapshot/*

arn:aws:ec2:region::snapshot/snapshot-id
ec2:CreateAction

ec2:Owner

ec2:ParentVolume

ec2:Region

ec2:ResourceTag/tag-key

ec2:SnapshotTime

ec2:VolumeSize
aws:RequestTag/tag-key

aws:TagKeys
Spot Instance request

arn:aws:ec2:region:account:spot-instances-request/*

arn:aws:ec2:region:account:spot-instances-request/spot-instance-request-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Subnet

arn:aws:ec2:region:account:subnet/*

arn:aws:ec2:region:account:subnet/subnet-id
ec2:AvailabilityZone

ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
aws:RequestTag/tag-key

aws:TagKeys
Volume

arn:aws:ec2:region:account:volume/*

arn:aws:ec2:region:account:volume/volume-id
ec2:AvailabilityZone

ec2:CreateAction

ec2:Encrypted

ec2:ParentSnapshot

ec2:Region

ec2:ResourceTag/tag-key

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
aws:RequestTag/tag-key

aws:TagKeys
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key

ec2:Tenancy
aws:RequestTag/tag-key

aws:TagKeys
VPN connection

arn:aws:ec2:region:account:vpn-connection/*

arn:aws:ec2:region:account:vpn-connection/vpn-connection-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
VPN gateway

arn:aws:ec2:region:account:vpn-gateway/*

arn:aws:ec2:region:account:vpn-gateway/vpn-gateway-id
ec2:CreateAction

ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
CreateVolume	
Volume

arn:aws:ec2:region:account:volume/*
ec2:AvailabilityZone

ec2:Encrypted

ec2:ParentSnapshot

ec2:Region

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
aws:RequestTag/tag-key

aws:TagKeys
CreateVpcPeeringConnection	
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id

Where vpc-id is a requester VPC.
ec2:ResourceTag/tag-key

ec2:Region

ec2:Tenancy
VPC peering connection

arn:aws:ec2:region:account:vpc-peering-connection/*
ec2:AccepterVpc

ec2:Region

ec2:RequesterVpc
DeleteCustomerGateway	
Customer gateway

arn:aws:ec2:region:account:customer-gateway/*

arn:aws:ec2:region:account:customer-gateway/cgw-id
ec2:Region

ec2:ResourceTag/tag-key
DeleteDhcpOptions	
DHCP options set

arn:aws:ec2:region:account:dhcp-options/*

arn:aws:ec2:region:account:dhcp-options/dhcp-options-id
ec2:Region

ec2:ResourceTag/tag-key
DeleteInternetGateway	
Internet gateway

arn:aws:ec2:region:account:internet-gateway/*

arn:aws:ec2:region:account:internet-gateway/igw-id
ec2:Region

ec2:ResourceTag/tag-key
DeleteNetworkAcl	
Network ACL

arn:aws:ec2:region:account:network-acl/*

arn:aws:ec2:region:account:network-acl/nacl-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
DeleteNetworkAclEntry	
Network ACL

arn:aws:ec2:region:account:network-acl/*

arn:aws:ec2:region:account:network-acl/nacl-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
DeleteRoute	
Route table

arn:aws:ec2:region:account:route-table/*

arn:aws:ec2:region:account:route-table/route-table-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
DeleteRouteTable	
Route table

arn:aws:ec2:region:account:route-table/*

arn:aws:ec2:region:account:route-table/route-table-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
DeleteSecurityGroup	
Security group

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
DeleteTags	
DHCP options set

arn:aws:ec2:region:account:dhcp-options/*

arn:aws:ec2:region:account:dhcp-options/dhcp-options-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Image

arn:aws:ec2:region::image/*

arn:aws:ec2:region::image/image-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Internet gateway

arn:aws:ec2:region:account:internet-gateway/*

arn:aws:ec2:region:account:internet-gateway/igw-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Network ACL

arn:aws:ec2:region:account:network-acl/*

arn:aws:ec2:region:account:network-acl/nacl-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Network interface

arn:aws:ec2:region:account:network-interface/*

arn:aws:ec2:region:account:network-interface/eni-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Reserved Instance

arn:aws:ec2:region:account:reserved-instance/*

arn:aws:ec2:region:account:reserved-instance/reservation-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Route table

arn:aws:ec2:region:account:route-table/*

arn:aws:ec2:region:account:route-table/route-table-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Snapshot

arn:aws:ec2:region::snapshot/*

arn:aws:ec2:region::snapshot/snapshot-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Spot Instance request

arn:aws:ec2:region:account:spot-instances-request/*

arn:aws:ec2:region:account:spot-instances-request/spot-instance-request-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Subnet

arn:aws:ec2:region:account:subnet/*

arn:aws:ec2:region:account:subnet/subnet-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
Volume

arn:aws:ec2:region:account:volume/*

arn:aws:ec2:region:account:volume/volume-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
VPN connection

arn:aws:ec2:region:account:vpn-connection/*

arn:aws:ec2:region:account:vpn-connection/vpn-connection-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
VPN gateway

arn:aws:ec2:region:account:vpn-gateway/*

arn:aws:ec2:region:account:vpn-gateway/vpn-gateway-id
ec2:Region

ec2:ResourceTag/tag-key
aws:RequestTag/tag-key

aws:TagKeys
DeleteVolume	
Volume

arn:aws:ec2:region:account:volume/*

arn:aws:ec2:region:account:volume/volume-id
ec2:AvailabilityZone

ec2:Encrypted

ec2:ParentSnapshot

ec2:Region

ec2:ResourceTag/tag-key

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
DeleteVpcPeeringConnection	
VPC peering connection

arn:aws:ec2:region:account:vpc-peering-connection/*

arn:aws:ec2:region:account:vpc-peering-connection/vpc-peering-connection-id
ec2:AccepterVpc

ec2:Region

ec2:ResourceTag/tag-key

ec2:RequesterVpc
DetachClassicLinkVpc	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Tenancy
DetachVolume	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
Volume

arn:aws:ec2:region:account:volume/*

arn:aws:ec2:region:account:volume/volume-id
ec2:AvailabilityZone

ec2:Encrypted

ec2:ParentSnapshot

ec2:Region

ec2:ResourceTag/tag-key

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
DisableVpcClassicLink	
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Tenancy
DisassociateIamInstanceProfile	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
EnableVpcClassicLink	
VPC

arn:aws:ec2:region:account:vpc/*

arn:aws:ec2:region:account:vpc/vpc-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Tenancy
GetConsoleScreenshot	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
RebootInstances	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
RejectVpcPeeringConnection	
VPC peering connection

arn:aws:ec2:region:account:vpc-peering-connection/*

arn:aws:ec2:region:account:vpc-peering-connection/vpc-peering-connection-id
ec2:AccepterVpc

ec2:Region

ec2:ResourceTag/tag-key

ec2:RequesterVpc
ReplaceIamInstanceProfileAssociation	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
RevokeSecurityGroupEgress	
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
RevokeSecurityGroupIngress	
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
RunInstances	
Image

arn:aws:ec2:region::image/*

arn:aws:ec2:region::image/image-id
ec2:ImageType

ec2:Owner

ec2:Public

ec2:Region

ec2:RootDeviceType

ec2:ResourceTag/tag-key
Instance

arn:aws:ec2:region:account:instance/*
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:RootDeviceType

ec2:Tenancy
aws:RequestTag/tag-key

aws:TagKeys
Key pair

arn:aws:ec2:region:account:key-pair/*

arn:aws:ec2:region:account:key-pair/key-pair-name
ec2:Region
Network interface

arn:aws:ec2:region:account:network-interface/*

arn:aws:ec2:region:account:network-interface/eni-id
ec2:AvailabilityZone

ec2:Region

ec2:Subnet

ec2:ResourceTag/tag-key

ec2:Vpc
Placement group

arn:aws:ec2:region:account:placement-group/*

arn:aws:ec2:region:account:placement-group/placement-group-name
ec2:Region

ec2:PlacementGroupStrategy
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
Snapshot

arn:aws:ec2:region::snapshot/*

arn:aws:ec2:region::snapshot/snapshot-id
ec2:Owner

ec2:ParentVolume

ec2:Region

ec2:SnapshotTime

ec2:ResourceTag/tag-key

ec2:VolumeSize
Subnet

arn:aws:ec2:region:account:subnet/*

arn:aws:ec2:region:account:subnet/subnet-id
ec2:AvailabilityZone

ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
Volume

arn:aws:ec2:region:account:volume/*
ec2:AvailabilityZone

ec2:Encrypted

ec2:ParentSnapshot

ec2:Region

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
aws:RequestTag/tag-key

aws:TagKeys
StartInstances	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
StopInstances	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
TerminateInstances	
Instance

arn:aws:ec2:region:account:instance/*

arn:aws:ec2:region:account:instance/instance-id
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:ResourceTag/tag-key

ec2:RootDeviceType

ec2:Tenancy
UpdateSecurityGroupRuleDescriptionsEgress	
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
UpdateSecurityGroupRuleDescriptionsIngress	
Security group

arn:aws:ec2:region:account:security-group/*

arn:aws:ec2:region:account:security-group/security-group-id
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
Resource-Level Permissions for RunInstances

The RunInstances API action launches one or more instances, and creates and uses a number of Amazon EC2 resources. The action requires an AMI and creates an instance; and the instance must be associated with a security group. Launching into a VPC requires a subnet, and creates a network interface. Launching from an Amazon EBS-backed AMI creates a volume. The user must have permission to use these resources, so they must be specified in the Resource element of any policy that uses resource-level permissions for the ec2:RunInstances action. If you don't intend to use resource-level permissions with the ec2:RunInstances action, you can specify the * wildcard in the Resource element of your statement instead of individual ARNs.

If you are using resource-level permissions, the following table describes the minimum resources required to use the ec2:RunInstances action.

Type of launch	Resources required	Condition keys
Launching into EC2-Classic using an instance store-backed AMI	
arn:aws:ec2:region:account:instance/*
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:RootDeviceType

ec2:Tenancy
arn:aws:ec2:region::image/* (or a specific AMI ID)	
ec2:ImageType

ec2:Owner

ec2:Public

ec2:Region

ec2:RootDeviceType

ec2:ResourceTag/tag-key
arn:aws:ec2:region:account:security-group/* (or a specific security group ID)	
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
Launching into EC2-Classic using an Amazon EBS-backed AMI	
arn:aws:ec2:region:account:instance/*
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:RootDeviceType

ec2:Tenancy
arn:aws:ec2:region::image/* (or a specific AMI ID)	
ec2:ImageType

ec2:Owner

ec2:Public

ec2:Region

ec2:RootDeviceType

ec2:ResourceTag/tag-key
arn:aws:ec2:region:account:security-group/* (or a specific security group ID)	
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
arn:aws:ec2:region:account:volume/*	
ec2:AvailabilityZone

ec2:ParentSnapshot

ec2:Region

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
Launching into a VPC using an instance store-backed AMI	
arn:aws:ec2:region:account:instance/*
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:RootDeviceType

ec2:Tenancy
arn:aws:ec2:region::image/* (or a specific AMI ID)	
ec2:ImageType

ec2:Owner

ec2:Public

ec2:Region

ec2:RootDeviceType

ec2:ResourceTag/tag-key
arn:aws:ec2:region:account:security-group/* (or a specific security group ID)	
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
arn:aws:ec2:region:account:network-interface/* (or a specific network interface ID)	
ec2:AvailabilityZone

ec2:Region

ec2:Subnet

ec2:ResourceTag/tag-key

ec2:Vpc
arn:aws:ec2:region:account:subnet/* (or a specific subnet ID)	
ec2:AvailabilityZone

ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
Launching into a VPC using an Amazon EBS-backed AMI	
arn:aws:ec2:region:account:instance/*
ec2:AvailabilityZone

ec2:EbsOptimized

ec2:InstanceProfile

ec2:InstanceType

ec2:PlacementGroup

ec2:Region

ec2:RootDeviceType

ec2:Tenancy
arn:aws:ec2:region::image/* (or a specific AMI ID)	
ec2:ImageType

ec2:Owner

ec2:Public

ec2:Region

ec2:RootDeviceType

ec2:ResourceTag/tag-key
arn:aws:ec2:region:account:security-group/* (or a specific security group ID)	
ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
arn:aws:ec2:region:account:network-interface/* (or a specific network interface ID)	
ec2:AvailabilityZone

ec2:Region

ec2:Subnet

ec2:ResourceTag/tag-key

ec2:Vpc
arn:aws:ec2:region:account:volume/*	
ec2:AvailabilityZone

ec2:Encrypted

ec2:ParentSnapshot

ec2:Region

ec2:VolumeIops

ec2:VolumeSize

ec2:VolumeType
arn:aws:ec2:region:account:subnet/* (or a specific subnet ID)	
ec2:AvailabilityZone

ec2:Region

ec2:ResourceTag/tag-key

ec2:Vpc
We recommend that you also specify the key pair resource in your policy — even though it's not required to launch an instance, you cannot connect to your instance without a key pair. For examples of using resource-level permissions with the ec2:RunInstances action, see 5: Launching Instances (RunInstances).

For additional information about resource-level permissions in Amazon EC2, see the following AWS Security Blog post: Demystifying EC2 Resource-Level Permissions.

Resource-Level Permissions for Tagging

Some resource-creating Amazon EC2 API actions enable you to specify tags when you create the resource. For more information, see Tagging Your Resources.

To enable users to tag resources on creation, they must have permission to use the action that creates the resource (for example, ec2:RunInstances or ec2:CreateVolume). If tags are specified in the resource-creating action, Amazon performs additional authorization on the ec2:CreateTags action to verify if users have permission to create tags. Therefore, users must also have explicit permission to use the ec2:CreateTags action.

For the ec2:CreateTags action, you can use the ec2:CreateAction condition key to restrict tagging permissions to the resource-creating actions only. For example, the following policy allows users to launch instances and apply any tags to instances and volumes during launch. Users are not permitted to tag any existing resources (they cannot call the ec2:CreateTags action directly).

Copy
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:RunInstances"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateTags"
      ],
      "Resource": "arn:aws:ec2:region:account:*/*",
      "Condition": {
         "StringEquals": {
             "ec2:CreateAction" : "RunInstances"
          }
       }
    }
  ]
}
Similarly, the following policy allows users to create volumes and apply any tags to the volumes during volume creation. Users are not permitted to tag any existing resources (they cannot call the ec2:CreateTags action directly).

Copy
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateVolume"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateTags"
      ],
      "Resource": "arn:aws:ec2:region:account:*/*",
      "Condition": {
         "StringEquals": {
             "ec2:CreateAction" : "CreateVolume"
          }
       }
    }
  ]
}
The ec2:CreateTags action is only evaluated if tags are applied during the resource-creating action. Therefore, a user that has permission to create a resource (assuming there are no tagging conditions) does not require permission to use the ec2:CreateTags action if no tags are specified in the request. However, if the user attempts to create a resource with tags, the request fails if the user does not have permission to use the ec2:CreateTags action.

You can control the tag keys and values that are applied to resources by using the following condition keys:

aws:RequestTag: To indicate that a particular tag key or tag key and value must be present in a request. Other tags can also be specified in the request.
Use with the StringEquals condition operator to enforce a specific tag key and value combination, for example, to enforce the tag cost-center=cc123:
"StringEquals": { "aws:RequestTag/cost-center": "cc123" }
Use with the StringLike condition operator to enforce a specific tag key in the request; for example, to enforce the tag key purpose:
"StringLike": { "aws:RequestTag/purpose": "*" }
aws:TagKeys: To enforce the tag keys that are used in the request.
Use with the ForAllValues modifier to enforce specific tag keys if they are provided in the request (if tags are specified in the request, only specific tag keys are allowed; no other tags are allowed). For example, the tag keys environment or cost-center are allowed:
"ForAllValues:StringEquals": { "aws:TagKeys": ["environment","cost-center"] }
Use with the ForAnyValue modifier to enforce the presence of at least one of the specified tag keys in the request. For example, at least one of the tag keys environment or webserver must be present in the request:
"ForAnyValue:StringEquals": { "aws:TagKeys": ["environment","webserver"] }
These condition keys can be applied to resource-creating actions that support tagging, as well as the ec2:CreateTags and ec2:DeleteTags actions.

To force users to specify tags when they create a resource, you must use the aws:RequestTag condition key or the aws:TagKeys condition key with the ForAnyValue modifier on the resource-creating action. The ec2:CreateTags action is not evaluated if a user does not specify tags for the resource-creating action.

For conditions, the condition key is not case-sensitive and the condition value is case-sensitive. Therefore, to enforce the case-sensitivity of a tag key, use the aws:TagKeys condition key, where the tag key is specified as a value in the condition.

For more information about multi-value conditions, see Creating a Condition That Tests Multiple Key Values in the IAM User Guide. For example IAM policies, see Example Policies for Working With the AWS CLI or an AWS SDK.

Example Policies for Working With the AWS CLI or an AWS SDK

The following examples show policy statements that you could use to control the permissions that IAM users have to Amazon EC2. These policies are designed for requests that are made with the AWS CLI or an AWS SDK. For example policies for working in the Amazon EC2 console, see Example Policies for Working in the Amazon EC2 Console. For examples of IAM policies specific to Amazon VPC, see Controlling Access to Amazon VPC Resources.

Contents

1: Read-Only Access
2: Restricting Access to a Specific Region
3: Working with Instances
4. Working with Volumes
5: Launching Instances (RunInstances)
6. Working with ClassicLink
7. Working with Reserved Instances
8. Tagging Resources
9: Working with IAM Roles
1: Read-Only Access

The following policy grants users permission to use all Amazon EC2 API actions whose names begin with Describe. The Resource element uses a wildcard to indicate that users can specify all resources with these API actions. The * wildcard is also necessary in cases where the API action does not support resource-level permissions. For more information about which ARNs you can use with which Amazon EC2 API actions, see Supported Resource-Level Permissions for Amazon EC2 API Actions.

Users don't have permission to perform any actions on the resources (unless another statement grants them permission to do so) because they're denied permission to use API actions by default.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    }
   ]
}
2: Restricting Access to a Specific Region

The following policy grants users permission to use all Amazon EC2 API actions in the EU (Frankfurt) region only. Users cannot view, create, modify, or delete resources in any other region.

Copy
{
  "Version":"2012-10-17",
  "Statement":[
    {
    "Effect": "Allow",
    "Action": "ec2:*",
    "Resource": "*",
    "Condition": {
      "StringEquals": {
        "ec2:Region": "eu-central-1"
      }
    }
  }
  ]
}
3: Working with Instances

Topics

Describe, launch, stop, start, and terminate all instances
Describe all instances, and stop, start, and terminate only particular instances
Describe, launch, stop, start, and terminate all instances

The following policy grants users permission to use the API actions specified in the Action element. The Resource element uses a * wildcard to indicate that users can specify all resources with these API actions. The * wildcard is also necessary in cases where the API action does not support resource-level permissions. For more information about which ARNs you can use with which Amazon EC2 API actions, see Supported Resource-Level Permissions for Amazon EC2 API Actions.

The users don't have permission to use any other API actions (unless another statement grants them permission to do so) because users are denied permission to use API actions by default.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances", "ec2:DescribeImages",
        "ec2:DescribeKeyPairs", "ec2:DescribeSecurityGroups",
        "ec2:DescribeAvailabilityZones",
        "ec2:RunInstances", "ec2:TerminateInstances",
        "ec2:StopInstances", "ec2:StartInstances"
      ],
      "Resource": "*"
    }
   ]
}
Describe all instances, and stop, start, and terminate only particular instances

The following policy allows users to describe all instances, to start and stop only instances i-1234567890abcdef0 and i-0598c7d356eba48d7, and to terminate only instances in the US East (N. Virginia) Region (us-east-1) with the resource tag "purpose=test".

The first statement uses a * wildcard for the Resource element to indicate that users can specify all resources with the action; in this case, they can list all instances. The * wildcard is also necessary in cases where the API action does not support resource-level permissions (in this case, ec2:DescribeInstances). For more information about which ARNs you can use with which Amazon EC2 API actions, see Supported Resource-Level Permissions for Amazon EC2 API Actions.

The second statement uses resource-level permissions for the StopInstances and StartInstances actions. The specific instances are indicated by their ARNs in the Resource element.

The third statement allows users to terminate all instances in the US East (N. Virginia) Region (us-east-1) that belong to the specified AWS account, but only where the instance has the tag "purpose=test". The Condition element qualifies when the policy statement is in effect.

Copy
{
   "Version": "2012-10-17",
   "Statement": [
   {
   "Effect": "Allow",
      "Action": "ec2:DescribeInstances",
      "Resource": "*"
   },
   {
      "Effect": "Allow",
      "Action": [
        "ec2:StopInstances", 
        "ec2:StartInstances"
      ],
      "Resource": [
      "arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0",
      "arn:aws:ec2:us-east-1:123456789012:instance/i-0598c7d356eba48d7"
      ]
    },
    {
      "Effect": "Allow",
      "Action": "ec2:TerminateInstances",
      "Resource": "arn:aws:ec2:us-east-1:123456789012:instance/*",
      "Condition": {
         "StringEquals": {
            "ec2:ResourceTag/purpose": "test"
         }
      }
   }

   ]
}
4. Working with Volumes

Topics

Attaching and detaching volumes
Creating a volume
Creating a volume with tags
Attaching and detaching volumes

When an API action requires a caller to specify multiple resources, you must create a policy statement that allows users to access all required resources. If you need to use a Condition element with one or more of these resources, you must create multiple statements as shown in this example.

The following policy allows users to attach volumes with the tag "volume_user=iam-user-name" to instances with the tag "department=dev", and to detach those volumes from those instances. If you attach this policy to an IAM group, the aws:username policy variable gives each IAM user in the group permission to attach or detach volumes from the instances with a tag named volume_user that has his or her IAM user name as a value.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
        "ec2:AttachVolume",
        "ec2:DetachVolume"
      ],
      "Resource": "arn:aws:ec2:us-east-1:123456789012:instance/*",
      "Condition": {
        "StringEquals": {
          "ec2:ResourceTag/department": "dev"
        }
      }
   },
   {
      "Effect": "Allow",
      "Action": [
        "ec2:AttachVolume",
        "ec2:DetachVolume"
      ],
      "Resource": "arn:aws:ec2:us-east-1:123456789012:volume/*",
      "Condition": {
        "StringEquals": {
          "ec2:ResourceTag/volume_user": "${aws:username}"
        }
      }
   }
  ]
}
Creating a volume

The following policy allows users to use the CreateVolume API action. The user is allowed to create a volume only if the volume is encrypted and only if the volume size is less than 20 GiB.

Copy
{
  "Version": "2012-10-17", 
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateVolume"
      ],
      "Resource": "arn:aws:ec2:us-east-1:123456789012:volume/*",
      "Condition":{
         "NumericLessThan": {
             "ec2:VolumeSize" : "20"
          },
          "Bool":{
              "ec2:Encrypted" : "true"
          }
       }
    }
  ]
}
Creating a volume with tags

The following policy includes the aws:RequestTag condition key that requires users to tag any volumes they create with the tags costcenter=115 and stack=prod. The aws:TagKeys condition key uses the ForAllValues modifier to indicate that only the keys costcenter and stack are allowed in the request (no other tags can be specified). If users don't pass these specific tags, or if they don't specify tags at all, the request fails.

For resource-creating actions that apply tags, users must also have permission to use the CreateTags action. The second statement uses the ec2:CreateAction condition key to allow users to create tags only in the context of CreateVolume. Users cannot tag existing volumes or any other resources. For more information, see Resource-Level Permissions for Tagging.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCreateTaggedVolumes",
      "Effect": "Allow",
      "Action": "ec2:CreateVolume",
      "Resource": "arn:aws:ec2:us-east-1:123456789012:volume/*",
      "Condition": {
        "StringEquals": {
          "aws:RequestTag/costcenter": "115",
          "aws:RequestTag/stack": "prod"
         },
         "ForAllValues:StringEquals": {
             "aws:TagKeys": ["costcenter","stack"]
         }
       }
     },
     {
       "Effect": "Allow",
       "Action": [
         "ec2:CreateTags"
       ],
       "Resource": "arn:aws:ec2:us-east-1:123456789012:volume/*",
       "Condition": {
         "StringEquals": {
             "ec2:CreateAction" : "CreateVolume"
        }
      }
    }
  ]
}
The following policy allows users to create a volume without having to specify tags. The CreateTags action is only evaluated if tags are specified in the CreateVolume request. If users do specify tags, the tag must be purpose=test. No other tags are allowed in the request.

Copy
{
  "Version": "2012-10-17", 
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:CreateVolume",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateTags"
      ],
      "Resource": "arn:aws:ec2:us-east-1:1234567890:volume/*",
      "Condition": {
         "StringEquals": {
             "aws:RequestTag/purpose": "test",
             "ec2:CreateAction" : "CreateVolume"
          },
         "ForAllValues:StringEquals": {
             "aws:TagKeys": "purpose"
          }
       }
    }
  ]
}
5: Launching Instances (RunInstances)

The RunInstances API action launches one or more instances. RunInstances requires an AMI and creates an instance; and users can specify a key pair and security group in the request. Launching into EC2-VPC requires a subnet, and creates a network interface. Launching from an Amazon EBS-backed AMI creates a volume. Therefore, the user must have permission to use these Amazon EC2 resources. The caller can also configure the instance using optional parameters to RunInstances, such as the instance type and a subnet. You can create a policy statement that requires users to specify an optional parameter, or restricts users to particular values for a parameter. The examples in this section demonstrate some of the many possible ways that you can control the configuration of an instance that a user can launch.

Note that by default, users don't have permission to describe, start, stop, or terminate the resulting instances. One way to grant the users permission to manage the resulting instances is to create a specific tag for each instance, and then create a statement that enables them to manage instances with that tag. For more information, see 3: Working with Instances.

Topics

AMI
Instance Type
Subnet
EBS Volumes
Applying tags
AMI

The following policy allows users to launch instances using only the AMIs that have the specified tag, "department=dev", associated with them. The users can't launch instances using other AMIs because the Condition element of the first statement requires that users specify an AMI that has this tag. The users also can't launch into a subnet, as the policy does not grant permissions for the subnet and network interface resources. They can, however, launch into EC2-Classic. The second statement uses a wildcard to enable users to create instance resources, and requires users to specify the key pair project_keypair and the security group sg-1a2b3c4d. Users are still able to launch instances without a key pair.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [ 
         "arn:aws:ec2:region::image/ami-*"
      ],
      "Condition": {
         "StringEquals": {
            "ec2:ResourceTag/department": "dev"
         }
      }
   },
   {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [ 
          "arn:aws:ec2:region:account:instance/*",
          "arn:aws:ec2:region:account:volume/*",
          "arn:aws:ec2:region:account:key-pair/project_keypair",
          "arn:aws:ec2:region:account:security-group/sg-1a2b3c4d"
         ]
      }
   ]
}
Alternatively, the following policy allows users to launch instances using only the specified AMIs, ami-9e1670f7 and ami-45cf5c3c. The users can't launch an instance using other AMIs (unless another statement grants the users permission to do so), and the users can't launch an instance into a subnet.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
        "arn:aws:ec2:region::image/ami-9e1670f7",
        "arn:aws:ec2:region::image/ami-45cf5c3c",
        "arn:aws:ec2:region:account:instance/*",
        "arn:aws:ec2:region:account:volume/*",
        "arn:aws:ec2:region:account:key-pair/*",
        "arn:aws:ec2:region:account:security-group/*"
      ]
    }
   ]
}
Alternatively, the following policy allows users to launch instances from all AMIs owned by Amazon. The Condition element of the first statement tests whether ec2:Owner is amazon. The users can't launch an instance using other AMIs (unless another statement grants the users permission to do so). The users are able to launch an instance into a subnet.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [ 
         "arn:aws:ec2:region::image/ami-*"
      ],
      "Condition": {
         "StringEquals": {
            "ec2:Owner": "amazon"
         }
      }
   },
   {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [ 
         "arn:aws:ec2:region:account:instance/*",
         "arn:aws:ec2:region:account:subnet/*",
         "arn:aws:ec2:region:account:volume/*",
         "arn:aws:ec2:region:account:network-interface/*",
         "arn:aws:ec2:region:account:key-pair/*",
         "arn:aws:ec2:region:account:security-group/*"
         ]
      }
   ]
}
Instance Type

The following policy allows users to launch instances using only the t2.micro or t2.small instance type, which you might do to control costs. The users can't launch larger instances because the Condition element of the first statement tests whether ec2:InstanceType is either t2.micro or t2.small.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:region:account:instance/*"
      ],
      "Condition": {
         "StringEquals": {
            "ec2:InstanceType": ["t2.micro", "t2.small"]
         }
      }
   },
   {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:region::image/ami-*",
         "arn:aws:ec2:region:account:subnet/*",
         "arn:aws:ec2:region:account:network-interface/*",
         "arn:aws:ec2:region:account:volume/*",
         "arn:aws:ec2:region:account:key-pair/*",
         "arn:aws:ec2:region:account:security-group/*"
         ]
      }
   ]
}
Alternatively, you can create a policy that denies users permission to launch any instances except t2.micro and t2.small instance types.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:region:account:instance/*"
      ],
      "Condition": {
         "StringNotEquals": {
            "ec2:InstanceType": ["t2.micro", "t2.small"]
         }
      }
   },
   {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:region::image/ami-*",
         "arn:aws:ec2:region:account:network-interface/*",
         "arn:aws:ec2:region:account:instance/*",
         "arn:aws:ec2:region:account:subnet/*",
         "arn:aws:ec2:region:account:volume/*",
         "arn:aws:ec2:region:account:key-pair/*",
         "arn:aws:ec2:region:account:security-group/*"
         ]
      }
   ]
}
Subnet

The following policy allows users to launch instances using only the specified subnet, subnet-12345678. The group can't launch instances into any another subnet (unless another statement grants the users permission to do so). Users are still able to launch instances into EC2-Classic.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
        "arn:aws:ec2:region:account:subnet/subnet-12345678",
        "arn:aws:ec2:region:account:network-interface/*",
        "arn:aws:ec2:region:account:instance/*",
        "arn:aws:ec2:region:account:volume/*",
        "arn:aws:ec2:region::image/ami-*",
        "arn:aws:ec2:region:account:key-pair/*",
        "arn:aws:ec2:region:account:security-group/*"
      ]
    }
   ]
}
Alternatively, you could create a policy that denies users permission to launch an instance into any other subnet. The statement does this by denying permission to create a network interface, except where subnet subnet-12345678 is specified. This denial overrides any other policies that are created to allow launching instances into other subnets. Users are still able to launch instances into EC2-Classic.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:region:account:network-interface/*"
      ],
      "Condition": {
         "ArnNotEquals": {
            "ec2:Subnet": "arn:aws:ec2:region:account:subnet/subnet-12345678"
         }
      }
   },
   {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:region::image/ami-*",
         "arn:aws:ec2:region:account:network-interface/*",
         "arn:aws:ec2:region:account:instance/*",
         "arn:aws:ec2:region:account:subnet/*",
         "arn:aws:ec2:region:account:volume/*",
         "arn:aws:ec2:region:account:key-pair/*",
         "arn:aws:ec2:region:account:security-group/*"
         ]
      }
   ]
}
EBS Volumes

The following policy allows users to launch instances only if the EBS volumes for the instance are encrypted. The user must launch an instance from an AMI that was created with encrypted snapshots, to ensure that the root volume is encrypted. Any additional volume that the user attaches to the instance during launch must also be encrypted.

Copy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:RunInstances",
            "Resource": [
                "arn:aws:ec2:*:*:volume/*"
            ],
            "Condition": {
                "Bool": {
                    "ec2:Encrypted": "true"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": "ec2:RunInstances",
            "Resource": [
                "arn:aws:ec2:*::image/ami-*",
                "arn:aws:ec2:*:*:network-interface/*",
                "arn:aws:ec2:*:*:instance/*",
                "arn:aws:ec2:*:*:subnet/*",
                "arn:aws:ec2:*:*:key-pair/*",
                "arn:aws:ec2:*:*:security-group/*"
            ]
        }
    ]
}
Applying tags

The following policy allows users to launch instances and tag the instances during creation. For resource-creating actions that apply tags, users must have permission to use the CreateTags action. The second statement uses the ec2:CreateAction condition key to allow users to create tags only in the context of RunInstances, and only for instances. Users cannot tag existing resources, and users cannot tag volumes using the RunInstances request.

For more information, see Resource-Level Permissions for Tagging.

Copy
{
  "Version": "2012-10-17", 
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:RunInstances"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateTags"
      ],
      "Resource": "arn:aws:ec2:us-east-1:123456789012:instance/*",
      "Condition": {
         "StringEquals": {
             "ec2:CreateAction" : "RunInstances"
          }
       }
    }
  ]
}
The following policy includes the aws:RequestTag condition key that requires users to tag any instances and volumes that are created by RunInstances with the tags environment=production and purpose=webserver. The aws:TagKeys condition key uses the ForAllValues modifier to indicate that only the keys environment and purpose are allowed in the request (no other tags can be specified). If no tags are specified in the request, the request fails.

Copy
{
  "Version": "2012-10-17", 
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:RunInstances"
      ],
      "Resource": [
         "arn:aws:ec2:region::image/*",
         "arn:aws:ec2:region:account:subnet/*",
         "arn:aws:ec2:region:account:network-interface/*",
         "arn:aws:ec2:region:account:security-group/*",
         "arn:aws:ec2:region:account:key-pair/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:RunInstances"
      ],
      "Resource": [
          "arn:aws:ec2:region:account:volume/*",
          "arn:aws:ec2:region:account:instance/*"
      ],
      "Condition": {
         "StringEquals": {
             "aws:RequestTag/environment": "production" ,
             "aws:RequestTag/purpose": "webserver"
          },
          "ForAllValues:StringEquals": {
              "aws:TagKeys": ["environment","purpose"]
          }
       }
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateTags"
      ],
      "Resource": "arn:aws:ec2:region:account:*/*",
      "Condition": {
         "StringEquals": {
             "ec2:CreateAction" : "RunInstances"
          }
       }
    }
  ]
}
The following policy uses the ForAnyValue modifier on the aws:TagKeys condition to indicate that at least one tag must be specified in the request, and it must contain the key environment or webserver. The tag must be applied to both instances and volumes. Any tag values can be specified in the request.

Copy
{
  "Version": "2012-10-17", 
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:RunInstances"
      ],
      "Resource": [
         "arn:aws:ec2:region::image/*",
         "arn:aws:ec2:region:account:subnet/*",
         "arn:aws:ec2:region:account:network-interface/*",
         "arn:aws:ec2:region:account:security-group/*",
         "arn:aws:ec2:region:account:key-pair/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
          "ec2:RunInstances"
      ],
      "Resource": [
          "arn:aws:ec2:region:account:volume/*",
          "arn:aws:ec2:region:account:instance/*"
      ],
      "Condition": {
          "ForAnyValue:StringEquals": {
              "aws:TagKeys": ["environment","webserver"]
          }
       }
    },
    {
      "Effect": "Allow",
      "Action": [
          "ec2:CreateTags"
      ],
      "Resource": "arn:aws:ec2:region:account:*/*",
      "Condition": {
          "StringEquals": {
              "ec2:CreateAction" : "RunInstances"
          }
       }
    }
  ]
}
In the following policy, users do not have to specify tags in the request, but if they do, the tag must be purpose=test. No other tags are allowed. Users can apply the tags to any taggable resource in the RunInstances request.

Copy
{
  "Version": "2012-10-17", 
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:RunInstances"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:CreateTags"
      ],
      "Resource": "arn:aws:ec2:region:account:*/*",
      "Condition": {
         "StringEquals": {
             "aws:RequestTag/purpose": "test",
             "ec2:CreateAction" : "RunInstances"
          },
          "ForAllValues:StringEquals": {
              "aws:TagKeys": "purpose"
          }
       }
    }
  ]
}
6. Working with ClassicLink

You can enable a VPC for ClassicLink and then link an EC2-Classic instance to the VPC. You can also view your ClassicLink-enabled VPCs, and all of your EC2-Classic instances that are linked to a VPC. You can create policies with resource-level permission for the ec2:EnableVpcClassicLink, ec2:DisableVpcClassicLink, ec2:AttachClassicLinkVpc, and ec2:DetachClassicLinkVpc actions to control how users are able to use those actions. Resource-level permissions are not supported for ec2:Describe* actions.

Topics

Full permission to work with ClassicLink
Enable and disable a VPC for ClassicLink
Link instances
Unlink instances
Full permission to work with ClassicLink

The following policy grants users permission to view ClassicLink-enabled VPCs and linked EC2-Classic instances, to enable and disable a VPC for ClassicLink, and to link and unlink instances from a ClassicLink-enabled VPC.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeClassicLinkInstances", "ec2:DescribeVpcClassicLink",
        "ec2:EnableVpcClassicLink", "ec2:DisableVpcClassicLink",
        "ec2:AttachClassicLinkVpc", "ec2:DetachClassicLinkVpc"
      ],
      "Resource": "*"
    }
   ]
}
Enable and disable a VPC for ClassicLink

The following policy allows user to enable and disable VPCs for ClassicLink that have the specific tag 'purpose=classiclink'. Users cannot enable or disable any other VPCs for ClassicLink.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*VpcClassicLink",
      "Resource": "arn:aws:ec2:region:account:vpc/*",
      "Condition": {
        "StringEquals": {
          "ec2:ResourceTag/purpose":"classiclink"
        }
      }
    }
  ]
}
Link instances

The following policy grants users permission to link instances to a VPC only if the instance is an m3.large instance type. The second statement allows users to use the VPC and security group resources, which are required to link an instance to a VPC.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:AttachClassicLinkVpc",
      "Resource": "arn:aws:ec2:region:account:instance/*",
      "Condition": {
        "StringEquals": {
          "ec2:InstanceType":"m3.large"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": "ec2:AttachClassicLinkVpc",
      "Resource": [
        "arn:aws:ec2:region:account:vpc/*",
        "arn:aws:ec2:region:account:security-group/*"
      ]
    }
  ]
}				
The following policy grants users permission to link instances to a specific VPC (vpc-1a2b3c4d) only, and to associate only specific security groups from the VPC to the instance (sg-1122aabb and sg-aabb2233). Users cannot link an instance to any other VPC, and they cannot specify any other of the VPC security groups to associate with the instance in the request.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:AttachClassicLinkVpc",
      "Resource": [
         "arn:aws:ec2:region:account:vpc/vpc-1a2b3c4d",
         "arn:aws:ec2:region:account:instance/*",
         "arn:aws:ec2:region:account:security-group/sg-1122aabb",
         "arn:aws:ec2:region:account:security-group/sg-aabb2233"
       ]
    }
  ]
}				
Unlink instances

The following grants users permission to unlink any linked EC2-Classic instance from a VPC, but only if the instance has the tag "unlink=true". The second statement grants users permission to use the VPC resource, which is required to unlink an instance from a VPC.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": "ec2:DetachClassicLinkVpc",
      "Resource": [
         "arn:aws:ec2:region:account:instance/*"
      ],
      "Condition": {
         "StringEquals": {
            "ec2:ResourceTag/unlink":"true"
         }
      }
   },
   {
      "Effect": "Allow",
      "Action": "ec2:DetachClassicLinkVpc",
      "Resource": [
         "arn:aws:ec2:region:account:vpc/*"
         ]
      }
   ]
}
7. Working with Reserved Instances

The following policy gives users permission to view, modify, and purchase Reserved Instances in your account.

It is not possible to set resource-level permissions for individual Reserved Instances. This policy means that users have access to all the Reserved Instances in the account.

The Resource element uses a * wildcard to indicate that users can specify all resources with the action; in this case, they can list and modify all Reserved Instances in the account. They can also purchase Reserved Instances using the account credentials. The * wildcard is also necessary in cases where the API action does not support resource-level permissions.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeReservedInstances", "ec2:ModifyReservedInstances",
        "ec2:PurchaseReservedInstancesOffering", "ec2:DescribeAvailabilityZones",
        "ec2:DescribeReservedInstancesOfferings"
      ],
      "Resource": "*"
    }
   ]
}
To allow users to view and modify the Reserved Instances in your account, but not purchase new Reserved Instances.

Copy
{
  ""Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeReservedInstances", "ec2:ModifyReservedInstances",
        "ec2:DescribeAvailabilityZones"
      ],
      "Resource": "*"
    }
  ]
}
8. Tagging Resources

The following policy allows users to use the CreateTags action to apply tags to an instance only if the tag contains the key environment and the value production. The ForAllValues modifier is used with the aws:TagKeys condition key to indicate that only the key environment is allowed in the request (no other tags are allowed). The user cannot tag any other resource types.

Copy

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:CreateTags"
            ],
            "Resource": "arn:aws:ec2:region:account:instance/*",
            "Condition": {
                "StringEquals": {
                    "ec2:RequestTag/environment": "production"
                },
                "ForAllValues:StringEquals": {
                    "aws:TagKeys": [
                        "environment"
                    ]
                }
            }
        }
    ]
}
The following policy allows users to tag any taggable resource that already has a tag with a key of owner and a value of the IAM username. In addition, users must specify a tag with a key of environment and a value of either test or prod in the request. Users can specify additional tags in the request.

Copy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:CreateTags"
            ],
            "Resource": "arn:aws:ec2:region:account:*/*",
            "Condition": {
                "StringEquals": {
                    "aws:RequestTag/environment": ["test","prod"],
                    "ec2:ResourceTag/owner": "${aws:username}"
                }
            }
        }
    ]
}
You can create an IAM policy that allows users to delete specific tags for a resource. For example, the following policy allows users to delete tags for a volume if the tag keys specified in the request are environment or cost-center. Any value can be specified for the tag but the tag key must match either of the specified keys.

Note
If you delete a resource, all tags associated with the resource are also deleted. Users do not need permission to use the ec2:DeleteTags action to delete a resource that has tags; they only need permission to perform the deleting action.
Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:DeleteTags",
      "Resource": "arn:aws:ec2:us-east-1:123456789012:volume/*",
      "Condition": {
        "ForAllValues:StringEquals": {
          "aws:TagKeys": ["environment","cost-center"]
        }
      }
    }
  ]
}
This policy allows users to delete only the environment=prod tag on any resource, and only if the resource is already tagged with a key of owner and a value of the IAM username. Users cannot delete any other tags for a resource.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DeleteTags"
      ],
      "Resource": "arn:aws:ec2:region:account:*/*",
      "Condition": {
        "StringEquals": {
          "aws:RequestTag/environment": "prod",
          "ec2:ResourceTag/owner": "${aws:username}"
        },
        "ForAllValues:StringEquals": {
          "aws:TagKeys": ["environment"]
        }
      }
    }
  ]
}
9: Working with IAM Roles

The following policy allows users to attach, replace, and detach an IAM role to instances that have the tag department=test. Replacing or detaching an IAM role requires an association ID, therefore the policy also grants users permission to use the ec2:DescribeIamInstanceProfileAssociations action.

IAM users must have permission to use the iam:PassRole action in order to pass the role to the instance.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:AssociateIamInstanceProfile",
         "ec2:ReplaceIamInstanceProfileAssociation",
         "ec2:DisassociateIamInstanceProfile"
      ],
      "Resource": "arn:aws:ec2:region:account:instance/*",
      "Condition": {
        "StringEquals": {
          "ec2:ResourceTag/department":"test"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": "ec2:DescribeIamInstanceProfileAssociations",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "*"
    }
  ]
}
The following policy allows users to attach or replace an IAM role for any instance. Users can only attach or replace IAM roles with names that begin with TestRole-. For the iam:PassRole action, ensure that you specify the name of the IAM role and not the instance profile (if the names are different). For more information, see Instance Profiles.

Copy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:AssociateIamInstanceProfile",
                "ec2:ReplaceIamInstanceProfileAssociation"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "ec2:DescribeIamInstanceProfileAssociations",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "arn:aws:iam::account:role/TestRole-*"
        }
    ]
}

Example Policies for Working in the Amazon EC2 Console

You can use IAM policies to grant users permissions to view and work with specific resources in the Amazon EC2 console. You can use the example policies in the previous section; however, they are designed for requests that are made with the AWS CLI or an AWS SDK. The console uses additional API actions for its features, so these policies may not work as expected. For example, a user that has permission to use only the DescribeVolumes API action will encounter errors when trying to view volumes in the console. This section demonstrates policies that enable users to work with specific parts of the console.

Topics

1: Read-Only Access
2: Using the EC2 Launch Wizard
3: Working with Volumes
4: Working with Security Groups
5: Working with Elastic IP Addresses
6: Working with Reserved Instances
Note
To help you work out which API actions are required to perform tasks in the console, you can use a service such as AWS CloudTrail. For more information, see the AWS CloudTrail User Guide. If your policy does not grant permission to create or modify a specific resource, the console displays an encoded message with diagnostic information. You can decode the message using the DecodeAuthorizationMessage API action for AWS STS, or the decode-authorization-message command in the AWS CLI.
For additional information about creating policies for the Amazon EC2 console, see the following AWS Security Blog post: Granting Users Permission to Work in the Amazon EC2 Console.

1: Read-Only Access

To allow users to view all resources in the Amazon EC2 console, you can use the same policy as the following example: 1: Read-Only Access. Users cannot perform any actions on those resources or create new resources, unless another statement grants them permission to do so.

a. View instances, AMIs, and snapshots

Alternatively, you can provide read-only access to a subset of resources. To do this, replace the * wildcard in the ec2:Describe API action with specific ec2:Describe actions for each resource. The following policy allows users to view all instances, AMIs, and snapshots in the Amazon EC2 console. The ec2:DescribeTags action allows users to view public AMIs. The console requires the tagging information to display public AMIs; however, you can remove this action to allow users to view only private AMIs.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
         "ec2:DescribeInstances", "ec2:DescribeImages",
         "ec2:DescribeTags", "ec2:DescribeSnapshots"
      ],
      "Resource": "*"
   }
   ]
}
Note
Currently, the Amazon EC2 ec2:Describe* API actions do not support resource-level permissions, so you cannot control which individual resources users can view in the console. Therefore, the * wildcard is necessary in the Resource element of the above statement. For more information about which ARNs you can use with which Amazon EC2 API actions, see Supported Resource-Level Permissions for Amazon EC2 API Actions.
b. View instances and CloudWatch metrics

The following policy allows users to view instances in the Amazon EC2 console, as well as CloudWatch alarms and metrics in the Monitoring tab of the Instances page. The Amazon EC2 console uses the CloudWatch API to display the alarms and metrics, so you must grant users permission to use the cloudwatch:DescribeAlarms and cloudwatch:GetMetricStatistics actions.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
         "ec2:DescribeInstances",
         "cloudwatch:DescribeAlarms",
         "cloudwatch:GetMetricStatistics"
      ],
      "Resource": "*"
   }
   ]
}
2: Using the EC2 Launch Wizard

The Amazon EC2 launch wizard is a series of screens with options to configure and launch an instance. Your policy must include permission to use the API actions that allow users to work with the wizard's options. If your policy does not include permission to use those actions, some items in the wizard cannot load properly, and users cannot complete a launch.

a. Basic launch wizard access

To complete a launch successfully, users must be given permission to use the ec2:RunInstances API action, and at least the following API actions:

ec2:DescribeImages: To view and select an AMI.
ec2:DescribeVPCs: To view the available network options, which are EC2-Classic and a list of VPCs. This is required even if you are not launching into a VPC.
ec2:DescribeSubnets: If launching into a VPC, to view all available subnets for the chosen VPC.
ec2:DescribeSecurityGroups: To view the security groups page in the wizard. Users can select an existing security group.
ec2:DescribeKeyPairs or ec2:CreateKeyPair: To select an existing key pair, or create a new one.
Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
		"ec2:DescribeInstances", "ec2:DescribeImages",
        "ec2:DescribeKeyPairs","ec2:DescribeVpcs", "ec2:DescribeSubnets", 
        "ec2:DescribeSecurityGroups"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": "*"
    }
   ]
}
You can add API actions to your policy to provide more options for users, for example:

ec2:DescribeAvailabilityZones: If launching into EC2-Classic, to view and select a specific Availability Zone.
ec2:DescribeNetworkInterfaces: If launching into a VPC, to view and select existing network interfaces for the selected subnet.
ec2:CreateSecurityGroup: To create a new security group; for example, to create the wizard's suggested launch-wizard-x security group. However, this action alone only creates the security group; it does not add or modify any rules. To add inbound rules, users must be granted permission to use the ec2:AuthorizeSecurityGroupIngress API action. To add outbound rules to VPC security groups, users must be granted permission to use the ec2:AuthorizeSecurityGroupEgress API action. To modify or delete existing rules, users must be granted permission to use the relevant ec2:RevokeSecurityGroup* API action.
ec2:CreateTags: To tag the resources that are created by RunInstances. For more information, see Resource-Level Permissions for Tagging. If users do not have permission to use this action and they attempt to apply tags on the tagging page of the launch wizard, the launch fails.
Important
Be careful about granting users permission to use the ec2:CreateTags action. This limits your ability to use the ec2:ResourceTag condition key to restrict the use of other resources; users can change a resource's tag in order to bypass those restrictions.
Currently, the Amazon EC2 Describe* API actions do not support resource-level permissions, so you cannot restrict which individual resources users can view in the launch wizard. However, you can apply resource-level permissions on the ec2:RunInstances API action to restrict which resources users can use to launch an instance. The launch fails if users select options that they are not authorized to use.

b. Restrict access to specific instance type, subnet, and region

The following policy allows users to launch m1.small instances using AMIs owned by Amazon, and only into a specific subnet (subnet-1a2b3c4d). Users can only launch in the sa-east-1 region. If users select a different region, or select a different instance type, AMI, or subnet in the launch wizard, the launch fails.

The first statement grants users permission to view the options in the launch wizard, as demonstrated in the example above. The second statement grants users permission to use the network interface, volume, key pair, security group, and subnet resources for the ec2:RunInstances action, which are required to launch an instance into a VPC. For more information about using the ec2:RunInstances action, see 5: Launching Instances (RunInstances). The third and fourth statements grant users permission to use the instance and AMI resources respectively, but only if the instance is an m1.small instance, and only if the AMI is owned by Amazon.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
         "ec2:DescribeInstances", "ec2:DescribeImages",
         "ec2:DescribeKeyPairs","ec2:DescribeVpcs", "ec2:DescribeSubnets", "ec2:DescribeSecurityGroups"
	  ],
	  "Resource": "*"
   },
   {
      "Effect": "Allow",
      "Action":"ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:sa-east-1:111122223333:network-interface/*",
         "arn:aws:ec2:sa-east-1:111122223333:volume/*",
         "arn:aws:ec2:sa-east-1:111122223333:key-pair/*",
         "arn:aws:ec2:sa-east-1:111122223333:security-group/*",
         "arn:aws:ec2:sa-east-1:111122223333:subnet/subnet-1a2b3c4d"
      ]
   },
   {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
         "arn:aws:ec2:sa-east-1:111122223333:instance/*"
      ],
      "Condition": {
         "StringEquals": {
            "ec2:InstanceType": "m1.small"
         }
      }
   },
   {
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [ 
            "arn:aws:ec2:sa-east-1::image/ami-*"
      ],
      "Condition": {
         "StringEquals": {
            "ec2:Owner": "amazon"
         }
      }
   }
   ]
}
3: Working with Volumes

The following policy grants users permission to view and create volumes, and attach and detach volumes to specific instances.

Users can attach any volume to instances that have the tag "purpose=test", and also detach volumes from those instances. To attach a volume using the Amazon EC2 console, it is helpful for users to have permission to use the ec2:DescribeInstances action, as this allows them to select an instance from a pre-populated list in the Attach Volume dialog box. However, this also allows users to view all instances on the Instances page in the console, so you can omit this action.

In the first statement, the ec2:DescribeVolumeStatus and ec2:DescribeAvailabilityZones actions are necessary to ensure that volumes display correctly in the console.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeVolumes", "ec2:DescribeVolumeStatus", 
        "ec2:DescribeAvailabilityZones", "ec2:CreateVolume", 
        "ec2:DescribeInstances"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:AttachVolume",
        "ec2:DetachVolume"
      ],
      "Resource": "arn:aws:ec2:region:111122223333:instance/*",
      "Condition": {
        "StringEquals": {
          "ec2:ResourceTag/purpose": "test"
        }
     }
   },
   {
      "Effect": "Allow",
      "Action": [
        "ec2:AttachVolume",
        "ec2:DetachVolume"
      ],
      "Resource": "arn:aws:ec2:region:111122223333:volume/*"
   }    
   ]
}
4: Working with Security Groups

a. View security groups and add and remove rules

The following policy grants users permission to view security groups in the Amazon EC2 console, and to add and remove inbound and outbound rules for existing security groups that have the tag Department=Test.

Note
You can't modify outbound rules for EC2-Classic security groups. For more information about security groups, see Amazon EC2 Security Groups for Linux Instances.
In the first statement, the ec2:DescribeTags action allows users to view tags in the console, which makes it easier for users to identify the security groups that they are allowed to modify.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
         "ec2:DescribeSecurityGroups", "ec2:DescribeTags"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
         "ec2:AuthorizeSecurityGroupIngress", "ec2:RevokeSecurityGroupIngress",
         "ec2:AuthorizeSecurityGroupEgress", "ec2:RevokeSecurityGroupEgress"
      ],
      "Resource": [
         "arn:aws:ec2:region:111122223333:security-group/*"
      ],
      "Condition": {
         "StringEquals": {
            "ec2:ResourceTag/Department": "Test"
         }
      }
   }
   ]
}
b. Working with the Create Security Group dialog box

You can create a policy that allows users to work with the Create Security Group dialog box in the Amazon EC2 console. To use this dialog box, users must be granted permission to use at the least the following API actions:

ec2:CreateSecurityGroup: To create a new security group.
ec2:DescribeVpcs: To view a list of existing VPCs in the VPC list. This action is not required for creating security groups in EC2-Classic.
With these permissions, users can create a new security group successfully, but they cannot add any rules to it. To work with rules in the Create Security Group dialog box, you can add the following API actions to your policy:

ec2:AuthorizeSecurityGroupIngress: To add inbound rules.
ec2:AuthorizeSecurityGroupEgress: To add outbound rules to VPC security groups.
ec2:RevokeSecurityGroupIngress: To modify or delete existing inbound rules. This is useful to allow users to use the Copy to new feature in the console. This feature opens the Create Security Group dialog box and populates it with the same rules as the security group that was selected.
ec2:RevokeSecurityGroupEgress: To modify or delete outbound rules for VPC security groups. This is useful to allow users to modify or delete the default outbound rule that allows all outbound traffic.
ec2:DeleteSecurityGroup: To cater for when invalid rules cannot be saved. The console first creates the security group, and then adds the specified rules. If the rules are invalid, the action fails, and the console attempts to delete the security group. The user remains in the Create Security Group dialog box so that they can correct the invalid rule and try to create the security group again. This API action is not required, but if a user is not granted permission to use it and attempts to create a security group with invalid rules, the security group is created without any rules, and the user must add them afterward.
Currently, the ec2:CreateSecurityGroup API action does not support resource-level permissions; however, you can apply resource-level permissions to the ec2:AuthorizeSecurityGroupIngress and ec2:AuthorizeSecurityGroupEgress actions to control how users can create rules.

The following policy grants users permission to use the Create Security Group dialog box, and to create inbound and outbound rules for security groups that are associated with a specific VPC (vpc-1a2b3c4d). Users can create security groups for EC2-Classic or another VPC, but they cannot add any rules to them. Similarly, users cannot add any rules to any existing security group that's not associated with VPC vpc-1a2b3c4d. Users are also granted permission to view all security groups in the console. This makes it easier for users to identify the security groups to which they can add inbound rules. This policy also grants users permission to delete security groups that are associated with VPC vpc-1a2b3c4d.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeSecurityGroups", "ec2:CreateSecurityGroup", "ec2:DescribeVpcs"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DeleteSecurityGroup", "ec2:AuthorizeSecurityGroupIngress", "ec2:AuthorizeSecurityGroupEgress"
      ],
      "Resource": "arn:aws:ec2:region:111122223333:security-group/*",
      "Condition":{
         "ArnEquals": {
            "ec2:Vpc": "arn:aws:ec2:region:111122223333:vpc/vpc-1a2b3c4d"
         }
      }
    }
   ]
}
5: Working with Elastic IP Addresses

To allow users to view Elastic IP addresses in the Amazon EC2 console, you must grant users permission to use the ec2:DescribeAddresses action.

To allow users to work with Elastic IP addresses, you can add the following actions to your policy.

ec2:AllocateAddress: To allocate an address for use in VPC or EC2-Classic.
ec2:ReleaseAddress: To release an Elastic IP address.
ec2:AssociateAddress: To associate an Elastic IP address with an instance or a network interface.
ec2:DescribeNetworkInterfaces and ec2:DescribeInstances: To work with the Associate address screen. The screen displays the available instances or network interfaces to which you can associate an Elastic IP address. For an EC2-Classic instance, users only need permission to use ec2:DescribeInstances.
ec2:DisassociateAddress: To disassociate an Elastic IP address from an instance or a network interface.
The following policy allows users to view, allocate, and associate Elastic IP addresses with instances. Users cannot associate Elastic IP addresses with network interfaces, disassociate Elastic IP addresses, or release them.

Copy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeAddresses",
                "ec2:AllocateAddress",
                "ec2:DescribeInstances",
                "ec2:AssociateAddress"
            ],
            "Resource": "*"
        }
    ]
}
6: Working with Reserved Instances

The following policy can be attached to an IAM user. It gives the user access to view and modify Reserved Instances in your account, as well as purchase new Reserved Instances in the AWS Management Console.

This policy allows users to view all the Reserved Instances, as well as On-Demand Instances, in the account. It's not possible to set resource-level permissions for individual Reserved Instances.

Copy
{
   "Version": "2012-10-17",
   "Statement": [{
      "Effect": "Allow",
      "Action": [
         "ec2:DescribeReservedInstances", "ec2:ModifyReservedInstances",
         "ec2:PurchaseReservedInstancesOffering", "ec2:DescribeInstances",
         "ec2:DescribeAvailabilityZones", "ec2:DescribeReservedInstancesOfferings"
      ],
      "Resource": "*"
   }
   ]
}
The ec2:DescribeAvailabilityZones action is necessary to ensure that the Amazon EC2 console can display information about the Availability Zones in which you can purchase Reserved Instances. The ec2:DescribeInstances action is not required, but ensures that the user can view the instances in the account and purchase reservations to match the correct specifications.

You can adjust the API actions to limit user access, for example removing ec2:DescribeInstances and ec2:DescribeAvailabilityZones means the user has read-only access.

IAM Roles for Amazon EC2

Applications must sign their API requests with AWS credentials. Therefore, if you are an application developer, you need a strategy for managing credentials for your applications that run on EC2 instances. For example, you can securely distribute your AWS credentials to the instances, enabling the applications on those instances to use your credentials to sign requests, while protecting your credentials from other users. However, it's challenging to securely distribute credentials to each instance, especially those that AWS creates on your behalf, such as Spot Instances or instances in Auto Scaling groups. You must also be able to update the credentials on each instance when you rotate your AWS credentials.

We designed IAM roles so that your applications can securely make API requests from your instances, without requiring you to manage the security credentials that the applications use. Instead of creating and distributing your AWS credentials, you can delegate permission to make API requests using IAM roles as follows:

Create an IAM role.

Define which accounts or AWS services can assume the role.

Define which API actions and resources the application can use after assuming the role.

Specify the role when you launch your instance, or attach the role to a running or stopped instance.

Have the application retrieve a set of temporary credentials and use them.

For example, you can use IAM roles to grant permissions to applications running on your instances that needs to use a bucket in Amazon S3. You can specify permissions for IAM roles by creating a policy in JSON format. These are similar to the policies that you create for IAM users. If you make a change to a role, the change is propagated to all instances.

You cannot attach multiple IAM roles to a single instance, but you can attach a single IAM role to multiple instances. For more information about creating and using IAM roles, see Roles in the IAM User Guide.

You can apply resource-level permissions to your IAM policies to control users' ability to attach, replace, or detach IAM roles for an instance. For more information, see Supported Resource-Level Permissions for Amazon EC2 API Actions and the following example: 9: Working with IAM Roles.

Topics

Instance Profiles
Retrieving Security Credentials from Instance Metadata
Granting an IAM User Permission to Pass an IAM Role to an Instance
Working with IAM Roles
Instance Profiles

Amazon EC2 uses an instance profile as a container for an IAM role. When you create an IAM role using the IAM console, the console creates an instance profile automatically and gives it the same name as the role to which it corresponds. If you use the Amazon EC2 console to launch an instance with an IAM role or to attach an IAM role to an instance, you choose the instance based on a list of instance profile names.

If you use the AWS CLI, API, or an AWS SDK to create a role, you create the role and instance profile as separate actions, with potentially different names. If you then use the AWS CLI, API, or an AWS SDK to launch an instance with an IAM role or to attach an IAM role to an instance, specify the instance profile name.

An instance profile can contain only one IAM role. This limit cannot be increased.

For more information, see Instance Profiles in the IAM User Guide.

Retrieving Security Credentials from Instance Metadata

An application on the instance retrieves the security credentials provided by the role from the instance metadata item iam/security-credentials/role-name. The application is granted the permissions for the actions and resources that you've defined for the role through the security credentials associated with the role. These security credentials are temporary and we rotate them automatically. We make new credentials available at least five minutes prior to the expiration of the old credentials.

Warning
If you use services that use instance metadata with IAM roles, ensure that you don't expose your credentials when the services make HTTP calls on your behalf. The types of services that could expose your credentials include HTTP proxies, HTML/CSS validator services, and XML processors that support XML inclusion.
The following command retrieves the security credentials for an IAM role named s3access.

Copy
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/s3access
The following is example output.

{
  "Code" : "Success",
  "LastUpdated" : "2012-04-26T16:39:16Z",
  "Type" : "AWS-HMAC",
  "AccessKeyId" : "ASIAIOSFODNN7EXAMPLE",
  "SecretAccessKey" : "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
  "Token" : "token",
  "Expiration" : "2017-05-17T15:09:54Z"
}
For applications, AWS CLI, and Tools for Windows PowerShell commands that run on the instance, you do not have to explicitly get the temporary security credentials — the AWS SDKs, AWS CLI, and Tools for Windows PowerShell automatically get the credentials from the EC2 instance metadata service and use them. To make a call outside of the instance using temporary security credentials (for example, to test IAM policies), you must provide the access key, secret key, and the session token. For more information, see Using Temporary Security Credentials to Request Access to AWS Resources in the IAM User Guide.

For more information about instance metadata, see Instance Metadata and User Data.

Granting an IAM User Permission to Pass an IAM Role to an Instance

To enable an IAM user to launch an instance with an IAM role or to attach or replace an IAM role for an existing instance, you must grant the user permission to pass the role to the instance.

The following IAM policy grants users permission to launch instances (ec2:RunInstances) with an IAM role, or to attach or replace an IAM role for an existing instance (ec2:AssociateIamInstanceProfile and ec2:ReplaceIamInstanceProfileAssociation).

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
         "ec2:RunInstances",
         "ec2:AssociateIamInstanceProfile",
         "ec2:ReplaceIamInstanceProfileAssociation"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "*"
    }
  ]
}
This policy grants IAM users access to all your roles by specifying the resource as "*" in the policy. However, consider whether users who launch instances with your roles (ones that exist or that you'll create later on) might be granted permissions that they don't need or shouldn't have.

Working with IAM Roles

You can create an IAM role and attach it to an instance during or after launch. You can also replace or detach an IAM role for an instance.

Contents

Creating an IAM Role
Launching an Instance with an IAM Role
Attaching an IAM Role to an Instance
Detaching an IAM Role
Replacing an IAM Role
Creating an IAM Role

You must create an IAM role before you can launch an instance with that role or attach it to an instance.

To create an IAM role using the IAM console

Open the IAM console at https://console.aws.amazon.com/iam/.

In the navigation pane, choose Roles, Create new role.

On the Select role type page, choose Select next to Amazon EC2.

On the Attach Policy page, select an AWS managed policy that grants your instances access to the resources that they need.

On the Set role name and review page, type a name for the role and choose Create role.

Alternatively, you can use the AWS CLI to create an IAM role.

To create an IAM role and instance profile using the AWS CLI

Create an IAM role with a policy that allows the role to use an Amazon S3 bucket.

Create the following trust policy and save it in a text file named ec2-role-trust-policy.json.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com"},
      "Action": "sts:AssumeRole"
    }
  ]
}
Create the s3access role and specify the trust policy that you created.

Copy
aws iam create-role --role-name s3access --assume-role-policy-document file://ec2-role-trust-policy.json
{
    "Role": {
        "AssumeRolePolicyDocument": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Action": "sts:AssumeRole",
                    "Effect": "Allow",
                    "Principal": {
                        "Service": "ec2.amazonaws.com"
                    }
                }
            ]
        },
        "RoleId": "AROAIIZKPBKS2LEXAMPLE",
        "CreateDate": "2013-12-12T23:46:37.247Z",
        "RoleName": "s3access",
        "Path": "/",
        "Arn": "arn:aws:iam::123456789012:role/s3access"
    }
}
Create an access policy and save it in a text file named ec2-role-access-policy.json. For example, this policy grants administrative permissions for Amazon S3 to applications running on the instance.

Copy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:*"],
      "Resource": ["*"]
    }
  ]
}
Attach the access policy to the role.

Copy
aws iam put-role-policy --role-name s3access --policy-name S3-Permissions --policy-document file://ec2-role-access-policy.json
Create an instance profile named s3access-profile.

Copy
aws iam create-instance-profile --instance-profile-name s3access-profile
{
    "InstanceProfile": {
        "InstanceProfileId": "AIPAJTLBPJLEGREXAMPLE",
        "Roles": [],
        "CreateDate": "2013-12-12T23:53:34.093Z",
        "InstanceProfileName": "s3access-profile",
        "Path": "/",
        "Arn": "arn:aws:iam::123456789012:instance-profile/s3access-profile"
    }
}
Add the s3access role to the s3access-profile instance profile.

Copy
aws iam add-role-to-instance-profile --instance-profile-name s3access-profile --role-name s3access
For more information about these commands, see create-role, put-role-policy, and create-instance-profile in the AWS Command Line Interface Reference.

Alternatively, you can use the following AWS Tools for Windows PowerShell commands:

New-IAMRole
Register-IAMRolePolicy
New-IAMInstanceProfile
Launching an Instance with an IAM Role

After you've created an IAM role, you can launch an instance, and associate that role with the instance during launch.

Important
After you create an IAM role, it may take several seconds for the permissions to propagate. If your first attempt to launch an instance with a role fails, wait a few seconds before trying again. For more information, see Troubleshooting Working with Roles in the IAM User Guide.
To launch an instance with an IAM role using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the dashboard, choose Launch Instance.

Select an AMI and instance type and then choose Next: Configure Instance Details.

On the Configure Instance Details page, for IAM role, select the IAM role that you created.

Note
The IAM role list displays the name of the instance profile that you created when you created your IAM role. If you created your IAM role using the console, the instance profile was created for you and given the same name as the role. If you created your IAM role using the AWS CLI, API, or an AWS SDK, you may have named your instance profile differently.
Configure any other details, then follow the instructions through the rest of the wizard, or choose Review and Launch to accept default settings and go directly to the Review Instance Launch page.

Review your settings, then choose Launch to choose a key pair and launch your instance.

If you are using the Amazon EC2 API actions in your application, retrieve the AWS security credentials made available on the instance and use them to sign the requests. Note that the AWS SDK does this for you.

Copy
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/role_name
Alternatively, you can use the AWS CLI to associate a role with an instance during launch. You must specify the instance profile in the command.

To launch an instance with an IAM role using the AWS CLI

Use the run-instances command to launch an instance using the instance profile. The following example shows how to launch an instance with the instance profile.

Copy
aws ec2 run-instances --image-id ami-11aa22bb --iam-instance-profile Name="s3access-profile" --key-name my-key-pair --security-groups my-security-group --subnet-id subnet-1a2b3c4d
Alternatively, use the New-EC2Instance Tools for Windows PowerShell command.

If you are using the Amazon EC2 API actions in your application, retrieve the AWS security credentials made available on the instance and use them to sign the requests. Note that the AWS SDK does this for you.

Copy
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/role_name
Attaching an IAM Role to an Instance

After you've created an IAM role, you can attach it to a running or stopped instance.

To attach an IAM role to an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance, choose Actions, Instance Settings, Attach/Replace IAM role.

Select the IAM role to attach to your instance, and choose Apply.

To attach an IAM role to an instance using the AWS CLI

If required, describe your instances to get the ID of the instance to which to attach the role.

Copy
aws ec2 describe-instances
Use the associate-iam-instance-profile command to attach the IAM role to the instance by specifying the instance profile. You can use the Amazon Resource Name (ARN) of the instance profile, or you can use its name.

Copy
aws ec2 associate-iam-instance-profile --instance-id i-1234567890abcdef0 --iam-instance-profile Name="TestRole-1"

{
    "IamInstanceProfileAssociation": {
        "InstanceId": "i-1234567890abcdef0", 
        "State": "associating", 
        "AssociationId": "iip-assoc-0dbd8529a48294120", 
        "IamInstanceProfile": {
            "Id": "AIPAJLNLDX3AMYZNWYYAY", 
            "Arn": "arn:aws:iam::123456789012:instance-profile/TestRole-1"
        }
    }
}
Alternatively, use the following Tools for Windows PowerShell commands:

Get-EC2Instance
Register-EC2IamInstanceProfile
Detaching an IAM Role

You can detach an IAM role from a running or stopped instance.

To detach an IAM role from an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance, choose Actions, Instance Settings, Attach/Replace IAM role.

For IAM role, choose No Role. Choose Apply.

In the confirmation dialog box, choose Yes, Detach.

To detach an IAM role from an instance using the AWS CLI

If required, use describe-iam-instance-profile-associations to describe your IAM instance profile associations and get the association ID for the IAM instance profile to detach.

Copy
aws ec2 describe-iam-instance-profile-associations

{
    "IamInstanceProfileAssociations": [
        {
            "InstanceId": "i-088ce778fbfeb4361", 
            "State": "associated", 
            "AssociationId": "iip-assoc-0044d817db6c0a4ba", 
            "IamInstanceProfile": {
                "Id": "AIPAJEDNCAA64SSD265D6", 
                "Arn": "arn:aws:iam::123456789012:instance-profile/TestRole-2"
            }
        }
    ]
}
Use the disassociate-iam-instance-profile command to detach the IAM instance profile using its association ID.

Copy
aws ec2 disassociate-iam-instance-profile --association-id iip-assoc-0044d817db6c0a4ba

{
    "IamInstanceProfileAssociation": {
        "InstanceId": "i-087711ddaf98f9489", 
        "State": "disassociating", 
        "AssociationId": "iip-assoc-0044d817db6c0a4ba", 
        "IamInstanceProfile": {
            "Id": "AIPAJEDNCAA64SSD265D6", 
            "Arn": "arn:aws:iam::123456789012:instance-profile/TestRole-2"
        }
    }
}
Alternatively, use the following Tools for Windows PowerShell commands:

Get-EC2IamInstanceProfileAssociation
Unregister-EC2IamInstanceProfile
Replacing an IAM Role

You can replace an IAM role for a running instance. You can do this if you want to change the IAM role for an instance without detaching the existing one first; for example, to ensure that API actions performed by applications running on the instance are not interrupted.

Te replace an IAM role for an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance, choose Actions, Instance Settings, Attach/Replace IAM role.

Select the IAM role to attach to your instance, and choose Apply.

To replace an IAM role for an instance using the AWS CLI

If required, describe your IAM instance profile associations to get the association ID for the IAM instance profile to replace.

Copy
aws ec2 describe-iam-instance-profile-associations
Use the replace-iam-instance-profile-association command to replace the IAM instance profile by specifying the association ID for the existing instance profile and the ARN or name of the instance profile that should replace it.

Copy
aws ec2 replace-iam-instance-profile-association --association-id iip-assoc-0044d817db6c0a4ba --iam-instance-profile Name="TestRole-2"

{
    "IamInstanceProfileAssociation": {
        "InstanceId": "i-087711ddaf98f9489", 
        "State": "associating", 
        "AssociationId": "iip-assoc-09654be48e33b91e0", 
        "IamInstanceProfile": {
            "Id": "AIPAJCJEDKX7QYHWYK7GS", 
            "Arn": "arn:aws:iam::123456789012:instance-profile/TestRole-2"
        }
    }
}
Alternatively, use the following Tools for Windows PowerShell commands:

Get-EC2IamInstanceProfileAssociation
Set-EC2IamInstanceProfileAssociation

Authorizing Inbound Traffic for Your Linux Instances

Security groups enable you to control traffic to your instance, including the kind of traffic that can reach your instance. For example, you can allow computers from only your home network to access your instance using SSH. If your instance is a web server, you can allow all IP addresses to access your instance via HTTP, so that external users can browse the content on your web server.

To enable network access to your instance, you must allow inbound traffic to your instance. To open a port for inbound traffic, add a rule to a security group that you associated with your instance when you launched it.

To connect to your instance, you must set up a rule to authorize SSH traffic from your computer's public IPv4 address. To allow SSH traffic from additional IP address ranges, add another rule for each range you need to authorize.

If you've enabled your VPC for IPv6 and launched your instance with an IPv6 address, you can connect to your instance using its IPv6 address instead of a public IPv4 address. Your local computer must have an IPv6 address and must be configured to use IPv6.

If you need to enable network access to a Windows instance, see Authorizing Inbound Traffic for Your Windows Instances in the Amazon EC2 User Guide for Windows Instances.

Before You Start

Decide who requires access to your instance; for example, a single host or a specific network that you trust such as your local computer's public IPv4 address. The security group editor in the Amazon EC2 console can automatically detect the public IPv4 address of your local computer for you. Alternatively, you can use the search phrase "what is my IP address" in an Internet browser, or use the following service: Check IP. If you are connecting through an ISP or from behind your firewall without a static IP address, you need to find out the range of IP addresses used by client computers.

Warning
If you use 0.0.0.0/0, you enable all IPv4 addresses to access your instance using SSH. If you use ::/0, you enable all IPv6 address to access your instance. This is acceptable for a short time in a test environment, but it's unsafe for production environments. In production, you'll authorize only a specific IP address or range of addresses to access your instance.
For more information about security groups, see Amazon EC2 Security Groups for Linux Instances.

Adding a Rule for Inbound SSH Traffic to a Linux Instance

Security groups act as a firewall for associated instances, controlling both inbound and outbound traffic at the instance level. You must add rules to a security group that enable you to connect to your Linux instance from your IP address using SSH.

To add a rule to a security group for inbound SSH traffic over IPv4 using the console

In the navigation pane of the Amazon EC2 console, choose Instances. Select your instance and look at the Description tab; Security groups lists the security groups that are associated with the instance. Choose view rules to display a list of the rules that are in effect for the instance.

In the navigation pane, choose Security Groups. Select one of the security groups associated with your instance.

In the details pane, on the Inbound tab, choose Edit. In the dialog, choose Add Rule, and then choose SSH from the Type list.

In the Source field, choose My IP to automatically populate the field with the public IPv4 address of your local computer. Alternatively, choose Custom and specify the public IPv4 address of your computer or network in CIDR notation. For example, if your IPv4 address is 203.0.113.25, specify 203.0.113.25/32 to list this single IPv4 address in CIDR notation. If your company allocates addresses from a range, specify the entire range, such as 203.0.113.0/24.

For information about finding your IP address, see Before You Start.

Choose Save.

(VPC only) If you launched an instance with an IPv6 address and want to connect to your instance using its IPv6 address, you must add rules that allow inbound IPv6 traffic over SSH.

To add a rule to a security group for inbound SSH traffic over IPv6 using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups. Select the security group for your instance.

Choose Inbound, Edit, Add Rule.

For Type, choose SSH.

In the Source field, specify the IPv6 address of your computer in CIDR notation. For example, if your IPv6 address is 2001:db8:1234:1a00:9691:9503:25ad:1761, specify 2001:db8:1234:1a00:9691:9503:25ad:1761/128 to list the single IP address in CIDR notation. If your company allocates addresses from a range, specify the entire range, such as 2001:db8:1234:1a00::/64.

Choose Save.

To add a rule to a security group using the command line

You can use one of the following commands. Be sure to run this command on your local system, not on the instance itself. For more information about these command line interfaces, see Accessing Amazon EC2.

authorize-security-group-ingress (AWS CLI)
Grant-EC2SecurityGroupIngress (AWS Tools for Windows PowerShell)
Assigning a Security Group to an Instance

You can assign a security group to an instance when you launch the instance. When you add or remove rules, those changes are automatically applied to all instances to which you've assigned the security group.

After you launch an instance in EC2-Classic, you can't change its security groups. After you launch an instance in a VPC, you can change its security groups. For more information, see Changing an Instance's Security Groups in the Amazon VPC User Guide.

Amazon EC2 and Amazon Virtual Private Cloud

Amazon Virtual Private Cloud (Amazon VPC) enables you to define a virtual network in your own logically isolated area within the AWS cloud, known as a virtual private cloud (VPC). You can launch your AWS resources, such as instances, into your VPC. Your VPC closely resembles a traditional network that you might operate in your own data center, with the benefits of using AWS's scalable infrastructure. You can configure your VPC; you can select its IP address range, create subnets, and configure route tables, network gateways, and security settings. You can connect instances in your VPC to the internet. You can connect your VPC to your own corporate data center, making the AWS cloud an extension of your data center. To protect the resources in each subnet, you can use multiple layers of security, including security groups and network access control lists. For more information, see the Amazon VPC User Guide.

Your account may support both the EC2-VPC and EC2-Classic platforms, on a region-by-region basis. If you created your account after 2013-12-04, it supports EC2-VPC only. To find out which platforms your account supports, see Supported Platforms. If your accounts supports EC2-VPC only, we create a default VPC for you. A default VPC is a VPC that is already configured and ready for you to use. You can launch instances into your default VPC immediately. For more information, see Your Default VPC and Subnets in the Amazon VPC User Guide. If your account supports EC2-Classic and EC2-VPC, you can launch instances into either platform. Regardless of which platforms your account supports, you can create your own nondefault VPC, and configure it as you need.

Contents

Benefits of Using a VPC
Differences Between EC2-Classic and EC2-VPC
Sharing and Accessing Resources Between EC2-Classic and EC2-VPC
Instance Types Available Only in a VPC
Amazon VPC Documentation
Supported Platforms
ClassicLink
Migrating from a Linux Instance in EC2-Classic to a Linux Instance in a VPC
Benefits of Using a VPC

By launching your instances into a VPC instead of EC2-Classic, you gain the ability to:

Assign static private IPv4 addresses to your instances that persist across starts and stops
Assign multiple IPv4 addresses to your instances
Define network interfaces, and attach one or more network interfaces to your instances
Change security group membership for your instances while they're running
Control the outbound traffic from your instances (egress filtering) in addition to controlling the inbound traffic to them (ingress filtering)
Add an additional layer of access control to your instances in the form of network access control lists (ACL)
Run your instances on single-tenant hardware
Assign IPv6 addresses to your instances
Differences Between EC2-Classic and EC2-VPC

The following table summarizes the differences between instances launched in EC2-Classic, instances launched in a default VPC, and instances launched in a nondefault VPC.

Characteristic	EC2-Classic	Default VPC	Nondefault VPC
Public IPv4 address (from Amazon's public IP address pool)
Your instance receives a public IPv4 address.
Your instance launched in a default subnet receives a public IPv4 address by default, unless you specify otherwise during launch, or you modify the subnet's public IPv4 address attribute.
Your instance doesn't receive a public IPv4 address by default, unless you specify otherwise during launch, or you modify the subnet's public IPv4 address attribute.
Private IPv4 address
Your instance receives a private IPv4 address from the EC2-Classic range each time it's started.
Your instance receives a static private IPv4 address from the address range of your default VPC.
Your instance receives a static private IPv4 address from the address range of your VPC.
Multiple private IPv4 addresses
We select a single private IP address for your instance; multiple IP addresses are not supported.
You can assign multiple private IPv4 addresses to your instance.
You can assign multiple private IPv4 addresses to your instance.
Elastic IP address (IPv4)
An Elastic IP is disassociated from your instance when you stop it.
An Elastic IP remains associated with your instance when you stop it.
An Elastic IP remains associated with your instance when you stop it.
DNS hostnames
DNS hostnames are enabled by default.
DNS hostnames are enabled by default.
DNS hostnames are disabled by default.
Security group
A security group can reference security groups that belong to other AWS accounts.

You can create up to 500 security groups in each region.
A security group can reference security groups for your VPC only.

You can create up to 100 security groups per VPC.
A security group can reference security groups for your VPC only.

You can create up to 100 security groups per VPC.
Security group association
You can assign an unlimited number of security groups to an instance when you launch it.

You can't change the security groups of your running instance. You can either modify the rules of the assigned security groups, or replace the instance with a new one (create an AMI from the instance, launch a new instance from this AMI with the security groups that you need, disassociate any Elastic IP address from the original instance and associate it with the new instance, and then terminate the original instance).
You can assign up to 5 security groups to an instance.

You can assign security groups to your instance when you launch it and while it's running.
You can assign up to 5 security groups to an instance.

You can assign security groups to your instance when you launch it and while it's running.
Security group rules
You can add rules for inbound traffic only.

You can add up to 100 rules to a security group.
You can add rules for inbound and outbound traffic.

You can add up to 50 rules to a security group.
You can add rules for inbound and outbound traffic.

You can add up to 50 rules to a security group.
Tenancy
Your instance runs on shared hardware.
You can run your instance on shared hardware or single-tenant hardware.
You can run your instance on shared hardware or single-tenant hardware.
Accessing the Internet	Your instance can access the Internet. Your instance automatically receives a public IP address, and can access the Internet directly through the AWS network edge.	By default, your instance can access the Internet. Your instance receives a public IP address by default. An Internet gateway is attached to your default VPC, and your default subnet has a route to the Internet gateway.	By default, your instance cannot access the Internet. Your instance doesn't receive a public IP address by default. Your VPC may have an Internet gateway, depending on how it was created.
IPv6 addressing	IPv6 addressing is not supported. You cannot assign IPv6 addresses to your instances.	You can optionally associate an IPv6 CIDR block with your VPC, and assign IPv6 addresses to instances in your VPC.	You can optionally associate an IPv6 CIDR block with your VPC, and assign IPv6 addresses to instances in your VPC.
The following diagram shows instances in each platform. Note the following:

Instances 1, 2, 3, and 4 are in the EC2-Classic platform. 1 and 2 were launched by one account, and 3 and 4 were launched by a different account. These instances can communicate with each other, can access the Internet directly.
Instances 5 and 6 are in different subnets in the same VPC in the EC2-VPC platform. They were launched by the account that owns the VPC; no other account can launch instances in this VPC. These instances can communicate with each other and can access instances in EC2-Classic and the Internet through the Internet gateway.

					Amazon EC2 supported platforms
				
Sharing and Accessing Resources Between EC2-Classic and EC2-VPC

Some resources and features in your AWS account can be shared or accessed between the EC2-Classic and EC2-VPC platforms, for example, through ClassicLink. For more information about ClassicLink, see ClassicLink.

If your account supports EC2-Classic, you might have set up resources for use in EC2-Classic. If you want to migrate from EC2-Classic to a VPC, you must recreate those resources in your VPC. For more information about migrating from EC2-Classic to a VPC, see Migrating from a Linux Instance in EC2-Classic to a Linux Instance in a VPC.

The following resources can be shared or accessed between EC2-Classic and a VPC.

Resource	Notes
AMI	
Bundle task	
EBS volume	
Elastic IP address (IPv4)	
You can migrate an Elastic IP address from EC2-Classic to EC2-VPC. You can't migrate an Elastic IP address that was originally allocated for use in a VPC to EC2-Classic. For more information, see Migrating an Elastic IP Address from EC2-Classic to EC2-VPC.
Instance	
An EC2-Classic instance can communicate with instances in a VPC using public IPv4 addresses, or you can use ClassicLink to enable communication over private IPv4 addresses.

You can't migrate an instance from EC2-Classic to a VPC. However, you can migrate your application from an instance in EC2-Classic to an instance in a VPC. For more information, see Migrating from a Linux Instance in EC2-Classic to a Linux Instance in a VPC.
Key pair	
Load balancer	
If you're using ClassicLink, you can register a linked EC2-Classic instance with a load balancer in a VPC, provided that the VPC has a subnet in the same Availability Zone as the instance.

You can't migrate a load balancer from EC2-Classic to a VPC. You can't register an instance in a VPC with a load balancer in EC2-Classic.
Placement group	
Reserved Instance	
You can change the network platform for your Reserved Instances from EC2-Classic to EC2-VPC. For more information, see Modifying Standard Reserved Instances.
Security group	
A linked EC2-Classic instance can use a VPC security groups through ClassicLink to control traffic to and from the VPC. VPC instances can't use EC2-Classic security groups.

You can't migrate a security group from EC2-Classic to a VPC. You can copy rules from a security group in EC2-Classic to a security group in a VPC. For more information, see Creating a Security Group.
Snapshot	
The following resources can't be shared or moved between EC2-Classic and a VPC:

Spot instances
Instance Types Available Only in a VPC

Instances of the following instance types are not supported in EC2-Classic and must be launched in a VPC:

C4
F1
G3
I3
M4
P2
R4
T2
X1
If your account supports EC2-Classic but you have not created a nondefault VPC, you can do one of the following to launch a VPC-only instance:

Create a nondefault VPC and launch your VPC-only instance into it by specifying a subnet ID or a network interface ID in the request. Note that you must create a nondefault VPC if you do not have a default VPC and you are using the AWS CLI, Amazon EC2 API, or AWS SDK to launch a VPC-only instance. For more information, see Create a Virtual Private Cloud (VPC).
Launch your VPC-only instance using the Amazon EC2 console. The Amazon EC2 console creates a nondefault VPC in your account and launches the instance into the subnet in the first Availability Zone. The console creates the VPC with the following attributes:
One subnet in each Availability Zone, with the public IPv4 addressing attribute set to true so that instances receive a public IPv4 address. For more information, see IP Addressing in Your VPC in the Amazon VPC User Guide.
An Internet gateway, and a main route table that routes traffic in the VPC to the Internet gateway. This enables the instances you launch in the VPC to communicate over the Internet. For more information, see Internet Gateways in the Amazon VPC User Guide.
A default security group for the VPC and a default network ACL that is associated with each subnet. For more information, see Security in Your VPC in the Amazon VPC User Guide.
If you have other resources in EC2-Classic, you can take steps to migrate them to EC2-VPC. For more information, see Migrating from a Linux Instance in EC2-Classic to a Linux Instance in a VPC.

Amazon VPC Documentation

For more information about Amazon VPC, see the following documentation.

Guide	Description
Amazon VPC Getting Started Guide
Provides a hands-on introduction to Amazon VPC.
Amazon VPC User Guide
Provides detailed information about how to use Amazon VPC.
Amazon VPC Network Administrator Guide
Helps network administrators configure your customer gateway.

Supported Platforms

Amazon EC2 supports the following platforms. Your AWS account is capable of launching instances either into both platforms or only into EC2-VPC, on a region by region basis.

Platform	Introduced In	Description
EC2-Classic
The original release of Amazon EC2
Your instances run in a single, flat network that you share with other customers.
EC2-VPC
The original release of Amazon VPC
Your instances run in a virtual private cloud (VPC) that's logically isolated to your AWS account.
For more information about the availability of either platform in your account, see Availability in the Amazon VPC User Guide. For more information about the differences between EC2-Classic and EC2-VPC, see Differences Between EC2-Classic and EC2-VPC.

Supported Platforms in the Amazon EC2 Console

The Amazon EC2 console indicates which platforms you can launch instances into for the selected region, and whether you have a default VPC in that region.

Verify that the region you'll use is selected in the navigation bar. On the Amazon EC2 console dashboard, look for Supported Platforms under Account Attributes. If there are two values, EC2 and VPC, you can launch instances into either platform. If there is one value, VPC, you can launch instances only into EC2-VPC.

If you can launch instances only into EC2-VPC, we create a default VPC for you. Then, when you launch an instance, we launch it into your default VPC, unless you create a nondefault VPC and specify it when you launch the instance.

EC2-VPC

The dashboard displays the following under Account Attributes to indicate that the account supports only the EC2-VPC platform, and has a default VPC with the identifier vpc-1a2b3c4d.


						  	The Supported Platforms indicator
  						
If your account supports only EC2-VPC, you can select a VPC from the Network list, and a subnet from the Subnet list when you launch an instance using the launch wizard.


								Instance details: default VPC
							
EC2-Classic, EC2-VPC

The dashboard displays the following under Account Attributes to indicate that the account supports both the EC2-Classic and EC2-VPC platforms.


						  	The Supported Platforms indicator
  						
If your account supports EC2-Classic and EC2-VPC, you can launch into EC2-Classic using the launch wizard by selecting Launch into EC2-Classic from the Network list. To launch into a VPC, you can select a VPC from the Network list, and a subnet from the Subnet list.

Related Topic

For more information about how you can tell which platforms you can launch instances into, see Detecting Your Supported Platforms in the Amazon VPC User Guide.

ClassicLink

ClassicLink allows you to link your EC2-Classic instance to a VPC in your account, within the same region. This allows you to associate the VPC security groups with the EC2-Classic instance, enabling communication between your EC2-Classic instance and instances in your VPC using private IPv4 addresses. ClassicLink removes the need to make use of public IPv4 addresses or Elastic IP addresses to enable communication between instances in these platforms. For more information about private and public IPv4 addresses, see IP Addressing in Your VPC.

ClassicLink is available to all users with accounts that support the EC2-Classic platform, and can be used with any EC2-Classic instance. To find out which platform your account supports, see Supported Platforms. For more information about the benefits of using a VPC, see Amazon EC2 and Amazon Virtual Private Cloud. For more information about migrating your resources to a VPC, see Migrating from a Linux Instance in EC2-Classic to a Linux Instance in a VPC.

There is no additional charge for using ClassicLink. Standard charges for data transfer and instance hour usage apply.

Note
EC2-Classic instances cannot be enabled for IPv6 communication. You can associate an IPv6 CIDR block with your VPC and assign IPv6 address to resources in your VPC, however, communication between a ClassicLinked instance and resources in the VPC is over IPv4 only.
Topics

ClassicLink Basics
ClassicLink Limitations
Working with ClassicLink
API and CLI Overview
Example: ClassicLink Security Group Configuration for a Three-Tier Web Application
ClassicLink Basics

There are two steps to linking an EC2-Classic instance to a VPC using ClassicLink. First, you must enable the VPC for ClassicLink. By default, all VPCs in your account are not enabled for ClassicLink, to maintain their isolation. After you've enabled the VPC for ClassicLink, you can then link any running EC2-Classic instance in the same region in your account to that VPC. Linking your instance includes selecting security groups from the VPC to associate with your EC2-Classic instance. After you've linked the instance, it can communicate with instances in your VPC using their private IP addresses, provided the VPC security groups allow it. Your EC2-Classic instance does not lose its private IP address when linked to the VPC.

Note
Linking your instance to a VPC is sometimes referred to as attaching your instance.
A linked EC2-Classic instance can communicate with instances in a VPC, but it does not form part of the VPC. If you list your instances and filter by VPC, for example, through the DescribeInstances API request, or by using the Instances screen in the Amazon EC2 console, the results do not return any EC2-Classic instances that are linked to the VPC. For more information about viewing your linked EC2-Classic instances, see Viewing Your ClassicLink-Enabled VPCs and Linked EC2-Classic Instances.

By default, if you use a public DNS hostname to address an instance in a VPC from a linked EC2-Classic instance, the hostname resolves to the instance's public IP address. The same occurs if you use a public DNS hostname to address a linked EC2-Classic instance from an instance in the VPC. If you want the public DNS hostname to resolve to the private IP address, you can enable ClassicLink DNS support for the VPC. For more information, see Enabling ClassicLink DNS Support.

If you no longer require a ClassicLink connection between your instance and the VPC, you can unlink the EC2-Classic instance from the VPC. This disassociates the VPC security groups from the EC2-Classic instance. A linked EC2-Classic instance is automatically unlinked from a VPC when it's stopped. After you've unlinked all linked EC2-Classic instances from the VPC, you can disable ClassicLink for the VPC.

Using Other AWS Services in Your VPC With ClassicLink

Linked EC2-Classic instances can access the following AWS services in the VPC: Amazon Redshift, Amazon ElastiCache, Elastic Load Balancing, and Amazon RDS. However, instances in the VPC cannot access the AWS services provisioned by the EC2-Classic platform using ClassicLink.

If you use Elastic Load Balancing in your VPC, you can register your linked EC2-Classic instance with the load balancer, provided that the instance is in an Availability Zone in which your VPC has a subnet. If you terminate the linked EC2-Classic instance, the load balancer deregisters the instance. For more information about working with load balancers in a VPC, see Elastic Load Balancing in Amazon VPC in the Elastic Load Balancing User Guide.

If you use Auto Scaling, you can create an Auto Scaling group with instances that are automatically linked to a specified ClassicLink-enabled VPC at launch. For more information, see Linking EC2-Classic Instances to a VPC in the Auto Scaling User Guide.

If you use Amazon RDS instances or Amazon Redshift clusters in your VPC, and they are publicly accessible (accessible from the Internet), the endpoint you use to address those resources from a linked EC2-Classic instance by default resolves to a public IP address. If those resources are not publicly accessible, the endpoint resolves to a private IP address. To address a publicly accessible RDS instance or Redshift cluster over private IP using ClassicLink, you must use their private IP address or private DNS hostname, or you must enable ClassicLink DNS support for the VPC.

If you use a private DNS hostname or a private IP address to address an RDS instance, the linked EC2-Classic instance cannot use the failover support available for Multi-AZ deployments.

You can use the Amazon EC2 console to find the private IP addresses of your Amazon Redshift, Amazon ElastiCache, or Amazon RDS resources.

To locate the private IP addresses of AWS resources in your VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Check the descriptions of the network interfaces in the Description column. A network interface that's used by Amazon Redshift, Amazon ElastiCache, or Amazon RDS will have the name of the service in the description. For example, a network interface that's attached to an Amazon RDS instance will have the following description: RDSNetworkInterface.

Select the required network interface.

In the details pane, get the private IP address from the Primary private IPv4 IP field.

Controlling the Use of ClassicLink

By default, IAM users do not have permission to work with ClassicLink. You can create an IAM policy that grants users permissions to enable or disable a VPC for ClassicLink, link or unlink an instance to a ClassicLink-enabled VPC, and to view ClassicLink-enabled VPCs and linked EC2-Classic instances. For more information about IAM policies for Amazon EC2, see IAM Policies for Amazon EC2.

For more information about policies for working with ClassicLink, see the following example: 6. Working with ClassicLink.

Security Groups in ClassicLink

Linking your EC2-Classic instance to a VPC does not affect your EC2-Classic security groups. They continue to control all traffic to and from the instance. This excludes traffic to and from instances in the VPC, which is controlled by the VPC security groups that you associated with the EC2-Classic instance. EC2-Classic instances that are linked to the same VPC cannot communicate with each other through the VPC; regardless of whether they are associated with the same VPC security group. Communication between EC2-Classic instances is controlled by the EC2-Classic security groups associated with those instances. For an example of a security group configuration, see Example: ClassicLink Security Group Configuration for a Three-Tier Web Application.

After you've linked your instance to a VPC, you cannot change which VPC security groups are associated with the instance. To associate different security groups with your instance, you must first unlink the instance, and then link it to the VPC again, choosing the required security groups.

Routing for ClassicLink

When you enable a VPC for ClassicLink, a static route is added to all of the VPC route tables with a destination of 10.0.0.0/8 and a target of local. This allows communication between instances in the VPC and any EC2-Classic instances that are then linked to the VPC. If you add a custom route table to a ClassicLink-enabled VPC, a static route is automatically added with a destination of 10.0.0.0/8 and a target of local. When you disable ClassicLink for a VPC, this route is automatically deleted in all of the VPC route tables.

VPCs that are in the 10.0.0.0/16 and 10.1.0.0/16 IP address ranges can be enabled for ClassicLink only if they do not have any existing static routes in route tables in the 10.0.0.0/8 IP address range, excluding the local routes that were automatically added when the VPC was created. Similarly, if you've enabled a VPC for ClassicLink, you may not be able to add any more specific routes to your route tables within the 10.0.0.0/8 IP address range.

Important
If your VPC CIDR block is a publicly routable IP address range, consider the security implications before you link an EC2-Classic instance to your VPC. For example, if your linked EC2-Classic instance receives an incoming Denial of Service (DoS) request flood attack from a source IP address that falls within the VPC’s IP address range, the response traffic is sent into your VPC. We strongly recommend that you create your VPC using a private IP address range as specified in RFC 1918.
For more information about route tables and routing in your VPC, see Route Tables in the Amazon VPC User Guide.

Enabling a VPC Peering Connection for ClassicLink

If you have a VPC peering connection between two VPCs, and there are one or more EC2-Classic instances that are linked to one or both of the VPCs via ClassicLink, you can extend the VPC peering connection to enable communication between the EC2-Classic instances and the instances in the VPC on the other side of the VPC peering connection. This enables the EC2-Classic instances and the instances in the VPC to communicate using private IP addresses. To do this, you can enable a local VPC to communicate with a linked EC2-Classic instance in a peer VPC, or you can enable a local linked EC2-Classic instance to communicate with instances in a peer VPC.

If you enable a local VPC to communicate with a linked EC2-Classic instance in a peer VPC, a static route is automatically added to your route tables with a destination of 10.0.0.0/8 and a target of local.

For more information and examples, see Configurations With ClassicLink in the Amazon VPC Peering Guide.

ClassicLink Limitations

To use the ClassicLink feature, you need to be aware of the following limitations:

You can link an EC2-Classic instance to only one VPC at a time.
If you stop your linked EC2-Classic instance, it's automatically unlinked from the VPC, and the VPC security groups are no longer associated with the instance. You can link your instance to the VPC again after you've restarted it.
You cannot link an EC2-Classic instance to a VPC that's in a different region, or a different AWS account.
VPCs configured for dedicated hardware tenancy cannot be enabled for ClassicLink. Contact AWS support to request that your dedicated tenancy VPC be allowed to be enabled for ClassicLink.
Important
EC2-Classic instances are run on shared hardware. If you've set the tenancy of your VPC to dedicated because of regulatory or security requirements, then linking an EC2-Classic instance to your VPC may not conform to those requirements, as you will be allowing a shared tenancy resource to address your isolated resources directly using private IP addresses. If you want to enable your dedicated VPC for ClassicLink, provide a detailed motivation in your request to AWS support.
VPCs with routes that conflict with the EC2-Classic private IP address range of 10/8 cannot be enabled for ClassicLink. This does not include VPCs with 10.0.0.0/16 and 10.1.0.0/16 IP address ranges that already have local routes in their route tables. For more information, see Routing for ClassicLink.
You cannot associate a VPC Elastic IP address with a linked EC2-Classic instance.
You can link a running Spot instance to a VPC. To indicate in a Spot instance request that the instance should be linked to a VPC when the request is fulfilled, you must use the launch wizard in the Amazon EC2 console.
ClassicLink does not support transitive relationships out of the VPC. Your linked EC2-Classic instance will not have access to any VPN connection, VPC endpoint, or Internet gateway associated with the VPC. Similarly, resources on the other side of a VPN connection, or an Internet gateway will not have access to a linked EC2-Classic instance.
You cannot use ClassicLink to link a VPC instance to a different VPC, or to a EC2-Classic resource. To establish a private connection between VPCs, you can use a VPC peering connection. For more information, see the Amazon VPC Peering Guide.
If you link your EC2-Classic instance to a VPC in the 172.16.0.0/16 range, and you have a DNS server running on the 172.16.0.23/32 IP address within the VPC, then your linked EC2-Classic instance will not be able to access the VPC DNS server. To work around this issue, run your DNS server on a different IP address within the VPC.
Working with ClassicLink

You can use the Amazon EC2 and Amazon VPC consoles to work with the ClassicLink feature. You can enable or disable a VPC for ClassicLink, and link and unlink EC2-Classic instances to a VPC.

Note
The ClassicLink features are only visible in the consoles for accounts and regions that support EC2-Classic.
Topics

Enabling a VPC for ClassicLink
Linking an Instance to a VPC
Creating a VPC with ClassicLink Enabled
Linking an EC2-Classic Instance to a VPC at Launch
Viewing Your ClassicLink-Enabled VPCs and Linked EC2-Classic Instances
Enabling ClassicLink DNS Support
Disabling ClassicLink DNS Support
Unlinking a EC2-Classic Instance from a VPC
Disabling ClassicLink for a VPC
Enabling a VPC for ClassicLink

To link an EC2-Classic instance to a VPC, you must first enable the VPC for ClassicLink. You cannot enable a VPC for ClassicLink if the VPC has routing that conflicts with the EC2-Classic private IP address range. For more information, see Routing for ClassicLink.

To enable a VPC for ClassicLink

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs.

Choose a VPC, and then choose Actions, Enable ClassicLink.

In the confirmation dialog box, choose Yes, Enable.

Linking an Instance to a VPC

After you've enabled a VPC for ClassicLink, you can link an EC2-Classic instance to it.

Note
You can only link a running EC2-Classic instance to a VPC. You cannot link an instance that's in the stopped state.
To link an instance to a VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the running EC2-Classic instance, choose Actions, ClassicLink, Link to VPC. You can select more than one instance to link to the same VPC.

In the dialog box that displays, select a VPC from the list. Only VPCs that have been enabled for ClassicLink are displayed.

Select one or more of the VPC security groups to associate with your instance. When you are done, choose Link to VPC.

Creating a VPC with ClassicLink Enabled

You can create a new VPC and immediately enable it for ClassicLink by using the VPC wizard in the Amazon VPC console.

To create a VPC with ClassicLink enabled

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

From the Amazon VPC dashboard, choose Start VPC Wizard.

Select one of the VPC configuration options and choose Select.

On the next page of the wizard, choose Yes for Enable ClassicLink. Complete the rest of the steps in the wizard to create your VPC. For more information about using the VPC wizard, see Scenarios for Amazon VPC in the Amazon VPC User Guide.

Linking an EC2-Classic Instance to a VPC at Launch

You can use the launch wizard in the Amazon EC2 console to launch an EC2-Classic instance and immediately link it to a ClassicLink-enabled VPC.

To link an instance to a VPC at launch

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the Amazon EC2 dashboard, choose Launch Instance.

Select an AMI, and then choose an instance type. On the Configure Instance Details page, ensure that you select Launch into EC2-Classic from the Network list.

Note
Some instance types, such as T2 instance types, can only be launched into a VPC. Ensure that you select an instance type that can be launched into EC2-Classic.
In the Link to VPC (ClassicLink) section, select a VPC from Link to VPC. Only ClassicLink-enabled VPCs are displayed. Select the security groups from the VPC to associate with the instance. Complete the other configuration options on the page, and then complete the rest of the steps in the wizard to launch your instance. For more information about using the launch wizard, see Launching Your Instance from an AMI.

Viewing Your ClassicLink-Enabled VPCs and Linked EC2-Classic Instances

You can view all of your ClassicLink-enabled VPCs in the Amazon VPC console, and your linked EC2-Classic instances in the Amazon EC2 console.

To view your ClassicLink-enabled VPCs

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs.

Select a VPC, and in the Summary tab, look for the ClassicLink field. A value of Enabled indicates that the VPC is enabled for ClassicLink.

Alternatively, look for the ClassicLink column, and view the value that's displayed for each VPC (Enabled or Disabled). If the column is not visible, choose Edit Table Columns (the gear-shaped icon), select the ClassicLink attribute, and then choose Close.

To view your linked EC2-Classic instances

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select an EC2-Classic instance, and in the Description tab, look for the ClassicLink field. If the instance is linked to a VPC, the field displays the ID of the VPC to which the instance is linked. If the instance is not linked to any VPC, the field displays Unlinked.

Alternatively, you can filter your instances to display only linked EC2-Classic instances for a specific VPC or security group. In the search bar, start typing ClassicLink, select the relevant ClassicLink resource attribute, and then select the security group ID or the VPC ID.

Enabling ClassicLink DNS Support

You can enable ClassicLink DNS support for your VPC so that DNS hostnames that are addressed between linked EC2-Classic instances and instances in the VPC resolve to private IP addresses and not public IP addresses. For this feature to work, your VPC must be enabled for DNS hostnames and DNS resolution.

Note
If you enable ClassicLink DNS support for your VPC, your linked EC2-Classic instance can access any private hosted zone associated with the VPC. For more information, see Working with Private Hosted Zones in the Amazon Route 53 Developer Guide.
To enable ClassicLink DNS support

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs.

Select your VPC, and choose Actions, Edit ClassicLink DNS Support.

Choose Yes to enable ClassicLink DNS support, and choose Save.

Disabling ClassicLink DNS Support

You can disable ClassicLink DNS support for your VPC so that DNS hostnames that are addressed between linked EC2-Classic instances and instances in the VPC resolve to public IP addresses and not private IP addresses.

To disable ClassicLink DNS support

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs.

Select your VPC, and choose Actions, Edit ClassicLink DNS Support.

Choose No to disable ClassicLink DNS support, and choose Save.

Unlinking a EC2-Classic Instance from a VPC

If you no longer require a ClassicLink connection between your EC2-Classic instance and your VPC, you can unlink the instance from the VPC. Unlinking the instance disassociates the VPC security groups from the instance.

Note
A stopped instance is automatically unlinked from a VPC.
To unlink an instance from a VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances, and select your instance.

In the Actions list, select ClassicLink, Unlink Instance. You can select more than one instance to unlink from the same VPC.

Choose Yes in the confirmation dialog box.

Disabling ClassicLink for a VPC

If you no longer require a connection between EC2-Classic instances and your VPC, you can disable ClassicLink on the VPC. You must first unlink all linked EC2-Classic instances that are linked to the VPC.

To disable ClassicLink for a VPC

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs.

Select your VPC, then choose Actions, Disable ClassicLink.

In the confirmation dialog box, choose Yes, Disable.

API and CLI Overview

You can perform the tasks described on this page using the command line or the Query API. For more information about the command line interfaces and a list of available API actions, see Accessing Amazon EC2.

Enable a VPC for ClassicLink

enable-vpc-classic-link (AWS CLI)
Enable-EC2VpcClassicLink (AWS Tools for Windows PowerShell)
EnableVpcClassicLink (Amazon EC2 Query API)
Link (attach) an EC2-Classic instance to a VPC

attach-classic-link-vpc (AWS CLI)
Add-EC2ClassicLinkVpc (AWS Tools for Windows PowerShell)
AttachClassicLinkVpc (Amazon EC2 Query API)
Unlink (detach) an EC2-Classic instance from a VPC

detach-classic-link-vpc (AWS CLI)
Dismount-EC2ClassicLinkVpc (AWS Tools for Windows PowerShell)
DetachClassicLinkVpc (Amazon EC2 Query API)
Disable ClassicLink for a VPC

disable-vpc-classic-link (AWS CLI)
Disable-EC2VpcClassicLink (AWS Tools for Windows PowerShell)
DisableVpcClassicLink (Amazon EC2 Query API)
Describe the ClassicLink status of VPCs

describe-vpc-classic-link (AWS CLI)
Get-EC2VpcClassicLink (AWS Tools for Windows PowerShell)
DescribeVpcClassicLink (Amazon EC2 Query API)
Describe linked EC2-Classic instances

describe-classic-link-instances (AWS CLI)
Get-EC2ClassicLinkInstance (AWS Tools for Windows PowerShell)
DescribeClassicLinkInstances (Amazon EC2 Query API)
Enable a VPC peering connection for ClassicLink

modify-vpc-peering-connection-options (AWS CLI)
Edit-EC2VpcPeeringConnectionOption (AWS Tools for Windows PowerShell)
ModifyVpcPeeringConnectionOptions(Amazon EC2 Query API)
Enable a VPC for ClassicLink DNS support

enable-vpc-classic-link-dns-support (AWS CLI)
Enable-EC2VpcClassicLinkDnsSupport (AWS Tools for Windows PowerShell)
EnableVpcClassicLinkDnsSupport (Amazon EC2 Query API)
Disable a VPC for ClassicLink DNS support

disable-vpc-classic-link-dns-support (AWS CLI)
Disable-EC2VpcClassicLinkDnsSupport (AWS Tools for Windows PowerShell)
DisableVpcClassicLinkDnsSupport (Amazon EC2 Query API)
Describe ClassicLink DNS support for VPCs

describe-vpc-classic-link-dns-support (AWS CLI)
Get-EC2VpcClassicLinkDnsSupport (AWS Tools for Windows PowerShell)
DescribeVpcClassicLinkDnsSupport (Amazon EC2 Query API)
Example: ClassicLink Security Group Configuration for a Three-Tier Web Application

In this example, you have an application with three instances: a public-facing web server, an application server, and a database server. Your web server accepts HTTPS traffic from the Internet, and then communicates with your application server over TCP port 6001. Your application server then communicates with your database server over TCP port 6004. You're in the process of migrating your entire application to a VPC in your account. You've already migrated your application server and your database server to your VPC. Your web server is still in EC2-Classic and linked to your VPC via ClassicLink.

You want a security group configuration that allows traffic to flow only between these instances. You have four security groups: two for your web server (sg-1a1a1a1a and sg-2b2b2b2b), one for your application server (sg-3c3c3c3c), and one for your database server (sg-4d4d4d4d).

The following diagram displays the architecture of your instances, and their security group configuration.


          Security group configuration using ClassicLink.
        
Security Groups for Your Web Server (sg-1a1a1a1a and sg-2b2b2b2b)

You have one security group in EC2-Classic, and the other in your VPC. You associated the VPC security group with your web server instance when you linked the instance to your VPC via ClassicLink. The VPC security group enables you to control the outbound traffic from your web server to your application server.

The following are the security group rules for the EC2-Classic security group (sg-1a1a1a1a).

Inbound
Source	Type	Port Range	Comments
0.0.0.0/0
HTTPS
443
Allows Internet traffic to reach your web server.
The following are the security group rules for the VPC security group (sg-2b2b2b2b).

Outbound
Destination	Type	Port Range	Comments
sg-3c3c3c3c
TCP
6001
Allows outbound traffic from your web server to your application server in your VPC (or to any other instance associated with sg-3c3c3c3c).
Security Group for Your Application Server (sg-3c3c3c3c)

The following are the security group rules for the VPC security group that's associated with your application server.

Inbound
Source	Type	Port Range	Comments
sg-2b2b2b2b
TCP
6001
Allows the specified type of traffic from your web server (or any other instance associated with sg-2b2b2b2b) to reach your application server.
Outbound
Destination	Type	Port Range	Comments
sg-4d4d4d4d	TCP	6004	Allows outbound traffic from the application server to the database server (or to any other instance associated with sg-4d4d4d4d).
Security Group for Your Database Server (sg-4d4d4d4d)

The following are the security group rules for the VPC security group that's associated with your database server.

Inbound
Source	Type	Port Range	Comments
sg-3c3c3c3c
TCP
6004
Allows the specified type of traffic from your application server (or any other instance associated with sg-3c3c3c3c) to reach your database server.

Migrating from a Linux Instance in EC2-Classic to a Linux Instance in a VPC

Your AWS account might support both EC2-Classic and EC2-VPC, depending on when you created your account and which regions you've used. For more information, and to find out which platform your account supports, see Supported Platforms. For more information about the benefits of using a VPC, and the differences between EC2-Classic and EC2-VPC, see Amazon EC2 and Amazon Virtual Private Cloud.

You create and use resources in your AWS account. Some resources and features, such as enhanced networking and certain instance types, can be used only in a VPC. Some resources can be shared between EC2-Classic and a VPC, while some can't. For more information, see Sharing and Accessing Resources Between EC2-Classic and EC2-VPC.

If your account supports EC2-Classic, you might have set up resources for use in EC2-Classic. If you want to migrate from EC2-Classic to a VPC, you must recreate those resources in your VPC.

There are two ways of migrating to a VPC. You can do a full migration, or you can do an incremental migration over time. The method you choose depends on the size and complexity of your application in EC2-Classic. For example, if your application consists of one or two instances running a static website, and you can afford a short period of downtime, you can do a full migration. If you have a multi-tier application with processes that cannot be interrupted, you can do an incremental migration using ClassicLink. This allows you to transfer functionality one component at a time until your application is running fully in your VPC.

If you need to migrate a Windows instance, see Migrating a Windows Instance from EC2-Classic to a VPC in the Amazon EC2 User Guide for Windows Instances.

Contents

Full Migration to a VPC
Incremental Migration to a VPC Using ClassicLink
Full Migration to a VPC

Complete the following tasks to fully migrate your application from EC2-Classic to a VPC.

Tasks

Step 1: Create a VPC
Step 2: Configure Your Security Group
Step 3: Create an AMI from Your EC2-Classic Instance
Step 4: Launch an Instance Into Your VPC
Example: Migrating a Simple Web Application
Step 1: Create a VPC

To start using a VPC, ensure that you have one in your account. You can create one using one of these methods:

Use a new, EC2-VPC-only AWS account. Your EC2-VPC-only account comes with a default VPC in each region, which is ready for you to use. Instances that you launch are by default launched into this VPC, unless you specify otherwise. For more information about your default VPC, see Your Default VPC and Subnets. Use this option if you'd prefer not to set up a VPC yourself, or if you do not need specific requirements for your VPC configuration.
In your existing AWS account, open the Amazon VPC console and use the VPC wizard to create a new VPC. For more information, see Scenarios for Amazon VPC. Use this option if you want to set up a VPC quickly in your existing EC2-Classic account, using one of the available configuration sets in the wizard. You'll specify this VPC each time you launch an instance.
In your existing AWS account, open the Amazon VPC console and set up the components of a VPC according to your requirements. For more information, see Your VPC and Subnets. Use this option if you have specific requirements for your VPC, such as a particular number of subnets. You'll specify this VPC each time you launch an instance.
Step 2: Configure Your Security Group

You cannot use the same security groups between EC2-Classic and a VPC. However, if you want your instances in your VPC to have the same security group rules as your EC2-Classic instances, you can use the Amazon EC2 console to copy your existing EC2-Classic security group rules to a new VPC security group.

Important
You can only copy security group rules to a new security group in the same AWS account in the same region. If you've created a new AWS account, you cannot use this method to copy your existing security group rules to your new account. You'll have to create a new security group, and add the rules yourself. For more information about creating a new security group, see Amazon EC2 Security Groups for Linux Instances.
To copy your security group rules to a new security group

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Security Groups.

Select the security group that's associated with your EC2-Classic instance, then choose Actions and select Copy to new.

In the Create Security Group dialog box, specify a name and description for your new security group. Select your VPC from the VPC list.

The Inbound tab is populated with the rules from your EC2-Classic security group. You can modify the rules as required. In the Outbound tab, a rule that allows all outbound traffic has automatically been created for you. For more information about modifying security group rules, see Amazon EC2 Security Groups for Linux Instances.

Note
If you've defined a rule in your EC2-Classic security group that references another security group, you will not be able to use the same rule in your VPC security group. Modify the rule to reference a security group in the same VPC.
Choose Create.

Step 3: Create an AMI from Your EC2-Classic Instance

An AMI is a template for launching your instance. You can create your own AMI based on an existing EC2-Classic instance, then use that AMI to launch instances into your VPC.

The method you use to create your AMI depends on the root device type of your instance, and the operating system platform on which your instance runs. To find out the root device type of your instance, go to the Instances page, select your instance, and look at the information in the Root device type field in the Description tab. If the value is ebs, then your instance is EBS-backed. If the value is instance-store, then your instance is instance store-backed. You can also use the describe-instances AWS CLI command to find out the root device type.

The following table provides options for you to create your AMI based on the root device type of your instance, and the software platform.

Important
Some instance types support both PV and HVM virtualization, while others support only one or the other. If you plan to use your AMI to launch a different instance type than your current instance type, check that the instance type supports the type of virtualization that your AMI offers. If your AMI supports PV virtualization, and you want to use an instance type that supports HVM virtualization, you may have to reinstall your software on a base HVM AMI. For more information about PV and HVM virtualization, see Linux AMI Virtualization Types.
Instance Root Device Type	Action
EBS	Create an EBS-backed AMI from your instance. For more information, see Creating an Amazon EBS-Backed Linux AMI.
Instance store	Create an instance store-backed AMI from your instance using the AMI tools. For more information, see Creating an Instance Store-Backed Linux AMI.
Instance store	Transfer your instance data to an EBS volume, then take a snapshot of the volume, and create an AMI from the snapshot. For more information, see Converting your Instance Store-Backed AMI to an Amazon EBS-Backed AMI.
Note
This method converts an instance store-backed instance to an EBS-backed instance.
(Optional) Store Your Data on Amazon EBS Volumes

You can create an Amazon EBS volume and use it to back up and store the data on your instance—like you would use a physical hard drive. Amazon EBS volumes can be attached and detached from any instance in the same Availability Zone. You can detach a volume from your instance in EC2-Classic, and attach it to a new instance that you launch into your VPC in the same Availability Zone.

For more information about Amazon EBS volumes, see the following topics:

Amazon EBS Volumes
Creating an Amazon EBS Volume
Attaching an Amazon EBS Volume to an Instance
To back up the data on your Amazon EBS volume, you can take periodic snapshots of your volume. If you need to, you can restore an Amazon EBS volume from your snapshot. For more information about Amazon EBS snapshots, see the following topics:

Amazon EBS Snapshots
Creating an Amazon EBS Snapshot
Restoring an Amazon EBS Volume from a Snapshot
Step 4: Launch an Instance Into Your VPC

After you've created an AMI, you can launch an instance into your VPC. The instance will have the same data and configurations as your existing EC2-Classic instance.

You can either launch your instance into a VPC that you've created in your existing account, or into a new, VPC-only AWS account.

Using Your Existing EC2-Classic Account

You can use the Amazon EC2 launch wizard to launch an instance into your VPC.

To launch an instance into your VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the dashboard, choose Launch Instance.

On the Choose an Amazon Machine Image page, select the My AMIs category, and select the AMI you created.

On the Choose an Instance Type page, select the type of instance, and choose Next: Configure Instance Details.

On the Configure Instance Details page, select your VPC from the Network list. Select the required subnet from the Subnet list. Configure any other details you require, then go through the next pages of the wizard until you reach the Configure Security Group page.

Select Select an existing group, and select the security group you created earlier. Choose Review and Launch.

Review your instance details, then choose Launch to specify a key pair and launch your instance.

For more information about the parameters you can configure in each step of the wizard, see Launching an Instance.

Using Your New, VPC-Only Account

To launch an instance in your new AWS account, you'll first have to share the AMI you created with your new account. You can then use the Amazon EC2 launch wizard to launch an instance into your default VPC.

To share an AMI with your new AWS account

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Switch to the account in which you created your AMI.

In the navigation pane, choose AMIs.

In the Filter list, ensure Owned by me is selected, then select your AMI.

In the Permissions tab, choose Edit. Enter the account number of your new AWS account, choose Add Permission, and then choose Save.

To launch an instance into your default VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Switch to your new AWS account.

In the navigation pane, choose AMIs.

In the Filter list, select Private images. Select the AMI that you shared from your EC2-Classic account, then choose Launch.

On the Choose an Instance Type page, select the type of instance, and choose Next: Configure Instance Details.

On the Configure Instance Details page, your default VPC should be selected in the Network list. Configure any other details you require, then go through the next pages of the wizard until you reach the Configure Security Group page.

Select Select an existing group, and select the security group you created earlier. Choose Review and Launch.

Review your instance details, then choose Launch to specify a key pair and launch your instance.

For more information about the parameters you can configure in each step of the wizard, see Launching an Instance.

Example: Migrating a Simple Web Application

In this example, you use AWS to host your gardening website. To manage your website, you have three running instances in EC2-Classic. Instances A and B host your public-facing web application, and you use an Elastic Load Balancer to load balance the traffic between these instances. You've assigned Elastic IP addresses to instances A and B so that you have static IP addresses for configuration and administration tasks on those instances. Instance C holds your MySQL database for your website. You've registered the domain name www.garden.example.com, and you've used Amazon Route 53 to create a hosted zone with an alias record set that's associated with the DNS name of your load balancer.


					A web application in EC2-Classic
				
The first part of migrating to a VPC is deciding what kind of VPC architecture will suit your needs. In this case, you've decided on the following: one public subnet for your web servers, and one private subnet for your database server. As your website grows, you can add more web servers and database servers to your subnets. By default, instances in the private subnet cannot access the Internet; however, you can enable Internet access through a Network Address Translation (NAT) device in the public subnet. You may want to set up a NAT device to support periodic updates and patches from the Internet for your database server. You'll migrate your Elastic IP addresses to EC2-VPC, and create an Elastic Load Balancer in your public subnet to load balance the traffic between your web servers.


					A web application in a VPC
				
To migrate your web application to a VPC, you can follow these steps:

Create a VPC: In this case, you can use the VPC wizard in the Amazon VPC console to create your VPC and subnets. The second wizard configuration creates a VPC with one private and one public subnet, and launches and configures a NAT device in your public subnet for you. For more information, see Scenario 2: VPC with Public and Private Subnets in the Amazon VPC User Guide.
Create AMIs from your instances: Create an AMI from one of your web servers, and a second AMI from your database server. For more information, see Step 3: Create an AMI from Your EC2-Classic Instance.
Configure your security groups: In your EC2-Classic environment, you have one security group for your web servers, and another security group for your database server. You can use the Amazon EC2 console to copy the rules from each security group into new security groups for your VPC. For more information, see Step 2: Configure Your Security Group.
Tip
Create the security groups that are referenced by other security groups first.
Launch an instance into your new VPC: Launch replacement web servers into your public subnet, and launch your replacement database server into your private subnet. For more information, see Step 4: Launch an Instance Into Your VPC.
Configure your NAT device: If you are using a NAT instance, you must create security group for it that allows HTTP and HTTPS traffic from your private subnet. For more information, see NAT Instances. If you are using a NAT gateway, traffic from your private subnet is automatically allowed.
Configure your database: When you created an AMI from your database server in EC2-Classic, all the configuration information that was stored in that instance was copied to the AMI. You may have to connect to your new database server and update the configuration details; for example, if you configured your database to grant full read, write, and modification permissions to your web servers in EC2-Classic, you'll have to update the configuration files to grant the same permissions to your new VPC web servers instead.
Configure your web servers: Your web servers will have the same configuration settings as your instances in EC2-Classic. For example, if you configured your web servers to use the database in EC2-Classic, update your web servers' configuration settings to point to your new database instance.
Note
By default, instances launched into a nondefault subnet are not assigned a public IP address, unless you specify otherwise at launch. Your new database server may not have a public IP address. In this case, you can update your web servers' configuration file to use your new database server's private DNS name. Instances in the same VPC can communicate with each other via private IP address.
Migrate your Elastic IP addresses: Disassociate your Elastic IP addresses from your web servers in EC2-Classic, and then migrate them to EC2-VPC. After you've migrated them, you can associate them with your new web servers in your VPC. For more information, see Migrating an Elastic IP Address from EC2-Classic to EC2-VPC.
Create a new load balancer: To continue using Elastic Load Balancing to load balance the traffic to your instances, make sure you understand the various ways you can configure your load balancer in VPC. For more information, see Elastic Load Balancing in Amazon VPC.
Update your DNS records: After you've set up your load balancer in your public subnet, ensure that your www.garden.example.com domain points to your new load balancer. To do this, you'll need to update your DNS records and update your alias record set in Amazon Route 53. For more information about using Amazon Route 53, see Getting Started with Amazon Route 53.
Shut down your EC2-Classic resources: After you've verified that your web application is working from within the VPC architecture, you can shut down your EC2-Classic resources to stop incurring charges for them. Terminate your EC2-Classic instances, and release your EC2-Classic Elastic IP addresses.
Incremental Migration to a VPC Using ClassicLink

The ClassicLink feature makes it easier to manage an incremental migration to a VPC. ClassicLink allows you to link an EC2-Classic instance to a VPC in your account in the same region, allowing your new VPC resources to communicate with the EC2-Classic instance using private IPv4 addresses. You can then migrate functionality to the VPC one step at a time. This topic provides some basic steps for managing an incremental migration from EC2-Classic to a VPC.

For more information about ClassicLink, see ClassicLink.

Topics

Step 1: Prepare Your Migration Sequence
Step 2: Create a VPC
Step 3: Enable Your VPC for ClassicLink
Step 4: Create an AMI from Your EC2-Classic Instance
Step 5: Launch an Instance Into Your VPC
Step 6: Link Your EC2-Classic Instances to Your VPC
Step 7: Complete the VPC Migration
Step 1: Prepare Your Migration Sequence

To use ClassicLink effectively, you must first identify the components of your application that must be migrated to the VPC, and then confirm the order in which to migrate that functionality.

For example, you have an application that relies on a presentation web server, a backend database server, and authentication logic for transactions. You may decide to start the migration process with the authentication logic, then the database server, and finally, the web server.

Step 2: Create a VPC

To start using a VPC, ensure that you have one in your account. You can create one using one of these methods:

In your existing AWS account, open the Amazon VPC console and use the VPC wizard to create a new VPC. For more information, see Scenarios for Amazon VPC. Use this option if you want to set up a VPC quickly in your existing EC2-Classic account, using one of the available configuration sets in the wizard. You'll specify this VPC each time you launch an instance.
In your existing AWS account, open the Amazon VPC console and set up the components of a VPC according to your requirements. For more information, see Your VPC and Subnets. Use this option if you have specific requirements for your VPC, such as a particular number of subnets. You'll specify this VPC each time you launch an instance.
Step 3: Enable Your VPC for ClassicLink

After you've created a VPC, you can enable it for ClassicLink. For more information about ClassicLink, see ClassicLink.

To enable a VPC for ClassicLink

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

In the navigation pane, choose Your VPCs.

Select your VPC, and then select Enable ClassicLink from the Actions list.

In the confirmation dialog box, choose Yes, Enable.

Step 4: Create an AMI from Your EC2-Classic Instance

An AMI is a template for launching your instance. You can create your own AMI based on an existing EC2-Classic instance, then use that AMI to launch instances into your VPC.

The method you use to create your AMI depends on the root device type of your instance, and the operating system platform on which your instance runs. To find out the root device type of your instance, go to the Instances page, select your instance, and look at the information in the Root device type field in the Description tab. If the value is ebs, then your instance is EBS-backed. If the value is instance-store, then your instance is instance store-backed. You can also use the describe-instances AWS CLI command to find out the root device type.

The following table provides options for you to create your AMI based on the root device type of your instance, and the software platform.

Important
Some instance types support both PV and HVM virtualization, while others support only one or the other. If you plan to use your AMI to launch a different instance type than your current instance type, check that the instance type supports the type of virtualization that your AMI offers. If your AMI supports PV virtualization, and you want to use an instance type that supports HVM virtualization, you may have to reinstall your software on a base HVM AMI. For more information about PV and HVM virtualization, see Linux AMI Virtualization Types.
Instance Root Device Type	Action
EBS	Create an EBS-backed AMI from your instance. For more information, see Creating an Amazon EBS-Backed Linux AMI.
Instance store	Create an instance store-backed AMI from your instance using the AMI tools. For more information, see Creating an Instance Store-Backed Linux AMI.
Instance store	Transfer your instance data to an EBS volume, then take a snapshot of the volume, and create an AMI from the snapshot. For more information, see Converting your Instance Store-Backed AMI to an Amazon EBS-Backed AMI.
Note
This method converts an instance store-backed instance to an EBS-backed instance.
(Optional) Store Your Data on Amazon EBS Volumes

You can create an Amazon EBS volume and use it to back up and store the data on your instance—like you would use a physical hard drive. Amazon EBS volumes can be attached and detached from any instance in the same Availability Zone. You can detach a volume from your instance in EC2-Classic, and attach it to a new instance that you launch into your VPC in the same Availability Zone.

For more information about Amazon EBS volumes, see the following topics:

Amazon EBS Volumes
Creating an Amazon EBS Volume
Attaching an Amazon EBS Volume to an Instance
To back up the data on your Amazon EBS volume, you can take periodic snapshots of your volume. If you need to, you can restore an Amazon EBS volume from your snapshot. For more information about Amazon EBS snapshots, see the following topics:

Amazon EBS Snapshots
Creating an Amazon EBS Snapshot
Restoring an Amazon EBS Volume from a Snapshot
Step 5: Launch an Instance Into Your VPC

The next step in the migration process is to launch instances into your VPC so that you can start transferring functionality to them. You can use the AMIs that you created in the previous step to launch instances into your VPC. The instances will have the same data and configurations as your existing EC2-Classic instances.

To launch an instance into your VPC using your custom AMI

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

On the dashboard, choose Launch Instance.

On the Choose an Amazon Machine Image page, select the My AMIs category, and select the AMI you created.

On the Choose an Instance Type page, select the type of instance, and choose Next: Configure Instance Details.

On the Configure Instance Details page, select your VPC from the Network list. Select the required subnet from the Subnet list. Configure any other details you require, then go through the next pages of the wizard until you reach the Configure Security Group page.

Select Select an existing group, and select the security group you created earlier. Choose Review and Launch.

Review your instance details, then choose Launch to specify a key pair and launch your instance.

For more information about the parameters you can configure in each step of the wizard, see Launching an Instance.

After you've launched your instance and it's in the running state, you can connect to it and configure it as required.

Step 6: Link Your EC2-Classic Instances to Your VPC

After you've configured your instances and made the functionality of your application available in the VPC, you can use ClassicLink to enable private IP communication between your new VPC instances and your EC2-Classic instances.

To link an instance to a VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your EC2-Classic instance, then choose Actions, ClassicLink, and Link to VPC.

Note
Ensure that your instance is in the running state.
In the dialog box, select your ClassicLink-enabled VPC (only VPCs that are enabled for ClassicLink are displayed).

Select one or more of the VPC security groups to associate with your instance. When you are done, choose Link to VPC.

Step 7: Complete the VPC Migration

Depending on the size of your application and the functionality that must be migrated, repeat steps 4 to 6 until you've moved all the components of your application from EC2-Classic into your VPC.

After you've enabled internal communication between the EC2-Classic and VPC instances, you must update your application to point to your migrated service in your VPC, instead of your service in the EC2-Classic platform. The exact steps for this depend on your application’s design. Generally, this includes updating your destination IP addresses to point to the IP addresses of your VPC instances instead of your EC2-Classic instances. You can migrate your Elastic IP addresses that you are currently using in the EC2-Classic platform to the EC2-VPC platform. For more information, see Migrating an Elastic IP Address from EC2-Classic to EC2-VPC.

After you've completed this step and you've tested that the application is functioning from your VPC, you can terminate your EC2-Classic instances, and disable ClassicLink for your VPC. You can also clean up any EC2-Classic resources that you may no longer need to avoid incurring charges for them; for example, you can release Elastic IP addresses, and delete the volumes that were associated with your EC2-Classic instances.


Amazon EC2 Instance IP Addressing

We provide your instances with IP addresses and IPv4 DNS hostnames. These can vary depending on whether you launched the instance in the EC2-Classic platform or in a virtual private cloud (VPC). For information about the EC2-Classic and EC2-VPC platforms, see Supported Platforms.

Amazon EC2 and Amazon VPC support both the IPv4 and IPv6 addressing protocols. By default, Amazon EC2 and Amazon VPC use the IPv4 addressing protocol; you can't disable this behavior. When you create a VPC, you must specify an IPv4 CIDR block (a range of private IPv4 addresses). You can optionally assign an IPv6 CIDR block to your VPC and subnets, and assign IPv6 addresses from that block to instances in your subnet. IPv6 addresses are reachable over the Internet. For more information about IPv6, see IP Addressing in Your VPC in the Amazon VPC User Guide.

IPv6 is not supported for the EC2-Classic platform.

Contents

Private IPv4 Addresses and Internal DNS Hostnames
Public IPv4 Addresses and External DNS Hostnames
Elastic IP Addresses (IPv4)
Amazon DNS Server
IPv6 Addresses
IP Address Differences Between EC2-Classic and EC2-VPC
Working with IP Addresses for Your Instance
Multiple IP Addresses
Private IPv4 Addresses and Internal DNS Hostnames

A private IPv4 address is an IP address that's not reachable over the Internet. You can use private IPv4 addresses for communication between instances in the same network (EC2-Classic or a VPC). For more information about the standards and specifications of private IPv4 addresses, see RFC 1918.

Note
You can create a VPC with a publicly routable CIDR block that falls outside of the private IPv4 address ranges specified in RFC 1918. However, for the purposes of this documentation, we refer to private IPv4 addresses (or 'private IP addresses') as the IP addresses that are within the IPv4 CIDR range of your VPC.
When you launch an instance, we allocate a private IPv4 address for the instance using DHCP. Each instance is also given an internal DNS hostname that resolves to the private IPv4 address of the instance; for example, ip-10-251-50-12.ec2.internal. You can use the internal DNS hostname for communication between instances in the same network, but we can't resolve the DNS hostname outside the network that the instance is in.

An instance launched in a VPC is given a primary private IP address in the IPv4 address range of the subnet. For more information, see Subnet Sizing in the Amazon VPC User Guide. If you don't specify a primary private IP address when you launch the instance, we select an available IP address in the subnet's IPv4 range for you. Each instance in a VPC has a default network interface (eth0) that is assigned the primary private IPv4 address. You can also specify additional private IPv4 addresses, known as secondary private IPv4 addresses. Unlike primary private IP addresses, secondary private IP addresses can be reassigned from one instance to another. For more information, see Multiple IP Addresses.

For instances launched in EC2-Classic, we release the private IPv4 address when the instance is stopped or terminated. If you restart your stopped instance, it receives a new private IPv4 address.

For instances launched in a VPC, a private IPv4 address remains associated with the network interface when the instance is stopped and restarted, and is released when the instance is terminated.

If you create a custom firewall configuration in EC2-Classic, you must create a rule in your firewall that allows inbound traffic from port 53 (DNS)—with a destination port from the ephemeral range—from the address of the Amazon DNS server; otherwise, internal DNS resolution from your instances fails. If your firewall doesn't automatically allow DNS query responses, then you need to allow traffic from the IP address of the Amazon DNS server. To get the IP address of the Amazon DNS server, use the following command from within your instance:

Copy
grep nameserver /etc/resolv.conf
Public IPv4 Addresses and External DNS Hostnames

A public IP address is an IPv4 address that's reachable from the Internet. You can use public addresses for communication between your instances and the Internet.

Each instance that receives a public IP address is also given an external DNS hostname; for example, ec2-203-0-113-25.compute-1.amazonaws.com. We resolve an external DNS hostname to the public IP address of the instance outside the network of the instance, and to the private IPv4 address of the instance from within the network of the instance. The public IP address is mapped to the primary private IP address through network address translation (NAT). For more information about NAT, see RFC 1631: The IP Network Address Translator (NAT).

When you launch an instance in EC2-Classic, we automatically assign a public IP address to the instance from the EC2-Classic public IPv4 address pool. You cannot modify this behavior. When you launch an instance into a VPC, your subnet has an attribute that determines whether instances launched into that subnet receive a public IP address from the EC2-VPC public IPv4 address pool. By default, we assign a public IP address to instances launched in a default VPC, and we don't assign a public IP address to instances launched in a nondefault subnet.

You can control whether your instance in a VPC receives a public IP address by doing the following:

Modifying the public IP addressing attribute of your subnet. For more information, see Modifying the Public IPv4 Addressing Attribute for Your Subnet in the Amazon VPC User Guide.
Enabling or disabling the public IP addressing feature during launch, which overrides the subnet's public IP addressing attribute. For more information, see Assigning a Public IPv4 Address During Instance Launch.
A public IP address is assigned to your instance from Amazon's pool of public IPv4 addresses, and is not associated with your AWS account. When a public IP address is disassociated from your instance, it is released back into the public IPv4 address pool, and you cannot reuse it.

You cannot manually associate or disassociate a public IP address from your instance. Instead, in certain cases, we release the public IP address from your instance, or assign it a new one:

We release the public IP address for your instance when it's stopped or terminated. Your stopped instance receives a new public IP address when it's restarted.
We release the public IP address for your instance when you associate an Elastic IP address with your instance, or when you associate an Elastic IP address with the primary network interface (eth0) of your instance in a VPC. When you disassociate the Elastic IP address from your instance, it receives a new public IP address.
If the public IP address of your instance in a VPC has been released, it will not receive a new one if there is more than one network interface attached to your instance.
If you require a persistent public IP address that can be associated to and from instances as you require, use an Elastic IP address instead. For example, if you use dynamic DNS to map an existing DNS name to a new instance's public IP address, it might take up to 24 hours for the IP address to propagate through the Internet. As a result, new instances might not receive traffic while terminated instances continue to receive requests. To solve this problem, use an Elastic IP address. You can allocate your own Elastic IP address, and associate it with your instance. For more information, see Elastic IP Addresses.

If your instance is in a VPC and you assign it an Elastic IP address, it receives an IPv4 DNS hostname if DNS hostnames are enabled. For more information, see Using DNS with Your VPC in the Amazon VPC User Guide.

Note
Instances that access other instances through their public NAT IP address are charged for regional or Internet data transfer, depending on whether the instances are in the same region.
Elastic IP Addresses (IPv4)

An Elastic IP address is a public IPv4 address that you can allocate to your account. You can associate it to and from instances as you require, and it's allocated to your account until you choose to release it. For more information about Elastic IP addresses and how to use them, see Elastic IP Addresses.

We do not support Elastic IP addresses for IPv6.

Amazon DNS Server

Amazon provides a DNS server that resolves Amazon-provided IPv4 DNS hostnames to IPv4 addresses. In EC2-Classic, the Amazon DNS server is located at 172.16.0.23. In EC2-VPC, the Amazon DNS server is located at the base of your VPC network range plus two. For more information, see Amazon DNS Server in the Amazon VPC User Guide.

IPv6 Addresses

You can optionally associate an IPv6 CIDR block with your VPC, and associate IPv6 CIDR blocks with your subnets. The IPv6 CIDR block for your VPC is automatically assigned from Amazon's pool of IPv6 addresses; you cannot choose the range yourself. For more information, see the following topics in the Amazon VPC User Guide:

VPC and Subnet Sizing for IPv6
Associating an IPv6 CIDR Block with Your VPC
Associating an IPv6 CIDR Block with Your Subnet
IPv6 addresses are globally unique, and therefore reachable over the Internet. Your instance in a VPC receives an IPv6 address if an IPv6 CIDR block is associated with your VPC and subnet, and if one of the following is true:

Your subnet is configured to automatically assign an IPv6 address to an instance during launch. For more information, see Modifying the IPv6 Addressing Attribute for Your Subnet.
You assign an IPv6 address to your instance during launch.
You assign an IPv6 address to the primary network interface of your instance after launch.
You assign an IPv6 address to a network interface in the same subnet, and attach the network interface to your instance after launch.
When your instance receives an IPv6 address during launch, the address is associated with the primary network interface (eth0) of the instance. You can disassociate the IPv6 address from the network interface. We do not support IPv6 DNS hostnames for your instance.

An IPv6 address persists when you stop and start your instance, and is released when you terminate your instance. You cannot reassign an IPv6 address while it's assigned to another network interface—you must first unassign it.

You can assign additional IPv6 addresses to your instance by assigning them to a network interface attached to your instance. The number of IPv6 addresses you can assign to a network interface and the number of network interfaces you can attach to an instance varies per instance type. For more information, see IP Addresses Per Network Interface Per Instance Type.

IP Address Differences Between EC2-Classic and EC2-VPC

The following table summarizes the differences between IP addresses for instances launched in EC2-Classic, instances launched in a default subnet, and instances launched in a nondefault subnet.

Characteristic	EC2-Classic	Default Subnet	Nondefault Subnet
Public IP address (from Amazon's public IPv4 address pool)
Your instance receives a public IP address.
Your instance receives a public IP address by default, unless you specify otherwise during launch, or you modify the subnet's public IP address attribute.
Your instance doesn't receive a public IP address by default, unless you specify otherwise during launch, or you modify the subnet's public IP address attribute.
Private IPv4 address
Your instance receives a private IP address from the EC2-Classic range each time it's started.
Your instance receives a static private IP address from the IPv4 address range of your default subnet.
Your instance receives a static private IP address from the IPv4 address range of your subnet.
Multiple IPv4 addresses
We select a single private IP address for your instance; multiple IP addresses are not supported.
You can assign multiple private IP addresses to your instance.
You can assign multiple private IP addresses to your instance.
Network interfaces
IP addresses are associated with the instance; network interfaces aren't supported.
IP addresses are associated with a network interface. Each instance has one or more network interfaces.
IP addresses are associated with a network interface. Each instance has one or more network interfaces.
Elastic IP address (IPv4)
An Elastic IP address is disassociated from your instance when you stop it.
An Elastic IP address remains associated with your instance when you stop it.
An Elastic IP address remains associated with your instance when you stop it.
DNS hostnames (IPv4)
DNS hostnames are enabled by default.
DNS hostnames are enabled by default.
DNS hostnames are disabled by default, except if you've created your VPC using the VPC wizard in the Amazon VPC console.
IPv6 address	Not supported. Your instance cannot receive an IPv6 address.	Your instance does not receive an IPv6 address by default unless you've associated an IPv6 CIDR block with your VPC and subnet, and either specified an IPv6 address during launch, or modified your subnet's IPv6 addressing attribute.	Your instance does not receive an IPv6 address by default unless you've associated an IPv6 CIDR block with your VPC and subnet, and either specified an IPv6 address during launch, or modified your subnet's IPv6 addressing attribute.
Working with IP Addresses for Your Instance

You can view the IP addresses assigned to your instance, assign a public IPv4 address to your instance during launch, or assign an IPv6 address to your instance during launch.

Contents

Determining Your Public, Private, and Elastic IP Addresses
Determining Your IPv6 Addresses
Assigning a Public IPv4 Address During Instance Launch
Assigning an IPv6 Address to an Instance
Unassigning an IPv6 Address From an Instance
Determining Your Public, Private, and Elastic IP Addresses

You can use the Amazon EC2 console to determine the private IPv4 addresses, public IPv4 addresses, and Elastic IP addresses of your instances. You can also determine the public IPv4 and private IPv4 addresses of your instance from within your instance by using instance metadata. For more information, see Instance Metadata and User Data.

To determine your instance's private IPv4 addresses using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance. In the details pane, get the private IPv4 address from the Private IPs field, and get the internal DNS hostname from the Private DNS field.

(VPC only) If you have one or more secondary private IPv4 addresses assigned to network interfaces that are attached to your instance, get those IP addresses from the Secondary private IPs field.

(VPC only) Alternatively, in the navigation pane, choose Network Interfaces, and then select the network interface that's associated with your instance.

Get the primary private IP address from the Primary private IPv4 IP field, and the internal DNS hostname from the Private DNS (IPv4) field.

If you've assigned secondary private IP addresses to the network interface, get those IP addresses from the Secondary private IPv4 IPs field.

To determine your instance's public IPv4 addresses using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance. In the details pane, get the public IP address from the IPv4 Public IP field, and get the external DNS hostname from the Public DNS (IPv4) field.

If an Elastic IP address has been associated with the instance, get the Elastic IP address from the Elastic IPs field.

Note
If you've associated an Elastic IP address with your instance, the IPv4 Public IP field also displays the Elastic IP address.
(VPC only) Alternatively, in the navigation pane, choose Network Interfaces, and then select a network interface that's associated with your instance.

Get the public IP address from the IPv4 Public IP field. An asterisk (*) indicates the public IPv4 address or Elastic IP address that's mapped to the primary private IPv4 address.

Note
The public IPv4 address is displayed as a property of the network interface in the console, but it's mapped to the primary private IPv4 address through NAT. Therefore, if you inspect the properties of your network interface on your instance, for example, through ifconfig (Linux) or ipconfig (Windows), the public IPv4 address is not displayed. To determine your instance's public IPv4 address from within the instance, you can use instance metadata.
To determine your instance's IPv4 addresses using instance metadata

Connect to your instance.

Use the following command to access the private IP address:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/local-ipv4
Use the following command to access the public IP address:

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/public-ipv4
Note that if an Elastic IP address is associated with the instance, the value returned is that of the Elastic IP address.

Determining Your IPv6 Addresses

(VPC only) You can use the Amazon EC2 console to determine the IPv6 addresses of your instances.

To determine your instance's IPv6 addresses using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance. In the details pane, get the IPv6 addresses from IPv6 IPs.

To determine your instance's IPv6 addresses using instance metadata

Connect to your instance.

Use the following command to view the IPv6 address (you can get the MAC address from http://169.254.169.254/latest/meta-data/network/interfaces/macs/):

Copy
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/mac-address/ipv6s
Assigning a Public IPv4 Address During Instance Launch

If you launch an instance in EC2-Classic, it is assigned a public IPv4 address by default. You can't modify this behavior.

In a VPC, all subnets have an attribute that determines whether instances launched into that subnet are assigned a public IP address. By default, nondefault subnets have this attribute set to false, and default subnets have this attribute set to true. When you launch an instance, a public IPv4 addressing feature is also available for you to control whether your instance is assigned a public IPv4 address; you can override the default behavior of the subnet's IP addressing attribute. The public IPv4 address is assigned from Amazon's pool of public IPv4 addresses, and is assigned to the network interface with the device index of eth0. This feature depends on certain conditions at the time you launch your instance.

Important
You can't manually disassociate the public IP address from your instance after launch. Instead, it's automatically released in certain cases, after which you cannot reuse it. For more information, see Public IPv4 Addresses and External DNS Hostnames. If you require a persistent public IP address that you can associate or disassociate at will, assign an Elastic IP address to the instance after launch instead. For more information, see Elastic IP Addresses.
To access the public IP addressing feature when launching an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Launch Instance.

Select an AMI and an instance type, and then choose Next: Configure Instance Details.

On the Configure Instance Details page, for Network, select a VPC . The Auto-assign Public IP list is displayed. Choose Enable or Disable to override the default setting for the subnet.

Important
You cannot auto-assign a public IP address if you specify more than one network interface. Additionally, you cannot override the subnet setting using the auto-assign public IP feature if you specify an existing network interface for eth0.
Follow the steps on the next pages of the wizard to complete your instance's setup. For more information about the wizard configuration options, see Launching an Instance. On the final Review Instance Launch page, review your settings, and then choose Launch to choose a key pair and launch your instance.

On the Instances page, select your new instance and view its public IP address in IPv4 Public IP field in the details pane.

The public IP addressing feature is only available during launch. However, whether you assign a public IP address to your instance during launch or not, you can associate an Elastic IP address with your instance after it's launched. For more information, see Elastic IP Addresses. You can also modify your subnet's public IPv4 addressing behavior. For more information, see Modifying the Public IPv4 Addressing Attribute for Your Subnet.

To enable or disable the public IP addressing feature using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

Use the --associate-public-ip-address or the --no-associate-public-ip-address option with the run-instances command (AWS CLI)
Use the -AssociatePublicIp parameter with the New-EC2Instance command (AWS Tools for Windows PowerShell)
Assigning an IPv6 Address to an Instance

If your VPC and subnet have IPv6 CIDR blocks associated with them, you can assign an IPv6 address to your instance during or after launch. The IPv6 address is assigned from the IPv6 address range of the subnet, and is assigned to the network interface with the device index of eth0.

To assign an IPv6 address to an instance during launch

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Select an AMI, an instance type, and choose Next: Configure Instance Details.

Note
Ensure that you select an instance type that supports IPv6 addresses. For more information, see Instance Types.
On the Configure Instance Details page, for Network, select a VPC and for Subnet, select a subnet. For Auto-assign IPv6 IP, choose Enable.

Follow the remaining steps in the wizard to launch your instance.

Alternatively, you can assign an IPv6 address to your instance after launch.

To assign an IPv6 address to your instance after launch

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance, choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Assign new IP. You can specify an IPv6 address from the range of the subnet, or leave the Auto-assign value to let Amazon choose an IPv6 address for you.

Choose Save.

Note
If you launched your instance using Amazon Linux 2016.09.0 or later, or Windows Server 2008 R2 or later, your instance is configured for IPv6, and no additional steps are needed to ensure that the IPv6 address is recognized on the instance. If you launched your instance from an older AMI, you may have to configure your instance manually. For more information, see Configure IPv6 on Your Instances in the Amazon VPC User Guide.
To assign an IPv6 address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

Use the --ipv6-addresses option with the run-instances command (AWS CLI)
Use the Ipv6Addresses property for -NetworkInterface in the New-EC2Instance command (AWS Tools for Windows PowerShell)
assign-ipv6-addresses (AWS CLI)
Register-EC2Ipv6AddressList (AWS Tools for Windows PowerShell)
Unassigning an IPv6 Address From an Instance

You can unassign an IPv6 address from an instance using the Amazon EC2 console.

To unassign an IPv6 address from an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance, choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Unassign for the IPv6 address to unassign.

Choose Yes, Update.

To unassign an IPv6 address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

unassign-ipv6-addresses (AWS CLI)
Unregister-EC2Ipv6AddressList (AWS Tools for Windows PowerShell).

Multiple IP Addresses

In EC2-VPC, you can specify multiple private IPv4 and IPv6 addresses for your instances. The number of network interfaces and private IPv4 and IPv6 addresses that you can specify for an instance depends on the instance type. For more information, see IP Addresses Per Network Interface Per Instance Type.

It can be useful to assign multiple IP addresses to an instance in your VPC to do the following:

Host multiple websites on a single server by using multiple SSL certificates on a single server and associating each certificate with a specific IP address.
Operate network appliances, such as firewalls or load balancers, that have multiple IP addresses for each network interface.
Redirect internal traffic to a standby instance in case your instance fails, by reassigning the secondary IP address to the standby instance.
Contents

How Multiple IP Addresses Work
Working with Multiple IPv4 Addresses
Working with Multiple IPv6 Addresses
How Multiple IP Addresses Work

The following list explains how multiple IP addresses work with network interfaces:

You can assign a secondary private IPv4 address to any network interface. The network interface can be attached to or detached from the instance.
You can assign multiple IPv6 addresses to a network interface that's in a subnet that has an associated IPv6 CIDR block.
You must choose the secondary IPv4 from the IPv4 CIDR block range of the subnet for the network interface.
You must choose IPv6 addresses from the IPv6 CIDR block range of the subnet for the network interface.
Security groups apply to network interfaces, not to IP addresses. Therefore, IP addresses are subject to the security group of the network interface in which they're specified.
Multiple IP addresses can be assigned and unassigned to network interfaces attached to running or stopped instances.
Secondary private IPv4 addresses that are assigned to a network interface can be reassigned to another one if you explicitly allow it.
An IPv6 address cannot be reassigned to another network interface; you must first unassign the IPv6 address from the existing network interface.
When assigning multiple IP addresses to a network interface using the command line tools or API, the entire operation fails if one of the IP addresses can't be assigned.
Primary private IPv4 addresses, secondary private IPv4 addresses, Elastic IP addresses, and IPv6 addresses remain with the network interface when it is detached from an instance or attached to another instance.
Although you can't move the primary network interface from an instance, you can reassign the secondary private IPv4 address of the primary network interface to another network interface.
You can move any additional network interface from one instance to another.
The following list explains how multiple IP addresses work with Elastic IP addresses (IPv4 only):

Each private IPv4 address can be associated with a single Elastic IP address, and vice versa.
When a secondary private IPv4 address is reassigned to another interface, the secondary private IPv4 address retains its association with an Elastic IP address.
When a secondary private IPv4 address is unassigned from an interface, an associated Elastic IP address is automatically disassociated from the secondary private IPv4 address.
Working with Multiple IPv4 Addresses

You can assign a secondary private IPv4 address to an instance, associate an Elastic IPv4 address with a secondary private IPv4 address, and unassign a secondary private IPv4 address.

Contents

Assigning a Secondary Private IPv4 Address
Configuring the Operating System on Your Instance to Recognize the Secondary Private IPv4 Address
Associating an Elastic IP Address with the Secondary Private IPv4 Address
Viewing Your Secondary Private IPv4 Addresses
Unassigning a Secondary Private IPv4 Address
Assigning a Secondary Private IPv4 Address

You can assign the secondary private IPv4 address to the network interface for an instance as you launch the instance, or after the instance is running. This section includes the following procedures.

To assign a secondary private IPv4 address when launching an instance in EC2-VPC
To assign a secondary IPv4 address during launch using the command line
To assign a secondary private IPv4 address to a network interface
To assign a secondary private IPv4 to an existing instance using the command line
To assign a secondary private IPv4 address when launching an instance in EC2-VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Launch Instance.

Select an AMI, then choose an instance type and choose Next: Configure Instance Details.

On the Configure Instance Details page, for Network, select a VPC and for Subnet, select a subnet.

In the Network Interfaces section, do the following, and then choose Next: Add Storage:

To add another network interface, choose Add Device. The console enables you to specify up to two network interfaces when you launch an instance. After you launch the instance, choose Network Interfaces in the navigation pane to add additional network interfaces. The total number of network interfaces that you can attach varies by instance type. For more information, see IP Addresses Per Network Interface Per Instance Type.
Important
When you add a second network interface, the system can no longer auto-assign a public IPv4 address. You will not be able to connect to the instance over IPv4 unless you assign an Elastic IP address to the primary network interface (eth0). You can assign the Elastic IP address after you complete the Launch wizard. For more information, see Working with Elastic IP Addresses.
For each network interface, under Secondary IP addresses, choose Add IP, and then enter a private IP address from the subnet range, or accept the default Auto-assign value to let Amazon select an address.
On the next Add Storage page, you can specify volumes to attach to the instance besides the volumes specified by the AMI (such as the root device volume), and then choose Next: Add Tags.

On the Add Tags page, specify tags for the instance, such as a user-friendly name, and then choose Next: Configure Security Group.

On the Configure Security Group page, select an existing security group or create a new one. Choose Review and Launch.

On the Review Instance Launch page, review your settings, and then choose Launch to choose a key pair and launch your instance. If you're new to Amazon EC2 and haven't created any key pairs, the wizard prompts you to create one.

Important
After you have added a secondary private IP address to a network interface, you must connect to the instance and configure the secondary private IP address on the instance itself. For more information, see Configuring the Operating System on Your Instance to Recognize the Secondary Private IPv4 Address .
To assign a secondary IPv4 address during launch using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

The --secondary-private-ip-addresses option with the run-instances command (AWS CLI)
Define -NetworkInterface and specify the PrivateIpAddresses parameter with the New-EC2Instance command (AWS Tools for Windows PowerShell).
To assign a secondary private IPv4 address to a network interface

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces, and then select the network interface attached to the instance.

Choose Actions, Manage IP Addresses.

Under IPv4 Addresses, choose Assign new IP.

Enter a specific IPv4 address that's within the subnet range for the instance, or leave the field blank to let Amazon select an IP address for you.

(Optional) Choose Allow reassignment to allow the secondary private IP address to be reassigned if it is already assigned to another network interface.

Choose Yes, Update.

Alternatively, you can assign a secondary private IPv4 address to an instance. Choose Instances in the navigation pane, select the instance, and then choose Actions, Networking, Manage IP Addresses. You can configure the same information as you did in the steps above. The IP address is assigned to the primary network interface (eth0) for the instance.

To assign a secondary private IPv4 to an existing instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

assign-private-ip-addresses (AWS CLI)
Register-EC2PrivateIpAddress (AWS Tools for Windows PowerShell)
Configuring the Operating System on Your Instance to Recognize the Secondary Private IPv4 Address

After you assign a secondary private IPv4 address to your instance, you need to configure the operating system on your instance to recognize the secondary private IP address.

If you are using Amazon Linux, the ec2-net-utils package can take care of this step for you. It configures additional network interfaces that you attach while the instance is running, refreshes secondary IPv4 addresses during DHCP lease renewal, and updates the related routing rules. You can immediately refresh the list of interfaces by using the command sudo service network restart and then view the up-to-date list using ip addr li. If you require manual control over your network configuration, you can remove the ec2-net-utils package. For more information, see Configuring Your Network Interface Using ec2-net-utils.
If you are using another Linux distribution, see the documentation for your Linux distribution. Search for information about configuring additional network interfaces and secondary IPv4 addresses. If the instance has two or more interfaces on the same subnet, search for information about using routing rules to work around asymmetric routing.
For information about configuring a Windows instance, see Configuring a Secondary Private IP Address for Your Windows Instance in a VPC in the Amazon EC2 User Guide for Windows Instances.

Associating an Elastic IP Address with the Secondary Private IPv4 Address

To associate an Elastic IP address with a secondary private IPv4 address in EC2-VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Choose Actions, and then select Associate address.

For Network interface, select the network interface, and then select the secondary IP address from the Private IP list.

Choose Associate.

To associate an Elastic IP address with a secondary private IPv4 address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

associate-address (AWS CLI)
Register-EC2Address (AWS Tools for Windows PowerShell)
Viewing Your Secondary Private IPv4 Addresses

To view the private IPv4 addresses assigned to a network interface in EC2-VPC

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface with private IP addresses to view.

On the Details tab in the details pane, check the Primary private IPv4 IP and Secondary private IPv4 IPs fields for the primary private IPv4 address and any secondary private IPv4 addresses assigned to the network interface.

To view the private IPv4 addresses assigned to an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance with private IPv4 addresses to view.

On the Description tab in the details pane, check the Private IPs and Secondary private IPs fields for the primary private IPv4 address and any secondary private IPv4 addresses assigned to the instance through its network interface.

Unassigning a Secondary Private IPv4 Address

If you no longer require a secondary private IPv4 address, you can unassign it from the instance or the network interface. When a secondary private IPv4 address is unassigned from a network interface, the Elastic IP address (if it exists) is also disassociated.

To unassign a secondary private IPv4 address from an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select an instance, choose Actions, Networking, Manage IP Addresses.

Under IPv4 Addresses, choose Unassign for the IPv4 address to unassign.

Choose Yes, Update.

To unassign a secondary private IPv4 address from a network interface

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface, choose Actions, Manage IP Addresses.

Under IPv4 Addresses, choose Unassign for the IPv4 address to unassign.

Choose Yes, Update.

To unassign a secondary private IPv4 address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

unassign-private-ip-addresses (AWS CLI)
Unregister-EC2PrivateIpAddress (AWS Tools for Windows PowerShell)
Working with Multiple IPv6 Addresses

You can assign multiple IPv6 addresses to your instance, view the IPv6 addresses assigned to your instance, and unassign IPv6 addresses from your instance.

Contents

Assigning Multiple IPv6 Addresses
Viewing Your IPv6 Addresses
Unassigning an IPv6 Address
Assigning Multiple IPv6 Addresses

You can assign one or more IPv6 addresses to your instance during launch or after launch. To assign an IPv6 address to an instance, the VPC and subnet in which you launch the instance must have an associated IPv6 CIDR block. For more information, see VPCs and Subnets in the Amazon VPC User Guide.

To assign multiple IPv6 addresses during launch

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the dashboard, choose Launch Instance.

Select an AMI, choose an instance type, and choose Next: Configure Instance Details. Ensure that you choose an instance type that support IPv6. For more information, see Instance Types.

On the Configure Instance Details page, select a VPC from the Network list, and a subnet from the Subnet list.

In the Network Interfaces section, do the following, and then choose Next: Add Storage:

To assign a single IPv6 address to the primary network interface (eth0), under IPv6 IPs, choose Add IP. To add a secondary IPv6 address, choose Add IP again. You can enter an IPv6 address from the range of the subnet, or leave the default Auto-assign value to let Amazon choose an IPv6 address from the subnet for you.
Choose Add Device to add another network interface and repeat the steps above to add one or more IPv6 addresses to the network interface. The console enables you to specify up to two network interfaces when you launch an instance. After you launch the instance, choose Network Interfaces in the navigation pane to add additional network interfaces. The total number of network interfaces that you can attach varies by instance type. For more information, see IP Addresses Per Network Interface Per Instance Type.
Follow the next steps in the wizard to attach volumes and tag your instance.

On the Configure Security Group page, select an existing security group or create a new one. If you want your instance to be reachable over IPv6, ensure that your security group has rules that allow access from IPv6 addresses. For more information, see Security Group Rules Reference. Choose Review and Launch.

On the Review Instance Launch page, review your settings, and then choose Launch to choose a key pair and launch your instance. If you're new to Amazon EC2 and haven't created any key pairs, the wizard prompts you to create one.

You can use the Instances screen Amazon EC2 console to assign multiple IPv6 addresses to an existing instance. This assigns the IPv6 addresses to the primary network interface (eth0) for the instance. To assign a specific IPv6 address to the instance, ensure that the IPv6 address is not already assigned to another instance or network interface.

To assign multiple IPv6 addresses to an existing instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance, choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Assign new IP for each IPv6 address you want to add. You can specify an IPv6 address from the range of the subnet, or leave the Auto-assign value to let Amazon choose an IPv6 address for you.

Choose Yes, Update.

Alternatively, you can assign multiple IPv6 addresses to an existing network interface. The network interface must have been created in a subnet that has an associated IPv6 CIDR block. To assign a specific IPv6 address to the network interface, ensure that the IPv6 address is not already assigned to another network interface.

To assign multiple IPv6 addresses to a network interface

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select your network interface, choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Assign new IP for each IPv6 address you want to add. You can specify an IPv6 address from the range of the subnet, or leave the Auto-assign value to let Amazon choose an IPv6 address for you.

Choose Yes, Update.

CLI Overview

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

Assign an IPv6 address during launch:
Use the --ipv6-addresses or --ipv6-address-count options with the run-instances command (AWS CLI)
Define -NetworkInterface and specify the Ipv6Addresses or Ipv6AddressCount parameters with the New-EC2Instance command (AWS Tools for Windows PowerShell).
Assign an IPv6 address to a network interface:
assign-ipv6-addresses (AWS CLI)
Register-EC2Ipv6AddressList (AWS Tools for Windows PowerShell)
Viewing Your IPv6 Addresses

You can view the IPv6 addresses for an instance or for a network interface.

To view the IPv6 addresses assigned to an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance. In the details pane, review the IPv6 IPs field.

To view the IPv6 addresses assigned to a network interface

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select your network interface. In the details pane, review the IPv6 IPs field.

CLI Overview

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

View the IPv6 addresses for an instance:
describe-instances (AWS CLI)
Get-EC2Instance (AWS Tools for Windows PowerShell).
View the IPv6 addresses for a network interface:
describe-network-interfaces (AWS CLI)
Get-EC2NetworkInterface (AWS Tools for Windows PowerShell)
Unassigning an IPv6 Address

You can unassign an IPv6 address from the primary network interface of an instance, or you can unassign an IPv6 address from a network interface.

To unassign an IPv6 address from an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select your instance, choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Unassign for the IPv6 address to unassign.

Choose Yes, Update.

To unassign an IPv6 address from a network interface

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select your network interface, choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Unassign for the IPv6 address to unassign.

Choose Save.

CLI Overview

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

unassign-ipv6-addresses (AWS CLI)
Unregister-EC2Ipv6AddressList (AWS Tools for Windows PowerShell).

Elastic IP Addresses

An Elastic IP address is a static IPv4 address designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account. With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.

An Elastic IP address is a public IPv4 address, which is reachable from the Internet. If your instance does not have a public IPv4 address, you can associate an Elastic IP address with your instance to enable communication with the Internet; for example, to connect to your instance from your local computer.

We currently do not support Elastic IP addresses for IPv6.

Topics

Elastic IP Address Basics
Elastic IP Address Differences for EC2-Classic and EC2-VPC
Working with Elastic IP Addresses
Using Reverse DNS for Email Applications
Elastic IP Address Limit
Elastic IP Address Basics

The following are the basic characteristics of an Elastic IP address:

To use an Elastic IP address, you first allocate one to your account, and then associate it with your instance or a network interface.
When you associate an Elastic IP address with an instance or its primary network interface, the instance's public IPv4 address (if it had one) is released back into Amazon's pool of public IPv4 addresses. You cannot reuse a public IPv4 address. For more information, see Public IPv4 Addresses and External DNS Hostnames.
You can disassociate an Elastic IP address from a resource, and reassociate it with a different resource.
A disassociated Elastic IP address remains allocated to your account until you explicitly release it.
To ensure efficient use of Elastic IP addresses, we impose a small hourly charge if an Elastic IP address is not associated with a running instance, or if it is associated with a stopped instance or an unattached network interface. While your instance is running, you are not charged for one Elastic IP address associated with the instance, but you are charged for any additional Elastic IP addresses associated with the instance. For more information, see Amazon EC2 Pricing.
An Elastic IP address is for use in a specific region only.
When you associate an Elastic IP address with an instance that previously had a public IPv4 address, the public DNS hostname of the instance changes to match the Elastic IP address.
We resolve a public DNS hostname to the public IPv4 address or the Elastic IP address of the instance outside the network of the instance, and to the private IPv4 address of the instance from within the network of the instance.
If your account supports EC2-Classic, the use and behavior of Elastic IP addresses for EC2-Classic and EC2-VPC may differ. For more information, see Elastic IP Address Differences for EC2-Classic and EC2-VPC.

Elastic IP Address Differences for EC2-Classic and EC2-VPC

If your account supports EC2-Classic, there's one pool of Elastic IP addresses for use with the EC2-Classic platform and another for use with the EC2-VPC platform. You can't associate an Elastic IP address that you allocated for use with a VPC with an instance in EC2-Classic, and vice-versa. However, you can migrate an Elastic IP address you've allocated for use in the EC2-Classic platform to the EC2-VPC platform. You cannot migrate an Elastic IP address to another region. For more information about EC2-Classic and EC2-VPC, see Supported Platforms.

When you associate an Elastic IP address with an instance in EC2-Classic, a default VPC, or an instance in a nondefault VPC in which you assigned a public IPv4 to the eth0 network interface during launch, the instance's current public IPv4 address is released back into the public IP address pool. If you disassociate an Elastic IP address from the instance, the instance is automatically assigned a new public IPv4 address within a few minutes. However, if you have attached a second network interface to an instance in a VPC, the instance is not automatically assigned a new public IPv4 address. For more information about public IPv4 addresses, see Public IPv4 Addresses and External DNS Hostnames.

For information about using an Elastic IP address with an instance in a VPC, see Elastic IP Addresses in the Amazon VPC User Guide.

The following table lists the differences between Elastic IP addresses on EC2-Classic and EC2-VPC. For more information about the differences between private and public IP addresses, see IP Address Differences Between EC2-Classic and EC2-VPC.

Characteristic	EC2-Classic	EC2-VPC
Allocating an Elastic IP address
When you allocate an Elastic IP address, it's for use in EC2-Classic; however, you can migrate an Elastic IP address to the EC2-VPC platform. For more information, see Migrating an Elastic IP Address from EC2-Classic to EC2-VPC.
When you allocate an Elastic IP address, it's for use only in a VPC.
Associating an Elastic IP address
You associate an Elastic IP address with an instance.
An Elastic IP address is a property of a network interface. You can associate an Elastic IP address with an instance by updating the network interface attached to the instance. For more information, see Elastic Network Interfaces.
Reassociating an Elastic IP address
If you try to associate an Elastic IP address that's already associated with another instance, the address is automatically associated with the new instance.
If your account supports EC2-VPC only, and you try to associate an Elastic IP address that's already associated with another instance, the address is automatically associated with the new instance. If you're using a VPC in an EC2-Classic account, and you try to associate an Elastic IP address that's already associated with another instance, it succeeds only if you allowed reassociation.
Associating an Elastic IP address with a target that has an existing Elastic IP address	The existing Elastic IP address is disassociated from the instance, but remains allocated to your account.	If your account supports EC2-VPC only, the existing Elastic IP address is disassociated from the instance, but remains allocated to your account. If you're using a VPC in an EC2-Classic account, you cannot associate an Elastic IP address with a network interface or instance that has an existing Elastic IP address.
Stopping an instance
If you stop an instance, its Elastic IP address is disassociated, and you must reassociate the Elastic IP address when you restart the instance.
If you stop an instance, its Elastic IP address remains associated.
Assigning multiple IP addresses
Instances support only a single private IPv4 address and a corresponding Elastic IP address.
Instances support multiple IPv4 addresses, and each one can have a corresponding Elastic IP address. For more information, see Multiple IP Addresses.
Migrating an Elastic IP Address from EC2-Classic to EC2-VPC

If your account supports EC2-Classic, you can migrate Elastic IP addresses that you've allocated for use in the EC2-Classic platform to the EC2-VPC platform, within the same region. This can assist you to migrate your resources from EC2-Classic to a VPC; for example, you can launch new web servers in your VPC, and then use the same Elastic IP addresses that you used for your web servers in EC2-Classic for your new VPC web servers.

After you've migrated an Elastic IP address to EC2-VPC, you cannot use it in the EC2-Classic platform; however, if required, you can restore it to EC2-Classic. After you've restored an Elastic IP address to EC2-Classic, you cannot use it in EC2-VPC until you migrate it again. You can only migrate an Elastic IP address from EC2-Classic to EC2-VPC. You cannot migrate an Elastic IP address that was originally allocated for use in EC2-VPC to EC2-Classic.

To migrate an Elastic IP address, it must not be associated with an instance. For more information about disassociating an Elastic IP address from an instance, see Disassociating an Elastic IP Address and Reassociating it with a Different Instance.

You can migrate as many EC2-Classic Elastic IP addresses as you can have in your account. However, when you migrate an Elastic IP address to EC2-VPC, it counts against your Elastic IP address limit for EC2-VPC. You cannot migrate an Elastic IP address if it will result in you exceeding your limit. Similarly, when you restore an Elastic IP address to EC2-Classic, it counts against your Elastic IP address limit for EC2-Classic. For more information, see Elastic IP Address Limit.

You cannot migrate an Elastic IP address that has been allocated to your account for less than 24 hours.

For more information, see Moving an Elastic IP Address.

Working with Elastic IP Addresses

The following sections describe how you can work with Elastic IP addresses.

Tasks

Allocating an Elastic IP Address
Describing Your Elastic IP Addresses
Associating an Elastic IP Address with a Running Instance
Disassociating an Elastic IP Address and Reassociating it with a Different Instance
Moving an Elastic IP Address
Releasing an Elastic IP Address
Recovering an Elastic IP Address
Allocating an Elastic IP Address

You can allocate an Elastic IP address using the Amazon EC2 console or the command line. If your account supports EC2-Classic, you can allocate an address for use in EC2-Classic or in EC2-VPC.

To allocate an Elastic IP address for use in EC2-VPC using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Choose Allocate new address.

(EC2-Classic accounts) Choose VPC, and then choose Allocate. Close the confirmation screen.

(VPC-only accounts) Choose Allocate, and close the confirmation screen.

To allocate an Elastic IP address for use in EC2-Classic using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Choose Allocate new address.

Select Classic, and then choose Allocate. Close the confirmation screen.

To allocate an Elastic IP address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

allocate-address (AWS CLI)
New-EC2Address (AWS Tools for Windows PowerShell)
Describing Your Elastic IP Addresses

You can describe an Elastic IP address using the Amazon EC2 or the command line.

To describe your Elastic IP addresses using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Select a filter from the Resource Attribute list to begin searching. You can use multiple filters in a single search.

To describe your Elastic IP addresses using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-addresses (AWS CLI)
Get-EC2Address (AWS Tools for Windows PowerShell)
Associating an Elastic IP Address with a Running Instance

You can associate an Elastic IP address to an instance using the Amazon EC2 console or the command line.

(VPC only) If you're associating an Elastic IP address with your instance to enable communication with the Internet, you must also ensure that your instance is in a public subnet. For more information, see Internet Gateways in the Amazon VPC User Guide.

To associate an Elastic IP address with an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Select an Elastic IP address and choose Actions, Associate address.

Select the instance from Instance and then choose Associate.

To associate an Elastic IP address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

associate-address (AWS CLI)
Register-EC2Address (AWS Tools for Windows PowerShell)
Disassociating an Elastic IP Address and Reassociating it with a Different Instance

You can disassociate an Elastic IP address and then reassociate it using the Amazon EC2 console or the command line.

To disassociate and reassociate an Elastic IP address using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address, choose Actions, and then select Disassociate address.

Choose Disassociate address.

Select the address that you disassociated in the previous step. For Actions, choose Associate address.

Select the new instance from Instance, and then choose Associate.

To disassociate an Elastic IP address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

disassociate-address (AWS CLI)
Unregister-EC2Address (AWS Tools for Windows PowerShell)
To associate an Elastic IP address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

associate-address (AWS CLI)
Register-EC2Address (AWS Tools for Windows PowerShell)
Moving an Elastic IP Address

You can move an Elastic IP address from EC2-Classic to EC2-VPC using the Amazon EC2 console or the Amazon VPC console. This option is only available if your account supports EC2-Classic.

To move an Elastic IP address to EC2-VPC using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address, and choose Actions, Move to VPC scope.

In the confirmation dialog box, choose Move Elastic IP.

You can restore an Elastic IP address to EC2-Classic using the Amazon EC2 console or the Amazon VPC console.

To restore an Elastic IP address to EC2-Classic using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address, choose Actions, Restore to EC2 scope.

In the confirmation dialog box, choose Restore.

After you've performed the command to move or restore your Elastic IP address, the process of migrating the Elastic IP address can take a few minutes. Use the describe-moving-addresses command to check whether your Elastic IP address is still moving, or has completed moving.

After you've moved your Elastic IP address to EC2-VPC, you can view its allocation ID on the Elastic IPs page in the Allocation ID field.

If the Elastic IP address is in a moving state for longer than 5 minutes, contact https://aws.amazon.com/premiumsupport/.

To move an Elastic IP address using the Amazon EC2 Query API or AWS CLI

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

move-address-to-vpc (AWS CLI)
MoveAddressToVpc (Amazon EC2 Query API)
Move-EC2AddressToVpc (AWS Tools for Windows PowerShell)
To restore an Elastic IP address to EC2-Classic using the Amazon EC2 Query API or AWS CLI

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

restore-address-to-classic (AWS CLI)
RestoreAddressToClassic (Amazon EC2 Query API)
Restore-EC2AddressToClassic (AWS Tools for Windows PowerShell)
To describe the status of your moving addresses using the Amazon EC2 Query API or AWS CLI

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-moving-addresses (AWS CLI)
DescribeMovingAddresses (Amazon EC2 Query API)
Get-EC2Address (AWS Tools for Windows PowerShell)
To retrieve the allocation ID for your migrated Elastic IP address in EC2-VPC

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-addresses (AWS CLI)
DescribeAddresses (Amazon EC2 Query API)
Get-EC2Address (AWS Tools for Windows PowerShell)
Releasing an Elastic IP Address

If you no longer need an Elastic IP address, we recommend that you release it (the address must not be associated with an instance). You incur charges for any Elastic IP address that's allocated for use with EC2-Classic but not associated with an instance.

You can release an Elastic IP address using the Amazon EC2 console or the command line.

To release an Elastic IP address using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Elastic IPs.

Select the Elastic IP address, choose Actions, and then select Release addresses. Choose Release when prompted.

To release an Elastic IP address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

release-address (AWS CLI)
Remove-EC2Address (AWS Tools for Windows PowerShell)
Recovering an Elastic IP Address

If you have released your Elastic IP address, you might be able to recover it. The following rules apply:

You can only recover an Elastic IP address that was originally allocated for use in EC2-VPC, or that was moved from EC2-Classic to EC2-VPC.
You cannot recover an Elastic IP address if it has been allocated to another AWS account, or if it will result you in exceeding your Elastic IP address limit.
Currently, you can recover an Elastic IP address using the Amazon EC2 API or a command line tool only.

To recover an Elastic IP address using the command line

(AWS CLI) Use the allocate-address command and specify the IP address using the --address parameter.

Copy
aws ec2 allocate-address --domain vpc --address 203.0.113.3
(AWS Tools for Windows PowerShell) Use the New-EC2Address command and specify the IP address using the -Address parameter.

Copy
PS C:\> New-EC2Address -Address 203.0.113.3 -Domain vpc -Region us-east-1
Using Reverse DNS for Email Applications

If you intend to send email to third parties from an instance, we suggest you provision one or more Elastic IP addresses and provide them to us. AWS works with ISPs and Internet anti-spam organizations to reduce the chance that your email sent from these addresses will be flagged as spam.

In addition, assigning a static reverse DNS record to your Elastic IP address used to send email can help avoid having email flagged as spam by some anti-spam organizations. Note that a corresponding forward DNS record (record type A) pointing to your Elastic IP address must exist before we can create your reverse DNS record.

If a reverse DNS record is associated with an Elastic IP address, the Elastic IP address is locked to your account and cannot be released from your account until the record is removed.

To remove email sending limits, or to provide us with your Elastic IP addresses and reverse DNS records, go to the Request to Remove Email Sending Limitations page.

Elastic IP Address Limit

By default, all AWS accounts are limited to 5 Elastic IP addresses per region, because public (IPv4) Internet addresses are a scarce public resource. We strongly encourage you to use an Elastic IP address primarily for the ability to remap the address to another instance in the case of instance failure, and to use DNS hostnames for all other inter-node communication.

If you feel your architecture warrants additional Elastic IP addresses, please complete the Amazon EC2 Elastic IP Address Request Form. We will ask you to describe your use case so that we can understand your need for additional addresses.

Elastic Network Interfaces

An elastic network interface (referred to as a network interface in this documentation) is a virtual network interface that you can attach to an instance in a VPC. Network interfaces are available only for instances running in a VPC.

A network interface can include the following attributes:

A primary private IPv4 address
One or more secondary private IPv4 addresses
One Elastic IP address (IPv4) per private IPv4 address
One public IPv4 address
One or more IPv6 addresses
One or more security groups
A MAC address
A source/destination check flag
A description
You can create a network interface, attach it to an instance, detach it from an instance, and attach it to another instance. The attributes of a network interface follow it as it's attached or detached from an instance and reattached to another instance. When you move a network interface from one instance to another, network traffic is redirected to the new instance.

Every instance in a VPC has a default network interface, called the primary network interface (eth0). You cannot detach a primary network interface from an instance. You can create and attach additional network interfaces. The maximum number of network interfaces that you can use varies by instance type. For more information, see IP Addresses Per Network Interface Per Instance Type.

Private IPv4 addresses for network interfaces

The primary network interface for an instance is assigned a primary private IPv4 address from the IPv4 address range of your VPC. You can assign additional private IPv4 addresses to a network interface.

Public IPv4 addresses for network interfaces

In a VPC, all subnets have a modifiable attribute that determines whether network interfaces created in that subnet (and therefore instances launched into that subnet) are assigned a public IPv4 address. For more information, see IP Addressing Behavior for Your Subnet in the Amazon VPC User Guide. The public IPv4 address is assigned from Amazon's pool of public IPv4 addresses. When you launch an instance, the IP address is assigned to the primary network interface (eth0) that's created.

When you create a network interface, it inherits the public IPv4 addressing attribute from the subnet. If you later modify the public IPv4 addressing attribute of the subnet, the network interface keeps the setting that was in effect when it was created. If you launch an instance and specify an existing network interface for eth0, the public IPv4 addressing attribute is determined by the network interface.

For more information, see Public IPv4 Addresses and External DNS Hostnames.

IPv6 addresses for network interfaces

You can associate an IPv6 CIDR block with your VPC and subnet, and assign one or more IPv6 addresses from the subnet range to a network interface.

All subnets have a modifiable attribute that determines whether network interfaces created in that subnet (and therefore instances launched into that subnet) are automatically assigned an IPv6 address from the range of the subnet. For more information, see IP Addressing Behavior for Your Subnet in the Amazon VPC User Guide. When you launch an instance, the IPv6 address is assigned to the primary network interface (eth0) that's created.

For more information, see IPv6 Addresses.

Contents

IP Addresses Per Network Interface Per Instance Type
Scenarios for Network Interfaces
Best Practices for Configuring Network Interfaces
Configuring Your Network Interface Using ec2-net-utils
Working with Network Interfaces
IP Addresses Per Network Interface Per Instance Type

The following table lists the maximum number of network interfaces per instance type, and the maximum number of private IPv4 addresses and IPv6 addresses per network interface. The limit for IPv6 addresses is separate from the limit for private IPv4 addresses per network interface. Not all instance types support IPv6 addressing. Network interfaces, multiple private IPv4 addresses, and IPv6 addresses are only available for instances running in a VPC. For more information, see Multiple IP Addresses. For more information about IPv6 in VPC, see IP Addressing in Your VPC in the Amazon VPC User Guide.

Instance Type	Maximum Network Interfaces	IPv4 Addresses per Interface	IPv6 Addresses per Interface
c1.medium
2
6
IPv6 not supported
c1.xlarge
4
15
IPv6 not supported
c3.large
3
10
10
c3.xlarge
4
15
15
c3.2xlarge
4
15
15
c3.4xlarge
8
30
30
c3.8xlarge
8
30
30
c4.large
3
10
10
c4.xlarge
4
15
15
c4.2xlarge
4
15
15
c4.4xlarge
8
30
30
c4.8xlarge
8
30
30
cc2.8xlarge
8
30
IPv6 not supported
cg1.4xlarge
8
30
IPv6 not supported
cr1.8xlarge
8
30
IPv6 not supported
d2.xlarge
4
15
15
d2.2xlarge
4
15
15
d2.4xlarge
8
30
30
d2.8xlarge
8
30
30
f1.2xlarge	4	15	15
f1.16xlarge	8	50	50
g2.2xlarge
4
15
IPv6 not supported
g2.8xlarge
8
30
IPv6 not supported
g3.4xlarge	8	30	30
g3.8xlarge	8	30	30
g3.16xlarge	15	50	50
hi1.4xlarge
8
30
IPv6 not supported
hs1.8xlarge
8
30
IPv6 not supported
i2.xlarge
4
15
15
i2.2xlarge
4
15
15
i2.4xlarge
8
30
30
i2.8xlarge
8
30
30
i3.large
3
10
10
i3.xlarge
4
15
15
i3.2xlarge
4
15
15
i3.4xlarge
8
30
30
i3.8xlarge
8
30
30
i3.16xlarge
15
50
50
m1.small
2
4
IPv6 not supported
m1.medium
2
6
IPv6 not supported
m1.large
3
10
IPv6 not supported
m1.xlarge
4
15
IPv6 not supported
m2.xlarge
4
15
IPv6 not supported
m2.2xlarge
4
30
IPv6 not supported
m2.4xlarge
8
30
IPv6 not supported
m3.medium
2
6
IPv6 not supported
m3.large
3
10
IPv6 not supported
m3.xlarge
4
15
IPv6 not supported
m3.2xlarge
4
30
IPv6 not supported
m4.large	2	10	10
m4.xlarge	4	15	15
m4.2xlarge	4	15	15
m4.4xlarge	8	30	30
m4.10xlarge	8	30	30
m4.16xlarge	8	30	30
p2.xlarge	4	15	15
p2.8xlarge	8	30	30
p2.16xlarge	8	30	30
r3.large	3	10	10
r3.xlarge	4	15	15
r3.2xlarge	4	15	15
r3.4xlarge	8	30	30
r3.8xlarge	8	30	30
r4.large	3	10	10
r4.xlarge	4	15	15
r4.2xlarge	4	15	15
r4.4xlarge	8	30	30
r4.8xlarge	8	30	30
r4.16xlarge	15	50	50
t1.micro
2
2
IPv6 not supported
t2.nano
2
2
2
t2.micro
2
2
2
t2.small
2
4
4
t2.medium
3
6
6
t2.large
3
12
12
t2.xlarge
3
15
15
t2.2xlarge
3
15
15
x1.16xlarge	8	30	30
x1.32xlarge	8	30	30
Scenarios for Network Interfaces

Attaching multiple network interfaces to an instance is useful when you want to:

Create a management network.
Use network and security appliances in your VPC.
Create dual-homed instances with workloads/roles on distinct subnets.
Create a low-budget, high-availability solution.
Creating a Management Network

You can create a management network using network interfaces. In this scenario, the secondary network interface on the instance handles public-facing traffic and the primary network interface handles back-end management traffic and is connected to a separate subnet in your VPC that has more restrictive access controls. The public-facing interface, which may or may not be behind a load balancer, has an associated security group that allows access to the server from the Internet (for example, allow TCP port 80 and 443 from 0.0.0.0/0, or from the load balancer) while the private facing interface has an associated security group allowing SSH access only from an allowed range of IP addresses either within the VPC or from the Internet, a private subnet within the VPC or a virtual private gateway.

To ensure failover capabilities, consider using a secondary private IPv4 for incoming traffic on a network interface. In the event of an instance failure, you can move the interface and/or secondary private IPv4 address to a standby instance.


						Creating a Management Network
					
Use Network and Security Appliances in Your VPC

Some network and security appliances, such as load balancers, network address translation (NAT) servers, and proxy servers prefer to be configured with multiple network interfaces. You can create and attach secondary network interfaces to instances in a VPC that are running these types of applications and configure the additional interfaces with their own public and private IP addresses, security groups, and source/destination checking.

Creating Dual-homed Instances with Workloads/Roles on Distinct Subnets

You can place a network interface on each of your web servers that connects to a mid-tier network where an application server resides. The application server can also be dual-homed to a back-end network (subnet) where the database server resides. Instead of routing network packets through the dual-homed instances, each dual-homed instance receives and processes requests on the front end, initiates a connection to the back end, and then sends requests to the servers on the back-end network.

Create a Low Budget High Availability Solution

If one of your instances serving a particular function fails, its network interface can be attached to a replacement or hot standby instance pre-configured for the same role in order to rapidly recover the service. For example, you can use a network interface as your primary or secondary network interface to a critical service such as a database instance or a NAT instance. If the instance fails, you (or more likely, the code running on your behalf) can attach the network interface to a hot standby instance. Because the interface maintains its private IP addresses, Elastic IP addresses, and MAC address, network traffic begins flowing to the standby instance as soon as you attach the network interface to the replacement instance. Users experience a brief loss of connectivity between the time the instance fails and the time that the network interface is attached to the standby instance, but no changes to the VPC route table or your DNS server are required.

Best Practices for Configuring Network Interfaces

You can attach a network interface to an instance when it's running (hot attach), when it's stopped (warm attach), or when the instance is being launched (cold attach).
You can detach secondary (ethN) network interfaces when the instance is running or stopped. However, you can't detach the primary (eth0) interface.
You can attach a network interface in one subnet to an instance in another subnet in the same VPC; however, both the network interface and the instance must reside in the same Availability Zone.
When launching an instance from the CLI or API, you can specify the network interfaces to attach to the instance for both the primary (eth0) and additional network interfaces.
Launching an Amazon Linux or Windows Server instance with multiple network interfaces automatically configures interfaces, private IPv4 addresses, and route tables on the operating system of the instance.
A warm or hot attach of an additional network interface may require you to manually bring up the second interface, configure the private IPv4 address, and modify the route table accordingly. Instances running Amazon Linux or Windows Server automatically recognize the warm or hot attach and configure themselves.
Attaching another network interface to an instance (for example, a NIC teaming configuration) cannot be used as a method to increase or double the network bandwidth to or from the dual-homed instance.
If you attach two or more network interfaces from the same subnet to an instance, you may encounter networking issues such as asymmetric routing. If possible, use a secondary private IPv4 address on the primary network interface instead. For more information, see Assigning a Secondary Private IPv4 Address.
Configuring Your Network Interface Using ec2-net-utils

Amazon Linux AMIs may contain additional scripts installed by AWS, known as ec2-net-utils. These scripts optionally automate the configuration of your network interfaces. These scripts are available for Amazon Linux only.

Use the following command to install the package on Amazon Linux if it's not already installed, or update it if it's installed and additional updates are available:

Copy
$ yum install ec2-net-utils
The following components are part of ec2-net-utils:

udev rules (/etc/udev/rules.d)
Identifies network interfaces when they are attached, detached, or reattached to a running instance, and ensures that the hotplug script runs (53-ec2-network-interfaces.rules). Maps the MAC address to a device name (75-persistent-net-generator.rules, which generates 70-persistent-net.rules).

hotplug script
Generates an interface configuration file suitable for use with DHCP (/etc/sysconfig/network-scripts/ifcfg-ethN). Also generates a route configuration file (/etc/sysconfig/network-scripts/route-ethN).

DHCP script
Whenever the network interface receives a new DHCP lease, this script queries the instance metadata for Elastic IP addresses. For each Elastic IP address, it adds a rule to the routing policy database to ensure that outbound traffic from that address uses the correct network interface. It also adds each private IP address to the network interface as a secondary address.

ec2ifup ethN
Extends the functionality of the standard ifup. After this script rewrites the configuration files ifcfg-ethN and route-ethN, it runs ifup.

ec2ifdown ethN
Extends the functionality of the standard ifdown. After this script removes any rules for the network interface from the routing policy database, it runs ifdown.

ec2ifscan
Checks for network interfaces that have not been configured and configures them.

Note that this script isn't available in the initial release of ec2-net-utils.

To list any configuration files that were generated by ec2-net-utils, use the following command:

Copy
$ ls -l /etc/sysconfig/network-scripts/*-eth?
To disable the automation on a per-instance basis, you can add EC2SYNC=no to the corresponding ifcfg-ethN file. For example, use the following command to disable the automation for the eth1 interface:

Copy
$ sed -i -e 's/^EC2SYNC=yes/EC2SYNC=no/' /etc/sysconfig/network-scripts/ifcfg-eth1
If you want to disable the automation completely, you can remove the package using the following command:

Copy
$ yum remove ec2-net-utils
Working with Network Interfaces

You can work with network interfaces using the Amazon EC2 console.

Contents

Creating a Network Interface
Deleting a Network Interface
Viewing Details about a Network Interface
Monitoring IP Traffic
Attaching a Network Interface When Launching an Instance
Attaching a Network Interface to a Stopped or Running Instance
Detaching a Network Interface from an Instance
Changing the Security Group
Changing the Source/Destination Checking
Associating an Elastic IP Address (IPv4)
Disassociating an Elastic IP Address (IPv4)
Assigning an IPv6 Address
Unassigning an IPv6 Address
Changing Termination Behavior
Adding or Editing a Description
Adding or Editing Tags
Creating a Network Interface

You can create a network interface using the Amazon EC2 console or the command line.

To create a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Choose Create Network Interface.

For Description, enter a descriptive name.

For Subnet, select the subnet. Note that you can't move the network interface to another subnet after it's created, and you can only attach the interface to instances in the same Availability Zone.

For Private IP (or IPv4 Private IP), enter the primary private IPv4 address. If you don't specify an IPv4 address, we select an available private IPv4 address from within the selected subnet.

(IPv6 only) If you selected a subnet that has an associated IPv6 CIDR block, you can optionally specify an IPv6 address in the IPv6 IP field.

For Security groups, select one or more security groups.

Choose Yes, Create.

To create a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-network-interface (AWS CLI)
New-EC2NetworkInterface (AWS Tools for Windows PowerShell)
Deleting a Network Interface

You must first detach a network interface from an instance before you can delete it. Deleting a network interface releases all attributes associated with the interface and releases any private IP addresses or Elastic IP addresses to be used by another instance.

You can delete a network interface using the Amazon EC2 console or the command line.

To delete a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select a network interface and choose Delete.

In the Delete Network Interface dialog box, choose Yes, Delete.

To delete a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

delete-network-interface (AWS CLI)
Remove-EC2NetworkInterface (AWS Tools for Windows PowerShell)
Viewing Details about a Network Interface

You can describe a network interface using the Amazon EC2 console or the command line.

To describe a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface.

View the details on the Details tab.

To describe a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-network-interfaces (AWS CLI)
Get-EC2NetworkInterface (AWS Tools for Windows PowerShell)
To describe a network interface attribute using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

describe-network-interface-attribute (AWS CLI)
Get-EC2NetworkInterfaceAttribute (AWS Tools for Windows PowerShell)
Monitoring IP Traffic

You can enable a VPC flow log on your network interface to capture information about the IP traffic going to and from the interface. After you've created a flow log, you can view and retrieve its data in Amazon CloudWatch Logs.

For more information, see VPC Flow Logs in the Amazon VPC User Guide.

Attaching a Network Interface When Launching an Instance

You can specify an existing network interface or attach an additional network interface when you launch an instance. You can do this using the Amazon EC2 console or the command line.

Note
If an error occurs when attaching a network interface to your instance, this causes the instance launch to fail.
To attach a network interface when launching an instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Choose Launch Instance.

Select an AMI and instance type and choose Next: Configure Instance Details.

On the Configure Instance Details page, select a VPC for Network, and a subnet for Subnet.

In the Network Interfaces section, the console enables you to specify up to two network interfaces (new, existing, or a combination) when you launch an instance. You can also enter a primary IPv4 address and one or more secondary IPv4 addresses for any new interface.

You can add additional network interfaces to the instance after you launch it. The total number of network interfaces that you can attach varies by instance type. For more information, see IP Addresses Per Network Interface Per Instance Type.

Note
You cannot auto-assign a public IPv4 address to your instance if you specify more than one network interface.
(IPv6 only) If you're launching an instance into a subnet that has an associated IPv6 CIDR block, you can specify IPv6 addresses for any network interfaces that you attach. Under IPv6 IPs, choose Add IP. To add a secondary IPv6 address, choose Add IP again. You can enter an IPv6 address from the range of the subnet, or leave the default Auto-assign value to let Amazon choose an IPv6 address from the subnet for you.

Choose Next: Add Storage.

On the Add Storage page, you can specify volumes to attach to the instance besides the volumes specified by the AMI (such as the root device volume), and then choose Next: Add Tags.

On the Add Tags page, specify tags for the instance, such as a user-friendly name, and then choose Next: Configure Security Group.

On the Configure Security Group page, you can select a security group or create a new one. Choose Review and Launch.

Note
If you specified an existing network interface in step 5, the instance is associated with the security group for that network interface, regardless of any option you select in this step.
On the Review Instance Launch page, details about the primary and additional network interface are displayed. Review the settings, and then choose Launch to choose a key pair and launch your instance. If you're new to Amazon EC2 and haven't created any key pairs, the wizard prompts you to create one.

To attach a network interface when launching an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

run-instances (AWS CLI)
New-EC2Instance (AWS Tools for Windows PowerShell)
Attaching a Network Interface to a Stopped or Running Instance

You can attach a network interface to any of your stopped or running instances in your VPC using either the Instances or Network Interfaces page of the Amazon EC2 console, or using a command line interface.

Note
If the public IPv4 address on your instance is released, it does not receive a new one if there is more than one network interface attached to the instance. For more information about the behavior of public IPv4 addresses, see Public IPv4 Addresses and External DNS Hostnames.
To attach a network interface to an instance using the Instances page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Choose Actions, Networking, Attach Network Interface.

In the Attach Network Interface dialog box, select the network interface and choose Attach.

To attach a network interface to an instance using the Network Interfaces page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Attach.

In the Attach Network Interface dialog box, select the instance and choose Attach.

To attach a network interface to an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

attach-network-interface (AWS CLI)
Add-EC2NetworkInterface (AWS Tools for Windows PowerShell)
Detaching a Network Interface from an Instance

You can detach a secondary network interface at any time, using either the Instances or Network Interfaces page of the Amazon EC2 console, or using a command line interface.

To detach a network interface from an instance using the Instances page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Choose Actions, Networking, Detach Network Interface.

In the Detach Network Interface dialog box, select the network interface and choose Detach.

To detach a network interface from an instance using the Network Interfaces page

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Detach.

In the Detach Network Interface dialog box, choose Yes, Detach. If the network interface fails to detach from the instance, choose Force detachment, and then try again.

To detach a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

detach-network-interface (AWS CLI)
Dismount-EC2NetworkInterface (AWS Tools for Windows PowerShell)
Changing the Security Group

You can change the security groups that are associated with a network interface. When you create the security group, be sure to specify the same VPC as the subnet for the interface.

You can change the security group for your network interfaces using the Amazon EC2 console or the command line.

Note
To change security group membership for interfaces owned by other services, such as Elastic Load Balancing, use the console or command line interface for that service.
To change the security group of a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Actions, Change Security Groups.

In the Change Security Groups dialog box, select the security groups to use, and choose Save.

To change the security group of a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-network-interface-attribute (AWS CLI)
Edit-EC2NetworkInterfaceAttribute (AWS Tools for Windows PowerShell)
Changing the Source/Destination Checking

The Source/Destination Check attribute controls whether source/destination checking is enabled on the instance. Disabling this attribute enables an instance to handle network traffic that isn't specifically destined for the instance. For example, instances running services such as network address translation, routing, or a firewall should set this value to disabled. The default value is enabled.

You can change source/destination checking using the Amazon EC2 console or the command line.

To change source/destination checking for a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Actions, Change Source/Dest Check.

In the dialog box, choose Enabled (if enabling) or Disabled (if disabling), and Save.

To change source/destination checking for a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-network-interface-attribute (AWS CLI)
Edit-EC2NetworkInterfaceAttribute (AWS Tools for Windows PowerShell)
Associating an Elastic IP Address (IPv4)

If you have an Elastic IP address (IPv4), you can associate it with one of the private IPv4 addresses for the network interface. You can associate one Elastic IP address with each private IPv4 address.

You can associate an Elastic IP address using the Amazon EC2 console or the command line.

To associate an Elastic IP address using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Actions, Associate Address.

In the Associate Elastic IP Address dialog box, select the Elastic IP address from the Address list.

For Associate to private IP address, select the private IPv4 address to associate with the Elastic IP address.

Choose Allow reassociation to allow the Elastic IP address to be associated with the specified network interface if it's currently associated with another instance or network interface, and then choose Associate Address.

To associate an Elastic IP address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

associate-address (AWS CLI)
Register-EC2Address (AWS Tools for Windows PowerShell)
Disassociating an Elastic IP Address (IPv4)

If the network interface has an Elastic IP address (IPv4) associated with it, you can disassociate the address, and then either associate it with another network interface or release it back to the address pool. Note that this is the only way to associate an Elastic IP address with an instance in a different subnet or VPC using a network interface, as network interfaces are specific to a particular subnet.

You can disassociate an Elastic IP address using the Amazon EC2 console or the command line.

To disassociate an Elastic IP address using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Actions, Disassociate Address.

In the Disassociate IP Address dialog box, choose Yes, Disassociate.

To disassociate an Elastic IP address using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

disassociate-address (AWS CLI)
Unregister-EC2Address (AWS Tools for Windows PowerShell)
Assigning an IPv6 Address

You can assign one or more IPv6 addresses to a network interface. The network interface must be in a subnet that has an associated IPv6 CIDR block. To assign a specific IPv6 address to the network interface, ensure that the IPv6 address is not already assigned to another network interface.

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces and select the network interface.

Choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Assign new IP. Specify an IPv6 address from the range of the subnet, or leave the Auto-assign value to let Amazon choose one for you.

Choose Yes, Update.

To assign an IPv6 address to a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

assign-ipv6-addresses (AWS CLI)
Register-EC2Ipv6AddressList (AWS Tools for Windows PowerShell)
Unassigning an IPv6 Address

You can unassign an IPv6 address from a network interface using the Amazon EC2 console.

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces and select the network interface.

Choose Actions, Manage IP Addresses.

Under IPv6 Addresses, choose Unassign for the IPv6 address to remove.

Choose Yes, Update.

To unassign an IPv6 address from a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

unassign-ipv6-addresses (AWS CLI)
Unregister-EC2Ipv6AddressList (AWS Tools for Windows PowerShell)
Changing Termination Behavior

You can set the termination behavior for a network interface that's attached to an instance. You can specify whether the network interface should be automatically deleted when you terminate the instance to which it's attached.

You can change the terminating behavior for a network interface using the Amazon EC2 console or the command line.

To change the termination behavior for a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Actions, Change Termination Behavior.

In the Change Termination Behavior dialog box, select the Delete on termination check box if you want the network interface to be deleted when you terminate an instance.

To change the termination behavior for a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-network-interface-attribute (AWS CLI)
Edit-EC2NetworkInterfaceAttribute (AWS Tools for Windows PowerShell)
Adding or Editing a Description

You can change the description for a network interface using the Amazon EC2 console or the command line.

To change the description for a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface and choose Actions, Change Description.

In the Change Description dialog box, enter a description for the network interface, and then choose Save.

To change the description for a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

modify-network-interface-attribute (AWS CLI)
Edit-EC2NetworkInterfaceAttribute (AWS Tools for Windows PowerShell)
Adding or Editing Tags

Tags are metadata that you can add to a network interface. Tags are private and are only visible to your account. Each tag consists of a key and an optional value. For more information about tags, see Tagging Your Amazon EC2 Resources.

You can tag a resource using the Amazon EC2 console or the command line.

To add or edit tags for a network interface using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Network Interfaces.

Select the network interface.

In the details pane, choose Tags, Add/Edit Tags.

In the Add/Edit Tags dialog box, choose Create Tag for each tag to create, and enter a key and optional value. When you're done, choose Save.

To add or edit tags for a network interface using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

create-tags (AWS CLI)
New-EC2Tag (AWS Tools for Windows PowerShell)

Placement Groups

A placement group is a logical grouping of instances within a single Availability Zone. Placement groups are recommended for applications that benefit from low network latency, high network throughput, or both. To provide the lowest latency, and the highest packet-per-second network performance for your placement group, choose an instance type that supports enhanced networking. For more information, see Enhanced Networking.

First, you create a placement group and then you launch multiple instances into the placement group. We recommend that you launch the number of instances that you need in the placement group in a single launch request and that you use the same instance type for all instances in the placement group. If you try to add more instances to the placement group later, or if you try to launch more than one instance type in the placement group, you increase your chances of getting an insufficient capacity error.

There is no charge for creating a placement group.

If you stop an instance in a placement group and then start it again, it still runs in the placement group. However, the start fails if there isn't enough capacity for the instance.

If you receive a capacity error when launching an instance in a placement group that already has running instances, stop and start all of the instances in the placement group, and try the launch again. Restarting the instances may migrate them to hardware that has capacity for all the requested instances.

Contents

Placement Group Limitations
Launching Instances into a Placement Group
Deleting a Placement Group
Placement Group Limitations

Placement groups have the following limitations:

A placement group can't span multiple Availability Zones.
The name you specify for a placement group must be unique within your AWS account.
The following are the only instance types that you can use when you launch an instance into a placement group:
General purpose: m4.large | m4.xlarge | m4.2xlarge | m4.4xlarge | m4.10xlarge | m4.16xlarge
Compute optimized: c4.large | c4.xlarge | c4.2xlarge | c4.4xlarge | c4.8xlarge | c3.large | c3.xlarge | c3.2xlarge | c3.4xlarge | c3.8xlarge | cc2.8xlarge
Memory optimized: cr1.8xlarge | r3.large | r3.xlarge | r3.2xlarge | r3.4xlarge | r3.8xlarge | r4.large | r4.xlarge | r4.2xlarge | r4.4xlarge | r4.8xlarge | r4.16xlarge | x1.16xlarge | x1.32xlarge
Storage optimized: d2.xlarge | d2.2xlarge | d2.4xlarge | d2.8xlarge | hi1.4xlarge | hs1.8xlarge | i2.xlarge | i2.2xlarge | i2.4xlarge | i2.8xlarge | i3.large | i3.xlarge | i3.2xlarge | i3.4xlarge | i3.8xlarge | i3.16xlarge
Accelerated computing: cg1.4xlarge | f1.2xlarge | f1.16xlarge | g2.2xlarge | g2.8xlarge | g3.4xlarge | g3.8xlarge | g3.16xlarge | p2.xlarge | p2.8xlarge | p2.16xlarge
The maximum network throughput speed of traffic between two instances in a placement group is limited by the slower of the two instances. For applications with high-throughput requirements, choose an instance type with 10 Gbps or 20 Gbps network connectivity. For more information about instance type network performance, see the Amazon EC2 Instance Types Matrix.
Although launching multiple instance types into a placement group is possible, this reduces the likelihood that the required capacity will be available for your launch to succeed. We recommend using the same instance type for all instances in a placement group.
You can't merge placement groups. Instead, you must terminate the instances in one placement group, and then relaunch those instances into the other placement group.
A placement group can span peered VPCs; however, you will not get full-bisection bandwidth between instances in peered VPCs. For more information about VPC peering connections, see the Amazon VPC Peering Guide.
You can't move an existing instance into a placement group. You can create an AMI from your existing instance, and then launch a new instance from the AMI into a placement group.
Reserved Instances provide a capacity reservation for EC2 instances in an Availability Zone. The capacity reservation can be used by instances in a placement group that are assigned to the same Availability Zone. However, it is not possible to explicitly reserve capacity for a placement group.
To ensure that network traffic remains within the placement group, members of the placement group must address each other via their private IPv4 addresses or IPv6 addresses (if applicable). If members address each other using their public IPv4 addresses, throughput drops to 5 Gbps or less.
Network traffic to and from resources outside the placement group is limited to 5 Gbps.
Launching Instances into a Placement Group

We suggest that you create an AMI specifically for the instances that you'll launch into a placement group.

To launch instances into a placement group using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Create an AMI for your instances.

From the Amazon EC2 dashboard, choose Launch Instance. After you complete the wizard, choose Launch.

Connect to your instance. (For more information, see Connect to Your Linux Instance.)

Install software and applications on the instance, copy data, or attach additional Amazon EBS volumes.

(Optional) If your instance type supports enhanced networking, ensure that this feature is enabled by following the procedures in Enhanced Networking on Linux.

In the navigation pane, choose Instances, select your instance, choose Actions, Image, Create Image. Provide the information requested by the Create Image dialog box, and then choose Create Image.

(Optional) You can terminate this instance if you have no further use for it.

Create a placement group.

In the navigation pane, choose Placement Groups.

Choose Create Placement Group.

In the Create Placement Group dialog box, provide a name for the placement group that is unique in the AWS account you're using, and then choose Create.

When the status of the placement group is available, you can launch instances into the placement group.

Launch instances into your placement group.

In the navigation pane, choose Instances.

Choose Launch Instance. Complete the wizard as directed, taking care to do the following:

On the Choose an Amazon Machine Image (AMI) page, select the My AMIs tab, and then select the AMI that you created.
On the Choose an Instance Type page, select an instance type that can be launched into a placement group.
On the Configure Instance Details page, enter the total number of instances that you'll need in this placement group, as you might not be able to add instances to the placement group later on.
On the Configure Instance Details page, select the placement group that you created from Placement group. If you do not see the Placement group list on this page, verify that you have selected an instance type that can be launched into a placement group, as this option is not available otherwise.
To launch instances into a placement group using the command line

Create an AMI for your instances using one of the following commands:

create-image (AWS CLI)
New-EC2Image (AWS Tools for Windows PowerShell)
Create a placement group using one of the following commands:

create-placement-group (AWS CLI)
New-EC2PlacementGroup (AWS Tools for Windows PowerShell)
Launch instances into your placement group using one of the following options:

--placement with run-instances (AWS CLI)
-PlacementGroup with New-EC2Instance (AWS Tools for Windows PowerShell)
Deleting a Placement Group

You can delete a placement group if you need to replace it or no longer need a placement group. Before you can delete your placement group, you must terminate all instances that you launched into the placement group.

To delete a placement group using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select and terminate all instances in the placement group. (You can verify that the instance is in a placement group before you terminate it by checking the value of Placement Group in the details pane.)

In the navigation pane, choose Placement Groups.

Select the placement group, and then choose Delete Placement Group.

When prompted for confirmation, choose Yes, Delete.

To delete a placement group using the command line

You can use one of the following sets of commands. For more information about these command line interfaces, see Accessing Amazon EC2.

terminate-instances and delete-placement-group (AWS CLI)
Stop-EC2Instance and Remove-EC2PlacementGroup(AWS Tools for Windows PowerShell)

Network Maximum Transmission Unit (MTU) for Your EC2 Instance

The maximum transmission unit (MTU) of a network connection is the size, in bytes, of the largest permissible packet that can be passed over the connection. The larger the MTU of a connection, the more data that can be passed in a single packet. Ethernet packets consist of the frame, or the actual data you are sending, and the network overhead information that surrounds it.

Ethernet frames can come in different formats, and the most common format is the standard Ethernet v2 frame format. It supports 1500 MTU, which is the largest Ethernet packet size supported over most of the Internet. The maximum supported MTU for an instance depends on its instance type. All Amazon EC2 instance types support 1500 MTU, and many current instance sizes support 9001 MTU, or jumbo frames.

Contents

Jumbo Frames (9001 MTU)
Path MTU Discovery
Check the Path MTU Between Two Hosts
Check and Set the MTU on your Amazon EC2 Instance
Troubleshooting
Jumbo Frames (9001 MTU)

Jumbo frames allow more than 1500 bytes of data by increasing the payload size per packet, and thus increasing the percentage of the packet that is not packet overhead. Fewer packets are needed to send the same amount of usable data. However, outside of a given AWS region (EC2-Classic), a single VPC, or a VPC peering connection, you will experience a maximum path of 1500 MTU. VPN connections and traffic sent over an Internet gateway are limited to 1500 MTU. If packets are over 1500 bytes, they are fragmented, or they are dropped if the Don't Fragment flag is set in the IP header.

Jumbo frames should be used with caution for Internet-bound traffic or any traffic that leaves a VPC. Packets are fragmented by intermediate systems, which slows down this traffic. To use jumbo frames inside a VPC and not slow traffic that's bound for outside the VPC, you can configure the MTU size by route, or use multiple elastic network interfaces with different MTU sizes and different routes.

For instances that are collocated inside a placement group, jumbo frames help to achieve the maximum network throughput possible, and they are recommended in this case. For more information, see Placement Groups.

The following instances support jumbo frames:

Compute optimized: C3, C4, CC2
General purpose: M3, M4, T2
Accelerated computing: CG1, F1, G2, G3, P2
Memory optimized: CR1, R3, R4, X1
Storage optimized: D2, HI1, HS1, I2, I3
Path MTU Discovery

Path MTU Discovery is used to determine the path MTU between two devices. The path MTU is the maximum packet size that's supported on the path between the originating host and the receiving host. If a host sends a packet that's larger than the MTU of the receiving host or that's larger than the MTU of a device along the path, the receiving host or device returns the following ICMP message: Destination Unreachable: Fragmentation Needed and Don't Fragment was Set (Type 3, Code 4). This instructs the original host to adjust the MTU until the packet can be transmitted.

By default, security groups do not allow any inbound ICMP traffic. To ensure that your instance can receive this message and the packet does not get dropped, you must add a Custom ICMP Rule with the Destination Unreachable protocol to the inbound security group rules for your instance. For more information, see Path MTU Discovery.

Important
Modifying your instance's security group to allow path MTU discovery does not guarantee that jumbo frames will not be dropped by some routers. An Internet gateway in your VPC will forward packets up to 1500 bytes only. 1500 MTU packets are recommended for Internet traffic.
Check the Path MTU Between Two Hosts

You can check the path MTU between two hosts using the tracepath command, which is part of the iputils package that is available by default on many Linux distributions, including Amazon Linux.

To check path MTU with tracepath

Use the following command to check the path MTU between your Amazon EC2 instance and another host. You can use a DNS name or an IP address as the destination; this example checks the path MTU between an EC2 instance and amazon.com.

Copy
[ec2-user ~]$ tracepath amazon.com
 1?: [LOCALHOST]     pmtu 9001
 1:  ip-172-31-16-1.us-west-1.compute.internal (172.31.16.1)   0.187ms pmtu 1500
 1:  no reply
 2:  no reply
 3:  no reply
 4:  100.64.16.241 (100.64.16.241)                          0.574ms
 5:  72.21.222.221 (72.21.222.221)                         84.447ms asymm 21
 6:  205.251.229.97 (205.251.229.97)                       79.970ms asymm 19
 7:  72.21.222.194 (72.21.222.194)                         96.546ms asymm 16
 8:  72.21.222.239 (72.21.222.239)                         79.244ms asymm 15
 9:  205.251.225.73 (205.251.225.73)                       91.867ms asymm 16
...
31:  no reply
     Too many hops: pmtu 1500
     Resume: pmtu 1500
In this example, the path MTU is 1500.

Note
If you're using tracepath to another Amazon EC2 instance, you may need to check that the instance's security group rules allow inbound UDP traffic.
Check and Set the MTU on your Amazon EC2 Instance

Some instances are configured to use jumbo frames, and others are configured to use standard frame sizes. You may want to use jumbo frames for network traffic within your VPC or you may want to use standard frames for Internet traffic. Whatever your use case, we recommend verifying that your instance will behave the way you expect it to. You can use the procedures in this section to check your network interface's MTU setting and modify it if needed.

To check the MTU setting on a Linux instance

You can check the current MTU value using the following ip command. Note that in the example output, mtu 9001 indicates that this instance uses jumbo frames.

Copy
[ec2-user ~]$ ip link show eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether 02:90:c0:b7:9e:d1 brd ff:ff:ff:ff:ff:ff
To set the MTU value on a Linux instance

You can set the MTU value using the ip command. The following command sets the desired MTU value to 1500, but you could use 9001 instead.

Copy
[ec2-user ~]$ sudo ip link set dev eth0 mtu 1500
(Optional) To persist your network MTU setting after a reboot, modify the following configuration files, based on your operating system type.

For Amazon Linux, add the following lines to your /etc/dhcp/dhclient-eth0.conf file.

Copy
interface "eth0" {
supersede interface-mtu 1500;
}
For Ubuntu, add the following line to /etc/network/interfaces.d/eth0.cfg.

Copy
post-up /sbin/ifconfig eth0 mtu 1500
For other Linux distributions, consult their specific documentation.

(Optional) Reboot your instance and verify that the MTU setting is correct.

Troubleshooting

If you experience connectivity issues between your EC2 instance and an Amazon Redshift cluster when using jumbo frames, see Queries Appear to Hang in the Amazon Redshift Cluster Management Guide

Enhanced Networking on Linux

Enhanced networking uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on supported instance types. SR-IOV is a method of device virtualization that provides higher I/O performance and lower CPU utilization when compared to traditional virtualized network interfaces. Enhanced networking provides higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies. There is no additional charge for using enhanced networking.

Contents

Enhanced Networking Types
Enabling Enhanced Networking on Your Instance
Enabling Enhanced Networking with the Intel 82599 VF Interface on Linux Instances in a VPC
Enabling Enhanced Networking with the Elastic Network Adapter (ENA) on Linux Instances in a VPC
Troubleshooting the Elastic Network Adapter (ENA)
Enhanced Networking Types

Depending on your instance type, enhanced networking can be enabled using one of the following mechanisms:

Intel 82599 Virtual Function (VF) interface
The Intel 82599 Virtual Function interface supports network speeds of up to 10 Gbps for supported instance types.

C3, C4, D2, I2, R3, and M4 (excluding m4.16xlarge) instances use the Intel 82599 VF interface for enhanced networking. To find out which instance types support 10 Gbps network speeds, see the Instance Type Matrix.

Elastic Network Adapter (ENA)
The Elastic Network Adapter (ENA) supports network speeds of up to 20 Gbps for supported instance types.

F1, G3, I3, P2, R4, X1, and m4.16xlarge instances use the Elastic Network Adapter for enhanced networking. To find out which instance types support 20 Gbps network speeds, see the Instance Type Matrix.

Enabling Enhanced Networking on Your Instance

If your instance type supports the Intel 82599 VF interface for enhanced networking, follow the procedures in Enabling Enhanced Networking with the Intel 82599 VF Interface on Linux Instances in a VPC.

If your instance type supports the Elastic Network Adapter for enhanced networking, follow the procedures in Enabling Enhanced Networking with the Elastic Network Adapter (ENA) on Linux Instances in a VPC.

Enabling Enhanced Networking with the Intel 82599 VF Interface on Linux Instances in a VPC

Amazon EC2 provides enhanced networking capabilities to C3, C4, D2, I2, R3, and M4 (excluding m4.16xlarge) instances with the Intel 82599 VF interface, which uses the Intel ixgbevf driver.

To prepare for enhanced networking with the Intel 82599 VF interface, set up your instance as follows:

Launch the instance from an HVM AMI using Linux kernel version of 2.6.32 or later. The latest Amazon Linux HVM AMIs have the modules required for enhanced networking installed and have the required attributes set. Therefore, if you launch an Amazon EBS–backed, enhanced networking–supported instance using a current Amazon Linux HVM AMI, enhanced networking is already enabled for your instance.
Warning
Enhanced networking is supported only for HVM instances. Enabling enhanced networking with a PV instance can make it unreachable. Setting this attribute without the proper module or module version can also make your instance unreachable.
Launch the instance in a VPC. (You can't enable enhanced networking if the instance is in EC2-Classic.)
Install and configure the AWS CLI or the AWS Tools for Windows PowerShell on any computer you choose, preferably your local desktop or laptop. For more information, see Accessing Amazon EC2. Enhanced networking cannot be managed from the Amazon EC2 console.
If you have important data on the instance that you want to preserve, you should back that data up now by creating an AMI from your instance. Updating kernels and kernel modules, as well as enabling the sriovNetSupport attribute, may render incompatible instances or operating systems unreachable; if you have a recent backup, your data will still be retained if this happens.
Contents

Testing Whether Enhanced Networking with the Intel 82599 VF Interface is Enabled
Enabling Enhanced Networking with the Intel 82599 VF Interface on Amazon Linux
Enabling Enhanced Networking with the Intel 82599 VF Interface on Ubuntu
Enabling Enhanced Networking with the Intel 82599 VF Interface on Other Linux Distributions
Troubleshooting Connectivity Issues
Testing Whether Enhanced Networking with the Intel 82599 VF Interface is Enabled

To test whether enhanced networking with the Intel 82599 VF interface is already enabled, verify that the ixgbevf module is installed on your instance and that the sriovNetSupport attribute is set. If your instance satisfies these two conditions, then the ethtool -i ethn command should show that the module is in use on the network interface.

Kernel Module (ixgbevf)

To verify that the ixgbevf module is installed and that the version is compatible with enhanced networking, use the modinfo command as follows:

Copy
[ec2-user ~]$ modinfo ixgbevf
filename:       /lib/modules/3.10.48-55.140.amzn1.x86_64/kernel/drivers/amazon/ixgbevf/ixgbevf.ko
version:        2.14.2
license:        GPL
description:    Intel(R) 82599 Virtual Function Driver
author:         Intel Corporation, <linux.nics@intel.com>
srcversion:     50CBF6F36B99FE70E56C95A
alias:          pci:v00008086d00001515sv*sd*bc*sc*i*
alias:          pci:v00008086d000010EDsv*sd*bc*sc*i*
depends:
intree:         Y
vermagic:       3.10.48-55.140.amzn1.x86_64 SMP mod_unload modversions
parm:           InterruptThrottleRate:Maximum interrupts per second, per vector, (956-488281, 0=off, 1=dynamic), default 1 (array of int)
In the above Amazon Linux case, the ixgbevf module is already installed and it is at the minimum recommended version (2.14.2).

Copy
ubuntu:~$ modinfo ixgbevf
filename:       /lib/modules/3.13.0-29-generic/kernel/drivers/net/ethernet/intel/ixgbevf/ixgbevf.ko
version:        2.11.3-k
license:        GPL
description:    Intel(R) 82599 Virtual Function Driver
author:         Intel Corporation, <linux.nics@intel.com>
srcversion:     0816EA811025C8062A9C269
alias:          pci:v00008086d00001515sv*sd*bc*sc*i*
alias:          pci:v00008086d000010EDsv*sd*bc*sc*i*
depends:
intree:         Y
vermagic:       3.13.0-29-generic SMP mod_unload modversions
signer:         Magrathea: Glacier signing key
sig_key:        66:02:CB:36:F1:31:3B:EA:01:C4:BD:A9:65:67:CF:A7:23:C9:70:D8
sig_hashalgo:   sha512
parm:           debug:Debug level (0=none,...,16=all) (int)
In the above Ubuntu instance, the module is installed, but the version is 2.11.3-k, which does not have all of the latest bug fixes that the recommended version 2.14.2 does. In this case, the ixgbevf module would work, but a newer version can still be installed and loaded on the instance for the best experience.

Instance Attribute (sriovNetSupport)

To check whether an instance has the enhanced networking sriovNetSupport attribute set, use one of the following commands:

describe-instance-attribute (AWS CLI)
Copy
aws ec2 describe-instance-attribute --instance-id instance_id --attribute sriovNetSupport
Get-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Copy
Get-EC2InstanceAttribute -InstanceId instance-id -Attribute sriovNetSupport
If the attribute isn't set, SriovNetSupport is empty; otherwise, it is set as follows:

"SriovNetSupport": {
    "Value": "simple"
},
Image Attribute (sriovNetSupport)

To check whether an AMI already has the enhanced networking sriovNetSupport attribute set, use one of the following commands:

describe-image-attribute (AWS CLI)
Copy
aws ec2 describe-image-attribute --image-id ami_id --attribute sriovNetSupport
Note that this command only works for images that you own. You receive an AuthFailure error for images that do not belong to your account.
Get-EC2ImageAttribute (AWS Tools for Windows PowerShell)
Copy
Get-EC2ImageAttribute -ImageId ami-id -Attribute sriovNetSupport
If the attribute isn't set, SriovNetSupport is empty; otherwise, it is set as follows:

"SriovNetSupport": {
    "Value": "simple"
},
Network Interface Driver

Use the following command to verify that the module is being used on a particular interface, substituting the interface name that you wish to check. If you are using a single interface (default), it will be eth0.

Copy
[ec2-user ~]$ ethtool -i eth0
driver: vif
version:
firmware-version:
bus-info: vif-0
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no
In the above case, the ixgbevf module is not loaded, because the listed driver is vif.

Copy
[ec2-user ~]$ ethtool -i eth0
driver: ixgbevf
version: 2.14.2
firmware-version: N/A
bus-info: 0000:00:03.0
supports-statistics: yes
supports-test: yes
supports-eeprom-access: no
supports-register-dump: yes
supports-priv-flags: no
In this case, the ixgbevf module is loaded and at the minimum recommended version. This instance has enhanced networking properly configured.

Enabling Enhanced Networking with the Intel 82599 VF Interface on Amazon Linux

The latest Amazon Linux HVM AMIs have the ixgbevf module required for enhanced networking installed and have the required sriovNetSupport attribute set. Therefore, if you launch a C3, C4, D2, I2, R3, or M4 (excluding m4.16xlarge) instance using a current Amazon Linux HVM AMI, enhanced networking is already enabled for your instance. For more information, see Testing Whether Enhanced Networking with the Intel 82599 VF Interface is Enabled.

If you launched your instance using an older Amazon Linux AMI and it does not have enhanced networking enabled already, use the following procedure to enable enhanced networking.

Warning
There is no way to disable the enhanced networking attribute after you've enabled it.
Warning
Enhanced networking is supported only for HVM instances. Enabling enhanced networking with a PV instance can make it unreachable. Setting this attribute without the proper module or module version can also make your instance unreachable.
To enable enhanced networking (EBS-backed instances)

Connect to your instance.

From the instance, run the following command to update your instance with the newest kernel and kernel modules, including ixgbevf:

Copy
[ec2-user ~]$ sudo yum update
From your local computer, reboot your instance using the Amazon EC2 console or one of the following commands: reboot-instances (AWS CLI), Restart-EC2Instance (AWS Tools for Windows PowerShell).

Connect to your instance again and verify that the ixgbevf module is installed and at the minimum recommended version using the modinfo ixgbevf command from Testing Whether Enhanced Networking with the Intel 82599 VF Interface is Enabled.

From your local computer, stop the instance using the Amazon EC2 console or one of the following commands: stop-instances (AWS CLI), Stop-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should stop the instance in the AWS OpsWorks console so that the instance state remains in sync.

Important
If you are using an instance store-backed instance, you can't stop the instance. Instead, proceed to To enable enhanced networking (instance store-backed instances).
From your local computer, enable the enhanced networking attribute using one of the following commands:

modify-instance-attribute (AWS CLI)
Copy
aws ec2 modify-instance-attribute --instance-id instance_id --sriov-net-support simple
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Copy
Edit-EC2InstanceAttribute -InstanceId instance_id -SriovNetSupport "simple"
(Optional) Create an AMI from the instance, as described in Creating an Amazon EBS-Backed Linux AMI . The AMI inherits the enhanced networking attribute from the instance. Therefore, you can use this AMI to launch another instance with enhanced networking enabled by default.

From your local computer, start the instance using the Amazon EC2 console or one of the following commands: start-instances (AWS CLI), Start-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should start the instance in the AWS OpsWorks console so that the instance state remains in sync.

Connect to your instance and verify that the ixgbevf module is installed and loaded on your network interface using the ethtool -i ethn command from Testing Whether Enhanced Networking with the Intel 82599 VF Interface is Enabled.

To enable enhanced networking (instance store-backed instances)

If your instance is an instance store–backed instance, follow Step 1 through Step 4 in the previous procedure, and then create a new AMI as described in Creating an Instance Store-Backed Linux AMI. Be sure to enable the enhanced networking attribute when you register the AMI.

register-image (AWS CLI)
Copy
aws ec2 register-image --sriov-net-support simple ...
Register-EC2Image (AWS Tools for Windows PowerShell)
Copy
Register-EC2Image -SriovNetSupport "simple" ...
Enabling Enhanced Networking with the Intel 82599 VF Interface on Ubuntu

The following procedure provides the general steps that you'll take when enabling enhanced networking with the Intel 82599 VF interface on an Ubuntu instance.

To enable enhanced networking on Ubuntu (EBS-backed instances)

Connect to your instance.

Update the package cache and packages.

Copy
ubuntu:~$ sudo apt-get update && sudo apt-get upgrade -y
Important
If during the update process, you are prompted to install grub, use /dev/xvda to install grub onto, and then choose to keep the current version of /boot/grub/menu.lst.
Install the dkms package so that your ixgbevf module is rebuilt every time your kernel is updated.

Copy
ubuntu:~$ sudo apt-get install -y dkms
Download the source for version 2.16.4 of the ixgbevf module on your instance from Sourceforge at http://sourceforge.net/projects/e1000/files/ixgbevf%20stable/.

Note that earlier versions of ixgbevf, including the minimum recommended version, 2.14.2, do not build properly on some versions of Ubuntu. The 2.16.4 version of ixgbevf should be used for Ubuntu instances.

Copy
ubuntu:~$ wget "sourceforge.net/projects/e1000/files/ixgbevf stable/2.16.4/ixgbevf-2.16.4.tar.gz"
Decompress and unarchive the ixgbevf package.

Copy
ubuntu:~$ tar -xzf ixgbevf-2.16.4.tar.gz
Move the ixgbevf package to the /usr/src/ directory so that dkms can find it and build it for each kernel update.

Copy
ubuntu:~$ sudo mv ixgbevf-2.16.4 /usr/src/
Create the dkms configuration file with the following values, substituting your version of ixgbevf.

Create the file.

Copy
ubuntu:~$ sudo touch /usr/src/ixgbevf-2.16.4/dkms.conf
Edit the file and add the following values.

Copy
ubuntu:~$ sudo vim /usr/src/ixgbevf-2.16.4/dkms.conf
PACKAGE_NAME="ixgbevf"
PACKAGE_VERSION="2.16.4"
CLEAN="cd src/; make clean"
MAKE="cd src/; make BUILD_KERNEL=${kernelver}"
BUILT_MODULE_LOCATION[0]="src/"
BUILT_MODULE_NAME[0]="ixgbevf"
DEST_MODULE_LOCATION[0]="/updates"
DEST_MODULE_NAME[0]="ixgbevf"
AUTOINSTALL="yes"
Add, build, and install the ixgbevf module on your instance using dkms.

Add the module to dkms.

Copy
ubuntu:~$ sudo dkms add -m ixgbevf -v 2.16.4
Build the module with dkms.

Copy
ubuntu:~$ sudo dkms build -m ixgbevf -v 2.16.4
Note
If your build fails, verify that perl is installed and that it is in your path. The dkms package requires perl, but it is not always installed by default on all operating systems.
Copy
ubuntu:~$ which perl
If the output of the above command does not show perl in your path, you need to install it.
Install the module with dkms.

Copy
ubuntu:~$ sudo dkms install -m ixgbevf -v 2.16.4
Rebuild initramfs so the correct module is loaded at boot time.

Copy
ubuntu:~$ sudo update-initramfs -c -k all
Verify that the ixgbevf module is installed and at the minimum recommended version using the modinfo ixgbevf command from Testing Whether Enhanced Networking with the Intel 82599 VF Interface is Enabled.

Copy
ubuntu:~$ modinfo ixgbevf
filename:       /lib/modules/3.13.0-74-generic/updates/dkms/ixgbevf.ko
version:        2.16.4
license:        GPL
description:    Intel(R) 10 Gigabit Virtual Function Network Driver
author:         Intel Corporation, <linux.nics@intel.com>
srcversion:     759A432E3151C8F9F6EA882
alias:          pci:v00008086d00001515sv*sd*bc*sc*i*
alias:          pci:v00008086d000010EDsv*sd*bc*sc*i*
depends:
vermagic:       3.13.0-74-generic SMP mod_unload modversions
parm:           InterruptThrottleRate:Maximum interrupts per second, per vector, (956-488281, 0=off, 1=dynamic), default 1 (array of int)
From your local computer, stop the instance using the Amazon EC2 console or one of the following commands: stop-instances (AWS CLI), Stop-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should stop the instance in the AWS OpsWorks console so that the instance state remains in sync.

Important
If you are using an instance store-backed instance, you can't stop the instance. Instead, proceed to To enable enhanced networking on Ubuntu (instance store-backed instances).
From your local computer, enable the enhanced networking sriovNetSupport attribute using one of the following commands. Note that there is no way to disable this attribute after you've enabled it.

modify-instance-attribute (AWS CLI)
Copy
aws ec2 modify-instance-attribute --instance-id instance_id --sriov-net-support simple
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Copy
Edit-EC2InstanceAttribute -InstanceId instance_id -SriovNetSupport "simple"
(Optional) Create an AMI from the instance, as described in Creating an Amazon EBS-Backed Linux AMI . The AMI inherits the enhanced networking sriovNetSupport attribute from the instance. Therefore, you can use this AMI to launch another instance with enhanced networking enabled by default.

From your local computer, start the instance using the Amazon EC2 console or one of the following commands: start-instances (AWS CLI), Start-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should start the instance in the AWS OpsWorks console so that the instance state remains in sync.

(Optional) Connect to your instance and verify that the module is installed.

To enable enhanced networking on Ubuntu (instance store-backed instances)

If your instance is an instance store-backed instance, follow Step 1 through Step 10 in the previous procedure, and then create a new AMI as described in Creating an Instance Store-Backed Linux AMI. Be sure to enable the enhanced networking attribute when you register the AMI.

register-image (AWS CLI)
Copy
aws ec2 register-image --sriov-net-support simple ...
Register-EC2Image (AWS Tools for Windows PowerShell)
Copy
Register-EC2Image -SriovNetSupport "simple" ...
Enabling Enhanced Networking with the Intel 82599 VF Interface on Other Linux Distributions

The following procedure provides the general steps that you'll take when enabling enhanced networking with the Intel 82599 VF interface on a Linux distribution other than Amazon Linux or Ubuntu. For more information, such as detailed syntax for commands, file locations, or package and tool support, see the specific documentation for your Linux distribution.

To enable enhanced networking on Linux (EBS-backed instances)

Connect to your instance.

Download the source for version 2.14.2 of the ixgbevf module on your instance from Sourceforge at http://sourceforge.net/projects/e1000/files/ixgbevf%20stable/. This is the minimum version recommended for enhanced networking.

Earlier versions of ixgbevf, including the minimum recommended version, 2.14.2, do not build properly on some Linux distributions, including certain versions of Ubuntu. If you receive build errors, you may try a newer version, such as 2.16.4 (which fixes the build issue on affected Ubuntu versions).

Compile and install the ixgbevf module on your instance.

If your distribution supports dkms, then you should consider configuring dkms to recompile the ixgbevf module whenever your system's kernel is updated. If your distribution does not support dkms natively, you can find it in the EPEL repository (https://fedoraproject.org/wiki/EPEL) for Red Hat Enterprise Linux variants, or you can download the software at http://linux.dell.com/dkms/. Use Step 6 through Step 8 in To enable enhanced networking on Ubuntu (EBS-backed instances) for help configuring dkms.

Warning
If you compile the ixgbevf module for your current kernel and then upgrade your kernel without rebuilding the driver for the new kernel, your system may revert to the distribution-specific ixgbevf module at the next reboot, which could make your system unreachable if the distribution-specific version is incompatible with enhanced networking.
Run the sudo depmod command to update module dependencies.

Update initramfs on your instance to ensure that the new module loads at boot time.

Determine if your system uses predictable network interface names by default. Systems that use systemd or udev versions 197 or greater can rename Ethernet devices and they do not guarantee that a single network interface will be named eth0. This behavior can cause problems connecting to your instance. For more information and to see other configuration options, see Predictable Network Interface Names on the freedesktop.org website.

You can check the systemd or udev versions on RPM-based systems with the following command:

Copy
[ec2-user ~]$ rpm -qa | grep -e '^systemd-[0-9]\+\|^udev-[0-9]\+'
systemd-208-11.el7_0.2.x86_64
In the above Red Hat 7 example, the systemd version is 208, so predictable network interface names must be disabled.

Disable predictable network interface names by adding the net.ifnames=0 option to the GRUB_CMDLINE_LINUX line in /etc/default/grub.

Copy
[ec2-user ~]$ sudo sed -i '/^GRUB\_CMDLINE\_LINUX/s/\"$/\ net\.ifnames\=0\"/' /etc/default/grub
Rebuild the grub configuration file.

Copy
[ec2-user ~]$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
From your local computer, stop the instance using the Amazon EC2 console or one of the following commands: stop-instances (AWS CLI), Stop-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should stop the instance in the AWS OpsWorks console so that the instance state remains in sync.

Important
If you are using an instance store-backed instance, you can't stop the instance. Instead, proceed to To enabled enhanced networking (instance store–backed instances)
From your local computer, enable the enhanced networking attribute using one of the following commands:

modify-instance-attribute (AWS CLI)
Copy
aws ec2 modify-instance-attribute --instance-id instance_id --sriov-net-support simple
Edit-EC2InstanceAttribute (AWS Tools for Windows PowerShell)
Copy
Edit-EC2InstanceAttribute -InstanceId instance_id -SriovNetSupport "simple"
(Optional) Create an AMI from the instance, as described in Creating an Amazon EBS-Backed Linux AMI . The AMI inherits the enhanced networking attribute from the instance. Therefore, you can use this AMI to launch another instance with enhanced networking enabled by default.

Important
If your instance operating system contains an /etc/udev/rules.d/70-persistent-net.rules file, you must delete it before creating the AMI. This file contains the MAC address for the Ethernet adapter of the original instance. If another instance boots with this file, the operating system will be unable to find the device and eth0 may fail, causing boot issues. This file is regenerated at the next boot cycle, and any instances launched from the AMI create their own version of the file.
From your local computer, start the instance using the Amazon EC2 console or one of the following commands: start-instances (AWS CLI), Start-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should start the instance in the AWS OpsWorks console so that the instance state remains in sync.

(Optional) Connect to your instance and verify that the module is installed.

To enabled enhanced networking (instance store–backed instances)

If your instance is an instance store–backed instance, follow Step 1 through Step 5 in the previous procedure, and then create a new AMI as described in Creating an Instance Store-Backed Linux AMI. Be sure to enable the enhanced networking attribute when you register the AMI.

register-image (AWS CLI)
Copy
aws ec2 register-image --sriov-net-support simple ...
Register-EC2Image (AWS Tools for Windows PowerShell)
Copy
Register-EC2Image -SriovNetSupport "simple" ...
Troubleshooting Connectivity Issues

If you lose connectivity while enabling enhanced networking, the ixgbevf module might be incompatible with the kernel. Try installing the version of the ixgbevf module included with the distribution of Linux for your instance.

If you enable enhanced networking for a PV instance or AMI, this can make your instance unreachable.

Enabling Enhanced Networking with the Elastic Network Adapter (ENA) on Linux Instances in a VPC

To prepare for enhanced networking with the ENA network adapter, set up your instance as follows:

Launch the instance from an HVM AMI using Linux kernel version of 3.2 or later. The latest Amazon Linux HVM AMIs have the modules required for enhanced networking installed and have the required attributes set. Therefore, if you launch an Amazon EBS–backed, enhanced networking–supported instance using a current Amazon Linux HVM AMI, ENA enhanced networking is already enabled for your instance.
Launch the instance in a VPC. (You can't enable enhanced networking if the instance is in EC2-Classic.)
Install and configure the AWS CLI or the AWS Tools for Windows PowerShell on any computer you choose, preferably your local desktop or laptop. For more information, see Accessing Amazon EC2. Enhanced networking cannot be managed from the Amazon EC2 console.
If you have important data on the instance that you want to preserve, you should back that data up now by creating an AMI from your instance. Updating kernels and kernel modules, as well as enabling the enaSupport attribute, may render incompatible instances or operating systems unreachable; if you have a recent backup, your data will still be retained if this happens.
Contents

Testing Whether Enhanced Networking with ENA Is Enabled
Enabling Enhanced Networking with ENA on Amazon Linux
Enabling Enhanced Networking with ENA on Ubuntu
Enabling Enhanced Networking with ENA on Other Linux Distributions
Troubleshooting
Testing Whether Enhanced Networking with ENA Is Enabled

To test whether enhanced networking with ENA is already enabled, verify that the ena module is installed on your instance and that the enaSupport attribute is set. If your instance satisfies these two conditions, then the ethtool -i ethn command should show that the module is in use on the network interface.

Kernel Module (ena)

To verify that the ena module is installed, use the modinfo command as follows:

Copy
[ec2-user ~]$ modinfo ena
filename:       /lib/modules/4.4.11-23.53.amzn1.x86_64/kernel/drivers/amazon/net/ena/ena.ko
version:        0.6.6
license:        GPL
description:    Elastic Network Adapter (ENA)
author:         Amazon.com, Inc. or its affiliates
srcversion:     3141E47566402C79D6B8284
alias:          pci:v00001D0Fd0000EC21sv*sd*bc*sc*i*
alias:          pci:v00001D0Fd0000EC20sv*sd*bc*sc*i*
alias:          pci:v00001D0Fd00001EC2sv*sd*bc*sc*i*
alias:          pci:v00001D0Fd00000EC2sv*sd*bc*sc*i*
depends:
intree:         Y
vermagic:       4.4.11-23.53.amzn1.x86_64 SMP mod_unload modversions
parm:           debug:Debug level (0=none,...,16=all) (int)
parm:           push_mode:Descriptor / header push mode (0=automatic,1=disable,3=enable)
			  0 - Automatically choose according to device capability (default)
			  1 - Don't push anything to device memory
			  3 - Push descriptors and header buffer to device memory (int)
parm:           enable_wd:Enable keepalive watchdog (0=disable,1=enable,default=1) (int)
parm:           enable_missing_tx_detection:Enable missing Tx completions. (default=1) (int)
parm:           numa_node_override_array:Numa node override map
 (array of int)
parm:           numa_node_override:Enable/Disable numa node override (0=disable)
 (int)
In the above Amazon Linux case, the ena module is installed.

Copy
ubuntu:~$ modinfo ena
ERROR: modinfo: could not find module ena
In the above Ubuntu instance, the module is not installed, so you must first install it. For more information, see Enabling Enhanced Networking with ENA on Ubuntu.

Instance Attribute (enaSupport)

To check whether an instance has the enhanced networking enaSupport attribute set, use one of the following commands. If the attribute is set, the response is true.

describe-instances (AWS CLI)
Copy
aws ec2 describe-instances --instance-ids instance_id --query 'Reservations[].Instances[].EnaSupport'
Get-EC2Instance (Tools for Windows PowerShell)
Copy
(Get-EC2Instance -InstanceId instance-id).Instances.EnaSupport
Image Attribute (enaSupport)

To check whether an AMI has the enhanced networking enaSupport attribute set, use one of the following commands. If the attribute is set, the response is true.

describe-images (AWS CLI)
Copy
aws ec2 describe-images --image-id ami_id --query 'Images[].EnaSupport'
Get-EC2Image (Tools for Windows PowerShell)
Copy
(Get-EC2Image -ImageId ami_id).EnaSupport
Network Interface Driver

Use the following command to verify that the ena module is being used on a particular interface, substituting the interface name that you wish to check. If you are using a single interface (default), it will be eth0.

Copy
[ec2-user ~]$ ethtool -i eth0
driver: vif
version:
firmware-version:
bus-info: vif-0
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no
In the above case, the ena module is not loaded, because the listed driver is vif.

Copy
[ec2-user ~]$ ethtool -i eth0
driver: ena
version: 0.6.6
firmware-version:
bus-info: 0000:00:03.0
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no
In this case, the ena module is loaded and at the minimum recommended version. This instance has enhanced networking properly configured.

Enabling Enhanced Networking with ENA on Amazon Linux

The latest Amazon Linux HVM AMIs have the module required for enhanced networking with ENA installed and have the required enaSupport attribute set. Therefore, if you launch an instance with the latest Amazon Linux HVM AMI on a supported instance type, enhanced networking with ENA is already enabled for your instance. For more information, see Testing Whether Enhanced Networking with ENA Is Enabled.

If you launched your instance using an older Amazon Linux AMI and it does not have enhanced networking enabled already, use the following procedure to enable enhanced networking.

To enable enhanced networking with ENA (EBS-backed instances)

Connect to your instance.

From the instance, run the following command to update your instance with the newest kernel and kernel modules, including ena:

Copy
[ec2-user ~]$ sudo yum update
From your local computer, reboot your instance using the Amazon EC2 console or one of the following commands: reboot-instances (AWS CLI), Restart-EC2Instance (AWS Tools for Windows PowerShell).

Connect to your instance again and verify that the ena module is installed and at the minimum recommended version using the modinfo ena command from Testing Whether Enhanced Networking with ENA Is Enabled.

From your local computer, stop the instance using the Amazon EC2 console or one of the following commands: stop-instances (AWS CLI), Stop-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should stop the instance in the AWS OpsWorks console so that the instance state remains in sync.

Important
If you are using an instance store-backed instance, you can't stop the instance. Instead, proceed to To enable enhanced networking with ENA (instance store-backed instances).
From your local computer, enable the enhanced networking attribute using one of the following commands:

modify-instance-attribute (AWS CLI)
Copy
aws ec2 modify-instance-attribute --instance-id instance_id --ena-support
Edit-EC2InstanceAttribute (Tools for Windows PowerShell)
Copy
Edit-EC2InstanceAttribute -InstanceId instance-id -EnaSupport $true
(Optional) Create an AMI from the instance, as described in Creating an Amazon EBS-Backed Linux AMI. The AMI inherits the enhanced networking enaSupport attribute from the instance. Therefore, you can use this AMI to launch another instance with enhanced networking with ENA enabled by default.

From your local computer, start the instance using the Amazon EC2 console or one of the following commands: start-instances (AWS CLI), Start-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should start the instance in the AWS OpsWorks console so that the instance state remains in sync.

Connect to your instance and verify that the ena module is installed and loaded on your network interface using the ethtool -i ethn command from Testing Whether Enhanced Networking with ENA Is Enabled.

If you are unable to connect to your instance after enabling enhanced networking with ENA, see Troubleshooting the Elastic Network Adapter (ENA).

To enable enhanced networking with ENA (instance store-backed instances)

If your instance is an instance store–backed instance, follow Step 1 through Step 4 in the previous procedure, and then create a new AMI as described in Creating an Instance Store-Backed Linux AMI. Be sure to enable the enhanced networking enaSupport attribute when you register the AMI.

register-image (AWS CLI)
Copy
aws ec2 register-image --ena-support ...
Register-EC2Image (AWS Tools for Windows PowerShell)
Copy
Register-EC2Image -EnaSupport $true ...
Enabling Enhanced Networking with ENA on Ubuntu

The following procedure provides the general steps that you'll take when enabling enhanced networking with ENA on an Ubuntu instance.

To enable enhanced networking with ENA on Ubuntu (EBS-backed instances)

Connect to your instance.

Update the package cache and packages.

Copy
ubuntu:~$ sudo apt-get update && sudo apt-get upgrade -y
Important
If during the update process you are prompted to install grub, use /dev/xvda to install grub onto, and then choose to keep the current version of /boot/grub/menu.lst.
Install the build-essential packages to compile the kernel module and the dkms package so that your ena module is rebuilt every time your kernel is updated.

Copy
ubuntu:~$ sudo apt-get install -y build-essential dkms
Clone the source code for the ena module on your instance from GitHub at https://github.com/amzn/amzn-drivers.

Copy
ubuntu:~$ git clone https://github.com/amzn/amzn-drivers
Move the amzn-drivers package to the /usr/src/ directory so dkms can find it and build it for each kernel update. Append the version number (you can find the current version number in the release notes) of the source code to the directory name. For example, version 1.0.0 is shown in the example below.

Copy
ubuntu:~$ sudo mv amzn-drivers /usr/src/amzn-drivers-1.0.0
Create the dkms configuration file with the following values, substituting your version of ena.

Create the file.

Copy
ubuntu:~$ sudo touch /usr/src/amzn-drivers-1.0.0/dkms.conf
Edit the file and add the following values.

Copy
ubuntu:~$ sudo vim /usr/src/amzn-drivers-1.0.0/dkms.conf
PACKAGE_NAME="ena"
PACKAGE_VERSION="1.0.0"
CLEAN="make -C kernel/linux/ena clean"
MAKE="make -C kernel/linux/ena/ BUILD_KERNEL=${kernelver}"
BUILT_MODULE_NAME[0]="ena"
BUILT_MODULE_LOCATION="kernel/linux/ena"
DEST_MODULE_LOCATION[0]="/updates"
DEST_MODULE_NAME[0]="ena"
AUTOINSTALL="yes"
Add, build, and install the ena module on your instance using dkms.

Add the module to dkms.

Copy
ubuntu:~$ sudo dkms add -m amzn-drivers -v 1.0.0
Build the module using dkms.

Copy
ubuntu:~$ sudo dkms build -m amzn-drivers -v 1.0.0
Install the module using dkms.

Copy
ubuntu:~$ sudo dkms install -m amzn-drivers -v 1.0.0
Rebuild initramfs so the correct module is loaded at boot time.

Copy
ubuntu:~$ sudo update-initramfs -c -k all
Verify that the ena module is installed using the modinfo ena command from Testing Whether Enhanced Networking with ENA Is Enabled.

Copy
ubuntu:~$ modinfo ena
filename:       /lib/modules/3.13.0-74-generic/updates/dkms/ena.ko
version:        1.0.0
license:        GPL
description:    Elastic Network Adapter (ENA)
author:         Amazon.com, Inc. or its affiliates
srcversion:     9693C876C54CA64AE48F0CA
alias:          pci:v00001D0Fd0000EC21sv*sd*bc*sc*i*
alias:          pci:v00001D0Fd0000EC20sv*sd*bc*sc*i*
alias:          pci:v00001D0Fd00001EC2sv*sd*bc*sc*i*
alias:          pci:v00001D0Fd00000EC2sv*sd*bc*sc*i*
depends:
vermagic:       3.13.0-74-generic SMP mod_unload modversions
parm:           debug:Debug level (0=none,...,16=all) (int)
parm:           push_mode:Descriptor / header push mode (0=automatic,1=disable,3=enable)
			  0 - Automatically choose according to device capability (default)
			  1 - Don't push anything to device memory
			  3 - Push descriptors and header buffer to device memory (int)
parm:           enable_wd:Enable keepalive watchdog (0=disable,1=enable,default=1) (int)
parm:           enable_missing_tx_detection:Enable missing Tx completions. (default=1) (int)
parm:           numa_node_override_array:Numa node override map
 (array of int)
parm:           numa_node_override:Enable/Disable numa node override (0=disable)
 (int)
From your local computer, stop the instance using the Amazon EC2 console or one of the following commands: stop-instances (AWS CLI), Stop-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should stop the instance in the AWS OpsWorks console so that the instance state remains in sync.

Important
If you are using an instance store-backed instance, you can't stop the instance. Instead, proceed to To enable enhanced networking with ENA on Ubuntu (instance store-backed instances).
From your local computer, enable the enhanced networking attribute using one of the following commands:

modify-instance-attribute (AWS CLI)
Copy
aws ec2 modify-instance-attribute --instance-id instance_id --ena-support
Edit-EC2InstanceAttribute (Tools for Windows PowerShell)
Copy
Edit-EC2InstanceAttribute -InstanceId instance-id -EnaSupport $true
(Optional) Create an AMI from the instance, as described in Creating an Amazon EBS-Backed Linux AMI . The AMI inherits the enhanced networking attribute from the instance. Therefore, you can use this AMI to launch another instance with enhanced networking enabled by default.

From your local computer, start the instance using the Amazon EC2 console or one of the following commands: start-instances (AWS CLI), Start-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should start the instance in the AWS OpsWorks console so that the instance state remains in sync.

(Optional) Connect to your instance and verify that the module is installed.

If you are unable to connect to your instance after enabling enhanced networking with ENA, see Troubleshooting the Elastic Network Adapter (ENA).

To enable enhanced networking with ENA on Ubuntu (instance store-backed instances)

If your instance is an instance store-backed instance, follow Step 1 through Step 9 in the previous procedure, and then create a new AMI as described in Creating an Instance Store-Backed Linux AMI. Be sure to enable the enhanced networking enaSupport attribute when you register the AMI.

register-image (AWS CLI)
Copy
aws ec2 register-image --ena-support ...
Register-EC2Image (AWS Tools for Windows PowerShell)
Copy
Register-EC2Image -EnaSupport $true ...
Enabling Enhanced Networking with ENA on Other Linux Distributions

The following procedure provides the general steps that you'll take when enabling enhanced networking with ENA on a Linux distribution other than Amazon Linux or Ubuntu. For more information, such as detailed syntax for commands, file locations, or package and tool support, see the specific documentation for your Linux distribution.

To enable enhanced networking with ENA on Linux (EBS-backed instances)

Connect to your instance.

Clone the source code for the ena module on your instance from GitHub at https://github.com/amzn/amzn-drivers.

Copy
ubuntu:~$ git clone https://github.com/amzn/amzn-drivers
Compile and install the ena module on your instance.

If your distribution supports dkms, then you should consider configuring dkms to recompile the ena module whenever your system's kernel is updated. If your distribution does not support dkms natively, you can find it in the EPEL repository (https://fedoraproject.org/wiki/EPEL) for Red Hat Enterprise Linux variants, or you can download the software at http://linux.dell.com/dkms/. Use Step 5 through Step 7 in To enable enhanced networking with ENA on Ubuntu (EBS-backed instances) for help configuring dkms.

Run the sudo depmod command to update module dependencies.

Update initramfs on your instance to ensure that the new module loads at boot time.

Determine if your system uses predictable network interface names by default. Systems that use systemd or udev versions 197 or greater can rename Ethernet devices and they do not guarantee that a single network interface will be named eth0. This behavior can cause problems connecting to your instance. For more information and to see other configuration options, see Predictable Network Interface Names on the freedesktop.org website.

You can check the systemd or udev versions on RPM-based systems with the following command:

Copy
[ec2-user ~]$ rpm -qa | grep -e '^systemd-[0-9]\+\|^udev-[0-9]\+'
systemd-208-11.el7_0.2.x86_64
In the above Red Hat 7 example, the systemd version is 208, so predictable network interface names must be disabled.

Disable predictable network interface names by adding the net.ifnames=0 option to the GRUB_CMDLINE_LINUX line in /etc/default/grub.

Copy
[ec2-user ~]$ sudo sed -i '/^GRUB\_CMDLINE\_LINUX/s/\"$/\ net\.ifnames\=0\"/' /etc/default/grub
Rebuild the grub configuration file.

Copy
[ec2-user ~]$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
From your local computer, stop the instance using the Amazon EC2 console or one of the following commands: stop-instances (AWS CLI), Stop-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should stop the instance in the AWS OpsWorks console so that the instance state remains in sync.

Important
If you are using an instance store-backed instance, you can't stop the instance. Instead, proceed to To enabled enhanced networking with ENA (instance store–backed instances)
From your local computer, enable the enhanced networking enaSupport attribute using one of the following commands:

modify-instance-attribute (AWS CLI)
Copy
aws ec2 modify-instance-attribute --instance-id instance_id --ena-support
Edit-EC2InstanceAttribute (Tools for Windows PowerShell)
Copy
Edit-EC2InstanceAttribute -InstanceId instance-id -EnaSupport $true
(Optional) Create an AMI from the instance, as described in Creating an Amazon EBS-Backed Linux AMI . The AMI inherits the enhanced networking enaSupport attribute from the instance. Therefore, you can use this AMI to launch another instance with enhanced networking enabled by default.

Important
If your instance operating system contains an /etc/udev/rules.d/70-persistent-net.rules file, you must delete it before creating the AMI. This file contains the MAC address for the Ethernet adapter of the original instance. If another instance boots with this file, the operating system will be unable to find the device and eth0 may fail, causing boot issues. This file is regenerated at the next boot cycle, and any instances launched from the AMI create their own version of the file.
From your local computer, start the instance using the Amazon EC2 console or one of the following commands: start-instances (AWS CLI), Start-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should start the instance in the AWS OpsWorks console so that the instance state remains in sync.

(Optional) Connect to your instance and verify that the module is installed.

If you are unable to connect to your instance after enabling enhanced networking with ENA, see Troubleshooting the Elastic Network Adapter (ENA).

To enabled enhanced networking with ENA (instance store–backed instances)

If your instance is an instance store–backed instance, follow the Step 1 through the Step 5 in the previous procedure, and then create a new AMI as described in Creating an Instance Store-Backed Linux AMI. Be sure to enable the enhanced networking enaSupport attribute when you register the AMI.

register-image (AWS CLI)
Copy
aws ec2 register-image --ena-support ...
Register-EC2Image (AWS Tools for Windows PowerShell)
Copy
Register-EC2Image -EnaSupport ...
Troubleshooting

For additional information about troubleshooting your ENA adapter, see Troubleshooting the Elastic Network Adapter (ENA).

Troubleshooting the Elastic Network Adapter (ENA)

The Elastic Network Adapter (ENA) is designed to improve operating system health and reduce the chances of long-term disruption because of unexpected hardware behavior and or failures. The ENA architecture keeps device or driver failures as transparent to the system as possible. This topic provides troubleshooting information for ENA.

If you are unable to connect to your instance, start with the Troubleshooting Connectivity Issues section.

If you are able to connect to your instance, you can gather diagnostic information by using the failure detection and recovery mechanisms that are covered in the later sections of this topic.

Contents

Troubleshooting Connectivity Issues
Keep-Alive Mechanism
Register Read Timeout
Statistics
Driver Error Logs in syslog
Troubleshooting Connectivity Issues

If you lose connectivity while enabling enhanced networking, the ena module might be incompatible with your instance's current running kernel. This can happen if you install the module for a specific kernel version (without dkms, or with an improperly configured dkms.conf file) and then your instance kernel is updated. If the instance kernel that is loaded at boot time does not have the ena module properly installed, your instance will not recognize the network adapter and your instance becomes unreachable.

If you enable enhanced networking for a PV instance or AMI, this can also make your instance unreachable.

If your instance becomes unreachable after enabling enhanced networking with ENA, you can disable the enaSupport attribute for your instance and it will fall back to the stock network adapter.

To disable enhanced networking with ENA (EBS-backed instances)

From your local computer, stop the instance using the Amazon EC2 console or one of the following commands: stop-instances (AWS CLI), Stop-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should stop the instance in the AWS OpsWorks console so that the instance state remains in sync.

Important
If you are using an instance store-backed instance, you can't stop the instance. Instead, proceed to To disable enhanced networking with ENA (instance store-backed instances).
From your local computer, disable the enhanced networking attribute using the following command.

modify-instance-attribute (AWS CLI)
Copy
$ aws ec2 modify-instance-attribute --instance-id instance_id --no-ena-support
From your local computer, start the instance using the Amazon EC2 console or one of the following commands: start-instances (AWS CLI), Start-EC2Instance (AWS Tools for Windows PowerShell). If your instance is managed by AWS OpsWorks, you should start the instance in the AWS OpsWorks console so that the instance state remains in sync.

(Optional) Connect to your instance and try reinstalling the ena module with your current kernel version by following the steps in Enabling Enhanced Networking with the Elastic Network Adapter (ENA) on Linux Instances in a VPC.

To disable enhanced networking with ENA (instance store-backed instances)

If your instance is an instance store-backed instance, create a new AMI as described in Creating an Instance Store-Backed Linux AMI. Be sure to disable the enhanced networking enaSupport attribute when you register the AMI.

register-image (AWS CLI)
Copy
$ aws ec2 register-image --no-ena-support ...
Register-EC2Image (AWS Tools for Windows PowerShell)
Copy
C:\> Register-EC2Image -EnaSupport $false ...
Keep-Alive Mechanism

The ENA device posts keep-alive events at a fixed rate (usually once every second). The ENA driver implements a watchdog mechanism, which checks every for the presence of these keep-alive messages. If a message or messages are present, the watchdog is rearmed, otherwise the driver concludes that the device experienced a failure and then does the following:

Dumps its current statistics to syslog
Resets the ENA device
Resets the ENA driver state
The above reset procedure may result in some traffic loss for a short period of time (TCP connections should be able to recover), but should not otherwise affect the user.

The ENA device may also indirectly request a device reset procedure, by not sending a keep-alive notification, for example, if the ENA device reaches an unknown state after loading an irrecoverable configuration.

Below is an example of the reset procedure:

[18509.800135] ena 0000:00:07.0 eth1: Keep alive watchdog timeout. // The watchdog process initiates a reset
[18509.815244] ena 0000:00:07.0 eth1: Trigger reset is on		
[18509.825589] ena 0000:00:07.0 eth1: tx_timeout: 0 // The driver logs the current statistics
[18509.834253] ena 0000:00:07.0 eth1: io_suspend: 0
[18509.842674] ena 0000:00:07.0 eth1: io_resume: 0
[18509.850275] ena 0000:00:07.0 eth1: wd_expired: 1
[18509.857855] ena 0000:00:07.0 eth1: interface_up: 1
[18509.865415] ena 0000:00:07.0 eth1: interface_down: 0
[18509.873468] ena 0000:00:07.0 eth1: admin_q_pause: 0
[18509.881075] ena 0000:00:07.0 eth1: queue_0_tx_cnt: 0
[18509.888629] ena 0000:00:07.0 eth1: queue_0_tx_bytes: 0
[18509.895286] ena 0000:00:07.0 eth1: queue_0_tx_queue_stop: 0
.......
........
[18511.280972] ena 0000:00:07.0 eth1: free uncompleted tx skb qid 3 idx 0x7 // At the end of the down process, the driver discards incomplete packets.
[18511.420112] [ENA_COM: ena_com_validate_version] ena device version: 0.10 //The driver begins its up process
[18511.420119] [ENA_COM: ena_com_validate_version] ena controller version: 0.0.1 implementation version 1
[18511.420127] [ENA_COM: ena_com_admin_init] ena_defs : Version:[b9692e8] Build date [Wed Apr  6 09:54:21 IDT 2016]
[18512.252108] ena 0000:00:07.0: Device watchdog is Enabled
[18512.674877] ena 0000:00:07.0: irq 46 for MSI/MSI-X
[18512.674933] ena 0000:00:07.0: irq 47 for MSI/MSI-X
[18512.674990] ena 0000:00:07.0: irq 48 for MSI/MSI-X
[18512.675037] ena 0000:00:07.0: irq 49 for MSI/MSI-X
[18512.675085] ena 0000:00:07.0: irq 50 for MSI/MSI-X
[18512.675141] ena 0000:00:07.0: irq 51 for MSI/MSI-X
[18512.675188] ena 0000:00:07.0: irq 52 for MSI/MSI-X
[18512.675233] ena 0000:00:07.0: irq 53 for MSI/MSI-X
[18512.675279] ena 0000:00:07.0: irq 54 for MSI/MSI-X
[18512.772641] [ENA_COM: ena_com_set_hash_function] Feature 10 isn't supported
[18512.772647] [ENA_COM: ena_com_set_hash_ctrl] Feature 18 isn't supported
[18512.775945] ena 0000:00:07.0: Device reset completed successfully // The reset process is complete
Register Read Timeout

The ENA architecture suggests a limited usage of memory mapped I/O (MMIO) read operations. MMIO registers are accessed by the ENA device driver only during its initialization procedure.

If the driver logs (available in dmesg output) indicate failures of read operations, this may be caused by an incompatible or incorrectly compiled driver, a busy hardware device, or hardware failure.

Intermittent log entries that indicate failures on read operations should not be considered an issue; the driver will retry them in this case. However, a sequence of log entries containing read failures indicate a driver or hardware problem.

Below is an example of driver log entry indicating a read operation failure due to a timeout:

[ 47.113698] [ENA_COM: ena_com_reg_bar_read32] reading reg failed for timeout. expected: req id[1] offset[88] actual: req id[57006] offset[0] 
[ 47.333715] [ENA_COM: ena_com_reg_bar_read32] reading reg failed for timeout. expected: req id[2] offset[8] actual: req id[57007] offset[0] 
[ 47.346221] [ENA_COM: ena_com_dev_reset] Reg read32 timeout occurred
Statistics

If you experience insufficient network performance or latency issues, you should retrieve the device statistics and examine them. These statistics can be obtained using ethtool, as shown below:

Copy
[ec2-user ~]$ ethtool –S ethN
NIC statistics:
     tx_timeout: 0
     io_suspend: 0
     io_resume: 0
     wd_expired: 0
     interface_up: 1
     interface_down: 0
     admin_q_pause: 0
     queue_0_tx_cnt: 4329
     queue_0_tx_bytes: 1075749
     queue_0_tx_queue_stop: 0
...
The following command output parameters are described below:

tx_timeout: N
The number of times that the Netdev watchdog was activated.

io_suspend: N
Unsupported. This value should always be zero.

io_resume: N
Unsupported. This value should always be zero.

wd_expired: N
The number of times that the driver did not receive the keep-alive event in the preceding 3 seconds.

interface_up: N
The number of times that the ENA interface was brought up.

interface_down: N
The number of times that the ENA interface was brought down.

admin_q_pause: N
The admin queue is in an unstable state. This value should always be zero.

queue_N_tx_cnt: N
The number of transmitted packets for queue N.

queue_N_tx_bytes: N
The number of transmitted bytes for queue N.

queue_N_tx_queue_stop: N
The number of times that queue N was full and stopped.

queue_N_tx_queue_wakeup: N
The number of times that queue N resumed after being stopped.

queue_N_tx_dma_mapping_err: N
Direct memory access error count. If this value is not 0, it indicates low system resources.

queue_N_tx_napi_comp: N
The number of times the napi handler called napi_complete for queue N.

queue_N_tx_poll: N
The number of times the napi handler was scheduled for queue N.

queue_N_tx_doorbells: N
The number of transmission doorbells for queue N.

queue_N_tx_linearize: N
The number of times SKB linearization was attempted for queue N.

queue_N_tx_linearize_failed: N
The number of times SKB linearization failed for queue N.

queue_N_tx_prepare_ctx_err: N
The number of times ena_com_prepare_tx failed for queue N. This value should always be zero; if not, see the driver logs.

queue_N_tx_missing_tx_comp: codeN
The number of packets that were left uncompleted for queue N. This value should always be zero.

queue_N_tx_bad_req_id: N
Invalid req_id for queue N. The valid req_id is zero, minus the queue_size, minus 1.

queue_N_rx_cnt: N
The number of received packets for queue N.

queue_N_rx_bytes: N
The number of received bytes for queue N.

queue_N_rx_refil_partial: N
The number of times the driver did not succeed in refilling the empty portion of the rx queue with the buffers for queue N. If this value is not zero, it indicates low memory resources.

queue_N_rx_bad_csum: N
The number of times the rx queue had a bad checksum for queue N (only if rx checksum offload is supported).

queue_N_rx_page_alloc_fail: N
The number of time that page allocation failed for queue N. If this value is not zero, it indicates low memory resources.

queue_N_rx_skb_alloc_fail: N
The number of time that SKB allocation failed for queue N. If this value is not zero, it indicates low system resources.

queue_N_rx_dma_mapping_err: N
Direct memory access error count. If this value is not 0, it indicates low system resources.

queue_N_rx_bad_desc_num: N
Too many buffers per packet. If this value is not 0, it indicates usage of very small buffers.

queue_N_rx_small_copy_len_pkt: N
Optimization: For packets smaller that this threshold, which is set by sysfs, the packet is copied directly to the stack to avoid allocation of a new page.

ena_admin_q_aborted_cmd: N
The number of admin commands that were aborted. This usually happens during the auto-recovery procedure.

ena_admin_q_submitted_cmd: N
The number of admin queue doorbells.

ena_admin_q_completed_cmd: N
The number of admin queue completions.

ena_admin_q_out_of_space: N
The number of times that the driver tried to submit new admin command, but the queue was full.

ena_admin_q_no_completion: N
The number of times that the driver did not get an admin completion for a command.

Driver Error Logs in syslog

The ENA driver writes log messages to syslog during system boot. You can examine these logs to look for errors if you are experiencing issues. Below is an example of information logged by the ENA driver in syslog during system boot, along with some annotations for select messages.

Jun  3 22:37:46 ip-172-31-2-186 kernel: [  478.416939] [ENA_COM: ena_com_validate_version] ena device version: 0.10
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  478.420915] [ENA_COM: ena_com_validate_version] ena controller version: 0.0.1 implementation version 1
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.256831] ena 0000:00:03.0: Device watchdog is Enabled
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.672947] ena 0000:00:03.0: creating 8 io queues. queue size: 1024
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.680885] [ENA_COM: ena_com_init_interrupt_moderation] Feature 20 isn't supported  // Interrupt moderation is not supported by the device
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.691609] [ENA_COM: ena_com_get_feature_ex] Feature 10 isn't supported // RSS HASH function configuration is not supported by the device
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.694583] [ENA_COM: ena_com_get_feature_ex] Feature 18 isn't supported //RSS HASH input source configuration is not supported by the device 
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.697433] [ENA_COM: ena_com_set_host_attributes] Set host attribute isn't supported
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.701064] ena 0000:00:03.0 (unnamed net_device) (uninitialized): Cannot set host attributes
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  479.704917] ena 0000:00:03.0: Elastic Network Adapter (ENA) found at mem f3000000, mac addr 02:8a:3c:1e:13:b5 Queues 8
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  480.805037] EXT4-fs (xvda1): re-mounted. Opts: (null)
Jun  3 22:37:46 ip-172-31-2-186 kernel: [  481.025842] NET: Registered protocol family 10
Which errors can I ignore?

The following warnings that may appear in your system's error logs can be ignored for the Elastic Network Adapter:

Set host attribute isn't supported
Host attributes are not supported for this device.

failed to alloc buffer for rx queue
This is a recoverable error, and it indicates that there may have been a memory pressure issue when the error was thrown.

Feature X isn't supported
The referenced feature is not supported by the Elastic Network Adapter. Possible values for X include:

10: RSS Hash function configuration is not supported for this device.
12: RSS Indirection table configuration is not supported for this device.
18: RSS Hash Input configuration is not supported for this device.
20: Interrupt moderation is not supported for this device.
Failed to config AENQ
The Elastic Network Adapter does not support AENQ configuration.

Trying to set unsupported AENQ events
This error indicates an attempt to set an AENQ events group that is not supported by the Elastic Network Adapter.

