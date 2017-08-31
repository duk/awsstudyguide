Monitoring Amazon EC2

Monitoring is an important part of maintaining the reliability, availability, and performance of your Amazon Elastic Compute Cloud (Amazon EC2) instances and your AWS solutions. You should collect monitoring data from all of the parts in your AWS solutions so that you can more easily debug a multi-point failure if one occurs. Before you start monitoring Amazon EC2, however, you should create a monitoring plan that should include:

What are your goals for monitoring?
What resources you will monitor?
How often you will monitor these resources?
What monitoring tools will you use?
Who will perform the monitoring tasks?
Who should be notified when something goes wrong?
After you have defined your monitoring goals and have created your monitoring plan, the next step is to establish a baseline for normal Amazon EC2 performance in your environment. You should measure Amazon EC2 performance at various times and under different load conditions. As you monitor Amazon EC2, you should store a history of monitoring data that you've collected. You can compare current Amazon EC2 performance to this historical data to help you to identify normal performance patterns and performance anomalies, and devise methods to address them. For example, you can monitor CPU utilization, disk I/O, and network utilization for your Amazon EC2 instances. When performance falls outside your established baseline, you might need to reconfigure or optimize the instance to reduce CPU utilization, improve disk I/O, or reduce network traffic.

To establish a baseline you should, at a minimum, monitor the following items:

Item to Monitor	Amazon EC2 Metric	Monitoring Script/CloudWatch Logs
CPU utilization
CPUUtilization
Memory utilization
[Linux instances] Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances

[Windows instances] Configure Integration with CloudWatch
Memory used
[Linux instances] Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances

[Windows instances] Configure Integration with CloudWatch
Memory available
[Linux instances] Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances

[Windows instances] Configure Integration with CloudWatch
Network utilization
NetworkIn

NetworkOut
Disk performance
DiskReadOps

DiskWriteOps
Disk Swap utilization [Linux instances]

Swap used [Linux instances]
Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances
Page File utilization (Windows instances only)

Page File used (Windows instances only)

Page File available (Windows instances only)
Configure Integration with CloudWatch
Disk Reads/Writes
DiskReadBytes

DiskWriteBytes
Disk Space utilization [Linux instances]
Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances
Disk Space used [Linux instances]
Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances
Disk Space available [Linux instances only]
Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances

Automated and Manual Monitoring

AWS provides various tools that you can use to monitor Amazon EC2. You can configure some of these tools to do the monitoring for you, while some of the tools require manual intervention.

Topics

Automated Monitoring Tools
Manual Monitoring Tools
Automated Monitoring Tools

You can use the following automated monitoring tools to watch Amazon EC2 and report back to you when something is wrong:

System Status Checks - monitor the AWS systems required to use your instance to ensure they are working properly. These checks detect problems with your instance that require AWS involvement to repair. When a system status check fails, you can choose to wait for AWS to fix the issue or you can resolve it yourself (for example, by stopping and restarting or terminating and replacing an instance). Examples of problems that cause system status checks to fail include:
Loss of network connectivity
Loss of system power
Software issues on the physical host
Hardware issues on the physical host that impact network reachability
For more information, see Status Checks for Your Instances.
Instance Status Checks - monitor the software and network configuration of your individual instance. These checks detect problems that require your involvement to repair. When an instance status check fails, typically you will need to address the problem yourself (for example by rebooting the instance or by making modifications in your operating system). Examples of problems that may cause instance status checks to fail include:
Failed system status checks
Misconfigured networking or startup configuration
Exhausted memory
Corrupted file system
Incompatible kernel
For more information, see Status Checks for Your Instances.
Amazon CloudWatch Alarms - watch a single metric over a time period you specify, and perform one or more actions based on the value of the metric relative to a given threshold over a number of time periods. The action is a notification sent to an Amazon Simple Notification Service (Amazon SNS) topic or Auto Scaling policy. Alarms invoke actions for sustained state changes only. CloudWatch alarms will not invoke actions simply because they are in a particular state, the state must have changed and been maintained for a specified number of periods. For more information, see Monitoring Your Instances Using CloudWatch.
Amazon CloudWatch Events - automate your AWS services and respond automatically to system events. Events from AWS services are delivered to CloudWatch Events in near real time, and you can specify automated actions to take when an event matches a rule you write. For more information, see What is Amazon CloudWatch Events?.
Amazon CloudWatch Logs - monitor, store, and access your log files from Amazon EC2 instances, AWS CloudTrail, or other sources. For more information, see What is Amazon CloudWatch Logs?.
Amazon EC2 Monitoring Scripts - Perl scripts that can monitor memory, disk, and swap file usage in your instances. For more information, see Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances.
AWS Management Pack for Microsoft System Center Operations Manager - links Amazon EC2 instances and the Windows or Linux operating systems running inside them. The AWS Management Pack is an extension to Microsoft System Center Operations Manager. It uses a designated computer in your datacenter (called a watcher node) and the Amazon Web Services APIs to remotely discover and collect information about your AWS resources. For more information, see AWS Management Pack for Microsoft System Center.
Manual Monitoring Tools

Another important part of monitoring Amazon EC2 involves manually monitoring those items that the monitoring scripts, status checks, and CloudWatch alarms don't cover. The Amazon EC2 and CloudWatch console dashboards provide an at-a-glance view of the state of your Amazon EC2 environment.

Amazon EC2 Dashboard shows:
Service Health and Scheduled Events by region
Instance state
Status checks
Alarm status
Instance metric details (In the navigation pane click Instances, select an instance, and then click the Monitoring tab)
Volume metric details (In the navigation pane click Volumes, select a volume, and then click the Monitoring tab)
Amazon CloudWatch Dashboard shows:
Current alarms and status
Graphs of alarms and resources
Service health status
In addition, you can use CloudWatch to do the following:
Graph Amazon EC2 monitoring data to troubleshoot issues and discover trends
Search and browse all your AWS resource metrics
Create and edit alarms to be notified of problems
See at-a-glance overviews of your alarms and AWS resources

Best Practices for Monitoring

Use the following best practices for monitoring to help you with your Amazon EC2 monitoring tasks.

Make monitoring a priority to head off small problems before they become big ones.
Create and implement a monitoring plan that collects monitoring data from all of the parts in your AWS solution so that you can more easily debug a multi-point failure if one occurs. Your monitoring plan should address, at a minimum, the following questions:
What are your goals for monitoring?
What resources you will monitor?
How often you will monitor these resources?
What monitoring tools will you use?
Who will perform the monitoring tasks?
Who should be notified when something goes wrong?
Automate monitoring tasks as much as possible.
Check the log files on your EC2 instances.

Monitoring the Status of Your Instances

You can monitor the status of your instances by viewing status checks and scheduled events for your instances. A status check gives you the information that results from automated checks performed by Amazon EC2. These automated checks detect whether specific issues are affecting your instances. The status check information, together with the data provided by Amazon CloudWatch, gives you detailed operational visibility into each of your instances.

You can also see status on specific events scheduled for your instances. Events provide information about upcoming activities such as rebooting or retirement that are planned for your instances, along with the scheduled start and end time of each event.

Contents

Status Checks for Your Instances
Scheduled Events for Your Instances

Status Checks for Your Instances

With instance status monitoring, you can quickly determine whether Amazon EC2 has detected any problems that might prevent your instances from running applications. Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues. You can view the results of these status checks to identify specific and detectable problems. This data augments the information that Amazon EC2 already provides about the intended state of each instance (such as pending, running, stopping) as well as the utilization metrics that Amazon CloudWatch monitors (CPU utilization, network traffic, and disk activity).

Status checks are performed every minute and each returns a pass or a fail status. If all checks pass, the overall status of the instance is OK. If one or more checks fail, the overall status is impaired. Status checks are built into Amazon EC2, so they cannot be disabled or deleted. You can, however create or delete alarms that are triggered based on the result of the status checks. For example, you can create an alarm to warn you if status checks fail on a specific instance. For more information, see Creating and Editing Status Check Alarms.

You can also create an Amazon CloudWatch alarm that monitors an Amazon EC2 instance and automatically recovers the instance if it becomes impaired due to an underlying issue. For more information, see Recover Your Instance.

Contents

Types of Status Checks
Viewing Status Checks
Reporting Instance Status
Creating and Editing Status Check Alarms
Types of Status Checks

There are two types of status checks: system status checks and instance status checks.

System Status Checks

Monitor the AWS systems on which your instance runs. These checks detect underlying problems with your instance that require AWS involvement to repair. When a system status check fails, you can choose to wait for AWS to fix the issue, or you can resolve it yourself. For instances backed by Amazon EBS, you can stop and start the instance yourself, which in most cases migrates it to a new host computer. For instances backed by instance store, you can terminate and replace the instance.

The following are examples of problems that can cause system status checks to fail:

Loss of network connectivity
Loss of system power
Software issues on the physical host
Hardware issues on the physical host that impact network reachability
Instance Status Checks

Monitor the software and network configuration of your individual instance. These checks detect problems that require your involvement to repair. When an instance status check fails, typically you will need to address the problem yourself (for example, by rebooting the instance or by making instance configuration changes).

The following are examples of problems that can cause instance status checks to fail:

Failed system status checks
Incorrect networking or startup configuration
Exhausted memory
Corrupted file system
Incompatible kernel
Viewing Status Checks

Amazon EC2 provides you with several ways to view and work with status checks.

