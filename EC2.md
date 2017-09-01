# What Is Amazon EC2?

Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) cloud. Using Amazon EC2 eliminates your need to invest in hardware up front, so you can develop and deploy applications faster. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage. Amazon EC2 enables you to scale up or down to handle changes in requirements or spikes in popularity, reducing your need to forecast traffic.

## Features of Amazon EC2

Amazon EC2 provides the following features:

- Virtual computing environments, known as instances
- Preconfigured templates for your instances, known as Amazon Machine Images (AMIs), that package the bits you need for your server (including the operating system and additional software)
- Various configurations of CPU, memory, storage, and networking capacity for your instances, known as instance types
- Secure login information for your instances using key pairs (AWS stores the public key, and you store the private key in a secure place)
- Storage volumes for temporary data that's deleted when you stop or terminate your instance, known as instance store volumes
- Persistent storage volumes for your data using Amazon Elastic Block Store (Amazon EBS), known as Amazon EBS volumes
- Multiple physical locations for your resources, such as instances and Amazon EBS volumes, known as regions and Availability Zones
- A firewall that enables you to specify the protocols, ports, and source IP ranges that can reach your instances using security groups
- Static IPv4 addresses for dynamic cloud computing, known as Elastic IP addresses
- Metadata, known as tags, that you can create and assign to your Amazon EC2 resources
- Virtual networks you can create that are logically isolated from the rest of the AWS cloud, and that you can optionally connect to your own network, known as virtual private clouds (VPCs)

## How to Get Started with Amazon EC2

The first thing you need to do is get set up to use Amazon EC2. After you are set up, you are ready to complete the Getting Started tutorial for Amazon EC2. 

## Related Services

You can provision Amazon EC2 resources, such as instances and volumes, directly using Amazon EC2. You can also provision Amazon EC2 resources using other services in AWS. 

To automatically distribute incoming application traffic across multiple instances, use Elastic Load Balancing.

To monitor basic statistics for your instances and Amazon EBS volumes, use Amazon CloudWatch.

To automate actions, such as activating a Lambda function whenever a new Amazon EC2 instance starts, or invoking SSM Run Command whenever an event in another AWS service happens, use Amazon CloudWatch Events. 

To monitor the calls made to the Amazon EC2 API for your account, including calls made by the AWS Management Console, command line tools, and other services, use AWS CloudTrail.

To get a managed relational database in the cloud, use Amazon Relational Database Service (Amazon RDS) to launch a database instance. Although you can set up a database on an EC2 instance, Amazon RDS offers the advantage of handling your database management tasks, such as patching the software, backing up, and storing the backups.

To import virtual machine (VM) images from your local environment into AWS and convert them into ready-to-use AMIs or instances, use VM Import/Export.

## Accessing Amazon EC2

Amazon EC2 provides a web-based user interface, the Amazon EC2 console. If you've signed up for an AWS account, you can access the Amazon EC2 console by signing into the AWS Management Console and selecting EC2 from the console home page.

If you prefer to use a command line interface, you have the following options:

### AWS Command Line Interface (CLI)
Provides commands for a broad set of AWS products, and is supported on Windows, Mac, and Linux. To get started, see AWS Command Line Interface User Guide.

### AWS Tools for Windows PowerShell
Provides commands for a broad set of AWS products for those who script in the PowerShell environment.

Amazon EC2 provides a Query API. These requests are HTTP or HTTPS requests that use the HTTP verbs GET or POST and a Query parameter named Action.

If you prefer to build applications using language-specific APIs instead of submitting a request over HTTP or HTTPS, AWS provides libraries, sample code, tutorials, and other resources for software developers. These libraries provide basic functions that automate tasks such as cryptographically signing your requests, retrying requests, and handling error responses, making it is easier for you to get started.

## Pricing for Amazon EC2

When you sign up for AWS, you can get started with Amazon EC2 for free using the AWS Free Tier.

Amazon EC2 provides the following purchasing options for instances:

On-Demand instances

Pay for the instances that you use by the hour, with no long-term commitments or up-front payments.

Reserved Instances

Make a low, one-time, up-front payment for an instance, reserve it for a one- or three-year term, and pay a significantly lower hourly rate for these instances.

Spot instances

Specify the maximum hourly price that you are willing to pay to run a particular instance type. The Spot price fluctuates based on supply and demand, but you never pay more than the maximum price you specified. If the Spot price moves higher than your maximum price, Amazon EC2 shuts down your Spot instances.

## PCI DSS Compliance

Amazon EC2 supports the processing, storage, and transmission of credit card data by a merchant or service provider, and has been validated as being compliant with Payment Card Industry (PCI) Data Security Standard (DSS). For more information about PCI DSS, including how to request a copy of the AWS PCI Compliance Package, see PCI DSS Level 1.

# Instances and AMIs

An Amazon Machine Image is a template that contains a software configuration (for example, an operating system, an application server, and applications). From an AMI, you launch an instance, which is a copy of the AMI running as a virtual server in the cloud. You can launch multiple instances of an AMI, as shown in the following figure.
			
Your instances keep running until you stop or terminate them, or until they fail. If an instance fails, you can launch a new one from the AMI.

## Instances

You can launch different types of instances from a single AMI. An instance type essentially determines the hardware of the host computer used for your instance. Each instance type offers different compute and memory capabilities. Select an instance type based on the amount of memory and computing power that you need for the application or software	that you plan to run on the instance. For more information about the hardware specifications for each Amazon EC2 instance type, see Amazon EC2 Instances.

After you launch an instance, it looks like a traditional host, and you can interact with it as you would any computer. You have complete control of your instances; you can use sudo to run commands that require root privileges.

Your AWS account has a limit on the number of instances that you can have running.

### Storage for Your Instance

