Troubleshooting Instances

The following documentation can help you troubleshoot problems that you might have with your instance.

Contents

What To Do If An Instance Immediately Terminates
Troubleshooting Connecting to Your Instance
Troubleshooting Stopping Your Instance
Troubleshooting Terminating (Shutting Down) Your Instance
Troubleshooting Instance Recovery Failures
Troubleshooting Instances with Failed Status Checks
Troubleshooting Instance Capacity
Getting Console Output and Rebooting Instances
My Instance is Booting from the Wrong Volume
For additional help with Windows instances, see Troubleshooting Windows Instances in the Amazon EC2 User Guide for Windows Instances.

You can also search for answers and post questions on the Amazon EC2 forum.

What To Do If An Instance Immediately Terminates

After you launch an instance, we recommend that you check its status to confirm that it goes from the pending state to the running state, not the terminated state.

The following are a few reasons why an instance might immediately terminate:

You've reached your EBS volume limit. For information about the volume limit, and to submit a request to increase your volume limit, see Request to Increase the Amazon EBS Volume Limit.
An EBS snapshot is corrupt.
The instance store-backed AMI you used to launch the instance is missing a required part (an image.part.xx file).
Getting the Reason for Instance Termination

You can use the Amazon EC2 console, CLI, or API to get information about the reason that the instance terminated.

To get the reason that an instance terminated using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances, and select your instance.

In the Description tab, locate the reason next to the label State transition reason. If the instance is still running, there's typically no reason listed. If you've explicitly stopped or terminated the instance, the reason is User initiated shutdown.

To get the reason that an instance terminated using the command line

Use the describe-instances command:

Copy
aws ec2 describe-instances --instance-id instance_id
In the JSON response that's displayed, locate the StateReason element. It looks similar to the following example.

"StateReason": {
  "Message": "Client.UserInitiatedShutdown: User initiated shutdown", 
  "Code": "Client.UserInitiatedShutdown"
},
This example response shows the reason code that you'll see after you stop or terminate a running instance. If the instance terminated immediately, you'll see code and message elements that describe the reason that the instance terminated (for example, VolumeLimitExceeded).

Troubleshooting Connecting to Your Instance

The following are possible problems you may have and error messages you may see while trying to connect to your instance.

Contents

Error connecting to your instance: Connection timed out
Error: User key not recognized by server
Error: Host key not found, Permission denied (publickey), or Authentication failed, permission denied
Error: Unprotected Private Key File
Error: Server refused our key or No supported authentication methods available
Error using MindTerm on Safari Browser
Error Using Mac OS X RDP Client
Cannot Ping Instance
For additional help with Windows instances, see Troubleshooting Windows Instances in the Amazon EC2 User Guide for Windows Instances.

You can also search for answers and post questions on the Amazon EC2 forum.

Error connecting to your instance: Connection timed out

If you try to connect to your instance and get an error message Network error: Connection timed out or Error connecting to [instance], reason: -> Connection timed out: connect, try the following:

Check your security group rules. You need a security group rule that allows inbound traffic from your public IPv4 address on the proper port.
Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
In the navigation pane, choose Instances, and then select your instance.
In the Description tab, next to Security groups, choose view rules to display the list of rules that are in effect.
For Linux instances: Verify that there is a rule that allows traffic from your computer to port 22 (SSH).
For Windows instances: Verify that there is a rule that allows traffic from your computer to port 3389 (RDP).
If your security group has a rule that allows inbound traffic from a single IP address, this address may not be static if your computer is on a corporate network or if you are connecting through an Internet service provider (ISP). Instead, specify the range of IP addresses used by client computers. If your security group does not have a rule that allows inbound traffic as described in the previous step, add a rule to your security group. For more information, see Authorizing Network Access to Your Instances.
[EC2-VPC] Check the route table for the subnet. You need a route that sends all traffic destined outside the VPC to the Internet gateway for the VPC.
Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
In the navigation pane, choose Instances, and then select your instance.
In the Description tab, write down the values of VPC ID and Subnet ID.
Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.
In the navigation pane, choose Internet Gateways. Verify that there is an Internet gateway attached to your VPC. Otherwise, choose Create Internet Gateway to create an Internet gateway. Select the Internet gateway, and then choose Attach to VPC and follow the directions to attach it to your VPC.
In the navigation pane, choose Subnets, and then select your subnet.
On the Route Table tab, verify that there is a route with 0.0.0.0/0 as the destination and the Internet gateway for your VPC as the target. Otherwise, choose the ID of the route table (rtb-xxxxxxxx) to navigate to the Routes tab for the route table, choose Edit, Add another route, enter 0.0.0.0/0 in Destination, select your Internet gateway from Target, and then choose Save.
If you're connecting to your instance using its IPv6 address, verify that there is a route for all IPv6 traffic (::/0) that points to the Internet gateway. If not, add a route with ::/0 as the destination, and the Internet gateway as the target.
[EC2-VPC] Check the network access control list (ACL) for the subnet. The network ACLs must allow inbound and outbound traffic from your local IP address on the proper port. The default network ACL allows all inbound and outbound traffic.
Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.
In the navigation pane, choose Your VPCs.
On the Summary tab, find Network ACL, choose the ID (acl-xxxxxxxx), and select the ACL.
On the Inbound Rules tab, verify that the rules allow traffic from your computer. Otherwise, delete or modify the rule that is blocking traffic from your computer.
On the Outbound Rules tab, verify that the rules allow traffic to your computer. Otherwise, delete or modify the rule that is blocking traffic to your computer.
If your computer is on a corporate network, ask your network administrator whether the internal firewall allows inbound and outbound traffic from your computer on port 22 (for Linux instances) or port 3389 (for Windows instances).
If you have a firewall on your computer, verify that it allows inbound and outbound traffic from your computer on port 22 (for Linux instances) or port 3389 (for Windows instances).
Check that your instance has a public IPv4 address. If not, you can associate an Elastic IP address with your instance. For more information, see Elastic IP Addresses.
Check the CPU load on your instance; the server may be overloaded. AWS automatically provides data such as Amazon CloudWatch metrics and instance status, which you can use to see how much CPU load is on your instance and, if necessary, adjust how your loads are handled. For more information, see Monitoring Your Instances Using CloudWatch.
If your load is variable, you can automatically scale your instances up or down using Auto Scaling and Elastic Load Balancing.
If your load is steadily growing, you can move to a larger instance type. For more information, see Resizing Your Instance.
To connect to your instance using an IPv6 address, check the following:

Your subnet must be associated with a route table that has a route for IPv6 traffic (::/0) to an Internet gateway.
Your security group rules must allow inbound traffic from your local IPv6 address on the proper port (22 for Linux and 3389 for Windows).
Your network ACL rules must allow inbound and outbound IPv6 traffic.
If you launched your instance from an older AMI, it may not be configured for DHCPv6 (IPv6 addresses are not automatically recognized on the network interface). For more information, see Configure IPv6 on Your Instances in the Amazon VPC User Guide.
Your local computer must have an IPv6 address, and must be configured to use IPv6.
Error: User key not recognized by server

If you use SSH to connect to your instance

