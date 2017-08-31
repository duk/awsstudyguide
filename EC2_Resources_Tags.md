# Resources and Tags

Amazon EC2 provides different resources that you can create and use. Some of these resources include images, instances, volumes, and snapshots. When you create a resource, we assign the resource a unique resource ID.

Some resources can be tagged with values that you define, to help you organize and identify them.

The following topics describe resources and tags, and how you can work with them.

Contents

Resource Locations
Resource IDs
Listing and Filtering Your Resources
Tagging Your Amazon EC2 Resources
Amazon EC2 Service Limits
Amazon EC2 Usage Reports

Resource Locations

Some resources can be used in all regions (global), and some resources are specific to the region or Availability Zone in which they reside.

Resource	Type	Description
AWS account
Global
You can use the same AWS account in all regions.
Key pairs
Global or Regional
The key pairs that you create using Amazon EC2 are tied to the region where you created them. You can create your own RSA key pair and upload it to the region in which you want to use it; therefore, you can make your key pair globally available by uploading it to each region.

For more information, see Amazon EC2 Key Pairs.
Amazon EC2 resource identifiers
Regional
Each resource identifier, such as an AMI ID, instance ID, EBS volume ID, or EBS snapshot ID, is tied to its region and can be used only in the region where you created the resource.
User-supplied resource names
Regional
Each resource name, such as a security group name or key pair name, is tied to its region and can be used only in the region where you created the resource. Although you can create resources with the same name in multiple regions, they aren't related to each other.
AMIs
Regional
An AMI is tied to the region where its files are located within Amazon S3. You can copy an AMI from one region to another. For more information, see Copying an AMI.
Elastic IP addresses
Regional
An Elastic IP address is tied to a region and can be associated only with an instance in the same region.
Security groups
Regional
A security group is tied to a region and can be assigned only to instances in the same region. You can't enable an instance to communicate with an instance outside its region using security group rules. Traffic from an instance in another region is seen as WAN bandwidth.
EBS snapshots
Regional
An EBS snapshot is tied to its region and can only be used to create volumes in the same region. You can copy a snapshot from one region to another. For more information, see Copying an Amazon EBS Snapshot.
EBS volumes
Availability Zone
An Amazon EBS volume is tied to its Availability Zone and can be attached only to instances in the same Availability Zone.
Instances
Availability Zone
An instance is tied to the Availability Zones in which you launched it. However, note that its instance ID is tied to the region.

Resource IDs

When resources are created, we assign each resource a unique resource ID. You can use resource IDs to find your resources in the Amazon EC2 console. If you are using a command line tool or the Amazon EC2 API to work with Amazon EC2, resource IDs are required for certain commands. For example, if you are using the stop-instances AWS CLI command to stop an instance, you must specify the instance ID in the command.

Resource ID Length

A resource ID takes the form of a resource identifier (such as snap for a snapshot) followed by a hyphen and a unique combination of letters and numbers. Starting in January 2016, we're gradually introducing longer length IDs for some Amazon EC2 and Amazon EBS resource types. The length of the alphanumeric character combination was in an 8-character format; the new IDs are in a 17-character format, for example, i-1234567890abcdef0 for an instance ID.

Supported resource types will have an opt-in period, during which you can enable the longer ID format. After you've enabled longer IDs for a resource type, any new resources that you create are created with a longer ID unless you explicitly disable the longer ID format. A resource ID does not change after it's created; therefore, your existing resources with shorter IDs are not affected. Similarly, if you disable longer IDs for a resource type, any resources that you created with the longer IDs are not affected.

All supported resource types will have a deadline date, after which all new resources of this type default to the longer ID format, and you can no longer disable the longer ID format. You can enable or disable longer IDs per IAM user and IAM role. By default, an IAM user or role defaults to the same settings as the root user.

Depending on when you created your account, supported resource types may default to using longer IDs. However, you can opt out of using longer IDs until the deadline date for that resource type. For more information, see Longer EC2 and EBS Resource IDs in the Amazon EC2 FAQs.

Resources created with longer IDs are visible to all IAM users and IAM roles, regardless of individual settings and provided that they have permissions to view the relevant resource types.

Topics

Working with Longer IDs
Controlling Access to Longer ID Settings
Working with Longer IDs

You can view and modify the longer ID settings for yourself, or for a different IAM user, IAM role, or the root user of the account.

Topics

Viewing and Modifying Your Longer ID Settings
Viewing and Modifying Longer ID Settings for Users or Roles
Viewing and Modifying Your Longer ID Settings

You can use the Amazon EC2 console or the AWS CLI to view the resource types that support long IDs, and enable or disable the longer ID format for yourself. The procedures in this section apply to the IAM user or IAM role that's logged into the console or that makes the request; they do not apply to the entire AWS account.

To view and modify the longer ID settings using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation bar at the top of the screen, the current region is displayed. Select the region for which you want to view or change the longer ID settings. Settings are not shared between regions.

From the dashboard, under Account Attributes, choose Resource ID length management. The resource types that support longer IDs are listed. The date at which you're automatically switched over to using longer IDs for each resource type is displayed in the Deadline column.

To enable the longer ID format for a supported resource type, choose the check box for the Use Longer IDs column. To disable the longer ID format, clear the check box.

Important
If you’re logged in as the root user, these settings apply to the entire account, unless an IAM user or role logs in and explicitly overrides these settings for themselves. Resources created with longer IDs are visible to all IAM users, regardless of individual settings and provided that they have permissions to view the relevant resource types.
To view and modify longer ID settings using the AWS CLI

To view the longer ID settings of all supported resources, use the describe-id-format AWS CLI command:

Copy
aws ec2 describe-id-format

{
    "Statuses": [
        {
            "Deadline": "2016-11-01T13:00:00.000Z",
            "UseLongIds": false,
            "Resource": "instance"
        },
        {
            "Deadline": "2016-11-01T13:00:00.000Z",
            "UseLongIds": true,
            "Resource": "reservation"
        },
        {
            "Deadline": "2016-11-01T13:00:00.000Z",
            "UseLongIds": false,
            "Resource": "volume"
        },
        {
            "Deadline": "2016-11-01T13:00:00.000Z",
            "UseLongIds": false,
            "Resource": "snapshot"
        }
    ]
}
The results apply to the IAM user, IAM role, or root user that makes the request; they do not apply to the entire AWS account. The results above indicate that the instance, reservation, volume, and snapshot resource types can be enabled or disabled for longer IDs; the reservation resource is already enabled. The Deadline field indicates the date (in UTC) at which you will be automatically switched over to using longer IDs for that resource. If a deadline date is not yet available, this value is not returned.