The root device for your instance contains the image used to boot the instance.

Your instance may include local storage volumes, known as instance store volumes, which you can configure at launch time with block device mapping. After these volumes have been added to and mapped on your instance, they are available for you to mount and use. If your instance fails, or if your instance is stopped or terminated, the data on these volumes is lost; therefore, these volumes are best used for temporary data. For important data, you should use a replication strategy across multiple instances in order to keep your data safe, or store your persistent data in Amazon S3 or Amazon EBS volumes.

### Security Best Practices

- Use AWS Identity and Access Management to control access to your AWS resources, including your instances. You can create IAM users and groups under your AWS account, assign security credentials to each, and control the access that each has to resources and services in AWS. For more information, see Controlling Access to Amazon EC2 Resources.
- Restrict access by only allowing trusted hosts or networks to access ports on your instance. For example, you can restrict SSH access by restricting incoming traffic on port 22.
- Review the rules in your security groups regularly, and ensure that you apply the principle of least privilege—only open up permissions that you require. You can also create different security groups to deal with instances that have different security requirements. Consider creating a bastion security group that allows external logins, and keep the remainder of your instances in a group that does not allow external logins.
- Disable password-based logins for instances launched from your AMI. Passwords can be found or cracked, and are a security risk.

### Stopping, Starting, and Terminating Instances

#### Stopping an instance

When an instance is stopped, the instance performs a normal shutdown, and then transitions to a stopped state. All of its Amazon EBS volumes remain attached, and you can start the instance again at a later time.

You are not charged for additional instance hours while the instance is in a stopped state. A full instance hour will be charged for every transition from a stopped state to a running state, even if this happens multiple times within a single hour. If the instance type was changed while the instance was stopped, you will be charged the rate for the new instance type after the instance is started. All of the associated Amazon EBS usage of your instance, including root device usage, is billed using typical Amazon EBS prices.

When an instance is in a stopped state, you can attach or detach Amazon EBS volumes. You can also create an AMI from the instance, and you can change the kernel, RAM disk, and instance type.

#### Terminating an instance

When an instance is terminated, the instance performs a normal shutdown, then the attached Amazon EBS volumes are deleted unless the volume's deleteOnTermination attribute is set to false. The instance itself is also deleted, and you can't start the instance again at a later time.

To prevent accidental termination, you can disable instance termination. If you do so, ensure that the disableApiTermination attribute is set to true for the instance. To control the behavior of an instance shutdown, such as shutdown -h in Linux or shutdown in Windows, set the instanceInitiatedShutdownBehavior instance attribute to stop or terminate as desired. Instances with Amazon EBS volumes for the root device default to stop, and instances with instance-store root devices are always terminated as the result of an instance shutdown.

### AMIs

Amazon Web Services (AWS) publishes many Amazon Machine Images (AMIs) that contain common software configurations for public use. In addition, members of the AWS developer community have published their own custom AMIs. You can also create your own custom AMI or AMIs; doing so enables you to quickly and easily start new instances that have everything you need. For example, if your application is a website or a web service, your AMI could include a web server, the associated static content, and the code for the dynamic pages. As a result, after you launch an instance from this AMI, your web server starts, and your application is ready to accept requests.

All AMIs are categorized as either backed by Amazon EBS, which means that the root device for an instance launched from the AMI is an Amazon EBS volume, or backed by instance store, which means that the root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3.

The description of an AMI indicates the type of root device (either ebs or instance store). This is important because there are significant differences in what you can do with each type of AMI.

# Regions and Availability Zones

Amazon EC2 is hosted in multiple locations world-wide. These locations are composed of regions and Availability Zones. Each region is a separate geographic area. Each region has multiple, isolated locations known as Availability Zones. Amazon EC2 provides you the ability to place resources, such as instances, and data in multiple locations. Resources aren't replicated across regions unless you do so specifically.

Amazon operates state-of-the-art, highly-available data centers. Although rare, failures can occur that affect the availability of instances that are in the same location. If you host all your instances in a single location that is affected by such a failure, none of your instances would be available.

## Region and Availability Zone Concepts

Each region is completely independent. Each Availability Zone is isolated, but the Availability Zones in a region are connected through low-latency links. The following diagram illustrates the relationship between regions and Availability Zones.

Amazon EC2 resources are either global, tied to a region, or tied to an Availability Zone.

### Regions

Each Amazon EC2 region is designed to be completely isolated from the other Amazon EC2 regions. This achieves the greatest possible fault tolerance and stability.

When you view your resources, you'll only see the resources tied to the region you've specified. This is because regions are isolated from each other, and we don't replicate resources across regions automatically.

When you launch an instance, you must select an AMI that's in the same region. If the AMI is in another region, you can copy the AMI to the region you're using.

Note that there is a charge for data transfer between regions.

### Availability Zones

When you launch an instance, you can select an Availability Zone or let us choose one for you. If you distribute your instances across multiple Availability Zones and one instance fails, you can design your application so that an instance in another Availability Zone can handle requests.

You can also use Elastic IP addresses to mask the failure of an instance in one Availability Zone by rapidly remapping the address to an instance in another Availability Zone. For more information, see Elastic IP Addresses.

An Availability Zone is represented by a region code followed by a letter identifier; for example, us-east-1a. To ensure that resources are distributed across the Availability Zones for a region, we independently map Availability Zones to identifiers for each account. For example, your Availability Zone us-east-1a might not be the same location as us-east-1a for another account. There's no way for you to coordinate Availability Zones between accounts.

As Availability Zones grow over time, our ability to expand them can become constrained. If this happens, we might restrict you from launching an instance in a constrained Availability Zone unless you already have an instance in that Availability Zone. Eventually, we might also remove the constrained Availability Zone from the list of Availability Zones for new customers. Therefore, your account might have a different number of available Availability Zones in a region than another account.