Use ssh -vvv to get triple verbose debugging information while connecting:
Copy
ssh -vvv -i [your key name].pem ec2-user@[public DNS address of your instance].compute-1.amazonaws.com
The following sample output demonstrates what you might see if you were trying to connect to your instance with a key that was not recognized by the server:
open/ANT/myusername/.ssh/known_hosts).
debug2: bits set: 504/1024
debug1: ssh_rsa_verify: signature correct
debug2: kex_derive_keys
debug2: set_newkeys: mode 1
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug2: set_newkeys: mode 0
debug1: SSH2_MSG_NEWKEYS received
debug1: Roaming not allowed by server
debug1: SSH2_MSG_SERVICE_REQUEST sent
debug2: service_accept: ssh-userauth
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug2: key: boguspem.pem ((nil))
debug1: Authentications that can continue: publickey
debug3: start over, passed a different list publickey
debug3: preferred gssapi-keyex,gssapi-with-mic,publickey,keyboard-interactive,password
debug3: authmethod_lookup publickey
debug3: remaining preferred: keyboard-interactive,password
debug3: authmethod_is_enabled publickey
debug1: Next authentication method: publickey
debug1: Trying private key: boguspem.pem
debug1: read PEM private key done: type RSA
debug3: sign_and_send_pubkey: RSA 9c:4c:bc:0c:d0:5c:c7:92:6c:8e:9b:16:e4:43:d8:b2
debug2: we sent a publickey packet, wait for reply
debug1: Authentications that can continue: publickey
debug2: we did not send a packet, disable method
debug1: No more authentication methods to try.
Permission denied (publickey).
If you use SSH (MindTerm) to connect to your instance

If Java is not enabled, the server does not recognize the user key. To enable Java, go to How do I enable Java in my web browser? in the Java documentation.
If you use PuTTY to connect to your instance

Verify that your private key (.pem) file has been converted to the format recognized by PuTTY (.ppk). For more information about converting your private key, see Connecting to Your Linux Instance from Windows Using PuTTY.
Note
In PuTTYgen, load your private key file and select Save Private Key rather than Generate.
Verify that you are connecting with the appropriate user name for your AMI. Enter the user name in the Host name box in the PuTTY Configuration window.
For an Amazon Linux AMI, the user name is ec2-user.
For a RHEL AMI, the user name is ec2-user or root.
For an Ubuntu AMI, the user name is ubuntu or root.
For a Centos AMI, the user name is centos.
For a Fedora AMI, the user name is ec2-user.
For SUSE, the user name is ec2-user or root.
Otherwise, if ec2-user and root don't work, check with the AMI provider.
Verify that you have an inbound security group rule to allow inbound traffic to the appropriate port. For more information, see Authorizing Network Access to Your Instances.
Error: Host key not found, Permission denied (publickey), or Authentication failed, permission denied

If you connect to your instance using SSH and get any of the following errors, Host key not found in [directory], Permission denied (publickey), or Authentication failed, permission denied, verify that you are connecting with the appropriate user name for your AMI and that you have specified the proper private key (.pem) file for your instance. For MindTerm clients, enter the user name in the User name box in the Connect To Your Instance window.

The appropriate user names are as follows:

For an Amazon Linux AMI, the user name is ec2-user.
For a RHEL AMI, the user name is ec2-user or root.
For an Ubuntu AMI, the user name is ubuntu or root.
For a Centos AMI, the user name is centos.
For a Fedora AMI, the user name is ec2-user.
For SUSE, the user name is ec2-user or root.
Otherwise, if ec2-user and root don't work, check with the AMI provider.
Confirm that you are using the private key file that corresponds to the key pair that you selected when you launched the instance.

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

Select your instance. In the Description tab, verify the value of Key pair name.

If you did not specify a key pair when you launched the instance, you can terminate the instance and launch a new instance, ensuring that you specify a key pair. If this is an instance that you have been using but you no longer have the .pem file for your key pair, you can replace the key pair with a new one. For more information, see Connecting to Your Linux Instance if You Lose Your Private Key.

If you generated your own key pair, ensure that your key generator is set up to create RSA keys. DSA keys are not accepted.

If you get a Permission denied (publickey) error and none of the above applies (for example, you were able to connect previously), the permissions on the home directory of your instance may have been changed. Permissions for /home/ec2-user/.ssh/authorized_keys must be limited to the owner only.

To verify the permissions on your instance

Stop your instance and detach the root volume. For more information, see Stop and Start Your Instance and Detaching an Amazon EBS Volume from an Instance.

Launch a temporary instance in the same Availability Zone as your current instance (use a similar or the same AMI as you used for your current instance), and attach the root volume to the temporary instance. For more information, see Attaching an Amazon EBS Volume to an Instance.

Connect to the temporary instance, create a mount point, and mount the volume that you attached. For more information, see Making an Amazon EBS Volume Available for Use.

From the temporary instance, check the permissions of the /home/ec2-user/ directory of the attached volume. If necessary, adjust the permissions as follows:

Copy
[ec2-user ~]$ chmod 600 mount_point/home/ec2-user/.ssh/authorized_keys
Copy
[ec2-user ~]$ chmod 700 mount_point/home/ec2-user/.ssh
Copy
[ec2-user ~]$ chmod 700 mount_point/home/ec2-user
Unmount the volume, detach it from the temporary instance, and re-attach it to the original instance. Ensure that you specify the correct device name for the root volume; for example, /dev/xvda.

Start your instance. If you no longer require the temporary instance, you can terminate it.

Error: Unprotected Private Key File

Your private key file must be protected from read and write operations from any other users. If your private key can be read or written to by anyone but you, then SSH ignores your key and you see the following warning message below.

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0777 for '.ssh/my_private_key.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
bad permissions: ignore key: .ssh/my_private_key.pem
Permission denied (publickey).
If you see a similar message when you try to log in to your instance, examine the first line of the error message to verify that you are using the correct public key for your instance. The above example uses the private key .ssh/my_private_key.pem with file permissions of 0777, which allow anyone to read or write to this file. This permission level is very insecure, and so SSH ignores this key. To fix the error, execute the following command, substituting the path for your private key file.

Copy
[ec2-user ~]$ chmod 0400 .ssh/my_private_key.pem
Error: Server refused our key or No supported authentication methods available

If you use PuTTY to connect to your instance and get either of the following errors, Error: Server refused our key or Error: No supported authentication methods available, verify that you are connecting with the appropriate user name for your AMI. Enter the user name in the User name box in the PuTTY Configuration window.

The appropriate user names are as follows:

For an Amazon Linux AMI, the user name is ec2-user.
For a RHEL AMI, the user name is ec2-user or root.
For an Ubuntu AMI, the user name is ubuntu or root.
For a Centos AMI, the user name is centos.
For a Fedora AMI, the user name is ec2-user.
For SUSE, the user name is ec2-user or root.
Otherwise, if ec2-user and root don't work, check with the AMI provider.
You should also verify that your private key (.pem) file has been correctly converted to the format recognized by PuTTY (.ppk). For more information about converting your private key, see Connecting to Your Linux Instance from Windows Using PuTTY.

Error using MindTerm on Safari Browser

If you use MindTerm to connect to your instance, and are using the Safari web browser, you may get the following error:

Error connecting to your_instance_ip, reason: 
 —> Key exchange failed: Host authentication failed