To enable longer IDs for a specified resource, use the modify-id-format AWS CLI command:

Copy
aws ec2 modify-id-format --resource resource-type --use-long-ids
To disable longer IDs for a specified resource, use the modify-id-format AWS CLI command:

Copy
aws ec2 modify-id-format --resource resource-type --no-use-long-ids
If you’re using these actions as the root user, then these settings apply to the entire account, unless an IAM user or role explicitly overrides these settings for themselves. These commands are per-region only. To modify the settings for other regions, use the --region parameter in the command.

Note
In the 2015-10-01 version of the Amazon EC2 API, if you call describe-id-format or modify-id-format using IAM role credentials, the results apply to the entire AWS account, and not the specific IAM role. In the current version of the Amazon EC2 API, the results apply to the IAM role only.
Alternatively, you can use the following commands:

To describe the ID format

DescribeIdFormat (Amazon EC2 API)
Get-EC2IdFormat (AWS Tools for Windows PowerShell)
To modify the ID format

ModifyIdFormat (Amazon EC2 API)
Edit-EC2IdFormat (AWS Tools for Windows PowerShell)
Viewing and Modifying Longer ID Settings for Users or Roles

You can view supported resource types and enable the longer ID settings for a specific IAM user, IAM role, or the root user of your account by using the describe-identity-id-format and modify-identity-id-format AWS CLI commands. To use these commands, you must specify the ARN of an IAM user, IAM role, or root account user in the request. For example, the ARN of the role 'EC2Role' in account 123456789012 is arn:aws:iam::123456789012:role/EC2Role. For more information, see Principal in the IAM User Guide.

To view the longer ID settings of all supported resources for a specific IAM user or IAM role, use the following AWS CLI command:

Copy
aws ec2 describe-identity-id-format --principal-arn arn-of-iam-principal
To enable the longer ID settings for a resource type for a specific IAM user or IAM role, use the following AWS CLI command:

Copy
aws ec2 modify-identity-id-format --principal-arn arn-of-iam-principal --resource resource-type --use-long-ids
These commands apply to the ARN specified in the request, they do not apply to the IAM user, IAM role, or root user that made the request.

You can enable the longer ID settings for all IAM users, IAM roles, and the root user of your account by using the following AWS CLI command:

Copy
aws ec2 modify-identity-id-format --principal-arn all --resource resource-type --use-long-ids
Alternatively, you can use the following commands:

To describe the ID format

DescribeIdentityIdFormat (Amazon EC2 API)
Get-EC2IdentityIdFormat (AWS Tools for Windows PowerShell)
To modify the ID format

ModifyIdentityIdFormat (Amazon EC2 API)
Edit-EC2IdentityIdFormat (AWS Tools for Windows PowerShell)
Controlling Access to Longer ID Settings

By default, IAM users and roles do not have permission to use the ec2:DescribeIdFormat, ec2:DescribeIdentityIdFormat, ec2:ModifyIdFormat, and ec2:ModifyIdentityIdFormat actions unless they're explicitly granted permission through their associated IAM policies. For example, an IAM role may have permission to use all Amazon EC2 actions through an "Action": "ec2:*" element in the policy statement.

To prevent IAM users and roles from viewing or modifying the longer resource ID settings for themselves or other users and roles in your account, ensure that the IAM policy contains the following statement:

Copy
{
  "Version": "2012-10-17", 
  "Statement": [ 
    { 
      "Effect": "Deny",
      "Action": [
        "ec2:ModifyIdFormat", 
        "ec2:DescribeIdFormat", 
        "ec2:ModifyIdentityIdFormat", 
        "ec2:DescribeIdentityIdFormat" 
      ],
      "Resource": "*"
    }
  ] 
}   
We do not support resource-level permissions for the ec2:DescribeIdFormat, ec2:DescribeIdentityIdFormat, ec2:ModifyIdFormat, and ec2:ModifyIdentityIdFormat actions.

Listing and Filtering Your Resources

You can get a list of some types of resource using the Amazon EC2 console. You can get a list of each type of resource using its corresponding command or API action. If you have many resources, you can filter the results to include only the resources that match certain criteria.

Contents

Advanced Search
Listing Resources Using the Console
Filtering Resources Using the Console
Listing and Filtering Using the CLI and API
Advanced Search

Advanced search allows you to search using a combination of filters to achieve precise results. You can filter by keywords, user-defined tag keys, and predefined resource attributes.

The specific search types available are:

Search by keyword
To search by keyword, type or paste what you’re looking for in the search box, and then choose Enter. For example, to search for a specific instance, you can type the instance ID.
Search by fields
You can also search by fields, tags, and attributes associated with a resource. For example, to find all instances in the stopped state:
In the search box, start typing Instance State. As you type, you'll see a list of suggested fields.
Select Instance State from the list.
Select Stopped from the list of suggested values.
To further refine your list, select the search box for more search options.
Advanced search
You can create advanced queries by adding multiple filters. For example, you can search by tags and see instances for the Flying Mountain project running in the Production stack, and then search by attributes to see all t2.micro instances, or all instances in us-west-2a, or both.
Inverse search
You can search for resources that do not match a specified value. For example, to list all instances that are not terminated, search by the Instance State field, and prefix the Terminated value with an exclamation mark (!).
Partial search
When searching by field, you can also enter a partial string to find all resources that contain the string in that field. For example, search by Instance Type, and then type t2 to find all t2.micro, t2.small or t2.medium instances.
Regular expression
Regular expressions are useful when you need to match the values in a field with a specific pattern. For example, search by the Name tag, and then type ^s.* to see all instances with a Name tag that starts with an 's'. Regular expression search is not case-sensitive.
After you have the precise results of your search, you can bookmark the URL for easy reference. In situations where you have thousands of instances, filters and bookmarks can save you a great deal of time; you don’t have to run searches repeatedly.