Viewing Status Using the Console

You can view status checks using the AWS Management Console.

To view status checks using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

On the Instances page, the Status Checks column lists the operational status of each instance.

To view the status of a specific instance, select the instance, and then choose the Status Checks tab.


                                Viewing status
                            
If you have an instance with a failed status check and the instance has been unreachable for over 20 minutes, choose AWS Support to submit a request for assistance. To troubleshoot system or instance status check failures yourself, see Troubleshooting Instances with Failed Status Checks.

Viewing Status Using the Command Line or API

You can view status checks for running instances using the describe-instance-status (AWS CLI) command.

To view the status of all instances, use the following command:

Copy
aws ec2 describe-instance-status
To get the status of all instances with a instance status of impaired:

Copy
aws ec2 describe-instance-status --filters Name=instance-status.status,Values=impaired
To get the status of a single instance, use the following command:

Copy
aws ec2 describe-instance-status --instance-ids i-1234567890abcdef0
Alternatively, use the following commands:

Get-EC2InstanceStatus (AWS Tools for Windows PowerShell)
DescribeInstanceStatus (Amazon EC2 Query API)
If you have an instance with a failed status check, see Troubleshooting Instances with Failed Status Checks.

Reporting Instance Status

You can provide feedback if you are having problems with an instance whose status is not shown as impaired, or want to send AWS additional details about the problems you are experiencing with an impaired instance.

We use reported feedback to identify issues impacting multiple customers, but do not respond to individual account issues. Providing feedback does not change the status check results that you currently see for the instance.

Reporting Status Feedback Using the Console

To report instance status using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance.

Select the Status Checks tab, and then choose Submit feedback.

Complete the Report Instance Status form, and then choose Submit.

Reporting Status Feedback Using the Command Line or API

Use the following report-instance-status (AWS CLI) command to send feedback about the status of an impaired instance:

Copy
aws ec2 report-instance-status --instances i-1234567890abcdef0 --status impaired --reason-codes code
Alternatively, use the following commands:

Send-EC2InstanceStatus (AWS Tools for Windows PowerShell)
ReportInstanceStatus (Amazon EC2 Query API)
Creating and Editing Status Check Alarms

You can create instance status and system status alarms to notify you when an instance has a failed status check.

Creating a Status Check Alarm Using the Console

You can create status check alarms for an existing instance to monitor instance status or system status. You can configure the alarm to send you a notification by email or stop, terminate, or recover an instance when it fails an instance status check or system status check.

To create a status check alarm

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance.

Select the Status Checks tab, and then choose Create Status Check Alarm.

Select Send a notification to. Choose an existing SNS topic, or click create topic to create a new one. If creating a new topic, in With these recipients, enter your email address and the addresses of any additional recipients, separated by commas.

(Optional) Choose Take the action, and then select the action that you'd like to take.

In Whenever, select the status check that you want to be notified about.

Note
If you selected Recover this instance in the previous step, select Status Check Failed (System).
In For at least, set the number of periods you want to evaluate and in consecutive periods, select the evaluation period duration before triggering the alarm and sending an email.

(Optional) In Name of alarm, replace the default name with another name for the alarm.

Choose Create Alarm.

Important
If you added an email address to the list of recipients or created a new topic, Amazon SNS sends a subscription confirmation email message to each new address. Each recipient must confirm the subscription by clicking the link contained in that message. Alert notifications are sent only to confirmed addresses.
If you need to make changes to an instance status alarm, you can edit it.

To edit a status check alarm

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance, choose Actions, select CloudWatch Monitoring, and then choose Add/Edit Alarms.

In the Alarm Details dialog box, choose the name of the alarm.

In the Edit Alarm dialog box, make the desired changes, and then choose Save.

Creating a Status Check Alarm Using the AWS CLI

In the following example, the alarm publishes a notification to an SNS topic, arn:aws:sns:us-west-2:111122223333:my-sns-topic, when the instance fails either the instance check or system status check for at least two consecutive periods. The metric is StatusCheckFailed.

To create a status check alarm using the CLI

Select an existing SNS topic or create a new one. For more information, see Using the AWS CLI with Amazon SNS in the AWS Command Line Interface User Guide.

Use the following list-metrics command to view the available Amazon CloudWatch metrics for Amazon EC2:

Copy
aws cloudwatch list-metrics --namespace AWS/EC2
Use the following put-metric-alarm command to create the alarm:

Copy
aws cloudwatch put-metric-alarm --alarm-name StatusCheckFailed-Alarm-for-i-1234567890abcdef0 --metric-name StatusCheckFailed --namespace AWS/EC2 --statistic Maximum --dimensions Name=InstanceId,Value=i-1234567890abcdef0 --unit Count --period 300 --evaluation-periods 2 --threshold 1 --comparison-operator GreaterThanOrEqualToThreshold --alarm-actions arn:aws:sns:us-west-2:111122223333:my-sns-topic
Note

--period is the time frame, in seconds, in which Amazon CloudWatch metrics are collected. This example uses 300, which is 60 seconds multiplied by 5 minutes.
--evaluation-periods is the number of consecutive periods for which the value of the metric must be compared to the threshold. This example uses 2.
--alarm-actions is the list of actions to perform when this alarm is triggered. Each action is specified as an Amazon Resource Name (ARN). This example configures the alarm to send an email using Amazon SNS.

Scheduled Events for Your Instances

AWS can schedule events for your instances, such as a reboot, stop/start, or retirement. These events do not occur frequently. If one of your instances will be affected by a scheduled event, AWS sends an email to the email address that's associated with your AWS account prior to the scheduled event, with details about the event, including the start and end date. Depending on the event, you might be able to take action to control the timing of the event.

To update the contact information for your account so that you can be sure to be notified about scheduled events, go to the Account Settings page.

Contents

Types of Scheduled Events
Viewing Scheduled Events
Working with Instances Scheduled to Stop or Retire
Working with Instances Scheduled for Reboot
Working with Instances Scheduled for Maintenance
Types of Scheduled Events

Amazon EC2 supports the following types of scheduled events for your instances:

Instance stop: The instance will be stopped. When you start it again, it's migrated to a new host computer. Applies only to instances backed by Amazon EBS.
Instance retirement: The instance will be stopped or terminated.
Reboot: Either the instance will be rebooted (instance reboot) or the host computer for the instance will be rebooted (system reboot).
System maintenance: The instance might be temporarily affected by network maintenance or power maintenance.
Viewing Scheduled Events

In addition to receiving notification of scheduled events in email, you can check for scheduled events.

To view scheduled events for your instances using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, click Events. Any resources with an associated event are displayed. You can filter by resource type, or by specific event types. You can select the resource to view details.


                                Viewing events using the Events page.
                            
Alternatively, in the navigation pane, choose EC2 Dashboard. Any resources with an associated event are displayed under Scheduled Events.


                                Viewing events using the dashboard.
                            
Note that some events are also shown for affected resources. For example, in the navigation pane, choose Instances, and then select an instance. If the instance has an associated instance stop or instance retirement event, it is displayed in the lower pane.


                                Viewing events in the instance details.
                            
To view scheduled events for your instances using the command line or API

Use the following AWS CLI command:

Copy
aws ec2 describe-instance-status --instance-id i-1234567890abcdef0
The following is example output showing an instance retirement event:

{
    "InstanceStatuses": [
        {
            "InstanceStatus": {
                "Status": "ok",
                "Details": [
                    {
                        "Status": "passed",
                        "Name": "reachability"
                    }
                ]
            },
            "AvailabilityZone": "us-west-2a",
            "InstanceId": "i-1234567890abcdef0",
            "InstanceState": {
                "Code": 16,
                "Name": "running"
            },
            "SystemStatus": {
                "Status": "ok",
                "Details": [
                    {
                        "Status": "passed",
                        "Name": "reachability"
                    }
                ]
            },
            "Events": [
                {
                    "Code": "instance-stop",
                    "Description": "The instance is running on degraded hardware",
                    "NotBefore": "2015-05-23T00:00:00.000Z"
                }
            ]
        }
    ]
}
Alternatively, use the following commands:

Get-EC2InstanceStatus (AWS Tools for Windows PowerShell)
DescribeInstanceStatus (Amazon EC2 Query API)
Working with Instances Scheduled to Stop or Retire

When AWS detects irreparable failure of the underlying host computer for your instance, it schedules the instance to stop or terminate, depending on the type of root device for the instance. If the root device is an EBS volume, the instance is scheduled to stop. If the root device is an instance store volume, the instance is scheduled to terminate. For more information, see Instance Retirement.

Important
Any data stored on instance store volumes is lost when an instance is stopped or terminated. This includes instance store volumes that are attached to an instance that has an EBS volume as the root device. Be sure to save data from your instance store volumes that you will need later before the instance is stopped or terminated.
Actions for Instances Backed by Amazon EBS

You can wait for the instance to stop as scheduled. Alternatively, you can stop and start the instance yourself, which migrates it to a new host computer. For more information about stopping your instance, as well as information about the changes to your instance configuration when it's stopped, see Stop and Start Your Instance.

Actions for Instances Backed by Instance Store

We recommend that you launch a replacement instance from your most recent AMI and migrate all necessary data to the replacement instance before the instance is scheduled to terminate. Then, you can terminate the original instance, or wait for it to terminate as scheduled.

Working with Instances Scheduled for Reboot

