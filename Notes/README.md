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
  5. https://d1.awsstatic.com/training-and-certification/docs-sysops-associate/AWS-Certified-SysOps-Administrator-Associate_Sample-Questions.pdf
  6. Practice question set: https://explore.skillbuilder.aws/learn/course/external/view/elearning/12485/aws-certified-sysops-administrator-associate-practice-question-set-soa-c02-english?syops=sec&sec=prep
  7. https://explore.skillbuilder.aws/learn/course/9457/play/32355/benchmark-assessment
  8. skillbuilder test (course test and separate test course are same?) https://explore.skillbuilder.aws/learn/mycourses
* Study guides:
	* https://digitalcloud.training/category/aws-cheat-sheets/aws-sysops-administrator-associate/
		* This has super helpful overviews for each service
	* Exam scenarios from digitalcloud.training: https://digitalcloud.training/aws-sysops-administrator-exam-scenarios/

# Notes
Hoping to note out some main study points that I realize I don't know from the practice tests that are much harder than the course content.
Goal is a study guide for things I didn't learn enough of to go back and read more on later. 

| Item | Score | Date | \#Q | Note |
| ---- | ---- | ---- | ---- | ---- |
| C.1 | - | - | 65 | Forgot to note |
| C.2 | - | - | 65 |  |
| C.3 | - | - | 65 |  |
| 2.1 | 41 | 4 | 65 |  |
| 2.2 | 60 | 5 | 65 |  |
| 2.3 | 63 | 5 | 65 |  |
| 1.1 | 81 | 6 | 65 | remembered some for sure |
| 1.5 | 60 | 7 | 65 |  |
| 2.4 | 43 | 7 | 65 |  |
| 5 | 55 | 7 | 8 |  |
| 1.2 | 80 | 8 | 65 | side-side > all at once |
| 1.4 | 72 | 8 | 65 |  |
| 6 | 65 | 8 | 20 |  |
| 1.5 | 89 | 9 | 65 | no more retaking tests |
| 1.3 | 72 | 9 | 65 |  |
| 5 | 90 | 10 | 8 |  |
| 6 | 90 | 10 | 20 |  |
| 7 | 60 | 10 | 40 | wrong on multiple choice gives you negative points wtf? |
| 8 | 778 | 10 | 65 |  |