Combining search filters

In general, multiple filters with the same key field (for example, tag:Name, search, Instance State) are automatically joined with OR. This is intentional, as the vast majority of filters would not be logical if they were joined with AND. For example, you would get zero results for a search on Instance State=running AND Instance State=stopped. In many cases, you can granulate the results by using complementary search terms on different key fields, where the AND rule is automatically applied instead. If you search for tag: Name:=All values and tag:Instance State=running, you get search results that contain both those criteria. To fine-tune your results, simply remove one filter in the string until the results fit your requirements.

Listing Resources Using the Console

You can view the most common Amazon EC2 resource types using the console. To view additional resources, use the command line interface or the API actions.

To list EC2 resources using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose the option that corresponds to the resource, such as AMIs or Instances.


                     Amazon EC2 console navigation pane
                  
The page displays all the available resources.

Filtering Resources Using the Console

You can perform filtering and sorting of the most common resource types using the Amazon EC2 console. For example, you can use the search bar on the instances page to sort instances by tags, attributes, or keywords.

You can also use the search field on each page to find resources with specific attributes or values. You can use regular expressions to search on partial or multiple strings. For example, to find all instances that are using the MySG security group, enter MySG in the search field. The results will include any values that contain MySG as a part of the string, such as MySG2 and MySG3. To limit your results to MySG only, enter \bMySG\b in the search field. To list all the instances whose type is either m1.small or m1.large, enter m1.small|m1.large in the search field.

To list volumes in the us-east-1b Availability Zone with a status of available

In the navigation pane, choose Volumes.

Click on the search box, select Attachment Status from the menu, and then select Detached. (A detached volume is available to be attached to an instance in the same Availability Zone.)

Click on the search box again, select State, and then select Available.

Click on the search box again, select Availability Zone, and then select us-east-1b.

Any volumes that meet this criteria are displayed.

To list public 64-bit Linux AMIs backed by Amazon EBS

In the navigation pane, choose AMIs.

In the Filter pane, select Public images, EBS images, and then your Linux distribution from the Filter lists.

Type x86_64 in the search field.

Any AMIs that meet this criteria are displayed.

Listing and Filtering Using the CLI and API

Each resource type has a corresponding CLI command or API request that you use to list resources of that type. For example, you can list Amazon Machine Images (AMI) using ec2-describe-images or DescribeImages. The response contains information for all your resources.

The resulting lists of resources can be long, so you might want to filter the results to include only the resources that match certain criteria. You can specify multiple filter values, and you can also specify multiple filters. For example, you can list all the instances whose type is either m1.small or m1.large, and that have an attached EBS volume that is set to delete when the instance terminates. The instance must match all your filters to be included in the results.

You can also use wildcards with the filter values. An asterisk (*) matches zero or more characters, and a question mark (?) matches exactly one character. For example, you can use *database* as a filter value to get all EBS snapshots that include database in the description. If you were to specify database as the filter value, then only snapshots whose description equals database would be returned. Filter values are case sensitive. We support only exact string matching, or substring matching (with wildcards). If a resulting list of resources is long, using an exact string filter may return the response faster.

Your search can include the literal values of the wildcard characters; you just need to escape them with a backslash before the character. For example, a value of \*amazon\?\\ searches for the literal string *amazon?\.

For a list of supported filters per Amazon EC2 resource, see the relevant documentation:

For the AWS CLI, see the relevant describe command in the AWS Command Line Interface Reference.
For Windows PowerShell, see the relevant Get command in the AWS Tools for Windows PowerShell Reference.
For the Query API, see the relevant Describe API action in the Amazon EC2 API Reference.
Note
The response of a describe action includes information about any tags that are applied to your resources. However, when describing multiple resources, the results may be eventually consistent and may not return all of your tags. To confirm the tags for a resource, describe a single resource.

Tagging Your Amazon EC2 Resources

To help you manage your instances, images, and other Amazon EC2 resources, you can optionally assign your own metadata to each resource in the form of tags. This topic describes tags and shows you how to create them.

Contents

Tag Basics
Tagging Your Resources
Tag Restrictions
Tagging Your Resources for Billing
Working with Tags Using the Console
Working with Tags Using the CLI or API
Tag Basics

Tags enable you to categorize your AWS resources in different ways, for example, by purpose, owner, or environment. This is useful when you have many resources of the same type — you can quickly identify a specific resource based on the tags you've assigned to it. Each tag consists of a key and an optional value, both of which you define. For example, you could define a set of tags for your account's Amazon EC2 instances that helps you track each instance's owner and stack level. We recommend that you devise a set of tag keys that meets your needs for each resource type. Using a consistent set of tag keys makes it easier for you to manage your resources. You can search and filter the resources based on the tags you add.

The following diagram illustrates how tagging works. In this example, you've assigned two tags to each of your instances, one called Owner and another called Stack. Each of the tags also has an associated value.


					Tag example
				
Tags don't have any semantic meaning to Amazon EC2 and are interpreted strictly as a string of characters. Also, tags are not automatically assigned to your resources. You can edit tag keys and values, and you can remove tags from a resource at any time. You can set the value of a tag to an empty string, but you can't set the value of a tag to null. If you add a tag that has the same key as an existing tag on that resource, the new value overwrites the old value. If you delete a resource, any tags for the resource are also deleted.

You can work with tags using the AWS Management Console, the AWS CLI, and the Amazon EC2 API.

If you're using AWS Identity and Access Management (IAM), you can control which users in your AWS account have permission to create, edit, or delete tags. For more information, see Controlling Access to Amazon EC2 Resources.

Tagging Your Resources

You can tag most Amazon EC2 resources that already exist in your account. The table below lists the resources that support tagging.

If you're using the Amazon EC2 console, you can apply tags to resources by using the Tags tab on the relevant resource screen, or you can use the Tags screen. Some resource screens enable you to specify tags for a resource when you create the resource; for example, a tag with a key of Name and a value that you specify. In most cases, the console applies the tags immediately after the resource is created (rather than during resource creation). The console may organize resources according the Name tag, but this tag doesn't have any semantic meaning to the Amazon EC2 service.