When AWS needs to perform tasks such as installing updates or maintaining the underlying host computer, it can schedule an instance or the underlying host computer for the instance for a reboot. Regardless of any existing instances that are scheduled for reboot, a new instance launch does not require a reboot, as the updates are already applied on the underlying host.

You can determine whether the reboot event is an instance reboot or a system reboot.

To view the type of scheduled reboot event using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Events.

Select Instance resources from the filter list, and then select your instance.

In the bottom pane, locate Event type. The value is either system-reboot or instance-reboot.

To view the type of scheduled reboot event using the AWS CLI

Use the following describe-instance-status command:

Copy
aws ec2 describe-instance-status --instance-ids i-1234567890abcdef0
Actions for Instance Reboot

You can wait for the instance reboot to occur within its scheduled maintenance window. Alternatively, you can reboot your instance yourself at a time that is convenient for you. For more information, see Reboot Your Instance.

After you reboot your instance, the scheduled event for the instance reboot is canceled immediately and the event's description is updated. The pending maintenance to the underlying host computer is completed, and you can begin using your instance again after it has fully booted.

Actions for System Reboot

It is not possible for you to reboot the system yourself. We recommend that you wait for the system reboot to occur during its scheduled maintenance window. A system reboot typically completes in a matter of minutes, the instance retains its IP address and DNS name, and any data on local instance store volumes is preserved. After the system reboot has occurred, the scheduled event for the instance is cleared, and you can verify that the software on your instance is operating as you expect.

Alternatively, if it is necessary to maintain the instance at a different time, you can stop and start an EBS-backed instance, which migrates it to a new host. However, the data on the local instance store volumes would not be preserved. In the case of an instance store-backed instance, you can launch a replacement instance from your most recent AMI.

Working with Instances Scheduled for Maintenance

When AWS needs to maintain the underlying host computer for an instance, it schedules the instance for maintenance. There are two types of maintenance events: network maintenance and power maintenance.

During network maintenance, scheduled instances lose network connectivity for a brief period of time. Normal network connectivity to your instance will be restored after maintenance is complete.

During power maintenance, scheduled instances are taken offline for a brief period, and then rebooted. When a reboot is performed, all of your instance's configuration settings are retained.

After your instance has rebooted (this normally takes a few minutes), verify that your application is working as expected. At this point, your instance should no longer have a scheduled event associated with it, or the description of the scheduled event begins with [Completed]. It sometimes takes up to 1 hour for this instance status to refresh. Completed maintenance events are displayed on the Amazon EC2 console dashboard for up to a week.

Actions for Instances Backed by Amazon EBS

You can wait for the maintenance to occur as scheduled. Alternatively, you can stop and start the instance, which migrates it to a new host computer. For more information about stopping your instance, as well as information about the changes to your instance configuration when it's stopped, see Stop and Start Your Instance.

Actions for Instances Backed by Instance Store

You can wait for the maintenance to occur as scheduled. Alternatively, if you want to maintain normal operation during a scheduled maintenance window, you can launch a replacement instance from your most recent AMI, migrate all necessary data to the replacement instance before the scheduled maintenance window, and then terminate the original instance.

Monitoring Your Instances Using CloudWatch

You can monitor your instances using Amazon CloudWatch, which collects and processes raw data from Amazon EC2 into readable, near real-time metrics. These statistics are recorded for a period of 15 months, so that you can access historical information and gain a better perspective on how your web application or service is performing.

By default, Amazon EC2 sends metric data to CloudWatch in 5-minute periods. To send metric data for your instance to CloudWatch in 1-minute periods, you can enable detailed monitoring on the instance. For more information, see Enable or Disable Detailed Monitoring for Your Instances.

The Amazon EC2 console displays a series of graphs based on the raw data from Amazon CloudWatch. Depending on your needs, you might prefer to get data for your instances from Amazon CloudWatch instead of the graphs in the console.

For more information about Amazon CloudWatch, see the Amazon CloudWatch User Guide.

Contents

Enable or Disable Detailed Monitoring for Your Instances
List the Available CloudWatch Metrics for Your Instances
Get Statistics for Metrics for Your Instances
Graph Metrics for Your Instances
Create a CloudWatch Alarm for an Instance
Create Alarms That Stop, Terminate, Reboot, or Recover an Instance

Enable or Disable Detailed Monitoring for Your Instances

By default, your instance is enabled for basic monitoring. You can optionally enable detailed monitoring. After you enable detailed monitoring, the Amazon EC2 console displays monitoring graphs with a 1-minute period for the instance. The following table describes basic and detailed monitoring for instances.

Type	Description
Basic
Data is available automatically in 5-minute periods at no charge.
Detailed
Data is available in 1-minute periods for an additional cost. To get this level of data, you must specifically enable it for the instance. For the instances where you've enabled detailed monitoring, you can also get aggregated data across groups of similar instances.

For information about pricing, see the Amazon CloudWatch product page.
Enabling Detailed Monitoring

You can enable detailed monitoring on an instance as you launch it or after the instance is running or stopped.

To enable detailed monitoring for an existing instance using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance, choose Actions, CloudWatch Monitoring, Enable Detailed Monitoring.

In the Enable Detailed Monitoring dialog box, choose Yes, Enable.

Choose Close.

To enable detailed monitoring when launching an instance using the console

When launching an instance using the AWS Management Console, select the Monitoring check box on the Configure Instance Details page.

To enable detailed monitoring for an existing instance using the AWS CLI

Use the following monitor-instances command to enable detailed monitoring for the specified instances.

Copy
aws ec2 monitor-instances --instance-ids i-1234567890abcdef0
To enable detailed monitoring when launching an instance using the AWS CLI

Use the run-instances command with the --monitoring flag to enable detailed monitoring.

Copy
aws ec2 run-instances --image-id ami-09092360 --monitoring Enabled=true...
Disabling Detailed Monitoring

You can disable detailed monitoring on an instance as you launch it or after the instance is running or stopped.

To disable detailed monitoring using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance, choose Actions, CloudWatch Monitoring, Disable Detailed Monitoring.

In the Disable Detailed Monitoring dialog box, choose Yes, Disable.

Choose Close.

To disable detailed monitoring using the AWS CLI

Use the following unmonitor-instances command to disable detailed monitoring for the specified instances.

Copy
aws ec2 unmonitor-instances --instance-ids i-1234567890abcdef0

List the Available CloudWatch Metrics for Your Instances

Amazon EC2 sends metrics to Amazon CloudWatch. You can use the AWS Management Console, the AWS CLI, or an API to list the metrics that Amazon EC2 sends to CloudWatch. By default, each data point covers the previous 5 minutes of activity for the instance. If you've enabled detailed monitoring, each data point covers the previous 1 minute of activity.

For information about getting the statistics for these metrics, see Get Statistics for Metrics for Your Instances.

Instance Metrics

The AWS/EC2 namespace includes the following CPU credit metrics for your T2 instances.

Metric	Description
CPUCreditUsage
[T2 instances] The number of CPU credits consumed by the instance. One CPU credit equals one vCPU running at 100% utilization for one minute or an equivalent combination of vCPUs, utilization, and time (for example, one vCPU running at 50% utilization for two minutes or two vCPUs running at 25% utilization for two minutes).

CPU credit metrics are available only at a 5 minute frequency. If you specify a period greater than five minutes, use the Sum statistic instead of the Average statistic.

Units: Count
CPUCreditBalance
[T2 instances] The number of CPU credits available for the instance to burst beyond its base CPU utilization. Credits are stored in the credit balance after they are earned and removed from the credit balance after they expire. Credits expire 24 hours after they are earned.

CPU credit metrics are available only at a 5 minute frequency.

Units: Count
The AWS/EC2 namespace includes the following instance metrics.

Metric	Description
CPUUtilization
The percentage of allocated EC2 compute units that are currently in use on the instance. This metric identifies the processing power required to run an application upon a selected instance.

To use the percentiles statistic, you must enable detailed monitoring.

Depending on the instance type, tools in your operating system can show a lower percentage than CloudWatch when the instance is not allocated a full processor core.

Units: Percent
DiskReadOps
Completed read operations from all instance store volumes available to the instance in a specified period of time.

To calculate the average I/O operations per second (IOPS) for the period, divide the total operations in the period by the number of seconds in that period.

Units: Count
DiskWriteOps
Completed write operations to all instance store volumes available to the instance in a specified period of time.

To calculate the average I/O operations per second (IOPS) for the period, divide the total operations in the period by the number of seconds in that period.

Units: Count
DiskReadBytes
Bytes read from all instance store volumes available to the instance.

This metric is used to determine the volume of the data the application reads from the hard disk of the instance. This can be used to determine the speed of the application.

The number reported is the number of bytes received during the period. If you are using basic (five-minute) monitoring, you can divide this number by 300 to find Bytes/second. If you have detailed (one-minute) monitoring, divide it by 60.

Units: Bytes
DiskWriteBytes
Bytes written to all instance store volumes available to the instance.

This metric is used to determine the volume of the data the application writes onto the hard disk of the instance. This can be used to determine the speed of the application.

The number reported is the number of bytes received during the period. If you are using basic (five-minute) monitoring, you can divide this number by 300 to find Bytes/second. If you have detailed (one-minute) monitoring, divide it by 60.

Units: Bytes
NetworkIn
The number of bytes received on all network interfaces by the instance. This metric identifies the volume of incoming network traffic to a single instance.