You can list the Availability Zones that are available to your account. For more information, see Describing Your Regions and Availability Zones.

## Available Regions

Your account determines the regions that are available to you. For example:

An AWS account provides multiple regions so that you can launch Amazon EC2 instances in locations that meet your requirements. For example, you might want to launch instances in Europe to be closer to your European customers or to meet legal requirements.
An AWS GovCloud (US) account provides access to the AWS GovCloud (US) region only. For more information, see AWS GovCloud (US) Region.
An Amazon AWS (China) account provides access to the China (Beijing) region only.
The following table lists the regions provided by an AWS account. You can't describe or access additional regions from an AWS account, such as AWS GovCloud (US) or China (Beijing).

The number and mapping of Availability Zones per region may vary between AWS accounts. To get a list of the Availability Zones that are available to your account, you can use the Amazon EC2 console or the command line interface.

## Regions and Endpoints

When you work with an instance using the command line interface or API actions, you must specify its regional endpoint.

Describing Your Regions and Availability Zones

You can use the Amazon EC2 console or the command line interface to determine which regions and Availability Zones are available for your account. For more information about these command line interfaces, see Accessing Amazon EC2.

### To find your regions and Availability Zones using the console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
2. From the navigation bar, view the options in the region selector.
3. View the Availability Zones on the dashboard under Service Health, Availability Zone Status.

### To find your regions and Availability Zones using the command line

1. Use the describe-regions command as follows to describe the regions for your account.

`aws ec2 describe-regions`