If you're using the Amazon EC2 API, the AWS CLI, or an AWS SDK, you can use the CreateTags EC2 API action to apply tags to existing resources. Additionally, some resource-creating actions enable you to specify tags for a resource when the resource is created. If tags cannot be applied during resource creation, we roll back the resource creation process. This can help to ensure that resources are either created with tags or not created at all, and that no resources are left untagged at any time. By tagging resources at the time of creation, you can eliminate the need to run custom tagging scripts after resource creation.

The following table describes the Amazon EC2 resources that can be tagged, and the resources that can be tagged on creation.

Tagging Support for Amazon EC2 Resources

Resource	Supports tags	Supports tagging on creation (EC2 API, AWS CLI, AWS SDK)
AMI
Yes
No
Bundle task
No
No
Customer gateway
Yes
No
Dedicated Host
No
No
DHCP option
Yes
No
EBS snapshot
Yes
No
EBS volume
Yes
Yes
Egress-only Internet gateway
No
No
Elastic IP address
No
No
Instance
Yes
Yes
Instance store volume
N/A
N/A
Internet gateway
Yes
No
Key pair
No
No
NAT gateway
No
No
Network ACL
Yes
No
Network interface
Yes
No
Placement group
No
No
Reserved Instance
Yes
No
Reserved Instance listing
No
No
Route table	
Yes
No
Spot Instance request
Yes
No
Security group–EC2-Classic
Yes
No
Security group–VPC
Yes
No
Subnet
Yes
No
Virtual private gateway
Yes
No
VPC
Yes
No
VPC endpoint
No
No
VPC flow log
No
No
VPC peering connection
Yes
No
VPN connection
Yes
No
To tag your instances or volumes on creation, you can use the Amazon EC2 Launch Instances wizard in the Amazon EC2 console, the RunInstances Amazon EC2 API, or the CreateVolume Amazon EC2 API. You can tag your EBS volumes on creation using the Volumes screen in the Amazon EC2 console.

You can apply tag-based resource-level permissions to the CreateVolume and RunInstances Amazon EC2 API actions in your IAM policies to implement granular control over the users and groups that can tag resources on creation. Your resources are properly secured from creation—tags are applied immediately to your resources, therefore any tag-based resource-level permissions controlling the use of resources are immediately effective. Your resources can be tracked and reported on more accurately. You can enforce the use of tagging on new resources, and control which tag keys and values are set on your resources.

You can also apply resource-level permissions to the CreateTags and DeleteTags Amazon EC2 API actions in your IAM policies to control which tag keys and values are set on your existing resources. For more information, see Supported Resource-Level Permissions for Amazon EC2 API Actions and Example Policies for Working With the AWS CLI or an AWS SDK.

For more information about tagging your resources for billing, see Using Cost Allocation Tags in the AWS Billing and Cost Management User Guide.

Tag Restrictions

The following basic restrictions apply to tags:

Maximum number of tags per resource—50
Maximum key length—127 Unicode characters in UTF-8
Maximum value length—255 Unicode characters in UTF-8
Tag keys and values are case sensitive.
Do not use the aws: prefix in your tag names or values because it is reserved for AWS use. You can't edit or delete tag names or values with this prefix. Tags with this prefix do not count against your tags per resource limit.
If your tagging schema will be used across multiple services and resources, remember that other services may have restrictions on allowed characters. Generally allowed characters are: letters, spaces, and numbers representable in UTF-8, plus the following special characters: + - = . _ : / @.
You can't terminate, stop, or delete a resource based solely on its tags; you must specify the resource identifier. For example, to delete snapshots that you tagged with a tag key called DeleteMe, you must use the DeleteSnapshots action with the resource identifiers of the snapshots, such as snap-1234567890abcdef0.

You can tag public or shared resources, but the tags you assign are available only to your AWS account and not to the other accounts sharing the resource.

You can't tag all resources. For more information, see Tagging Support for Amazon EC2 Resources.

Tagging Your Resources for Billing

You can use tags to organize your AWS bill to reflect your own cost structure. To do this, sign up to get your AWS account bill with tag key values included. For more information about setting up a cost allocation report with tags, see The Monthly Cost Allocation Report in About AWS Account Billing. To see the cost of your combined resources, you can organize your billing information based on resources that have the same tag key values. For example, you can tag several resources with a specific application name, and then organize your billing information to see the total cost of that application across several services. For more information, see Using Cost Allocation Tags in the AWS Billing and Cost Management User Guide.

Cost allocation tags can indicate which resources are contributing to costs, but deleting or deactivating resources doesn't always reduce costs. For example, snapshot data that is referenced by another snapshot is preserved, even if the snapshot that contains the original data is deleted. For more information, see Amazon Elastic Block Store Volumes and Snapshots in the AWS Billing and Cost Management User Guide.

Note
If you've just enabled reporting, data for the current month is available for viewing after 24 hours.
Working with Tags Using the Console

Using the Amazon EC2 console, you can see which tags are in use across all of your Amazon EC2 resources in the same region. You can view tags by resource and by resource type, and you can also view how many items of each resource type are associated with a specified tag. You can also use the Amazon EC2 console to apply or remove tags from one or more resources at a time.

For more information about using filters when listing your resources, see Listing and Filtering Your Resources.

For ease of use and best results, use Tag Editor in the AWS Management Console, which provides a central, unified way to create and manage your tags. For more information, see Working with Tag Editor in Getting Started with the AWS Management Console.

Contents

Displaying Tags
Adding and Deleting Tags on an Individual Resource
Adding and Deleting Tags to a Group of Resources
Adding a Tag When You Launch an Instance
Filtering a List of Resources by Tag
Displaying Tags

You can display tags in two different ways in the Amazon EC2 console. You can display the tags for an individual resource or for all resources.

To display tags for individual resources

When you select a resource-specific page in the Amazon EC2 console, it displays a list of those resources. For example, if you select Instances from the navigation pane, the console displays a list of Amazon EC2 instances. When you select a resource from one of these lists (e.g., an instance), if the resource supports tags, you can view and manage its tags. On most resource pages, you can view the tags in the Tags tab on the details pane.

You can add a column to the resource list that displays all values for tags with the same key. This column enables you to sort and filter the resource list by the tag. There are two ways to add a new column to the resource list to display your tags.