The number reported is the number of bytes received during the period. If you are using basic (five-minute) monitoring, you can divide this number by 300 to find Bytes/second. If you have detailed (one-minute) monitoring, divide it by 60.

Units: Bytes
NetworkOut
The number of bytes sent out on all network interfaces by the instance. This metric identifies the volume of outgoing network traffic from a single instance.

The number reported is the number of bytes received during the period. If you are using basic (five-minute) monitoring, you can divide this number by 300 to find Bytes/second. If you have detailed (one-minute) monitoring, divide it by 60.

Units: Bytes
NetworkPacketsIn
The number of packets received on all network interfaces by the instance. This metric identifies the volume of incoming traffic in terms of the number of packets on a single instance. This metric is available for basic monitoring only.

Units: Count

Statistics: Minimum, Maximum, Average
NetworkPacketsOut
The number of packets sent out on all network interfaces by the instance. This metric identifies the volume of outgoing traffic in terms of the number of packets on a single instance. This metric is available for basic monitoring only.

Units: Count

Statistics: Minimum, Maximum, Average
The AWS/EC2 namespace includes the following status checks metrics. Status check metrics are available at a 1 minute frequency. For a newly-launched instance, status check metric data is only available after the instance has completed the initialization state (within a few minutes of the instance entering the running state). For more information about EC2 status checks, see Status Checks For Your Instances.

Metric	Description
StatusCheckFailed
Reports whether the instance has passed both the instance status check and the system status check in the last minute.

This metric can be either 0 (passed) or 1 (failed).

Units: Count
StatusCheckFailed_Instance
Reports whether the instance has passed the instance status check in the last minute.

This metric can be either 0 (passed) or 1 (failed).

Units: Count
StatusCheckFailed_System
Reports whether the instance has passed the system status check in the last minute.

This metric can be either 0 (passed) or 1 (failed).

Units: Count
For information about the metrics provided for your EBS volumes, see Amazon EBS Metrics. For information about the metrics provided for your Spot fleets, see CloudWatch Metrics for Spot Fleet.

Amazon EC2 Dimensions

You can use the following dimensions to refine the metrics returned for your instances.

Dimension	Description
AutoScalingGroupName	
This dimension filters the data you request for all instances in a specified capacity group. An Auto Scaling group is a collection of instances you define if you're using Auto Scaling. This dimension is available only for Amazon EC2 metrics when the instances are in such an Auto Scaling group. Available for instances with Detailed or Basic Monitoring enabled.
ImageId	
This dimension filters the data you request for all instances running this Amazon EC2 Amazon Machine Image (AMI). Available for instances with Detailed Monitoring enabled.
InstanceId	
This dimension filters the data you request for the identified instance only. This helps you pinpoint an exact instance from which to monitor data.
InstanceType	
This dimension filters the data you request for all instances running with this specified instance type. This helps you categorize your data by the type of instance running. For example, you might compare data from an m1.small instance and an m1.large instance to determine which has the better business value for your application. Available for instances with Detailed Monitoring enabled.
Listing Metrics Using the Console

Metrics are grouped first by namespace, and then by the various dimension combinations within each namespace. For example, you can view all metrics provided by Amazon EC2, or metrics grouped by instance ID, instance type, image (AMI) ID, or Auto Scaling group.

To view available metrics by category

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, choose Metrics.

Select the EC2 metric namespace.


              Select the EC2 metrics namespace
            
Select a metric dimension (for example, Per-Instance Metrics).


              View the metric dimensions for Amazon EC2
            
To sort the metrics, use the column heading. To graph a metric, select the check box next to the metric. To filter by resource, choose the resource ID and then choose Add to search. To filter by metric, choose the metric name and then choose Add to search.


              View the metrics for Amazon EC2
            
Listing Metrics Using the AWS CLI

Use the list-metrics command to list the CloudWatch metrics for your instances.

To list all the available metrics for Amazon EC2

The following example specifies the AWS/EC2 namespace to view all the metrics for Amazon EC2.

Copy
aws cloudwatch list-metrics --namespace AWS/EC2
The following is example output:

{
  "Metrics": [
    {
        "Namespace": "AWS/EC2",
        "Dimensions": [
            {
                "Name": "InstanceId",
                "Value": "i-1234567890abcdef0"
            }
        ],
        "MetricName": "NetworkOut"
    },
    {
        "Namespace": "AWS/EC2",
        "Dimensions": [
            {
                "Name": "InstanceId",
                "Value": "i-1234567890abcdef0"
            }
        ],
        "MetricName": "CPUUtilization"
    },
    {
        "Namespace": "AWS/EC2",
        "Dimensions": [
            {
                "Name": "InstanceId",
                "Value": "i-1234567890abcdef0"
            }
        ],
        "MetricName": "NetworkIn"
    },
    ...
  ]
}
To list all the available metrics for an instance

The following example specifies the AWS/EC2 namespace and the InstanceId dimension to view the results for the specified instance only.

Copy
aws cloudwatch list-metrics --namespace AWS/EC2 --dimensions Name=InstanceId,Value=i-1234567890abcdef0
To list a metric across all instances

The following example specifies the AWS/EC2 namespace and a metric name to view the results for the specified metric only.

Copy
aws cloudwatch list-metrics --namespace AWS/EC2 --metric-name CPUUtilization

Get Statistics for Metrics for Your Instances

You can get statistics for the CloudWatch metrics for your instances.

Contents

Statistics Overview
Get Statistics for a Specific Instance
Aggregate Statistics Across Instances
Aggregate Statistics by Auto Scaling Group
Aggregate Statistics by AMI
Statistics Overview

Statistics are metric data aggregations over specified periods of time. CloudWatch provides statistics based on the metric data points provided by your custom data or provided by other services in AWS to CloudWatch. Aggregations are made using the namespace, metric name, dimensions, and the data point unit of measure, within the time period you specify. The following table describes the available statistics.

Statistic	Description
Minimum	
The lowest value observed during the specified period. You can use this value to determine low volumes of activity for your application.
Maximum	
The highest value observed during the specified period. You can use this value to determine high volumes of activity for your application.
Sum	
All values submitted for the matching metric added together. This statistic can be useful for determining the total volume of a metric.
Average	
The value of Sum / SampleCount during the specified period. By comparing this statistic with the Minimum and Maximum, you can determine the full scope of a metric and how close the average use is to the Minimum and Maximum. This comparison helps you to know when to increase or decrease your resources as needed.
SampleCount	
The count (number) of data points used for the statistical calculation.
pNN.NN	
The value of the specified percentile. You can specify any percentile, using up to two decimal places (for example, p95.45).

Get Statistics for a Specific Instance

The following examples show you how to use the AWS Management Console or the AWS CLI to determine the maximum CPU utilization of a specific EC2 instance.

Requirements

You must have the ID of the instance. You can get the instance ID using the AWS Management Console or the describe-instances command.
By default, basic monitoring is enabled, but you can enable detailed monitoring. For more information, see Enable or Disable Detailed Monitoring for Your Instances.
To display the CPU utilization for a specific instance using the console

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, choose Metrics.

Select the EC2 metric namespace.


              Select the EC2 metrics namespace
            
Select the Per-Instance Metrics dimension.


              View the metric dimensions for Amazon EC2
            
In the search field, type CPUUtilization and press Enter. Select the row for the specific instance, which displays a graph for the CPUUtilization metric for the instance. To name the graph, choose the pencil icon. To change the time range, select one of the predefined values or choose custom.


              Graph a single metric
            
To change the statistic or the period for the metric, choose the Graphed metrics tab. Choose the column heading or an individual value, and then choose a different value.


              Change the statistic or period for a metric
            
To get the CPU utilization for a specific instance using the AWS CLI

Use the following get-metric-statistics command to get the CPUUtilization metric for the specified instance, using the specified period and time interval:

Copy
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization  --period 3600 \
--statistics Maximum --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
--start-time 2016-10-18T23:18:00 --end-time 2016-10-19T23:18:00
The following is example output. Each value represents the maximum CPU utilization percentage for a single EC2 instance.

{
    "Datapoints": [
        {
            "Timestamp": "2016-10-19T00:18:00Z", 
            "Maximum": 0.33000000000000002, 
            "Unit": "Percent"
        }, 
        {
            "Timestamp": "2016-10-19T03:18:00Z", 
            "Maximum": 99.670000000000002, 
            "Unit": "Percent"
        }, 
        {
            "Timestamp": "2016-10-19T07:18:00Z", 
            "Maximum": 0.34000000000000002, 
            "Unit": "Percent"
        }, 
        {
            "Timestamp": "2016-10-19T12:18:00Z", 
            "Maximum": 0.34000000000000002, 
            "Unit": "Percent"
        }, 
        ...
    ], 
    "Label": "CPUUtilization"
}

Aggregate Statistics Across Instances

Aggregate statistics are available for the instances that have detailed monitoring enabled. Instances that use basic monitoring are not included in the aggregates. In addition, Amazon CloudWatch does not aggregate data across regions. Therefore, metrics are completely separate between regions. Before you can get statistics aggregated across instances, you must enable detailed monitoring (at an additional charge), which provides data in 1-minute periods.

This example shows you how to use detailed monitoring to get the average CPU usage for your EC2 instances. Because no dimension is specified, CloudWatch returns statistics for all dimensions in the AWS/EC2 namespace.