You need to update the browser's security settings to allow the AWS Management Console to run the Java plugin in unsafe mode.

To enable the Java plugin to run in unsafe mode

In Safari, keep the Amazon EC2 console open, and choose Safari, Preferences, Security.

Choose Plug-in Settings (or Manage Website Settings on older versions of Safari).

Choose the Java plugin on the left, then locate the AWS Management Console URL in the Currently Open Websites list. Select Run in Unsafe Mode from its associated list.

When prompted, choose Trust in the warning dialog. Choose Done to return the browser.

Error Using Mac OS X RDP Client

If you are connecting to a Windows Server 2012 R2 instance using the Remote Desktop Connection client from the Microsoft website, you may get the following error:

Remote Desktop Connection cannot verify the identity of the computer that you want to connect to.
Download the Microsoft Remote Desktop app from the Apple iTunes store, and use the app to connect to your instance.

Cannot Ping Instance

The ping command is a type of ICMP traffic — if you are unable to ping your instance, ensure that your inbound security group rules allow ICMP traffic for the Echo Request message from all sources, or from the computer or instance from which you are issuing the command. If you are unable to issue a ping command from your instance, ensure that your outbound security group rules allow ICMP traffic for the Echo Request message to all destinations, or to the host that you are attempting to ping.

Troubleshooting Stopping Your Instance

If you have stopped your Amazon EBS-backed instance and it appears "stuck" in the stopping state, there may be an issue with the underlying host computer.

First, try stopping the instance again. If you are using the stop-instances (AWS CLI) command be sure to use the --force option.

If you can't force the instance to stop, you can create an AMI from the instance and launch a replacement instance.

You are not billed for any instance hours while an instance is not in the running state.

To create a replacement instance

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances and select the instance.

Choose Actions, Image, Create Image.

In the Create Image dialog box, fill in the following fields and then choose Create Image:

Specify a name and description for the AMI.

Choose No reboot.

Launch an instance from the AMI and verify that the instance is working.

Select the stuck instance, choose Actions, Instance State, Terminate. If the instance also gets stuck terminating, Amazon EC2 automatically forces it to terminate within a few hours.

If you are unable to create an AMI from the instance as described in the previous procedure, you can set up a replacement instance as follows:

To create a replacement instance (if the previous procedure fails)

Select the instance, open the Description tab, and view the Block devices list. Select each volume and write down its volume ID. Be sure to note which volume is the root volume.

In the navigation pane, choose Volumes. Select each volume for the instance, and choose Actions, Create Snapshot.

In the navigation pane, choose Snapshots. Select the snapshot that you just created, and choose Actions, Create Volume.

Launch an instance of the same type as the stuck instance (Amazon Linux, Windows, and so on). Note the volume ID and device name of its root volume.

In the navigation pane, choose Instances, select the instance that you just launched, choose Actions, Instance State, and then choose Stop.

In the navigation pane, choose Volumes, select the root volume of the stopped instance, and choose Actions, Detach Volume.

Select the root volume that you created from the stuck instance, choose Actions, Attach Volume, and attach it to the new instance as its root volume (using the device name that you wrote down). Attach any additional non-root volumes to the instance.

In the navigation pane, choose Instances and select the replacement instance. Choose Actions, Instance State, Start. Verify that the instance is working.

Select the stuck instance, choose Actions, Instance State, Terminate. If the instance also gets stuck terminating, Amazon EC2 automatically forces it to terminate within a few hours.

If you're unable to complete these procedures, you can post a request for help to the Amazon EC2 forum. To help expedite a resolution, include the instance ID and describe the steps that you've already taken.

Troubleshooting Terminating (Shutting Down) Your Instance

You are not billed for any instance hours while an instance is not in the running state. In other words, when you terminate an instance, you stop incurring charges for that instance as soon as its state changes to shutting-down.

Delayed Instance Termination

If your instance remains in the shutting-down state longer than a few minutes, it might be delayed due to shutdown scripts being run by the instance.

Another possible cause is a problem with the underlying host computer. If your instance remains in the shutting-down state for several hours, Amazon EC2 treats it as a stuck instance and forcibly terminates it.

If it appears that your instance is stuck terminating and it has been longer than several hours, post a request for help to the Amazon EC2 forum. To help expedite a resolution, include the instance ID and describe the steps that you've already taken.

Terminated Instance Still Displayed

After you terminate an instance, it remains visible for a short while before being deleted. The status shows as terminated. If the entry is not deleted after several hours, contact Support.

Automatically Launch or Terminate Instances

If you terminate all your instances, you may see that we launch a new instance for you. If you launch an instance, you may see that we terminate one of your instances. If you stop an instance, you may see that we terminate the instance and launch a new instance. Generally, these behaviors mean that you've used Auto Scaling or Elastic Beanstalk to scale your computing resources automatically based on criteria that you've defined.

For more information, see the Auto Scaling User Guide or the AWS Elastic Beanstalk Developer Guide.

Troubleshooting Instance Recovery Failures

The following issues can cause automatic recovery of your instance to fail:

Temporary, insufficient capacity of replacement hardware.
The instance has an attached instance store storage, which is an unsupported configuration for automatic instance recovery.
There is an ongoing Service Health Dashboard event that prevented the recovery process from successfully executing. Refer to http://status.aws.amazon.com/ for the latest service availability information.
The instance has reached the maximum daily allowance of three recovery attempts.
The automatic recovery process will attempt to recover your instance for up to three separate failures per day. If the instance system status check failure persists, we recommend that you manually start and stop the instance. For more information, see Stop and Start Your Instance.

Your instance may subsequently be retired if automatic recovery fails and a hardware degradation is determined to be the root cause for the original system status check failure.

Troubleshooting Instances with Failed Status Checks

Topics

Initial Steps
Retrieving System Logs
Troubleshooting System Log Errors for Linux-Based Instances
Out of memory: kill process
ERROR: mmu_update failed (Memory management update failed)
I/O error (Block device failure)
IO ERROR: neither local nor remote disk (Broken distributed block device)
request_module: runaway loop modprobe (Looping legacy kernel modprobe on older Linux versions)
"FATAL: kernel too old" and "fsck: No such file or directory while trying to open /dev" (Kernel and AMI mismatch)
"FATAL: Could not load /lib/modules" or "BusyBox" (Missing kernel modules)
ERROR Invalid kernel (EC2 incompatible kernel)
request_module: runaway loop modprobe (Looping legacy kernel modprobe on older Linux versions)
fsck: No such file or directory while trying to open... (File system not found)
General error mounting filesystems (Failed mount)
VFS: Unable to mount root fs on unknown-block (Root filesystem mismatch)
Error: Unable to determine major/minor number of root device... (Root file system/device mismatch)
XENBUS: Device with no driver...
... days without being checked, check forced (File system check required)
fsck died with exit status... (Missing device)
GRUB prompt (grubdom>)
Bringing up interface eth0: Device eth0 has different MAC address than expected, ignoring. (Hard-coded MAC address)
Unable to load SELinux Policy. Machine is in enforcing mode. Halting now. (SELinux misconfiguration)
XENBUS: Timeout connecting to devices (Xenbus timeout)
Initial Steps