On the Tags tab, select Show Column. A new column will be added to the console.
Choose the Show/Hide Columns gear-shaped icon, and in the Show/Hide Columns dialog box, select the tag key under Your Tag Keys.
To display tags for all resources

You can display tags across all resources by selecting Tags from the navigation pane in the Amazon EC2 console. The following image shows the Tags pane, which lists all tags in use by resource type.


						The Tags pane in the Amazon EC2 console
					
Adding and Deleting Tags on an Individual Resource

You can manage tags for an individual resource directly from the resource's page.

To add a tag to an individual resource

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region that meets your needs. This choice is important because some Amazon EC2 resources can be shared between regions, while others can't. For more information, see Resource Locations.

In the navigation pane, select a resource type (for example, Instances).

Select the resource from the resource list.

Select the Tags tab in the details pane.

Choose the Add/Edit Tags button.

In the Add/Edit Tags dialog box, specify the key and value for each tag, and then choose Save.

To delete a tag from an individual resource

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region that meets your needs. This choice is important because some Amazon EC2 resources can be shared between regions, while others can't. For more information, see Resource Locations.

In the navigation pane, choose a resource type (for example, Instances).

Select the resource from the resource list.

Select the Tags tab in the details pane.

Choose Add/Edit Tags, select the Delete icon for the tag, and choose Save.

Adding and Deleting Tags to a Group of Resources

To add a tag to a group of resources

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region that meets your needs. This choice is important because some Amazon EC2 resources can be shared between regions, while others can't. For more information, see Resource Locations.

In the navigation pane, choose Tags.

At the top of the content pane, choose Manage Tags.

For Filter, select the type of resource (for example, instances) to which to add tags.

In the resources list, select the check box next to each resource to which to add tags.

Under Add Tag, for Key and Value, type the tag key and values, and then choose Add Tag.

Note
If you add a new tag with the same tag key as an existing tag, the new tag overwrites the existing tag.
To remove a tag from a group of resources

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select the region that meets your needs. This choice is important because some Amazon EC2 resources can be shared between regions, while others can't. For more information, see Resource Locations.

In the navigation pane, choose Tags, Manage Tags.

To view the tags in use, select the Show/Hide Columns gear-shaped icon, and in the Show/Hide Columns dialog box, select the tag keys to view and choose Close.

For Filter, select the type of resource (for example, instances) from which to remove tags.

In the resource list, select the check box next to each resource from which to remove tags.

Under Remove Tag, for Key, type the tag's name and choose Remove Tag.

Adding a Tag When You Launch an Instance

To add a tag using the Launch Wizard

From the navigation bar, select the region for the instance. This choice is important because some Amazon EC2 resources can be shared between regions, while others can't. Select the region that meets your needs. For more information, see Resource Locations.

Choose Launch Instance.

The Choose an Amazon Machine Image (AMI) page displays a list of basic configurations called Amazon Machine Images (AMIs). Select the AMI to use and choose Select. For more information about selecting an AMI, see Finding a Linux AMI.

On the Configure Instance Details page, configure the instance settings as necessary, and then choose Next: Add Storage.

On the Add Storage page, you can specify additional storage volumes for your instance. Choose Next: Add Tags when done.

On the Add Tags page, specify tags for the instance, the volumes, or both. Choose Add another tag to add more than one tag to your instance. Choose Next: Configure Security Group when you are done.

On the Configure Security Group page, you can choose from an existing security group that you own, or let the wizard create a new security group for you. Choose Review and Launch when you are done.

Review your settings. When you're satisfied with your selections, choose Launch. Select an existing key pair or create a new one, select the acknowledgment check box, and then choose Launch Instances.

Filtering a List of Resources by Tag

You can filter your list of resources based on one or more tag keys and tag values.

To filter a list of resources by tag

Display a column for the tag as follows:

Select a resource.

In the details pane, choose Tags.

Locate the tag in the list and choose Show Column.

Choose the filter icon in the top right corner of the column for the tag to display the filter list.

Select the tag values, and then choose Apply Filter to filter the results list.

Note
For more information about filters, see Listing and Filtering Your Resources.
Working with Tags Using the CLI or API

Use the following to add, update, list, and delete the tags for your resources. The corresponding documentation provides examples.

Task	AWS CLI	AWS Tools for Windows PowerShell	API Action
Add or overwrite one or more tags.
create-tags
New-EC2Tag
CreateTags
Delete one or more tags.
delete-tags
Remove-EC2Tag
DeleteTags
Describe one or more tags.
describe-tags
Get-EC2Tag
DescribeTags
You can also filter a list of resources according to their tags. The following examples demonstrate how to filter your instances using tags with the describe-instances command.

Important
Tags are immediately applied to your resources, therefore any tag-based resource-level permissions that you use in your IAM policies are immediately effective. However, when describing multiple resources, the results may be eventually consistent and may not return all of your tags. To confirm the tags for a resource, describe a single resource.
Example 1: Describe instances with the specified tag key

The following command describes the instances with a Stack tag, regardless of the value of the tag.

Copy
aws ec2 describe-instances --filters Name=tag-key,Values=Stack
Example 2: Describe instances with the specified tag

The following command describes the instances with the tag Stack=production.

Copy
aws ec2 describe-instances --filters Name=tag:Stack,Values=production
Example 3: Describe instances with the specified tag value

The following command describes the instances with a tag with the value production, regardless of the tag key.

Copy
aws ec2 describe-instances --filters Name=tag-value,Values=production
Some resource-creating actions enable you to specify tags when you create the resource. The following actions support tagging on creation.

Task	AWS CLI	AWS Tools for Windows PowerShell	API Action
Launch one or more instances.
run-instances
New-EC2Instance
RunInstances
Create an EBS volume.
create-volume
New-EC2Volume
CreateVolume
The following examples demonstrate how to apply tags when you create resources.

Example 4: Launch an instance and apply tags to the instance and volume

The following command launches an instance and applies a tag with a key of webserver and value of production to the instance. The command also applies a tag with a key of cost-center and a value of cc123 to any EBS volume that's created (in this case, the root volume).