Important
This technique for retrieving all dimensions across an AWS namespace does not work for custom namespaces that you publish to Amazon CloudWatch. With custom namespaces, you must specify the complete set of dimensions that are associated with any given data point to retrieve statistics that include the data point.
To display average CPU utilization across your instances

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, choose Metrics.

Select the EC2 namespace and then select Across All Instances.

Select the row that contains CPUUtilization, which displays a graph for the metric for all your EC2 instances. To name the graph, choose the pencil icon. To change the time range, select one of the predefined values or choose custom.


              Metrics aggregated across your EC2 instances
            
To change the statistic or the period for the metric, choose the Graphed metrics tab. Choose the column heading or an individual value, and then choose a different value.

To get average CPU utilization across your instances

Use the get-metric-statistics command as follows to get the average of the CPUUtilization metric across your instances.

Copy
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization \ 
--period 3600  --statistics "Average" "SampleCount" \ 
--start-time 2016-10-11T23:18:00 --end-time 2016-10-12T23:18:00
The following is example output:

{
    "Datapoints": [
        {
            "SampleCount": 238.0, 
            "Timestamp": "2016-10-12T07:18:00Z", 
            "Average": 0.038235294117647062, 
            "Unit": "Percent"
        }, 
        {
            "SampleCount": 240.0, 
            "Timestamp": "2016-10-12T09:18:00Z", 
            "Average": 0.16670833333333332, 
            "Unit": "Percent"
        }, 
        {
            "SampleCount": 238.0, 
            "Timestamp": "2016-10-11T23:18:00Z", 
            "Average": 0.041596638655462197, 
            "Unit": "Percent"
        },
        ...
    ], 
    "Label": "CPUUtilization"
}

Aggregate Statistics by Auto Scaling Group

You can aggregate statistics for the EC2 instances in an Auto Scaling group. Note that Amazon CloudWatch cannot aggregate data across regions. Metrics are completely separate between regions.

This example shows you how to retrieve the total bytes written to disk for one Auto Scaling group. The total is computed for one-minute periods for a 24-hour interval across all EC2 instances in the specified Auto Scaling group.

To display DiskWriteBytes for the instances in an Auto Scaling group using the console

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, choose Metrics.

Select the EC2 namespace and then select By Auto Scaling Group.

Select the row for the DiskWriteBytes metric and the specific Auto Scaling group, which displays a graph for the metric for the instances in the Auto Scaling group. To name the graph, choose the pencil icon. To change the time range, select one of the predefined values or choose custom.

To change the statistic or the period for the metric, choose the Graphed metrics tab. Choose the column heading or an individual value, and then choose a different value.

To display DiskWriteBytes for the instances in an Auto Scaling group using the AWS CLI

Use the get-metric-statistics command as follows.

Copy
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name DiskWriteBytes --period 360 \
--statistics "Sum" "SampleCount" --dimensions Name=AutoScalingGroupName,Value=my-asg --start-time 2016-10-16T23:18:00 --end-time 2016-10-18T23:18:00
The following is example output:

{
    "Datapoints": [
        {
            "SampleCount": 18.0, 
            "Timestamp": "2016-10-19T21:36:00Z", 
            "Sum": 0.0, 
            "Unit": "Bytes"
        }, 
        {
            "SampleCount": 5.0, 
            "Timestamp": "2016-10-19T21:42:00Z", 
            "Sum": 0.0, 
            "Unit": "Bytes"
        }
    ], 
    "Label": "DiskWriteBytes"
}

Aggregate Statistics by AMI

You can aggregate statistics for your instances that have detailed monitoring enabled. Instances that use basic monitoring are not included. Note that Amazon CloudWatch cannot aggregate data across regions. Metrics are completely separate between regions.

Before you can get statistics aggregated across instances, you must enable detailed monitoring (at an additional charge), which provides data in 1-minute periods. For more information, see Enable or Disable Detailed Monitoring for Your Instances.

This example shows you how to determine average CPU utilization for all instances that use a specific Amazon Machine Image (AMI). The average is over 60-second time intervals for a one-day period.

To display the average CPU utilization by AMI using the console

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, choose Metrics.

Select the EC2 namespace and then select By Image (AMI) Id.

Select the row for the CPUUtilization metric and the specific AMI, which displays a graph for the metric for the specified AMI. To name the graph, choose the pencil icon. To change the time range, select one of the predefined values or choose custom.

To change the statistic or the period for the metric, choose the Graphed metrics tab. Choose the column heading or an individual value, and then choose a different value.

To get the average CPU utilization for an image ID

Use the get-metric-statistics command as follows.

Copy
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization  --period 3600 \
--statistics Average --dimensions Name=ImageId,Value=ami-3c47a355 --start-time 2016-10-10T00:00:00 --end-time 2016-10-11T00:00:00
The following is example output. Each value represents an average CPU utilization percentage for the EC2 instances running the specified AMI.

{
    "Datapoints": [
        {
            "Timestamp": "2016-10-10T07:00:00Z", 
            "Average": 0.041000000000000009, 
            "Unit": "Percent"
        }, 
        {
            "Timestamp": "2016-10-10T14:00:00Z", 
            "Average": 0.079579831932773085, 
            "Unit": "Percent"
        }, 
        {
            "Timestamp": "2016-10-10T06:00:00Z", 
            "Average": 0.036000000000000011, 
            "Unit": "Percent"
        }, 
        ...
    ], 
    "Label": "CPUUtilization"
}

Graph Metrics for Your Instances

After you launch an instance, you can open the Amazon EC2 console and view the monitoring graphs for an instance on the Monitoring tab. Each graph is based on one of the available Amazon EC2 metrics.

The following graphs are available:

Average CPU Utilization (Percent)
Average Disk Reads (Bytes)
Average Disk Writes (Bytes)
Maximum Network In (Bytes)
Maximum Network Out (Bytes)
Summary Disk Read Operations (Count)
Summary Disk Write Operations (Count)
Summary Status (Any)
Summary Status Instance (Count)
Summary Status System (Count)
For more information about the metrics and the data they provide to the graphs, see List the Available CloudWatch Metrics for Your Instances.

Graph Metrics Using the CloudWatch Console

You can also use the CloudWatch console to graph metric data generated by Amazon EC2 and other AWS services. For more information, see Graph Metrics in the Amazon CloudWatch User Guide.

Create a CloudWatch Alarm for an Instance

You can create a CloudWatch alarm that monitors CloudWatch metrics for one of your instances. CloudWatch will automatically send you a notification when the metric reaches a threshold you specify. You can create a CloudWatch alarm using the Amazon EC2 console, or using the more advanced options provided by the CloudWatch console.

To create an alarm using the CloudWatch console

For examples, see Creating Amazon CloudWatch Alarms in the Amazon CloudWatch User Guide.

To create an alarm using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance.

On the Monitoring tab, choose Create Alarm.

On the Create Alarm page, do the following:

Choose create topic. For Send a notification to, type a name for the SNS topic. For With these recipients, type one or more email addresses to receive notification.

Specify the metric and the criteria for the policy. For example, you can leave the default settings for Whenever (Average of CPU Utilization). For Is, choose >= and type 80 percent. For For at least, type 1 consecutive period of 5 Minutes.

Choose Create Alarm.

Create Alarms That Stop, Terminate, Reboot, or Recover an Instance

Using Amazon CloudWatch alarm actions, you can create alarms that automatically stop, terminate, reboot, or recover your instances. You can use the stop or terminate actions to help you save money when you no longer need an instance to be running. You can use the reboot and recover actions to automatically reboot those instances or recover them onto new hardware if a system impairment occurs.

Every alarm action you create uses alarm action ARNs. One set of ARNs is more secure because it requires you to have the EC2ActionsAccess IAM role in your account. This IAM role enables you to perform stop, terminate, or reboot actions—previously you could not execute an action if you were using an IAM role. Existing alarms that use the previous alarm action ARNs do not require this IAM role, however it is recommended that you change the ARN and add the role when you edit an existing alarm that uses these ARNs.

The EC2ActionsAccess role enables AWS to perform alarm actions on your behalf. When you create an alarm action for the first time using the Amazon EC2 or Amazon CloudWatch consoles, AWS automatically creates this role for you.

There are a number of scenarios in which you might want to automatically stop or terminate your instance. For example, you might have instances dedicated to batch payroll processing jobs or scientific computing tasks that run for a period of time and then complete their work. Rather than letting those instances sit idle (and accrue charges), you can stop or terminate them which can help you to save money. The main difference between using the stop and the terminate alarm actions is that you can easily restart a stopped instance if you need to run it again later, and you can keep the same instance ID and root volume. However, you cannot restart a terminated instance. Instead, you must launch a new instance.

You can add the stop, terminate, reboot, or recover actions to any alarm that is set on an Amazon EC2 per-instance metric, including basic and detailed monitoring metrics provided by Amazon CloudWatch (in the AWS/EC2 namespace), as well as any custom metrics that include the InstanceId dimension, as long as its value refers to a valid running Amazon EC2 instance.

Console Support

You can create alarms using the Amazon EC2 console or the CloudWatch console. The procedures in this documentation use the Amazon EC2 console. For procedures that use the CloudWatch console, see Create Alarms That Stop, Terminate, Reboot, or Recover an Instance in the Amazon CloudWatch User Guide.

Permissions

If you are an AWS Identity and Access Management (IAM) user, you must have the following permissions to create or modify an alarm:

ec2:DescribeInstanceStatus and ec2:DescribeInstances — For all alarms on Amazon EC2 instance status metrics
ec2:StopInstances — For alarms with stop actions
ec2:TerminateInstances — For alarms with terminate actions
ec2:DescribeInstanceRecoveryAttribute, and ec2:RecoverInstances — For alarms with recover actions
If you have read/write permissions for Amazon CloudWatch but not for Amazon EC2, you can still create an alarm but the stop or terminate actions won't be performed on the Amazon EC2 instance. However, if you are later granted permission to use the associated Amazon EC2 APIs, the alarm actions you created earlier will be performed. For more information about IAM permissions, see Permissions and Policies in the IAM User Guide.

If you want to use an IAM role to stop, terminate, or reboot an instance using an alarm action, you can only use the EC2ActionsAccess role. Other IAM roles are not supported. If you are using another IAM role, you cannot stop, terminate, or reboot the instance. However, you can still see the alarm state and perform any other actions such as Amazon SNS notifications or Auto Scaling policies.

Contents

Adding Stop Actions to Amazon CloudWatch Alarms
Adding Terminate Actions to Amazon CloudWatch Alarms
Adding Reboot Actions to Amazon CloudWatch Alarms
Adding Recover Actions to Amazon CloudWatch Alarms
Using the Amazon CloudWatch Console to View the History of Triggered Alarms and Actions
Amazon CloudWatch Alarm Action Scenarios
Adding Stop Actions to Amazon CloudWatch Alarms

You can create an alarm that stops an Amazon EC2 instance when a certain threshold has been met. For example, you may run development or test instances and occasionally forget to shut them off. You can create an alarm that is triggered when the average CPU utilization percentage has been lower than 10 percent for 24 hours, signaling that it is idle and no longer in use. You can adjust the threshold, duration, and period to suit your needs, plus you can add an Amazon Simple Notification Service (Amazon SNS) notification, so that you will receive an email when the alarm is triggered.

Instances that use an Amazon EBS volume as the root device can be stopped or terminated, whereas instances that use the instance store as the root device can only be terminated.

To create an alarm to stop an idle instance using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under INSTANCES, choose Instances.

Select the instance. On the Monitoring tab, choose Create Alarm.

In the Alarm Details for dialog box, choose Create Alarm.

If you want to receive an email when the alarm is triggered, in the Create Alarm for dialog box, for Send a notification to, choose an existing Amazon SNS topic, or choose Create Topic to create a new one.

To create a new topic, for Send a notification to, type a name for the topic, and then for With these recipients, type the email addresses of the recipients (separated by commas). After you create the alarm, you will receive a subscription confirmation email that you must accept before you can get notifications for this topic.

Choose Take the action, and then choose the Stop this instance radio button.

If prompted, select Create IAM role: EC2ActionsAccess to automatically create an IAM role so that AWS can automatically stop the instance on your behalf when the alarm is triggered.

For Whenever, choose the statistic you want to use and then choose the metric. In this example, choose Average and CPU Utilization.

For Is, define the metric threshold. In this example, type 10 percent.

For For at least, choose the sampling period for the alarm. In this example, type 24 consecutive periods of one hour.

To change the name of the alarm, for Name this alarm, type a new name.

If you don't type a name for the alarm, Amazon CloudWatch will automatically create one for you.

Note
You can adjust the alarm configuration based on your own requirements before creating the alarm, or you can edit them later. This includes the metric, threshold, duration, action, and notification settings. However, after you create an alarm, you cannot edit its name later.
Choose Create Alarm.

Adding Terminate Actions to Amazon CloudWatch Alarms

You can create an alarm that terminates an EC2 instance automatically when a certain threshold has been met (as long as termination protection is not enabled for the instance). For example, you might want to terminate an instance when it has completed its work, and you don’t need the instance again. If you might want to use the instance later, you should stop the instance instead of terminating it. For information on enabling and disabling termination protection for an instance, see Enabling Termination Protection for an Instance in the Amazon EC2 User Guide for Linux Instances.

To create an alarm to terminate an idle instance using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under INSTANCES, choose Instances.

Select the instance. On the Monitoring tab, choose Create Alarm.

In the Alarm Details for dialog box, choose Create Alarm.

If you want to receive an email when the alarm is triggered, in the Create Alarm for dialog box, for Send a notification to, choose an existing Amazon SNS topic, or choose Create Topic to create a new one.

To create a new topic, for Send a notification to, type a name for the topic, and then for With these recipients, type the email addresses of the recipients (separated by commas). After you create the alarm, you will receive a subscription confirmation email that you must accept before you can get notifications for this topic.

Select Take the action, and then choose Terminate this instance.

If prompted, select Create IAM role: EC2ActionsAccess to automatically create an IAM role so that AWS can automatically stop the instance on your behalf when the alarm is triggered.

For Whenever, choose a statistic and then choose the metric. In this example, choose Average and CPU Utilization.

For Is, define the metric threshold. In this example, type 10 percent.

For For at least, choose the sampling period for the alarm. In this example, type 24 consecutive periods of one hour.

To change the name of the alarm, for Name this alarm, type a new name.

If you don't type a name for the alarm, Amazon CloudWatch will automatically create one for you.

Note
You can adjust the alarm configuration based on your own requirements before creating the alarm, or you can edit them later. This includes the metric, threshold, duration, action, and notification settings. However, after you create an alarm, you cannot edit its name later.
Choose Create Alarm.

Adding Reboot Actions to Amazon CloudWatch Alarms

You can create an Amazon CloudWatch alarm that monitors an Amazon EC2 instance and automatically reboots the instance. The reboot alarm action is recommended for Instance Health Check failures (as opposed to the recover alarm action, which is suited for System Health Check failures). An instance reboot is equivalent to an operating system reboot. In most cases, it takes only a few minutes to reboot your instance. When you reboot an instance, it remains on the same physical host, so your instance keeps its public DNS name, private IP address, and any data on its instance store volumes.

Rebooting an instance doesn't start a new instance billing hour, unlike stopping and restarting your instance. For more information, see Reboot Your Instance in the Amazon EC2 User Guide for Linux Instances.

Important
To avoid a race condition between the reboot and recover actions, we recommend that you set the alarm threshold to 3 for 1 minute when creating alarms that reboot an Amazon EC2 instance.
To create an alarm to reboot an instance using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under INSTANCES, choose Instances.

Select the instance. On the Monitoring tab, choose Create Alarm.

In the Alarm Details for dialog box, choose Create Alarm.

If you want to receive an email when the alarm is triggered, in the Create Alarm for dialog box, for Send a notification to, choose an existing Amazon SNS topic, or choose Create Topic to create a new one.

To create a new topic, for Send a notification to, type a name for the topic, and for With these recipients, type the email addresses of the recipients (separated by commas). After you create the alarm, you will receive a subscription confirmation email that you must accept before you can get notifications for this topic.

Select Take the action, and then choose Reboot this instance.

If prompted, select Create IAM role: EC2ActionsAccess to automatically create an IAM role so that AWS can automatically stop the instance on your behalf when the alarm is triggered.

For Whenever, choose Status Check Failed (Instance).

For For at least, type 2.

For consecutive period(s) of, choose 1 minute.

To change the name of the alarm, for Name of alarm, type a new name.

If you don't type a name for the alarm, Amazon CloudWatch will automatically create one for you.

Choose Create Alarm.

Adding Recover Actions to Amazon CloudWatch Alarms

You can create an Amazon CloudWatch alarm that monitors an Amazon EC2 instance and automatically recovers the instance if it becomes impaired due to an underlying hardware failure or a problem that requires AWS involvement to repair. Terminated instances cannot be recovered. A recovered instance is identical to the original instance, including the instance ID, private IP addresses, Elastic IP addresses, and all instance metadata.

When the StatusCheckFailed_System alarm is triggered, and the recover action is initiated, you will be notified by the Amazon SNS topic that you chose when you created the alarm and associated the recover action. During instance recovery, the instance is migrated during an instance reboot, and any data that is in-memory is lost. When the process is complete, information is published to the SNS topic you've configured for the alarm. Anyone who is subscribed to this SNS topic will receive an email notification that includes the status of the recovery attempt and any further instructions. You will notice an instance reboot on the recovered instance.

Examples of problems that cause system status checks to fail include:

Loss of network connectivity
Loss of system power
Software issues on the physical host
Hardware issues on the physical host that impact network reachability
The recover action is supported only on instances with the following characteristics:

Use a C3, C4, M3, M4, R3, R4, T2, or X1 instance type
Run in a VPC (not EC2-Classic)
Use shared tenancy (the tenancy attribute is set to default)
Use EBS volumes only (do not configure instance store volumes). For more information, see 'Recover this instance' is disabled.
If your instance has a public IP address, it retains the public IP address after recovery.

Important
To avoid a race condition between the reboot and recover actions, we recommend that you set the alarm threshold to 2 for 1 minute when creating alarms that recover an Amazon EC2 instance.
To create an alarm to recover an instance using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, under INSTANCES, choose Instances.

Select the instance. On the Monitoring tab, choose Create Alarm.

In the Alarm Details for dialog box, choose Create Alarm.

To receive an email when the alarm is triggered, in the Create Alarm for dialog box, for Send a notification to, choose an existing Amazon SNS topic, or choose Create Topic to create a new one.