* ASG
  * Scale-in (protection) - making it smaller (but doesn't delete any)
  * may terminate instances that are stopped, pause if you are updating an instance
  * launch process can get suspended 
  * Can terminate instances with DisableApiTermination, need instance protection or to suspend ReplaceUnhealthy
  * Launch configuration cannot be updated, only replaced
  * Need a special role to access CMKs
  * Warm pool for things that take long to start. Not sure the cost point? 
  * 

* Artifact
	* AWS Artifact provides information about compliance of the AWS platform
	* provides on-demand downloads of AWS security and compliance documents

* Athena 
	* Analyze data where it's at (in S3)
	* serverless

* AWS Redshift
	* Data warehouse in PQL to analyze data you put into it

* Aurora
	* managed database

* Backup
	* Centralized backup management for everything across accounts
	* Use this if not just EBS instances (which is DLM)

* Beanstalk
  * Default scaling is based on network traffic (high or low)

* CloudFormation
  * Stack policy - defines what can be done on some resources to prevent unintentional updates, have to specify them explicitly
	  * Only applies during updates
  * Change set - show changes from last deployed set, deleted after successful deployment
  * Stack set - act across multiple accounts and regions
  * Resource Import - bring in things you already have
  * Export to send to another stack, ImportValue to bring in
  * UPDATE_ROLLBACK_FAILED can be corrected with continue update rollback 
  * autoscalingrollingupdate - can update instances in the ASG
  * autoscalingreplacingupdate - update the entire ASG at once
  * Drift detection is via config 

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
	* Management events - controlplane events - default. For events on resources in account
	* Data events - off by default - events performed on a resource 

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
    * Insight: search or analyze logs 
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
	* Can't enforce that people don't do non-compliant things 
	* discover existing AWS resources, export a complete inventory of your AWS resources with all configuration details, and determine how a resource was configured at any point in time.
	* two triggers: configuration and period triggers to run things on a schedule
	* Things can remain on console for a bit after deleting

* Control Tower
	* AWS Control Tower offers a straightforward way to set up and govern an AWS multi-account environment, following prescriptive best practices.
	* Extends AWS Organizations

* EBS
	* Consistency check for impaired storage
	* Expand with elastic volumes
	* Increasing size gives more I/O credits for performance
	* Initialize/Pre-warm it to make sure it works right away
	* Data Lifecycle Manager for snapshots 
	* Volumeread/writebyes (not diskread/write)

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
  * Traffic mirroring: ensure that target MTU is >= source MTU
  * Most metrics that aren't just based on status checks or CPU utilization require CW agent

* EFS
	* Access points - help manage application access to shared data. Enforce identity, user groups, etc. Can be combined with IAM 
	* Pay for what you use
	* many AZ
	* Burst throughput - scales as efs size scaled
	* Provisioned throughput - scales independently

* ELB
  * 503 if no registered targets
  * routes to unhealthy if there are no healthy
  * Cloudtrail logs capture all API calls, including IP, who/when, etc.
  * NLB is best for high throughput
  * ALB Access logs include IP address, latencies, paths, responses
  * Can't disable AZs after creation

* Encryption
	* SSE-C - encryption in AWS by customer key 
	* SSE-S3 - encryption with S3 managed keys, everything keys a different key that is encrypted with the master key
	* SSE-CMK - like S3 but additional logging and permissions
	* AES256 in policy = sses3
	* ACM - SSL certs only for HTTPS
	* AWS managed CMK - auto rotation, can't change
	* Customer managed CMK - can enable rotation

* EventBridge
	* Something happens, send trigger to something else (Lambda, SNS, etc)
		  * Sending to Kinesis - requires IAM role
		  * Send to SNS
		  * Sending to anything else - configure resource-based policy 

* Gateways
	* Volume - iSCSI
	* Egress Only Internet Gateway - IPv6
	* FSx Windows File Server - NTFS and SMB EFS
	* Cached vs stored volume gateway - only keep cached files local vs keeping all files local 

* IAM
  * Resources must be globally unique named
  * Policies
	  * identity based apply to user, group role
	  * resource based apply to things, buckets, keys, etc.
	  * to access things cross-account: need identify based on user, and resource based on object
	  * Any explicit deny overrides any allow
	  * Password policies to force changes
	  * Access keys can't be expired via policy 
	  * Users can be in multiple groups
	  * Groups can't be in other groups

* Inspector
	* security assessment service
	* check security state 
	* Assessment templates can do custom checks 
	* Agent has to be installed on instances 

* Lambda
  * Not self-invoking
  * default in a secure VPC, you can put into other othes

* Trusted Advisor
  * monitor against service limints
  * monitor for best practices
  * provides you real time guidance to help you provision your resources following AWS best practices
  * reduce cost, increase performance, and improve security by optimizing your AWS environment.

* S3
	* Delete marker - versioned object marked deleted, not actually gone
	* Replication Time Control - notice when replication fails
	* Versions can have different retention periods
	* Upload to another accounts bucket and you still retain rights unless you delegate them 
	* Storage options:
		* have to be in for 30 days before going to IA
	* Access points - manage access at scale for using shared datasets

* Secrets Manager
	* Supports automatic rotation for RDS, Redshift, DocumentDB

* Service Catalog
	* Create and manage catalogs of approved services . VMs, DBs, etc
	* End users can deploy approved things

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
	* Dynamo streams and Global table for HA
	* point in time recovery to undo write/delete
	* Redis shard = data partition

* Route 53
	* Alias - special record to map an apex to an ELB DNS (only one since you can't CNAME the apex)

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

* See this? Think that (should have started this earlier). There might be a lot of nuance to services, but there's also some big points and relationships they want to convey. 
	* Organizations - SCP
	* CF & Region - AMI mismatch
	* Subnet Access - ACL
	* Audit - artifact
	* DNS to LB/Cloudfront - Alias
	* Almost anything and need to encrypt what exists - recreate
	* Customer secure access - signed url
	* patch performance issues - 10% only
	* An answer that uses the services capabilites - probably that (vs a chain of others). 
	* Anything with private subnet - NAT gateway