Copy
aws ec2 run-instances --image-id ami-abc12345 --count 1 --instance-type t2.micro --key-name MyKeyPair --subnet-id subnet-6e7f829e --tag-specifications 'ResourceType=instance,Tags=[{Key=webserver,Value=production}]' 'ResourceType=volume,Tags=[{Key=cost-center,Value=cc123}]' 
You can apply the same tag keys and values to both instances and volumes during launch. The following command launches an instance and applies a tag with a key of cost-center and a value of cc123 to both the instance and any EBS volume that's created.

Copy
aws ec2 run-instances --image-id ami-abc12345 --count 1 --instance-type t2.micro --key-name MyKeyPair --subnet-id subnet-6e7f829e --tag-specifications 'ResourceType=instance,Tags=[{Key=cost-center,Value=cc123}]' 'ResourceType=volume,Tags=[{Key=cost-center,Value=cc123}]' 
Example 5: Create a volume and apply a tag

The following command creates a volume and applies two tags: purpose = production, and cost-center = cc123.

Copy
aws ec2 create-volume --availability-zone us-east-1a --volume-type gp2 --size 80 --tag-sp

Amazon EC2 Service Limits

Amazon EC2 provides different resources that you can use. These resources include images, instances, volumes, and snapshots. When you create your AWS account, we set default limits on these resources on a per-region basis. For example, there is a limit on the number of instances that you can launch in a region. Therefore, when you launch an instance in the US West (Oregon) Region, the request must not cause your usage to exceed your current instance limit in that region.

The Amazon EC2 console provides limit information for the resources managed by the Amazon EC2 and Amazon VPC consoles. You can request an increase for many of these limits. Use the limit information that we provide to manage your AWS infrastructure. Plan to request any limit increases in advance of the time that you'll need them.

For more information about the limits for other services, see AWS Service Limits in the Amazon Web Services General Reference.

Viewing Your Current Limits

Use the EC2 Service Limits page in the Amazon EC2 console to view the current limits for resources provided by Amazon EC2 and Amazon VPC, on a per-region basis.

To view your current limits

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select a region.


                  Select a region
               
From the navigation pane, choose Limits.

Locate the resource in the list. The Current Limit column displays the current maximum for that resource for your account.

Requesting a Limit Increase

Use the Limits page in the Amazon EC2 console to request an increase in the limits for resources provided by Amazon EC2 or Amazon VPC, on a per-region basis.

To request a limit increase

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the navigation bar, select a region.

From the navigation pane, choose Limits.

Locate the resource in the list. Choose Request limit increase.

Complete the required fields on the limit increase form. We'll respond to you using the contact method that you specified.

Amazon EC2 Usage Reports

The usage reports provided by Amazon EC2 enable you to analyze the usage of your instances in depth. The data in the usage reports is updated multiple times each day. You can filter the reports by AWS account, region, Availability Zone, operating system, instance type, purchasing option, tenancy, and tags.

To get usage and cost data for an account, you must have its account credentials and enable detailed billing reports with resources and tags for the account. If you're using consolidated billing, you must log into the payer account to view data for the payer account and all its linked accounts. For information about consolidated billing, see Pay Bills for Multiple Accounts with Consolidated Billing.

Topics

Available Reports
Getting Set Up for Usage Reports
Granting IAM Users Access to the Amazon EC2 Usage Reports
Instance Usage Report
Reserved Instance Utilization Reports
Available Reports

You can generate the following reports:

Instance usage report. This report covers your usage of On-Demand instances, Spot instances, and Reserved Instances.
Reserved Instances utilization report. This report covers the usage of your capacity reservation.
To access the reports, open the AWS Management Console. In the navigation pane, choose Reports then choose the report you'd like to view.

Getting Set Up for Usage Reports

Before you begin, enable detailed billing reports with resources and tags as shown in the following procedure. After you complete this procedure, we'll start collecting usage data for your instances. If you've already enabled detailed billing reports, you can access the usage data that we've been collecting since you enabled them.

Important
To complete these procedures, you must log in using your AWS account credentials. You can't complete these procedures if you log in using IAM user credentials.
To enable detailed billing reports

Select an existing Amazon S3 bucket to receive your usage data. Be sure to manage access to this bucket as it contains your billing data. (We don't require that you keep these files; in fact, you can delete them immediately if you don't need them.) If you don't have a bucket, create one as follows:

Open the Amazon S3 console.

Select Create Bucket.

In the Create a Bucket dialog box, enter a name for your bucket (for example, username-ec2-usage-data), select a region, and then choose Create. For more information about the requirements for bucket names, see Creating a Bucket in the Amazon Simple Storage Service Console User Guide.

Open the Billing and Cost Management console at https://console.aws.amazon.com/billing/home?#.

Choose Preferences in the navigation pane.

Select Receive Billing Reports.

Specify the name of your Amazon S3 bucket in Save to S3 Bucket.

Under Receive Billing Reports, choose sample policy. Copy the sample policy. Notice that the sample policy uses the bucket name you specified.

Grant AWS permission to publish usage data to your Amazon S3 bucket.

Open the Amazon S3 console in another browser tab. Select your bucket, choose Properties, and then expand Permissions. In the Permissions section, choose Add bucket policy. Paste the sample policy into the text area and choose Save. In the Permissions section, choose Save.

Return to the browser tab with the sample policy and choose Verify.

Under Report, select Detailed billing report with resources and tags.

Choose Save preferences.

Note
It can take up to a day before you can see your data in the reports.
You can categorize your instances using tags. After you tag your instances, you must enable reporting on these tags.

To enable usage reporting by tag

Tag your instances. For best results, ensure that you add each tag you plan to use for reporting to each of your instances. For more information about how to tag an instance, see Tagging Your Amazon EC2 Resources.

Open the Billing and Cost Management console at https://console.aws.amazon.com/billing/home?#.

Select Preferences in the navigation pane.

Under Report, choose Manage report tags.

The page displays the list of tags that you've created. Select the tags that you'd like to use to filter or group your instance usage data, and then click Save. We automatically exclude any tags that you don't select from your instance usage report.

Note
We apply these changes only to the data for the current month. It can take up to a day for these changes to take effect.
Granting IAM Users Access to the Amazon EC2 Usage Reports

By default, IAM users can't access the Amazon EC2 usage reports. You must create an IAM policy that grants IAM users permission to access these reports.