2. Use the describe-availability-zones command as follows to describe the Availability `Zones within the specified region.

`aws ec2 describe-availability-zones --region region-name`

## Specifying the Region for a Resource

Every time you create an Amazon EC2 resource, you can specify the region for the resource. You can specify the region for a resource using the AWS Management Console or the command line.

Note

Some AWS resources might not be available in all regions and Availability Zones. Ensure that you can create the resources you need in the desired regions or Availability Zone before launching an instance in a specific Availability Zone.

### To specify the region for a resource using the console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
2. Use the region selector in the navigation bar.

### To specify the default region using the command line

You can set the value of an environment variable to the desired regional endpoint

- AWS_DEFAULT_REGION (AWS CLI)
- Set-AWSDefaultRegion (AWS Tools for Windows PowerShell)

Alternatively, you can use the --region (AWS CLI) or -Region (AWS Tools for Windows PowerShell) command line option with each individual command. For example, --region us-east-2.

## Launching Instances in an Availability Zone

When you launch an instance, select a region that puts your instances closer to specific customers, or meets the legal or other requirements you have. By launching your instances in separate Availability Zones, you can protect your applications from the failure of a single location.

When you launch an instance, you can optionally specify an Availability Zone in the region that you are using. If you do not specify an Availability Zone, we select one for you. When you launch your initial instances, we recommend that you accept the default Availability Zone, because this enables us to select the best Availability Zone for you based on system health and available capacity. If you launch additional instances, only specify an Availability Zone if your new instances must be close to, or separated from, your running instances.

To specify an Availability Zone for your instance using the console

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
2. On the dashboard, choose Launch Instance.
3. Follow the directions for the wizard. On the Configure Instance Details page, do the following:

- [EC2-Classic] Select one of the Availability Zone options from the list, or select No Preference to enable us to select the best one for you.
							
- [EC2-VPC] Select one of the subnet options from the list, or select No preference (default subnet in any Availability Zone) to enable us to select the best one for you.
		
### To specify an Availability Zone for your instance using the AWS CLI

You can use the run-instances command with one of the following options:

- [EC2-Classic] --placement
- [EC2-VPC] --subnet-id

### To specify an Availability Zone for your instance using the AWS Tools for Windows PowerShell

You can use the New-EC2Instance command with one of the following options:

- [EC2-Classic] -AvailabilityZone
- [EC2-VPC] -SubnetId

## Migrating an Instance to Another Availability Zone

If you need to, you can migrate an instance from one Availability Zone to another. For example, if you are trying to modify the instance type of your instance and we can't launch an instance of the new instance type in the current Availability Zone, you could migrate the instance to an Availability Zone where we can launch an instance of that instance type.

The migration process involves creating an AMI from the original instance, launching an instance in the new Availability Zone, and updating the configuration of the new instance, as shown in the following procedure.

To migrate an instance to another Availability Zone

1. Create an AMI from the instance. The procedure depends on the operating system and the type of root device volume for the instance. For more information, see the documentation that corresponds to your operating system and root device volume:

- Creating an Amazon EBS-Backed Linux AMI
- Creating an Instance Store-Backed Linux AMI
- Creating an Amazon EBS-Backed Windows AMI
- Creating an Instance Store-Backed Windows AMI

2. [EC2-VPC] If you need to preserve the private IPv4 address of the instance, you must delete the subnet in the current Availability Zone and then create a subnet in the new Availability Zone with the same IPv4 address range as the original subnet. Note that you must terminate all instances in a subnet before you can delete it. Therefore, you should create AMIs from all the instances in your subnet so that you can move all instances in the current subnet to the new subnet.

3. Launch an instance from the AMI that you just created, specifying the new Availability Zone or subnet. You can use the same instance type as the original instance, or select a new instance type. For more information, see Launching Instances in an Availability Zone.

4. If the original instance has an associated Elastic IP address, associate it with the new instance. For more information, see Disassociating an Elastic IP Address and Reassociating it with a Different Instance.

5. If the original instance is a Reserved Instance, change the Availability Zone for your reservation. (If you also changed the instance type, you can also change the instance type for your reservation.) For more information, see Submitting Modification Requests.

6. (Optional) Terminate the original instance. For more information, see Terminating an Instance.

# Amazon EC2 Root Device Volume

When you launch an instance, the root device volume contains the image used to boot the instance. When we introduced Amazon EC2, all AMIs were backed by Amazon EC2 instance store, which means the root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3. After we introduced Amazon EBS, we introduced AMIs that are backed by Amazon EBS. This means that the root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot.

You can choose between AMIs backed by Amazon EC2 instance store and AMIs backed by Amazon EBS. We recommend that you use AMIs backed by Amazon EBS, because they launch faster and use persistent storage.

## Root Device Storage Concepts

You can launch an instance from either an instance store-backed AMI or an Amazon EBS-backed AMI. The description of an AMI includes which type of AMI it is; you'll see the root device referred to in some places as either ebs (for Amazon EBS-backed) or instance store (for instance store-backed). This is important because there are significant differences between what you can do with each type of AMI. For more information about these differences, see Storage for the Root Device.

### Instance Store-backed Instances

Instances that use instance stores for the root device automatically have one or more instance store volumes available, with one volume serving as the root device volume. When an instance is launched, the image that is used to boot the instance is copied to the root volume. Note that you can optionally use additional instance store volumes, depending on the instance type.

Any data on the instance store volumes persists as long as the instance is running, but this data is deleted when the instance is terminated (instance store-backed instances do not support the Stop action) or if it fails (such as if an underlying drive has issues).

After an instance store-backed instance fails or terminates, it cannot be restored. If you plan to use Amazon EC2 instance store-backed instances, we highly recommend that you distribute the data on your instance stores across multiple Availability Zones. You should also back up critical data on your instance store volumes to persistent storage on a regular basis.

### Amazon EBS-backed Instances

Instances that use Amazon EBS for the root device automatically have an Amazon EBS volume attached. When you launch an Amazon EBS-backed instance, we create an Amazon EBS volume for each Amazon EBS snapshot referenced by the AMI you use. You can optionally use other Amazon EBS volumes or instance store volumes, depending on the instance type.

An Amazon EBS-backed instance can be stopped and later restarted without affecting data stored in the attached volumes. There are various instance– and volume-related tasks you can do when an Amazon EBS-backed instance is in a stopped state. For example, you can modify the properties of the instance, you can change the size of your instance or update the kernel it is using, or you can attach your root volume to a different running instance for debugging or any other purpose.

If an Amazon EBS-backed instance fails, you can restore your session by following one of these methods:

- Stop and then start again (try this method first).
- Automatically snapshot all relevant volumes and create a new AMI. For more information, see Creating an Amazon EBS-Backed Linux AMI.
- Attach the volume to the new instance by following these steps:
  1. Create a snapshot of the root volume.
  2. Register a new AMI using the snapshot.
  3. Launch a new instance from the new AMI.
  4. Detach the remaining Amazon EBS volumes from the old instance.
  5. Reattach the Amazon EBS volumes to the new instance.

## Choosing an AMI by Root Device Type

The AMI that you specify when you launch your instance determines the type of root device volume that your instance has.

To choose an Amazon EBS-backed AMI using the console

1. Open the Amazon EC2 console.
2. In the navigation pane, choose AMIs.
3. From the filter lists, select the image type (such as Public images). In the search bar choose Platform to select the operating system (such as Amazon Linux), and Root Device Type to select EBS images.
4. (Optional) To get additional information to help you make your choice, choose the Show/Hide Columns icon, update the columns to display, and choose Close.
5. Choose an AMI and write down its AMI ID.

### To choose an instance store-backed AMI using the console

1. Open the Amazon EC2 console.
2. In the navigation pane, choose AMIs.
3. From the filter lists, select the image type (such as Public images). In the search bar, choose Platform to select the operating system (such as Amazon Linux), and Root Device Type to select Instance store.
4. (Optional) To get additional information to help you make your choice, choose the Show/Hide Columns icon, update the columns to display, and choose Close.
5. Choose an AMI and write down its AMI ID.

### To verify the type of the root device volume of an AMI using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

- describe-images (AWS CLI)
- Get-EC2Image (AWS Tools for Windows PowerShell)

## Determining the Root Device Type of Your Instance

To determine the root device type of an instance using the console

1. Open the Amazon EC2 console.
2. In the navigation pane, choose Instances, and select the instance.
3. Check the value of Root device type in the Description tab as follows:

  - If the value is ebs, this is an Amazon EBS-backed instance.
  - If the value is instance store, this is an instance store-backed instance.
  
### To determine the root device type of an instance using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

  - describe-instances (AWS CLI)
  - Get-EC2Instance (AWS Tools for Windows PowerShell)

## Changing the Root Device Volume to Persist

By default, the root device volume for an AMI backed by Amazon EBS is deleted when the instance terminates. To change the default behavior, set the DeleteOnTermination attribute to false using a block device mapping.

### Changing the Root Volume to Persist Using the Console

Using the console, you can change the DeleteOnTermination attribute when you launch an instance. To change this attribute for a running instance, you must use the command line.

#### To change the root device volume of an instance to persist at launch using the console
1. Open the Amazon EC2 console.
2. From the Amazon EC2 console dashboard, choose Launch Instance.
3. On the Choose an Amazon Machine Image (AMI) page, select the AMI to use and choose Select.
4. Follow the wizard to complete the Choose an Instance Type and Configure Instance Details pages.
5. On the Add Storage page, deselect Delete On Termination for the root volume.
6. Complete the remaining wizard pages, and then choose Launch.

You can verify the setting by viewing details for the root device volume on the instance's details pane. Next to Block devices, choose the entry for the root device volume. By default, Delete on termination is True. If you change the default behavior, Delete on termination is False.

### Changing the Root Volume of an Instance to Persist Using the AWS CLI

Using the AWS CLI, you can change the DeleteOnTermination attribute when you launch an instance or while the instance is running.

#### Example at Launch

Use the run-instances command to preserve the root volume by including a block device mapping that sets its DeleteOnTermination attribute for to false.

`aws ec2 run-instances --block-device-mappings file://mapping.json other parameters...
Specify the following in mapping.json.`

```json
[
  {
    "DeviceName": "/dev/sda1",
    "Ebs": {
        "DeleteOnTermination": false
    }
  }
]
```
You can confirm that DeleteOnTermination is false by using the describe-instances command and looking for the BlockDeviceMappings entry for the device in the command output, as shown here.

```json
  "BlockDeviceMappings": [
    {
        "DeviceName": "/dev/sda1",
        "Ebs": {
            "Status": "attached",
            "DeleteOnTermination": false,
            "VolumeId": "vol-1234567890abcdef0",
            "AttachTime": "2013-07-19T02:42:39.000Z"
        }
    }              
```

#### Example While the Instance is Running

Use the modify-instance-attribute command to preserve the root volume by including a block device mapping that sets its DeleteOnTermination attribute to false.


`aws ec2 modify-instance-attribute --instance-id i-1234567890abcdef0 --block-device-mappings file://mapping.json`

Specify the following in mapping.json.

```json
[
  {
    "DeviceName": "/dev/sda1",
    "Ebs" : {
        "DeleteOnTermination": false
    }
  }
]
```

Setting Up with Amazon EC2

If you've already signed up for Amazon Web Services (AWS), you can start using Amazon EC2 immediately. You can open the Amazon EC2 console, choose Launch Instance, and follow the steps in the launch wizard to launch your first instance.

If you haven't signed up for AWS yet, or if you need assistance launching your first instance, complete the following tasks to get set up to use Amazon EC2:

Sign Up for AWS

Create an IAM User

Create a Key Pair

Create a Virtual Private Cloud (VPC)

Create a Security Group

Sign Up for AWS

When you sign up for Amazon Web Services (AWS), your AWS account is automatically signed up for all services in AWS, including Amazon EC2. You are charged only for the services that you use.

With Amazon EC2, you pay only for what you use. If you are a new AWS customer, you can get started with Amazon EC2 for free. For more information, see AWS Free Tier.

If you have an AWS account already, skip to the next task. If you don't have an AWS account, use the following procedure to create one.

To create an AWS account

Open https://aws.amazon.com/, and then choose Create an AWS Account.

Follow the online instructions.

Part of the sign-up procedure involves receiving a phone call and entering a PIN using the phone keypad.

Note your AWS account number, because you'll need it for the next task.

Create an IAM User

Services in AWS, such as Amazon EC2, require that you provide credentials when you access them, so that the service can determine whether you have permission to access its resources. The console requires your password. You can create access keys for your AWS account to access the command line interface or API. However, we don't recommend that you access AWS using the credentials for your AWS account; we recommend that you use AWS Identity and Access Management (IAM) instead. Create an IAM user, and then add the user to an IAM group with administrative permissions or and grant this user administrative permissions. You can then access AWS using a special URL and the credentials for the IAM user.

If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console. If you aren't familiar with using the console, see Working with the AWS Management Console for an overview.

To create an IAM user for yourself and add the user to an Administrators group

Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.

In the navigation pane, choose Users, and then choose Add user.

For User name, type a user name, such as Administrator. The name can consist of letters, digits, and the following characters: plus (+), equal (=), comma (,), period (.), at (@), underscore (_), and hyphen (-). The name is not case sensitive and can be a maximum of 64 characters in length.

Select the check box next to AWS Management Console access, select Custom password, and then type the new user's password in the text box. You can optionally select Require password reset to force the user to select a new password the next time the user signs in.

Choose Next: Permissions.

On the Set permissions for user page, choose Add user to group.

Choose Create group.

In the Create group dialog box, type the name for the new group. The name can consist of letters, digits, and the following characters: plus (+), equal (=), comma (,), period (.), at (@), underscore (_), and hyphen (-). The name is not case sensitive and can be a maximum of 128 characters in length.

For Filter, choose Job function.

In the policy list, select the check box for AdministratorAccess. Then choose Create group.

Back in the list of groups, select the check box for your new group. Choose Refresh if necessary to see the group in the list.

Choose Next: Review to see the list of group memberships to be added to the new user. When you are ready to proceed, choose Create user.

You can use this same process to create more groups and users, and to give your users access to your AWS account resources. To learn about using policies to restrict users' permissions to specific AWS resources, go to Access Management and Example Policies for Administering AWS Resources.

To sign in as this new IAM user, sign out of the AWS console, then use the following URL, where your_aws_account_id is your AWS account number without the hyphens (for example, if your AWS account number is 1234-5678-9012, your AWS account ID is 123456789012):

https://your_aws_account_id.signin.aws.amazon.com/console/
Enter the IAM user name (not your email address) and password that you just created. When you're signed in, the navigation bar displays "your_user_name @ your_aws_account_id".

If you don't want the URL for your sign-in page to contain your AWS account ID, you can create an account alias. From the IAM console, choose Dashboard in the navigation pane. From the dashboard, choose Customize and enter an alias such as your company name. To sign in after you create an account alias, use the following URL:

https://your_account_alias.signin.aws.amazon.com/console/
To verify the sign-in link for IAM users for your account, open the IAM console and check under IAM users sign-in link on the dashboard.

For more information about IAM, see IAM and Amazon EC2.

Create a Key Pair

AWS uses public-key cryptography to secure the login information for your instance. A Linux instance has no password; you use a key pair to log in to your instance securely. You specify the name of the key pair when you launch your instance, then provide the private key when you log in using SSH.

If you haven't created a key pair already, you can create one using the Amazon EC2 console. Note that if you plan to launch instances in multiple regions, you'll need to create a key pair in each region. For more information about regions, see Regions and Availability Zones.

To create a key pair

Sign in to AWS using the URL that you created in the previous section.

From the AWS dashboard, choose EC2 to open the Amazon EC2 console.

From the navigation bar, select a region for the key pair. You can select any region that's available to you, regardless of your location. However, key pairs are specific to a region; for example, if you plan to launch an instance in the US West (Oregon) Region, you must create a key pair for the instance in the US West (Oregon) Region.


						Select a region
					
In the navigation pane, under NETWORK & SECURITY, choose Key Pairs.

Tip
The navigation pane is on the left side of the console. If you do not see the pane, it might be minimized; choose the arrow to expand the pane. You may have to scroll down to see the Key Pairs link.

						Open the key pairs page
					
Choose Create Key Pair.

Enter a name for the new key pair in the Key pair name field of the Create Key Pair dialog box, and then choose Create. Use a name that is easy for you to remember, such as your IAM user name, followed by -key-pair, plus the region name. For example, me-key-pair-uswest2.

The private key file is automatically downloaded by your browser. The base file name is the name you specified as the name of your key pair, and the file name extension is .pem. Save the private key file in a safe place.

Important
This is the only chance for you to save the private key file. You'll need to provide the name of your key pair when you launch an instance and the corresponding private key each time you connect to the instance.
If you will use an SSH client on a Mac or Linux computer to connect to your Linux instance, use the following command to set the permissions of your private key file so that only you can read it.

Copy
chmod 400 your_user_name-key-pair-region_name.pem
For more information, see Amazon EC2 Key Pairs.

To connect to your instance using your key pair

To connect to your Linux instance from a computer running Mac or Linux, you'll specify the .pem file to your SSH client with the -i option and the path to your private key. To connect to your Linux instance from a computer running Windows, you can use either MindTerm or PuTTY. If you plan to use PuTTY, you'll need to install it and use the following procedure to convert the .pem file to a .ppk file.

(Optional) To prepare to connect to a Linux instance from Windows using PuTTY

Download and install PuTTY from http://www.chiark.greenend.org.uk/~sgtatham/putty/. Be sure to install the entire suite.

Start PuTTYgen (for example, from the Start menu, choose All Programs > PuTTY > PuTTYgen).

Under Type of key to generate, choose SSH-2 RSA.


						SSH-2 RSA key in PuTTYgen
					
Choose Load. By default, PuTTYgen displays only files with the extension .ppk. To locate your .pem file, select the option to display files of all types.


						Select all file types
					
Select the private key file that you created in the previous procedure and choose Open. Choose OK to dismiss the confirmation dialog box.

Choose Save private key. PuTTYgen displays a warning about saving the key without a passphrase. Choose Yes.

Specify the same name for the key that you used for the key pair. PuTTY automatically adds the .ppk file extension.

Create a Virtual Private Cloud (VPC)

Amazon VPC enables you to launch AWS resources into a virtual network that you've defined. If you have a default VPC, you can skip this section and move to the next task, Create a Security Group. To determine whether you have a default VPC, see Supported Platforms in the Amazon EC2 Console. Otherwise, you can create a nondefault VPC in your account using the steps below.

Important
If your account supports EC2-Classic in a region, then you do not have a default VPC in that region. T2 instances must be launched into a VPC.
To create a nondefault VPC

Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

From the navigation bar, select a region for the VPC. VPCs are specific to a region, so you should select the same region in which you created your key pair.

On the VPC dashboard, choose Start VPC Wizard.

On the Step 1: Select a VPC Configuration page, ensure that VPC with a Single Public Subnet is selected, and choose Select.

On the Step 2: VPC with a Single Public Subnet page, enter a friendly name for your VPC in the VPC name field. Leave the other default configuration settings, and choose Create VPC. On the confirmation page, choose OK.

For more information about Amazon VPC, see What is Amazon VPC? in the Amazon VPC User Guide.

Create a Security Group

Security groups act as a firewall for associated instances, controlling both inbound and outbound traffic at the instance level. You must add rules to a security group that enable you to connect to your instance from your IP address using SSH. You can also add rules that allow inbound and outbound HTTP and HTTPS access from anywhere.

Note that if you plan to launch instances in multiple regions, you'll need to create a security group in each region. For more information about regions, see Regions and Availability Zones.

Prerequisites

You'll need the public IPv4 address of your local computer. The security group editor in the Amazon EC2 console can automatically detect the public IPv4 address for you. Alternatively, you can use the search phrase "what is my IP address" in an Internet browser, or use the following service: Check IP. If you are connecting through an Internet service provider (ISP) or from behind a firewall without a static IP address, you need to find out the range of IP addresses used by client computers.

To create a security group with least privilege

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Tip
Alternatively, you can use the Amazon VPC console to create a security group. However, the instructions in this procedure don't match the Amazon VPC console. Therefore, if you switched to the Amazon VPC console in the previous section, either switch back to the Amazon EC2 console and use these instructions, or use the instructions in Set Up a Security Group for Your VPC in the Amazon VPC Getting Started Guide.
From the navigation bar, select a region for the security group. Security groups are specific to a region, so you should select the same region in which you created your key pair.


						Select a region
					
Choose Security Groups in the navigation pane.

Choose Create Security Group.

Enter a name for the new security group and a description. Use a name that is easy for you to remember, such as your IAM user name, followed by _SG_, plus the region name. For example, me_SG_uswest2.

In the VPC list, select your VPC. If you have a default VPC, it's the one that is marked with an asterisk (*).

Note
If your account supports EC2-Classic, select the VPC that you created in the previous task.
On the Inbound tab, create the following rules (choose Add Rule for each new rule), and then choose Create:

Choose HTTP from the Type list, and make sure that Source is set to Anywhere (0.0.0.0/0).
Choose HTTPS from the Type list, and make sure that Source is set to Anywhere (0.0.0.0/0).
Choose SSH from the Type list. In the Source box, choose My IP to automatically populate the field with the public IPv4 address of your local computer. Alternatively, choose Custom and specify the public IPv4 address of your computer or network in CIDR notation. To specify an individual IP address in CIDR notation, add the routing suffix /32, for example, 203.0.113.25/32. If your company allocates addresses from a range, specify the entire range, such as 203.0.113.0/24.
Warning
For security reasons, we don't recommend that you allow SSH access from all IPv4 addresses (0.0.0.0/0) to your instance, except for testing purposes and only for a short time.
For more information, see Amazon EC2 Security Groups for Linux Instances.

Getting Started with Amazon EC2 Linux Instances

Let's get started with Amazon Elastic Compute Cloud (Amazon EC2) by launching, connecting to, and using a Linux instance. An instance is a virtual server in the AWS cloud. With Amazon EC2, you can set up and configure the operating system and applications that run on your instance.

When you sign up for AWS, you can get started with Amazon EC2 for free using the AWS Free Tier. If you created your AWS account less than 12 months ago, and have not already exceeded the free tier benefits for Amazon EC2, it will not cost you anything to complete this tutorial, because we help you select options that are within the free tier benefits. Otherwise, you'll incur the standard Amazon EC2 usage fees from the time that you launch the instance until you terminate the instance (which is the final task of this tutorial), even if it remains idle.

Contents

Overview
Prerequisites
Step 1: Launch an Instance
Step 2: Connect to Your Instance
Step 3: Clean Up Your Instance
Next Steps
Overview

The instance is an Amazon EBS-backed instance (meaning that the root volume is an EBS volume). You can either specify the Availability Zone in which your instance runs, or let Amazon EC2 select an Availability Zone for you. When you launch your instance, you secure it by specifying a key pair and security group. When you connect to your instance, you must specify the private key of the key pair that you specified when launching your instance.


					An Amazon EBS-backed instance with an additional Amazon Elastic Block Store (EBS) volume
				
Tasks

To complete this tutorial, perform the following tasks:

Launch an Instance

Connect to Your Instance

Clean Up Your Instance

Related Tutorials

If you'd prefer to launch a Windows instance, see this tutorial in the Amazon EC2 User Guide for Windows Instances: Getting Started with Amazon EC2 Windows Instances.
If you'd prefer to use the command line, see this tutorial in the AWS Command Line Interface User Guide: Using Amazon EC2 through the AWS CLI.
Prerequisites

Before you begin, be sure that you've completed the steps in Setting Up with Amazon EC2.

Step 1: Launch an Instance

You can launch a Linux instance using the AWS Management Console as described in the following procedure. This tutorial is intended to help you launch your first instance quickly, so it doesn't cover all possible options. For more information about the advanced options, see Launching an Instance.

To launch an instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the console dashboard, choose Launch Instance.

The Choose an Amazon Machine Image (AMI) page displays a list of basic configurations, called Amazon Machine Images (AMIs), that serve as templates for your instance. Select the HVM edition of the Amazon Linux AMI. Notice that this AMI is marked "Free tier eligible."

On the Choose an Instance Type page, you can select the hardware configuration of your instance. Select the t2.micro type, which is selected by default. Notice that this instance type is eligible for the free tier.

Note
T2 instances, such as t2.micro, must be launched into a VPC. If your AWS account supports EC2-Classic and you do not have a VPC in the selected region, the launch wizard creates a VPC for you and you can continue to the next step. Otherwise, the Review and Launch button is disabled and you must choose Next: Configure Instance Details and follow the directions to select a subnet.
Choose Review and Launch to let the wizard complete the other configuration settings for you.

On the Review Instance Launch page, under Security Groups, you'll see that the wizard created and selected a security group for you. You can use this security group, or alternatively you can select the security group that you created when getting set up using the following steps:

Choose Edit security groups.

On the Configure Security Group page, ensure that Select an existing security group is selected.

Select your security group from the list of existing security groups, and then choose Review and Launch.

On the Review Instance Launch page, choose Launch.

When prompted for a key pair, select Choose an existing key pair, then select the key pair that you created when getting set up.

Alternatively, you can create a new key pair. Select Create a new key pair, enter a name for the key pair, and then choose Download Key Pair. This is the only chance for you to save the private key file, so be sure to download it. Save the private key file in a safe place. You'll need to provide the name of your key pair when you launch an instance and the corresponding private key each time you connect to the instance.

Warning
Don't select the Proceed without a key pair option. If you launch your instance without a key pair, then you can't connect to it.
When you are ready, select the acknowledgement check box, and then choose Launch Instances.

A confirmation page lets you know that your instance is launching. Choose View Instances to close the confirmation page and return to the console.

On the Instances screen, you can view the status of the launch. It takes a short time for an instance to launch. When you launch an instance, its initial state is pending. After the instance starts, its state changes to running and it receives a public DNS name. (If the Public DNS (IPv4) column is hidden, choose the Show/Hide icon in the top right corner of the page and then select Public DNS (IPv4).)

It can take a few minutes for the instance to be ready so that you can connect to it. Check that your instance has passed its status checks; you can view this information in the Status Checks column.

Step 2: Connect to Your Instance

There are several ways to connect to a Linux instance. In this procedure, you'll connect using your browser. Alternatively, you can connect using PuTTY or an SSH client. It's also assumed that you followed the steps earlier and launched an instance from an Amazon Linux AMI, which has a specific user name. Other Linux distributions may use a different user name. For more information, see Connecting to Your Linux Instance from Windows Using PuTTY or Connecting to Your Linux Instance Using SSH.

Important
You can't connect to your instance unless you launched it with a key pair for which you have the .pem file and you launched it with a security group that allows SSH access. If you can't connect to your instance, see Troubleshooting Connecting to Your Instance for assistance.
To connect to your Linux instance using a web browser

You must have Java installed and enabled in the browser. If you don't have Java already, you can contact your system administrator to get it installed, or follow the steps outlined in the following pages: Install Java and Enable Java in your web browser.

From the Amazon EC2 console, choose Instances in the navigation pane.

Select the instance, and then choose Connect.

Choose A Java SSH client directly from my browser (Java required).

Amazon EC2 automatically detects the public DNS name of your instance and populates Public DNS for you. It also detects the key pair that you specified when you launched the instance. Complete the following, and then choose Launch SSH Client.

In User name, enter ec2-user.

In Private key path, enter the fully qualified path to your private key (.pem) file, including the key pair name.

(Optional) Choose Store in browser cache to store the location of the private key in your browser cache. This enables Amazon EC2 to detect the location of the private key in subsequent browser sessions, until you clear your browser's cache.

If necessary, choose Yes to trust the certificate, and choose Run to run the MindTerm client.

If this is your first time running MindTerm, a series of dialog boxes asks you to accept the license agreement, confirm setup for your home directory, and confirm setup of the known hosts directory. Confirm these settings.

A dialog prompts you to add the host to your set of known hosts. If you do not want to store the host key information on your local computer, choose No.

A window opens and you are connected to your instance.

Note
If you chose No in the previous step, you'll see the following message, which is expected:
Verification of server key disabled in this session.
Step 3: Clean Up Your Instance

After you've finished with the instance that you created for this tutorial, you should clean up by terminating the instance. If you want to do more with this instance before you clean up, see Next Steps.

Important
Terminating an instance effectively deletes it; you can't reconnect to an instance after you've terminated it.
If you launched an instance that is not within the AWS Free Tier, you'll stop incurring charges for that instance as soon as the instance status changes to shutting down or terminated. If you'd like to keep your instance for later, but not incur charges, you can stop the instance now and then start it again later. For more information, see Stopping Instances.

To terminate your instance

In the navigation pane, choose Instances. In the list of instances, select the instance.

Choose Actions, then Instance State, and then choose Terminate.

Choose Yes, Terminate when prompted for confirmation.

Amazon EC2 shuts down and terminates your instance. After your instance is terminated, it remains visible on the console for a short while, and then the entry is deleted.

Next Steps

After you start your instance, you might want to try some of the following exercises:

Learn how to remotely manage you EC2 instance using Run Command. For more information, see Tutorial: Remotely Manage Your Amazon EC2 Instances and Systems Manager Remote Management (Run Command).
Configure a CloudWatch alarm to notify you if your usage exceeds the Free Tier. For more information, see Create a Billing Alarm in the AWS Billing and Cost Management User Guide.
Add an EBS volume. For more information, see Creating an Amazon EBS Volume and Attaching an Amazon EBS Volume to an Instance.
Install the LAMP stack. For more information, see Tutorial: Installing a LAMP Web Server on Amazon Linux.

Best Practices for Amazon EC2

This checklist is intended to help you get the maximum benefit from and satisfaction with Amazon EC2.

Security and Network

Manage access to AWS resources and APIs using identity federation, IAM users, and IAM roles. Establish credential management policies and procedures for creating, distributing, rotating, and revoking AWS access credentials. For more information, see IAM Best Practices in the IAM User Guide.
Implement the least permissive rules for your security group. For more information, see Security Group Rules.
Regularly patch, update, and secure the operating system and applications on your instance. For more information about updating Amazon Linux, see Managing Software on Your Linux Instance. For more information about updating your Windows instance, see Updating Your Windows Instance in the Amazon EC2 User Guide for Windows Instances.
Launch your instances into a VPC instead of EC2-Classic. Note that if you created your AWS account after 2013-12-04, we automatically launch your instances into a VPC. For more information about the benefits, see Amazon EC2 and Amazon Virtual Private Cloud.
Storage

Understand the implications of the root device type for data persistence, backup, and recovery. For more information, see Storage for the Root Device.
Use separate Amazon EBS volumes for the operating system versus your data. Ensure that the volume with your data persists after instance termination. For more information, see Preserving Amazon EBS Volumes on Instance Termination.
Use the instance store available for your instance to store temporary data. Remember that the data stored in instance store is deleted when you stop or terminate your instance. If you use instance store for database storage, ensure that you have a cluster with a replication factor that ensures fault tolerance.
Resource Management

Use instance metadata and custom resource tags to track and identify your AWS resources. For more information, see Instance Metadata and User Data and Tagging Your Amazon EC2 Resources.
View your current limits for Amazon EC2. Plan to request any limit increases in advance of the time that you'll need them. For more information, see Amazon EC2 Service Limits.
Backup and Recovery

Regularly back up your EBS volumes using Amazon EBS snapshots, and create an Amazon Machine Image (AMI) from your instance to save the configuration as a template for launching future instances.
Deploy critical components of your application across multiple Availability Zones, and replicate your data appropriately.
Design your applications to handle dynamic IP addressing when your instance restarts. For more information, see Amazon EC2 Instance IP Addressing.
Monitor and respond to events. For more information, see Monitoring Amazon EC2.
Ensure that you are prepared to handle failover. For a basic solution, you can manually attach a network interface or Elastic IP address to a replacement instance. For more information, see Elastic Network Interfaces. For an automated solution, you can use Auto Scaling. For more information, see the Auto Scaling User Guide.
Regularly test the process of recovering your instances and Amazon EBS volumes if they fail.

