Using EC2Rescue for Linux

EC2Rescue for Linux is an easy-to-use tool that you can run on an Amazon EC2 Linux instance to diagnose and troubleshoot possible problems. It is valuable for collecting log files, troubleshooting issues, and proactively searching for possible areas of concern. It can even examine Amazon EBS root volumes from other instances and collect relevant logs for troubleshooting Linux instances using that volume.

Note
If you are using a Windows instance, see EC2Rescue for Windows Server.
Contents

Installing EC2Rescue for Linux
Working with EC2Rescue for Linux
Developing EC2Rescue Modules

Installing EC2Rescue for Linux

The EC2Rescue for Linux tool can be installed on an Amazon EC2 Linux instance that meets the following prerequisites.

Prerequisites

Supported operating systems:
Amazon Linux 2016.09+
SLES 12+
RHEL 7+
Ubuntu 16.04+
Software requirements:
Python 2.7.9+ or 3.2+
Note
For instances with earlier versions of Python installed, there is a binary version of the EC2Rescue for Linux that you can use. This version is supported on a best effort basis. The binary version of EC2Rescue for Linux requires glibc >= 2.5 and zlib >= 1.2.3.
To install EC2Rescue for Linux

From a working Linux instance, download the EC2Rescue for Linux tool:

Copy
[ec2-user ~]$ wget https://s3.amazonaws.com/ec2rescuelinux/ec2rl.tgz
Unpack the tarball:

Copy
[ec2-user ~]$ tar -xvf ec2rl.tgz
Verify the installation by listing out the help file:

Copy
[ec2-user ~]$ cd ec2rl
[ec2-user ~]$ ./ec2rl help

Working with EC2Rescue for Linux

The following are common tasks to get you started using this tool.

Topics

Getting Help
Running a Module
Uploading the Results
Creating Backups
Getting Help

EC2Rescue for Linux includes a help file that gives you information and syntax for each available command.

To use the help command

Use the help command to get general help:

Copy
[ec2-user ~]$ ./ec2rl help
To list the available modules

List all available modules:

Copy
[ec2-user ~]$ ./ec2rl list
To get help for a specific module

List the help details for a specific command:

Copy
[ec2-user ~]$ ./ec2rl help module_name
Example command for showing the help file for the dig module:

Copy
[ec2-user ~]$ ./ec2rl help dig
Running a Module

You can run an EC2Rescue for Linux using these steps.

To run a module

Run a module:

Copy
[ec2-user ~]$ ./ec2rl run --only-modules=module_name --arguments
Example command, using the dig module to query the amazon.com domain:

[ec2-user ~]$ ./ec2rl run --only-modules=dig --domain=amazon.com
View the results:

Copy
[ec2-user ~]$ cat /var/tmp/awsDiag/logfile_location
Example:

Copy
[ec2-user ~]$ cat /var/tmp/awsDiag/2017-05-11T15_39_21.893145/mod_out/run/dig.log
Uploading the Results

If AWS Support has requested the results or to share the results from an S3 bucket, upload using the EC2Rescue for Linux CLI tool. The output of the EC2Rescue for Linux commands should provide the commands to achieve this.

To upload to support

Upload the results to support:

Copy
[ec2-user ~]$ ./ec2rl upload --upload-directory=/var/tmp/awsDiag/2017-05-11T15_39_21.893145 --support-url="URLProvidedByAWSSupport"
To upload to an S3 bucket

To upload the results to an S3 bucket:

Copy
[ec2-user ~]$ ./ec2rl upload --upload-directory=/var/tmp/awsDiag/2017-05-11T15_39_21.893145 --presigned-url="YourPresignedS3URL"
Note
For more information about generating presigned URLs for Amazon S3, see Uploading Objects Using Pre-Signed URLs.
Creating Backups

Create a backup for your instance, one or more volumes, or a specific device ID using the following commands.

To back up an instance

Create a backup of your instance:

Copy
[ec2-user ~]$ ./ec2rl run --backup=ami
To back up all volumes

Create a backup of all volumes associated with the instance:

Copy
[ec2-user ~]$ ./ec2rl run --backup=allvolumes
To back up a volume

Create a backup of a single volume:

Copy
[ec2-user ~]$ ./ec2rl run --backup=volume ID

Developing EC2Rescue Modules

Modules are written in YAML, a data serialization standard. A module's YAML file consists of a single document, representing the module and its attributes.

Adding Module Attributes

The following table lists the available module attributes.


Attribute

Description

name
The name of the module. The name should be less than or equal to 18 characters in length.
version
The version number of the module.
title
A short, descriptive title for the module. This value should be less than or equal to 50 characters in length.
helptext
The extended description of the module. Each line should be less than or equal to 75 characters in length. If the module consumes arguments, required or optional, include them in the helptext value.

For example:

Copy
helptext: !!str |
  Collect output from ps for system analysis
  Consumes --times= for number of times to repeat
  Consumes --period= for time period between repetition
placement
The stage in which the module should be run. Supported values:

prediagnostic
run
postdiagnostic
language
The language that the module code is written in. Supported values:

bash
python
Note
Python code must be compatible with both Python 2.7.9+ and Python 3.2+.
content
The entirety of the script code.
constraint
The name of the object containing the constraint values.
domain
A descriptor of how the module is grouped or classified. The set of included modules uses the following domains:

application
net
os
performance
class
A descriptor of the type of task performed by the module. The set of included modules uses the following classes:

collect (collects output from programs)
diagnose (pass/fail based on a set of criteria)
gather (copies files and writes to specific file)
distro
The list of Linux distributions that this module supports. The set of included modules use the following distributions:

alami (Amazon Linux)
rhel
ubuntu
suse
required
The required arguments that the module is consuming from the CLI options.
optional
The optional arguments that the module can use.
software
The software executables used in the module. This attribute is intended to specify software that is not installed by default. The EC2Rescue for Linux logic ensures that these programs are present and executable before running the module.
package
The source software package for an executable. This attribute is intended to provide extended details on the package with the software, including a URL for downloading or getting further information.
sudo
Indicates whether root access is required to run the module.

You do not need to implement sudo checks in the module script. If the value is true, then the EC2Rescue for Linux logic only runs the module when the executing user has root access.
perfimpact
Indicates whether the module can have significant performance impact upon the environment in which it is run. If the value is true and the --perfimpact=true argument is not present, then the module is skipped.
parallelexclusive
Specifies a program that requires mutual exclusivity. For example, all modules specifying "bpf" run in a serial manner.
Adding Environment Variables

The following table lists the available environment variables.


Environment Variable	Description
EC2RL_WORKDIR
The main tmp directory for the diagnostic tool.
Default value: /var/tmp/awsDiag.
EC2RL_RUNDIR
The directory where all output is stored.

Default value: /var/tmp/awsDiag/<date&timestamp>.
EC2RL_GATHEREDDIR
The root directory for placing gathered module data.

Default value:/var/tmp/awsDiag/<date&timestamp>/mod_out/gathered/.
EC2RL_NET_DRIVER
The driver in use for the first, alphabetically ordered, non-virtual network interface on the instance.

Examples:

xen_netfront
ixgbevf
ena
EC2RL_SUDO
True if EC2Rescue for Linux is running as root; otherwise, false.
EC2RL_VIRT_TYPE
The virtualization type as provided by the instance metadata.

Examples:

default-hvm
default-paravirtual
EC2RL_INTERFACES
An enumerated list of interfaces on the system. The value is a string containing names, such as eth0, eth1, etc. This is generated via the functions.bash and is only available for modules that have sourced it.
Using YAML Syntax

The following should be noted when constructing your module YAML files:

The triple hyphen (---) denotes the explicit start of a document.
The !ec2rlcore.module.Module tag tells the YAML parser which constructor to call when creating the object from the data stream. You can find the constructor inside the module.py file.
The !!str tag tells the YAML parser to not attempt to determine the type of data, and instead interpret the content as a string literal.
The pipe character (|) tells the YAML parser that the value is a literal-style scalar. In this case, the parser includes all whitespace. This is important for modules because indentation and newline characters are kept.
The YAML standard indent is two spaces, which can be seen in the following examples. Ensure that you maintain standard indentation (for example, four spaces for Python) for your script and then indent the entire content two spaces inside the module file.
Example Modules

Example one (mod.d/ps.yaml):

Copy
--- !ec2rlcore.module.Module
# Module document. Translates directly into an almost-complete Module object
name: !!str ps
path: !!str
version: !!str 1.0
title: !!str Collect output from ps for system analysis
helptext: !!str |
  Collect output from ps for system analysis
  Requires --times= for number of times to repeat
  Requires --period= for time period between repetition
placement: !!str run
package: 
  - !!str
language: !!str bash
content: !!str |
  #!/bin/bash
  error_trap()
  {
      printf "%0.s=" {1..80}
      echo -e "\nERROR:	"$BASH_COMMAND" exited with an error on line ${BASH_LINENO[0]}"
      exit 0
  }
  trap error_trap ERR

  # read-in shared function
  source functions.bash
  echo "I will collect ps output from this $EC2RL_DISTRO box for $times times every $period seconds."
  for i in $(seq 1 $times); do
      ps auxww
      sleep $period
  done
constraint:
  requires_ec2: !!str False
  domain: !!str performance
  class: !!str collect
  distro: !!str alami ubuntu rhel suse
  required: !!str period times
  optional: !!str
  software: !!str
  sudo: !!str False
  perfimpact: !!str False
  parallelexclusive: !!str

  