The following policy allows users to view both Amazon EC2 usage reports.

Copy
{
  "Version": "2012-10-17",
  "Statement":[{
    "Effect": "Allow",
    "Action": "ec2-reports:*",
    "Resource": "*"
  }
  ]
}
The following policy allows users to view the instance usage report.

Copy
{
  "Version": "2012-10-17",
  "Statement":[{
    "Effect": "Allow",
    "Action": "ec2-reports:ViewInstanceUsageReport",
    "Resource": "*"
  }
  ]
}
The following policy allows users to view the Reserved Instances utilization report.

Copy
{
  "Version": "2012-10-17",
  "Statement":[{
    "Effect": "Allow",
    "Action": "ec2-reports:ViewReservedInstanceUtilizationReport",
    "Resource": "*"
  }
  ]
}
For more information, see Permissions and Policies in the IAM User Guide.

Instance Usage Report

You can use the instance usage report to view your instance usage and cost trends. You can see your usage data in either instance hours or cost. You can choose to see hourly, daily and monthly aggregates of your usage data. You can filter or group the report by region, Availability Zone, instance type, AWS account, platform, tenancy, purchase option, or tag. After you configure a report, you can bookmark it so that it's easy to get back to later.

Here's an example of some of the questions that you can answer by creating an instance usage report:

How much am I spending on instances of each instance type?
How many instance hours are being used by a particular department?
How is my instance usage distributed across Availability Zones?
How is my instance usage distributed across AWS accounts?
Topics

Report Formats
Viewing Your Instance Usage
Bookmarking a Customized Report
Exporting Your Usage Data
Report Formats

We display the usage data that you request as both a graph and a table.

For example, the following graph displays cost by instance type. The key for the graph indicates which color represents which instance type. To get detailed information about a segment of a bar, hover over it.


                    Example graphical usage report for cost by instance type
                
The corresponding table displays one column for each instance type. Notice that we include a color band in the column head that is the same color as the instance type in the graph.


                    Example tabular usage report for cost by instance type
                
Viewing Your Instance Usage

The following procedures demonstrate how to generate usage reports using some of the capabilities we provide.

Before you begin, you must get set up. For more information, see Getting Set Up for Usage Reports.

To filter and group your instance usage by instance type

Open the Amazon EC2 console.

In the navigation pane, choose Reports and then select EC2 Instance Usage Report.

Select an option for Unit. To view the time that your instances have been running, in hours, select Instance Hours. To view the cost of your instance usage, select Cost.

Select options for Granularity and Time range.

To view the data summarized for each hour in the time range, select Hourly granularity. You can select a time range of up to 2 days when viewing hourly data.
To view the data summarized for each day in the time range, select Daily granularity. You can select a time range of up to 2 months when viewing daily data.
To view the data summarized for each month in the time range, select Monthly granularity.
In the Filter list, select Instance Type. In the Group by list, select Instance Type.

In the filter area, select one or more instance types and then select Update Report. The filters you specify appear under Applied Filters.


                            Example filters for cost by instance type
                        
Notice that you can return to the Amazon EC2 console by choosing either Reports or EC2 Management Console at the top of the page.

To group your instance usage based on tags

Open the Instance Usage Reports page.

Select an option for Unit. To view the time that your instances have been running, in hours, select Instance Hours. To view the cost of your instance usage, select Cost.

Select options for Granularity and Time range.

To view the data summarized for each hour in the time range, select Hourly granularity. You can select a time range of up to 2 days when viewing hourly data.
To view the data summarized for each day in the time range, select Daily granularity. You can select a time range of up to 2 months when viewing daily data.
To view the data summarized for each month in the time range, select Monthly granularity.
In the Group by list, select Tag.

Choose the Key Name box, select a name from the list, and then choose Update Report. If there are no items in this list, you must enable usage reporting by tag. For more information, see To enable usage reporting by tag.


                            Example grouping by tag
                        
Bookmarking a Customized Report

You might want to generate a customized report again. Do this by bookmarking the report.

To bookmark a custom report

Select the options and filters for your report. Each selection you make adds a parameter to the console URL. For example, granularity=Hourly and Filters=filter_list.

Using your browser, add the console URL as a bookmark.

To generate the same report in the future, use the bookmark that you created.

Exporting Your Usage Data

You might want to include your report graph or table in other reports. Do this by exporting the data.

To export usage data

Select the options and filters for your report.

To export the usage data from the table as a .csv file, choose Download and select CSV Only.

To export the graphical usage data as a .png file, choose Download and select Graph Only.

Reserved Instance Utilization Reports

The Reserved Instance utilization report describes the utilization over time of each group (or bucket) of Amazon EC2 Reserved Instances that you own. Each bucket has a unique combination of regions, instance type, accounts, platforms, tenancy and offering types. You can specify the time range that the report covers, from a custom range of weeks, months, a year, or three years. The available data depends on when you enable detailed billing reports for the account (see Getting Set Up for Usage Reports). The Reserved Instance utilization report compares the Reserved Instance prices paid for instance usage in the bucket with On-Demand prices and shows your savings for the time range covered by the report.

To get usage and cost data for an account, you must have its account credentials and enable detailed billing reports with resources and tags for the account. If you're using consolidated billing and are logged into the payer account, you can view data for the payer account and all its linked accounts. If you're using consolidated billing and are logged into one of the linked accounts, you can only view data for that linked account. For information about consolidated billing, see Pay Bills for Multiple Accounts with Consolidated Billing.

Note
The Reserved Instance buckets aggregate Reserved Instances across EC2-VPC and EC2-Classic network platform types in the same way that your bill is calculated. Additionally, Reserved Instances in a bucket may have different upfront and hourly prices.
Here are examples of some of the questions that you can answer using the Reserved Instance utilization report:

How well am I utilizing my Reserved Instances?
Are my Reserved Instances helping me save money?
For information about Reserved Instances, see Reserved Instances.

Before you begin, you must get set up. For more information, see Getting Set Up for Usage Reports.

Topics

Getting to Know the Report
Viewing Your Reserved Instance Utilization
Bookmarking a Customized Report
Exporting Your Usage Data
Options Reference
Getting to Know the Report

