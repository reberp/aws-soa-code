# Links

* Courses:
	* https://digitalu.udemy.com/course/aws-certified-sysops-administrator-associate-training/
	    * The main course and the one the code came from. 
	    * From what I can tell of practice tests so far, the course is probably more tailored to the exam labs that don't exist anymore, and not tailored enough to detailing specifics about the nuance of some of the services. 
	* https://digitalu.udemy.com/course/ultimate-aws-certified-sysops-administrator-associate/learn/lecture/27512496#overview
		* This one is probably more comprehensive since it's twice the length, but I didn't do it. If I study for it again, probable do a bunch of tests so I know what to learn, then by the time I complete the course I won't remember the test questions but I hopefully focused on the important points. 
* Practice Tests:
  1. https://digitalu.udemy.com/course/aws-certified-sysops-administrator-associate-aws-practice-exams
  2. https://digitalu.udemy.com/course/practice-exams-aws-certified-sysops-administrator-associate
  3. Main course has a practice test
  4. Maybe (it's getting expired soon): https://digitalu.udemy.com/course/aws-sysops-admin-associate-3-full-practice-tests/
* Study guides:
	* https://digitalcloud.training/aws-cheat-sheets/#Services?megamenu
		* This has super helpful overviews for each service

# Notes
Hoping to note out some main study points that I realize I don't know from the practice tests that are much harder than the course content.
Goal is a study guide for things I didn't learn enough of to go back and read more on later. 

Noted: 
* 1.1,5
* 2.1-3  

Score:  
* 2.1: 41, 4 Jan
* 2.2: 60, 5 Jan
* 2.3: 63, 5 Jan
* 1.1: 81, 6 Jan (looks like same questions from the course, think I remembered some)
* 1.5: 60, 7 Jan



* ASG
  * Scale-in (protection) - making it smaller (but doesn't delete any)
  * may terminate instances that are stopped, pause if you are updating an instance
  * launch process can get suspended 
  * Can terminate instances with DisableApiTermination, need instance protection or to suspend ReplaceUnhealthy
  * Launch configuration cannot be updated, only replaced

* Artifact
	* AWS Artifact provides information about compliance of the AWS platform
	* provides on-demand downloads of AWS security and compliance documents

* Athena 
	* Analyze data where it's at (in S3)
	* serverless

* Aurora
	* managed database

* Backup
	* Centralized backup management for everything across accounts

* Beanstalk
  * Default scaling is based on network traffic (high or low)

* CloudFormation
  * Stack policy - defines what can be done on some resources to prevent unintentional updates, have to specify them explicitly
	  * Only applies during updates
  * Change set - show changes from last deployed set, deleted after successful deployment
  * Stack set - act across multiple accounts and regions
  * Resource Import - bring in things you already have
  * Export to send to another stack, ImportValue to bring in

* CloudFront
	* Configure log files to contain every request info
	* TotalErrorRate to see everything wrong 
	* Remove quickly - invalidate the file then serve a new file
	* caches for 24 hrs
	* Use custom origin or origin access identity to require it's use for s3
	* Errors if you move buckets from one region to another, have to update the CF distribution
	* Signed URLs for ensuring only certain people can access
		* Signed URLs created with CF Key Pairs
	* If it goes to a website s3, can't be https to bucket

* CloudTrail
	* Track API activities made by console, CLI, CF, etc. 
	* Can track federated users 

* CloudWatch
  * Can have two config files - different file names
  * Events
	  * Used for state changes
	  * do things on a schedule
  * Synthetics - Creates canaries - scripts that run on a schedule to monitor endpoints and APIs
  * ServiceLens - enhances observaibility by integrating traces, metrics, logs, alarms
  * Metrics:
	* Basic monitoring is 5 minutes, detailed is 1 minute
	* Filter things based on name
    * Bandwidth: NetworkIn, NetworkOut
    * Disk Use: DiskReadBytes, DiskWriteBytes
    * Status: StatusCheckFailed is combination of StatusCheckFailed_Instance and StatusCheckFailed_System
    * CPUUtilization
    * Custom: StatsD for L/W, CollectD for L
    * Custom metrics via CLI or API
    * Alarm
	    * automatic actions on EC2
	* Agent
	    * CloudWatchAgentServerRole - IAM role for EC2 instances
	    * Custom metrics via CLI or API
	    * Agent
		    * Preinstalled on some AMIs, can be installed
		* Events - do things on a schedule
			* e.x.: snapshot EBS
		* Synthetics - Creates canaries - scripts that run on a schedule to monitor endpoints and APIs
		* ServiceLens - enhances observaibility by integrating traces, metrics, logs, alarms

* Config
	* keeps track of configuration and relationships to other resources and evaluates for compliance
	* Auto Remediation to fix things that aren't right
	* discover existing AWS resources, export a complete inventory of your AWS resources with all configuration details, and determine how a resource was configured at any point in time.

* EBS
	* Consistency check for impaired storage
	* Expand with elastic volumes
	* Increasing size gives more I/O credits for performance

* EC2
  * DisableApiTermination: stops termination from API, CLI, UI
  * Detailed monitoring for 1 minute logs to CW
  * Health checks cover the instance, not any applications 
  * Status checks can not be disabled
  * T2 unlimited - CPU better for longer
  * Enhanced Networking - many packets per second
  * Cluster placement group - fast inter-ec2 networking
  * Dedicated instances are normal instances but hardware separated per customer, dedicated host gives full host
  * Instance Profile - gives IAM role information to instance
  * EC2Rescue - help resolve windows OS level issues 

* ELB
  * 503 if no registered targets
  * routes to unhealthy if there are no healthy
  * Cloudtrail logs capture all API calls, including IP, who/when, etc.
  * NLB is best for high throughput
  * ALB Access logs include IP address, latencies, paths, responses

* Encryption
	* SSE-C - encryption in AWS by customer key 
	* SSE-S3 - encryption with S3 managed keys, everything keys a different key that is encrypted with the master key
	* SSE-CMK - like S3 but additional logging and permissions

* EventBridge
	* Something happends, send trigger to something else (Lambda, SNS, etc)
		  * Sending to Kinesis - requires IAM role
		  * Sending to anything else - configure resource-based policy 

* Gateways
	* Volume - iSCSI
	* Egress Only Internet Gateway - IPv6

* IAM
  * Resources must be globally unique named
  * Policies
	  * identity based apply to user, group role
	  * resource based apply to things, buckets, keys, etc.
	  * to access things cross-account: need identify based on user, and resource based on object
	  * Any explicit deny overrides any allow
	  * Password policies to force changes
	  * Access keys can't be expired via policy 

* Inspector
	* security assessment service
	* check security state 

* Lambda
  * Not self-invoking

* Trusted Advisor
  * monitor against service limints
  * monitor for best practices
  * provides you real time guidance to help you provision your resources following AWS best practices
  * reduce cost, increase performance, and improve security by optimizing your AWS environment.

* S3
	* Delete marker - versioned object marked deleted, not actually gone
	* Replication Time Control - notice when replication fails
	* Versions can have different retention periods
	* Storage options:
		* have to be in for 30 days before going to IA

* Secrets Manager
	* Supports automatic rotation

* Site to site
	* direct connect - physical
	* The rest - can be software VPNs

* Shield
	* DDoS protection

* Systems Manager
	* Collect metadata about instances 
	* AWSSupport-TroubleshootS3PublicRead automation document to help fix public S3 issues
	* Automation document to update automate common and repetitive IT operations and management tasks across AWS resources

* RDS
	* parameter groups to enforce SSL
	* Multi-AZ is HA
	* Enhanced monitoring: 1.Free Memory 2.Active Memory 3.Swap Free 4.Processes Running 5.File System Used
		* OS level metrics not part of standard cloudwatch 
	* Read replicas are asynchronous on change to dB, Multi-AZ is synchronous
	* Upgrade - snapshot existing and create new then upgrade and test 
	* Only ever one writable node
	* 

* Route 53
	* Alias - special record to map an apex to an ELB DNS (only one since you can't CNAME the apex)

* AWS Redshift
	* Data warehouse in PQL to analyze data you put into it

* Accidental deleting
  * AMI - can't be recovered, only remade

* Volumes
	* EBS
		* separate OS and data best practice
		* root can be encrypted
		* HDDs are good for throughput, not IOPS and can't be used for boot volumes

* VPC/Subnet
	* NACL - firewall at subnet level
		* Default allow all
		* stateless
	* Flow logs - can't be updated, only recreated, take a few minutes

* X-Ray
	* helps trace app workflows, integrated with S3, ELB, Lambda, APIs. Not ALB. 

* WAF
	* Only in front of CF, ALB, API Gateway
	* Manage rate limits 