If your instance fails a status check, first determine whether your applications are exhibiting any problems. If you verify that the instance is not running your applications as expected, follow these steps:

To investigate impaired instances using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances, and then select your instance.

In the details pane, choose Status Checks to see the individual results for all System Status Checks and Instance Status Checks.

If a system status check has failed, you can try one of the following options:

Create an instance recovery alarm. For more information, see Create Alarms That Stop, Terminate, or Recover an Instance in the Amazon CloudWatch User Guide.
For an instance using an Amazon EBS-backed AMI, stop and restart the instance.
For an instance using an instance-store backed AMI, terminate the instance and launch a replacement.
Wait for Amazon EC2 to resolve the issue.
Post your issue to the Amazon EC2 forum.
Retrieve the system log and look for errors.
Retrieving System Logs

If an instance status check fails, you can reboot the instance and retrieve the system logs. The logs may reveal an error that can help you troubleshoot the issue. Rebooting clears unnecessary information from the logs.

To reboot an instance and retrieve the system log

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances, and select your instance.

Choose Actions, Instance State, Reboot. It may take a few minutes for your instance to reboot.

Verify that the problem still exists; in some cases, rebooting may resolve the problem.

When the instance is in the running state, choose Actions, Instance Settings, Get System Log.

Review the log that appears on the screen, and use the list of known system log error statements below to troubleshoot your issue.

If your experience differs from our check results, or if you are having an issue with your instance that our checks did not detect, choose Submit feedback on the Status Checks tab to help us improve our detection tests.

If your issue is not resolved, you can post your issue to the Amazon EC2 forum.

Troubleshooting System Log Errors for Linux-Based Instances

For Linux-based instances that have failed an instance status check, such as the instance reachability check, verify that you followed the steps above to retrieve the system log. The following list contains some common system log errors and suggested actions you can take to resolve the issue for each error .

Memory Errors

Out of memory: kill process
ERROR: mmu_update failed (Memory management update failed)
Device Errors

I/O error (Block device failure)
IO ERROR: neither local nor remote disk (Broken distributed block device)
Kernel Errors

request_module: runaway loop modprobe (Looping legacy kernel modprobe on older Linux versions)
"FATAL: kernel too old" and "fsck: No such file or directory while trying to open /dev" (Kernel and AMI mismatch)
"FATAL: Could not load /lib/modules" or "BusyBox" (Missing kernel modules)
ERROR Invalid kernel (EC2 incompatible kernel)
File System Errors

request_module: runaway loop modprobe (Looping legacy kernel modprobe on older Linux versions)
fsck: No such file or directory while trying to open... (File system not found)
General error mounting filesystems (Failed mount)
VFS: Unable to mount root fs on unknown-block (Root filesystem mismatch)
Error: Unable to determine major/minor number of root device... (Root file system/device mismatch)
XENBUS: Device with no driver...
... days without being checked, check forced (File system check required)
fsck died with exit status... (Missing device)
Operating System Errors

GRUB prompt (grubdom>)
Bringing up interface eth0: Device eth0 has different MAC address than expected, ignoring. (Hard-coded MAC address)
Unable to load SELinux Policy. Machine is in enforcing mode. Halting now. (SELinux misconfiguration)
XENBUS: Timeout connecting to devices (Xenbus timeout)
Out of memory: kill process

An out of memory error is indicated by a system log entry similar to the one shown below.

[115879.769795] Out of memory: kill process 20273 (httpd) score 1285879
or a child 
[115879.769795] Killed process 1917 (php-cgi) vsz:467184kB, anon-
rss:101196kB, file-rss:204kB
Potential Cause

Exhausted memory

Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Do one of the following:

Stop the instance, and modify the instance to use a different instance type, and start the instance again. For example, a larger or a memory-optimized instance type.
Reboot the instance to return it to a non-impaired status. The problem will probably occur again unless you change the instance type.
Instance store-backed
Do one of the following:

Terminate the instance and launch a new instance, specifying a different instance type. For example, a larger or a memory-optimized instance type.
Reboot the instance to return it to an unimpaired status. The problem will probably occur again unless you change the instance type.
ERROR: mmu_update failed (Memory management update failed)

Memory management update failures are indicated by a system log entry similar to the following:

...
Press `ESC' to enter the menu... 0   [H[J  Booting 'Amazon Linux 2011.09 (2.6.35.14-95.38.amzn1.i686)'


root (hd0)

 Filesystem type is ext2fs, using whole disk

kernel /boot/vmlinuz-2.6.35.14-95.38.amzn1.i686 root=LABEL=/ console=hvc0 LANG=

en_US.UTF-8 KEYTABLE=us

initrd /boot/initramfs-2.6.35.14-95.38.amzn1.i686.img

ERROR: mmu_update failed with rc=-22
Potential Cause

Issue with Amazon Linux

Suggested Action

Post your issue to the Developer Forums or contact AWS Support.

I/O error (Block device failure)

An input/output error is indicated by a system log entry similar to the following example:

[9943662.053217] end_request: I/O error, dev sde, sector 52428288
[9943664.191262] end_request: I/O error, dev sde, sector 52428168
[9943664.191285] Buffer I/O error on device md0, logical block 209713024
[9943664.191297] Buffer I/O error on device md0, logical block 209713025
[9943664.191304] Buffer I/O error on device md0, logical block 209713026
[9943664.191310] Buffer I/O error on device md0, logical block 209713027
[9943664.191317] Buffer I/O error on device md0, logical block 209713028
[9943664.191324] Buffer I/O error on device md0, logical block 209713029
[9943664.191332] Buffer I/O error on device md0, logical block 209713030
[9943664.191339] Buffer I/O error on device md0, logical block 209713031
[9943664.191581] end_request: I/O error, dev sde, sector 52428280
[9943664.191590] Buffer I/O error on device md0, logical block 209713136
[9943664.191597] Buffer I/O error on device md0, logical block 209713137
[9943664.191767] end_request: I/O error, dev sde, sector 52428288
[9943664.191970] end_request: I/O error, dev sde, sector 52428288
[9943664.192143] end_request: I/O error, dev sde, sector 52428288
[9943664.192949] end_request: I/O error, dev sde, sector 52428288
[9943664.193112] end_request: I/O error, dev sde, sector 52428288
[9943664.193266] end_request: I/O error, dev sde, sector 52428288
...
Potential Causes

Instance type	Potential cause
Amazon EBS-backed
A failed Amazon EBS volume
Instance store-backed
A failed physical drive
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the instance.
Detach the volume.
Attempt to recover the volume.

Note
It's good practice to snapshot your Amazon EBS volumes often. This dramatically decreases the risk of data loss as a result of failure.
Re-attach the volume to the instance.
Detach the volume.
Instance store-backed
Terminate the instance and launch a new instance.

Note
Data cannot be recovered. Recover from backups.
Note
It's a good practice to use either Amazon S3 or Amazon EBS for backups. Instance store volumes are directly tied to single host and single disk failures.
IO ERROR: neither local nor remote disk (Broken distributed block device)

An input/output error on the device is indicated by a system log entry similar to the following example:

...
block drbd1: Local IO failed in request_timer_fn. Detaching...

Aborting journal on device drbd1-8.

block drbd1: IO ERROR: neither local nor remote disk

Buffer I/O error on device drbd1, logical block 557056

lost page write due to I/O error on drbd1

JBD2: I/O error detected when updating journal superblock for drbd1-8.
Potential Causes

Instance type	Potential cause
Amazon EBS-backed
A failed Amazon EBS volume
Instance store-backed
A failed physical drive
Suggested Action

Terminate the instance and launch a new instance.

For an Amazon EBS-backed instance you can recover data from a recent snapshot by creating an image from it. Any data added after the snapshot cannot be recovered.

request_module: runaway loop modprobe (Looping legacy kernel modprobe on older Linux versions)

This condition is indicated by a system log similar to the one shown below. Using an unstable or old Linux kernel (for example, 2.6.16-xenU) can cause an interminable loop condition at startup.

Linux version 2.6.16-xenU (builder@xenbat.amazonsa) (gcc version 4.0.1 
20050727 (Red Hat 4.0.1-5)) #1 SMP Mon May 28 03:41:49 SAST 2007

BIOS-provided physical RAM map:

 Xen: 0000000000000000 - 0000000026700000 (usable)

0MB HIGHMEM available.
...

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use a newer kernel, either GRUB-based or static, using one of the following options:

Option 1: Terminate the instance and launch a new instance, specifying the –kernel and –ramdisk parameters.

Option 2:

Stop the instance.
Modify the kernel and ramdisk attributes to use a newer kernel.
Start the instance.
Instance store-backed
Terminate the instance and launch a new instance, specifying the –kernel and –ramdisk parameters.
"FATAL: kernel too old" and "fsck: No such file or directory while trying to open /dev" (Kernel and AMI mismatch)

This condition is indicated by a system log similar to the one shown below.

Linux version 2.6.16.33-xenU (root@dom0-0-50-45-1-a4-ee.z-2.aes0.internal) 
(gcc version 4.1.1 20070105 (Red Hat 4.1.1-52)) #2 SMP Wed Aug 15 17:27:36 SAST 2007
...
FATAL: kernel too old
Kernel panic - not syncing: Attempted to kill init!
Potential Causes

Incompatible kernel and userland

Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the instance.
Modify the configuration to use a newer kernel.
Start the instance.
Instance store-backed
Use the following procedure:

Create an AMI that uses a newer kernel.
Terminate the instance.
Start a new instance from the AMI you created.
"FATAL: Could not load /lib/modules" or "BusyBox" (Missing kernel modules)

This condition is indicated by a system log similar to the one shown below.

[    0.370415] Freeing unused kernel memory: 1716k freed 
Loading, please wait...
WARNING: Couldn't open directory /lib/modules/2.6.34-4-virtual: No such file or directory
FATAL: Could not open /lib/modules/2.6.34-4-virtual/modules.dep.temp for writing: No such file or directory
FATAL: Could not load /lib/modules/2.6.34-4-virtual/modules.dep: No such file or directory
Couldn't get a file descriptor referring to the console
Begin: Loading essential drivers... ...
FATAL: Could not load /lib/modules/2.6.34-4-virtual/modules.dep: No such file or directory
FATAL: Could not load /lib/modules/2.6.34-4-virtual/modules.dep: No such file or directory
Done.
Begin: Running /scripts/init-premount ...
Done.
Begin: Mounting root file system... ...
Begin: Running /scripts/local-top ...
Done.
Begin: Waiting for root file system... ...
Done.
Gave up waiting for root device.  Common problems:
 - Boot args (cat /proc/cmdline)
   - Check rootdelay= (did the system wait long enough?)
   - Check root= (did the system wait for the right device?)
 - Missing modules (cat /proc/modules; ls /dev)
FATAL: Could not load /lib/modules/2.6.34-4-virtual/modules.dep: No such file or directory
FATAL: Could not load /lib/modules/2.6.34-4-virtual/modules.dep: No such file or directory
ALERT! /dev/sda1 does not exist. Dropping to a shell!


BusyBox v1.13.3 (Ubuntu 1:1.13.3-1ubuntu5) built-in shell (ash)
Enter 'help' for a list of built-in commands.

(initramfs)
Potential Causes

One or more of the following conditions can cause this problem:

Missing ramdisk
Missing correct modules from ramdisk
Amazon EBS root volume not correctly attached as /dev/sda1
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Select corrected ramdisk for the Amazon EBS volume.
Stop the instance.
Detach the volume and repair it.
Attach the volume to the instance.
Start the instance.
Modify the AMI to use the corrected ramdisk.
Instance store-backed
Use the following procedure:

Terminate the instance and launch a new instance with the correct ramdisk.
Create a new AMI with the correct ramdisk.
ERROR Invalid kernel (EC2 incompatible kernel)

This condition is indicated by a system log similar to the one shown below.

...
root (hd0)

 Filesystem type is ext2fs, using whole disk

kernel /vmlinuz root=/dev/sda1 ro

initrd /initrd.img

ERROR Invalid kernel: elf_xen_note_check: ERROR: Will only load images 
built for the generic loader or Linux images
xc_dom_parse_image returned -1

Error 9: Unknown boot failure

  Booting 'Fallback'
  
root (hd0)

 Filesystem type is ext2fs, using whole disk

kernel /vmlinuz.old root=/dev/sda1 ro

Error 15: File not found
Potential Causes

One or both of the following conditions can cause this problem:

Supplied kernel is not supported by GRUB
Fallback kernel does not exist
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the instance.
Replace with working kernel.
Install a fallback kernel.
Modify the AMI by correcting the kernel.
Instance store-backed
Use the following procedure:

Terminate the instance and launch a new instance with the correct kernel.
Create an AMI with the correct kernel.
(Optional) Seek technical assistance for data recovery using AWS Support.
request_module: runaway loop modprobe (Looping legacy kernel modprobe on older Linux versions)

This condition is indicated by a system log similar to the one shown below. Using an unstable or old Linux kernel (for example, 2.6.16-xenU) can cause an interminable loop condition at startup.

Linux version 2.6.16-xenU (builder@xenbat.amazonsa) (gcc version 4.0.1 
20050727 (Red Hat 4.0.1-5)) #1 SMP Mon May 28 03:41:49 SAST 2007

BIOS-provided physical RAM map:

 Xen: 0000000000000000 - 0000000026700000 (usable)

0MB HIGHMEM available.
...

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c

request_module: runaway loop modprobe binfmt-464c
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use a newer kernel, either GRUB-based or static, using one of the following options:

Option 1: Terminate the instance and launch a new instance, specifying the –kernel and –ramdisk parameters.

Option 2:

Stop the instance.
Modify the kernel and ramdisk attributes to use a newer kernel.
Start the instance.
Instance store-backed
Terminate the instance and launch a new instance, specifying the –kernel and –ramdisk parameters.
fsck: No such file or directory while trying to open... (File system not found)

This condition is indicated by a system log similar to the one shown below.

		Welcome to Fedora 
		Press 'I' to enter interactive startup.
Setting clock : Wed Oct 26 05:52:05 EDT 2011 [  OK  ]

Starting udev: [  OK  ]

Setting hostname localhost:  [  OK  ]

No devices found
Setting up Logical Volume Management: File descriptor 7 left open
  No volume groups found
[  OK  ]

Checking filesystems
Checking all file systems.
[/sbin/fsck.ext3 (1) -- /] fsck.ext3 -a /dev/sda1 
/dev/sda1: clean, 82081/1310720 files, 2141116/2621440 blocks
[/sbin/fsck.ext3 (1) -- /mnt/dbbackups] fsck.ext3 -a /dev/sdh 
fsck.ext3: No such file or directory while trying to open /dev/sdh

/dev/sdh: 
The superblock could not be read or does not describe a correct ext2
filesystem.  If the device is valid and it really contains an ext2
filesystem (and not swap or ufs or something else), then the superblock
is corrupt, and you might try running e2fsck with an alternate superblock:
    e2fsck -b 8193 <device>

[FAILED]


*** An error occurred during the file system check.
*** Dropping you to a shell; the system will reboot
*** when you leave the shell.
Give root password for maintenance
(or type Control-D to continue):
Potential Causes

A bug exists in ramdisk filesystem definitions /etc/fstab
Misconfigured filesystem definitions in /etc/fstab
Missing/failed drive
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the instance, detach the root volume, repair/modify /etc/fstab the volume, attach the volume to the instance, and start the instance.
Fix ramdisk to include modified /etc/fstab (if applicable).
Modify the AMI to use a newer ramdisk.
The sixth field in the fstab defines availability requirements of the mount – a nonzero value implies that an fsck will be done on that volume and must succeed. Using this field can be problematic in Amazon EC2 because a failure typically results in an interactive console prompt which is not currently available in Amazon EC2. Use care with this feature and read the Linux man page for fstab.
Instance store-backed
Use the following procedure:

Terminate the instance and launch a new instance.
Detach any errant Amazon EBS volumes and the reboot instance.
(Optional) Seek technical assistance for data recovery using AWS Support.
General error mounting filesystems (Failed mount)

This condition is indicated by a system log similar to the one shown below.

Loading xenblk.ko module 
xen-vbd: registered block device major 8

Loading ehci-hcd.ko module
Loading ohci-hcd.ko module
Loading uhci-hcd.ko module
USB Universal Host Controller Interface driver v3.0

Loading mbcache.ko module
Loading jbd.ko module
Loading ext3.ko module
Creating root device.
Mounting root filesystem.
kjournald starting.  Commit interval 5 seconds

EXT3-fs: mounted filesystem with ordered data mode.

Setting up other filesystems.
Setting up new root fs
no fstab.sys, mounting internal defaults
Switching to new root and running init.
unmounting old /dev
unmounting old /proc
unmounting old /sys
mountall:/proc: unable to mount: Device or resource busy
mountall:/proc/self/mountinfo: No such file or directory
mountall: root filesystem isn't mounted
init: mountall main process (221) terminated with status 1

General error mounting filesystems.
A maintenance shell will now be started.
CONTROL-D will terminate this shell and re-try.
Press enter for maintenance
(or type Control-D to continue):
Potential Causes

Instance type	Potential cause
Amazon EBS-backed
Detached or failed Amazon EBS volume.
Corrupted filesystem.
Mismatched ramdisk and AMI combination (e.g., Debian ramdisk with a SUSE AMI).
Instance store-backed
A failed drive.
A corrupted file system.
A mismatched ramdisk and combination (for example, a Debian ramdisk with a SUSE AMI).
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the instance.
Detach the root volume.
Attach the root volume to a known working instance.
Run filesystem check (fsck –a /dev/...).
Fix any errors.
Detach the volume from the known working instance.
Attach the volume to the stopped instance.
Start the instance.
Recheck the instance status.
Instance store-backed
Try one of the following:

Start a new instance.
(Optional) Seek technical assistance for data recovery using AWS Support.
VFS: Unable to mount root fs on unknown-block (Root filesystem mismatch)

This condition is indicated by a system log similar to the one shown below.

Linux version 2.6.16-xenU (builder@xenbat.amazonsa) (gcc version 4.0.1 
 20050727 (Red Hat 4.0.1-5)) #1 SMP Mon May 28 03:41:49 SAST 2007
...
Kernel command line:  root=/dev/sda1 ro 4
...
Registering block device major 8
...
Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block(8,1)
Potential Causes

Instance type	Potential cause
Amazon EBS-backed
Device not attached correctly.
Root device not attached at correct device point.
Filesystem not in expected format.
Use of legacy kernel (e.g., 2.6.16-XenU).
A recent kernel update on your instance (faulty update, or an update bug)
Instance store-backed
Hardware device failure.
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Do one of the following:

Stop and then restart the instance.
Modify root volume to attach at the correct device point, possible /dev/sda1 instead of /dev/sda.
Stop and modify to use modern kernel.
Refer to the documentation for your Linux distribution to check for known update bugs. Change or reinstall the kernel.
Instance store-backed
Terminate the instance and launch a new instance using a modern kernel.
Error: Unable to determine major/minor number of root device... (Root file system/device mismatch)

This condition is indicated by a system log similar to the one shown below.

...
XENBUS: Device with no driver: device/vif/0
XENBUS: Device with no driver: device/vbd/2048
drivers/rtc/hctosys.c: unable to open rtc device (rtc0)
Initializing network drop monitor service
Freeing unused kernel memory: 508k freed
:: Starting udevd...
done.
:: Running Hook [udev]
:: Triggering uevents...<30>udevd[65]: starting version 173
done.
Waiting 10 seconds for device /dev/xvda1 ...
Root device '/dev/xvda1' doesn't exist. Attempting to create it.
ERROR: Unable to determine major/minor number of root device '/dev/xvda1'.
You are being dropped to a recovery shell
    Type 'exit' to try and continue booting
sh: can't access tty; job control turned off
[ramfs /]#
Potential Causes

Missing or incorrectly configured virtual block device driver
Device enumeration clash (sda versus xvda or sda instead of sda1)
Incorrect choice of instance kernel
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the instance.
Detach the volume.
Fix the device mapping problem.
Start the instance.
Modify the AMI to address device mapping issues.
Instance store-backed
Use the following procedure:

Create a new AMI with the appropriate fix (map block device correctly).
Terminate the instance and launch a new instance from the AMI you created.
XENBUS: Device with no driver...

This condition is indicated by a system log similar to the one shown below.

XENBUS: Device with no driver: device/vbd/2048
drivers/rtc/hctosys.c: unable to open rtc device (rtc0)
Initalizing network drop monitor service
Freeing unused kernel memory: 508k freed
:: Starting udevd...
done.
:: Running Hook [udev]
:: Triggering uevents...<30>udevd[65]: starting version 173
done.
Waiting 10 seconds for device /dev/xvda1 ...
Root device '/dev/xvda1' doesn't exist. Attempting to create it.
ERROR: Unable to determine major/minor number of root device '/dev/xvda1'.
You are being dropped to a recovery shell
    Type 'exit' to try and continue booting
sh: can't access tty; job control turned off
[ramfs /]#
Potential Causes

Missing or incorrectly configured virtual block device driver
Device enumeration clash (sda versus xvda)
Incorrect choice of instance kernel
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the instance.
Detach the volume.
Fix the device mapping problem.
Start the instance.
Modify the AMI to address device mapping issues.
Instance store-backed
Use the following procedure:

Create an AMI with the appropriate fix (map block device correctly).
Terminate the instance and launch a new instance using the AMI you created.
... days without being checked, check forced (File system check required)

This condition is indicated by a system log similar to the one shown below.

...
Checking filesystems
Checking all file systems.
[/sbin/fsck.ext3 (1) -- /] fsck.ext3 -a /dev/sda1 
/dev/sda1 has gone 361 days without being checked, check forced
Potential Causes

Filesystem check time passed; a filesystem check is being forced

Suggested Actions

Wait until the filesystem check completes. Note that a filesystem check can take a long time depending on the size of the root filesystem.
Modify your filesystems to remove the filesystem check (fsck) enforcement using tune2fs or tools appropriate for your filesystem.
fsck died with exit status... (Missing device)

This condition is indicated by a system log similar to the one shown below.

Cleaning up ifupdown....
Loading kernel modules...done.
...
Activating lvm and md swap...done.
Checking file systems...fsck from util-linux-ng 2.16.2
/sbin/fsck.xfs: /dev/sdh does not exist
fsck died with exit status 8
[31mfailed (code 8).[39;49m
Potential Causes

Ramdisk looking for missing drive
Filesystem consistency check forced
Drive failed or detached
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Try one or more of the following to resolve the issue:

Stop the instance, attach the volume to an existing running instance.
Manually run consistency checks.
Fix ramdisk to include relevant utilities.
Modify filesystem tuning parameters to remove consistency requirements (not recommended).
Instance store-backed
Try one or more of the following to resolve the issue:

Rebundle ramdisk with correct tooling.
Modify file system tuning parameters to remove consistency requirements (not recommended).
Terminate the instance and launch a new instance.
(Optional) Seek technical assistance for data recovery using AWS Support.
GRUB prompt (grubdom>)

This condition is indicated by a system log similar to the one shown below.

    GNU GRUB  version 0.97  (629760K lower / 0K upper memory)

       [ Minimal BASH-like line editing is supported.   For

         the   first   word,  TAB  lists  possible  command

         completions.  Anywhere else TAB lists the possible

         completions of a device/filename. ]

grubdom> 
Potential Causes

Instance type	Potential causes
Amazon EBS-backed
Missing GRUB configuration file.
Incorrect GRUB image used, expecting GRUB configuration file at a different location.
Unsupported filesystem used to store your GRUB configuration file (for example, converting your root file system to a type that is not supported by an earlier version of GRUB).
Instance store-backed
Missing GRUB configuration file.
Incorrect GRUB image used, expecting GRUB configuration file at a different location.
Unsupported filesystem used to store your GRUB configuration file (for example, converting your root file system to a type that is not supported by an earlier version of GRUB).
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Option 1: Modify the AMI and relaunch the instance:

Modify the source AMI to create a GRUB configuration file at the standard location (/boot/grub/menu.lst).
Verify that your version of GRUB supports the underlying file system type and upgrade GRUB if necessary.
Pick the appropriate GRUB image, (hd0-1st drive or hd00 – 1st drive, 1st partition).
Terminate the instance and launch a new one using the AMI the you created.
Option 2: Fix the existing instance:

Stop the instance.
Detach the root filesystem.
Attach the root filesystem to a known working instance.
Mount filesystem.
Create a GRUB configuration file.
Verify that your version of GRUB supports the underlying file system type and upgrade GRUB if necessary.
Detach filesystem.
Attach to the original instance.
Modify kernel attribute to use the appropriate GRUB image (1st disk or 1st partition on 1st disk).
Start the instance.
Instance store-backed
Option 1: Modify the AMI and relaunch the instance:

Create the new AMI with a GRUB configuration file at the standard location (/boot/grub/menu.lst).
Pick the appropriate GRUB image, (hd0-1st drive or hd00 – 1st drive, 1st partition).
Verify that your version of GRUB supports the underlying file system type and upgrade GRUB if necessary.
Terminate the instance and launch a new instance using the AMI you created.
Option 2: Terminate the instance and launch a new instance, specifying the correct kernel.

Note
To recover data from the existing instance, contact AWS Support.
Bringing up interface eth0: Device eth0 has different MAC address than expected, ignoring. (Hard-coded MAC address)

This condition is indicated by a system log similar to the one shown below.

... 
Bringing up loopback interface:  [  OK  ]

Bringing up interface eth0:  Device eth0 has different MAC address than expected, ignoring.
[FAILED]

Starting auditd: [  OK  ]
Potential Causes

There is a hard-coded interface MAC in the AMI configuration

Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Do one of the following:

Modify the AMI to remove the hard coding and relaunch the instance.
Modify the instance to remove the hard-coded MAC address.
OR

Use the following procedure:

Stop the instance.
Detach the root volume.
Attach the volume to another instance and modify the volume to remove the hard-coded MAC address.
Attach the volume to the original instance.
Start the instance.
Instance store-backed
Do one of the following:

Modify the instance to remove the hard-coded MAC address.
Terminate the instance and launch a new instance.
Unable to load SELinux Policy. Machine is in enforcing mode. Halting now. (SELinux misconfiguration)

This condition is indicated by a system log similar to the one shown below.

audit(1313445102.626:2): enforcing=1 old_enforcing=0 auid=4294967295
Unable to load SELinux Policy. Machine is in enforcing mode. Halting now.
Kernel panic - not syncing: Attempted to kill init!
Potential Causes

SELinux has been enabled in error:

Supplied kernel is not supported by GRUB
Fallback kernel does not exist
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Use the following procedure:

Stop the failed instance.
Detach the failed instance's root volume.
Attach the root volume to another running Linux instance (later referred to as a recovery instance).
Connect to the recovery instance and mount the failed instance's root volume.
Disable SELinux on the mounted root volume. This process varies across Linux distributions; for more information, consult your OS-specific documentation.

Note
On some systems, you disable SELinux by setting SELINUX=disabled in the /mount_point/etc/sysconfig/selinux file, where mount_point is the location that you mounted the volume on your recovery instance.
Unmount and detach the root volume from the recovery instance and reattach it to the original instance.
Start the instance.
Instance store-backed
Use the following procedure:

Terminate the instance and launch a new instance.
(Optional) Seek technical assistance for data recovery using AWS Support.
XENBUS: Timeout connecting to devices (Xenbus timeout)

This condition is indicated by a system log similar to the one shown below.

Linux version 2.6.16-xenU (builder@xenbat.amazonsa) (gcc version 4.0.1 
20050727 (Red Hat 4.0.1-5)) #1 SMP Mon May 28 03:41:49 SAST 2007
...
XENBUS: Timeout connecting to devices!
...
Kernel panic - not syncing: No init found.  Try passing init= option to kernel.
Potential Causes

The block device not is connected to the instance
This instance is using a very old instance kernel
Suggested Actions

For this instance type	Do this
Amazon EBS-backed
Do one of the following:

Modify the AMI and instance to use a modern kernel and relaunch the instance.
Reboot the instance.
Instance store-backed
Do one of the following:

Terminate the instance.
Modify the AMI to use a modern kernel, and launch a new instance using this AMI.

Troubleshooting Instance Capacity

The following errors are related to instance capacity.

Error: InsufficientInstanceCapacity

If you get an InsufficientInstanceCapacity error when you try to launch an instance or start a stopped instance, AWS does not currently have enough available capacity to service your request. Try the following:

Wait a few minutes and then submit your request again; capacity can shift frequently.
Submit a new request with a reduced number of instances. For example, if you're making a single request to launch 15 instances, try making 3 requests for 5 instances, or 15 requests for 1 instance instead.
If you're launching an instance, submit a new request without specifying an Availability Zone.
If you're launching an instance, submit a new request using a different instance type (which you can resize at a later stage). For more information, see Resizing Your Instance.
Try purchasing Reserved Instances. Reserved Instances are a long-term capacity reservation. For more information, see: Amazon EC2 Reserved Instances.
Error: InstanceLimitExceeded

If you get an InstanceLimitExceeded error when you try to launch an instance, you have reached your concurrent running instance limit. For new AWS accounts, the default limit is 20. If you need additional running instances, complete the form at Request to Increase Amazon EC2 Instance Limit.

Getting Console Output and Rebooting Instances

Console output is a valuable tool for problem diagnosis. It is especially useful for troubleshooting kernel problems and service configuration issues that could cause an instance to terminate or become unreachable before its SSH daemon can be started.

Similarly, the ability to reboot instances that are otherwise unreachable is valuable for both troubleshooting and general instance management.

EC2 instances do not have a physical monitor through which you can view their console output. They also lack physical controls that allow you to power up, reboot, or shut them down. Instead, you perform these tasks through the Amazon EC2 API and the command line interface (CLI).

Instance Reboot

Just as you can reset a computer by pressing the reset button, you can reset EC2 instances using the Amazon EC2 console, CLI, or API. For more information, see Reboot Your Instance.

Warning
For Windows instances, this operation performs a hard reboot that might result in data corruption.
Instance Console Output

For Linux/Unix instances, the instance console output displays the exact console output that would normally be displayed on a physical monitor attached to a computer. This output is buffered because the instance produces it and then posts it to a store where the instance's owner can retrieve it.

For Windows instances, the instance console output displays the last three system event log errors.

The posted output is not continuously updated; only when it is likely to be of the most value. This includes shortly after instance boot, after reboot, and when the instance terminates.

Note
Only the most recent 64 KB of posted output is stored, which is available for at least 1 hour after the last posting.
Only the instance owner can access the console output. You can retrieve the console output for your instances using the console or the command line.

To get console output using the console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the left navigation pane, choose Instances, and select the instance.

Choose Actions, Instance Settings, Get System Log.

To get console output using the command line

You can use one of the following commands. For more information about these command line interfaces, see Accessing Amazon EC2.

get-console-output (AWS CLI)
Get-EC2ConsoleOutput (AWS Tools for Windows PowerShell)
For more information about common system log errors, see Troubleshooting System Log Errors for Linux-Based Instances.

Capture a Screenshot of an Unreachable Instance

If you are unable to reach your instance via SSH or RDP, you can capture a screenshot of your instance and view it as an image. This provides visibility as to the status of the instance, and allows for quicker troubleshooting.

There is no data transfer cost for this screenshot. The image is generated in JPG format, no larger than 100kb.

To access the instance console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the left navigation pane, choose Instances.

Select the instance to capture.

Choose Actions, Instance Settings.

Choose Get Instance Screenshot.

Right-click on the image to download and save it.

To capture a screenshot using the command line

You can use one of the following commands. The returned content is base64-encoded. For more information about these command line interfaces, see Accessing Amazon EC2.

get-console-screenshot (AWS CLI)
GetConsoleScreenshot (Amazon EC2 Query API)
Instance Recovery When a Host Computer Fails

If there is an unrecoverable issue with the hardware of an underlying host computer, AWS may schedule an instance stop event. You'll be notified of such an event ahead of time by email.

To recover an Amazon EBS-backed instance running on a host computer that failed

Back up any important data on your instance store volumes to Amazon EBS or Amazon S3.

Stop the instance.

Start the instance.

Restore any important data.

[EC2-Classic] If the instance had an associated Elastic IP address, you must reassociate it with the instance.

For more information, see Stop and Start Your Instance.

To recover an instance store-backed instance running on a host computer that failed

Create an AMI from the instance.

Upload the image to Amazon S3.

Back up important data to Amazon EBS or Amazon S3.

Terminate the instance.

Launch a new instance from the AMI.

Restore any important data to the new instance.

[EC2-Classic] If the original instance had an associated Elastic IP address, you must associate it with the new instance.

For more information, see Creating an Instance Store-Backed Linux AMI.

My Instance is Booting from the Wrong Volume

In some situations, you may find that a volume other than the volume attached to /dev/xvda or /dev/sda has become the root volume of your instance. This can happen when you have attached the root volume of another instance, or a volume created from the snapshot of a root volume, to an instance with an existing root volume.

This is due to how the initial ramdisk in Linux works. It will choose the volume defined as / in the /etc/fstab, and in some distributions, including Amazon Linux, this is determined by the label attached to the volume partition. Specifically, you will find that your /etc/fstab looks something like the following:

LABEL=/ / ext4 defaults,noatime 1 1 
tmpfs /dev/shm tmpfs defaults 0 0 
devpts /dev/pts devpts gid=5,mode=620 0 0 
sysfs /sys sysfs defaults 0 0 
proc /proc proc defaults 0 0
And if you were to check the label of both volumes, you would see that they both contain the / label:

Copy
[ec2-user ~]$ sudo e2label /dev/xvda1 
/ 
[ec2-user ~]$ sudo e2label /dev/xvdf1 
/
In this example, you could end up having /dev/xvdf1 become the root device that your instance boots to after the initial ramdisk runs, instead of the /dev/xvda1 volume you had intended to boot from. Solving this is fairly simple; you can use the same e2label command to change the label of the attached volume that you do not want to boot from.

In some cases, specifying a UUID in /etc/fstab can resolve this, however, if both volumes come from the same snapshot, or the secondary is created from a snapshot of the primary volume, they will share a UUID.

Copy
[ec2-user ~]$ sudo blkid 
/dev/xvda1: LABEL="/" UUID=73947a77-ddbe-4dc7-bd8f-3fe0bc840778 TYPE="ext4" PARTLABEL="Linux" PARTUUID=d55925ee-72c8-41e7-b514-7084e28f7334 
/dev/xvdf1: LABEL="old/" UUID=73947a77-ddbe-4dc7-bd8f-3fe0bc840778 TYPE="ext4" PARTLABEL="Linux" PARTUUID=d55925ee-72c8-41e7-b514-7084e28f7334
To change the label of an attached volume

Use the e2label command to change the label of the volume to something other than /.

Copy
[ec2-user ~]$ sudo e2label /dev/xvdf1 old/ 
Verify that the volume has the new label.

Copy
[ec2-user ~]$ sudo e2label /dev/xvdf1 
old/
After making this change, you should be able to reboot the instance and have the proper volume selected by the initial ramdisk when the instance boots.

Important
If you intend to detach the volume with the new label and return it to another instance to use as the root volume, you must perform the above procedure again and change the volume label back to its original value; otherwise, the other instance will not boot because the ramdisk will be unable to find the volume with the label /.