The Reserved Instance utilization report displays your requested utilization data in graph and table formats.

To access the report, open the AWS Management Console. In the navigation pane, choose Reports and then select EC2 Reserved Instance Usage Report.

The report aggregates Reserved Instance usage data for a given period by bucket. In the report, each row in the table represents a bucket and provides the following metrics:

Count—The highest number of Reserved Instances owned at the same time during the period of the report.
Usage Cost—The total Reserved Instance usage fees applied to instance usage covered by the Reserved Instance bucket.
Total Cost—The usage cost plus the amortized upfront fee for the usage period associated with the Reserved Instance bucket.
Note
If the bucket contains a Reserved Instance that you sold in the Reserved Instance Marketplace and that Reserved Instance was active at any point during the period of the report, the total cost of the bucket might be inflated and your savings might be underestimated.
Savings—The difference between what your usage for the period would have cost at On-Demand prices and what it actually cost using Reserved Instances (Total Cost).
Average Utilization—The average hourly utilization rate for the Reserved Instance bucket over the period.
Maximum Utilization—The highest utilization rate of any hour during the period covered by the report.
For each row—or Reserved Instance bucket—in the table, the graph represents data based on your selected Show metric over the selected Time range for the report. Each point in the graph represents a metric at a point in time. For information about report options, see Options Reference.

A color band at the edge of each selected row in the table corresponds to a report line in the graph. You can show a row in the graph by selecting the checkbox at the beginning of the row.

By default, the Reserved Instance utilization report returns data over the last 14 days for all Reserved Instance buckets. The graph shows the average utilization for the first five buckets in the table. You can customize the report graph to show different utilization (average utilization, maximum utilization) or cost (total cost, usage cost) data over a period ranging from 7 days to weeks, months, or years.

Customizing the Report

You can customize the Reserved Instance utilization report with Time range and Filter options.

Time range provides a list of common relative time ranges, ranging from Last 7 Days to Last 3 Years. Select the time range that works best for your needs, and then choose Update Report to apply the change. To apply a time range that is not on the list, select Custom and enter the start date and end date for which you want to run the report.

Filter lets you filter your Reserved Instance utilization report by one or more of the following Reserved Instance qualities: regions, instance type, accounts, platforms, tenancy, and offering types. For example, you can filter by region or by specific Availability Zones in a region, or both. To filter by region, select Regions, then select the regions and Availability Zones you want to include in the report, and choose Update Report.


                        Filter options for Reserved Instance utilization reports
                    
The report will return all results if no filter is applied.

For information about report options, see Options Reference.

Viewing Your Reserved Instance Utilization

In this section, we will highlight aspects of your Reserved Instance utilization that the graph and table capture. For the purposes of this discussion, we'll use the following report, which is based on test data.


                    A sample Reserved Instance utilization report that is based on test
                        data
                
This Reserved Instance utilization report displays the average utilization of Reserved Instances in the last three years. This report reveals the following information about the account's Reserved Instances and how they have been utilized.

Average Utilization
Only a few of the Reserved Instances in the table were utilized well. Standouts were the four t2.micro Reserved Instances (rows 2 and 3), which were utilized at 50% and 100% respectively.
Maximum Utilization
During the three-year reporting period, all of the t2.micro Reserved Instances were fully-utilized. The remainder of the Reserved Instances were under-utilized, resulting in less than satisfactory savings.
Savings
The report shows that for this test account, using Reserved Instances instead of On-Demand instances only resulted in savings for four t2.micro instances in US East (N. Virginia). The rest of the Reserved Instances did not provide adequate discount benefits.
Bookmarking a Customized Report

You might want to generate a customized report again. Do this by bookmarking the report.

To bookmark a custom report

Select the options and filters for your report. Each selection you make adds a parameter to the console URL. For example, granularity=Hourly and Filters=filter_list.

Using your browser, add the console URL as a bookmark.

To generate the same report in the future, use the bookmark that you created.

Exporting Your Usage Data

You might want to include your report graph or table in other reports. Do this by exporting the data.

To export usage data

Select the options and filters for your report.

To export the usage data from the table as a .csv file, choose Download and select CSV Only.

To export the graphical usage data as a .png file, choose Download and select Graph Only.

Options Reference

Use the Show options to specify the metric to be displayed by the report graph.

Average Utilization
Shows the average of the utilization rates for each hour over the selected time range, where the utilization rate of a bucket for an hour is the number of instance hours used for that hour divided by the total number of Reserved Instances owned in that hour.
Maximum Utilization
Shows the highest of the utilization rates of any hour over the selected time range, where the utilization rate of a bucket for an hour is the number of instance hours used for that hour divided by the total number of Reserved Instances owned in that hour.
Total Cost
Shows the usage cost plus the amortized portion of the upfront cost of the Reserved Instances in the bucket over the period for which the report is generated.
Usage Cost
Shows the total cost based on hourly fees for a selected bucket of Reserved Instances.
Use Time range to specify the period on which the report will be based.

Note
All times are specified in UTC time.
Last 7 Days
Shows data for usage that took place during the current and previous six calendar days. Can be used with daily or monthly granularities.
Last 14 Days
Shows data for usage that took place during the current and previous 13 calendar days. Can be used with daily or monthly granularities.
This Month
Shows data for usage that took place during the current calendar month. Can be used with daily or monthly granularities.
Last 3 Months
Shows data for usage that took place during the current and previous two calendar months. Can be used with daily or monthly granularities.
Last 6 Months
Shows data for usage that took place during the current and previous five calendar months. Can be used with monthly granularities.
Last 12 Months
Shows data for usage that took place during the current and previous 11 calendar months. Can be used with monthly granularity.
This Year
Shows data for usage that took place during the current calendar year. Can be used with monthly granularity.
Last 3 Years
Shows data for usage that took place during the current and previous two calendar years. Can be used with monthly granularity.
Custom
Shows data for the time range for the entered Start and End dates specified in the following format: mm/dd/yyyy. Can be used with hourly, daily, or monthly granularities, but you can only specify a maximum time range of two days for hourly data, two months for daily data, and three years for monthly data.
Use Filter to scope the data displayed in the report.

Regions
Instance Type
Accounts
Platforms
Tenancy
Offering Types