To create a new topic, for Send a notification to, type a name for the topic, and for With these recipients, type the email addresses of the recipients (separated by commas). After you create the alarm, you will receive a subscription confirmation email that you must accept before you can get email for this topic.

Select Take the action, and then choose Recover this instance.

If prompted, select Create IAM role: EC2ActionsAccess to automatically create an IAM role so that AWS can automatically stop the instance on your behalf when the alarm is triggered.

For Whenever, choose Status Check Failed (System).

For For at least, type 2.

For consecutive period(s) of, choose 1 minute.

To change the name of the alarm, for Name of alarm, type a new name.

If you don't type a name for the alarm, Amazon CloudWatch will automatically create one for you.

Choose Create Alarm.

Using the Amazon CloudWatch Console to View the History of Triggered Alarms and Actions

You can view alarm and action history in the Amazon CloudWatch console. Amazon CloudWatch keeps the last two weeks' worth of alarm and action history.

To view the history of triggered alarms and actions

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

In the navigation pane, choose Alarms.

Select an alarm.

The Details tab shows the most recent state transition along with the time and metric values.

Choose the History tab to view the most recent history entries.

Amazon CloudWatch Alarm Action Scenarios

You can use the Amazon EC2 console to create alarm actions that stop or terminate an Amazon EC2 instance when certain conditions are met. In the following screen capture of the console page where you set the alarm actions, we've numbered the settings. We've also numbered the settings in the scenarios that follow, to help you create the appropriate actions.


          Create Alarm for dialog box
        
Scenario 1: Stop Idle Development and Test Instances

Create an alarm that stops an instance used for software development or testing when it has been idle for at least an hour.

Setting	Value

Stop

Maximum

CPUUtilization

<=

10%

60 minutes

1
Scenario 2: Stop Idle Instances

Create an alarm that stops an instance and sends an email when the instance has been idle for 24 hours.

Setting	Value

Stop and email

Average

CPUUtilization

<=

5%

60 minutes

24
Scenario 3: Send Email About Web Servers with Unusually High Traffic

Create an alarm that sends email when an instance exceeds 10 GB of outbound network traffic per day.

Setting	Value

Email

Sum

NetworkOut

>

10 GB

1 day

1
Scenario 4: Stop Web Servers with Unusually High Traffic

Create an alarm that stops an instance and send a text message (SMS) if outbound traffic exceeds 1 GB per hour.

Setting	Value

Stop and send SMS

Sum

NetworkOut

>

1 GB

1 hour

1
Scenario 5: Stop an Instance Experiencing a Memory Leak

Create an alarm that stops an instance when memory utilization reaches or exceeds 90%, so that application logs can be retrieved for troubleshooting.

Note
The MemoryUtilization metric is a custom metric. In order to use the MemoryUtilization metric, you must install the Perl scripts for Linux instances. For more information, see Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances.
Setting	Value

Stop

Maximum

MemoryUtilization

>=

90%

1 minute

1
Scenario 6: Stop an Impaired Instance

Create an alarm that stops an instance that fails three consecutive status checks (performed at 5-minute intervals).

Setting	Value

Stop

Average

StatusCheckFailed_System

>=

1

15 minutes

1
Scenario 7: Terminate Instances When Batch Processing Jobs Are Complete

Create an alarm that terminates an instance that runs batch jobs when it is no longer sending results data.

Setting	Value

Terminate

Maximum

NetworkOut

<=

100,000 bytes

5 minutes

1

Automating Amazon EC2 with CloudWatch Events

Amazon CloudWatch Events enables you to automate your AWS services and respond automatically to system events such as application availability issues or resource changes. Events from AWS services are delivered to CloudWatch Events in near real time. You can write simple rules to indicate which events are of interest to you, and the automated actions to take when an event matches a rule. The actions that can be automatically triggered include the following:

Invoking an AWS Lambda function
Invoking Amazon EC2 Run Command
Relaying the event to Amazon Kinesis Streams
Activating an AWS Step Functions state machine
Notifying an Amazon SNS topic or an AWS SMS queue
Some examples of using CloudWatch Events with Amazon EC2 include:

Activating a Lambda function whenever a new Amazon EC2 instance starts.
Notifying an Amazon SNS topic when an Amazon EBS volume is created or modified.
Sending a command to one or more Amazon EC2 instances using Amazon EC2 Run Command whenever a certain event in another AWS service occurs.
For more information, see the Amazon CloudWatch Events User Guide.

Monitoring Memory and Disk Metrics for Amazon EC2 Linux Instances

The Amazon CloudWatch Monitoring Scripts for Amazon Elastic Compute Cloud (Amazon EC2) Linux-based instances demonstrate how to produce and consume Amazon CloudWatch custom metrics. These sample Perl scripts comprise a fully functional example that reports memory, swap, and disk space utilization metrics for a Linux instance. You can download the Amazon CloudWatch Monitoring Scripts for Linux from the AWS sample code library.

Important
These scripts are examples only. They are provided as is and are not supported.
Standard Amazon CloudWatch usage charges for custom metrics apply to your use of these scripts. For more information, see the Amazon CloudWatch pricing page.

Contents

Supported Systems
Package Contents
Prerequisites
Getting Started
mon-put-instance-data.pl
mon-get-instance-stats.pl
Viewing Your Custom Metrics in the Console
Troubleshooting
Supported Systems

These monitoring scripts are intended for use with Amazon EC2 instances running Linux. The scripts have been tested on instances using the following Amazon Machine Images (AMIs), both 32-bit and 64-bit versions:

Amazon Linux 2014.09.2
Red Hat Enterprise Linux 7.4 and 6.9
SUSE Linux Enterprise Server 12
Ubuntu Server 16.04 and 14.04
You can use EC2Config on Amazon EC2 instances running Windows to monitor memory and disk metrics by sending this data to CloudWatch Logs. For more information, see Sending Performance Counters to CloudWatch and Logs to CloudWatch Logs in the Amazon EC2 User Guide for Windows Instances.

Package Contents

The package for the monitoring scripts contains the following files:

CloudWatchClient.pm—Shared Perl module that simplifies calling Amazon CloudWatch from other scripts.
mon-put-instance-data.pl—Collects system metrics on an Amazon EC2 instance (memory, swap, disk space utilization) and sends them to Amazon CloudWatch.
mon-get-instance-stats.pl—Queries Amazon CloudWatch and displays the most recent utilization statistics for the EC2 instance on which this script is executed.
awscreds.template—File template for AWS credentials that stores your access key ID and secret access key.
LICENSE.txt—Text file containing the Apache 2.0 license.
NOTICE.txt—Copyright notice.
Prerequisites

With some versions of Linux, you must install additional modules before the monitoring scripts will work.

Amazon Linux AMI

If you are running Amazon Linux AMI version 2014.03 or later, you must install additional Perl modules.

To install the required packages

Log on to your instance. For more information, see Connect to Your Linux Instance.

At a command prompt, install packages as follows:

Copy
sudo yum install perl-Switch perl-DateTime perl-Sys-Syslog perl-LWP-Protocol-https -y
Red Hat Enterprise Linux

You must install additional Perl modules.

To install the required packages on Red Hat Enterprise Linux 6.9

Log on to your instance. For more information, see Connect to Your Linux Instance.

At a command prompt, install packages as follows:

Copy
sudo yum install perl-DateTime perl-Net-SSLeay perl-IO-Socket-SSL perl-Digest-SHA gcc -y
sudo yum install zip unzip
Run CPAN as an elevated user:

Copy
sudo cpan
Press ENTER through the prompts until you see the following prompt:

Copy
cpan[1]>
At the CPAN prompt, run each of the below commands: run one command and it installs, and when you return to the CPAN prompt, run the next command. Press ENTER like before when prompted to continue through the process:

Copy
cpan[1]> install YAML 
cpan[1]> install LWP::Protocol::https 
cpan[1]> install Sys::Syslog 
cpan[1]> install Switch 
To install the required packages on Red Hat Enterprise Linux 7.4

Log on to your instance. For more information, see Connect to Your Linux Instance.

At a command prompt, install packages as follows:

Copy
sudo yum install perl-Switch perl-DateTime perl-Sys-Syslog perl-LWP-Protocol-https perl-Digest-SHA --enablerepo="rhui-REGION-rhel-server-optional" -y 
sudo yum install zip unzip
SUSE Linux Enterprise Server

You must install additional Perl modules.

To install the required packages on SUSE

Log on to your instance. For more information, see Connect to Your Linux Instance.

At a command prompt, install packages as follows:

Copy
sudo zypper install perl-Switch perl-DateTime
sudo zypper install –y "perl(LWP::Protocol::https)"
Ubuntu Server

You must configure your server as follows.

To install the required packages on Ubuntu

Log on to your instance. For more information, see Connect to Your Linux Instance.

At a command prompt, install packages as follows:

Copy
sudo apt-get update
sudo apt-get install unzip
sudo apt-get install libwww-perl libdatetime-perl
Getting Started

The following steps show you how to download, uncompress, and configure the CloudWatch Monitoring Scripts on an EC2 Linux instance.

To download, install, and configure the monitoring scripts

At a command prompt, move to a folder where you want to store the monitoring scripts and run the following command to download them:

Copy
curl http://aws-cloudwatch.s3.amazonaws.com/downloads/CloudWatchMonitoringScripts-1.2.1.zip -O
Run the following commands to install the monitoring scripts you downloaded:

Copy
unzip CloudWatchMonitoringScripts-1.2.1.zip
rm CloudWatchMonitoringScripts-1.2.1.zip
cd aws-scripts-mon
Ensure that the scripts have permission to perform CloudWatch operations using one of the following options:

If you associated an AWS Identity and Access Management (IAM) role with your instance, verify that it grants permissions to perform the following operations:

cloudwatch:PutMetricData
cloudwatch:GetMetricStatistics
cloudwatch:ListMetrics
ec2:DescribeTags
Specify your AWS credentials in a credentials file. First, copy the awscreds.template file included with the monitoring scripts to awscreds.conf as follows:

Copy
cp awscreds.template awscreds.conf
Add the following content to this file:

Copy
AWSAccessKeyId=my-access-key-id
AWSSecretKey=my-secret-access-key
For information about how to view your AWS credentials, see Understanding and Getting Your Security Credentials in the Amazon Web Services General Reference.

mon-put-instance-data.pl

This script collects memory, swap, and disk space utilization data on the current system. It then makes a remote call to Amazon CloudWatch to report the collected data as custom metrics.

Options

Name	Description
--mem-util
Collects and sends the MemoryUtilization metrics in percentages. This option reports only memory allocated by applications and the operating system, and excludes memory in cache and buffers.
--mem-used
Collects and sends the MemoryUsed metrics, reported in megabytes. This option reports only memory allocated by applications and the operating system, and excludes memory in cache and buffers.
--mem-used-incl-cache-buff
Collects and sends the MemoryUsed metrics, reported in megabytes. This option reports used in cache and buffers, as well as memory allocated by applications and the operating system.
--mem-avail
Collects and sends the MemoryAvailable metrics, reported in megabytes. This option reports memory available for use by applications and the operating system.
--swap-util
Collects and sends SwapUtilization metrics, reported in percentages.
--swap-used
Collects and sends SwapUsed metrics, reported in megabytes.
--disk-path=PATH
Selects the disk on which to report.

PATH can specify a mount point or any file located on a mount point for the filesystem that needs to be reported. For selecting multiple disks, specify a --disk-path=PATH for each one of them.

To select a disk for the filesystems mounted on / and /home, use the following parameters:

--disk-path=/ --disk-path=/home
--disk-space-util
Collects and sends the DiskSpaceUtilization metric for the selected disks. The metric is reported in percentages.

Note that the disk utilization metrics calculated by this script differ from the values calculated by the df -k -l command. If you find the values from df -k -l more useful, you can change the calculations in the script.
--disk-space-used
Collects and sends the DiskSpaceUsed metric for the selected disks. The metric is reported by default in gigabytes.

Due to reserved disk space in Linux operating systems, disk space used and disk space available might not accurately add up to the amount of total disk space.
--disk-space-avail
Collects and sends the DiskSpaceAvailable metric for the selected disks. The metric is reported in gigabytes.

Due to reserved disk space in the Linux operating systems, disk space used and disk space available might not accurately add up to the amount of total disk space.
--memory-units=UNITS
Specifies units in which to report memory usage. If not specified, memory is reported in megabytes. UNITS may be one of the following: bytes, kilobytes, megabytes, gigabytes.
--disk-space-units=UNITS
Specifies units in which to report disk space usage. If not specified, disk space is reported in gigabytes. UNITS may be one of the following: bytes, kilobytes, megabytes, gigabytes.
--aws-credential- file=PATH
Provides the location of the file containing AWS credentials.

This parameter cannot be used with the --aws-access-key-id and --aws-secret-key parameters.
--aws-access-key-id=VALUE
Specifies the AWS access key ID to use to identify the caller. Must be used together with the --aws-secret-key option. Do not use this option with the --aws-credential-file parameter.
--aws-secret-key=VALUE
Specifies the AWS secret access key to use to sign the request to CloudWatch. Must be used together with the --aws-access-key-id option. Do not use this option with --aws-credential-file parameter.
--aws-iam-role=VALUE
Specifies the IAM role used to provide AWS credentials. The value =VALUE is required. If no credentials are specified, the default IAM role associated with the EC2 instance is applied. Only one IAM role can be used. If no IAM roles are found, or if more than one IAM role is found, the script will return an error.

Do not use this option with the --aws-credential-file, --aws-access-key-id, or --aws-secret-key parameters.
--aggregated[=only]
Adds aggregated metrics for instance type, AMI ID, and overall for the region. The value =only is optional; if specified, the script reports only aggregated metrics.
--auto-scaling[=only]
Adds aggregated metrics for the Auto Scaling group. The value =only is optional; if specified, the script reports only Auto Scaling metrics. The IAM policy associated with the IAM account or role using the scripts need to have permissions to call the EC2 action DescribeTags.
--verify
Performs a test run of the script that collects the metrics, prepares a complete HTTP request, but does not actually call CloudWatch to report the data. This option also checks that credentials are provided. When run in verbose mode, this option outputs the metrics that will be sent to CloudWatch.
--from-cron
Use this option when calling the script from cron. When this option is used, all diagnostic output is suppressed, but error messages are sent to the local system log of the user account.
--verbose
Displays detailed information about what the script is doing.
--help
Displays usage information.
--version
Displays the version number of the script.
Examples

The following examples assume that you provided an IAM role or awscreds.conf file. Otherwise, you must provide credentials using the --aws-access-key-id and --aws-secret-key parameters for these commands.

To perform a simple test run without posting data to CloudWatch

Copy
./mon-put-instance-data.pl --mem-util --verify --verbose
To collect all available memory metrics and send them to CloudWatch

Copy
./mon-put-instance-data.pl --mem-util --mem-used-incl-cache-buff --mem-used --mem-avail
To set a cron schedule for metrics reported to CloudWatch

Start editing the crontab using the following command:

Copy
crontab -e 
Add the following command to report memory and disk space utilization to CloudWatch every five minutes:

Copy
*/5 * * * * ~/aws-scripts-mon/mon-put-instance-data.pl --mem-used-incl-cache-buff --mem-util --disk-space-util --disk-path=/ --from-cron
If the script encounters an error, the script will write the error message in the system log.

To collect aggregated metrics for an Auto Scaling group and send them to Amazon CloudWatch without reporting individual instance metrics

Copy
./mon-put-instance-data.pl --mem-util --mem-used --mem-avail --auto-scaling=only
To collect aggregated metrics for instance type, AMI ID and region, and send them to Amazon CloudWatch without reporting individual instance metrics

Copy
./mon-put-instance-data.pl --mem-util --mem-used --mem-avail --aggregated=only
mon-get-instance-stats.pl

This script queries CloudWatch for statistics on memory, swap, and disk space metrics within the time interval provided using the number of most recent hours. This data is provided for the Amazon EC2 instance on which this script is executed.

Options

Name	Description
--recent-hours=N
Specifies the number of recent hours to report on, as represented by N where N is an integer.
--aws-credential-file=PATH
Provides the location of the file containing AWS credentials.
--aws-access-key-id=VALUE
Specifies the AWS access key ID to use to identify the caller. Must be used together with the --aws-secret-key option. Do not use this option with the --aws-credential-file option.
--aws-secret-key=VALUE
Specifies the AWS secret access key to use to sign the request to CloudWatch. Must be used together with the --aws-access-key-id option. Do not use this option with --aws-credential-file option.
--aws-iam-role=VALUE
Specifies the IAM role used to provide AWS credentials. The value =VALUE is required. If no credentials are specified, the default IAM role associated with the EC2 instance is applied. Only one IAM role can be used. If no IAM roles are found, or if more than one IAM role is found, the script will return an error.

Do not use this option with the --aws-credential-file, --aws-access-key-id, or --aws-secret-key parameters.
--verify
Performs a test run of the script that collects the metrics, prepares a complete HTTP request, but does not actually call CloudWatch to report the data. This option also checks that credentials are provided. When run in verbose mode, this option outputs the metrics that will be sent to CloudWatch.
--verbose
Displays detailed information about what the script is doing.
--help
Displays usage information.
--version
Displays the version number of the script.
Example

To get utilization statistics for the last 12 hours, run the following command:

Copy
./mon-get-instance-stats.pl --recent-hours=12
The following is an example response:

Instance metric statistics for the last 12 hours.

CPU Utilization
    Average: 1.06%, Minimum: 0.00%, Maximum: 15.22%

Memory Utilization
    Average: 6.84%, Minimum: 6.82%, Maximum: 6.89%

Swap Utilization
    Average: N/A, Minimum: N/A, Maximum: N/A

Disk Space Utilization on /dev/xvda1 mounted as /
    Average: 9.69%, Minimum: 9.69%, Maximum: 9.69%
Viewing Your Custom Metrics in the Console

After you successfully run the mon-put-instance-data.pl script, you can view your custom metrics in the Amazon CloudWatch console.

To view custom metrics

Run mon-put-instance-data.pl as described previously.

Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.

Choose View Metrics.

For Viewing, your custom metrics posted by the script are displayed with the prefix System/Linux.

Troubleshooting

The CloudWatchClient.pm module caches instance metadata locally. If you create an AMI from an instance where you have run the monitoring scripts, any instances launched from the AMI within the cache TTL (default: six hours, 24 hours for Auto Scaling groups) emit metrics using the instance ID of the original instance. After the cache TTL time period passes, the script retrieves fresh data and the monitoring scripts use the instance ID of the current instance. To immediately correct this, remove the cached data using the following command:

Copy
rm /var/tmp/aws-mon/instance-id

